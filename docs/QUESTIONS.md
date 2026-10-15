# Questions for the owner

These are the decisions only you can make. Each one sets the direction of OCOS v1.0.0. The other documents mark every point that waits for you as `TO-CONFIRM (Q-nn)`.

*Round 2, 2026-10-15. The questions were re-derived from the final documents after the research ([RESEARCH.md](RESEARCH.md)). Round-1 questions that the research settled were dropped, and the rest renumbered, most direction-setting first; [RESEARCH.md §9.2](RESEARCH.md#92-round-1-questions-settled-by-the-research) shows what was dropped, why, and the old → new numbering. No round-1 question had been answered, so nothing was carried over.*

## How to answer

**(a) Write your answer.** Open this file on github.com, click the pencil icon (Edit), and write your answer on the `ANSWER:` line of a question — either one of the listed options (for example `(b)`) or your own words. Put any explanation, condition or doubt on the `NOTES:` line.

**(b) Save it.** Commit directly to `main`, with a message like `answers: Q-03, Q-07`.

**(c) Answer at your own pace.** Answer as many or as few questions as you like, in any order. A question you leave unanswered keeps its default only where a default is stated — at present **no question states a default**, so every unanswered question simply waits for you. Nothing that depends on an unanswered question is treated as decided, and the recommendations below are suggestions, not decisions.

**(d) What happens next.** The next working session reads every newly answered question, updates the documents accordingly, removes the matching `TO-CONFIRM` markers, and writes `APPLIED: <date>` under your answer. If you change your mind later, add a line `REOPEN:` under the question with your reason; it will be treated as open again and the documents will be revised.

Each question has: why it matters; the options, simplest or least risky first; a recommendation; what it blocks; and `evidence:` — the research findings (`F-nn`, `V-nn` in RESEARCH.md) that inform the options.

---

## Market, pilot and how OCOS is used

## Q-01 Pilot market and region
- why it matters: the market decides the contract forms (CCAG Travaux, Moroccan CCAG-T, FIDIC, AIA), the inspection actors (bureau de contrôle, ITP hold points), the data-protection law (GDPR or Moroccan law 09-08), the languages (French, Arabic, Darija, English), and which messaging app the site really uses. Everything else is easier to answer once this is known.
- options: (a) Morocco — francophone and Arabic, mostly small and mid-size contractors, paper, Excel and WhatsApp, bureau de contrôle tied to construction insurance compulsory since 30 December 2024 (b) France — CCAG and OPC practice, GDPR, more site software already in use (c) Gulf / wider MENA — FIDIC contracts, large client-mandated platforms such as Aconex (d) another market, named in NOTES
- recommendation: (a) if you have a contractor relationship there — the gap OCOS fills (messages and Excel, no platform) is widest, and French/Arabic tooling is your ecosystem's strength; but choose the market where you have a willing pilot contractor, which matters more than the market itself.
- evidence: RESEARCH §8; F-13, F-18, F-19, F-20, F-22, F-23, F-35
- blocks: SPEC-002, SPEC-210; IDEA_v2 §16; architecture §1, §12
- ANSWER:
- NOTES:

## Q-02 Pilot contractor, project and work type
- why it matters: v1.0.0 is built and judged on one real project. The work type decides which prerequisites OCOS checks (the domain pack), which records it imports, and what can be measured. A pilot with frequent, measurable coordination problems gives a clear verdict.
- options: (a) the structural frame (formwork, rebar, concrete pours) of one building, run by a general contractor with its own crews (b) finishing works (partitions, plastering, MEP second fix), where many subcontractors share each zone (c) a civil or infrastructure job driven by equipment and deliveries (d) other — name the contractor, project and work type in NOTES
- recommendation: (a) — pours have hard, easily checked prerequisites (rebar, inspection hold point, concrete, pump) and costly idle crews; (b) is the stronger test of subcontractor commitments if the contractor mainly subcontracts.
- evidence: F-06, F-17; REALITY_CHECK scenarios 1–3
- blocks: SPEC-002, SPEC-066; architecture §1, §4.9
- ANSWER:
- NOTES:

## Q-03 Messaging channel for field input
- why it matters: field facts arrive as messages, photos and voice notes; OCOS is useless if it cannot see them. WhatsApp's business platform allows task-specific automation but bans general-purpose AI assistants (since January 2026), and reading existing group chats through the official platform is not established. The choice also decides whether shadow mode can run without sending anything.
- options: (a) a dedicated OCOS business number on the site's messaging app: people write or forward to it, and OCOS replies there; email-in and upload as fallbacks (b) as (a), plus periodic import of exported group chats (the app's own "export chat") for facts not forwarded, and for the baseline (c) OCOS joins the existing site groups (only if a compliant technical route is confirmed for the pilot) (d) no messaging in v1.0.0: email-in and upload only
- recommendation: (b) — compliant, needs no new app, works in shadow mode, and the chat exports also give a baseline; (c) only after a technical and policy check.
- evidence: F-09, F-32, F-36; V-07, V-16
- blocks: SPEC-086, SPEC-132; architecture §4.1, §9
- ANSWER:
- NOTES:

## Q-04 Who operates OCOS day to day in the pilot
- why it matters: every AI reading is confirmed by a person in v1.0.0. That person's time is the pilot's main cost, and the pilot fails if nobody does it.
- options: (a) a member of the OCOS team acts as operator ("concierge" pilot), with the site manager approving decisions; the site team learns the role over time (b) the contractor's site engineer or planner is the operator from day one, with a budget of about 20–30 minutes a day (c) the site manager is the operator
- recommendation: (a) for the first 4–8 weeks, then (b) — it protects the site team's time while the interpreter is tuned, and shows what the job really costs before asking the contractor to take it on.
- evidence: F-12, F-14, F-36; V-05
- blocks: SPEC-004; architecture §4.1, §4.11
- ANSWER:
- NOTES:

## Q-05 Planning method: fit the existing meeting, or introduce Last Planner
- why it matters: OCOS's main output is the weekly meeting pack and its main input the meeting's action list. Introducing the full Last Planner routine (weekly plan from ready work only, PPC and reasons) gives better data but asks the team to change how they meet; lean adoption fails mostly on that change.
- options: (a) fit the contractor's existing weekly meeting and minutes; OCOS adds a readiness section and records done / not done with reasons in the background (b) introduce a light Last Planner routine: commit only to ready work, record PPC and reasons each week (c) full Last Planner (pull planning, look-ahead sessions, weekly plan, PPC) with coaching
- recommendation: (a) at the start, moving to (b) once the pack is trusted — the method's value is proven, but forcing it on day one adds a second change on top of OCOS.
- evidence: F-01, F-02, F-04, F-07, F-16, F-37
- blocks: SPEC-006; architecture §4.4
- ANSWER:
- NOTES:

## Q-06 The metric that decides whether v1.0.0 worked
- why it matters: one or two metrics, with a threshold agreed before the pilot, must give the verdict, or any result can be argued either way. The research showed that some round-1 metrics (idle hours) are rarely recorded on real sites.
- options: (a) M-03 late discoveries — blockers first known less than 2 working days before start — target −50 % against baseline (b) M-01 PPC — target +15 percentage points (c) M-02 work made ready ahead (d) a combination you define
- recommendation: (a) as the verdict with (b) as the method figure, and M-11 operator overhead reported beside both — late discovery is what OCOS changes directly and what a site manager feels; PPC is the industry's recognised measure.
- evidence: F-04, F-05, F-07; V-17
- blocks: SPEC-202
- ANSWER:
- NOTES:

## Q-07 How the baseline is measured, and who sees OCOS's output meanwhile
- why it matters: a baseline is needed before OCOS influences the project. If the site team sees OCOS's warnings during the baseline weeks, they act on them and the "before" picture is no longer clean.
- options: (a) retrospective: count late discoveries and missed promises from the last 2–3 months of exported chat history and meeting minutes, plus 3–4 weeks of PPC and reasons recorded by hand at the meeting; shadow output seen only by the OCOS team (b) silent shadow for 4–6 weeks on live data, output seen only by the OCOS team (c) a similar project of the same contractor without OCOS, measured in parallel
- recommendation: (a) — cheaper and faster, and the chat history also builds the interpreter's evaluation set; the chat export needs the consent described in Q-13.
- evidence: F-32; V-17, V-18
- blocks: SPEC-142, SPEC-201; architecture §9
- ANSWER:
- NOTES:

## Positioning and business

## Q-08 Stand-alone, or alongside a project platform
- why it matters: tools such as Touchplan, Procore, Autodesk and Aconex already cover parts of the problem. OCOS can stand alone (messages and Excel) or connect to a platform the pilot already uses. A connector costs development time; ignoring the platform means double records.
- options: (a) stand-alone for v1.0.0; pilot chosen among contractors who use no project platform (b) stand-alone, plus export of OCOS's constraints and actions to the platform the pilot uses (file or API) (c) a two-way connector to the pilot's platform
- recommendation: (a) — the clearest gap is contractors without a platform; it keeps v1.0.0 small. Say in NOTES if the likely pilot uses a platform.
- evidence: F-10, F-26; RESEARCH §5
- blocks: SPEC-213; IDEA_v2 §15; architecture §10
- ANSWER:
- NOTES:

## Q-09 Business model and pilot terms
- why it matters: a contractor's director will ask what they pay, for what, and who is accountable if it fails. It also decides what goes into the open repository and what stays a service.
- options: (a) free pilot in exchange for data access, feedback and a case study; later open core free plus paid hosting, onboarding and support (b) paid pilot at a reduced fixed price with success criteria from Q-06 (c) fully open source, revenue only from services and configuration work
- recommendation: (a) for the first pilot, with a written agreement on data use and the Q-06 criteria; (b) from the second pilot.
- evidence: F-14 (cost is a top barrier), F-26
- blocks: IDEA_v2 §15; architecture §11
- ANSWER:
- NOTES:

## Authority, autonomy and trust

## Q-10 What the kernel guarantees versus what a company may configure
- why it matters: mandatory safety, security and legal constraints cannot be disabled by ordinary configuration, but the list must be fixed. The research adds the hold-point / witness-point distinction and the practice of verbal releases recorded later.
- options: (a) the kernel fixes: hold points block until released; statutory and safety permits block; configuration may add or tighten gates, never relax them; nobody can waive a kernel gate in OCOS (b) as (a), but a named person with an explicit "waive gate" authority may waive one with rationale and a heavy trace (c) only the SPEC-106 invariants are fixed; every gate is company configuration
- recommendation: (b) — real sites sometimes proceed on an engineer's written instruction; refusing it pushes the decision outside OCOS's trace. Whether *reported* (verbal) releases are accepted stays per inspection type in company configuration.
- evidence: F-17, F-18, F-34; V-11
- blocks: SPEC-031, SPEC-107; architecture §4.3, §4.9, §7.4
- ANSWER:
- NOTES:

## Q-11 Which actions v1.0.0 may ever take on its own
- why it matters: decides how far "autonomous" goes once shadow and confirm modes end. Automated chasing of outside companies can damage relationships and be read as a formal notice.
- options: (a) none: every action needs a person's click (b) internal only: reminders and information requests to the contractor's own staff, escalations along the configured path; everything to outside companies stays in confirm (c) as (b), plus reminders to suppliers and subcontractors who have agreed to receive them (d) as (b), plus automatic confirmation of high-confidence readings in categories where M-08 shows reliability
- recommendation: (b) — it removes most internal chasing with no external risk; (c) and (d) after the pilot's evidence.
- evidence: F-34, F-39; V-14, V-15
- blocks: SPEC-105; architecture §7.4, §9
- ANSWER:
- NOTES:

## Q-12 When and how an action type leaves shadow or confirm mode
- why it matters: sets the evidence bar before OCOS acts for real, and who carries that decision.
- options: (a) the contractor's project director decides per action type, after at least 4 weeks in shadow and 2 weeks in confirm mode, with at least 90 % of that type labelled correct and none labelled incorrect with consequences (b) as (a), but you (the owner) and the contractor decide jointly (c) case by case
- recommendation: (b) — written criteria protect both sides; joint sign-off fits a first pilot.
- evidence: F-30, F-33
- blocks: SPEC-145; architecture §9
- ANSWER:
- NOTES:

## Q-13 Records about named people: what is kept, who sees it, for how long
- why it matters: OCOS keeps who said, promised and decided what, and reads messages that name workers. Under GDPR (CNIL) or Morocco's law 09-08 (CNDP) this needs a legitimate purpose, information of staff, limited retention, and possibly authorisation for transfers abroad. Using exported chat history for the baseline also needs consent. Getting this wrong can stop a pilot.
- options: (a) individuals named only inside the contractor's team; outside companies at company level with a contact; no individual performance views; message authors pseudonymised in metrics; retention = project duration + contractual archive period; staff informed in writing before start (b) a policy written with the contractor's legal adviser, described in NOTES (c) everyone named everywhere with individual statistics
- recommendation: (a), checked by the contractor's legal adviser — enough for traceability without becoming a staff-rating tool.
- evidence: F-35; V-21
- blocks: SPEC-190; architecture §13, §14
- ANSWER:
- NOTES:

## Q-14 How strong the tamper evidence must be
- why it matters: records may be used in payment disputes. A hash chain detects changes, but whoever runs the server could rewrite the whole chain; a copy of the integrity checkpoints outside the operator's control prevents that.
- options: (a) hash chain only, verified by a tool (b) hash chain plus daily signed checkpoints sent to the contractor (email or their storage) (c) as (b) plus a public timestamping service
- recommendation: (b) — cheap, and the operator alone can no longer rewrite history unnoticed.
- evidence: F-10, F-24; V-24
- blocks: SPEC-186; architecture §6.5
- ANSWER:
- NOTES:

## Scope of v1.0.0

## Q-15 Source of truth and writing back to other systems
- why it matters: external files and systems stay authoritative for what they own. Still to decide: which records OCOS itself owns, and whether it ever updates other systems (for example the constraint spreadsheet).
- options: (a) read-only towards everything in v1.0.0; OCOS owns intake readings, missions, commitments recorded through it, requirement states, readiness, weekly plans, exceptions, decisions and the trace (b) as (a), plus OCOS becomes the master of the constraint list, replacing the spreadsheet with an exported copy (c) as (a), plus approved write-back of a few fields
- recommendation: (a) at the start, (b) once the team trusts the board — retiring the spreadsheet is the adoption milestone.
- evidence: F-31; V-20
- blocks: SPEC-127; architecture §4.10, §10
- ANSWER:
- NOTES:

## Q-16 Beam-stack products in v1.0.0
- why it matters: Planitor and Chantier Manager are first-class integrations in the idea, but OCOS must be useful without them. Building their adapters only makes sense if the pilot uses them and they can export data.
- options: (a) not in v1.0.0; optional adapters for the next release (b) in v1.0.0 if the pilot uses them (c) v1.0.0 built primarily around them
- recommendation: (b) — real data without extra effort for the pilot; the generic adapter contract keeps OCOS independent. Say in NOTES whether each product has an export or API today.
- evidence: F-26 (independence is part of the position)
- blocks: SPEC-122; IDEA_v2 §12; architecture §10
- ANSWER:
- NOTES:

## Q-17 Monthly statements: how far v1.0.0 goes
- why it matters: OCOS never certifies — certification is the maître d'œuvre's or Engineer's legal act. But disputes over monthly statements are where contractors lose money, and OCOS already holds the evidence.
- options: (a) evidence packs per work package only; no payment lines (b) as (a), plus import of payment lines (bill of quantities / schedule of values) linked to work packages, and recording of agreed (attachement) and certified quantities from documents (c) as (b), plus a draft monthly statement (projet de décompte / situation) for the contractor's quantity surveyor to check
- recommendation: (b) — high value in disputes, low risk; (c) after the pilot, since it moves OCOS into commercial territory.
- evidence: F-20–F-25; V-12, V-13; REALITY_CHECK scenario 4
- blocks: SPEC-024; IDEA_v2 §9; architecture §4.6
- ANSWER:
- NOTES:

## Q-18 How the pilot company's configuration is produced
- why it matters: the company's checklists, approval tables and templates are mostly Excel and Word. Typing them into configuration by hand takes weeks; a narrow AI-assisted compiler drafts them for review.
- options: (a) written by hand with the contractor as versioned files reviewed by a person; compiler later (b) narrow compiler in v1.0.0: AI drafts requirement templates, roles, grants and vocabulary from the company's tables; a person accepts, edits or rejects every item (c) full compiler from any document in v1.0.0
- recommendation: (b) — the onboarding scenario showed hand-writing is the bottleneck, and every drafted item is still reviewed.
- evidence: F-13; V-22; REALITY_CHECK scenario 5
- blocks: SPEC-110; IDEA_v2 §11; architecture §4.9
- ANSWER:
- NOTES:

## Openness, technology and operation

## Q-19 Open-source license and governance
- why it matters: "the Linux of construction" depends on others adopting, extending and trusting OCOS. The license decides whether others can build closed products on it; governance decides who controls the protocol and kernel.
- options: (a) Apache-2.0 for everything; you lead as maintainer with a public proposal process (b) AGPL-3.0 for the kernel, Apache-2.0 for protocol schemas, adapters and SDKs (c) as (a) or (b), moving to a neutral foundation once other organisations contribute
- recommendation: (a) now, (c) later — most adoption-friendly, with a patent grant; (b) better protects against a closed fork run as a service. Align with Q-09.
- evidence: F-26 (the open core is the part incumbents are unlikely to copy)
- blocks: IDEA_v2 §19; architecture §11; repository LICENSE file
- ANSWER:
- NOTES:

## Q-20 Hosting and data residency
- why it matters: decides who runs OCOS for the pilot, where data lives, and what the contractor's IT, legal and data-protection obligations require (for example CNDP authorisation for transfers out of Morocco).
- options: (a) single-tenant installation per company, run by the OCOS team in a region acceptable under the pilot's data law (b) installed on the contractor's own servers or cloud (c) one shared multi-company service
- recommendation: (a), built so (b) is always possible — data never mixed, simplest to support.
- evidence: F-35
- blocks: SPEC-210; architecture §11, §12, §13
- ANSWER:
- NOTES:

## Q-21 AI model and speech policy
- why it matters: the interpreter sends message text, photos and voice notes to a model. Provider, terms, region and whether a self-hosted model is required affect accuracy, cost and legality (data transfers abroad).
- options: (a) one commercial provider under no-training, limited-retention terms, behind the gateway; open-weight fallback tested (b) self-hosted open-weight models only, so no data leaves the installation (c) configurable per company: commercial by default, self-hosted on request
- recommendation: (a) for the pilot if the data-protection check (Q-13, Q-20) allows it, with (c) as the design target — reading Darija voice notes and messy messages needs the best available models now.
- evidence: F-35, F-39; V-08
- blocks: SPEC-211; architecture §4.8, §11, §14
- ANSWER:
- NOTES:

## Q-22 Languages
- why it matters: the interface, outbound messages and the interpreter must work in the languages the site writes and speaks. Spoken Darija in voice notes is much harder for AI than written French; unsupported languages go to a person to read.
- options: (a) French only, with Arabic and Darija messages sent to a person to read (b) French and Modern Standard Arabic for the interface and messages; the interpreter also reads Darija written in Latin or Arabic script and Darija voice notes, with accuracy measured per language (c) English only (d) other, named in NOTES
- recommendation: depends on Q-01; for Morocco (b), with Darija accuracy checked on the pilot's own message history before go-live; English for code and documentation in all cases.
- evidence: RESEARCH §8; F-39
- blocks: SPEC-005; architecture §4.1, §4.11
- ANSWER:
- NOTES:

## Q-23 Technology stack
- why it matters: the language and database shape who can contribute and how fast a small team builds. Reading MS Project and Primavera files needs MPXJ, a Java library.
- options: (a) Python (typed) back end, TypeScript web interface, PostgreSQL for the event table and projections; MPXJ run in a separate adapter process (b) TypeScript everywhere, PostgreSQL (c) Java/Kotlin back end (native MPXJ), TypeScript interface, PostgreSQL (d) the language the Beam-stack products use, named in NOTES
- recommendation: (a) — best libraries for spreadsheets, documents and AI providers; MPXJ isolated in one adapter.
- evidence: F-11; V-25
- blocks: architecture §11
- ANSWER:
- NOTES:

## Naming

## Q-24 Name of the product
- why it matters: the idea uses "OCOS" and sometimes "OOF"; the repository is "COS". One name is needed for code, documents, packages and a trademark check.
- options: (a) OCOS — Open Construction Operating System (b) COS, matching the repository (c) another name, given in NOTES
- recommendation: (a) — the idea's main name, already used in every document.
- evidence: none (naming is not a research question)
- blocks: nothing — direction only (all documents use OCOS until answered)
- ANSWER:
- NOTES:
