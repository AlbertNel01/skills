---
name: critic-prompt
description: Turns any finished artefact into one paste-ready prompt that makes a fresh agent tear it apart as the real person who receives it - a mail, a spec, a PR body, a ticket, a proposal, a design. Casts the critic as that named reader, arms it with the sources the artefact cites, and demands quoted defects worst-first plus a single blocking answer. Triggers on "/critic-prompt", "critic prompt", "critique this", "have a critic read this", "tear this apart", "review this as the reader".
---

# Critic prompt

The user points at a finished artefact. You give back ONE prompt they paste into a fresh agent session.

You are not critiquing the thing. You are writing the prompt that makes another agent do it properly.

## Flow

1. **Read the artefact.** Enough to know what it is, what it claims, and who receives it.
2. **Pick the cast.** If the recipient is obvious from the artefact, name them and carry on. If not, offer **2 or 3 candidate readers**, one line each, and stop. Wait for the pick.
3. **Collect the sources.** List the files the artefact cites or rests on, with paths. The critic must be able to open them.
4. **Write the prompt.** One block, paste-ready, no headings inside it, no narration after it.
5. **Offer to run it.** One flat line: "I can run this here." Not a question.

## The cast is the whole trick

A generic reviewer returns style notes. A **named reader with a stake** returns the defects that cost something, because it reads for what it needs rather than for what is wrong.

Three runs of this returned, between them: an ask handed to the wrong person, a merged decision record with a falsifiable sentence, a figure quoted with its denominator removed, an argument that misstated a speed cost as a quality cost, and a correction addressed to someone who had never received the thing being corrected. A generic reviewer finds none of those. It has no stake, so it cannot notice that the number missing is *its own workload*.

A cast has to carry four things:

- **A name and a role.** "You are Leigh Josephs, the Product Owner." Not "a product owner".
- **What they are not.** "You are not an engineer" is what surfaces jargon. Without it the critic reads schema names as normal.
- **What they own and what they do with this.** "You own the PRD and write the JIRA stories from it." This is what makes the critic ask whether the ask is even theirs.
- **How they read.** "You are busy and you will read this once." Kills the defence that something is explained further down.
- **What they already know, and who told whom.** "You told Albert in Monday's check-in that the Admin Portal
  PRD exists." A critic holding that fact flags being informed of it; a critic without it reads the same
  sentence as news and finds nothing. Everything else in the cast can be read off the artefact - **this has to
  be asked for**, and it is the element most often missing. Measured 2026-09-09: a mail opened by telling a
  Product Owner her own product had two PRDs, which she had said in a meeting. Ten drafts in that folder
  contained zero instances of *"you told me"*, *"as you said"* or *"in the meeting"* - the omission was
  systematic, and no file-reading critic could have seen it.

## What goes in the prompt

Every one of these earned its place. Drop one and the run gets measurably worse.

**The artefact, and only the part the reader sees.** Most artefacts have a working layer the recipient never gets — notes above a `---`, a scratch section, commented reasoning. Paste the reader-visible part into the prompt **verbatim, line breaks intact, between two `---` markers**. Do not hand over the file path instead. A path gives the critic your scratch layer and leaves you defending it with "ignore everything above the divider", which is a guard that can fail. If the reader-visible part runs past roughly 400 lines, give the path, name the exact heading or line range to read, and name what to ignore.

Measured across 5 baseline runs on one mail: two handed over the path, two pasted the body cleanly, one pasted it as a single run-on paragraph with the mail's line breaks destroyed. Three shapes from five runs. The critic read a different artefact each time.

**The sources, with paths the critic can actually open.** Repo-relative only if the critic will start in that repo; otherwise absolute. A path that looks plausible but does not resolve is worse than no source at all — the critic reports the claim as *unverifiable* rather than as *false*, and an unverifiable claim reads like a nitpick, so you drop it. Measured: 1 of 3 transfer runs emitted `docs/adr/0012-quota-store.md` for a file that sat under no `docs/` directory anywhere. It copied the path style out of the worked example below, where the paths are illustrative.

The PRD, the ADRs, the ticket, the sibling documents already in flight with this reader. Say what each is for. This is the difference between "this claim is unclear" and "this claim is false, here is the line". Include what the reader has *already been told* — two of the sharpest findings were a repeated ask and a correction to a mail never sent.

**Praise is discarded.** Say it outright: *"Praise is worthless and will be discarded. Report only what is wrong."* Without it you get a compliment sandwich and lose a third of the output.

**Named suspects — the name, and nothing after it.** List the specific terms, claims and counts to be hard on, by name. Every run returned hits on exactly the items named and few elsewhere. A critic told to look for jargon finds none; a critic given six words finds four.

Stop at the name. Do not append what you expect to be wrong.

- Write: `Be hard on: erasure, the trail, contract-only, the eleven amendments, the 40% figure.`
- Not: `Be hard on the eleven amendments — count them, it is really nineteen.`
- Not: `Be hard on the PRD claim — check whether it says that or the opposite.`

Measured: 5 of 5 baseline runs wrote the second shape. Each one handed the critic the finding and demoted the read to a confirmation. This is the same rule as *Do not tell it what you think is wrong* below, and it is the one the prompt-writer breaks without noticing, because attaching the check to the suspect feels like being helpful rather than like seeding.

**Falsifiable claims, called out as such.** Where the artefact says a source says something, tell the critic to open that source. Two runs found a merged, reviewed document asserting something the source did not say.

**Exact quotes.** *"Each defect with the exact sentence quoted."* An unquoted defect cannot be acted on and cannot be checked.

**One verdict, one blocker.** End the prompt with: *"Then one line: could you act on this today without a follow-up question — yes or no, and if no, the single blocking thing."* This produced the most useful sentence in every run, and it is what turns a defect list into a next action.

**A word cap.** Under 600 words forces ranking. Ask for worst-first.

**One complete message.** Say: *"Return the whole list in one message."* Two runs came back as continuations with the top of the list missing, and each cost a round trip to recover.

## What to leave out

**Do not tell it what you think is wrong.** The prompt sets up the read; it does not seed the answer. A prompt that lists your suspicions gets them confirmed.

**Do not ask for fixes.** A critic that proposes rewrites stops looking. Findings only; you decide the fix.

## The prompt, in order

Fill the brackets. Keep the order — the cast has to land before the critic sees a word of the artefact, or it reads as a proofreader who has been told a backstory.

```
You are [NAME], [ROLE]. You own [WHAT THEY OWN], and you [WHAT THEY DO WITH THIS ONE].
You are not [WHAT THEY ARE NOT]. You are busy and you will read this once.
You already know, because you said it or decided it yourself: [WHAT THE READER TOLD THE SENDER
OFF-RECORD, AND WHEN]. Nobody needs to tell you these.

Read only what is between the markers. It is the whole of what you received.

---
[READER-VISIBLE ARTEFACT, VERBATIM, LINE BREAKS INTACT]
---

Do not spawn sub-agents or delegate any part of this — read and verify every source yourself.
Open these before you answer, and check the artefact's claims against them rather than
taking its paraphrase on trust:
- [PATH THE CRITIC CAN OPEN] — [what it is and what it is authority for]
- [PATH THE CRITIC CAN OPEN] — [what it is and what it is authority for]

Praise is worthless and will be discarded. Report only what is wrong.

Be hard on: [BARE LIST OF TERMS, CLAIMS AND COUNTS. NAMES ONLY, NO CHECKS ATTACHED].

Where the artefact says a source says something, open that source and quote what it
actually says next to the claim.

[TOOL TRAPS, if the critic will search this machine]

Each defect with the exact sentence quoted. Worst first. Under 600 words. Do not propose
fixes or rewrites — findings only. Return the whole list in one message.

Then one line: could you act on this today without a follow-up question — yes or no, and
if no, the single blocking thing.
```

Two lines carry more than they look like. *"It is the whole of what you received"* is what stops the critic hunting for context it was not given and then reporting the absence as a defect. *"Do not propose fixes or rewrites"* has to sit next to the output shape, not in a rule of its own further up, or it gets read as a preference.

## Worked example

An engineer mails a Product Owner about a build that diverged from the spec. The mail carries a scratch layer above a `---`, cites two documents, and makes a count claim.

```
You are Leigh Josephs, Product Owner. You own docs/PRD-notifications.md and you write
the JIRA stories from it, including EVRD-1234 — the amendments this mail asks for are
yours to make, before Thursday's refinement. You are not an engineer. You are busy and
you will read this once.

Read only what is between the markers. It is the whole of what you received.

---
Hi Leigh,

Following up on the notification preferences work. Three things.

First, the PRD (docs/PRD-notifications.md) says every user gets granular
per-channel opt-out. We built channel-level only. The consumer group rebalance
made per-user fan-out non-viable at our current partition count, so the
idempotency key is now scoped to the channel rather than the subscriber.

Second, the audit found that 40% of our users never open the digest. On that
basis I think we should default the digest to off for new signups.

Third, EVRD-1234 (docs/EVRD-1234.md) is written against the old behaviour. It
needs eleven amendments and eight corrections before it can be estimated. Could
you get those in before Thursday's refinement?

Thanks,
Albert
---

Open these before you answer, and check the mail's claims against them rather than
taking its paraphrase on trust:
- docs/PRD-notifications.md — the PRD you own. Authority for what is in scope for v1,
  what is deferred, and who signs off on a default.
- docs/EVRD-1234.md — the ticket you own. Authority for its acceptance criteria and for
  what the engagement audit actually sampled.

Praise is worthless and will be discarded. Report only what is wrong.

Be hard on: granular per-channel opt-out, the 40% figure, defaulting the digest to off,
eleven amendments and eight corrections, consumer group rebalance, idempotency key,
partition count, Thursday.

Where the mail says a source says something, open that source and quote what it actually
says next to the claim.

Each defect with the exact sentence quoted. Worst first. Under 600 words. Do not propose
fixes or rewrites — findings only. Return the whole list in one message.

Then one line: could you act on this today without a follow-up question — yes or no, and
if no, the single blocking thing.
```

The source paths in that example are written short for readability. Real ones must resolve from wherever the critic starts — check them before you hand the prompt over.

Note what the suspect list does **not** do. It names `the 40% figure`, not *the 40% figure — check what population it was measured against*. The second version is the finding. Writing it into the prompt means the critic confirms your reading of the audit rather than doing its own, and if your reading is wrong the run cannot tell you so.

## Tool traps to carry into the prompt

Paste these into any prompt whose critic will search this machine:

> bash `grep` treats an unescaped `$` as an end-of-line anchor anywhere in the pattern and silently matches NOTHING. Use `grep -F` or bracket the sigil. Positive-control before reporting anything as absent — run the same search for something you know is there.

Add per-source traps where they apply: a shallow clone makes any history figure a floor, and a PDF cannot be grepped, so page ranges must be read.

## After the run

**Verify before you act.** A critic's finding is a hypothesis with a citation. Open the line yourself. Across three runs the critic was right nearly every time and wrong at least once per run, and the wrong one was stated as confidently as the rest.

**A finding that changes the answer is not a wording fix.** One run holed the central argument of the artefact rather than its prose. When that happens, stop editing and re-decide.

**Check the fix for over-shoot, because a correction lands harder than the thing it replaces.** A critic narrows a claim; the fix narrows it one step further and states the result absolutely. The new sentence sounds decisive, carries the authority of having just survived review, and is wrong in a way the original was not.

The tell is an absolute that the source does not carry: *no content at all*, *never*, *nothing to escape*, *the only surface*. Take each one back to the line it rests on and read what that line actually bounds. A source saying *"never holds **formatted** content"* does not say *no content*; a source saying *"the reason is optional"* does not say *there is no reason*.

Measured: a third run found an escaping test deleted as "vacuous" from a spec already pushed, because a fix for an earlier finding read *"never holds formatted content"* as *holds no text*. The trail records ordinary fields verbatim, so a script payload in an article title would have been stored and rendered — and the test that catches it was the one the fix removed.

Two habits close it: after fixing, **re-read the fix against its own citation** rather than against the finding it answers; and **grep your absolutes** across everything the fix touched, since the over-shot sentence usually gets copied into a sibling document in the same pass.
