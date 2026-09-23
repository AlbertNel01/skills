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

**Named red**:
The exact edit to the implementation that turns a specified test red. The unit `plan-preflight` demands per
test; a test without one asserts nothing, however green it runs.
_Avoid_: failing case, negative test

**Blast radius**:
Every file a change reaches — created, edited, or broken because something it calls changed — found the
way the code reaches it, not the way the plan names it. `plan-preflight` lists the files the plan never
names apart from the rest.
_Avoid_: impact, scope, footprint

**Pre-mortem**:
The plan assumed shipped and failed, with each cause written as the failure it produces, the plan task
that mitigates it (or none), and the mitigation proposed — two fields, never merged. Includes the deploy window, when old and new code share everything between them — database, queues,
caches, files, and the API an old client calls on a new server.
_Avoid_: risk assessment, what-ifs

**Defect class**:
A shape of plan defect that recurs across codebases, stated so it can be checked against any task. Ships in
the skill.
_Avoid_: bug type, anti-pattern

**Project trap**:
The project-specific shape a defect class takes in one codebase — the config that swaps a class out, the env
var a command actually reads. Lives in that project, never in the skill.
_Avoid_: gotcha, quirk, footgun

**Cast**:
The named reader a critic is instructed to be — name, role, what they own, what they are not, how they read,
and what they already know because they said it themselves. What makes a critic report defects that cost
something rather than style notes.
_Avoid_: persona, character, role-play

**Named suspect**:
A term, claim or count the critic is told to be hard on, written as the bare name with no check attached.
Attaching the expected finding demotes the read to a confirmation of it.
_Avoid_: hint, focus area, hot spot

**Reader-visible layer**:
The part of an artefact its recipient actually receives, pasted into the critic prompt verbatim. Distinct
from the working layer — scratch notes above a divider, commented reasoning — which never reaches them and
must never reach the critic either.
_Avoid_: the draft, the body, the content

### Artefacts

**Overreach shapes**:
The distributed catalogue of ways overreach has recurred, written with invented examples. Ships inside the
plugin.
_Avoid_: examples, patterns

**Overreach log**:
The personal, undistributed record of real overreach caught in real work. Lives outside this repo, on the
machine that caught it.
_Avoid_: log, findings

**Worked example**:
The single run that produced `plan-preflight` — eleven defects, how each was caught, and the project traps
they exposed. Evidence for the classes, not a second copy of them. Ships inside the plugin.
_Avoid_: case study, examples
