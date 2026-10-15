# OCOS — Reality check: the v1.0.0 design walked through five real situations

*Status: round 2, 2026-10-15. Written **before** the final rewrite, against the round-1 design (commit fad4232), to find where it breaks. Each scenario ends with "design changes required" (`DC-n.m`); section 6 lists where each change landed in the final documents. Section 7 is the adversarial review of the final documents.*
*Evidence ids (`F-nn`) refer to [RESEARCH.md](RESEARCH.md). Anything without an `F-nn` is the authors' inference.*

**Cast (the same in every scenario).** A mid-size general contractor builds a 6-storey residential block with its own structural crews and subcontracted MEP. *Karim*, site manager (*conducteur de travaux*), runs the site from their phone. *Youssef*, rebar foreman (*chef d'équipe ferraillage*). *Sara*, the planner, keeps the MS Project file and the Excel constraint list for the weekly site meeting. *Hicham*, the buyer, works from an Excel purchase register and the phone. *ElecPro*, the electrical subcontractor. *AcierSud*, the rebar supplier. The *maître d'œuvre* (architect and engineering office) and a *bureau de contrôle* represent the client side. Names and country are illustrative; the pilot market is open (`Q-01`).

---

## Scenario 1 — A slab pour is blocked by a late rebar delivery

### Today, without OCOS

1. Hicham ordered the level-3 slab rebar from AcierSud by phone and confirmed it by email; the promised date (Monday) is in their Excel register, nowhere else. (F-12, F-13)
2. Monday 10:00, Youssef posts in the site WhatsApp group: "lhdid ma jach" (Darija: "the steel hasn't come") with a photo of the empty bay. (F-09)
3. Karim sees it at 11:30 between two calls, phones Hicham, who phones AcierSud: "tomorrow morning". Nobody updates anything written.
4. The concrete order and pump for Thursday are in Karim's head and the batching plant's phone log. Tuesday the steel arrives at 14:00, fixing slips, the pre-pour inspection is moved by phone, and Thursday's pour is cancelled on Wednesday evening — the pump is paid anyway.
5. At Friday's meeting the reason recorded, if any, is "supplier late". (F-05, F-06)

### With the round-1 design

| Step | Input and channel | Becomes (primitive) | Who acts | Authority | Recorded |
|---|---|---|---|---|---|
| 1 | Excel purchase register imported weekly | `reported` assertions; commitment `promised` (AcierSud, Monday) linked to requirement "rebar on site" | integration | none | import events with row ids |
| 2 | Youssef's WhatsApp message | — round 1 has no defined path: messaging is optional (Q-14) | — | — | **nothing** |
| 3 | Monday 12:00 deadline + grace | commitment `missed` → requirement `unmet` → slab `not_ready`; `impact.assessed` | kernel, readiness engine | none | derived events |
| 4 | — | mission proposal to Hicham + 2 recovery options | coordinator agent | `choose` needs Karim | `shadow_action` (shadow) |
| 5 | Delivery note photo | evidence + `reported` assertion; verified by Karim | Karim via web form | verifier grant | requirement `met` |

### Where the design breaks

- **Missing input.** The most valuable fact (Youssef's message at 10:00) never reaches OCOS. Without a messaging path, OCOS learns of the miss only through a timer, and the weekly Excel import is too slow: the register may still say "Monday" on Wednesday.
- **Darija and photos.** The message is three words of Darija and a photo of an empty bay. Interpretation is the core AI job, not a side job (F-39), and the language is not covered.
- **Commitment granularity.** The purchase order has a date but no time; "Monday" for a supplier means "sometime Monday". The 12:00 grace rule produces false misses or late detections. Due *time* is often `unknown`.
- **Hidden commitments.** The concrete order and pump booking exist in nobody's file. The impact analysis can only list what OCOS knows; "concrete order at risk" is invisible unless someone records those bookings.
- **Friction for Karim.** In round 1 Karim must open a web form to verify the delivery note. They do it from the cab of their car, if at all.
- **Cost.** The pump cancellation fee is the money figure a director cares about; round 1 has no place to record it.

### Design changes required

- **DC-1.1** Messaging intake is core: every message, photo, voice note or file from the configured channel becomes an *intake item*; the AI proposes what it means; a person confirms.
- **DC-1.2** Due times can be a day or a window (`due_by` date with optional time); deadline rules use the configured end of working day when no time is given.
- **DC-1.3** The pilot domain pack must include the "service bookings" a pour needs (concrete order, pump, inspection booking) as requirements with their own commitments, even if they are only recorded from messages.
- **DC-1.4** Verification of routine evidence (delivery note) by the operator in a batch "confirm" list on the phone, not a separate form.
- **DC-1.5** Impact may carry a free-text cost note entered by a person (never computed by AI).

## Scenario 2 — A subcontractor misses a commitment; the foreman learns it at 7 am on WhatsApp

### Today

1. At Tuesday's site meeting ElecPro promised the cable sleeves in the level-2 slab formwork by Wednesday 17:00. Sara wrote it in the minutes (action list), sent as PDF on Thursday. (F-02, F-03)
2. Thursday 07:05, ElecPro's chief writes to Youssef on WhatsApp: "les gaines demain inchallah, manque de personnel" (sleeves tomorrow, short of staff).
3. Youssef forwards it to the site group; Karim reads it at 08:30 and has already started the rebar crew on level 2. Karim moves them to the stair core and phones ElecPro's manager. (F-09, F-14)
4. Nothing records that the promise was missed or that a new promise was made; next week's minutes repeat the action with a new date.

### With the round-1 design

| Step | Input and channel | Becomes | Who acts | Authority | Recorded |
|---|---|---|---|---|---|
| 1 | Minutes PDF | — round 1 has no import of minutes; Sara would type the commitment in a form | Sara | none | commitment `promised` |
| 2 | ElecPro's message (to Youssef, not to OCOS) | — not reachable | — | — | nothing |
| 3 | Wednesday 17:00 + grace | commitment `missed`; mission reminder to ElecPro (shadow) | kernel | escalation path | `missed`, `shadow_action` |
| 4 | Karim's decision to move the crew | `consequential resource change` → needs a `choose` decision in OCOS | Karim | grant | only if Karim records it |

### Where the design breaks

- **Double entry.** Sara will not type the meeting's 30 actions into OCOS after typing them into the minutes. The minutes (Word/Excel/PDF) are the commitment source.
- **Private channels.** ElecPro wrote to Youssef directly. OCOS can only see channels it is part of. Some facts will always arrive by phone call; OCOS must accept "Karim says ElecPro called" as a report by Karim.
- **Renegotiation.** "Demain inchallah" is a new, soft promise. Round 1 records a replacing commitment, which is right, but the AI must not turn "inchallah" into a firm date without the operator's confirmation. Commitment *firmness* is information the planners use.
- **Recording decisions after the fact.** Karim moved the crew at 08:35 by voice. Requiring an OCOS decision *before* a crew move is unrealistic; physical decisions happen on site. OCOS should record them afterwards as reported decisions, not block them.
- **Relationship.** An automatic reminder to ElecPro's chief from an unknown number would annoy and could be read as a formal notice (V-14). Round-1 Q-07 recommended reminders as the first autonomous action.

### Design changes required

- **DC-2.1** Import the weekly meeting's action list (Excel or the minutes' table) as commitments; AI may read a PDF/Word minutes table, with operator confirmation.
- **DC-2.2** Accept *second-hand reports* ("Karim reports ElecPro said…"): basis `reported`, actor Karim, original speaker named as source party.
- **DC-2.3** Commitment `firmness` (`firm`, `tentative`) set by the operator; tentative promises do not make a requirement `expected`.
- **DC-2.4** Decisions taken on site are recorded afterwards as `reported` decisions with their maker; OCOS never blocks physical work, it records and checks gates.
- **DC-2.5** Outbound messages to external parties start in `confirm` mode, are sent in the name of a named person of the contractor, carry a fixed footer that they are not a contractual notice, and each recipient can be marked "do not message".

## Scenario 3 — An inspection must pass before work continues

### Today

1. Before the level-2 pour, the rebar must be checked. Depending on the contract: the maître d'œuvre's engineer inspects (a hold point in the ITP, F-17), and the bureau de contrôle may visit and later issue an opinion to the client (F-18, F-19).
2. Karim books the visit by phone. The engineer comes Wednesday 16:00, says "OK, you can pour, fix the two chairs at the edge" and leaves. The written record (a signed inspection request or a line in the site book, F-19) arrives days later, or the observation appears in next week's minutes.
3. The bureau de contrôle's report, if any, goes to the client and reaches the contractor weeks later.

### With the round-1 design

| Step | Input | Becomes | Who acts | Authority | Recorded |
|---|---|---|---|---|---|
| 1 | Domain pack | requirement "pre-pour inspection passed", category `inspection`, mandatory (Q-06) | config | — | requirement |
| 2 | Karim's message "inspection OK" | `reported` assertion; gate stays closed until "the inspector's result is recorded by the person entitled to record it" | Karim | — | assertion |
| 3 | Inspector's signed record | evidence; verification by … the inspector? | — | the inspector has no OCOS account | — |

### Where the design breaks

- **The verifier is outside.** The person entitled to release a hold point is the maître d'œuvre's engineer or a third party, who will never log into the contractor's OCOS (F-18). Round 1 implicitly expects them to record the result.
- **Verbal release, written later.** Real practice: oral release on site, paper later. If OCOS keeps the gate closed until the signed paper arrives, the board says "not ready" while the slab is being poured — OCOS loses credibility on day one.
- **Hold vs witness.** Some inspections block (hold point), others do not (witness point, F-17). Round 1 has one "mandatory" flag.
- **Bureau de contrôle opinions** are reports to the client, often not a release condition for the contractor's next step at all; their "suspended" or "unfavourable" opinions matter later (insurance, acceptance).
- **Liability.** If OCOS shows "ready" because Karim reported a verbal OK, and the engineer later denies it, the trace must show exactly that: a verbal release reported by Karim, not a verified release.

### Design changes required

- **DC-3.1** Inspection requirements carry `gate_kind`: `hold_point` (blocks readiness until released) or `witness_point` (notification required, does not block).
- **DC-3.2** A hold point can be released in two steps: `release_reported` (by a named contractor person, e.g. "verbal release by the engineer at 16:00", which opens the gate only if the company configuration allows verbal releases for that inspection) and `release_evidenced` (the signed record is attached later). Missing written evidence after a configured delay opens an exception.
- **DC-3.3** External verifiers are recorded as named external parties; the contractor's operator records their decision with evidence. The *external* party is the decision authority in the trace; the operator is the recorder.
- **DC-3.4** Bureau de contrôle opinions (`favourable`, `unfavourable`, `suspended`) are recorded as external assertions with their document; an unfavourable or suspended opinion opens an exception; it is a gate only where the company configures it.

## Scenario 4 — Monthly progress is certified for payment and disputed

### Today

1. On the 25th, the contractor's quantity surveyor (*métreur*) prepares the monthly statement (projet de décompte / situation) from foremen's reports, site measurements and attachements (F-20, F-23).
2. The maître d'œuvre checks it within the contractual period, reduces the slab formwork line from 100 % to 80 % ("edge forms not complete on axis F"), and issues the décompte mensuel / état d'acompte (F-20, F-21). Under FIDIC the Engineer would issue an IPC (F-22).
3. The contractor disputes: the work was complete on the 24th. Evidence is scattered in WhatsApp photos and the foreman's memory. The dispute is settled weeks later, or carried into the final account. (F-24)

### With the round-1 design

| Step | Input | Becomes | Who acts | Authority | Recorded |
|---|---|---|---|---|---|
| 1 | Foreman's message "coffrage terminé axe F" + photos | `reported` quantity/progress | foreman via message | — | not reachable in round 1 |
| 2 | Surveyor's measurement | `measured` quantity | surveyor | — | assertion |
| 3 | Maître d'œuvre's certificate | `certified` — out of scope or TO-CONFIRM (Q-16) | — | — | — |
| 4 | Dispute | exception `dispute` | Karim | — | exception |

### Where the design breaks

- **The useful part is the evidence pack, not certification.** The contractor's pain is assembling dated, located evidence for each disputed line. OCOS already holds it (if messaging intake exists): photos with time, the reported completion, the measured quantity, any verbal release.
- **One quantity is missing.** Between *measured* (by the contractor) and *certified* (by the maître d'œuvre) lies the *contradictory* measurement both sides sign (attachement, F-23, F-25). Round 1's `accepted` quantity conflates quality acceptance of work with agreement on quantity.
- **Location.** "Axis F" is a location the dispute turns on. Photos without location linking are weak evidence.
- **Liability and wording.** OCOS must not state "the work was complete on the 24th" as a fact; it can only show that Youssef reported it at 17:40 with three photos, and that no measurement was recorded until the 27th.
- **Payment lines vs work packages.** Payment is per bill-of-quantities line or schedule-of-values line (F-22), not per work package. A mapping is needed if OCOS is to help.

### Design changes required

- **DC-4.1** Quantity kinds: `reported`, `measured`, `agreed` (contradictory measurement with both signatures), `certified` (recorded from the certifier's document, never computed). Quality acceptance stays a work-package state (`accepted`).
- **DC-4.2** An *evidence pack* export per work package and period: reported progress, photos with time and location, measurements, releases, and the trace, with integrity data.
- **DC-4.3** Work packages may link to payment lines (BoQ / schedule-of-values item ids) imported from Excel; whether v1.0.0 goes further is `Q-17`.
- **DC-4.4** Location must be a first-class field on intake items (from the message text, a selected location, or the photo's metadata when present), confirmed by the operator.

## Scenario 5 — A company onboards OCOS with its own Excel procedures

### Today

The contractor's procedures are a quality manual (Word/PDF), an approval matrix (who may order what up to which amount), checklists per trade (Excel), a constraint-list template, the meeting-minutes template, a purchase register and a weekly progress sheet. Each site adapts them. (F-13, F-31)

### With the round-1 design

| Step | Input | Becomes | Who acts | Authority | Recorded |
|---|---|---|---|---|---|
| 1 | Approval matrix (Excel) | grants (roles, action types, limits) | written by hand (round-1 Q-17 rec. (a)) | configuration approver | configuration version |
| 2 | Trade checklists (Excel) | requirement templates of the domain pack | by hand | approver | version |
| 3 | Purchase register, constraint list | import mappings | AI proposes, person confirms (SPEC-129) | — | mapping version |
| 4 | Test scenarios | must pass before approval (SPEC-108) | OCOS team | approver | — |

### Where the design breaks

- **Volume.** A checklist set can have hundreds of lines; typing them into configuration files by hand is weeks of work for a pilot. The AI-assisted mapping of SPEC-129 should also draft requirement templates from checklists.
- **Procedures do not match practice.** The manual says a buyer may order up to 50,000; in practice Karim orders sand by phone. The configuration must record the *written* rule and flag observed deviations as exceptions, not silently adopt either.
- **Who approves configuration?** The company has no "configuration approver" role. It must be a named manager (quality manager or works director).
- **Test scenarios** written by the OCOS team are not understood by the company. They must be shown as plain "if this happens, OCOS does that" examples the approver can read.
- **Language and vocabulary.** "Situation", "attachement", "réception", "OPR", "PV" must be terms of the company configuration, mapped to OCOS primitives.

### Design changes required

- **DC-5.1** v1.0.0 includes a *narrow* compiler: AI drafts requirement templates, roles and grants from the company's spreadsheets and tables; every drafted item is reviewed and accepted, edited or rejected by a person; nothing is effective before approval.
- **DC-5.2** Written rule and observed practice are kept apart: deviations become `deviation` exceptions, never automatic rule changes.
- **DC-5.3** The configuration approver is a named company role, set at onboarding.
- **DC-5.4** Scenario tests are shown in plain language ("if the rebar delivery is missed, the slab becomes not ready and Hicham gets a mission") for the approver to read and sign.
- **DC-5.5** Company vocabulary maps to OCOS primitives in the configuration; the interface uses the company's words.

## 6. Where each design change landed

| Change | Landed in |
|---|---|
| DC-1.1, DC-2.2 | IDEA_v2 §5; architecture §4.1; spec SPEC-130–SPEC-136 |
| DC-1.2 | spec SPEC-032, SPEC-033 |
| DC-1.3 | architecture §4.7; spec SPEC-066 |
| DC-1.4 | architecture §4.9; spec SPEC-087, SPEC-134 |
| DC-1.5 | spec SPEC-069 |
| DC-2.1 | spec SPEC-075, SPEC-121 |
| DC-2.3 | spec SPEC-032, SPEC-062 |
| DC-2.4 | IDEA_v2 §13; spec SPEC-039 |
| DC-2.5 | IDEA_v2 §8; spec SPEC-089, SPEC-105 |
| DC-3.1, DC-3.2, DC-3.3, DC-3.4 | IDEA_v2 §9; spec SPEC-031, SPEC-042, SPEC-043 |
| DC-4.1 | IDEA_v2 §9; spec SPEC-023, SPEC-024 |
| DC-4.2 | spec SPEC-192 |
| DC-4.3 | spec SPEC-024; question Q-17 |
| DC-4.4 | spec SPEC-131 |
| DC-5.1 | IDEA_v2 §11; spec SPEC-110 |
| DC-5.2 | spec SPEC-111 |
| DC-5.3, DC-5.4 | spec SPEC-108 |
| DC-5.5 | spec SPEC-112 |

## 7. Review

*Done after the final rewrite of IDEA_v2, core_logic, architecture, spec and questions, before committing them. Three critics, five strongest objections each. **Fixed** = the documents were changed; **answered** = the objection was judged not to require a change, with the reason.*

### 7.1 Critic A — a site manager with 20 years' experience who hates new software

| # | Objection | Verdict | What was done / why it stands |
|---|---|---|---|
| A-1 | "My site group gets 200 messages a day. You want me to tap through every one of them each evening?" | **fixed** | Chatter is proposed as `no_content` and dismissed in one action with a weekly sample check; the queue is ordered by impact (SPEC-137; ARCH §4.1; core_logic §5). Operator time is capped and reviewed (SPEC-205). |
| A-2 | "On day one your board will be full of 'unknown'. I'll look once and never again." | **fixed** | Go-live seeding session for the next two weeks, and a default board of the next two weeks plus anything `not_ready` (SPEC-077; ARCH §4.11; IDEA_v2 §14). |
| A-3 | "A robot chasing my subcontractors will ruin relationships I took years to build." | answered | Already designed out: messages to outside companies start and stay in `confirm` unless the owner decides otherwise (Q-11 recommends internal-only autonomy), are sent in a named person's name, and anyone can be flagged "do not message" (SPEC-089, SPEC-105). |
| A-4 | "This is a machine for blaming me and my foremen." | answered | No individual performance views, organisation-level reporting, pseudonymised metrics, no causation wording (SPEC-188; ARCH §14; Q-13 recommendation). The trace records roles, not fault. |
| A-5 | "Half of what matters is said on the phone or on the slab. It will never be in your system." | **fixed** | Any company person can dictate a ten-second voice note to the OCOS channel, recorded as their report of what someone else said (SPEC-135 extended; core_logic §5); coverage is measured (M-12) rather than assumed. |

### 7.2 Critic B — a contractor's director deciding whether to pay for a pilot

| # | Objection | Verdict | What was done / why it stands |
|---|---|---|---|
| B-1 | "Show me money. 'Late discoveries' is not a line in my accounts." | answered | OCOS deliberately does not compute cost (SPEC-069: people attach cost notes). The pilot's verdict is an operational change the site feels (Q-06); idle hours are tracked where recorded (M-06). Promising euros from a first pilot would be a claim without evidence. |
| B-2 | "Your pilot will eat my site engineer's time." | **fixed** | Concierge option (Q-04 recommendation), an explicit operator-time budget with a review trigger (SPEC-205), and M-11 reported beside every benefit (SPEC-203). |
| B-3 | "My project data and my client's data go to an American AI company? And CNDP / GDPR?" | answered | Hosting, provider and data transfers are pilot-blocking owner decisions (Q-13, Q-20, Q-21), with self-hosted models as an option, a gateway that sends only declared data (ARCH §14), and a personal-data store separate from the log (ARCH §13). |
| B-4 | "Why not just buy Procore or Touchplan?" | answered | Positioning stated honestly (IDEA_v2 §15; RESEARCH §5, F-26): those need the team to type into a platform; OCOS reads what the team already sends and adds a deterministic, auditable make-ready model and an open core. If the pilot already uses a platform, Q-08 decides the connection. |
| B-5 | "An open-source start-up: who is accountable mid-project, and what if you disappear?" | **fixed** | The company can export all its data in an open format at any time, restorable into a fresh installation (SPEC-214; ARCH §13; IDEA_v2 §14); accountability terms are part of Q-09. |

### 7.3 Critic C — a senior software architect judging whether a small team can build v1.0.0 in months

| # | Objection | Verdict | What was done / why it stands |
|---|---|---|---|
| C-1 | "Event sourcing, hash chains, projections, deterministic clock, replay comparison — this is a research project." | **fixed** | The architecture now states the plain implementation: one events table, projections updated in the same transaction, no bus, no event-store product, derived-event comparison only in the nightly replay (ARCH §6.1 implementation note). |
| C-2 | "130-odd requirements is a year of work, not months." | **fixed** | A build order in slices, each usable in shadow mode on the pilot, with spec sections mapped to slices (ARCH §17). Slices 1–2 carry no outbound messaging. |
| C-3 | "Your riskiest dependency is WhatsApp, and you don't know if the route you want is even allowed." | **fixed** | Slice 0 spike proves the channel route before any build (ARCH §17); email-in and upload are permanent fallbacks (SPEC-132); Q-03 recommends the compliant route (business number + chat-export import). |
| C-4 | "The whole value hangs on the AI reading Darija voice notes and messy French. You have no number for that." | **fixed** | Interpreter feasibility gate before go-live on the pilot's own history, per language, with a threshold; failing languages go to people (SPEC-138, SPEC-133; ARCH §17 slice 0). |
| C-5 | "Python, plus Java for MPXJ, plus TypeScript, plus an AI vendor and speech-to-text — too many moving parts." | answered | MPXJ runs in one isolated adapter process and is needed only to read schedule files; if the pilot's planner exports the schedule to Excel, it can wait. The AI vendor sits behind one gateway. Three languages for three clearly separated parts is ordinary for a web product (Q-23). |

**Result: 15 objections — 9 fixed, 6 answered.**

### 7.4 Consistency pass

Checked after the fixes, by script and by reading:

- **Names, states and ids.** State names in core_logic, architecture and spec were compared; the intake, commitment, mission, requirement, exception, readiness and quantity-kind names are identical in all three. Agent roles are `interpreter`, `coordinator`, `drafter` everywhere. The product is called OCOS everywhere.
- **Traceability.** Every `SPEC-nnn` has a `Trace:` line naming an `IDEA_v2 §n` and an `ARCH §n`; every DC in §6 points to an existing SPEC.
- **TO-CONFIRM vs questions.** Every `TO-CONFIRM (Q-nn)` in any document refers to one of Q-01…Q-24, and every question is referenced by at least one `TO-CONFIRM` (Q-24 in core_logic and IDEA_v2; Q-09, Q-19, Q-23 in IDEA_v2 or the architecture).
- **Claims.** Statements of fact about the industry carry an `F-nn`/`S-nn`; design statements are labelled PROPOSAL or point to a DC or an owner question.

