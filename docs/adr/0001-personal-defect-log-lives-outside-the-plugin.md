# The personal defect log lives outside the plugin

The `double-check` skill instructs the agent to append every new shape of overreach it catches, together
with the sentence that carried it. Those entries are drawn from real work, so they carry real schema names,
real row counts and the recipient of whatever was being written. Accumulating them inside a public,
distributed skill turns a teaching artefact into a standing disclosure channel — one that leaks a little
more on every use, at the moment the author is thinking about something else.

So the skill ships `overreach-shapes.md`, a catalogue of the shapes written entirely with invented examples,
and directs real finds to `~/.claude/double-check/overreach-log.md` on the user's own machine. The filename
`overreach-log.md` is in `.gitignore` at the repo root as a second line of defence.

## Consequences

The log does not travel between machines and is not backed up by this repo — that is the point, and it is
the cost. The skill degrades gracefully when the file is absent: `overreach-shapes.md` alone still teaches
the five lenses.

Anyone editing `double-check` must keep the two apart. An example added to `overreach-shapes.md` is invented
or it does not go in.
