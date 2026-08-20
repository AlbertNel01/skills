---
name: converge
description: Harden a recommendation until it converges — verify its facts, sweep a fresh angle set each pass, and hold or reverse with the reason named. Use when a decision is in play: the user asks you to think a recommendation through again, weigh the options, consider all angles, or says a decision leaves too much guesswork. To test whether a finished artefact's claims are supported rather than to decide anything, use double-check.
---

# Converge

A recommendation is not finished when it sounds right. It is finished when it has **converged**: a full pass that opened genuinely new angles and moved the answer nothing.

Each pass is **load-bearing** or it is void. A pass earns its place by introducing new evidence or a new angle. Re-running yesterday's argument with warmer adjectives is **oscillation** wearing the costume of rigour.

## The loop

### 1. Pin the claim

Write the decision in one line and the current recommendation in one line. Everything below tests exactly this pair.

*Done when:* both lines exist and a reader who has not followed the conversation could restate the decision from them.

### 2. Name the falsifiers, then go check them

A **falsifier** is a fact that, if true, kills the recommendation. Name them before you defend anything — the ones you would least like to be true.

Then verify each in the environment. Open the file, read the schema, run the query, check the version. Recall is not verification; neither is a plausible-sounding memory of how the code works.

*Done when:* every load-bearing factual claim in the recommendation is either (a) anchored to something you opened this pass, cited by `file:line`, version, or command output, or (b) restated as an explicit assumption with an owner who can confirm it.

### 3. Sweep a fresh angle set

Enumerate the angles for *this* pass before evaluating any of them, so the sweep is not steered by the answer you already like. Pull from the families below; a family that surfaces nothing is still a checked box.

- **Lifecycle** — create, edit, copy, duplicate, delete, restore, undo, replay. Which of these has nobody thought about?
- **Concurrency and retries** — double-submit, redelivery, two writers, partial failure.
- **Ownership of the invariant** — which system is the authority for this rule, and is the enforcement being placed on the authority or on a mirror of it?
- **Precedent** — has this codebase already solved the same shape? Copy it or contradict it deliberately.
- **Blast radius** — who else reads or writes this thing today, including code you would not have thought to look at.
- **Reversal cost** — if the next decision downstream goes the other way, what does undoing this cost, concretely?
- **Cross-boundary claims** — anything true only in another repo, another team's service, or a runtime you cannot inspect from here.

*Done when:* each family has been named and either produced an angle or been ruled irrelevant for a stated reason.

### 4. Weigh the asymmetry

Compare the cost of being wrong each way, not the benefits of being right. Recommendations turn on which failure is worse and who absorbs it — a user-facing error mid-task versus a prunable row nobody sees are not comparable magnitudes.

*Done when:* both failure modes are described concretely enough to rank.

### 5. Hold or reverse — name the reason

State which it is, out loud. When reversing, say which prior argument was weak and *why* it was weak — that is what separates convergence from oscillation. When holding, say what could have overturned it this pass and did not.

Reversing on new evidence is the loop working. Reversing on the same evidence, restated, is the loop failing.

*Done when:* the pass ends with `hold` or `reverse`, plus the specific input that decided it.

### 6. Repeat until converged

Run another pass. Stop when a load-bearing pass — new angles genuinely surfaced — leaves the recommendation unmoved.

*Done when:* the last pass introduced new angles and changed nothing.

### 7. Deliver with no guesswork

The recommendation ships as something someone can execute without asking a follow-up question:

- **The artifact, exactly.** The DDL, the signature, the config, the file list. Not a description of the artifact.
- **The landmines.** The specific way an implementer of this decision gets it silently wrong here — the trap this codebase has sprung before.
- **The contracts.** Every claim you could not verify from here, promoted from silent assumption to a stated requirement someone owns.
- **The revisit conditions.** What would reopen this, and what reopening costs.

*Done when:* each of the four is present, and no sentence in the deliverable rests on a fact that was never checked in step 2.

## Convergence and oscillation

Both look like changing your mind. They are told apart by the *input*, never by the confidence of the prose:

| | Input that moved it | Verdict |
|---|---|---|
| Convergence | A fact verified this pass, or an angle never previously swept | The loop working |
| Oscillation | An argument already on the table, re-weighted | The loop failing — the pass was void, run a real one |

When a pass produces no new angles, say so plainly and hold. A pass that finds nothing is a result.
