# OCOS — how it works, in plain words

*For site managers, contractors' directors, investors and anyone who is not a software engineer. Final v1.0.0 version, 2026-10-15.*
*Source of record: [IDEA_v2.md](IDEA_v2.md) (the owner's [IDEA.md](IDEA.md) refined by [RESEARCH.md](RESEARCH.md)). Where the owner has not decided yet, this text says so and points to a question in [QUESTIONS.md](QUESTIONS.md), marked `TO-CONFIRM (Q-nn)`.*

> **About the name.** The idea calls the product "OCOS" (Open Construction Operating System) and sometimes "OOF"; the repository is called "COS". This document uses **OCOS** everywhere. The final name is open: `TO-CONFIRM (Q-24)`.

---

## 1. OCOS in one paragraph

OCOS is open-source software that helps a site team **make next weeks' work ready**. It reads what the team already produces — WhatsApp-style messages, photos and voice notes from the site, the planning file, the Excel lists of constraints, purchases and deliveries, the action list of the weekly meeting — and keeps one up-to-date picture of each package of work: what it still needs, who promised what by when, and whether it can really start. It turns each missing item into a clear job for someone, follows up the promises, warns early when something slips, and keeps a complete record of who said, promised, decided and checked what. AI reads the messy messages and suggests actions; **a person confirms what the AI read, and people with the right authority make every important decision**. Fixed, predictable rules — not AI — decide what OCOS is allowed to do.

The owner's long-term ambition is for OCOS to become for construction operations what Linux is for computers: a shared, open foundation that many companies, tools and specialists build on.

## 2. The problem it solves

On a building site, the plan says *what should happen*. Whether it *can* happen depends on seven things coming together, which every planner knows: the **information** (drawings, answers, approvals), the **materials**, the **crew**, the **equipment**, the **space**, the **previous work** finished, and the **outside conditions** (weather, permits, neighbours).

Good site teams already manage this with a method — look ahead a few weeks, list what is missing ("constraints"), give each to someone, and only promise next week the work that is really ready. It is called *make-ready*, and it is the heart of the "Last Planner" method. Research shows it works when it is run, and that making work ready ahead is what shortens projects (RESEARCH F-04, F-07).

The trouble is keeping it up. The facts arrive in WhatsApp groups and phone calls, the constraint list is a separate spreadsheet, the promises are in the meeting minutes, and nobody has the hours each day to copy one into the other (F-09, F-14, F-16). So problems are still found the morning the crew arrives.

The owner describes the core problem as the **gap between four things**: **planned work** (what the schedule says), **executable work** (what can actually start), **actual execution** (what happened), and **verified outcomes** (what has been checked). OCOS exists to close that gap by doing the tedious part of make-ready for the team.

## 3. Five everyday situations

*(The full walk-through, with what goes wrong, is in [REALITY_CHECK.md](REALITY_CHECK.md).)*

**A slab pour blocked by a late rebar delivery.** At 10:00 on Monday, the rebar foreman writes in the site group: "the steel hasn't come", with a photo. OCOS reads it, links it to the level-3 slab and to the supplier's promise for Monday, and asks the site manager to confirm with one tap. Once confirmed, the slab still shows **expected ready** — the supplier's promise runs to the end of Monday — but its reasons now show the foreman's report, and OCOS proposes a job for the buyer ("get a confirmed new delivery time from the supplier by 14:00"). If nothing arrives by the end of the day, the promise is **missed** and the slab shows **not ready**, with what else is affected: the rebar crew has nothing to do tomorrow, the concrete order and the pump booked for Thursday are at risk, next week's walls depend on this slab. OCOS proposes two recovery options, each with its consequences. The site manager chooses. OCOS records the choice and follows up.

**A subcontractor's missed promise, learned at 7 am.** At Tuesday's meeting the electrician promised the cable sleeves by Wednesday 17:00; OCOS took that promise from the meeting's action list. Thursday at 07:05 the electrician writes "tomorrow, short of staff". OCOS marks the promise **missed**, records the new, **tentative** promise, and shows the site manager which work it blocks *before* the crew starts. If the site manager moves the crew by phone, OCOS records that decision afterwards — it never stands in the way of work on site.

**An inspection that must pass.** Before a pour, the engineer must check the reinforcement — a **hold point**: work may not go on until it is released. Other inspections are **witness points**: the inspector must be told but work may continue. The engineer will not use OCOS; the site manager records "verbal release by the engineer at 16:00" and, later, attaches the signed record. If the company allows verbal releases for that inspection, the slab can show ready at once; if the written record does not arrive in time, OCOS raises it. No AI can release a hold point.

**Monthly progress disputed.** The engineer certifies the formwork at 80 % instead of 100 %. OCOS cannot and does not certify anything, but it holds the evidence: the foreman's report with time and photos, the measurements, the releases. It produces an **evidence pack** for the disputed line.

**A company starting with its own Excel procedures.** The company's checklists, approval tables and templates are read by OCOS's AI, which drafts the company's rules; a person accepts, edits or rejects every line, and a named manager approves the result after reading plain-language examples ("if the rebar delivery is missed, the slab becomes not ready and the buyer gets a job").

## 4. Who uses it

- **Field people — foremen, subcontractors, suppliers — do not get a new app.** They keep writing, sending photos and voice notes in the channel they already use (which channel: `TO-CONFIRM (Q-03)`). OCOS reads, and when allowed, writes back there.
- **One operator per project** — usually the site manager, site engineer or planner — spends a short time each day confirming what OCOS read and approving what it proposes. In the pilot, the OCOS team may do this job: `TO-CONFIRM (Q-04)`.
- **Managers** see the readiness board, the weekly meeting pack and the evidence.
- **AI agents**, each with a narrow, declared job. In v1.0.0 there are three: an **interpreter** (reads messages, files and spreadsheets), a **coordinator** (proposes jobs, questions and recovery options for each package of work) and a **drafter** (prepares the meeting pack and messages). People act as the "stewards" who watch over the whole.

## 5. What it does, day to day

- **Reads what comes in**: messages, photos, voice notes, Excel lists, the planning file, the meeting's action list. Each one is kept as it arrived.
- **Proposes what it means** — "this is about slab L3-B; it says the rebar delivery is missed" — quoting the words it used. **A person confirms, corrects or throws it away.** Only then does the picture change. Chatter ("ok", "thanks", jokes) is set aside in one tap, and the most urgent readings come first.
- **Takes phone calls too.** The site manager can send OCOS a ten-second voice note — "ElecPro called, sleeves on Friday" — and it is recorded as their report of what ElecPro said.
- **Says what is ready and what is not, and why**, for the coming weeks: "not ready: rebar delivery missed; formwork done; inspection booked Wednesday".
- **Keeps "we don't know" visible.** If nobody has said whether the pump is booked, OCOS shows "unknown". It never fills the gap with a guess.
- **Turns each problem into a job (a "mission")** with a person responsible, a deadline, what counts as done and what proof is needed — acknowledged, tracked, closed only when checked.
- **Follows up promises** from suppliers, subcontractors and colleagues, firm or tentative, and raises overdue ones to the right person.
- **Prepares the weekly meeting**: what is ready, what is blocked and by whom, which promises fall due, and last week's score — the share of planned work actually done (PPC) and the reasons for what was not.
- **Keeps the whole story** of each issue: what triggered it, what was known, what was proposed, who decided, what happened, and what was checked.

OCOS keeps separate things separate. "The foreman says 80 m³ were poured", "the surveyor measured 78 m³", "both sides signed 78 m³", "the engineer certified 75 m³", "the work is complete" and "the client accepted it" are different facts by different people, recorded separately. How far the first version goes towards monthly payment statements: `TO-CONFIRM (Q-17)`.

## 6. What OCOS will never do alone

Some actions always need a person with the right authority: anything physical on site; safety-critical decisions; contractual commitments; purchases beyond someone's limit; financial approvals; accepting work as meeting quality requirements; significant changes to crews or equipment. In practice these are personal acts of named professionals — the engineer who releases a hold point, the maître d'œuvre who certifies a monthly statement — and no software can take them over (F-34).

On top of that:

- **OCOS never gives itself more power.** AI may suggest a new rule; a responsible person must test and approve it.
- **A digital record does not prove that physical work happened.** A ticked box is not a poured slab.
- **OCOS's messages are not formal notices.** A reminder from OCOS is sent in the name of a named person, says that it is not a contractual notice, instruction or acceptance, and goes only to people the company has listed. Anyone can be marked "do not message".
- **OCOS does not block work on site.** It records decisions made on site and checks them against the gates; it controls only what it shows as ready and what it does itself.
- When OCOS cannot resolve something within its authority, **it says so and passes it to a person.**

**Step by step.** OCOS starts in **shadow mode**: it reads the real project, works out what it would do, and records it, but sends nothing. Then **confirm mode**: it proposes, a person clicks to send. Only later, one type of action at a time and only after the evidence shows it is reliable, may small low-risk actions run on their own — for example reminders to the company's own staff. Messages to outside companies start in confirm mode. Which actions may ever run alone: `TO-CONFIRM (Q-11)`; the evidence needed and who decides: `TO-CONFIRM (Q-12)`.

## 7. How trust works

- **Every important action leaves a trail**: trigger, information used, interpretation, rule applied, proposal, who authorised, what happened, proof, outcome. Failures, rejections, overrides, missed deadlines and corrections are kept too.
- **Nothing is erased.** A mistake is fixed by a correction that points to the original.
- **The record is tamper-evident**: if anyone alters past records, a check shows it. This proves the record has not changed since it was written; it does not prove the original information was true, and OCOS never claims otherwise. How strong this protection must be: `TO-CONFIRM (Q-14)`.
- **Who said what is always clear.** A fact reported by a person, a reading proposed by AI, an observation that was checked, and a decision by someone with authority are always labelled differently. When the AI reads a foreman's message and the site manager confirms it, the fact is the foreman's; the confirmation is the site manager's; the reading was the AI's.
- **Accuracy is measured and shown.** How often the AI's readings were right, corrected or wrong is counted every week, by language.
- **Responsibility is not blame.** OCOS records who held which role and what contributed to a problem. It never treats an AI guess or the order of events as proof of who caused a delay.
- **The company keeps its data.** At any time it can export everything — records, originals, evidence, rules — in an open format, with the tool to check it.
- **Personal data is protected.** Records about named people fall under data-protection law (GDPR in Europe, law 09-08 in Morocco). What is kept, who sees it and for how long: `TO-CONFIRM (Q-13)`; where the data lives: `TO-CONFIRM (Q-20)`; which AI provider may see it: `TO-CONFIRM (Q-21)`.

## 8. Fitting the company, not the other way round

OCOS adapts to the company's roles, approval limits, checklists, forms and words — "situation", "attachement", "PV", "OPR" stay the company's words on screen — through a versioned **company configuration**, without rewriting the core. Basic safety, security and legal protections cannot be switched off. When the written procedure and what really happens differ, OCOS shows the difference to a person; it does not quietly adopt either one.

The owner's *Company Operations Compiler* will eventually draft the whole configuration from a company's documents. In v1.0.0 the configuration is written by hand with the company; a narrow version that drafts from the company's spreadsheets and tables, with every line reviewed, comes later: `TO-CONFIRM (Q-18)`. The planning rhythm OCOS fits into — the company's existing weekly meeting, or a full Last Planner routine: `TO-CONFIRM (Q-05)`.

## 9. Living alongside existing software

OCOS does not ask anyone to replace their tools. For v1.0.0 it connects to the minimum that real sites use: **Excel/CSV files, MS Project or Primavera files, one messaging channel, email, and photos or PDFs**. It exports the meeting pack and evidence packs as PDF or Excel. BIM standards (IFC, BCF, IDS, COBie) and company systems (ERP, Procore, Autodesk, Aconex) come later, through the same open connection rules — unless the pilot already depends on one: `TO-CONFIRM (Q-08)`.

If a record is owned by another system (the planning file owns the schedule, the purchasing register owns the order), that system stays the reference. When OCOS and another source disagree, OCOS shows both and raises it. Whether v1.0.0 ever writes back into other systems: `TO-CONFIRM (Q-15)`. The owner's own products — **Planitor** (planning and quantities) and **Chantier Manager** (site execution) — connect as optional modules: `TO-CONFIRM (Q-16)`.

Compared with existing products: tools such as Touchplan and vPlanner already support make-ready, but the team must type everything in; platforms such as Procore and Autodesk add AI but need everyone on the platform; WhatsApp-reading startups produce reports but no make-ready model. OCOS's difference is the combination: no typing for the field, a predictable and auditable make-ready model, and an open core a company can run itself.

## 10. What v1.0.0 delivers — and what comes later

**v1.0.0** is a make-ready assistant for **one general contractor, one project, one type of work, one site team** (market: `TO-CONFIRM (Q-01)`; contractor and work type: `TO-CONFIRM (Q-02)`). It:

1. imports the schedule, the constraint list, the purchase and delivery register, the crew plan and the weekly action list;
2. reads the site's messages, photos and voice notes and proposes what they mean, confirmed by the operator;
3. shows what is ready, not ready or unknown for the coming weeks, and why;
4. proposes jobs to clear what blocks the work and follows up promises;
5. escalates overdue or unresolved items to the right person;
6. proposes recovery options with consequences, chosen by authorised people;
7. records inspections as hold or witness points, with reported and evidenced releases;
8. keeps reported, measured, agreed and certified quantities apart and exports evidence packs;
9. prepares the weekly meeting pack, with PPC and reasons;
10. keeps a complete, tamper-evident trail;
11. runs first in shadow mode, then confirm mode; limited automatic actions come only after the pilot.

**Later** (not in v1.0.0): coordination across several companies; libraries of trade knowledge ("domain packs") and integrations built by others; BIM and platform connectors; a governed exchange of tested capabilities; a fuller agent hierarchy; and progressively more automation of routine problem-solving — always under appropriate human authority. How OCOS is offered and paid for: `TO-CONFIRM (Q-09)`; its open-source license: `TO-CONFIRM (Q-19)`.

## 11. How we will know it works

Before go-live, OCOS's reading of messages is tested on the project's own message history; a language it does not read well enough is left to people. Before OCOS influences the project, the current situation is measured (the baseline); afterwards the same measures are taken. The measures chosen are those a real site can actually produce:

- **PPC** — the share of the week's planned work actually done — and the **reasons** for what was not;
- **work made ready ahead** — the share of the look-ahead's work packages made ready in time;
- **late discoveries** — blockers first known less than two working days before the work was due to start;
- **time to clear a blocker**;
- **promises kept** by suppliers, subcontractors and colleagues;
- **how often the AI read messages correctly**, by language;
- **wrong actions and missed problems**;
- **completeness of the trail**;
- **the operator's time per day in OCOS**, against what it saves;
- **coverage** — how many of the site's facts actually reached OCOS.

Idle hours of crews and coordination effort are also tracked where the site records them. Which measure decides whether v1.0.0 worked, and the threshold: `TO-CONFIRM (Q-06)`. How the baseline is taken and who sees OCOS's output meanwhile: `TO-CONFIRM (Q-07)`. Exact definitions: [v1.0.0_spec.md](v1.0.0_spec.md), section 12.
