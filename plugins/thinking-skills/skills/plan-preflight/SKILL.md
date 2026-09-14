---
name: plan-preflight
description: Use when an implementation plan is about to be executed — dispatched to implementers or worked task-by-task — or when a suite is green but you cannot name what would turn it red.
---

# Plan Preflight

## Overview

A plan's test code is code nobody has run. Its claims about the codebase are recollections nobody has looked up. Preflight turns both into checked facts while defects are still free.

**A test that cannot go red proves nothing.** It stays green when the implementation is wrong, and the plan that produced it reads fine the whole time.

## When to use

- Before dispatching a plan's tasks to implementers.
- Before writing the first line of code from a plan, including one you wrote yourself.
- After a plan's self-review passes. That pass checks spec coverage, placeholders and type consistency, and reaches none of the classes below.

For code that already exists, run a code review instead.

## The check

1. **Name the red.** For every test the plan specifies, write down the exact edit to the implementation that turns it red.
2. **Open the file.** For every claim about the codebase — a class, a column, a config value, a command, a component's props — read the source. Recall is not a lookup.
3. **Trace what no red can reach.** Every string a reader will see and every comment explaining *why* — diff it against the spec, ADR or source it restates. Nothing asserts these, so step 1 never sees them. Then run it the other way: for every precondition the change alters, find the strings that were true *because* of the old one.
4. **Walk the classes** against each task.

**Done when** every test has a named edit that turns it red, every claim carries a `file:line`, and every string a reader sees traces to its authority. A test with no such edit is a fixture with an opinion.

## Defect classes

| Class | Name the check | Instance |
|---|---|---|
| **Unreachable failure mode** | Build the failure this test guards, and watch it fail. | A fixture chose a template with empty defaults, so the "carries the source, not the template" test passed with or without the flag it existed to protect. |
| **Non-exhaustive assertion** | Ask whether the assertion pins the whole shape or one member. `toContain`, `assertSee` and substring checks see additions and are blind to spurious extras. | A `toContain` could not see the duplicated row that was the actual failure mode. |
| **Carried but unasserted** | Diff the requirement's field list against the assertion chain, by name. | A field the fixture set and the code carried was asserted by nothing. |
| **Fixture starves its assertion** | For each assertion on a derived helper, trace the helper's inputs and confirm the fixture sets them. | A test asserted a helper while the fixture left null the one column that helper reads. |
| **Assertion string collides** | Grep the rendered sources for the literal. Page copy shares vocabulary with the thing under test. | An `assertDontSee` ran on a phrase that also sat in the explainer rendered at the top of the same page. |
| **Interface list ≠ code beneath** | Read each name in the plan's Produces block against the code the plan gives underneath it. | Two tasks listed methods the plan's own component and template never called. |
| **Counted expectations** | State the signature a failure will carry, not how many failures to expect. A count becomes a filter that hides a real one. | "Two cases fail on the missing route" — one did; the other returned early before reaching it. |
| **Guard omitted where code certifies** | For every write of a timestamp or flag asserting a human acted, find the guard proving they did. | An action stamped "consulted at" unconditionally while its caller never checked the consultation had happened. |
| **Step acts on real data** | Read each manual step for writes outside the test database. | A step told an implementer to mark a real record achieved, in a database holding live user data. |
| **Authority overridden by restatement** | Where the plan words a user-facing string itself, diff it against the spec's. A paraphrase becomes the authority without announcing it. | A shorter button label reverted a wording the spec had deliberately adopted from a later source — and the test asserted only the shared prefix, so it could not tell which shipped. |
| **Statement falsified by the change** | Name the precondition the change alters, then grep the strings that were true *because* of the old one — operator output, a value assembled before the branch that now exits differently, a docblock explaining an absence. | Shipping a missing table turned *"the protection list is absent, so this run certifies nothing"* into *"protection applied and fresh"*, on a run where nothing had been reviewed. |
| **Prose ships as fact** | Read every comment and docblock the plan supplies as a claim, and check it like one. Nothing tests a comment. | A docblock explained a deep link by a picker mechanism the page never uses; it would have shipped verbatim into the codebase. |
| **Anchor is ambiguous** | For each "insert after X", confirm X occurs once, and that *after* means the same to you and the implementer — next sibling, or last child. | "After the button" could mean inside its container or following it; the two put the block in different conditional branches. |

## Red flags

- "The test looks right" — you have not named the edit that turns it red.
- "That's how it's used elsewhere" — elsewhere is a different config.
- "I wrote this plan, I know what's in it" — every defect in the run that produced this skill was in a plan its author had just self-reviewed clean.
- Reaching for a count of expected failures instead of their signature.
- "It's only a comment" — a comment is a claim that ships, and no red edit will ever catch it.
- "That was already there, my change didn't touch it" — a fix retires the reasons other sentences were written. Three defects in one session were existing strings a change had just made false, each caught in review rather than here.
- "That's a copy call" — check whether the authority already settled the wording before offering anyone a choice.

## The project's own traps

Each class above has a project-specific shape: the config that swaps a class out from under an assertion, the env var a command actually reads, the linter that skips a file type. These live **in the project**, not here — a trap from one codebase loads uselessly in every other, and a subagent you dispatch cannot read your memory but can read the repo.

**Read them first.** Follow the repo's own convention for agent docs if it has one — a pointer in `AGENTS.md` / `CLAUDE.md`, a file under `docs/agents/`. Otherwise look for `docs/agents/plan-preflight.md`.

**Write one the first time a preflight surfaces it** — not on first read, so an untouched repo gains no empty scaffold. Create the file at the same path you would have read, and add a pointer from the repo's agent doc, or only this skill will ever find it.

Record what is written nowhere else. Where a trap already lives in a repo doc or an ADR, point at it in one line rather than restating it — two copies drift, and the copy here is the one that goes stale.

`worked-example.md` holds the run that produced this skill: eleven defects, the six project traps they exposed, and how each was caught. Read it when a class above needs a concrete case, or when starting that collection for a new project.
