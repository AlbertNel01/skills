---
name: status-check
description: Snapshot of exactly where the work stands right now — what is running, what needs you, what blocks each PR, and how far along the work is.
disable-model-invocation: true
---

# Status check

A **snapshot**: the state of the work at this second. Not a plan, not a history, not a next
move — `whats-next` picks the single next move, `journey-check` judges whether the work still
aims at its goal. This one answers *where are we and what is moving.*

**Signals are inputs, not blocks.** Most of what you gather never prints. A fact **earns a
line** by blocking something, by changing what the user would otherwise assume, or by being
asked for by the shape. Everything else stays in your head — reporting it costs the user the
one thing the snapshot exists to give them, which is speed.

Three rules on what does print:

- **Report the work, never the report.** "Snapshot only, nothing edited this run" describes
  the exercise and tells the user nothing about their work.
- **Absence carries its reason.** "No PRs" is half a fact. "No PRs, and none can exist yet —
  nothing is pushed, the branch has no upstream" is the whole one.
- **Every count names what it was measured against** — `4 of 5 PRs`, `5 behind origin/main`.
  Run `git -C <repo> rev-parse --is-shallow-repository` before quoting a commit count; when it
  returns `true`, the count is a floor, so write "at least N".

Mark anything believed-but-unproven in place, in the clause that makes the claim:
`suite green (claimed — last run was 40 minutes and 6 commits ago)`.

Scope is whatever the invocation names. With nothing named, scope is the work of this session.

## Signals

The working directory is often not a git repo, so pass `-C <repo>` on every git call and
resolve the repos from what this session actually touched.

1. **Live work — yours only.** Subagents you spawned, your background Bash tasks, your running
   Workflows. From `ListAgents` take your own subagents and drop peer sessions and other
   machines: the user can see their own windows and does not need them counted.
2. **Can a PR exist** — `git -C <repo> rev-parse --abbrev-ref --symbolic-full-name @{u}`.
   That command failing *is* the finding: nothing is pushed.
3. **Must it merge first** — `git -C <repo> fetch --quiet origin`, then
   `git -C <repo> rev-list --left-right --count <base>...HEAD`, with the base from
   `git -C <repo> symbolic-ref --short refs/remotes/origin/HEAD`. Without the fetch the number
   is stale and reads as reassurance. This prints only when it gates something.
4. **Uncommitted work this session left** — `git -C <repo> status --porcelain`, keeping only
   files this session edited. Dirt that was already there is not this session's business;
   name it only where it would interfere with an action you are listing.
5. **PRs — what blocks each one.** GitHub MCP `list_pull_requests` on the head branch. Convert
   the API's state fields into the blocker in plain words: an unresolved-thread count, a named
   merge conflict, a review still owed. Raw fields — `reviewDecision`, `mergeStateStatus`,
   a newest-review timestamp — never print. When a PR's review list comes back with exactly 30
   entries it has silently dropped the newest ones; re-read with
   `gh api "repos/<owner>/<repo>/pulls/<n>/reviews?per_page=100"`.
   A CI failure this repo produces on every PR of that kind is named once at the foot of the
   block, so an unexpected red stands out.
6. **Ticket** — Atlassian MCP `getJiraIssue` for every key named by the branch, the commits or
   the session. Print only its lane and the newest comment that changes something.
7. **Gates ahead — unsatisfied only.** The checks between here and a merge: `pr-gap-check`
   (hook-enforced; the PR tool is denied without it), a ledger entry, a suite re-run after a
   merge, unresolved review threads. A gate already satisfied is not a gate — leave it out.

**Done when:** each of the seven signals has been read this run, and each has either earned a
line or been deliberately left out.

## Needs you

The user's highest-value block, so give it the **exact action**, not a description of one: the
file and line, the command to run, or the patch to apply. "The two grep guards need applying"
sends them hunting; the path, the two lines, and why a human has to do it lets them act.

Two lines, one item. Where the user holds nothing, drop the block.

**Done when:** the block names something the user could do in the next minute without asking
you a follow-up question.

## Progress

Progress is **a count with a named denominator**, never a percentage invented from feel.
Take the denominator from a real artefact — the plan document's task list, the ticket's
acceptance criteria, this session's own PR set — and name that artefact in the line.

Where no such artefact exists, say so and list what is done instead. A missing denominator is
itself a finding worth reporting; a guessed one is a false claim.

**Done when:** the progress line names its denominator's source, or states that none exists.

## The surprise

The one fact that changes what the user would otherwise assume — including a thing you told
them that has since become false, especially where you said it somewhere they cannot easily
unsay, like a published PR comment.

Two lines: the fact, and what it changes. The evidence chain that convinced you stays out, and
anything that needs doing about it belongs in **Needs you** or **Before a PR** instead. A
surprise that turns into a paragraph of your own forensics has stopped being for the user.

**Done when:** one surprise is named with its consequence, or the report says a sweep found none.

## Report

Build the report from this shape, read fresh from this file every run. Blank line between
blocks. **Nothing prints outside the shape** — an extra trailing block the user has to decode
is the failure this shape exists to prevent.

```
**NOW** — <the state of the work, in one line>

**Live**
- <what you started> · running <how long> · answers <what question>

**Needs you** — <exact file, line, command or patch>

**Surprise** — <the fact> · <what it changes>

**Progress** — <n of m <units>> · denominator from <artefact>
- <remaining unit> — <what it needs>

**PRs**
- #<n> <what it is> · <blocked by what, in plain words | ready>
- expected across all of them: <the known red, named once>

**Ticket** — <key> · <lane> · <the newest comment that changes something>

**Uncommitted** — <files this session left uncommitted>

**Before a PR** (<which PR or branch>)
1. <unsatisfied gate> — <what it needs>
```

Drop any block that is empty: no live work of your own, nothing held by the user, no ticket,
nothing uncommitted, no surprise. Say "nothing running" or "no surprise" only where the
emptiness itself is the news.

Caps: three **Live** entries, three remaining **Progress** units, four **PRs**, four
**Before a PR** gates, two lines each for **Needs you** and **Surprise**. A fifth item gets
cut, not appended — the snapshot loses its value the moment it stops fitting one screen.
