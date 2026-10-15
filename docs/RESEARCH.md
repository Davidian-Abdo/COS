# OCOS — Research: how construction coordination really works, and what it means for v1.0.0

*Status: round 2, 2026-10-15. Purpose: ground the v1.0.0 design in how construction operations actually run today. Only findings that change the design are kept.*
*Used by: [IDEA_v2.md](IDEA_v2.md), [REALITY_CHECK.md](REALITY_CHECK.md), [core_logic.md](core_logic.md), [v1.0.0_architecture.md](v1.0.0_architecture.md), [v1.0.0_spec.md](v1.0.0_spec.md), [QUESTIONS.md](QUESTIONS.md). The owner's original idea, [IDEA.md](IDEA.md), is unchanged.*

## How to read this document

Every finding has an id `F-nn` and one label:

- **[E] established evidence** — peer-reviewed research, a published standard, a law or official contract form, or an independent survey.
- **[V] vendor claim** — a statement by a company selling a product, or a survey sponsored by one. Useful for what the market says and does; not proof of effect.
- **[I] inference** — the authors' reasoning from the sources. Treat as a proposal.

Sources are listed in section 10 as `S-nn` (title, URL, date accessed). Where a page could not be opened and only a search summary was available, the source line says so; such findings are weaker than ones read in full.

---

## 1. The actors and their daily practice

### 1.1 Who coordinates readiness today

- **F-01 [E]** In the Last Planner System (LPS), the people who decide what work will be done next week are the "last planners": site managers, superintendents and trade foremen. Readiness is made in a *look-ahead* window (typically 3–6 weeks) by breaking activities into operations, identifying constraints, assigning someone to remove each one, and only committing to work that is ready. (S-01, S-02)
- **F-02 [E]** In French practice the coordination role has a name and a contract mission: **OPC** (*ordonnancement, pilotage, coordination*). The OPC plans the sequence, runs the **weekly site meeting** (*réunion de chantier*) with all trades, the maître d'œuvre and the bureau de contrôle, and writes and circulates the **minutes** (*compte rendu*) listing actions, owners and dates. (S-35)
- **F-03 [I]** Whatever the country, there is a weekly rhythm (site meeting, coordination meeting, LPS weekly work plan) whose output is a list of *who promised what by when*. That list is exactly OCOS's "commitments". The weekly meeting, not the master schedule, is where readiness is negotiated.

### 1.2 What each actor decides, reports and uses

The table summarises sources F-01 to F-30; cells without a source are **[I]** from the sum of the evidence.

| Actor | Decides | Reports | Tools really used | Will / won't adopt |
|---|---|---|---|---|
| Contractor's project manager / *directeur de travaux* | budget, buying beyond site limits, subcontract issues, recovery choices with cost | monthly progress, situations / pay applications (F-20–F-23) | Excel, email, ERP or accounting, MS Project/P6 reports | Adopts what reduces surprises and disputes; won't add data entry for themselves |
| Site manager / superintendent / *conducteur de travaux* | daily and weekly sequence, crew moves, who works where | daily report (F-12), weekly meeting inputs | phone, WhatsApp groups (F-09), Excel, paper or app daily report | Main candidate user; time is the scarce resource (F-14) |
| Foreman / *chef d'équipe* | how the task is done today | what was done, what blocked them, by message or voice | phone, WhatsApp, paper (F-09, F-12) | Field-worker acceptance is the top adoption barrier (F-14); won't install or learn a new app |
| Planner / OPC | sequence, look-ahead, weekly plan | updated schedule, meeting minutes (F-02) | MS Project, Primavera P6, Excel, Touchplan/vPlanner where LPS is run (F-04, F-31) | Will adopt tools that feed their schedule; resent double entry |
| Buyer / procurement | orders, supplier chasing | order and delivery status | ERP or Excel, email, phone | Need delivery promises in one place; rarely use site apps |
| QA/QC | inspection requests, hold-point releases (F-17) | inspection records, non-conformities | inspection forms, ITPs, Aconex/Procore on large jobs, paper on small | Will adopt if it produces the record they must keep anyway |
| HSE | stop work, permits to work | incidents, observations | paper, apps, WhatsApp photos | Out of v1.0.0 scope except as a hard constraint (permit) |
| Subcontractors | their crew and sequence | commitments in meetings, completion | phone, WhatsApp | Won't use the GC's software unless the client mandates it (F-10) |
| Suppliers | delivery dates | delivery notes | phone, email, WhatsApp | Won't log in anywhere; reply to messages |
| Design office / engineers | answers to questions, revised drawings | RFIs, drawings | email, document platforms | Information is a top cause of non-completion (F-06) |
| Maître d'ouvrage (client) and representative | acceptance, payment | — | email, Excel, document platforms | Mandates platforms on large projects (Aconex in the Gulf, F-10) |
| Maître d'œuvre / Engineer | instructions (*ordres de service*), verifies monthly statements, certifies payment (F-20, F-22) | état d'acompte / payment certificate | Excel, email | Legally responsible for verification; cannot delegate it to software (F-21) |
| Bureau de contrôle (technical controller) | issues opinions: favourable, unfavourable, suspended (F-18) | reports to the maître d'ouvrage, not to the contractor | own reports, visits | Independent by law; will not use the contractor's tool (F-18) |
| Public inspectors | permits, conformity | site book entries (Morocco, F-26) | *cahier de chantier* | Paper and official forms |

### 1.3 Where coordination fails

- **F-04 [E]** Plan reliability is low without explicit make-ready. Ballard's work found substantial productivity gains when plan reliability (PPC, percent of planned weekly tasks completed) reached about 70 %, starting from lower levels. (S-01)
- **F-05 [E]** A study of 133 Brazilian projects running LPS found that "a major problem in most projects is the lack of effective implementation of look-ahead planning", and that labour and planning causes explain most of the variance of weekly PPC. (S-04)
- **F-06 [E]** Reasons for non-completion are classically grouped into seven preconditions: information, materials, labour (crew), equipment, space, previous work and external conditions; *information* (drawings, answers, approvals) is reported as the largest cause in some studies, but this was not confirmed in a primary source (S-05 does not say it; S-04 finds labour and planning explain most PPC variance). A study of 22,636 reasons in 50 projects finds about two in three are controllable by the main contractor (S-59). (S-04, S-59) *[Study: ranking downgraded to unproven.]*
- **F-07 [E]** Simulation shows that the share of **tasks made ready** in the look-ahead (TMR) predicts project duration better than PPC: making work ready ahead is what matters, not just keeping weekly promises. (S-03)
- **F-08 [V]** Vendor-sponsored surveys attribute 48 % of rework in the US to miscommunication and poor project data, and put the cost of time spent searching for data, fixing mistakes and resolving conflicts at USD 177 billion a year in US labour. (S-23, S-24) Sponsored by software vendors; the direction is consistent with F-05, the size is unverified.

## 2. Input reality: messaging, spreadsheets, paper

- **F-09 [V; E weak]** Messaging apps are widely used for site coordination. One qualitative interview study of Malaysian industrialised-building project managers finds WhatsApp an effective channel for timely information sharing (S-21) **[E, narrow]**; a vendor blog attributes to BauInfoConsult, without year or sample, a figure of 72 % of construction stakeholders using WhatsApp for internal coordination (S-20) **[V]**. No independent survey quantifying messaging as the *main* channel was found; whether it is on the pilot site must be measured from its own chat history (*Study*). Startups that read WhatsApp groups (Wenti Labs in Singapore, Sifu) are winning large contractors precisely because no new app is needed (S-18, S-19) **[V]**.
- **F-10 [V]** On large and client-driven projects, especially in the Gulf, the client mandates a common data environment such as Oracle Aconex, with formal correspondence and an unalterable audit trail across organisations. (S-13) Small and mid-size contractors are outside this world.
- **F-11 [E]** Schedules live in MS Project or Primavera P6; both export open formats (MSPDI XML, P6 XML, XER), and an open-source library (MPXJ, LGPL) reads them and about twenty other scheduling formats. (S-50, S-51)
- **F-12 [V]** Daily reports cost foremen 30–60 minutes a day and field leaders 5–8 hours a week of paperwork (S-27); vendors describe daily reports as the main administrative pain of superintendents (S-28).
- **F-13 [E/V]** French contractors (2018): 92 % use smartphones but only 52–60 % use any specialised construction software, depending on trade (S-29, study by a vendor). Morocco: site management still relies heavily on manual processes, paper reports and fragmented communication; BIM adoption is "inconsistent and limited" (S-41) **[E]**. 93 % of Moroccan firms are very small to medium (S-42) **[E]**, and the building trades are a large part of the informal economy (S-42) **[E]**.
- **F-31 [V]** Constraint logs are usually kept as separate spreadsheets or on boards; digital LPS tools (Touchplan, vPlanner) link constraints to planned tasks and dates. (S-10)
- **F-32 [V/I]** WhatsApp's business platform bans *general-purpose* AI assistants since 15 January 2026, while explicitly allowing task-specific business automation (notifications, structured workflows). (S-22) **[V]** An OCOS number that sends missions and reads replies is task-specific and should fit; reading *existing* group chats through the official platform is not established by any source found — vendors claim it (S-18), but the mechanism and its terms were not verified **[I]**. Meta's official Groups API only lets an Official Business Account **create its own groups, capped at 8 participants**; it gives no way to join an existing site group (S-57) **[E]**. Reading existing groups therefore needs an unofficial route, against the platform's terms, or people forwarding messages *(Study)*. WhatsApp's own "export chat" feature gives a text file plus media, usable for a retrospective baseline **[I]**.

## 3. Established methods for the readiness problem

- **F-37 [E]** LPS components: master and phase (pull) schedules, look-ahead with constraint analysis (make-ready), weekly work plan built from ready work only, PPC with reasons for non-completion, and learning from those reasons. (S-01, S-02)
- **F-38 [E]** Takt planning and takt control shortened interior-phase duration substantially even in a first pilot in Finnish residential work (S-07); location-based scheduling (flowline) has been the main scheduling method in Finland since the 1980s and controls the flow of crews through locations (S-09). Both need rapid feedback and problem solving to hold the plan (S-07).
- **F-16 [E]** Why adoption fails: resistance to change, many parties involved, lack of training, weak management commitment, and the discipline of running the weekly process (S-05; confirmed in a peer-reviewed action-research study on two Saudi projects: many subcontractors and people's commitment and attitude to time were the main barriers, S-56). Among an industry-representative panel of US general contractors, only two lean practices are used by more than half, the most common (production scheduling) by 59 % (S-06, search summary of the 2025 report).
- **F-14 [V]** Technology adoption: in a Dodge Data & Analytics survey commissioned by a software vendor (B2W), 153 US and Canadian contractors, 2018, 61 % name field-worker acceptance as a top barrier and 51 % name new mobile field apps as a concern — while 95 % expect such apps to become very or extremely important (S-25). This shows a barrier, not a rejection of field apps; time is the biggest barrier (30 %), then lack of mandate (25 %), people (22 %) and cost (21 %) (Revizto 2025 survey, S-26) **[V]**.
- **F-15 [I]** The method is known and works when run; it fails on the *effort and discipline* of keeping the constraint log, the commitments and the reasons current. That effort is what OCOS can take over. OCOS must not invent a new method: it should run LPS-compatible make-ready with the vocabulary planners already know.

## 4. Inspections, acceptance, measurement and payment

- **F-17 [E]** Quality plans (Inspection and Test Plans, ITPs) distinguish **hold points** — work cannot proceed until the designated authority signs a release — from **witness points** — the inspector is notified and may attend, but work may proceed. (S-14, S-54; a government roadworks specification uses the same definitions, S-58) Specifications expect the release from the designated person; that releases are often given orally on site and written later is the authors' inference from practice, not a sourced finding **[I]**.
- **F-18 [E]** In France the technical controller (*contrôleur technique*, bureau de contrôle) is regulated (CCH L125-1 to L125-6), approved, independent of design and execution, and gives the **maître d'ouvrage** opinions that are favourable, unfavourable or suspended (S-33, S-34). The controller's opinion does not go into the contractor's system as a release; the contractor learns of it through the maître d'œuvre, the meeting minutes or a report.
- **F-19 [E]** Morocco: since 30 December 2024, construction-all-risks and ten-year liability insurance are compulsory; insurers rely on approved bureaux de contrôle to assess risk and validate design and execution (S-38, S-39). Architects are compulsory in urban areas and must supervise execution (law 12-90), and a **cahier de chantier** (site book) records works and interventions for inspectors (S-40).
- **F-20 [E]** France, public works (CCAG Travaux 2021): before month end the contractor sends a **projet de décompte** (monthly statement); the **maître d'œuvre** accepts or corrects it into the *décompte mensuel*, draws up the *état d'acompte* and notifies it; the maître d'œuvre has 7 days (art. 12.2; S-31 re-read by the study, round 2 said 10 days); monthly amounts are provisional and do not bind the parties. (S-30, S-31)
- **F-21 [E]** French case law: the maître d'œuvre's duty to check monthly statements against work really executed cannot be escaped, even after handover. (S-32)
- **F-22 [E]** Internationally: under FIDIC the Engineer issues an Interim Payment Certificate within 28 days of the contractor's statement with measurement sheets, and fairly determines the amount (S-45); in the US the AIA G702/G703 pay application states percent complete per schedule-of-values line, and over-stated percentages ("front-end loading") are a classic dispute (S-46).
- **F-23 [E]** Moroccan public works follow the CCAG-T 2016 (decree 2-14-394), (S-36, official text read in the Bulletin officiel). Art. 61: the **contractor** draws up the *attachements* (record of work executed, by bill-of-quantities item, split into finished work, unfinished work and supplies) as work progresses and at least monthly; the client has them checked and signed by its agent and the maître d'œuvre, who may correct them within **15 days**; the contractor then accepts or objects in writing within **15 days**, after which the corrected attachement is **deemed accepted**. Work that will be hidden must be recorded **contradictorily** before it becomes inaccessible. Art. 62: the client's agent draws up the *décompte provisoire* from the attachements at least monthly. In France the corresponding act is the *constat contradictoire* (CCAG Travaux 2021 art. 11), which preserves rights but never assesses responsibility (S-37).
- **F-24 [E]** Disputes: failure to properly administer the contract is the most common cause of construction disputes, and the Middle East has had the highest average dispute value in Arcadis's reports (S-47).
- **F-25 [I]** Five quantities exist in practice and are produced by different people: *reported* (foreman), *measured* (site engineer or surveyor), *agreed* (signed by both sides, or deemed accepted after the contractual period — attachement, constat contradictoire, measurement sheet), *certified* (in the maître d'œuvre's or Engineer's payment certificate), and *paid*. OCOS can hold the first three as its own records with evidence; certification is another party's legal act, which OCOS can only record as received.

## 5. Existing products and where they stop

| Product | What it covers | Where it stops for OCOS's problem | Label |
|---|---|---|---|
| Procore | project management platform; 2025 AI agents: daily log review, action item generator, foreman's morning briefing, RFI drafting; Agent Builder in open beta (S-11) | Agents automate documents inside Procore; no deterministic readiness model or commitment ledger; needs everyone on Procore | [V] |
| Autodesk Construction Cloud / Build | documents, issues, field; AI assistant answers questions from project documents with citations (S-12) | Question answering, not make-ready; platform adoption required | [V] |
| Oracle Aconex / Primavera | client-mandated document control and correspondence with audit trail, strong in the Gulf (S-13); P6 scheduling (S-51) | Formal records and schedules; nothing on daily readiness or field messages | [V] |
| Fieldwire | task lists and plans for foremen, full offline use, quick training (S-15) | Tasks are typed in by people; no readiness logic or commitments from messages | [V] |
| Touchplan, vPlanner | digital LPS: pull plans, constraints linked to tasks, PPC (S-10) | The closest to OCOS's logic; but the team must run the sessions and type the constraints | [V] |
| Trunk Tools | AI agents on construction documents; a schedule agent that monitors the schedule and alerts (S-16) | Document-centred; closed platform | [V] |
| Doxel, Buildots | computer-vision progress measured against BIM and schedule (S-17) | Progress measurement, needs BIM and capture; not constraints or commitments | [V] |
| Wenti Labs, Sifu | AI agents inside WhatsApp groups turn messages, photos, voice notes into reports and tickets, chase missing updates (S-18, S-19) | Reports and tickets, not a readiness model or authority/audit kernel; Wenti reports that 90 % accuracy is not acceptable at its volume (S-18) | [V] |
| French site apps (Finalcad, Kaliti, Archipad, Kalitics) | site reports, snag/reserve lists, OPR (S-55) | Quality and reporting, not make-ready | [V] |

- **F-39 [V]** Wenti Labs reports that, at about 20,000 AI calls a day, even 90 % accuracy would leave about 2,000 unreliable outputs daily, "a margin that is not feasible in construction", and that it dropped cheaper open models for reliability. (S-18)
- **F-26 [I] Honest gap.** Each piece exists somewhere: LPS logic (Touchplan), messaging capture (Wenti, Sifu), AI agents (Procore, Trunk Tools), audit trail (Aconex). No product found combines **(1)** capture from the messages and spreadsheets teams already use, **(2)** a deterministic make-ready and commitment model with explicit authority and replayable audit, and **(3)** an open, self-hostable core usable by small and mid-size contractors, in French and Arabic. That combination, not any single feature, is OCOS's position. It is also fragile: incumbents can add any one piece quickly.

## 6. Data standards and integration reality

- **F-27 [E]** IDS 1.0 became a final buildingSMART standard on 4 June 2024; it specifies and checks information requirements in BIM models (S-49). BCF exchanges model-based issues between BIM tools.
- **F-28 [E, weak]** A mixed-methods study (216 survey respondents and 15 interviews, Chinese AEC professionals) found only 14.75 % regularly use IFC, with frequent attribute loss (S-48; paper identified from summaries, not read; not generalisable beyond its sample). Swedish medium-sized contractors use BIM in production mostly by individual initiative (S-48b).
- **F-29 [I]** IFC, BCF, IDS and COBie are design and handover standards. On small and mid-size sites, and in Morocco where BIM adoption is limited (F-13), they play no part in day-to-day readiness. The **minimum viable integration set** is: spreadsheets (Excel/CSV), schedule files (MS Project and P6 via MPXJ), one messaging channel, email, and photos/PDFs of delivery notes, inspection records and minutes.

## 7. Adoption, trust, liability and data protection

- **F-30 [V]** Trust in AI among AEC professionals fell in 2025 (Autodesk 2025 survey of 5,594 leaders: 65 % trust AI across design-and-make industries, down 11 points; in construction 68 %, down 14 points) (S-53, from independent summaries; the page itself is blocked). The round-2 figure "45 % of firms have no AI in use" was not found and is withdrawn.
- **F-33 [E]** RICS's global professional standard on responsible AI use (effective 9 March 2026) requires professional judgement over AI outputs, transparency to clients about AI use, and governance of reliability and data. (S-52)
- **F-34 [E]** Liability practice keeps acceptance and certification with named people: hold points are released by the designated authority (F-17); the maître d'œuvre's verification duty is personal (F-21); the Engineer must "fairly determine" (F-22). An AI cannot hold these roles.
- **F-35 [E]** France/EU: CNIL rules forbid permanent surveillance of employees and require a legitimate purpose and information of staff; construction firms must frame site-access, geolocation and cascade-subcontracting data (S-44). Morocco: law 09-08; prior CNDP authorisation is in principle required to transfer personal data abroad to countries without adequate protection, with criminal penalties (S-43). Sending site messages that name workers to a foreign AI provider is such a transfer **[I]**.
- **F-36 [I]** What makes field tools stick, from F-09, F-12, F-14, Fieldwire (S-15) and Wenti Labs (S-18, F-39): no new app for field staff, input in the channel they already use (messages, photos, voice), offline tolerance, value returned to the person who gives the data (fewer calls, a ready report), and one accountable person who keeps the system current.

## 8. Regional perspective (one view among several)

The owner's ecosystem uses French and Arabic tooling, but the pilot market is not decided (`Q-01`). What differs by region and what it changes:

| Topic | France | Morocco | International (FIDIC/AIA, Gulf) | Consequence for OCOS |
|---|---|---|---|---|
| Coordination role | OPC, weekly meeting and minutes (F-02) | conducteur de travaux, architect supervision, site book (F-19) | planner, superintendent, LPS where lean | Weekly meeting output = commitments; produce a draft minutes/actions list |
| Inspections | bureau de contrôle opinions to client (F-18) | bureau de contrôle tied to compulsory insurance (F-19) | ITP hold and witness points (F-17) | Gate kinds `hold_point` / `witness_point`; external records enter as evidence |
| Measurement and payment | projet de décompte → décompte mensuel by maître d'œuvre (F-20) | attachements → décomptes provisoires (F-23) | FIDIC IPC (F-22), AIA G702/703 | Keep reported / measured / agreed / certified distinct; never certify |
| Tools | some site apps, Excel, phone (F-13) | paper, Excel, WhatsApp (F-13) | Aconex mandated on megaprojects (F-10) | Messaging + Excel first; platform connectors only if the pilot uses one |
| Data protection | GDPR, CNIL (F-35) | law 09-08, CNDP authorisation for transfers (F-35) | varies | Hosting region and AI provider are pilot-blocking decisions |
| Languages | French | French, Arabic, Darija (spoken), some Amazigh | English, Arabic | Darija voice notes are a real interpretation risk |

## 9. Validation of round-1 claims and design choices

Status: **supported**, **contradicted**, or **unproven** (no evidence either way, or evidence too weak).

| # | Claim or choice (round 1 or IDEA.md) | Status | Evidence | Consequence for OCOS |
|---|---|---|---|---|
| V-01 | The core problem is the gap between planned, executable, executed and verified work (IDEA §2) | supported | F-04, F-05, F-07 | Keep; name it in LPS terms (make-ready, TMR, PPC) |
| V-02 | Information is fragmented across spreadsheets, messaging, documents, scheduling tools (IDEA §2) | supported | F-09, F-11, F-12, F-13 | Keep; make messaging the first-class input, not one adapter among many |
| V-03 | Existing tools do not coordinate the overall production process (IDEA §2) | partly contradicted | F-26 (Touchplan, vPlanner do make-ready; Procore adds agents) | Position honestly: OCOS's difference is capture without data entry + deterministic, auditable model + open core |
| V-04 | First workflow = work-package readiness and constraint resolution (IDEA §13) | supported | F-04–F-07, F-15 | Keep; align with LPS make-ready so planners recognise it |
| V-05 | Target user implied: site management team with foremen on phone forms (round-1 Q-02 rec. (b)) | unproven (Study: was "contradicted"; F-14 shows a barrier, not a rejection) | F-14, F-36, F-12 | Keep the choice as a low-friction design proposal: no forms for foremen; one operator per project confirms what the AI reads; field staff keep messaging |
| V-06 | Inputs: imports from "a small number of existing sources" (IDEA §13) | supported, but incomplete | F-09, F-11, F-29 | Minimum set: Excel/CSV, MS Project/P6 files, one messaging channel, email, photos/PDFs |
| V-07 | Messaging is an optional channel (round-1 Q-14 options (a)/(c) without it) | contradicted, on weak evidence (Study) | F-09, F-36 | Messaging intake is core to v1.0.0; the specific channel is a question (`Q-03`) |
| V-08 | AI interpretation of messy input is a side job (round-1 §4.1) | contradicted | F-09, F-39 | Interpretation is the main AI job; every interpretation is confirmed by a person in v1.0.0, and its accuracy is measured |
| V-09 | Readiness checked against the schedule's work packages (round-1 SPEC-060 ff.) | partly contradicted | F-01, F-03, F-05 | Readiness is negotiated in the weekly meeting on the look-ahead list; the master schedule sets the window and milestones only |
| V-10 | Requirement categories (round-1 SPEC-028) | supported, missing one | F-06 | Add `external_conditions`; map categories to the seven LPS preconditions |
| V-11 | Mandatory gate for inspections (round-1 §3, Q-06) | supported, refined | F-17, F-18 | Distinguish `hold_point` (blocks) from `witness_point` (does not block); external opinions enter as evidence |
| V-12 | Reported / measured / completed / accepted / certified kept distinct (IDEA §8) | supported | F-20–F-25 | Keep; add `agreed` quantity (contradictory measurement); certified only recorded, never computed |
| V-13 | Payment certification maybe out of v1 (round-1 Q-16) | supported, with nuance | F-20, F-23, F-24 | OCOS never certifies; v1 may assemble evidence for attachements (question `Q-17`) |
| V-14 | AI never verifies, accepts or decides human-authorisation actions (SPEC-103) | supported | F-33, F-34 | Keep; add: outbound messages are never formal notices or instructions |
| V-15 | Autonomy candidates: information requests, reminders, escalations (IDEA §12, round-1 Q-07) | unproven | F-14, F-36 (relationship risk); no evidence on automated chasing of subcontractors | Start internal-only; external recipients in `confirm`; per-recipient opt-out |
| V-16 | Shadow mode first (IDEA §13) | supported, but with a gap | F-30 (trust), F-32 | Shadow is feasible only if inputs flow in passively; the operator's confirmations are the labels; design a channel that works in shadow |
| V-17 | Success metrics M-01…M-11 measurable (round-1 spec §11) | partly contradicted | F-04, F-05, F-07, F-12 | PPC, reasons and TMR are standard and cheap; idle hours with reason codes are rarely recorded (unproven); coordination effort needs a time log; add "late discoveries" and extraction accuracy |
| V-18 | Baseline from silent shadow for 4–6 weeks (round-1 Q-05 rec.) | unproven | F-32 (chat export), F-05 | Retrospective baseline from exported chat history and minutes is cheaper; PPC baseline needs 3–4 weekly meetings |
| V-19 | Standards IFC/BCF/IDS as adapters (IDEA §11) | supported as long term, not v1 | F-27–F-29 | Out of v1.0.0; extension points only |
| V-20 | External systems remain authoritative (IDEA §11) | supported | F-10, F-18, F-20 | Keep; the bureau de contrôle's report and the maître d'œuvre's certificate are external records |
| V-21 | Records about individuals are sensitive (round-1 Q-10) | supported | F-35 | Stronger: GDPR/CNIL and CNDP make hosting and AI provider choices pilot-blocking |
| V-22 | Company Operations Compiler reads procedures and spreadsheets (IDEA §10) | unproven | F-13 (procedures largely paper/Excel); no product evidence | v1: AI-assisted mapping of spreadsheets and procedure tables, every item reviewed by a person |
| V-23 | Hierarchical agent runtime with global and domain stewards (IDEA §6) | unproven for v1 | F-30, F-39 | v1: three narrow agent roles; people are stewards |
| V-24 | Tamper-evident append-only audit (IDEA §7) | supported as a market expectation | F-10, F-24 | Keep; disputes make it valuable; integrity ≠ truth stays explicit |
| V-25 | Python back end (round-1 Q-22 rec.) | supported with one caveat | F-11 | Schedule reading relies on MPXJ (Java); isolate it in an adapter (Python wrapper to verify during build) |
| V-26 | "OCOS works without Beamstack products" (IDEA §11) | supported | F-13, F-26 | Keep; Beamstack remains optional |
| V-27 | Adoption is not addressed in IDEA.md | gap | F-14, F-16, F-36 | Add an adoption strategy: no field app, one operator, weekly meeting as the anchor, concierge pilot |

### 9.1 Specific checks requested

- **Target user and workflow vs reality.** The reality is a weekly make-ready rhythm run by the site manager / planner (F-01–F-03), with field facts arriving by message (F-09). v1.0.0's operator is therefore the site manager, site engineer or planner of one project, not the foreman (V-05, V-09).
- **Input assumptions.** Messaging-first: realistic and necessary (F-09), with a platform-policy and technical risk on reading groups (F-32). Spreadsheets: realistic for constraint logs, purchase and delivery lists, resource plans (F-12, F-13). Phone forms for foremen: not realistic (F-14).
- **Shadow mode and metrics on a real site.** Measurable: PPC and reasons (if the weekly meeting exists), TMR, late discoveries, commitment reliability, extraction accuracy, operator minutes. Hard: idle hours and coordination effort without self-reporting (V-17).
- **Autonomy vs liability.** The human-authorisation list matches practice (F-34). Risk not covered in round 1: an automated message to a subcontractor or supplier may be read as a formal notice or instruction (an *ordre de service* in French contracts is the maître d'œuvre's act, F-20) **[I]**. New rule: OCOS messages are never notices, instructions or acceptances.
- **Minimum viable integration set.** F-29: Excel/CSV, MS Project/P6 files, one messaging channel, email-in, photo/PDF upload; exports of the weekly pack to PDF/Excel. No ERP, BIM, or platform connector unless the pilot uses one (`Q-08`).

### 9.2 Round-1 questions settled by the research

| Round-1 question | How it was settled | Now |
|---|---|---|
| Q-03 look-ahead window and checkpoint | LPS practice gives defaults: look-ahead 6 weeks (configurable 3–6), weekly work plan built from `ready` packages at the weekly meeting (F-01, F-37). Company rhythm is configuration. | Specified as configurable defaults (SPEC-065) |
| Q-09 what counts as verified | Hold-point releases, inspection opinions and measurement sheets are defined by the contract's ITP and the company's procedures (F-17, F-18, F-23); v1 rule: a named human verifier, evidence per configured rule. | Specified (SPEC-088); evidence types are company configuration |
| Q-13 import sources | Minimum viable integration set (F-11, F-29). | Specified (SPEC-120); the messaging channel becomes new Q-03 |
| Q-18 agent roles | Trust and accuracy evidence (F-30, F-39) favour few, narrow roles. | Specified: three roles (SPEC-163) |
| Q-14 field reports and channels | Not dropped: replaced by the sharper new Q-03 (which messaging channel), since messaging is now core (V-07). | Q-03 |
| Q-22 + Q-23 language and database | Merged into one technology question (new Q-23), with the MPXJ caveat (V-25). | Q-23 |

Round-1 → new numbering: Q-01→Q-02, Q-02→Q-04, Q-04→Q-06, Q-05→Q-07, Q-06→Q-10, Q-07→Q-11, Q-08→Q-12, Q-10→Q-13, Q-11→Q-14, Q-12→Q-15, Q-15→Q-16, Q-16→Q-17, Q-17→Q-18, Q-19→Q-19, Q-20→Q-20, Q-21→Q-21, Q-24→Q-22, Q-22+Q-23→Q-23, Q-25→Q-24. New: Q-01 pilot market, Q-03 messaging channel, Q-05 planning method, Q-08 positioning, Q-09 business model. None of the round-1 questions had an answer, so nothing was carried over.

## Study verification

*Independent study, 2026-10-15 ([STUDY.md](STUDY.md)). Each source was re-opened; "summary" means only a search-engine or third-party summary could be read. Verdicts: **confirmed**, **corrected** (the claim was changed), **downgraded** (label weakened), **replaced** (a better source now carries it). The finding texts above already carry the corrections.*

### Weak sources named by round 2

| Source → finding | Verdict | What the study found | Source now |
|---|---|---|---|
| S-05 → F-16 | confirmed (bibliography) | Perez & Ghosh 2018, ECAM 25(9); the text is paywalled, so the barrier list is backed by S-56 | S-05 + S-56 [E] |
| S-06 → F-16 | confirmed | 59 % for production scheduling, only two lean practices used by more than half of GCs: two independent summaries agree | S-06 (summary) [E] |
| S-26 → F-14 | confirmed, figure corrected | Read in full: time 30 % (not "about one third"), mandate 25 %, people 22 %, cost 21 % | S-26 [V] |
| S-36 → F-23 | replaced, claim corrected | Official text read: the **contractor** draws up attachements; 15 + 15 days, then **deemed accepted**; hidden work recorded contradictorily; the client's agent draws up the décompte provisoire | S-36 (Bulletin officiel) [E] |
| S-37 → F-23 | replaced | The old source was a job-advert page; the French equivalent is the *constat contradictoire*, CCAG Travaux 2021 art. 11 | S-37 [E] |
| S-48 → F-28 | downgraded | 14.75 % comes from 216 Chinese respondents; not general | S-48 [E, weak] |
| S-53 → F-30 | corrected | 65 % is across design-and-make industries (−11); construction is 68 % (−14); "45 % no AI" not found, withdrawn | S-53 (summaries) [V] |

### Findings the top 10 changes rest on

| Finding (round-2 change) | Verdict | What the study found | Source now |
|---|---|---|---|
| F-09 messaging is the main input (change 1) | **downgraded** [E/V] → [V; E weak] | One qualitative interview study (Malaysia) and one undated vendor figure; startups' traction is vendor-reported. Plausible, not quantified | S-20, S-21, S-18 |
| F-32 reading existing groups (change 1) | **strengthened**, consequence changed | The official Groups API only creates business-owned groups of ≤ 8 people; OCOS cannot join an existing site group compliantly | S-57 [E] |
| F-14 field-app rejection (change 3) | **downgraded** [E] → [V] | Vendor-commissioned survey, 153 contractors, 2018; it shows worker acceptance as a barrier, and 95 % expect field apps to matter. V-05 becomes "unproven"; "no field app" stays as a design proposal | S-25 [V] |
| F-01 last planners, look-ahead (change 4) | stands | Primary academic sources, not re-opened | S-01, S-02 [E] |
| F-04 PPC ~70 % (change 4) | confirmed | Ballard 2000: improving plan reliability to ~70 % PPC gave substantial productivity gains. "Typical reliability is well below 70 %" (IDEA_v2 §2) is inference, now labelled | S-01 [E] |
| F-07 tasks made ready (change 4) | confirmed, scope noted | The result comes from computer simulation, not field data | S-03 [E, simulation] |
| F-16 why LPS adoption fails (change 4) | confirmed, strengthened | Peer-reviewed action research on two Saudi projects: many subcontractors, people's commitment and attitude to time | S-05, S-06, S-56 [E] |
| F-05 look-ahead rarely run well | confirmed | Abstract read: "lack of effective implementation of look-ahead planning"; work force and planning explain most PPC variance | S-04 [E] |
| F-06 seven preconditions; information largest | **corrected** | The seven categories stand; "information is the largest cause" was not found in a primary source → unproven | S-04, S-59 [E] |
| F-17 hold vs witness points (change 6) | confirmed; one part split off | Definitions confirmed by a government specification; "verbal release first, paper later" is inference [I] | S-14, S-54, S-58 |
| F-20 French monthly statements (change 7) | **corrected** | The maître d'œuvre has 7 days (art. 12.2), not 10; monthly amounts provisional, confirmed | S-31 [E] |
| F-21, F-22, F-24 certification and disputes (change 7) | stand | Not re-opened; no design figure depends on them | S-32, S-45, S-46, S-47 |
| F-23 Moroccan attachements (change 7) | **corrected** | See S-36 above. New design consequences: a deemed-acceptance deadline, and a contradictory record of work before it is hidden (pilot domain pack) | S-36 [E] |
| F-25 the quantity kinds (change 7) | confirmed in substance | `agreed` = signed by both sides **or deemed accepted**; the four kinds stay | S-36, S-37 [I on [E]] |
| F-39 90 % is not enough at volume (change 2) | confirmed | Quote and named customers checked in the article | S-18 [V] |

**Counts.** 17 sources re-opened: 8 confirmed (S-01, S-03, S-04, S-05, S-06, S-18, S-22, S-26), 2 corrected (S-31, S-53), 4 downgraded (S-20, S-21, S-25, S-48), 2 replaced (S-36, S-37), 1 inconclusive (S-30, members-only; S-31 covers it). 4 sources added (S-56–S-59). Findings: 19 checked: 10 confirmed or standing (F-01, F-04, F-05, F-07, F-17, F-21, F-22, F-24, F-25, F-39), 4 corrected (F-06, F-20, F-23, F-30), 3 downgraded (F-09, F-14, F-28), 2 strengthened (F-16, F-32).

**What this changes in the design.** (1) Messaging stays the main input, but as a hypothesis the channel trial must measure on the pilot's own chat history (ARCH §17). (2) "OCOS joins the existing site groups" is not available compliantly, so intake depends on people forwarding to an OCOS number and on chat exports (Q-03). (3) The quantity kinds hold; the domain pack gains a contradictory record of work before it is hidden, and `agreed` includes deemed acceptance (ARCH §4.6, §4.9).

## 10. Sources

All accessed 2026-10-15. "Search summary" means the page itself could not be opened (blocked or certificate error) and the content comes from the search engine's summary of it.

| Id | Title | URL |
|---|---|---|
| S-01 | Ballard, G. (2000) *The Last Planner System of Production Control*, PhD thesis, University of Birmingham | https://etheses.bham.ac.uk/4789/ |
| S-02 | Hamzeh, Ballard, Tommelein (2008) *Improving Construction Work Flow – The Connective Role of Lookahead Planning*, IGLC 16 | https://iglc.net/papers/Details/572 |
| S-03 | Hamzeh, Zankoul, Rouhana (2015) *How can 'tasks made ready' during lookahead planning impact reliable workflow and project duration?*, Construction Management and Economics 33(4) | https://ideas.repec.org/a/taf/conmgt/v33y2015i4p243-258.html |
| S-04 | Bortolazza, Formoso (2006) *A Quantitative Analysis of Data Collected From the Last Planner System in Brazil*, IGLC 14 | https://iglc.net/papers/Details/415 |
| S-05 | Perez, A.M., Ghosh, S. (2018) *Barriers faced by new-adopter of Last Planner System®: a case study*, Engineering, Construction and Architectural Management 25(9) 1110–1126 (bibliography checked; text paywalled) | https://www.emeraldinsight.com/doi/abs/10.1108/ECAM-08-2017-0162 |
| S-06 | LCI / Dodge Construction Network (2025) *Discover Lean: Insights from Over a Decade of Industry Research*; figure confirmed in the press release of 24 Apr 2025 (search summary; page blocked) | https://leanconstruction.org/resources/lci-research/dodge-report-2025/ ; https://www.businesswire.com/news/home/20250424215298/en/ |
| S-07 | Lehtovaara et al. (2019) *Implementing Takt Planning and Takt Control into Residential Construction*, IGLC 27 | https://acris.aalto.fi/ws/portalfiles/portal/36336144/Lehtovaara_et_al._2019_Implementing_Takt_Planning_and_Takt_Control_Into_Residential_Construction.pdf |
| S-09 | Kenley, Seppänen (2005) *Case Studies of Using Flowline for Production Planning and Control*, CIB | https://aaltodoc.aalto.fi/items/5bdec109-161f-4cf2-b86b-297bfe19c25f |
| S-10 | Touchplan, *Technology and constraint logs* (vendor blog; search summary) | https://touchplan.io/blog/technology-and-constraint-logs |
| S-11 | Procore (15 Oct 2025) *Procore Advances the Future of Construction with New AI Innovations at Groundbreak 2025*, press release | https://www.businesswire.com/news/home/20251015796723/en/Procore-Advances-the-Future-of-Construction-with-New-AI-Innovations-at-Groundbreak-2025 |
| S-12 | Autodesk University 2025, *Unlock Your AI Genius with Autodesk Assistant in Construction Cloud* | https://www.autodesk.com/autodesk-university/class/Unlock-Your-AI-Genius-with-Autodesk-Assistant-in-Construction-Cloud-2025 |
| S-13 | Oracle, *Aconex Construction Management* (Middle East) | https://www.oracle.com/middleeast/construction-engineering/aconex/ |
| S-14 | Aconex Help, *Hold Point / Witness Point* | https://help.aconex.com/implementation/hold-point--witness-point/ |
| S-15 | Fieldwire, *Field management software* | https://www.fieldwire.com/lp/field-management-software/ |
| S-16 | *Trunk Tools Secures $40 Million to Bring ChatGPT-Style AI to Construction Sites* (2025) | https://hiverlab.com/trunk-tools-secures-40-million-ai-to-construction |
| S-17 | Doxel, FAQs | https://doxel.ai/faqs |
| S-18 | e27 (2026) *The 30-second report: how one startup is killing construction's paperwork problem* (Wenti Labs) | https://e27.co/the-30-second-report-how-one-startup-is-killing-constructions-paperwork-problem-20260803/ |
| S-19 | Sifu on Product Hunt | https://www.producthunt.com/products/sifu |
| S-20 | Valoon, *Construction Site Communication: Why WhatsApp Is Not Enough* (vendor, cites BauInfoConsult) | https://valoon.chat/en/blog/construction-site-communication-and-whatsapp/ |
| S-21 | *An Ability of WhatsApp Usage in Industrialised Building System (IBS) Construction Project*, iJIM | https://online-journals.org/index.php/i-jim/article/view/10548 |
| S-22 | respond.io, *WhatsApp general-purpose chatbots ban* (2025–2026) | https://respond.io/blog/whatsapp-general-purpose-chatbots-ban |
| S-23 | PlanGrid & FMI (2018) survey, Autodesk blog | https://www.autodesk.com/blogs/construction/survey-plangrid-fmi/ |
| S-24 | Autodesk & FMI (2018) *Construction Disconnected* | https://www.autodesk.com/blogs/construction/construction-disconnected-fmi-report/ |
| S-25 | Construction Dive (23 May 2018) *Dodge: Worker acceptance, IT integration top challenges to construction tech* | https://www.constructiondive.com/news/dodge-worker-acceptance-it-integration-top-challenges-to-construction-tec/524111/ |
| S-26 | Construction Management, *Technology adoption* (Revizto 2025 *Bridging the Gap* report, 2,000+ AEC professionals; read in full) | https://constructionmanagement.co.uk/technology-adoption/ |
| S-27 | Rhumbix, *Why your best field foremen are spending 6 hours a week on paperwork* (vendor) | https://www.rhumbix.com/blog/why-your-best-field-foremen-are-spending-6-hours-a-week-on-paperwork-and-what-its-costing-you |
| S-28 | LetsBuild, *Construction daily reports: a big pain for superintendents and foremen* (vendor) | https://letsbuild.com/blog/construction-daily-reports |
| S-29 | Batiweb (11 Jun 2018) *Finalcad alerte sur la nécessité de digitaliser le BTP* | https://www.batiweb.com/actualites/vie-des-societes/finalcad-alerte-sur-la-necessite-de-digitaliser-le-btp-etude-2018-06-12-32744 |
| S-30 | FFB, *CCAG-Travaux : le paiement des situations mensuelles* | https://www.ffbatiment.fr/gestion-entreprise/passer-executer-un-marche/facturation-paiement/dossier-ba/ccag-travaux-paiement-situations-mensuelles |
| S-31 | marche-public.fr, *CCAG Travaux 2021, article 12 – modalités de règlement des comptes* | https://www.marche-public.fr/CCAG-travaux2021/12-modalites-reglement-comptes.htm |
| S-32 | Seban Avocats (2021) *Manquements du maître d'œuvre : absence de vérification des projets de décomptes mensuels* | https://www.seban-associes.avocat.fr/manquements-du-maitre-doeuvre-absence-de-verification-des-projets-de-decomptes-mensuels |
| S-33 | Techniques de l'Ingénieur, *Construction contracts – legislative and regulatory framework* | https://techniques-ingenieur.fr/en/resources/article/ti262/construction-contracts-c68/v4/legislative-and-regulatory-framework-1 |
| S-34 | AQC (2024) *Intervention du contrôleur technique* (leaflet) | https://qualiteconstruction.com/wp-content/uploads/2024/05/Plaquette-Intervention-Controleur-Technique-AQC.pdf |
| S-35 | Obat, *L'OPC chantier : définition, missions* | https://www.obat.fr/blog/opc-chantier/ |
| S-36 | Morocco, decree 2-14-394 approving the CCAG-T, *Bulletin officiel* n° 6470 (2 Jun 2016), arts. 61–62 (read in full) | https://www.marchespublics.gov.ma/pmmp/download/pdf/2-14-394-fr.pdf |
| S-37 | Code de la commande publique (site), *Constatations et constats contradictoires (CCAG Travaux)*, art. 11 | https://www.code-commande-publique.com/constatations-et-constat-contradictoires-ccag-travaux/ |
| S-38 | Wafir (2026) *Assurance décennale BTP Maroc 2026 : obligation* | https://wafir.ma/fr/guide/assurance-decennale-btp-maroc-2026-obligation-5-assureurs |
| S-39 | Médias24 (7 Aug 2025) *Métiers de l'immobilier : travailler dans un bureau de contrôle* | https://medias24.com/2025/08/07/metiers-de-limmobilier-travailler-dans-un-bureau-de-controle/ |
| S-40 | Bladi.net, *Lois constructions Maroc* (law 12-90, cahier de chantier) | https://www.bladi.net/lois-constructions-maroc.html |
| S-41 | AllAfrica (Nov 2024) *Maroc : El Jadida – opportunités et défis de la digitalisation dans le secteur de la construction*; and UNESCO Open Science record (Dec 2025) | https://fr.allafrica.com/stories/202411220641.html |
| S-42 | FNH, *Les TPME représentent 93 % des entreprises marocaines*; TelQuel (28 May 2025) informal enterprises | https://fnh.ma/article/actualite-economique/les-tpme-representent-93-des-entreprises-marocaines-en-2019 ; https://telquel.ma/instant-t/2025/05/28/au-maroc-le-nombre-dentreprises-informelles-a-augmente-en-dix-ans_1935062/ |
| S-43 | Upsilon Consulting, *International personal data transfer in Morocco* (law 09-08, CNDP) | https://upsilon-consulting.com/en/international-personal-data-transfer-morocco/ |
| S-44 | Legiscope, *RGPD BTP construction* | https://www.legiscope.com/blog/rgpd-btp-construction.html |
| S-45 | Kayrouz & Associates, *Unpaid interim payment certificates in UAE construction projects* (FIDIC) | https://www.kayrouzandassociates.com/insights/unpaid-interim-payment-certificates-in-uae-construction-projects |
| S-46 | JMCO, *AIA Billing: the complete guide for contractors* | https://www.jmco.com/articles/accounting-controllership/aia-billing-the-complete-guide-for-contractors/ |
| S-47 | Middle East Construction News, *The cost of construction disputes in the Middle East* (Arcadis) | https://meconstructionnews.com/16782/the-cost-of-construction-disputes-in-the-middle-east |
| S-48 | OpenBIM interoperability mixed-methods study, 216 respondents, Chinese AEC professionals (search summaries; paper not read), Salford repository; S-48b: Chalmers, *BIM use in the production process among medium sized contractors* | https://salford-repository.worktribe.com/OutputFile/1497837 ; https://research.chalmers.se/en/publication/239225 |
| S-49 | buildingSMART, *Information Delivery Specification (IDS)* (v1.0 final, 4 Jun 2024) | https://www.buildingsmart.org/standards/bsi-standards/information-delivery-specifications-ids/ |
| S-50 | MPXJ, open-source schedule file library (LGPL) | https://github.com/joniles/mpxj |
| S-51 | Oracle, *P6 Professional import/export file formats* | https://docs.oracle.com/cd/F25600_01/English/admin/p6_pro_importing_exporting/import_export_file_formats.htm |
| S-52 | RICS, *Professional conduct: responsible use of AI* (standard effective 9 Mar 2026) | https://www.rics.org/news-insights/wbef/professional-conduct-responsible-use-ai |
| S-53 | Autodesk (2025) *State of Design & Make* (page blocked); figures from DCD's summary and search summaries of Autodesk's construction blog | https://dcd.com/articles/key-insights-from-autodesks-2025-state-of-design-make-report/ ; https://www.autodesk.com/blogs/construction/state-of-design-make-spotlight-construction/ |
| S-54 | Infralens, *Hold point release* | https://infralens.in/qaqc/generic/hold-point-release |
| S-55 | La Fabrique du Net, *Logiciels de suivi de chantier* (comparison) | https://www.lafabriquedunet.fr/logiciels/gestion/suivi-de-chantier/ |
| S-56 | AlSehaimi, Tzortzopoulos, Koskela (2014) *Improving construction management practice with the Last Planner System: a case study*, ECAM 21(1) 51–64 | https://eprints.hud.ac.uk/id/eprint/20855/ |
| S-57 | Meta, *WhatsApp Cloud API – Groups* (developer documentation) | https://developers.facebook.com/docs/whatsapp/cloud-api/groups |
| S-58 | Northern Territory Government, *Hold points and witness points for roadworks* v5.4 (search summary) | https://dli.nt.gov.au/__data/assets/pdf_file/0004/1357834/hold-points-and-witness-points-for-roadworks-v5.4.pdf |
| S-59 | Lagos, Alarcón (2021) *Composition and Impact of Reasons for Noncompletion in Construction Projects*, IGLC 29 | https://iglc.net/Papers/Details/1938 |

Source count: **58 source ids** (S-01 to S-59; S-08 not used), **62 distinct URLs**. S-56 to S-59 and the corrected S-05, S-06, S-26, S-36, S-37, S-48 and S-53 lines were added by the study (see Study verification).
