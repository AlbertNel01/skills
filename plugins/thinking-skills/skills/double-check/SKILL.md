---
name: double-check
description: Catch overreach — a claim that outruns the evidence behind it — by anchoring every load-bearing claim to the artefact it rests on and testing coverage, authority, kind, derivation and scope. Use when asked to double-check, make sure or confirm something already produced, and before an artefact leaves this machine: an email, a PR body, a ticket comment, or a figure quoted to a person.
---

# Double-check

**Overreach** is a claim the evidence does not reach — sourced, true-sounding, and wider than its source can support. It survives ordinary verification, because verification asks whether the number is right, and overreach is about how far the number goes. A three-column extract cannot say *"every field"* however many times those three columns agree.

This is one pass, not a loop. When the pass shows the **answer** may be wrong rather than the wording, hand off to `converge`.

## Steps

### 1. List the load-bearing claims

A claim is load-bearing when a reader could act on it, quote it, or sign it off: a number, a filename, a line reference, an attribution, an absence, a date, a cause. Include the claims inside the ask — a question carries assertions in its premises.

*Done when:* every load-bearing claim in the artefact is on the list, the ask included.

### 2. Anchor each claim to its artefact

Name the file, command output, message or ruling each claim rests on. Open the artefact itself and read what it holds — its columns, its rows, the period it covers, who wrote it. Recall is not an artefact.

*Done when:* every claim on the list carries an artefact, and any claim with none is marked unsourced.

### 3. Run the five lenses on every claim

- **Coverage** — does the artefact hold the fields, rows and period the claim covers? *An `order_id,customer_id,placed_at` export supports "same id, customer and date"; it says nothing about `billing_address`.*
- **Authority** — who asserts this: you, a colleague, a policy, a ruling? Their finding travels under their name.
- **Kind** — measurement, inference, or purpose? *"Both installs issued the same new ids" is measured; "the customers table came across" is inferred; "the copy was taken to move an account" is a purpose nobody evidenced.*
- **Derivation** — what does the computation assume that the data does not carry? Timezone, units, rounding, locale, and today's date.
- **Scope** — does the figure cover exactly the set named? *1,204 rows named, 1,180 of them past their retention date.*

For prior art on the shapes that recur here, read `overreach-shapes.md`, and your own
`~/.claude/double-check/overreach-log.md` where it exists.

*Done when:* every claim has a verdict from all five lenses, and each lens that found nothing is recorded as checked.

### 4. Rewrite in place

Each claim ends one of three ways: **restricted** to what its artefact supports, **attributed** to whoever does support it, or **dropped**. A claim you keep reads as a measurement of the artefact you opened.

*Done when:* every claim carries restricted, attributed, or dropped, and the rewritten artefact reads back through step 3 clean.

### 5. Report the pass with counts

Give the number of load-bearing claims examined and the number changed, then each defect in the sentence it occurred in. Counts are what make *"I checked it"* a claim with evidence behind it rather than the next piece of overreach.

*Done when:* both counts are stated and every changed claim is named.

## Prove the search before trusting a negative

An absence claim rests on a search, and a search that cannot find anything returns the same empty output as a world with nothing in it. Run the same pattern against something you know is there; when the control comes back empty, the tool is lying and every negative it gave you is void.

## Add what you find

A shape that got past the five lenses belongs in `~/.claude/double-check/overreach-log.md` as its own entry,
in the format `overreach-shapes.md` uses — the sentence that carried it, the lens that catches it, what was
true, what it was rewritten to. Create the file if it is not there yet.

Write it to that path and never into this skill's own directory. A real entry carries the schema, the counts
and the recipient of whatever you were writing; this skill is distributed, and your log is not. The lenses
grow from real defects, which is exactly why the defects stay on your machine.
