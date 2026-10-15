# OCOS — how it works, in plain words

*For site managers, contractors' directors, investors and anyone who is not a software engineer.*
*Source of record: [IDEA.md](IDEA.md). Where the owner has not decided yet, this text says so and points to a question in [QUESTIONS.md](QUESTIONS.md), marked `TO-CONFIRM (Q-nn)`.*

> **About the name.** The owner's idea calls the product "OCOS" (Open Construction Operating System) and sometimes "OOF"; the repository is called "COS". This document uses **OCOS** everywhere. The final name is an open question: `TO-CONFIRM (Q-25)`.

---

## 1. OCOS in one paragraph

OCOS is open-source software that sits between the tools a construction company already uses (spreadsheets, planning software, purchase records, site reports, messages) and the people who run the work. It gathers what those tools and people say, builds one shared picture of each package of work, finds out what is still missing before that work can start, gives someone a clear job to fix each missing item, follows up until it is fixed, and keeps a complete record of who did what and why. It uses AI to read messy information and to suggest solutions, but **people with the right authority make every important decision**, and fixed, predictable rules (not AI) decide what the system is allowed to do.

The owner's long-term ambition is for OCOS to become for construction operations what Linux is for computers: a shared, open foundation that many companies, tools and specialists build on.

## 2. The problem it solves

On a building site, the plan says *what should happen*. Whether it *can* happen depends on dozens of things coming together: the previous work is finished, the crew is available, the crane is booked, the materials are delivered, the drawings are approved, the inspection has passed.

That information is spread across spreadsheets, WhatsApp groups, emails, planning software, the purchasing system and people's heads. Site managers spend a large part of their day phoning, checking and chasing to find out whether tomorrow's work can really go ahead. Problems are often discovered the morning the work was supposed to start, when the crew is already standing there.

The owner describes the core problem as the **gap between four things**:

1. **planned work** — what the schedule says;
2. **executable work** — what can actually start, because everything it needs is in place;
3. **actual execution** — what really happened on site;
4. **verified outcomes** — what has been checked and confirmed.

OCOS exists to close that gap.

## 3. Three everyday examples

**A slab pour blocked by a late rebar delivery.**
The level 3 slab is planned to be poured on Thursday. The pour needs the reinforcing steel (rebar) fixed, the formwork done, the concrete ordered, the pump booked and the pre-pour inspection passed. On Monday the steel supplier's delivery, promised for Monday, has not arrived. OCOS notices that the promise was missed, marks the slab as **not ready**, and shows what else is affected: the rebar crew will have nothing to do on Tuesday, the concrete order and the pump booking for Thursday are now at risk, and the level 4 walls planned for next week depend on this slab. It gives the buyer a clear job ("get a confirmed new delivery time from the supplier by 14:00 today"), and it prepares two or three recovery options for the site manager — for example, moving the rebar crew to the stair cores for two days and shifting the pour to Monday — each with its consequences spelled out. The site manager chooses. OCOS records the choice and follows up.

**A subcontractor's missed commitment.**
At Tuesday's coordination meeting the electrical subcontractor promised to finish the cable sleeves in the level 2 slab formwork by Wednesday evening. OCOS records that promise: who promised, what, to whom, by when. On Wednesday evening nobody has reported the sleeves as done. OCOS marks the promise as **missed**, reminds the subcontractor's foreman, and if there is still no answer it raises the issue to the person the company has named for that (for example the works manager). It does not decide who is to blame: it records the facts and the sequence of events, and leaves judgement and contractual questions to people.

**An inspection that must pass before work continues.**
Before the level 2 slab can be poured, the structural engineer's inspector must check the reinforcement. In OCOS this inspection is a **mandatory gate**: the slab cannot be marked ready to pour until the inspection result is recorded by the person entitled to record it. If the foreman reports "inspection done" in a message, OCOS records that report, but it waits for the inspector's result (or whatever proof the company requires) before it opens the gate. No AI can skip a mandatory gate. Which gates are mandatory, and whether any person may ever waive one (with a recorded reason), is still to be decided: `TO-CONFIRM (Q-06)`.

## 4. Who uses it

The idea describes two kinds of "operators" working side by side:

- **People** — site managers, planners, foremen, buyers, quality staff, subcontractors, suppliers. They provide information, do the physical work, resolve problems, make decisions and confirm results.
- **AI agents** — software assistants, each with a narrow, declared job: keeping one package of work on track, tracking deliveries, comparing documents, spotting constraints, estimating schedule impact, preparing reports.

The agents are organised like a company: a *global steward* keeps the overall picture, *domain stewards* look after areas such as planning, purchasing or quality, *work-package coordinators* each look after one package of work, and *specialists* do small precise tasks. This is a way of dividing responsibility, not a requirement for many separate programs.

Who exactly uses the first version (only the site management team, or also foremen, subcontractors and suppliers) is not decided yet: `TO-CONFIRM (Q-02)`. Which of these agent roles exist in the first version is also open: `TO-CONFIRM (Q-18)`.

## 5. What it does, day to day

- **Collects information** from a small number of existing sources — the schedule, quantities, who is assigned to what, purchase orders and deliveries, site reports — and keeps track of where each piece came from.
- **Builds the shared picture**: for each *work package* (a defined piece of work, such as "pour slab level 3, zone B"), what it needs and whether each need is met.
- **Says what is ready and what is not**, and why, in plain terms: "not ready: rebar delivery missed; formwork done; inspection not yet booked".
- **Keeps "we don't know" visible.** If nobody has said whether the pump is booked, OCOS shows "unknown". It never fills the gap with a guess. It asks for missing information only when a decision or action needs it.
- **Turns each problem into a mission**: a clear job with an objective, a person (or agent) responsible, a deadline, what counts as done and what proof is needed. A mission is not a notification: it is acknowledged, tracked, and closed only when its result is checked.
- **Follows up on promises** (from suppliers, subcontractors, colleagues) and raises overdue or unresolved issues to the right person.
- **Proposes recovery options** when something goes wrong, with the knock-on effects written out.
- **Compares what was reported with the evidence** (delivery notes, photos, measurements, inspection results) and updates the picture.
- **Keeps the whole story** of each issue: what triggered it, what was known, what was proposed, who decided, what happened and what was checked.

OCOS keeps separate things separate. "The foreman says 80 m³ were poured", "the surveyor measured 78 m³", "the work is complete", "the client accepted it" and "it was certified for payment" are five different facts, recorded separately. (Whether the first version handles acceptance and payment certification at all is open: `TO-CONFIRM (Q-16)`.)

## 6. What OCOS will never do alone

The owner designs OCOS for **gradually increasing autonomy**, never for unrestricted AI control. Some actions always need a person with the right authority, for example:

- anything that physically happens on site;
- safety-critical decisions;
- contractual commitments;
- purchases beyond the limit someone has been given;
- financial approvals;
- accepting work as meeting quality requirements;
- significant changes to who or what is assigned to the work.

On top of that:

- OCOS **never gives itself more power.** AI may suggest a new rule or a new way of working, but a responsible person must test and approve it first.
- A digital record **does not prove that physical work happened.** A ticked box is not a poured slab; evidence is judged according to what is at stake.
- When OCOS cannot resolve something within its authority, **it says so and passes it to a person.**

The first version starts in **shadow mode**: OCOS watches the real project, works out what it would do, and records it, but does not act. Only after people have compared its suggestions with what really happened may some small, low-risk actions be switched on — one type of action at a time. Which actions may ever be switched on in the first version, and who decides, is open: `TO-CONFIRM (Q-07)` and `TO-CONFIRM (Q-08)`.

## 7. How trust works

- **Every important action leaves a trail**: what triggered it, the information used, how it was interpreted, which company rule applied, what was proposed, who authorised it, what happened, the proof, and the final outcome. Failures, rejected proposals, overrides, missed deadlines and corrections are recorded too — not just successes.
- **Nothing is erased.** A mistake is fixed by adding a correction that points to the original, so the history stays complete.
- **The record is tamper-evident**: if anyone alters past records, a check will show it. This proves the record has not been changed; it does not prove the original information was true, and OCOS never claims otherwise.
- **Who said what is always clear.** A fact reported by a person, a conclusion drawn by AI, an observation that was checked, and a decision made by someone with authority are always labelled differently.
- **No hidden AI reasoning in the books.** OCOS can rebuild its full state from its records without asking the AI again. The AI's suggestions are stored as they were made.
- **Responsibility is not blame.** OCOS records who held which role (who was responsible, who did the work, who decided, who checked, who was affected) and what contributed to a problem. It does not treat an AI guess or the order in which things happened as proof of who caused a delay in the contractual sense.

How much of these records about individual people is visible, and to whom, is open: `TO-CONFIRM (Q-10)`.

## 8. Fitting the company, not the other way round

Every company organises itself differently. OCOS is meant to adapt to the company's own roles, approval limits, forms and vocabulary through a **company configuration**, without rewriting the core. The configuration is versioned and tested like software, and changes are approved by the company. Basic safety, security and legal protections cannot be switched off by ordinary configuration.

In the long run, OCOS should be able to read a company's organisation charts, procedures and approval tables and draft that configuration itself (the owner calls this the *Company Operations Compiler*), always handing ambiguities and contradictions to people. Whether a first version of this is part of v1.0.0 is open: `TO-CONFIRM (Q-17)`.

## 9. Living alongside existing software

OCOS does not ask companies to replace their tools. It connects to them. If a figure is owned by another system (for example the purchasing system owns the purchase order), that system stays the reference unless the company explicitly agrees otherwise. When OCOS and another system disagree, OCOS shows both and raises the disagreement; it does not quietly pick one. Whether the first version ever writes back into other systems is open: `TO-CONFIRM (Q-12)`.

The owner's other products (the "Beam stack") connect as optional, first-class modules: **Planitor** supplies planning intent and quantities, **Chantier Manager** supplies site execution and validated site records. OCOS must remain useful without them. Whether they are among the first version's connections depends on the pilot: `TO-CONFIRM (Q-15)`.

## 10. What v1.0.0 delivers — and what comes later

**v1.0.0** focuses on one workflow on one real project: **making sure work packages are ready and resolving what blocks them.** It:

1. imports planning, quantities, resource assignments, purchasing records and site reports from a small number of existing sources (`TO-CONFIRM (Q-13)` for which ones);
2. builds the shared picture and finds missing prerequisites, open promises and affected work packages;
3. assigns and tracks missions to people or agents to resolve problems;
4. follows up on promises and escalates overdue or unresolved issues;
5. proposes feasible recovery options with their knock-on effects written out;
6. requires authorisation for important changes;
7. checks what happened on site against the evidence and updates the picture;
8. keeps a complete trail of each issue, its responsibilities, decisions, actions and checked outcome;
9. runs first in shadow mode, before any limited automatic action is allowed.

The first pilot should be with a contractor and a type of work where quantities, dependencies, resources and recurring coordination problems can be measured. Which contractor and which work type: `TO-CONFIRM (Q-01)`.

**Later** (not in v1.0.0): coordinating many workflows across contractors, subcontractors, suppliers, engineers and project owners; libraries of reusable trade knowledge ("domain packs") and integrations built by others; a governed exchange where engineering firms, developers and consultants can contribute tested capabilities; and progressively more automation of routine problem-solving — always under appropriate human authority.

## 11. How we will know it works

OCOS must show **real improvement on site**, not just more complete records or cleverer AI. Before it is switched on, the current situation is measured (the "baseline"); afterwards the same measures are taken from real project evidence. The owner's list includes:

- how many upcoming work packages are genuinely ready to start;
- how long it takes from spotting a blocker to removing it;
- planned versus actual production, and whether milestones are met;
- hours of crews and machines standing idle that could have been avoided;
- disruptions caused by materials, and promises that were not kept;
- rework, rejected quantities and quality problems;
- how much coordination effort people spend per work package;
- how accurate OCOS is at finding constraints and predicting knock-on effects;
- wrong actions, missed prerequisites and unnecessary escalations;
- how complete and intact the responsibility records are;
- the effort OCOS itself costs people, compared with what it saves.

Which single measure decides whether v1.0.0 succeeded: `TO-CONFIRM (Q-04)`. How the baseline is taken: `TO-CONFIRM (Q-05)`. The exact definitions are in [v1.0.0_spec.md](v1.0.0_spec.md), section 11.
