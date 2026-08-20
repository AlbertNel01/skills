# Skills

A plugin marketplace holding Albert Nel's agent skills for Claude Code. The domain is the vocabulary of
distribution (how a skill reaches a machine) and the vocabulary the skills themselves define (the concepts
a reader must not conflate when editing them).

## Language

### Distribution

**Marketplace**:
A catalogue listing plugins and where each one lives. This repo is one marketplace, named `albertnel`.
_Avoid_: registry, store, index

**Plugin**:
An installable unit within a marketplace. It has a manifest and ships one or more skills. This repo holds
one, named `thinking-skills`.
_Avoid_: package, extension, bundle

**Skill**:
One directory holding a `SKILL.md` and its reference files, invoked by the `name` in its frontmatter. The
unit of behaviour; never the unit of installation.
_Avoid_: command, prompt, playbook

### What the skills test

**Converged**:
The state a recommendation reaches when a pass that opened genuinely new angles left it unmoved. Distinct
from agreed or finished.
_Avoid_: settled, final, done

**Oscillation**:
A change of position driven by an argument already on the table, re-weighted. The failure mode convergence
is defined against; the two look identical from the prose alone.
_Avoid_: flip-flopping, second-guessing

**Overreach**:
A claim wider than the evidence behind it — sourced, true-sounding, and reaching past what its artefact can
support. Not an error of fact; an error of reach.
_Avoid_: exaggeration, inaccuracy, overstatement

**Load-bearing claim**:
A claim a reader could act on, quote, or sign off. The unit `double-check` examines.
_Avoid_: key point, assertion

**North star**:
The intent a piece of work was started to serve, reduced to outcomes that must be true for it to be done.
Owned by the ticket or the originating request, never by the branch.
_Avoid_: goal, objective, requirement

**Leg**:
One purpose pursued within a journey, dated and evidenced. The unit `journey-check` judges against the
north star.
_Avoid_: step, task, phase

**Baton**:
The single holder of a move — the user or the agent — assigned to whoever takes the first action in it. A
move without one cannot be acted on.
_Avoid_: owner, assignee

### Artefacts

**Overreach shapes**:
The distributed catalogue of ways overreach has recurred, written with invented examples. Ships inside the
plugin.
_Avoid_: examples, patterns

**Overreach log**:
The personal, undistributed record of real overreach caught in real work. Lives outside this repo, on the
machine that caught it.
_Avoid_: log, findings
