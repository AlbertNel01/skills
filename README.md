# skills

Albert Nel's agent skills for [Claude Code](https://code.claude.com), distributed as a plugin
marketplace.

## Install

```
/plugin marketplace add AlbertNel01/skills
/plugin install thinking-skills@albertnel
```

From a terminal instead of a session:

```bash
claude plugin marketplace add AlbertNel01/skills
claude plugin install thinking-skills@albertnel
```

To pick up changes later, refresh the catalogue and then the plugin — `marketplace update` alone only
re-reads the catalogue, it does not move an installed plugin:

```
/plugin marketplace update albertnel
/plugin update thinking-skills@albertnel
```

Restart the session to apply.

The plugin declares no `version`, so its version resolves to the commit sha and every push to `main` is
picked up by that update — there is no version to bump and no release step. See
[ADR 0002](./docs/adr/0002-no-version-field-in-plugin-json.md).

## Plugins

### `thinking-skills`

Six skills that check work rather than produce it. Each is invoked by name
(`thinking-skills:converge`) or picked up automatically when its description matches what you're doing.

| Skill | Use it when |
| --- | --- |
| `converge` | A decision is in play and the recommendation needs hardening — verify its facts, sweep a fresh angle set each pass, hold or reverse with the reason named. |
| `critic-prompt` | An artefact is finished and you want it torn apart by the person who actually receives it — produces one paste-ready prompt that casts a fresh agent as that named reader. |
| `double-check` | An artefact is about to leave your machine — an email, a PR body, a ticket comment, a figure quoted to a person — and its claims need anchoring to the evidence behind them. |
| `journey-check` | A feature, fix or epic is mid-build and you want to know whether it still leads where it was started to lead. |
| `plan-preflight` | An implementation plan is about to be executed — its tests are code nobody has run and its claims about the codebase are recollections nobody has looked up. |
| `whats-next` | You're picking work back up, or want the single next move named with its baton holder and done-signal. |

They divide by what they test. `converge` tests whether the **answer** is right. `double-check` tests
whether the **wording** outruns its evidence. `journey-check` tests whether the **direction** is still
the one that was chosen. `plan-preflight` tests whether a **plan** can fail — whether each test it
specifies has an edit that turns it red, each claim it makes survives a lookup, and what it never names —
the files in its blast radius, the deploy window in its pre-mortem — is found anyway. `critic-prompt` tests
nothing itself — it builds the prompt that makes a **reader** test the artefact, which is what catches the
defects only a stake can see. `whats-next` tests nothing either — it reports standing and picks the next
move.

`double-check` and `critic-prompt` both aim at a finished artefact and are not substitutes. `double-check`
reads it against its own sources and asks whether each claim is carried. `critic-prompt` hands it to
somebody with a stake and asks whether they could act on it.

`double-check` writes its accumulated real-world findings to `~/.claude/double-check/overreach-log.md`,
outside this repo and outside the plugin. That is deliberate — see
[ADR 0001](./docs/adr/0001-personal-defect-log-lives-outside-the-plugin.md).

`plan-preflight` keeps the general defect classes here and expects each project's own traps to live in that
project, at `docs/agents/plan-preflight.md` or wherever the repo already points agents. A trap from one
codebase loads uselessly in every other, and a dispatched subagent can read the repo but not your memory.

## Layout

```
.claude-plugin/marketplace.json          the marketplace catalogue
plugins/thinking-skills/
  .claude-plugin/plugin.json             the plugin manifest
  skills/<name>/SKILL.md                 one directory per skill, auto-discovered
CONTEXT.md                               glossary
docs/adr/                                decisions and why they were made
```

Skills are auto-discovered from `skills/`, so adding one is a new directory with a `SKILL.md` and
nothing else — no manifest edit.

## Working on this repo

Validate before pushing:

```bash
claude plugin validate .
```

It warns about the missing `version` field. That warning is expected and deliberate; do not silence it
by adding a version without reading ADR 0002 first.

To try a change without pushing, add the working copy as a local marketplace:

```bash
claude plugin marketplace add ./
```

## Licence

MIT — see [LICENSE](./LICENSE).
