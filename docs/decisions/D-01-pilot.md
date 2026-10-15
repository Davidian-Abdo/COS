# D-01 The pilot: which contractor, where, on what work

*Opened 2026-10-15 under [DECIDING.md](../DECIDING.md). Status: **open**.*

## Your answer

- CHOICE:
- WEIGHTS:
- NOTES:
- DEFAULT-IF-SILENT: A, expires 2026-11-15. This is the QUESTIONS.md default (Q-01 (b), Q-02 (a)): French interface and Moroccan contract words in the test data, and the slab-pour checklist. Nothing market-specific beyond that is built.

*If you already have a contractor who would pilot, write its name, city and type of work in NOTES. **A willing contractor beats any score.** The session takes the approach that matches it (Q-01's recommendation).*

## What is being decided

- **Replaces** Q-01 (pilot market) and Q-02 (contractor, project and work type). The country decides the contract words, inspections, data law and languages. The work type decides the first prerequisite list. One cannot be chosen well without the other.
- **Blocks:** SPEC-002 and SPEC-066; the slice-1 exit check ("the board matches the site manager's own view"); trial T2's test data and languages.
- **Later joins it:** Q-04 (operator), Q-05 (weekly meeting), Q-08 (platform), Q-16 (Beamstack products), Q-22 (languages).
- **D-02 depends on it** (data law, languages).

## The approaches

- **A. Morocco, structural frame.** A mid-size Moroccan contractor with its own crews; the frame of a residential block (formwork, rebar, pours). This is REALITY_CHECK's cast as written.
- **B. Morocco, finishing works.** The same kind of contractor, on floors shared by many subcontractors.
- **C. France, structural frame.** A French contractor of the same size on the same work.
- **D. Gulf or wider MENA, FIDIC project.** A contractor on a client-run project.

## Scoreboard (default weights)

| Criterion (weight) | A | B | C | D |
|---|---|---|---|---|
| Learning (5) | 5: widest gap (paper, Excel, WhatsApp, F-13); Darija tests the hardest reading case | 4: more parties, but prerequisites are fuzzier and harder to measure | 3: more software already in use (F-13), no Darija | 2: the client's platform already holds the formal record (F-10) |
| Safety (4) | 3: CNDP authorisation for transfers abroad (F-35); informal subcontractors (F-13) | 3: same, plus more outside companies named in messages | 4: GDPR and CNIL are well documented (F-35) | 3: varies by country |
| Speed (3) | 4: one checklist (the pour), one site team | 3: a checklist per trade, many relationships | 3: an OPC and the minutes already exist (F-02), but more competing tools | 2: client approvals, platform onboarding |
| Cost (2) | 4 | 3 | 3 | 2 |
| Reversibility (2) | 3: a pilot is months of a relationship | 3 | 3 | 3 |
| **Total** | **63** | 53 | 52 | 38 |

**Recommendation: A.** It teaches the most and is the cheapest path to a first week on site.
- **What would change it:** C overtakes A only at extreme weights (Learning 1, Safety 5, Speed 1, Cost 1).
- **What decides in practice:** a named willing contractor.

## A. Morocco, structural frame

- **A week on site.**
  - **Monday:** the level-3 slab pour is planned for Thursday. Its checklist (SPEC-066) asks for rebar on site, the formwork done, the engineer's pre-pour hold point released, the concrete ordered and the pump booked. Hicham's Excel register says AcierSud delivers on Monday; it does not. At 10:00 Youssef writes "lhdid ma jach" (scenario 1). How that message reaches OCOS is D-02.
  - **Wednesday:** the engineer gives a verbal release at 16:00 (scenario 3). Karim records it; the signed paper follows.
  - **Thursday:** before the slab is hidden, the contractor's attachement for the rebar must be recorded contradictorily (F-23). OCOS lists it as a requirement.
  - **Friday:** the meeting pack shows the slab, its reasons and the promises that fell due.
- **Spec changes.**
  - SPEC-002 is filled in: one contractor, one project, the structural frame.
  - SPEC-066 is the pour checklist of ARCH §4.9, with the attachement before hiding.
  - SPEC-112: French and Moroccan contract words (situation, attachement, décompte provisoire).
  - SPEC-005 (Q-22): French and Arabic screens and messages; Darija read by the AI only if it passes T2.
  - SPEC-210 (Q-20): hosting acceptable under law 09-08.
- **Cost and time [I].** No extra build beyond slice 1. The operator (Q-04) must read French and Darija. First shadow week about 2–3 months after D-03 is answered, depending on the loops' pace.
- **Main risk (pre-mortem).** "The pilot failed because the site's real facts were in Darija voice notes and phone calls that never reached OCOS." D-02's check measures exactly this.
- **Door.** Two-way until the pilot agreement is signed. After that, changing the pilot costs the relationship and weeks of seeding.
- **Evidence:** F-13, F-17, F-19, F-23, F-35, F-39; V-11, V-12; RESEARCH §8.

## B. Morocco, finishing works

- **A week on site.** On level 4, ElecPro, the plumber and the plasterer share the floor. On Thursday at 07:05 ElecPro writes "les gaines demain inchallah" (scenario 2). Most prerequisites are "the previous trade is done" and "the space is free". These are reported by message and rarely measured.
- **Spec changes.** SPEC-066 becomes one checklist per trade. SPEC-002 changes. Commitment firmness (SPEC-032) carries most of the load.
- **Cost and time [I].** About one more week of configuration per trade checklist, written by hand (Q-18 (a)). Same build.
- **Main risk (pre-mortem).** "Nobody could say whether a room was ready, so the board was argued over and abandoned" (F-16: many subcontractors are the main barrier).
- **Door.** Two-way until signed.
- **Evidence:** F-06, F-16, F-31; V-15.

## C. France, structural frame

- **A week on site.** Sara, as OPC, already writes the minutes with actions and dates (F-02). Youssef's messages are in French. The site may already use Finalcad or a similar app (F-13), so OCOS risks keeping a second record (Q-08). The engineer's 7-day check of the projet de décompte (F-20) frames the month.
- **Spec changes.** SPEC-112: French vocabulary (projet de décompte, constat contradictoire). SPEC-005: French only. SPEC-210 and SPEC-190 follow GDPR. SPEC-213 matters if a platform is in use.
- **Cost and time [I].** Same build. Pilot terms are likely harder to obtain where software vendors already sell (F-14, F-26).
- **Main risk (pre-mortem).** "The site already had a tool good enough, and OCOS was a second one."
- **Door.** Two-way until signed.
- **Evidence:** F-02, F-13, F-18, F-20, F-26, F-35.

## D. Gulf or wider MENA, FIDIC

- **A week on site.** The client requires Aconex. Every formal letter and inspection request lives there (F-10). Youssef's messages are in Arabic or English. The Engineer's 28-day payment certificate (F-22) frames the month.
- **Spec changes.** SPEC-213 becomes central (a connector or an export). SPEC-112: FIDIC vocabulary.
- **Cost and time [I].** Platform onboarding and client approval add months.
- **Main risk (pre-mortem).** "The client's platform was the record, and OCOS was never allowed in."
- **Door.** Close to one-way: a client-imposed setting is hard to leave mid-project.
- **Evidence:** F-10, F-22, F-24.

## Validation plan

| Approach | Check, before building on it | Pass line | Revisit | If it fails |
|---|---|---|---|---|
| A | A 30-minute call with the site manager of the candidate contractor, walking through REALITY_CHECK scenarios 1–3, plus their pour checklist | They recognise at least 3 of the 5 scenarios from the last month; at least 80 % of their pour checks map onto SPEC-066; they agree in principle to a chat export (D-02) and a weekly 15-minute board check | Slice-1 exit check, or 2027-01-31 | No such contractor by 2026-12-15 → B with the same contacts; a willing contact elsewhere → that country's approach |
| B | The same call, with the floor's trade sequence | At least 3 scenarios recognised; the "previous trade done" facts can be named per room | as A | → A |
| C | The same call, plus a list of the site's current tools | No site app already covers the constraint list; the scenarios are recognised | as A | → A |
| D | Client approval for a read-only export from its platform | Written approval | 2027-01-31 | → A |

*The pass lines are proposals ([I]). You can change them in NOTES.*

## Left out

- **"Any country, decided later."** It is not a path: the first checklist, vocabulary and data law need one market.

## Log

*(written by the sessions: APPLIED, CHECK, RESULT, REOPEN)*
