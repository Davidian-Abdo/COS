# OCOS — Open Construction Operating System (idea, version 2)

*Status: round 2, 2026-10-15. This is the owner's idea ([IDEA.md](IDEA.md), unchanged and still the original) refined by research ([RESEARCH.md](RESEARCH.md)) and by walking it through real situations ([REALITY_CHECK.md](REALITY_CHECK.md)). The vision and principles are the owner's; what was added or corrected is listed below and labelled in the text. `F-nn` points to a research finding; "proposal" marks a design choice by the authors; `TO-CONFIRM (Q-nn)` points to an owner question in [QUESTIONS.md](QUESTIONS.md).*

## What changed from IDEA.md and why

1. **The problem is named in the industry's own terms** — make-ready, constraints, look-ahead, weekly work plan, PPC — because the method exists and works when run; what fails is the effort to run it (§2, §3; RESEARCH F-01–F-07, F-15, F-16).
2. **Messaging is the first input channel, not one adapter among many**: field facts arrive as WhatsApp-style messages, photos and voice notes (§5; F-09, F-36, V-07).
3. **Interpretation is the main AI job, and every interpretation is confirmed by a person in v1.0.0**, with its accuracy measured (§5, §7; F-39, F-30, V-08).
4. **Foremen, subcontractors and suppliers get no new app**; one operator per project reviews what OCOS reads (§14; F-14, F-36, V-05).
5. **The weekly coordination meeting is the anchor**: its action list is the main source of commitments, and OCOS's main output is a prepared meeting pack (§3, §8; F-02, F-03, V-09).
6. **Inspections distinguish hold points from witness points**, and external verifiers (maître d'œuvre, bureau de contrôle) are recorded, not expected to log in (§9; F-17, F-18, V-11).
7. **Quantities: `reported`, `measured`, `agreed`, `certified`** — the contradictory measurement (attachement) is added; certification is another party's legal act that OCOS only records (§9; F-20–F-25, V-12).
8. **Outbound messages are never notices, instructions or acceptances**, and messages to outside companies start in confirm mode (§8, §13; F-34, V-14, V-15).
9. **Decisions taken on site are recorded afterwards**; OCOS never blocks physical work, it records it and checks gates (§13; REALITY_CHECK DC-2.4).
10. **Minimum viable integration set** replaces "any source": spreadsheets, MS Project/P6 files, one messaging channel, email, photos/PDFs; BIM standards move to the long term (§12; F-11, F-27–F-29, V-19).
11. **Data protection is a design input** (GDPR/CNIL, Morocco law 09-08/CNDP): hosting region and AI provider are pilot-blocking decisions (§13; F-35, V-21).
12. **Adoption strategy and honest positioning against existing tools are added** (§14, §15; F-14, F-16, F-26, V-03, V-27).
13. **The v1.0.0 wedge is narrowed**: a make-ready assistant for one general contractor's site team, measured with PPC, late discoveries and operator overhead (§16, §17; V-17).
14. **The success metrics are made measurable on a real site**: idle hours become best-effort; late discoveries, interpretation accuracy and coverage are added (§17; V-17, V-18).

---

## 1. Vision *(owner's, unchanged)*

OCOS is an open, adaptable operational foundation that enables construction companies to coordinate projects through a shared operational model, a configurable deterministic kernel, and a hierarchical network of AI agents and human operators.

It does not require every company to adopt the same software, organisational structure, terminology or work methods. It provides a universal protocol through which different systems, people and agents exchange operational information, coordinate responsibilities, execute authorised actions and verify outcomes.

**Core principle:** one interoperable operational state; many specialised operators; configurable company rules; continuously coordinated work; traceable responsibility; verified physical outcomes.

**Ambition:** become the Linux of construction operations — a shared, open foundation that companies, tools and specialists build on.

## 2. Problem *(sharpened)*

Construction production depends on many preconditions coming together at the right place and time. The industry already knows the seven classic ones: **information** (drawings, answers, approvals), **materials**, **labour**, **equipment**, **space and access**, **previous work**, and **external conditions** (F-06). When one is missing, planned work does not happen.

The evidence on what goes wrong:

- **Plans are unreliable.** Typical plan reliability is well below the ~70 % of weekly tasks completed at which productivity gains appear (F-04). Lack of effective look-ahead planning is a major problem in most projects studied (F-05).
- **What predicts delivery is making work ready ahead**, not just keeping weekly promises: the share of *tasks made ready* in the look-ahead predicts project duration better than weekly plan reliability (F-07).
- **The method exists but is hard to sustain.** The Last Planner System (LPS) — look-ahead, constraint log, weekly work plan from ready work only, PPC and reasons — works when it is run, but adoption fails on discipline, training and the effort of keeping logs current (F-16). Even among US general contractors, most lean practices are used by a minority (F-16).
- **The facts are in messages.** Field facts — "steel hasn't come", "sleeves tomorrow", "inspection OK" — arrive in messaging groups, phone calls and paper (F-09, F-12, F-13). Constraint logs are separate spreadsheets (F-31). Someone must turn messages into an up-to-date list of constraints and promises, and nobody has the time (F-14).
- **Discovery is late.** The cost is the morning surprise: the crew is on site and the prerequisite is missing. (Proposal: this is measured as *late discoveries*, §17.)

The fundamental problem remains the owner's: **the gap between planned work, executable work, actual execution and verified outcomes.** Version 2 adds why the gap persists even where the method is known: **keeping the make-ready picture current costs more human effort than site teams can give, and the information needed arrives in unstructured messages.**

## 3. How readiness is managed today *(new)*

- **Actors.** The site manager or superintendent and the planner decide next week's work; foremen hold the field facts; the buyer holds delivery promises; subcontractors and suppliers make promises; the design office answers questions; the maître d'œuvre / Engineer and the bureau de contrôle release, accept and certify; the client pays (RESEARCH §1.2).
- **Rhythm.** A weekly coordination meeting (site meeting, OPC meeting, LPS weekly planning) produces an action list: who promised what by when (F-02, F-03). A look-ahead of 3 to 6 weeks is where constraints should be found (F-01).
- **Tools.** Phone and messaging for facts; Excel for constraint lists, purchase registers and progress; MS Project or Primavera P6 for the schedule; paper or simple apps for daily reports; client-mandated platforms on large projects (F-09–F-13).
- **Where it breaks.** Facts in messages are not transferred to the lists; promises made in meetings are not followed up until the next meeting; misses are discovered when the crew arrives; evidence for payment disputes is scattered (REALITY_CHECK scenarios 1–4).

## 4. Core innovation *(owner's four capabilities, kept)*

1. **Universal operational input protocol** — a common, context-sensitive way to ingest and validate information from any supported source; in v1.0.0 above all from **messages and spreadsheets** (§5).
2. **Hierarchical operational agent runtime** — a configurable organisation of AI agents and human operators; in v1.0.0, three narrow agent roles and people as stewards (§7).
3. **Deterministic operational kernel** — authoritative state transitions, permissions, invariants and auditable history (§6).
4. **Company adaptation and extensibility** — configuration and domain packs adapt OCOS to each company without rewriting the kernel (§11).

OCOS is not merely a shared database, workflow engine, chatbot or collection of agents. It is a runtime that continuously converts operational information into coordinated, authorised action.

## 5. Input reality and the universal input protocol

**What arrives, and how** (F-09–F-13, F-29):

| Input | Channel | Who sends it |
|---|---|---|
| Field facts, photos, voice notes, second-hand reports ("ElecPro called…") | messaging channel (`TO-CONFIRM (Q-03)`), email | foremen, site manager, subcontractors, suppliers |
| Weekly action list / minutes | Excel, Word/PDF table | planner / OPC |
| Constraint list, purchase and delivery register, resource plan, progress sheet | Excel/CSV | planner, buyer, site manager |
| Schedule | MS Project or Primavera P6 file | planner |
| Delivery notes, inspection records, opinions, measurement sheets, certificates | photo or PDF | anyone on site; operator |

**Primitives** *(owner's, unchanged)*: entities; facts and assertions; requirements; commitments; missions; evidence; decisions; state transitions; exceptions. Version 2 adds one working object: the **intake item** — one received message, file or row batch, kept as original evidence, with the AI's proposed reading attached.

**Rules** (owner's principles, made concrete):

- Every input is kept as original evidence. The AI proposes what it means — which work package, which requirement, which promise, which quantity, which location — quoting the words it relied on. **In v1.0.0 a person confirms, corrects or discards each proposed reading** before it changes state (proposal; F-39, F-30).
- A confirmed reading becomes a `reported` fact **attributed to the person who said it**, not to the AI and not to the operator; the operator is recorded as the one who confirmed the reading.
- Second-hand facts are accepted: "Karim reports ElecPro said tomorrow" is a report by Karim naming ElecPro as the original source.
- Missing information stays explicitly `unknown`. OCOS asks for more only when a decision or safe operation needs it.
- Voice notes and messages in a language OCOS does not handle well (for example Darija) are kept and flagged for a person to read; OCOS never guesses silently (`TO-CONFIRM (Q-22)`).

## 6. Deterministic operational kernel *(owner's, unchanged in substance)*

The kernel maintains the authoritative operational state and controls consequential transitions: identity and references; event ingestion, validation, ordering and reconciliation; state machines; identity, permissions, delegation and authority; requirements, invariants and gates; mission lifecycle, deadlines and escalation; idempotent execution; append-only history with corrections; evidence references and audit integrity; configuration versioning. It stays small, testable and independent of any AI model. Generative AI interprets, investigates and proposes; deterministic mechanisms authorise, enforce, change state and record. The state can be rebuilt from recorded events without calling an AI.

## 7. Agent runtime

*(Owner's hierarchy kept as the long-term model.)* A global operations steward, domain stewards, work-package coordinators and specialist agents, each declaring scope, responsibilities, triggers, tools, permissions, output contract, completion conditions, delegation, failure policy and escalation. The hierarchy is logical, not one process per role; no steward can override mandatory safety, security, legal, quality or authority constraints.

**v1.0.0** (proposal; F-30, F-39): three narrow roles, with **people as stewards**:

- **interpreter** — reads messages, voice transcripts, photos' captions, spreadsheets, minutes and procedure tables, and proposes readings, mappings and configuration drafts;
- **coordinator** — for each work package in the look-ahead, proposes constraint-resolution missions, information requests and recovery options;
- **drafter** — prepares the weekly meeting pack, draft action lists and the text of outbound messages.

## 8. Mission and accountability protocol

*(Owner's, kept.)* Agents can assign real, traceable missions to people or agents, with objective, accountable owner, assignee, deadline, priority, preconditions, permitted actions, completion criteria, evidence, parent mission, states and verification. Five roles stay separate: accountable owner, executor, decision authority, verifier, affected party. Everything consequential is traced, including failures, rejections, overrides, missed deadlines, corrections and disputes. Integrity is never presented as proof of truth; temporal order and AI inference are never presented as contractual causation.

**Added in version 2:**

- **Commitments come mostly from the weekly meeting's action list** and from messages; each has a **firmness** (`firm` or `tentative`) set by a person — "demain inchallah" is tentative (REALITY_CHECK DC-2.3).
- **Outbound messages** (missions, reminders, information requests) are sent in the name of a named person of the company, carry a statement that they are not a contractual notice, instruction or acceptance, go only to configured recipients, and respect a per-recipient "do not message" flag. Messages to outside companies start in confirm mode (F-34, V-14, V-15).

## 9. Construction production-control engine

The initial focus is **work-package readiness and constraint resolution**, run as **LPS-compatible make-ready** (F-01, F-37):

- a **look-ahead** (default 6 weeks, configurable) of work packages taken from the schedule and the weekly meeting;
- each package's **requirements** in the seven classic categories plus permits, inspections and approvals, each `hard`, `preference` or `conditional`;
- **readiness** computed deterministically: `ready`, `expected_ready`, `unknown`, `not_ready`, with the reasons;
- **constraint-resolution missions** and follow-up of commitments;
- a **weekly work plan** of the packages the team commits to, its **PPC** and the **reasons** for every item not done, and the share of tasks made ready;
- **impact** of a disruption on downstream packages, crews, equipment and milestones, and **recovery options** proposed by agents, filtered by hard rules and chosen by people.

**Inspections** (F-17–F-19): an inspection requirement is a **hold point** (blocks until released) or a **witness point** (notification required, does not block). A release can be *reported* first (for example a verbal release on site recorded by the site manager, if the company allows it for that inspection) and *evidenced* later by the signed record; missing evidence after the configured delay raises an exception. External verifiers are recorded by name; they are not expected to use OCOS. Bureau de contrôle opinions are recorded as external facts with their document.

**Progress and payment** (F-20–F-25): reported, measured, agreed (contradictory measurement such as an attachement) and certified quantities stay distinct, as do completed and accepted work. **OCOS never certifies**; a certified quantity is recorded from the certifier's document. How far v1.0.0 goes towards monthly statements: `TO-CONFIRM (Q-17)`.

The engine distinguishes hard constraints from preferences, conditions, uncertain forecasts and company practice; local optimisation never breaks project-wide dependencies, gates or authority.

## 10. Exception resolution and controlled adaptation *(owner's, kept)*

Detect and register; identify affected entities; separate known, uncertain, assumed and missing; assign a steward; develop responses with consequences and authority; obtain decisions or run a pre-authorised action; track and verify; propose rule improvements when exceptions recur. AI may propose rules; changes are validated, tested, versioned and approved; the system never silently expands its own authority.

*Added:* differences between the company's written procedure and observed practice are recorded as `deviation` exceptions, never silently adopted either way (DC-5.2).

## 11. Company Operations Compiler

*(Owner's goal kept.)* OCOS adapts to company practice: the compiler turns organisation charts, procedures, forms, spreadsheets, approval matrices and terminology into a validated, versioned configuration, surfacing ambiguities and conflicts for people.

*v1.0.0 reality* (F-13, DC-5.1): company procedures are mostly Word, PDF and Excel. The first step is a **narrow compiler**: the interpreter drafts requirement templates, roles, grants and vocabulary from the company's tables; a person accepts, edits or rejects every item; a named company approver signs a version after reading plain-language scenario tests. Whether this narrow compiler is in v1.0.0 or the configuration is written by hand: `TO-CONFIRM (Q-18)`.

## 12. Open ecosystem and interoperability

*(Owner's model kept:* core kernel, protocol implementations, company configurations, domain packs, adapters, operator interfaces, capability exchange; OCOS coexists with existing systems, stays useful without Beam-stack products, and external systems remain authoritative for what they own.)*

**Minimum viable integration set for v1.0.0** (F-11, F-29): Excel/CSV with confirmed mappings; MS Project and Primavera P6 files (read with an open-source library); one messaging channel (`TO-CONFIRM (Q-03)`); email-in; photo/PDF upload; exports of the weekly pack and evidence packs to PDF/Excel.

**Long term**, through the same adapter contract: IFC, BCF, IDS, COBie, ERP, project platforms (Procore, Autodesk, Aconex), sensors. BIM standards matter for design and handover but play no part in day-to-day readiness on most small and mid-size sites today (F-27–F-29). Whether the pilot needs a connector to a platform it already uses: `TO-CONFIRM (Q-08)`.

**Beam stack** *(owner's)*: Planitor (planning intent, quantities) and Chantier Manager (site execution, validated records) are first-class optional adapters: `TO-CONFIRM (Q-16)`.

## 13. Human authority, safety, trust and liability

*(Owner's, kept:* progressively increasing autonomy, never unrestricted AI control; autonomous actions bounded by permissions, preconditions, constraints and risk; physical execution, safety-critical decisions, contractual commitments, purchases beyond limits, financial approvals, quality acceptance and consequential resource changes need the matching human authority; no digital record alone proves physical work; uncertainty and conflicts are shown; what OCOS cannot resolve is escalated.)*

*Added in version 2:*

- **Practice confirms the boundary** (F-33, F-34): hold-point releases, quality acceptance and payment certification are personal acts of named professionals; an AI cannot hold those roles.
- **OCOS records, it does not block, physical work.** Decisions made on site are recorded afterwards as reported decisions with their maker (DC-2.4). OCOS's gates govern what OCOS shows as ready and what OCOS itself may do.
- **Messages are not notices** (§8).
- **Data protection** (F-35): records about named people are personal data under GDPR (CNIL) or Morocco's law 09-08 (CNDP), and sending them to an AI provider abroad may need prior authorisation. Hosting, AI provider and the visibility of personal records are decided before a pilot: `TO-CONFIRM (Q-13)`, `TO-CONFIRM (Q-20)`, `TO-CONFIRM (Q-21)`.
- **Trust is earned by measured accuracy**: interpretation accuracy, detection accuracy and wrong actions are measured and shown to the pilot team (F-30).

## 14. Adoption strategy *(new)*

From the evidence on what makes field tools stick and why lean methods fail (F-14, F-16, F-36):

1. **No new app for the field.** Foremen, subcontractors and suppliers keep their phone and messaging; OCOS reads what they already send and writes to them in the same channel.
2. **One accountable operator per project** — the site manager, site engineer or planner — spends a bounded time per day confirming what OCOS read. During the pilot, the OCOS team may do this job (a "concierge" pilot): `TO-CONFIRM (Q-04)`.
3. **The weekly meeting is the anchor.** OCOS prepares the meeting pack (ready / not ready, constraints with owners, promises due, last week's PPC and reasons) and imports the action list afterwards. It fits the company's existing meeting rather than imposing LPS vocabulary: `TO-CONFIRM (Q-05)`.
4. **Value back to the person who gives data**: fewer calls to chase, a prepared meeting pack, an evidence pack for payment disputes.
5. **Overhead is measured and capped**: if operator time exceeds the agreed budget, the pilot reviews the design, not the people.
6. **The board is useful on day one**: a seeding session at go-live fills the next two weeks, and the default view shows only what matters now.
7. **The company keeps its data**: complete export in an open format at any time, so a pilot carries no lock-in risk.

## 15. Positioning *(new; F-26)*

| Existing tool | What it already does | OCOS's honest difference |
|---|---|---|
| Touchplan, vPlanner | digital LPS, constraints linked to tasks, PPC | OCOS fills the constraint log and promises from messages; the team does not type them |
| Procore, Autodesk Construction Cloud | platforms with AI agents for logs, RFIs, Q&A | OCOS needs no platform adoption by the field; deterministic readiness and authority model; open core |
| Oracle Aconex / P6 | client-mandated document control and audit trail; scheduling | OCOS works below the formal record, on daily readiness, and can feed it |
| Fieldwire, French site apps | tasks, snags, reports by app | OCOS has no field app; it reads messages |
| Wenti Labs, Sifu | AI reading WhatsApp groups into reports and tickets | OCOS turns the same messages into a make-ready model with commitments, gates, authority and replayable audit; open and self-hostable |

OCOS's position is the **combination**: capture without data entry + deterministic, auditable make-ready + open, self-hostable core for small and mid-size contractors, in French and Arabic contexts as well as English. Incumbents can copy any single piece; the open protocol and kernel are what they are unlikely to give away. How OCOS is offered and paid for: `TO-CONFIRM (Q-09)`; stand-alone or alongside a platform: `TO-CONFIRM (Q-08)`.

## 16. v1.0.0 — the wedge

**One general contractor, one project, one work type, one site team** (`TO-CONFIRM (Q-01)` for the market, `TO-CONFIRM (Q-02)` for the contractor and work type). OCOS v1.0.0:

1. imports the schedule, the constraint list, the purchase/delivery register, the resource plan and the weekly action list (minimum integration set, §12);
2. reads the project's messages, photos and voice notes and proposes what they mean; the operator confirms;
3. builds the make-ready picture: requirements, commitments, readiness with reasons, for the look-ahead;
4. proposes and, once allowed, issues constraint-resolution missions and follows up commitments;
5. escalates overdue or unresolved items along the company's path;
6. proposes recovery options with consequences, chosen by authorised people;
7. records inspections as hold or witness points, with reported and evidenced releases;
8. keeps reported, measured, agreed and certified quantities distinct and exports evidence packs;
9. prepares the weekly meeting pack and computes PPC, reasons and tasks made ready;
10. keeps a complete, tamper-evident trace;
11. runs in shadow mode first, then confirm mode, then bounded autonomy one action type at a time.

## 17. Success criteria *(owner's principle kept; metrics made measurable)*

OCOS must demonstrate measurable improvement in real operations, not just more records or cleverer agents, with a baseline taken before it influences the project.

Measurable on a real site (F-04, F-05, F-07, V-17): **PPC and reasons**; **tasks made ready** in the look-ahead; **late discoveries** (blocking constraints first known less than two working days before the planned start); **constraint resolution time**; **commitment reliability**; **interpretation accuracy** (confirmed as-is / corrected / discarded); **detection accuracy and wrong actions**; **trace completeness**; **operator overhead**; **coverage** (share of field facts that reach OCOS). Harder, best effort: idle hours with a recorded reason, coordination effort by weekly self-report. The deciding metric and threshold: `TO-CONFIRM (Q-06)`; the baseline method and who sees shadow output: `TO-CONFIRM (Q-07)`.

## 18. Long-term vision *(owner's, unchanged)*

OCOS evolves from a constraint-resolution engine into a universal construction operational runtime coordinating workflows across contractors, subcontractors, suppliers, engineering firms, owners and software systems; it progressively automates discovery of problems, routine constraint resolution, assignment, resource coordination, verification and procedure improvement, always under appropriate human authority; it grows through reusable domain packs, company configurations, operational evidence and independently developed integrations.

## 19. Guiding principle *(owner's, unchanged)*

Any company can describe how it operates. Any authorised participant can contribute operational information. Any human or agent can be assigned a bounded responsibility. Every consequential action is traceable. Every verified outcome updates the shared operational state.

OCOS is an open operational foundation that turns construction information into controlled, coordinated, accountable action.

*Name:* the documents use OCOS; the final name is `TO-CONFIRM (Q-24)`. *License and governance:* `TO-CONFIRM (Q-19)`.
