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

To pick up changes later:

```
/plugin marketplace update albertnel
```

The plugin declares no `version`, so every push to `main` is picked up by a marketplace update — there
is no version to bump and no release step. See
[ADR 0002](./docs/adr/0002-no-version-field-in-plugin-json.md).

## Plugins

### `thinking-skills`

Four skills that check work already in progress, rather than producing new work. Each is invoked by name
(`thinking-skills:converge`) or picked up automatically when its description matches what you're doing.

| Skill | Use it when |
| --- | --- |
| `converge` | A decision is in play and the recommendation needs hardening — verify its facts, sweep a fresh angle set each pass, hold or reverse with the reason named. |
| `double-check` | An artefact is about to leave your machine — an email, a PR body, a ticket comment, a figure quoted to a person — and its claims need anchoring to the evidence behind them. |
| `journey-check` | A feature, fix or epic is mid-build and you want to know whether it still leads where it was started to lead. |
| `whats-next` | You're picking work back up, or want the single next move named with its baton holder and done-signal. |

They divide by what they test. `converge` tests whether the **answer** is right. `double-check` tests
whether the **wording** outruns its evidence. `journey-check` tests whether the **direction** is still
the one that was chosen. `whats-next` tests nothing — it reports standing and picks the next move.

`double-check` writes its accumulated real-world findings to `~/.claude/double-check/overreach-log.md`,
outside this repo and outside the plugin. That is deliberate — see
[ADR 0001](./docs/adr/0001-personal-defect-log-lives-outside-the-plugin.md).

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
