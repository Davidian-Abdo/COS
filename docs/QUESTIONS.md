# Questions for the owner

These are the decisions only you can make. Each one sets the direction of OCOS v1.0.0. The other documents mark every point that waits for you as `TO-CONFIRM (Q-nn)`.

## How to answer

**(a) Write your answer.** Open this file on github.com, click the pencil icon (Edit), and write your answer on the `ANSWER:` line of a question — either one of the listed options (for example `(b)`) or your own words. Put any explanation, condition or doubt on the `NOTES:` line.

**(b) Save it.** Commit directly to `main`, with a message like `answers: Q-03, Q-07`.

**(c) Answer at your own pace.** Answer as many or as few questions as you like, in any order. A question you leave unanswered keeps its default only where a default is stated — at present **no question states a default**, so every unanswered question simply waits for you. Nothing that depends on an unanswered question is treated as decided, and the recommendations below are suggestions, not decisions.

**(d) What happens next.** The next working session reads every newly answered question, updates the documents accordingly, removes the matching `TO-CONFIRM` markers, and writes `APPLIED: <date>` under your answer. If you change your mind later, add a line `REOPEN:` under the question with your reason; it will be treated as open again and the documents will be revised.

---

## Pilot, users and success

## Q-01 First pilot customer and work type
- why it matters: v1.0.0 is built and judged on one real project (idea §13). The work type decides which prerequisites OCOS checks, which records it must import, and which numbers we can measure. A pilot with frequent, measurable coordination problems gives a clear verdict; a vague one gives none.
- options: (a) the structural frame (formwork, rebar, concrete pours) of one building project run by a contractor you already work with (b) finishing works (partitions, plastering, MEP second fix) on one building, where many trades share each zone (c) a civil/infrastructure job (earthworks, networks) driven by equipment and deliveries (d) other — please name the contractor, project and work type
- recommendation: (a) — pours have hard, easily checked prerequisites (inspection, rebar, concrete, pump), measurable quantities and costly idle crews, so improvements show quickly.
- blocks: SPEC-002, SPEC-066; architecture §1 and §4.7 (pilot domain pack)
- ANSWER:
- NOTES:

## Q-02 First operator users
- why it matters: decides who logs into OCOS, who only receives missions and reminders, and therefore how much training, interface and support the pilot needs.
- options: (a) the contractor's site management only (site/works manager, planner, buyer); foremen, subcontractors and suppliers receive missions by message and answer by message (b) as (a) plus foremen using simple phone forms (c) everyone, including subcontractors and suppliers, has an OCOS account
- recommendation: (b) — foremen hold most of the field facts, but asking outside companies to adopt a new tool would slow the pilot.
- blocks: SPEC-004, SPEC-086; architecture §4.4, §4.9
- ANSWER:
- NOTES:

## Q-03 What "ready" means, and how far ahead OCOS looks
- why it matters: OCOS checks readiness inside a time window before each package starts. Too short and problems are found too late to fix; too long and people are chased about work weeks away. It also fixes when a package must be fully ready (for example the Friday before the week of work).
- options: (a) look ahead 3 weeks, check daily, a package must be `ready` 2 working days before its start (b) look ahead 6 weeks, check daily, weekly commitment meeting decides next week's work from the `ready` packages (the "Last Planner" practice) (c) follow the pilot contractor's current planning rhythm, to be described in NOTES
- recommendation: (c) if the contractor already has a weekly planning rhythm, otherwise (a) — fit the company's habits first (idea §10).
- blocks: SPEC-065, SPEC-066; architecture §4.3, §4.7
- ANSWER:
- NOTES:

## Q-04 The metric that decides whether v1.0.0 worked
- why it matters: the idea lists eleven metrics (spec §11). One or two must be the verdict, with a threshold agreed before the pilot, or any result can be argued either way.
- options: (a) M-01 share of work packages genuinely ready, with target improvement over baseline (for example +20 percentage points) (b) M-04 avoidable idle hours of crews and equipment (for example −30 %) (c) M-02 blocker detection-to-resolution time (for example −40 %) (d) a combination you define
- recommendation: (a) as the verdict with (b) as the money figure — readiness is what v1.0.0 directly acts on; idle hours turn it into cost for a director or investor.
- blocks: SPEC-202
- ANSWER:
- NOTES:

## Q-05 How the baseline is measured, and who sees OCOS's output meanwhile
- why it matters: the idea requires a baseline before deployment. If the site team sees OCOS's warnings during the baseline weeks, they start acting on them and the "before" picture is no longer clean.
- options: (a) silent shadow: OCOS runs on live data for N weeks, its output seen only by a reviewer (you or the OCOS team), while the site team measures M-01…M-11 with simple weekly forms (b) historical: rebuild the baseline from a recent finished project of the same contractor (c) comparison: a similar project of the same contractor without OCOS, measured in parallel
- recommendation: (a) for 4–6 weeks, plus (b) where records allow — it measures the same project and also produces the shadow-mode accuracy data.
- blocks: SPEC-142, SPEC-201; architecture §9
- ANSWER:
- NOTES:

## Authority, autonomy and trust

## Q-06 What the kernel guarantees versus what a company may configure
- why it matters: the idea says mandatory safety, security and legal constraints cannot be disabled by ordinary configuration, but does not list them. This sets what every OCOS installation guarantees, and what a company can change for itself.
- options: (a) the kernel guarantees the invariants of SPEC-106 plus a fixed list of mandatory gates (safety-critical decisions, statutory inspections and permits, quality hold points); configuration may only add or tighten rules, never relax them, and no one can waive a mandatory gate in OCOS (b) as (a), but a named person with an explicit "waive mandatory gate" authority may waive one, with rationale and a heavy trace (c) the kernel guarantees only SPEC-106; everything else, including which gates are mandatory, is company configuration
- recommendation: (b) — real sites sometimes need a documented waiver (for example an engineer's written instruction), and refusing it entirely would push the decision outside OCOS's trace.
- blocks: SPEC-031, SPEC-107; architecture §4.2, §4.7, §7.4
- ANSWER:
- NOTES:

## Q-07 Which actions v1.0.0 may ever take on its own
- why it matters: decides how far "autonomous" goes in the first release once shadow mode ends. Everything else stays proposal-only or needs a person's click.
- options: (a) none: after shadow, every action needs a person's confirmation (b) low-risk communication only: requesting missing information, reminding about due commitments and unacknowledged missions, sending escalations along the configured path (c) as (b) plus issuing routine constraint-resolution missions to people inside the contractor's team
- recommendation: (b) — these are the idea's own examples of permitted actions, they change nothing physical or contractual, and they remove most of the chasing effort.
- blocks: SPEC-105; architecture §7.4, §9
- ANSWER:
- NOTES:

## Q-08 When and how an action type leaves shadow mode
- why it matters: sets the evidence bar before OCOS acts for real, and who carries that decision.
- options: (a) the pilot contractor's project director decides per action type, after at least 4 weeks in shadow and 2 weeks in confirm mode, with at least 90 % of that type's actions labelled correct and none labelled incorrect with consequences (b) as (a) but you (the owner) and the contractor decide jointly (c) no fixed criteria; decided case by case
- recommendation: (b) — fixed, written criteria protect both sides, and joint sign-off fits a first pilot of a new product.
- blocks: SPEC-145; architecture §9
- ANSWER:
- NOTES:

## Q-09 What counts as "verified"
- why it matters: "no digital record alone proves that physical work occurred" (idea §12). This decides what proof turns a report into a verified fact — for a delivery, finished work or a passed inspection — and so how much extra effort each verification costs on site.
- options: (a) always a named human verifier, with the evidence type set per kind of claim (for example delivery note photo for deliveries, inspector's record for inspections, foreman photo plus supervisor check for completed work) (b) as (a), but some evidence verifies automatically when it matches an external record exactly (for example a delivery note number matching the purchase order) (c) the contractor's current practice, described in NOTES
- recommendation: (a) for v1.0.0 — simple and safe; automatic matching can be added after the pilot shows where it is reliable.
- blocks: SPEC-088; architecture §4.4
- ANSWER:
- NOTES:

## Q-10 Records about named individuals: what is kept, who sees it, for how long
- why it matters: OCOS records who promised what, who missed which deadline, who decided. That is personal data and can feel like surveillance; in many countries it is regulated (privacy law, employee representatives). Getting this wrong can stop a pilot.
- options: (a) individuals are named inside the contractor's own team; outside companies are recorded at company level with a contact person; individual performance views are not provided; retention is the project's duration plus the contractual archive period (b) everyone named everywhere, with individual statistics (c) a policy set by the pilot contractor with their legal adviser, described in NOTES
- recommendation: (a), confirmed by the contractor's legal adviser — enough for traceability without becoming a staff-rating tool.
- blocks: SPEC-190; architecture §13
- ANSWER:
- NOTES:

## Q-11 How strong the tamper evidence must be
- why it matters: the idea requires tamper-evident records. A hash chain inside the system detects changes, but whoever runs the server could rewrite the whole chain. If the records may be used in disputes, a copy of the integrity checkpoints should live outside the operator's control.
- options: (a) hash chain only, verified by a tool (b) hash chain plus daily signed checkpoints sent to the customer (for example by email or to their storage) (c) as (b) plus a public timestamping service
- recommendation: (b) — cheap, and the operator alone can no longer rewrite history unnoticed.
- blocks: SPEC-186; architecture §6.5
- ANSWER:
- NOTES:

## Data, sources and integration

## Q-12 Source of truth and writing back to other systems
- why it matters: the idea keeps external systems authoritative for what they own. Still to decide: which records OCOS itself owns, and whether OCOS ever updates other systems (for example changing a delivery date in the purchasing system).
- options: (a) read-only towards all external systems in v1.0.0; OCOS owns only missions, commitments recorded through it, requirement states, readiness, exceptions, decisions and the trace; disagreements are shown, never resolved silently (b) as (a), plus writing back a small agreed list of fields after human approval (c) OCOS becomes the master for coordination data the pilot currently keeps in spreadsheets
- recommendation: (a) — no risk of corrupting the contractor's systems during a pilot; (c) can be added for spreadsheets the contractor is happy to retire.
- blocks: SPEC-127; architecture §4.8, §10
- ANSWER:
- NOTES:

## Q-13 Minimal import sources for planning, quantities, resources and procurement
- why it matters: the idea asks for "a small number of existing sources". Each source means an adapter to build and maintain; the right ones are whatever the pilot contractor really uses today.
- options: (a) spreadsheets only (Excel/CSV): schedule, quantities, crew and equipment assignments, purchase orders and deliveries (b) one scheduling-tool export (for example MS Project or Primavera P6) plus spreadsheets for the rest (c) the contractor's ERP or purchasing system through its API, plus (b) (d) the actual tools of the pilot, listed in NOTES
- recommendation: (d), kept to at most three sources; failing that, (b) — schedules usually live in a scheduling tool, everything else in spreadsheets.
- blocks: SPEC-120; architecture §4.8, §10
- ANSWER:
- NOTES:

## Q-14 How site reports come in and how missions reach people
- why it matters: construction coordination happens on phones and in messaging groups. The channel decides whether foremen and subcontractors will actually answer, and how much interpretation the AI must do.
- options: (a) OCOS phone-friendly web forms and links sent by email/SMS; replies come back through the link (b) as (a) plus a messaging app (for example WhatsApp Business) for sending missions and receiving replies, photos and voice notes (c) email only
- recommendation: (b) if the pilot's site team already coordinates by messaging app, otherwise (a) — meet people where they already are.
- blocks: SPEC-086, SPEC-121; architecture §4.4, §4.8, §4.9
- ANSWER:
- NOTES:

## Q-15 Beam-stack products in v1.0.0
- why it matters: the idea makes Planitor and Chantier Manager first-class integrations but requires OCOS to be useful without them. Building their adapters in v1.0.0 only makes sense if the pilot uses them and they can export their data.
- options: (a) not in v1.0.0; designed as optional adapters for the next release (b) in v1.0.0 if the pilot uses them: Planitor for planning intent and quantities, Chantier Manager for site execution and validated records (c) v1.0.0 is built primarily around them, with generic sources second
- recommendation: (b) — real data with no extra effort for the pilot, while the generic adapter contract keeps OCOS independent. Please say in NOTES whether each product has an export or API today.
- blocks: SPEC-122; architecture §10
- ANSWER:
- NOTES:

## Q-16 Acceptance and payment certification in v1.0.0
- why it matters: the idea keeps reported, measured, completed, accepted and payment-certified quantities distinct. Payment certification brings in commercial and contractual rules that v1.0.0's readiness focus does not need.
- options: (a) v1.0.0 records reported, measured, completed and accepted quantities; payment certification is out of scope (b) as (a), plus certified quantities imported read-only from the contractor's commercial system (c) v1.0.0 also prepares certification proposals
- recommendation: (a) — keeps the pilot on production; (b) is an easy follow-up.
- blocks: SPEC-024
- ANSWER:
- NOTES:

## Q-17 How the pilot company's configuration is produced
- why it matters: the idea's Company Operations Compiler reads a company's documents and drafts its configuration. It is valuable, but large; v1.0.0 needs only one company configured.
- options: (a) written by hand with the contractor, as versioned files reviewed by a person; the compiler comes later (b) a first, narrow compiler: AI drafts roles, approval limits and mission templates from the contractor's documents; a person reviews every item (c) full compiler in v1.0.0
- recommendation: (a), keeping notes on every manual step — they become the compiler's specification.
- blocks: SPEC-110; architecture §4.7, §16
- ANSWER:
- NOTES:

## Q-18 Which AI agent roles exist in v1.0.0
- why it matters: the idea describes a global steward, domain stewards, work-package coordinators and specialists. More roles mean more to test and more ways to be wrong in the first pilot.
- options: (a) work-package coordinators plus a few specialists (constraint detection, delivery tracking, evidence check, schedule-impact analysis); people act as stewards (b) as (a) plus a global steward that only ranks exceptions for people (c) the full hierarchy
- recommendation: (a) — it covers all nine v1.0.0 capabilities; stewardship stays with people until shadow data shows where an agent would help.
- blocks: SPEC-163; architecture §4.6
- ANSWER:
- NOTES:

## Openness, technology and operation

## Q-19 Open-source license and governance
- why it matters: "the Linux of construction" depends on others adopting, extending and trusting OCOS. The license decides whether companies and vendors can build closed products on it; governance decides who controls the protocol and kernel.
- options: (a) Apache-2.0 for everything; you lead as maintainer with a public proposal process for protocol and kernel changes (b) AGPL-3.0 for the kernel (anyone offering it as a service must publish changes), Apache-2.0 for protocol schemas, adapters and SDKs; same governance (c) as (a) or (b), with a neutral foundation as soon as other organisations contribute
- recommendation: (a) now, (c) later — the most adoption-friendly, with a patent grant; note that (b) better protects against a competitor running a closed fork as a service.
- blocks: architecture §11 (license row); repository LICENSE file
- ANSWER:
- NOTES:

## Q-20 Hosting and data residency
- why it matters: decides who runs OCOS for the pilot, where project data lives, and what the contractor's IT and legal teams must approve.
- options: (a) a separate (single-tenant) installation per company, run by the OCOS team in a cloud region the customer chooses (b) installed and run on the customer's own servers or cloud (c) one shared multi-company service
- recommendation: (a) for the pilot, built so (b) is always possible — simplest to support, data never mixed between companies, and true to an open-source product.
- blocks: SPEC-210; architecture §11, §12, §13
- ANSWER:
- NOTES:

## Q-21 AI model policy
- why it matters: agents send project text, photos and documents to a model. Which provider, under what privacy terms, and whether a self-hosted model is required, affects quality, cost and what the contractor's legal team will accept.
- options: (a) one commercial model provider under contract terms with no training on customer data and limited retention, behind a gateway that makes the provider replaceable; no agent framework, a thin in-house loop (b) a self-hosted open-weight model only, so no data leaves the installation (c) configurable per company: commercial provider by default, self-hosted on request
- recommendation: (a) for the pilot, with (c) as the design target — best interpretation quality now, and the gateway keeps the kernel model-independent. Please name a preferred provider in NOTES if you have one.
- blocks: SPEC-211; architecture §4.6, §11, §14
- ANSWER:
- NOTES:

## Q-22 Implementation language
- why it matters: the language shapes who can contribute, how fast a small team builds, and which libraries are available for the formats construction uses.
- options: (a) Python (typed) for kernel, agents and adapters; TypeScript for the web interface (b) TypeScript everywhere (c) a compiled language such as Go or Rust for the kernel, Python for agents and adapters (d) the language the Beam-stack products already use, named in NOTES
- recommendation: (a) unless (d) gives a strong reason — Python has the best libraries for spreadsheets, IFC/BCF (IfcOpenShell) and AI providers.
- blocks: architecture §11 (language row)
- ANSWER:
- NOTES:

## Q-23 Database and event store
- why it matters: the event log is the system's memory and must be append-only, replayable and backed up reliably.
- options: (a) PostgreSQL for both the append-only event table and the current-state tables (b) a dedicated event-store database plus PostgreSQL for current state (c) SQLite files, one per project
- recommendation: (a) — one proven open-source database, easy to self-host, ample for a pilot's volume.
- blocks: architecture §11, §13
- ANSWER:
- NOTES:

## Q-24 Product language(s)
- why it matters: the interface, the messages to site staff and the AI's interpretation of reports must work in the language the site speaks; translation adds cost to every screen and message.
- options: (a) the pilot site's language only (please name it) (b) the pilot site's language plus English (c) several languages from the start
- recommendation: (b) — the site language for users, English for the open-source community and code.
- blocks: SPEC-005; architecture §4.9
- ANSWER:
- NOTES:

## Naming

## Q-25 Name of the product
- why it matters: the idea uses "OCOS" and sometimes "OOF"; the repository is "COS". One name is needed for the code, documents, packages and any trademark check.
- options: (a) OCOS — Open Construction Operating System (b) COS, matching the repository (c) another name, given in NOTES
- recommendation: (a) — it is the idea's main name and the documents already use it.
- blocks: nothing — direction only (all documents use OCOS until answered)
- ANSWER:
- NOTES:
