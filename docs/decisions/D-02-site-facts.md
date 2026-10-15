# D-02 Site facts: how they reach OCOS, and who may read them

*Opened 2026-10-15 under [DECIDING.md](../DECIDING.md). Status: **open**. Written for D-01 A (Morocco). The end of this file says what changes under D-01's other approaches.*

## Your answer

- CHOICE:
- WEIGHTS:
- NOTES:
- DEFAULT-IF-SILENT: A, expires 2026-11-15. These are today's QUESTIONS.md defaults (Q-03 (a), Q-13 (a), Q-21 (a)): email and upload only, no real chat history used, and no AI on real pilot data. Trial T1 does not start, and nothing leaves the installation.

## What is being decided

- **Replaces** three questions that make one path:
  - Q-03: how messages reach OCOS.
  - Q-13: records about named people.
  - Q-21: which AI may read the messages.
- **Why they belong together.** The channel decides what personal data arrives. Consent decides whether chat exports can feed the baseline and trial T2. The data law decides which AI may read the messages.
- **Blocks:** SPEC-086, SPEC-132, SPEC-190 and SPEC-211; trials T1 and T2 (ARCH §17).
- **Later joins it:** Q-07 (baseline from exports) and Q-20 (hosting).

## The approaches

- **A. Paper-safe.** Email and upload only. Nobody's chat history is used. The AI reads only anonymised or synthetic history. A person reads every real input.
- **B. Forward and export, with a commercial AI under terms.**
  - **Channel:** an OCOS business number. The operator forwards what matters; anyone may write or send voice notes to it. A weekly "export chat" of the site groups catches the rest.
  - **People's data:** Q-13 (a), checked by the contractor's legal adviser.
  - **AI:** one commercial provider under no-training and limited-retention terms, behind the gateway, with a self-hosted model tested as the fallback.
- **C. Forward and export, with self-hosted AI only.** As B, but the AI runs on open models inside the installation, so no message leaves it.

## Scoreboard (default weights)

| Criterion (weight) | A | B | C |
|---|---|---|---|
| Learning (5) | 2: tests neither F-09 (do facts arrive by message?) nor reading on real messages | 5: T1 and T2 both run on the pilot's own history | 4: as B, but with weaker models on Darija (F-39) |
| Safety (4) | 5: no transfer, no new number | 3: CNDP authorisation for a transfer abroad (F-35); Meta business verification; the platform's terms (F-32) | 4: no transfer abroad if hosted in Morocco |
| Speed (3) | 4: nothing to set up | 3: Meta verification, consent and a legal check take weeks | 2: plus a GPU server and model trials |
| Cost (2) | 2: the operator types every fact by hand (SPEC-205 is at risk) | 4: AI calls are cheap at a few hundred messages a day [I] | 2: GPU hosting [I] |
| Reversibility (2) | 5 | 4: the provider can be swapped behind the gateway, but messages already sent cannot be recalled | 4 |
| **Total** | 56 | **62** | 54 |

**Recommendation: B.** It is the only path that tests OCOS's weakest premise on real data (STUDY §6).
- **What would change it:** with Safety 5 and Learning 3, A comes first (A 57, B 55). That means waiting for legal clarity before testing anything.
- **C never comes first** under these scores, whatever the weights. It is there as the fallback if B's legal check fails.

## A. Paper-safe

- **A week on site.**
  - **Monday 10:00:** Youssef's "lhdid ma jach" stays in the site group. OCOS knows only what Hicham's imported Excel register says: AcierSud, Monday.
  - **Monday evening:** the deadline passes. The promise is missed and the slab shows not ready, about 8 hours after the site knew (scenario 1).
  - **Thursday 07:05:** ElecPro's "demain inchallah" reaches OCOS only if Karim emails it (scenario 2).
  - **Every evening:** the operator types what they heard.
- **Spec changes.**
  - SPEC-132 and SPEC-086: email and upload only.
  - SPEC-211: no provider; real inputs go to `needs_reading`.
  - SPEC-138 runs on synthetic data only.
  - SPEC-212 (works without AI) becomes the normal mode.
- **Cost and time [I].** No setup. The operator needs more than the 30 minutes a day of SPEC-205.
- **Main risk (pre-mortem).** "The pilot proved the board works but taught nothing about messages. The next decision was made blind."
- **Door.** Two-way.
- **Evidence:** F-35, F-36; V-16.

## B. Forward and export, with a commercial AI under terms

- **A week on site.**
  - **Monday 10:02:** Karim, already in the group, forwards Youssef's message and photo to the OCOS number. The AI proposes "rebar for slab L3-B not on site", quoting "lhdid ma jach". Karim confirms with one tap. The slab stays expected ready, since AcierSud's promise runs to the end of Monday, but its reasons show the report. OCOS proposes a job for Hicham: "a confirmed delivery time by 14:00".
  - **Thursday 07:05:** Youssef forwards ElecPro's message. OCOS records the promise as missed and the new one as tentative, before the crew starts (scenario 2).
  - **Saturday:** the week's chat export is imported. Facts nobody forwarded show up as late items, and their share is the coverage figure (M-12).
- **Spec changes.**
  - SPEC-132 and SPEC-086: the business number plus chat-export import; email and upload stay.
  - SPEC-190: Q-13 (a).
  - SPEC-211: one provider under no-training terms, with a self-hosted fallback.
  - SPEC-138 runs on the pilot's exported history.
  - SPEC-201: baseline from the exports (Q-07 (a)).
  - SPEC-142: shadow output seen by the OCOS team only.
- **Cost and time [I].**
  - **Owner acts:** a Meta-verified business account (STUDY L13); a written staff notice; the contractor's legal adviser; a CNDP filing for the transfer.
  - **Time:** these can run during slice 1, typically weeks.
  - **AI cost:** small at pilot volume.
- **Main risk (pre-mortem).** "The CNDP authorisation never came, or nobody forwarded anything after week two." The checks below catch both early.
- **Door.**
  - Two-way for the number and the exports.
  - **One-way for each message sent to the provider.** That is why it waits for the legal check (DECIDING §5).
- **Evidence:** F-09, F-32, F-35, F-36, F-39; V-07, V-08, V-16, V-18, V-21; S-57.

## C. Forward and export, with self-hosted AI only

- **A week on site.** As in B, but Karim's review queue has more readings to correct or to read themselves, wherever the open model misreads Darija. Voice notes in Darija may all go to `needs_reading` (SPEC-133).
- **Spec changes.**
  - As B, except SPEC-211: self-hosted only.
  - SPEC-210 (Q-20): hosting needs a GPU.
- **Cost and time [I].** A GPU server, and a model-selection trial before T2.
- **Main risk (pre-mortem).** "Accuracy stayed under the SPEC-138 line, so the operator did the reading anyway" (F-39: Wenti dropped cheaper open models).
- **Door.** Two-way.
- **Evidence:** F-35, F-39; V-08.

## Validation plan

| Approach | Check, before building on it | Pass line | Revisit | If it fails |
|---|---|---|---|---|
| A | One month's chat export of one site group, read by hand under staff notice | Under 30 % of the field facts in it also appear in the minutes or registers. That means messages are not the main source, and A is enough | 2027-01-31 | ≥ 30 % → B |
| B | (1) Legal: the adviser accepts the Q-13 (a) notice and the transfer route (CNDP). (2) T1: a verified test number, and one week of forwarding on the pilot | (1) a written OK before any real message reaches the provider. (2) ≥ 60 % of the field facts in that week's export reached OCOS by forwarding (M-12), with operator time ≤ 30 min/day (SPEC-205). (3) T2: ≥ 80 % per language (SPEC-138) | After T1, then after T2; 2027-01-31 at the latest | (1) fails → C. (2) fails → A plus exports only, and the "messaging first" premise is re-opened. (3) fails for Darija only → Darija goes to people (SPEC-133); B stands |
| C | T2 with two open models on the same history | ≥ 80 % per language (SPEC-138) | After T2 | → B if the legal check allows it, else A |

*The 30 % and 60 % lines are proposals ([I]). The 80 % line and the 30-minute budget are already in the spec, pending Q-12 and Q-04.*

## Left out

- **Reading the existing groups through an unofficial route** (Q-03 (d)). It is against WhatsApp's terms, and the number can be banned (F-32).
- **Forwarding without exports** (Q-03 (b)). It loses the baseline and the coverage figure. It is a variant of B: write "B, no exports" in NOTES.
- **Everyone named everywhere, with individual statistics** (Q-13 (c)). It contradicts SPEC-188 and F-35.

## If D-01 is not A

- **D-01 B:** unchanged. More outside companies are named in the messages, so the legal check must cover subcontractors.
- **D-01 C (France):** GDPR and CNIL replace law 09-08. An EU-region provider usually removes the transfer issue, so B's Safety rises to 4 and B wins more clearly.
- **D-01 D:** the client's platform may forbid both the provider and the exports. Re-score with the contract in hand.

## Log

*(written by the sessions: APPLIED, CHECK, RESULT, REOPEN)*
