---
name: whats-next
description: Report where the work stands, the goal it serves, and the single next move — who holds it, how it follows from what just finished, and what comes after it. Use when the user asks what's next, what they should do now, where things stand, or is picking work back up after a break.
---

# What's next

Answer one question: **what is the next move, and who makes it.** Everything else in the report exists to make that move make sense — the standing it follows from, the goal it serves, and the moves it unblocks.

**The baton.** Every move belongs to exactly one holder — **you** (the user) or **me** (the agent). A report that names a move without naming its holder leaves the user unable to act on it, which is the whole failure this skill exists to fix. The baton goes to whoever takes the *first* action in that move: work I run once the user picks between two options is theirs, because the pick comes first.

**The shape is the whole report.** Everything found while establishing the standing lands inside a slot of the shape in step 5 — a finding that justifies a move goes on that move, and anything with no slot is cut. An audit appended after the shape is the state-dump this skill replaces.

**Mark claims in place**, in the clause that makes them: `v3.2.0 never shipped (claimed — tags only; the deployment config repo is unreadable from here)`. A caveat parked in a closing paragraph is read after the decision it should have qualified.

Scope is whatever the invocation names — a ticket, an epic, a repo, a branch. With nothing named, scope is the work of this session.

This is a query, not an audit: take the cheapest evidence that settles each claim. To judge whether the work is still aimed at the right goal rather than what its next step is, use `journey-check` instead.

## Process

### 1. Fix the goal
State in one line why this work exists, quoted from its source — the JIRA ticket's Description and Acceptance Criteria, the bug's reproduction, or the user's originating request. A goal states an outcome, not a task. Quote the intent itself; where a source says only where the work came from, the *unwritten intent* label carries that on its own.
**Done when:** the goal line quotes a source fetched this session, or is labelled *unwritten intent* when it lives only in the conversation.

### 2. Establish the standing on evidence
Where the work actually stands now — not what the conversation remembers. Check the branch state, the working diff, open PRs and their review state, the ticket's lane, and the last test or build run. Every item believed finished is **verified** (a command output, a merged PR, a green test names it done) or **claimed** (believed done, unproven). Say which. `/skills/journey-check/evidence-sources.md` has where each source lives and how to fetch it — read its *North star* and *The three places* sections.
**Done when:** the last completed move is named with the evidence that proves it, and every other believed-done item carries verified or claimed.

### 3. Order what's left onto the critical path
The **critical path** is the chain of remaining moves that gates done; everything else is parallel work. Order the remaining moves by what blocks what, and mark work that sits off the path as parallel or optional.
**Done when:** every remaining move names what it needs before it can start, and off-path moves are marked as such.

### 4. Pick the single next move
Exactly one — the first unblocked move on the critical path. **One action, one done-signal:** a move that needs "and" or a step range is two moves, so take the first and push the rest to *Then*. The same rule binds every *Then* move. Give it a baton holder, a done-signal an observer could check in one line, the link back to what the last completed move produced, and the link forward — why this move rather than another, and why now. Where the move is a decision only the user can make, the baton is theirs and the move is the decision, not the work behind it. A decision between options carries them as a **ranked** list under the move, highest-priority first, one line of reasoning each — a triage whose order is invisible has thrown away its own answer. *Why now* stays one line, about the decision rather than the options.
**Done when:** one move is picked, its done-signal fits one line, and it carries a baton holder, the link to what just finished, and the reason it comes before the rest.

### 5. Report
Build the report from the shape below, read fresh from this file every run. An earlier report sitting in the conversation supplies the delta line's content and nothing else — never its layout, which is how a stale shape survives a re-run.

This shape, in this order, and nothing after it but the offer. Plain markdown: every block label starts its own line, a blank line separates blocks, and each *Then* item starts at column zero as `1.` — the renderer does the spacing.

```
**Changed since last time** — <one line, only on a re-run>

**Standing** — <where the work is now, at most 20 words>
**Goal** — <the outcome this serves>
**Just done** — <last completed move> (<evidence>) — unblocked <what>

**NEXT · <you|me>** — <one action>
1. <option> · <why it ranks here>     ← only when the move is a pick between options
2. …
**Why now** — <what makes this the move ahead of the rest>
**Done when** — <one observable signal>

**Then**
1. <move> · <baton> · needs <what gates it>
2. …
3. …

**Waiting on you**
- <decision> — <what stalls until it lands>

**Loose ends**
- <one line each — findings that belong to no move above>
```

Cap **Then** at three moves — the horizon that makes the next move make sense, not the plan. Cap **Loose ends** at three one-liners and drop the block entirely when there are none; it is the only home for stray findings, so a fourth one gets cut rather than appended elsewhere. Loose ends are inert facts; a finding with a live consequence someone must act on is a move or a *Waiting on you*, because the bottom block is the least-read one in the report. Drop *Waiting on you* the same way when nothing is held by the user, and *Changed since last time* on a first run. A decision the user must make lives in *Waiting on you* alone — *Then* holds moves, including the user's own actions, so a decision listed in both is one item read twice. When a re-run reverses or widens the last report's standing, that one line says so plainly — a correction belongs at the top, not folded into the standing as though it always read that way. Close with an offer to start the first move whose baton is mine, whether that is the next move or one further down.
**Done when:** every block of the shape is present or deliberately dropped, both caps hold, unverified claims are marked in place, the baton holder is named on the next move and on each *Then* move, `Goal` stands on its own line, and nothing follows the shape except the offer.
