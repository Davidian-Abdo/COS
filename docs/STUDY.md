# OCOS — independent study before the starting documents are finalised

*2026-10-15. COS becomes the first new Beamstack lane; the owner asked for an independent study of the round-2 documents (`8019c99`) before they are finalised. This study re-checked round 2's research and design instead of trusting them. [IDEA.md](IDEA.md) was not touched.*

## 1. What was checked

- **Research.** The seven weak sources named by round 2 (S-05, S-06, S-26, S-36, S-37, S-48, S-53) and ten more that design decisions rest on were re-opened. So were the findings behind the top-10 changes: messaging as the main input (F-09, F-32), rejection of field apps (F-14), Last Planner (F-01, F-04, F-05, F-06, F-07, F-16), inspections (F-17), and the quantity kinds and the attachement (F-20–F-25). The results are in [RESEARCH.md § Study verification](RESEARCH.md#study-verification).
- **Buildability as a Beamstack lane.** Can the build slices and the two trials be cut into loop tasks that each reach green CI in one turn? Checked against the diwan turn protocol (`diwan/AGENTS.md` §1, §2, §6).
- **Consistency.** Names, states, ids and numbers across IDEA_v2, core_logic, the architecture, the spec, REALITY_CHECK and QUESTIONS. This was done by script (SPEC references, `TO-CONFIRM` → question, slice coverage) and by reading.
- **Testability.** Does every `SPEC-nnn` have an acceptance criterion that a test can check? Does any SPEC hide a decision nobody asked the owner about?
- **Scope.** What a first paying pilot does not need.

## 2. What was wrong, and was fixed

### 2.1 Research (commit 1)

| # | Was | Now | Where |
|---|---|---|---|
| R1 | F-09 "messaging is the de facto channel", [E/V] | [V; E weak]: one qualitative study and one undated vendor figure; trial T1 must measure it on the pilot | RESEARCH F-09 |
| R2 | F-32: reading existing groups "not established" | The official Groups API only creates business-owned groups of ≤ 8 people: OCOS **cannot join existing site groups** compliantly (new S-57) | RESEARCH F-32; ARCH §4.1; Q-03 |
| R3 | F-14 [E], V-05 "contradicted" | [V], vendor-commissioned; it shows a barrier, not a rejection (95 % expect field apps to matter). V-05 is now "unproven"; "no field app" stays as a design proposal | RESEARCH F-14, V-05; IDEA_v2 change 4 |
| R4 | F-06 "information is the largest cause" | Not found in a primary source → unproven; the seven categories stand (new S-59) | RESEARCH F-06 |
| R5 | F-20 "maître d'œuvre has 10 days" | 7 days (CCAG Travaux 2021 art. 12.2) | RESEARCH F-20 |
| R6 | F-23 attachements as "contradictory measurements"; official text unread | Official text read: the **contractor** draws up the attachements; 15 + 15 days, then they are **deemed accepted**; work that will be hidden is recorded contradictorily; the client's agent draws up the décompte provisoire | RESEARCH F-23, F-25; SPEC-023, SPEC-066; ARCH §4.6, §4.9; Q-17 |
| R7 | S-37 was a job-advert page | Replaced by CCAG Travaux 2021 art. 11 (*constat contradictoire*) | RESEARCH S-37 |
| R8 | F-30: "65 % trust AI in AEC; 45 % have no AI" | 65 % is across all design-and-make industries; construction is 68 % (−14); the 45 % figure was not found and is withdrawn | RESEARCH F-30, S-53 |
| R9 | F-28 presented as a general IFC figure | 216 Chinese respondents; not generalisable | RESEARCH F-28 |
| R10 | F-16 rested on a paywalled source | Backed by a peer-reviewed Saudi study (new S-56) | RESEARCH F-16 |
| R11 | F-17: verbal release first, paper later, given as a fact | Labelled as the authors' inference; reported releases are **off by default** | RESEARCH F-17; SPEC-042 |
| R12 | IDEA_v2 §2 "typical plan reliability is well below 70 %" | Labelled as inference (F-04 supports only the 70 % threshold) | IDEA_v2 §2 |

### 2.2 Contradictions between the documents (commit 2)

| # | Contradiction | Fix | Where |
|---|---|---|---|
| C1 | core_logic: the slab is "not ready" as soon as the message is confirmed. The spec and ARCH §5: it stays `expected_ready` until the firm promise is `missed` at the end of the day | core_logic follows the spec | core_logic §3; ARCH §5 steps 3, 5 |
| C2 | ARCH §5 says "commitment at risk", but no such state exists | Removed | ARCH §5 |
| C3 | SPEC-106 makes "confirmation before state change" an invariant that cannot be switched off; SPEC-134 lets auto-confirmation bypass it | The invariant is now "a recorded confirmation event", whoever makes it | SPEC-106, SPEC-134 |
| C4 | SPEC-160 tests for "the right type", which is defined nowhere. A missed promise opens two exceptions; ARCH §5 shows one | Trigger → type table added; one exception per requirement and type | SPEC-160 |
| C5 | ARCH §17 slices: spec §3 is put in slice 1, but its missions belong to slice 2; spec §6 (authority) and SPEC-212 are in no slice; "intake with manual confirmation" sits beside all of spec §8 | Slice table rewritten by requirement id. Checked by script: every v1.0.0 requirement is in exactly one slice (SPEC-086 is split into inbound and outbound) | ARCH §17 |
| C6 | "Two spikes before building", but slice 1 needs neither | The trials run beside slice 1, and each gates only the slice-2 tasks that depend on it | ARCH §17; REALITY_CHECK C-3, C-4 |
| C7 | REALITY_CHECK §6 sent DC-1.3 to ARCH §4.7 and DC-1.4 to ARCH §4.9 | Now §4.9, and §4.1 with §4.11 | REALITY_CHECK §6 |
| C8 | Q-17(c) "projet de décompte" is the French document only; in Morocco the contractor's document is the attachement (R6) | Both are named | Q-17 |
| C9 | QUESTIONS said "no question states a default" | Every question now has a default, applied behind `TO-CONFIRM`, never treated as an answer | QUESTIONS (c) |
| C10 | "Beam stack" / "Beam-stack" against the owner's "Beamstack" | "Beamstack" in all round-2 documents (IDEA.md untouched) | all docs |

### 2.3 Testability and decisions nobody asked about (commit 2)

- **Made checkable by a test:** SPEC-068 (recomputed in the same transaction), SPEC-181 and SPEC-184 (golden logs of the five scenarios replayed in CI), SPEC-072 (mission creation limited to the board window and lead time, which also removes a flood of hundreds of proposed missions at go-live), SPEC-140 (`bounded_auto` refused).
- **Decisions that had not been asked, now tied to a question:** SPEC-138's 300-message set and 80 % threshold → Q-12; SPEC-205's 30-minute operator budget → Q-04; SPEC-042's default for reported releases (not accepted) → named in Q-10.
- **Checked by review, not by a test (acceptable):** SPEC-001 and SPEC-003 (release review), SPEC-187 (screens), SPEC-138 (an evaluation report), and the slice exit checks (field checks). Pending requirements cannot be tested until the owner answers.
- **Labelled PROPOSAL and left to a steward ADR under Q-23:** JSON Schema, an S3-compatible store, OpenID Connect, containers.

### 2.4 Moved to "later" (commit 2; spec §14)

| Id | Why a first paying pilot does not need it |
|---|---|
| SPEC-084 missions to agents | Agents are started by events; no pilot workflow gives an agent a mission |
| SPEC-085 sub-missions | One level of missions is enough for one site team |
| SPEC-102 delegation events | Grants from the approved configuration cover one pilot |
| SPEC-105 bounded autonomy (Q-11) | The pilot runs in shadow and confirm; autonomy needs the pilot's own evidence |
| SPEC-110 narrow compiler (Q-18) | One company's configuration is written by hand; the drafter pays off from the second company |
| SPEC-111 written rule vs practice | Needs approval limits and order amounts that v1.0.0 does not import |
| SPEC-165 rule-improvement drafts | Needs weeks of recurring exceptions |
| SPEC-186 external anchoring (Q-14) | Hash chain plus verification tool is enough at first; cheap to add later |
| SPEC-191 trace export | Covered by the full export (SPEC-214) and the evidence pack (SPEC-192) |

The spec now counts 135 requirements: **106 specified for v1.0.0, 20 pending, 9 later**.

## 3. What still stands

- **The core design.** A deterministic kernel over a plain event log (one table, projections in the same transaction). AI only proposes, and a person confirms every reading. Make-ready in Last Planner terms (F-01, F-04, F-05, F-07, F-16 confirmed). Hold and witness points (F-17 confirmed). The four quantity kinds, and OCOS never certifies (F-21, F-22, F-25 stand; R6 adds only a deadline and a domain-pack item). Messages are never notices. The minimum integration set. Measurable metrics.
- **Messaging as the main input stays the direction, but as a hypothesis** (R1, R2). Without official group access, intake depends on the operator forwarding messages and on chat exports. That puts the operator's time (SPEC-205) and coverage (M-12) at the centre of the pilot's verdict.
- **The 80 % go-live threshold does not contradict F-39** ("90 % is not enough"). A person confirms every reading, so the threshold measures the operator's workload, not whether wrong data gets in.

## 4. Can the loops build it?

**Yes, slice by slice, once the stack is chosen.** Slice 1 has 68 requirements and no AI, channel or outbound dependency. It divides into tasks of one requirement group each, every one with its own tests. An indicative start for the backlog:

| Task | Implements |
|---|---|
| Repository skeleton, CI, the event table with its insert-only role and hash chain | SPEC-050–052, SPEC-180, SPEC-185 |
| Grants, default deny, rejected commands | SPEC-100, SPEC-101, SPEC-103, SPEC-104, SPEC-109 |
| Entities, ids, unknown values, units | SPEC-010–013, SPEC-020, SPEC-021 |
| Assertions and their basis | SPEC-025–027 |
| Requirements and their states | SPEC-028–030 |
| Commitments and the deadline clock | SPEC-032, SPEC-033 |
| Readiness function, with table tests | SPEC-060–064 |
| Spreadsheet import with confirmed mappings | SPEC-120 (Excel part), SPEC-121, SPEC-123, SPEC-124, SPEC-129 |
| Replay of a golden log | SPEC-184 |

**Points the steward must handle before the matching task is `ready`:**

- **MPXJ needs a Java runtime.** That is not in the protocol's `requires:` list (`browser`, `dev-postgres`, `arabic-fonts`, `x86-browser`), and "an unknown need is never claimable". The schedule-file task waits for a new `requires:` value, or v1.0.0 starts from the planner's Excel export of the schedule.
- **The board and the review queue** need `browser` for end-to-end tests.
- **Arabic PDF exports** need `arabic-fonts`.
- **Neither trial is loop work.** T1 needs a WhatsApp business account verified by Meta. T2 needs the pilot's exported chats, with consent. Both are owner actions. Only the T2 evaluation harness is a loop task, built on synthetic data.

## 5. Lane readiness — what COS needs before a loop can build it

*Listed only; none of these files was created.*

| # | Item | Who |
|---|---|---|
| L1 | `AGENTS.md` stub, using the exact text of `diwan/docs/STUB-TEMPLATE.md` (`<CANONICAL>` = `AGENTS.md`), under 15 lines | a steward can do it |
| L2 | `.agent.toml` following `diwan/docs/seats/BINDINGS.md`: `[repo]` name `COS`, `language` (needs Q-23), `diwan`; `[paths]` for state, backlog, phase log, handoff, lock, stop, blockers, decisions; `[commands] verify` and `test`; `[git]` `Davidian-Abdo <daoudiabdellah1999@gmail.com>`; `.gitignore` for lock and stop | a steward can do it, after Q-23 |
| L3 | `docs/INVARIANTS.md`: what the repo is; the product invariants (ARCH §2 P1–P12, SPEC-106); which document wins in a conflict (IDEA.md is the owner's original, then IDEA_v2, spec, architecture, core_logic); where each document lives | a steward can do it |
| L4 | The owner-gated classes in `INVARIANTS.md`: proposed as changes to SPEC-103, SPEC-106 and SPEC-089, to the licence, and to applied answers | needs the owner (to confirm the list) |
| L5 | `docs/BACKLOG.md`: slice 1 cut into `T-nnn` rows, each with `implements:` naming its SPEC ids and a `requires:` where needed (§4) | a steward can do it |
| L6 | CI: GitHub Actions running lint, typecheck, tests (with a PostgreSQL service) and a docs check (SPEC references, `TO-CONFIRM` → question) | a steward can do it, after Q-23 |
| L7 | Stack choice | needs the owner (Q-23) |
| L8 | State files: `docs/CURRENT_STATE.md`, `PHASE_LOG.md`, `BLOCKERS.md`, `DECISIONS.md`, `handoff/` | a steward can do it |
| L9 | The owner channel. diwan makes `docs/DECISIONS.md` "the only file the owner edits", while COS uses `QUESTIONS.md`. Choose: keep `QUESTIONS.md` until the blocking questions are answered, or have a steward convert the open questions into `D-` records with `default-if-silent` and `expires` | needs the owner |
| L10 | A `[lanes.cos]` row in `diwan/docs/lanes.toml` (launcher, prompt `diwan:docs/prompts/brahim-orchestrator.md`, seat `brahim`, signal `backlog`), through a reviewed PR in diwan | a steward can do it |
| L11 | Admission and order of the lane in `diwan/docs/owner/PLAN.toml` (R76) | needs the owner |
| L12 | Move the repository to `TheBeamstack/COS`. Measured: `TheBeamstack/COS` does not exist yet; the repo is `Davidian-Abdo/COS`, public | needs the owner |
| L13 | A Meta-verified WhatsApp business account for T1, and the pilot's chat export with consent for T2 | needs the owner |

**Which owner answers block the first `ready` task.** Only **Q-23** (the stack), because a stack cannot be built behind a configuration marker. The other blocking questions (Q-01, Q-02, Q-19, Q-03, Q-13, Q-21) have defaults the loops can build behind `TO-CONFIRM`, as `diwan/AGENTS.md` §4 allows. They block the slice-1 exit check (Q-01, Q-02), releasing code under a licence (Q-19), and the two trials (Q-03, Q-13, Q-21). L4, L9, L11 and L12 are owner acts that do not need a question.

## 6. Verdict

The documents are ready to be finalised once the seven blocking questions (Q-01, Q-02, Q-23, Q-19, Q-03, Q-13, Q-21) are answered. With this study's fixes the design is consistent and slice-able: every v1.0.0 requirement is in one build slice, it has a criterion a test or a named review can check, and nine requirements a first pilot does not need are set aside. The research holds where the design rests on it (Last Planner, hold points, the quantity kinds, liability), with corrections that sharpen it rather than overturn it. One premise is weaker than round 2 said. That messages are the main source of site facts is a well-motivated hypothesis, not established evidence, and OCOS cannot read existing WhatsApp groups through the official API. Trial T1 must therefore measure, on the pilot's own chat history, how much reaches OCOS and what it costs the operator, before slice 2 builds on it. Lane setup is about one steward turn after Q-23, plus four owner acts (L4, L9, L11, L12).
