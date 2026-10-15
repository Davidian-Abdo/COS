# How the owner chooses and checks OCOS's direction

*2026-10-15. Asked for by the owner: "a well-designed mechanism for me to choose and validate the right approach, as a more generalised way than the questions." This file is the method. The decisions themselves are in [decisions/](decisions/).*

## 1. The idea in five lines

1. Questions that depend on each other become one **direction decision**, `D-nn`. Each decision offers 2–4 **approaches**: whole paths, not separate answers.
2. Each approach shows what it **leads to**: a week on the pilot site, the SPEC ids it changes, cost and time to the first pilot, its main risk, how reversible it is, and its evidence.
3. Approaches are scored against **five explicit criteria** that you can re-weight. The recommendation is the top score, with the arithmetic shown and the weights that would change it.
4. A chosen approach is **not yet the spec**. It carries a cheap **check**, a **pass line**, a **revisit date** and a **fallback** if the check fails. It becomes the spec only once the check passes.
5. You answer with **one letter on one line**, on github.com, phone included. Silence keeps a stated default until it expires. The next session applies your answer and records it.

## 2. Where it comes from, and what was changed

| Id | Practice | What OCOS takes from it | What was changed |
|---|---|---|---|
| K-01 | Architecture decision records: one short file per decision with context, decision, status and *all* consequences (Nygard 2011) | One file per decision, kept in the repo, never deleted, with a status line | Options are written as whole paths, and consequences are told as a site week, not as technical notes |
| K-02 | One-way and two-way doors: irreversible decisions go slowly and carefully, reversible ones go fast (Amazon, 2015 letter to shareholders) | Each approach is labelled by door type. Silence never walks through a one-way door | The label goes on the parts of an approach, because one path can mix both kinds |
| K-03 | Weighted decision matrix: options scored against weighted criteria (Pugh's concept selection) | Five fixed criteria, weights from 1 to 5, scores from 1 to 5, totals shown | The owner can re-weight on the answer line. Each decision shows which weights would change the winner |
| K-04 | Pre-mortem: imagine the project has already failed, then ask why (Klein, HBR 2007) | Each approach's "main risk" is written as the most likely reason for a failed pilot | Done in writing by the session, not in a meeting |
| K-05 | Test card: we believe…, we test…, we measure…, we are right if… (Strategyzer) | The check and pass line of each approach | Only checks that cost days and need no build: a call, a chat export, trial T1 or T2 |
| K-06 | Kill criteria: decide in advance on a state and a date that end an effort (Duke, *Quit*, 2022) | The pass line plus the revisit date. A failure triggers the named fallback, so nobody has to argue later | The fallback is a named approach of the same decision |
| K-07 | Final comment period: a proposal with a stated outcome is settled after a fixed period unless someone objects (Rust RFC process) | Default-if-silent with an expiry date | At expiry only two-way doors are applied. A one-way door waits for you |

Sources: K-01 <https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions> · K-02 <https://www.sec.gov/Archives/edgar/data/1018724/000119312516530910/d168744dex991.htm> · K-03 <https://en.wikipedia.org/wiki/Decision-matrix_method> · K-04 <https://hbr.org/2007/09/performing-a-project-premortem> · K-05 <https://www.strategyzer.com/library/validate-your-ideas-with-the-test-card> · K-06 Annie Duke, *Quit* (Portfolio, 2022), ch. on kill criteria · K-07 <https://rust-lang.github.io/rfcs/introduction.html>. All accessed 2026-10-15. These sources are about the method, so they are numbered `K-nn` to keep them apart from RESEARCH.md's `S-nn`.

## 3. What a decision file contains

Each `docs/decisions/D-nn-<name>.md` has, in this order:

1. **Your answer.** The box you edit, placed first so it is easy to reach on a phone (§6).
2. **What is being decided.** The questions it replaces (`Q-nn`, ids kept), what it blocks, and which other decision it depends on.
3. **The approaches, one line each.**
4. **Scoreboard.** Criteria × approaches, the weighted totals, the recommendation, and *what would change it*.
5. **Each approach in detail:**
   - **A week on site.** The REALITY_CHECK scenarios, with the same cast (Karim, Youssef, Sara, Hicham, ElecPro, AcierSud), played under this approach.
   - **Spec changes.** Which `SPEC-nnn` change, and how.
   - **Cost and time to the first pilot week.** Estimates are labelled [I].
   - **Main risk**, as a pre-mortem.
   - **Door.** One-way, two-way, or which part is which.
   - **Evidence.** `F-nn`, `V-nn` and `S-nn` from RESEARCH.md.
6. **Validation plan.** For every approach: the check, the pass line, the revisit date, and the fallback if it fails.
7. **Left out.** Options that were considered but are not approaches, with the reason (for example, against a platform's terms).
8. **Log.** Lines written by the sessions: `APPLIED:`, `CHECK:`, `RESULT:`, `REOPEN:`.

## 4. The criteria and their weights

The same five criteria apply to every decision, so that your weights mean the same thing everywhere. An approach scores 1 (poor) to 5 (good) on each one. A higher score is always better: for safety, 5 means *least* risk.

| Criterion | Question it answers | Default weight |
|---|---|---|
| **Learning** | How much does this path prove or disprove OCOS's riskiest assumptions: that site facts arrive by message (F-09), that AI can read them (F-39, SPEC-138), and that a site team uses the board (F-14, F-36)? | 5 |
| **Safety** | How low are the legal, relationship and technical risks: data law (F-35), the platform's terms (F-32), trust between contractor and subcontractors (V-14)? | 4 |
| **Speed** | How soon can the first pilot week run in shadow mode? | 3 |
| **Cost** | How little money and people's time does it need (owner, operator, contractor)? | 2 |
| **Reversibility** | How cheaply can it be undone if it turns out wrong? | 2 |

*Why these defaults:* the study found the core premise, that messages carry site facts, is a hypothesis (STUDY §6). So a pilot that teaches nothing is the worst outcome (Learning 5). A pilot stopped by a data-law problem comes next (Safety 4).

**Re-weighting.** On the answer line, write for example `WEIGHTS: safety=5 learning=3`. Weights you do not mention keep their defaults. Weights written in one decision apply to that decision only. To change them everywhere, edit the table above.

**Total** = Σ (weight × score). The maximum, with the default weights, is 80. The scores are judgements, each followed by its reason in a few words. If you disagree with a score, say so in `NOTES:`; the session re-scores and shows the new totals.

## 5. From choice to spec: validation

| Status | Meaning | What the docs say |
|---|---|---|
| `open` | No answer yet. The default is used where work reaches it | the old `TO-CONFIRM (Q-nn)` markers stay |
| `chosen` | You wrote a letter. The session has applied it to the docs | `TO-CONFIRM (Q-nn)` becomes `TO-VALIDATE (D-nn)` |
| `validating` | The approach's check is running | same |
| `confirmed` | The pass line was met. It is now the spec | the marker is removed and `RESULT:` is logged |
| `fell back` | The check failed. The named fallback becomes the working choice and the decision goes back to you with the result | `TO-VALIDATE (D-nn)` stays, now pointing to the fallback |

Rules:

- **Two-way doors** may be built behind `TO-VALIDATE`, as behind `TO-CONFIRM` today (`diwan/AGENTS.md` §4).
- **One-way parts** happen only after the check passes **and** you have chosen them. Examples: publishing code under a licence, or sending real pilot messages to an outside AI provider.
- **Revisit date.** On that date, or earlier if a revisit trigger fires, the next session puts the decision at the top of its report with the evidence so far. You confirm or reopen. Nothing changes without you.
- **Checks are owner or pilot actions**, not loop work, unless the decision says otherwise (STUDY §4).

## 6. How you answer: one edit

1. Open the decision file on github.com and tap the pencil icon (Edit).
2. In the **Your answer** box, write a letter after `CHOICE:`, for example `CHOICE: B`. Optionally add `WEIGHTS:` and `NOTES:`, for example a contractor's name or "B, but licence AGPL".
3. Commit to `main` with a message like `decide: D-01 B`. That is all.

**If you write only `WEIGHTS:`**, the top approach under your weights becomes your choice. **A mixed answer** ("B with A's licence") is applied if it is consistent. If it is not, the session explains the conflict in its report and keeps the default. **Silence:** `DEFAULT-IF-SILENT` applies until its expiry date. At expiry, the next session applies the default as if you had chosen it, but only for two-way doors, and it says so in its report. The defaults are the same as the defaults already stated in QUESTIONS.md, so nothing riskier happens than today.

## 7. What the next session does

1. It reads each `D-nn` whose answer box changed since the last `APPLIED:` line.
2. It applies the approach's "spec changes" to IDEA_v2, core_logic, the architecture and the spec, and swaps the markers (§5). It writes `APPLIED: <date> <approach> <commit>` in the log.
3. It lists the approach's check as an owner action in its report, with the pass line and the revisit date.
4. When a check result is recorded (by you, or by a trial report), it writes `RESULT:` and moves the status to `confirmed` or `fell back`.
5. It checks that every SPEC id and RESEARCH id cited in the decision exists, and that each `Q-nn` belongs to exactly one decision or stays in QUESTIONS.md.

## 8. When to use a decision, and when a plain question

- **Use a decision** when two or more questions constrain each other, or when one choice changes what the pilot site lives through.
- **Use a plain question** in [QUESTIONS.md](QUESTIONS.md) when a single choice affects nothing else, such as the product's name (Q-24). Each open question says which decision it would join if it becomes entangled.
- **No tools.** Markdown files in this repo only: no app, no service, no form.

## 9. The decisions

| Decision | Replaces | Blocks | Default if silent | Recommended |
|---|---|---|---|---|
| [D-01 The pilot](decisions/D-01-pilot.md) | Q-01, Q-02 | slice-1 exit check; T2; SPEC-002, SPEC-066 | A, until 2026-11-15 | A: Moroccan contractor, structural frame |
| [D-02 Site facts and who may read them](decisions/D-02-site-facts.md) | Q-03, Q-13, Q-21 | T1, T2; SPEC-086, SPEC-132, SPEC-190, SPEC-211 | A, until 2026-11-15 | B: forwarding plus chat exports, a commercial AI under terms |
| [D-03 How the code starts](decisions/D-03-code.md) | Q-23, Q-19 | the first `ready` build task; LICENSE | B, until 2026-10-29 | B: Python + TypeScript + PostgreSQL, licence chosen at the first release |

**If you have two minutes, answer D-03 first.** It alone blocks the first build task (STUDY §5). D-02 is written for D-01's recommended approach and says what changes under the others.
