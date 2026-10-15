# D-03 How the code starts: stack and licence

*Opened 2026-10-15 under [DECIDING.md](../DECIDING.md). Status: **open**. **The most urgent decision:** it alone blocks the first `ready` build task (STUDY §5).*

## Your answer

- CHOICE:
- WEIGHTS:
- NOTES:
- DEFAULT-IF-SILENT: B, expires 2026-10-29. This is today's default (Q-23 (a), Q-19 (a)): Python, TypeScript and PostgreSQL, with no open-source licence yet. A stack is costly to undo once several tasks stand on it (DECIDING §5). So at expiry, only the repository skeleton task may start on this default. Everything after it waits for your letter.

## What is being decided

- **Replaces** two questions:
  - Q-23: the technology stack.
  - Q-19: the open-source licence.
- **Why together.** Both are fixed by the same first steward turn: `.agent.toml`, CI and the LICENSE file (STUDY L2, L6, L7). Both decide what kind of open-source project the public repository is from its first line of code.
- **Blocks:** every build task; ARCH §11; the `TO-CONFIRM (Q-19)` markers in IDEA_v2 and core_logic.
- **Later joins it:** Q-09 (the business model, which the licence must fit) and Q-24 (the name used in code packages).
- **Independent of D-01 and D-02.**

## The approaches

- **A. Python + TypeScript + PostgreSQL, Apache-2.0 from the first push.**
- **B. Python + TypeScript + PostgreSQL, licence chosen at the first release.** Until then the code is public but all rights are reserved.
- **C. TypeScript everywhere + PostgreSQL, AGPL-3.0 for the kernel and Apache-2.0 for schemas, adapters and SDKs.**
- **D. Kotlin or Java back end (MPXJ native) + TypeScript interface + PostgreSQL, Apache-2.0.**

## Scoreboard (default weights)

| Criterion (weight) | A | B | C | D |
|---|---|---|---|---|
| Learning (5) | 4: Python's AI and spreadsheet libraries speed up the T2 harness; an open licence may draw early contributors (F-26) | 3: same speed; no outside contributions before the release | 3 | 3 |
| Safety (4) | 3: a closed product can be built on it (F-26: "incumbents can add any one piece quickly") | 4: nothing granted yet | 4: a closed copy run as a service must publish its changes | 3 |
| Speed (3) | 5: the loops already run Python lanes with PostgreSQL | 5 | 3: weaker libraries for documents and AI | 2: no JVM lane yet; a new `requires:` value is needed (STUDY §4) |
| Cost (2) | 4 | 4 | 3 | 3 |
| Reversibility (2) | 2: code released under Apache-2.0 stays released | 5: any licence can still be chosen | 2 | 2 |
| **Total** | 59 | **64** | 50 | 43 |

**Recommendation: B.** It differs from Q-19's earlier recommendation (Apache-2.0 now) for a reason the criteria make visible: the licence is a one-way door, and before the pilot nobody outside needs rights to the code.
- **What would change it:** A comes first only if you set Learning to 5 and both Safety and Reversibility to 1. That means early contributors matter more to you than keeping the choice open.

## A. Python stack, Apache-2.0 now

- **A week on site.**
  - **Monday:** Sara's MS Project file reaches OCOS through the MPXJ adapter, run in its own process, or through her Excel export (SPEC-120).
  - **On the evaluation:** the contractor's director asks, "What if you disappear?" (REALITY_CHECK B-5). The answer is their data export (SPEC-214) plus the right to run the code themselves.
- **Spec changes.** No requirement changes. ARCH §11 rows "language" and "licence"; a LICENSE file; IDEA_v2 §19 and core_logic §10 lose `TO-CONFIRM (Q-19)`.
- **Cost and time [I].** About one steward turn of lane setup (STUDY §5).
- **Main risk (pre-mortem).** "A platform vendor took the open kernel into a closed product before the pilot proved anything."
- **Door.** The stack is one-way after a few tasks. The licence is one-way for every pushed commit.
- **Evidence:** F-11, F-26; V-25; S-50.

## B. Python stack, licence chosen at the first release

- **A week on site.**
  - **Monday:** as A.
  - **On the director's question:** the pilot agreement (Q-09) grants the contractor the right to use the code and to export its data (SPEC-214) until a licence is chosen.
- **Spec changes.** As A for the stack. ARCH §11 "licence" reads "chosen at first release". No LICENSE file yet.
- **Cost and time [I].** As A, plus one clause in the pilot agreement.
- **Main risk (pre-mortem).** "A useful outside contributor walked away because there was no licence."
- **Door.**
  - The stack is one-way after a few tasks.
  - The licence stays two-way until the release. Then it becomes the one-way act and is put to you again.
- **Evidence:** F-11, F-26; V-25; S-50.

## C. TypeScript everywhere, AGPL kernel

- **A week on site.** Same as A. The T2 harness and the document readers take longer to build. Schedule files still need MPXJ's Java runtime, in a separate process.
- **Spec changes.** No requirement changes. ARCH §11: language and licence.
- **Cost and time [I].** The loops need a TypeScript lane setup. Slower on spreadsheets and AI.
- **Main risk (pre-mortem).** "Contractors' IT departments refused AGPL, and the pilot's self-hosting option died."
- **Door.** One-way, for the stack and the licence alike.
- **Evidence:** F-11, F-26.

## D. Kotlin or Java back end

- **A week on site.** Sara's `.mpp` file is read natively on Monday, with no export step. Nothing else differs on site.
- **Spec changes.** No requirement changes. ARCH §11.
- **Cost and time [I].** A JVM `requires:` value and a JVM lane must exist before the first task (STUDY §4). The AI and spreadsheet libraries are weaker than Python's.
- **Main risk (pre-mortem).** "The loops never got a JVM seat, and the build stalled at task one."
- **Door.** One-way after a few tasks.
- **Evidence:** F-11; V-25; S-50.

## Validation plan

| Approach | Check, before building on it | Pass line | Revisit | If it fails |
|---|---|---|---|---|
| A, B (stack) | (1) The skeleton task: SPEC-050–052, SPEC-180, SPEC-185. (2) A one-day MPXJ spike: a Python wrapper reads one sample schedule file through a separate JVM process | (1) green CI within 2 loop turns. (2) The tasks, dates and links match MS Project's own XML export of the same file | After the first 5 tasks | (1) → re-score D-03 with the failure noted. (2) → v1.0.0 reads the planner's Excel export (SPEC-120 Excel part); the stack stays |
| A (licence) | You confirm Q-09: nothing planned is closed source | Your yes in NOTES | First outside contributor | → B |
| B (licence) | Before pilot go-live, ask the contractor whether it needs rights to the code beyond the pilot agreement | No one needs a licence before the release | Pilot go-live, the first outside contributor, or 2027-03-31, whichever comes first | → the session asks you to choose A's or C's licence. This is a one-way act, so never on silence |
| C | The pilot contractor's IT or legal adviser reads AGPL-3.0 | A written OK for self-hosting | Before go-live | → B |
| D | A JVM `requires:` value is agreed for the loops (diwan) | A JVM-capable seat exists | 2026-11-15 | → B |

## Left out

- **Licence (d), "a foundation later"** (Q-19 (d)). It is a later step of A or C, not a starting path. Add it in NOTES if you want it recorded.

## Log

*(written by the sessions: APPLIED, CHECK, RESULT, REOPEN)*
