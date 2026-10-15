# Questions for the owner

**Start with the decisions, not this file.** The seven questions that blocked the first build slice are now three **direction decisions**. Each one offers whole approaches with their consequences, a recommendation that follows from weighted criteria, and a check to run before the choice becomes the spec. You answer each decision with one letter. The method is in [DECIDING.md](DECIDING.md).

| Decision | Replaces | Recommended | Default if silent |
|---|---|---|---|
| [D-03 How the code starts](decisions/D-03-code.md) (answer first: it blocks the first build task) | Q-23, Q-19 | B | B, until 2026-10-29 |
| [D-01 The pilot](decisions/D-01-pilot.md) | Q-01, Q-02 | A | A, until 2026-11-15 |
| [D-02 Site facts and who may read them](decisions/D-02-site-facts.md) | Q-03, Q-13, Q-21 | B | A, until 2026-11-15 |

*Round 2, 2026-10-15. The study ([STUDY.md](STUDY.md)) reordered the questions, and the decisions were added the same day. Question ids did not change. [RESEARCH.md §9.2](RESEARCH.md#92-round-1-questions-settled-by-the-research) shows which round-1 questions the research settled. No question or decision has been answered yet.*

## How to answer the questions below

**(a) Write your answer.** Open this file on github.com, click the pencil icon (Edit), and write your answer on the `ANSWER:` line of a question. It can be one of the listed options (for example `(b)`) or your own words. Put any explanation, condition or doubt on the `NOTES:` line.

**(b) Save it.** Commit directly to `main`, with a message like `answers: Q-05, Q-07`.

**(c) Answer at your own pace.** Answer as many or as few questions as you like, in any order. Each question states a **default**: what the next working session assumes, behind a `TO-CONFIRM` marker, if the work reaches that point before you answer. A default is never treated as your answer. The marker stays until you answer, and the recommendations are suggestions, not decisions.

**(d) What happens next.** The next working session reads every newly answered question, updates the documents, removes the matching `TO-CONFIRM` markers, and writes `APPLIED: <date>` under your answer. If you change your mind later, add a line `REOPEN:` under the question with your reason. It will be treated as open again and the documents will be revised.

Each question has: why it matters; the options, simplest or least risky first; a recommendation; a default; `evidence:` (the research findings `F-nn` and `V-nn` in RESEARCH.md that inform the options); what it blocks; and `joins:`, the decision it would become part of once it is entangled with others (see [DECIDING.md §8](DECIDING.md#8-when-to-use-a-decision-and-when-a-plain-question)). D-04 and D-05 do not exist yet. They are the likely next groupings.

---

## Moved into decisions

*These ids stay valid: every `TO-CONFIRM (Q-nn)` marker in the other documents now points to the decision named here. Answer the decision, not the question.*

## Q-01 Pilot market and region
- moved to: [D-01 The pilot](decisions/D-01-pilot.md)

## Q-02 Pilot contractor, project and work type
- moved to: [D-01 The pilot](decisions/D-01-pilot.md)

## Q-23 Technology stack
- moved to: [D-03 How the code starts](decisions/D-03-code.md)

## Q-19 Open-source licence and governance
- moved to: [D-03 How the code starts](decisions/D-03-code.md)

## Q-03 How site messages reach OCOS
- moved to: [D-02 Site facts and who may read them](decisions/D-02-site-facts.md)

## Q-13 Records about named people: what is kept, who sees it, for how long
- moved to: [D-02 Site facts and who may read them](decisions/D-02-site-facts.md)

## Q-21 Which AI may read the pilot's messages
- moved to: [D-02 Site facts and who may read them](decisions/D-02-site-facts.md)

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
- joins: D-01 (the operator is part of the pilot)
- ANSWER:
- NOTES:

## Q-05 Fit the existing weekly meeting, or introduce Last Planner
- why it matters: OCOS's main output is the weekly meeting pack. Changing how the team meets adds a second change on top of OCOS; lean methods mostly fail on that change.
- options: (a) fit the contractor's existing meeting and minutes; OCOS adds a readiness section and records done / not done with reasons (b) a light Last Planner routine: commit only to ready work, record PPC and reasons (c) full Last Planner with coaching
- recommendation: (a) at the start, (b) once the pack is trusted.
- default: (a).
- evidence: F-01, F-02, F-04, F-07, F-16, F-37
- blocks: SPEC-006 (slice 2); architecture §4.4
- joins: D-01
- ANSWER:
- NOTES:

## Q-06 The measure that decides whether v1.0.0 worked
- why it matters: one or two measures with a threshold agreed before the pilot, or any result can be argued either way.
- options: (a) late discoveries — blockers first known less than 2 working days before start — down 50 % against the baseline (b) PPC up 15 points (c) work made ready ahead (d) a combination you define
- recommendation: (a) as the verdict, (b) as the method figure, with the operator's time shown beside both.
- default: (a) + (b).
- evidence: F-04, F-05, F-07; V-17
- blocks: SPEC-202
- joins: D-04, future: how the pilot is judged (with Q-07, Q-12)
- ANSWER:
- NOTES:

## Q-07 How the baseline is measured, and who sees OCOS's output meanwhile
- why it matters: if the site team acts on OCOS's warnings during the baseline weeks, the "before" picture is no longer clean.
- options: (a) look back: count late discoveries and missed promises in the last 2–3 months of exported chats and minutes, plus 3–4 weeks of PPC recorded by hand; shadow output seen only by the OCOS team (b) 4–6 weeks of silent shadow on live data (c) a similar project without OCOS, measured in parallel
- recommendation: (a) — cheaper, faster, and the same history feeds trial T2; needs the Q-13 consent.
- default: (a).
- evidence: F-32; V-17, V-18
- blocks: SPEC-142, SPEC-201
- joins: D-02 (the baseline uses the chat exports and their consent)
- ANSWER:
- NOTES:

## Q-22 Languages
- why it matters: the screens, messages and the AI must work in the languages the site uses. Darija voice notes are much harder for AI than written French; what the AI cannot read goes to a person.
- options: (a) French only; Arabic and Darija go to a person (b) French and Arabic screens and messages; the AI also reads Darija (Latin or Arabic script, and voice), accuracy measured per language (c) English only (d) other, in NOTES
- recommendation: follows Q-01; for Morocco (b), with Darija checked in trial T2. English for code and documentation in all cases.
- default: (a).
- evidence: RESEARCH §8; F-39
- blocks: SPEC-005; architecture §4.1, §4.11
- joins: D-01 (follows the market; Darija is checked in D-02's T2)
- ANSWER:
- NOTES:

## Q-20 Hosting and where the data lives
- why it matters: who runs OCOS for the pilot, where data is stored, and what the law requires (for example CNDP authorisation for transfers out of Morocco).
- options: (a) one installation per company, run by the OCOS team in a region the pilot's data law accepts (b) on the contractor's own servers or cloud (c) one shared service for several companies
- recommendation: (a), built so (b) always works.
- default: (a).
- evidence: F-35
- blocks: SPEC-210 (before go-live); architecture §11–§13
- joins: D-02 (hosting region follows the data law)
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
- joins: D-01 (depends on the pilot's tools)
- ANSWER:
- NOTES:

## Q-09 Business model and pilot terms
- why it matters: a contractor's director asks what they pay, for what, and who is accountable if it fails. It also decides what is open and what is a service.
- options: (a) free pilot for data access, feedback and a case study; later a free open core plus paid hosting, onboarding and support (b) paid pilot at a reduced fixed price, with success criteria from Q-06 (c) fully open source, revenue only from services
- recommendation: (a) for the first pilot with a written agreement on data use and the Q-06 criteria; (b) from the second.
- default: (a).
- evidence: F-14 (cost is a barrier), F-26
- blocks: IDEA_v2 §15; architecture §11
- joins: D-03 (the licence must fit the business model)
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
- joins: D-04, future: authority and when OCOS may act (with Q-11, Q-12)
- ANSWER:
- NOTES:

## Q-12 The evidence needed before OCOS acts for real
- why it matters: sets the bar before OCOS sends anything itself, and before its AI readings are used on the pilot.
- options: (a) the contractor's project director decides per action type after at least 4 weeks in shadow and 2 in confirm mode, with at least 90 % labelled correct and none wrong with consequences; the AI goes live in a language when at least 80 % of 300 test readings are right or need one correction (b) as (a), but you and the contractor decide jointly (c) case by case
- recommendation: (b) — written criteria protect both sides.
- default: (b) with the figures in (a).
- evidence: F-30, F-33, F-39
- blocks: SPEC-145; the SPEC-138 thresholds
- joins: D-04, future
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
- joins: D-05, future: v1.0.0 scope after slice 1 (with Q-17, Q-18)
- ANSWER:
- NOTES:

## Q-16 Beamstack products in v1.0.0
- why it matters: Planitor and Chantier Manager are first-class integrations in the idea, but OCOS must work without them. Their adapters only make sense if the pilot uses them and they can export data.
- options: (a) not in v1.0.0; adapters in the next release (b) in v1.0.0 if the pilot uses them (c) v1.0.0 built around them
- recommendation: (b). Say in NOTES whether each product has an export or API today.
- default: (a).
- evidence: F-26 (independence is part of the position)
- blocks: SPEC-122; IDEA_v2 §12
- joins: D-01 (only if the pilot uses Beamstack products)
- ANSWER:
- NOTES:

## Q-17 Monthly statements: how far v1.0.0 goes
- why it matters: OCOS never certifies — that is the maître d'œuvre's or Engineer's legal act — but monthly-statement disputes are where contractors lose money, and OCOS holds the evidence.
- options: (a) evidence packs per work package only (b) as (a), plus import of the bill-of-quantities lines linked to work packages, and recording of agreed (attachement) and certified quantities from documents (c) as (b), plus a draft of the contractor's own document — the attachement in Morocco, the projet de décompte in France — for the contractor's quantity surveyor to check
- recommendation: (b); (c) after the pilot.
- default: (a).
- evidence: F-20–F-25; V-12, V-13; REALITY_CHECK scenario 4
- blocks: SPEC-024 (slice 3)
- joins: D-05, future
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
- joins: D-04, future
- ANSWER:
- NOTES:

## Q-14 How strong the tamper evidence must be
- why it matters: records may be used in payment disputes. A hash chain detects changes, but whoever runs the server could rewrite the whole chain; copies of checkpoints held by the contractor prevent that. The study moved anchoring out of v1.0.0.
- options: (a) hash chain only, checked by a tool (b) plus daily signed checkpoints sent to the contractor (c) as (b) plus a public timestamping service
- recommendation: (b), after v1.0.0 — cheap to add.
- default: (a) for v1.0.0.
- evidence: F-10, F-24; V-24
- blocks: SPEC-186 (later)
- joins: D-05, future
- ANSWER:
- NOTES:

## Q-18 How the pilot company's configuration is produced
- why it matters: the company's checklists, approval tables and templates are mostly Excel and Word. For one pilot, writing them up by hand is feasible; an AI-assisted drafter pays off from the second company. The study moved the drafter out of v1.0.0.
- options: (a) written by hand with the contractor, reviewed by a person (b) the AI drafts the lists, roles and vocabulary from the company's tables; a person accepts, edits or rejects every item (c) full compiler from any document
- recommendation: (a) for the pilot, (b) next.
- default: (a).
- evidence: F-13; V-22; REALITY_CHECK scenario 5
- blocks: SPEC-110 (later)
- joins: D-05, future
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
- joins: D-03 if code package names become entangled; otherwise it stays a plain question
- ANSWER:
- NOTES:
