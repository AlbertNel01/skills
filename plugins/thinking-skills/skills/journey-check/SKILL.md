---
name: journey-check
description: Map the journey a feature, fix or epic has taken so far and check it still leads to its original intent rather than down a rabbit hole. Use at any point mid-build when the user asks whether the work is still on the right path, or is resuming work whose original goal has gone hazy.
---

# Journey check

Meet a feature, fix or epic wherever it stands — barely started, mid-build, already merged — map the journey it has taken, and judge whether that journey still leads to its **north star**: the intent the work was started to serve.

**Drift compounds.** Each leg of a journey gets justified by the leg before it rather than by the north star, so a chain of individually reasonable hops ends somewhere nobody chose. The map exists to make that chain visible.

## Process

### 1. Fix the north star
Fetch the original intent and quote it — the JIRA epic and every child story (Description, Acceptance Criteria, Technical Criteria, comments), the design doc read from the remote's default branch, the bug report and its reproduction for a fix, the user's originating request where no ticket exists. Reduce it to **north-star items**: the outcomes that must be true for this work to be done. Name every repo the tickets touch — an epic's journey runs across all of them. `evidence-sources.md` says where each source lives and how to fetch it.
**Done when:** every ticket in scope has had Description, Acceptance Criteria, Technical Criteria and comments each read (confirmed present, not assumed empty); every north-star item quotes a line from a source fetched this session; every item whose only home is a doc or repo file is labelled *unticketed* and every item whose only home is the conversation *unwritten*; and the repo list is fixed.

### 2. Trace the journey
The journey runs from the moment the north star was set to now; a session is a slice of it, never its span. It lies in three places, and how far the work has got decides which of them holds it: **merged history** (PRs for this ticket, commits already on the base branch), the **branch** (commits since the merge-base, the working diff, untracked files), and the **unwritten** (work in flight, the plan, decisions taken in conversation). Sweep all three in every repo on the list, then group what they yield into **legs** — one leg per purpose pursued, in the order they happened — each naming what it changed and its date, and citing a commit sha, PR number, or file path. `evidence-sources.md` has the commands, including how to resolve each repo's base branch.
**Done when:** all three places have been swept in every repo, and each one either yielded legs or stands recorded as empty; every commit found and every uncommitted file belongs to exactly one dated leg; and the first leg on the map is the earliest one the sweep found rather than the earliest in this session.

### 3. Judge every leg against the north star
One verdict per leg. **On-path** — advances a named north-star item. **Detour** — advances none directly, but names both the item it unblocks and the point where the journey rejoins the path. **Rabbit hole** — names neither. **Off-journey** — serves a different north star, or the user asked for it outright: name the journey it belongs to and set it aside unjudged. Hold each leg against the north star rather than against the leg that spawned it; sunk cost carries no vote. `judging-legs.md` lists the shapes to recognise.
**Done when:** every leg carries a verdict — on-path and detour verdicts naming their north-star item, rabbit-hole verdicts naming the items the leg was held against, off-journey verdicts naming the other journey — and each rabbit-hole verdict has been re-checked a second time before it reaches the report.

### 4. Check what nobody started
The map shows only where the work went: drift is the loud failure, a north-star item nobody ever started is the silent one. Mark each item **reached**, **in flight** or **untouched** — reached on a named artifact (the passing test, the merged PR, the file on the base branch), rather than on the place you looked. Where a rabbit hole touched the mechanism of an item now marked reached, say in one clause why the item stands without it; absent that clause, one of the two verdicts is wrong. Then read the legs backwards: where a leg implies an intent no north-star item holds, decide between a **pivot** (the goal genuinely moved and nobody recorded it) and scope creep. `judging-legs.md` separates the two.
**Done when:** every north-star item carries one of the three marks with its named artifact; every rabbit hole adjacent to a reached item carries its clause; and every implied-but-unrecorded intent is classified pivot or creep.

### 5. Report the verdict, then the correction
Lead with one line — on path, drifting, or lost. Then the sweep: each of the three places, per repo, and what it yielded, *empty* included. Then the map, one line per leg:

`<date> — <leg> — <verdict> — <north-star item, or none> — <evidence>`

Then the untouched items, the pivots written down nowhere, and a ranked correction list — what to abandon, what to resume, what to record — ranked by distance from the north star.
**Done when:** the user has the verdict line, the sweep, the per-leg map, the untouched items, and the ranked correction list.

## References
- `evidence-sources.md` — where the north star and the journey evidence live, and how to fetch each (steps 1–2).
- `judging-legs.md` — the shapes behind the leg verdicts, and pivot against creep (steps 3–4).
