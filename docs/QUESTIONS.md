# Questions for the owner

These are the decisions only you can make. Each one sets the direction of OCOS v1.0.0. The other documents mark every point that waits for you as `TO-CONFIRM (Q-nn)`.

*Round 2, 2026-10-15, reordered by the study ([STUDY.md](STUDY.md)) so you can answer fast: **the seven questions that block the first build slice come first**; the rest can wait. Question ids did not change. [RESEARCH.md §9.2](RESEARCH.md#92-round-1-questions-settled-by-the-research) shows which round-1 questions the research settled. No question has been answered yet.*

## How to answer

**(a) Write your answer.** Open this file on github.com, click the pencil icon (Edit), and write your answer on the `ANSWER:` line of a question — either one of the listed options (for example `(b)`) or your own words. Put any explanation, condition or doubt on the `NOTES:` line.

**(b) Save it.** Commit directly to `main`, with a message like `answers: Q-03, Q-07`.

**(c) Answer at your own pace.** Answer as many or as few questions as you like, in any order. Each question now states a **default**: what the next working session assumes, behind a `TO-CONFIRM` marker, if the work reaches that point before you answer. A default is never treated as your answer — the marker stays until you answer, and the recommendations are suggestions, not decisions.

**(d) What happens next.** The next working session reads every newly answered question, updates the documents accordingly, removes the matching `TO-CONFIRM` markers, and writes `APPLIED: <date>` under your answer. If you change your mind later, add a line `REOPEN:` under the question with your reason; it will be treated as open again and the documents will be revised.

Each question has: why it matters; the options, simplest or least risky first; a recommendation; a default; `evidence:` — the research findings (`F-nn`, `V-nn` in RESEARCH.md) that inform the options; and what it blocks.

---

## Answer these first — they block the first build slice

*Slice 1 (the readiness board, no AI, nothing sent) and its two trials — the messaging channel (T1) and the AI's reading accuracy (T2) — cannot start properly without these. See [architecture §17](v1.0.0_architecture.md#17-build-order-v100).*

## Q-01 Pilot market and region
- why it matters: the country decides the contract forms and their words (situation, attachement, décompte), who inspects, which data-protection law applies, and which languages the site writes and speaks. It is the question most others depend on.
- options: (a) the country of a contractor you already know and who would pilot — name them in NOTES (b) Morocco — mostly small and mid-size contractors on paper, Excel and WhatsApp; French and Arabic (c) France — more site software already in use; GDPR (d) the Gulf or wider MENA — FIDIC contracts; big clients impose platforms such as Aconex
- recommendation: (a) — a willing pilot contractor matters more than the market; if you have none yet, (b), where the gap OCOS fills is widest.
- default: (b) Morocco — French interface and Moroccan contract vocabulary in the test data; nothing market-specific beyond that is built.
- evidence: RESEARCH §8; F-13, F-18, F-19, F-20, F-22, F-23, F-35
- blocks: SPEC-002, SPEC-210; slice 1 test data and vocabulary; trial T2
- ANSWER:
- NOTES:

## Q-02 Pilot contractor, project and work type
- why it matters: OCOS checks a list of prerequisites per type of work. The first list must match the pilot, and the type of work decides what can be measured.
- options: (a) the structural frame of one building — formwork, rebar, concrete pours — by a contractor with its own crews (b) finishing works, where many subcontractors share each floor (c) a civil-works job driven by equipment and deliveries (d) other — name the contractor, project and work type in NOTES
- recommendation: (a) — a pour has clear prerequisites (rebar, inspection, concrete, pump) and idle crews cost money; (b) if the contractor mostly subcontracts.
- default: (a) structural frame — the first prerequisite list is the slab pour of [architecture §4.9](v1.0.0_architecture.md#49-company-configuration-pilot-domain-pack-and-narrow-compiler).
- evidence: F-06, F-17, F-23; REALITY_CHECK scenarios 1–3
- blocks: SPEC-002, SPEC-066; slice 1 exit check
- ANSWER:
- NOTES:

## Q-23 Technology stack
- why it matters: the build loops need one stack, one test command and one CI before the first task. Reading MS Project and Primavera files needs MPXJ, a Java library.
- options: (a) Python (typed) back end, TypeScript web interface, PostgreSQL; MPXJ in its own small adapter — the same pattern as Chantier Manager (b) TypeScript everywhere, PostgreSQL — the pattern of Bunyan (c) Java or Kotlin back end (MPXJ native), TypeScript interface, PostgreSQL
- recommendation: (a) — best libraries for spreadsheets, documents and AI providers, and the loops already run Python lanes with PostgreSQL.
- default: (a).
- evidence: F-11; V-25
- blocks: every build task; architecture §11; `.agent.toml` and CI
- ANSWER:
- NOTES:

## Q-19 Open-source licence and governance
- why it matters: the licence decides whether others may build closed products on OCOS; it must be chosen before code is published.
- options: (a) no licence yet: the repository stays private and nothing is published until you decide (b) Apache-2.0 for everything; you lead as maintainer with a public proposal process (c) AGPL-3.0 for the kernel, Apache-2.0 for schemas, adapters and SDKs (d) (b) or (c), moving to a neutral foundation once other organisations contribute
- recommendation: (b) now, (d) later — the most adoption-friendly, with a patent grant; (c) protects better against a closed copy run as a service. Align with Q-09.
- default: (a) — the loops can build; nothing is published as open source.
- evidence: F-26 (the open core is the part incumbents are unlikely to copy)
- blocks: the repository LICENSE file; publishing any code; IDEA_v2 §19; architecture §11
- ANSWER:
- NOTES:

## Q-03 How site messages reach OCOS
- why it matters: field facts arrive as messages, photos and voice notes. WhatsApp's official interface **cannot join the site's existing groups**: it can only create its own groups of at most 8 people. So messages reach OCOS only if someone forwards them, or through exported chats.
- options: (a) email and upload only — no messaging app in v1.0.0 (b) an OCOS business number: the operator (already in the site groups) forwards what matters, and anyone may write or send voice notes to it (c) as (b), plus a regular export of the site groups ("export chat") to catch what was not forwarded and to measure the baseline (d) reading the existing groups through an unofficial route — against WhatsApp's terms, the number can be banned; not recommended
- recommendation: (c) — within the platform's terms, no new app for the field, works in shadow mode, and the exports measure how much really arrives by message.
- default: (a) until you answer; trial T1 does not start.
- evidence: F-09 (weak), F-32, F-36; V-07, V-16
- blocks: SPEC-086, SPEC-132; trial T1 (also needs a WhatsApp business account verified by Meta); architecture §4.1, §9
- ANSWER:
- NOTES:

## Q-13 Records about named people: what is kept, who sees it, for how long
- why it matters: OCOS records who said, promised and decided what, and reads messages that name workers. Under GDPR or Morocco's law 09-08 this needs a purpose, information of staff, limited retention and sometimes authorisation. Using exported chats for the trial also needs consent. Getting this wrong can stop a pilot.
- options: (a) people named only inside the contractor's team; outside companies at company level with a contact; no individual performance views; authors pseudonymised in metrics; kept for the project plus the contractual archive period; staff informed in writing before start (b) a policy written with the contractor's legal adviser, described in NOTES (c) everyone named everywhere, with individual statistics
- recommendation: (a), checked by the contractor's legal adviser.
- default: (a); no real chat history is used until you answer.
- evidence: F-35; V-21
- blocks: SPEC-190; trial T2; architecture §13, §14
- ANSWER:
- NOTES:

## Q-21 Which AI may read the pilot's messages
- why it matters: the AI reads message text, photos and voice notes. The provider, its terms and where it runs affect accuracy, cost and legality (data sent abroad).
- options: (a) no AI on real pilot data yet: the trial runs on anonymised history only (b) one commercial provider under no-training, limited-retention terms, behind OCOS's gateway; a self-hosted model tested as fallback (c) self-hosted open models only, so no data leaves the installation (d) per company: commercial by default, self-hosted on request
- recommendation: (b) for the pilot once the Q-13 check allows it, with (d) as the long-term design — Darija voice notes and messy messages need the best models now.
- default: (a).
- evidence: F-35, F-39; V-08
- blocks: SPEC-211; trial T2; architecture §4.8, §11, §14
- ANSWER:
- NOTES:

---

## Can wait — needed later in the build or for the pilot itself

### Running the pilot

## Q-04 Who operates OCOS day to day in the pilot
- why it matters: a person confirms every AI reading. Their time is the pilot's main cost, and the pilot fails if nobody does it.
- options: (a) a member of the OCOS team is the operator ("concierge" pilot), the site manager approves decisions (b) the contractor's site engineer or planner, about 20–30 minutes a day (c) the site manager
- recommendation: (a) for the first 4–8 weeks, then (b).
- default: (a), with an operator time budget of 30 minutes a day (SPEC-205).
- evidence: F-12, F-14, F-36; V-05
- blocks: SPEC-004, SPEC-205 budget; architecture §4.1, §4.11
- ANSWER:
- NOTES:

## Q-05 Fit the existing weekly meeting, or introduce Last Planner
- why it matters: OCOS's main output is the weekly meeting pack. Changing how the team meets adds a second change on top of OCOS; lean methods mostly fail on that change.
- options: (a) fit the contractor's existing meeting and minutes; OCOS adds a readiness section and records done / not done with reasons (b) a light Last Planner routine: commit only to ready work, record PPC and reasons (c) full Last Planner with coaching
- recommendation: (a) at the start, (b) once the pack is trusted.
- default: (a).
- evidence: F-01, F-02, F-04, F-07, F-16, F-37
- blocks: SPEC-006 (slice 2); architecture §4.4
- ANSWER:
- NOTES:

## Q-06 The measure that decides whether v1.0.0 worked
- why it matters: one or two measures with a threshold agreed before the pilot, or any result can be argued either way.
- options: (a) late discoveries — blockers first known less than 2 working days before start — down 50 % against the baseline (b) PPC up 15 points (c) work made ready ahead (d) a combination you define
- recommendation: (a) as the verdict, (b) as the method figure, with the operator's time shown beside both.
- default: (a) + (b).
- evidence: F-04, F-05, F-07; V-17
- blocks: SPEC-202
- ANSWER:
- NOTES:

## Q-07 How the baseline is measured, and who sees OCOS's output meanwhile
- why it matters: if the site team acts on OCOS's warnings during the baseline weeks, the "before" picture is no longer clean.
- options: (a) look back: count late discoveries and missed promises in the last 2–3 months of exported chats and minutes, plus 3–4 weeks of PPC recorded by hand; shadow output seen only by the OCOS team (b) 4–6 weeks of silent shadow on live data (c) a similar project without OCOS, measured in parallel
- recommendation: (a) — cheaper, faster, and the same history feeds trial T2; needs the Q-13 consent.
- default: (a).
- evidence: F-32; V-17, V-18
- blocks: SPEC-142, SPEC-201
- ANSWER:
- NOTES:

## Q-22 Languages
- why it matters: the screens, messages and the AI must work in the languages the site uses. Darija voice notes are much harder for AI than written French; what the AI cannot read goes to a person.
- options: (a) French only; Arabic and Darija go to a person (b) French and Arabic screens and messages; the AI also reads Darija (Latin or Arabic script, and voice), accuracy measured per language (c) English only (d) other, in NOTES
- recommendation: follows Q-01; for Morocco (b), with Darija checked in trial T2. English for code and documentation in all cases.
- default: (a).
- evidence: RESEARCH §8; F-39
- blocks: SPEC-005; architecture §4.1, §4.11
- ANSWER:
- NOTES:

## Q-20 Hosting and where the data lives
- why it matters: who runs OCOS for the pilot, where data is stored, and what the law requires (for example CNDP authorisation for transfers out of Morocco).
- options: (a) one installation per company, run by the OCOS team in a region the pilot's data law accepts (b) on the contractor's own servers or cloud (c) one shared service for several companies
- recommendation: (a), built so (b) always works.
- default: (a).
- evidence: F-35
- blocks: SPEC-210 (before go-live); architecture §11–§13
- ANSWER:
- NOTES:

### Positioning and business

## Q-08 Stand-alone, or alongside a project platform
- why it matters: Touchplan, Procore, Autodesk or Aconex already cover parts of the problem. A connector costs build time; ignoring a platform the pilot uses means double records.
- options: (a) stand-alone; pilot chosen among contractors with no project platform (b) stand-alone, plus an export of OCOS's constraints and actions to the pilot's platform (c) a two-way connector
- recommendation: (a). Say in NOTES if the likely pilot uses a platform.
- default: (a).
- evidence: F-10, F-26; RESEARCH §5
- blocks: SPEC-213; IDEA_v2 §15
- ANSWER:
- NOTES:

## Q-09 Business model and pilot terms
- why it matters: a contractor's director asks what they pay, for what, and who is accountable if it fails. It also decides what is open and what is a service.
- options: (a) free pilot for data access, feedback and a case study; later a free open core plus paid hosting, onboarding and support (b) paid pilot at a reduced fixed price, with success criteria from Q-06 (c) fully open source, revenue only from services
- recommendation: (a) for the first pilot with a written agreement on data use and the Q-06 criteria; (b) from the second.
- default: (a).
- evidence: F-14 (cost is a barrier), F-26
- blocks: IDEA_v2 §15; architecture §11
- ANSWER:
- NOTES:

### Authority and trust

## Q-10 What OCOS always enforces versus what a company may change
- why it matters: some safety and legal rules must never be switched off by a company's settings. The list must be fixed.
- options: (a) fixed for everyone: hold points block until released; legal and safety permits block; a company may add or tighten rules, never relax them; nobody can waive a fixed rule in OCOS (b) as (a), but a named person with an explicit "waive" right may waive one, with a reason and a full trace (c) only the core protections of SPEC-106 are fixed; every other rule is the company's
- recommendation: (b) — sites sometimes proceed on an engineer's written instruction; refusing it pushes the decision out of OCOS's record. Accepting verbal releases stays a per-inspection company setting (default: not accepted).
- default: (a).
- evidence: F-17, F-18, F-34; V-11
- blocks: SPEC-031, SPEC-107 (slice 3)
- ANSWER:
- NOTES:

## Q-12 The evidence needed before OCOS acts for real
- why it matters: sets the bar before OCOS sends anything itself, and before its AI readings are used on the pilot.
- options: (a) the contractor's project director decides per action type after at least 4 weeks in shadow and 2 in confirm mode, with at least 90 % labelled correct and none wrong with consequences; the AI goes live in a language when at least 80 % of 300 test readings are right or need one correction (b) as (a), but you and the contractor decide jointly (c) case by case
- recommendation: (b) — written criteria protect both sides.
- default: (b) with the figures in (a).
- evidence: F-30, F-33, F-39
- blocks: SPEC-145; the SPEC-138 thresholds
- ANSWER:
- NOTES:

### Scope of v1.0.0

## Q-15 Source of truth and writing back to other systems
- why it matters: other files and systems stay the reference for what they own. Still open: which records OCOS owns, and whether it ever updates other systems.
- options: (a) read-only towards everything; OCOS owns its readings, missions, promises recorded through it, readiness, weekly plans, exceptions, decisions and the trace (b) as (a), plus OCOS becomes the master of the constraint list, replacing the spreadsheet (c) as (a), plus approved write-back of a few fields
- recommendation: (a) at the start, (b) once the team trusts the board.
- default: (a).
- evidence: F-31; V-20
- blocks: SPEC-127
- ANSWER:
- NOTES:

## Q-16 Beamstack products in v1.0.0
- why it matters: Planitor and Chantier Manager are first-class integrations in the idea, but OCOS must work without them. Their adapters only make sense if the pilot uses them and they can export data.
- options: (a) not in v1.0.0; adapters in the next release (b) in v1.0.0 if the pilot uses them (c) v1.0.0 built around them
- recommendation: (b). Say in NOTES whether each product has an export or API today.
- default: (a).
- evidence: F-26 (independence is part of the position)
- blocks: SPEC-122; IDEA_v2 §12
- ANSWER:
- NOTES:

## Q-17 Monthly statements: how far v1.0.0 goes
- why it matters: OCOS never certifies — that is the maître d'œuvre's or Engineer's legal act — but monthly-statement disputes are where contractors lose money, and OCOS holds the evidence.
- options: (a) evidence packs per work package only (b) as (a), plus import of the bill-of-quantities lines linked to work packages, and recording of agreed (attachement) and certified quantities from documents (c) as (b), plus a draft of the contractor's own document — the attachement in Morocco, the projet de décompte in France — for the contractor's quantity surveyor to check
- recommendation: (b); (c) after the pilot.
- default: (a).
- evidence: F-20–F-25; V-12, V-13; REALITY_CHECK scenario 4
- blocks: SPEC-024 (slice 3)
- ANSWER:
- NOTES:

### Moved to later by the study — answer whenever you like

## Q-11 Which actions OCOS may one day take on its own
- why it matters: decides how far "autonomous" goes after shadow and confirm modes. Automatic chasing of outside companies can harm relationships and be read as a formal notice. The study moved this out of v1.0.0: the first pilot runs in shadow and confirm modes only.
- options: (a) none: every action needs a person's click (b) internal only: reminders and requests to the contractor's own staff, escalations; everything to outside companies stays in confirm (c) as (b), plus reminders to suppliers and subcontractors who agreed to receive them (d) as (b), plus automatic confirmation of readings in categories where accuracy is proven
- recommendation: (b) after the pilot; (c) and (d) later.
- default: (a) for v1.0.0.
- evidence: F-34, F-39; V-14, V-15
- blocks: SPEC-105 (later)
- ANSWER:
- NOTES:

## Q-14 How strong the tamper evidence must be
- why it matters: records may be used in payment disputes. A hash chain detects changes, but whoever runs the server could rewrite the whole chain; copies of checkpoints held by the contractor prevent that. The study moved anchoring out of v1.0.0.
- options: (a) hash chain only, checked by a tool (b) plus daily signed checkpoints sent to the contractor (c) as (b) plus a public timestamping service
- recommendation: (b), after v1.0.0 — cheap to add.
- default: (a) for v1.0.0.
- evidence: F-10, F-24; V-24
- blocks: SPEC-186 (later)
- ANSWER:
- NOTES:

## Q-18 How the pilot company's configuration is produced
- why it matters: the company's checklists, approval tables and templates are mostly Excel and Word. For one pilot, writing them up by hand is feasible; an AI-assisted drafter pays off from the second company. The study moved the drafter out of v1.0.0.
- options: (a) written by hand with the contractor, reviewed by a person (b) the AI drafts the lists, roles and vocabulary from the company's tables; a person accepts, edits or rejects every item (c) full compiler from any document
- recommendation: (a) for the pilot, (b) next.
- default: (a).
- evidence: F-13; V-22; REALITY_CHECK scenario 5
- blocks: SPEC-110 (later)
- ANSWER:
- NOTES:

### Naming

## Q-24 Name of the product
- why it matters: the idea uses "OCOS" and sometimes "OOF"; the repository is "COS". One name is needed for code, documents, packages and a trademark check.
- options: (a) OCOS — Open Construction Operating System (b) COS, matching the repository (c) another name, in NOTES
- recommendation: (a) — the idea's main name, already used in every document.
- default: (a); renaming code packages later costs one task.
- evidence: none (naming is not a research question)
- blocks: nothing — direction only
- ANSWER:
- NOTES:
