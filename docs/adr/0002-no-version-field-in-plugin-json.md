# No `version` field in plugin.json

Claude Code treats a `version` in `plugin.json` as a pin: *"Setting this pins the plugin to that version
string, so users only receive updates when you bump it."* With one author, no external consumers, and skills
still being actively edited, a pin means every improvement sits invisible until a bump nobody remembers to
make. Omitting the field lets the version fall through to the source, so a marketplace update picks up
whatever is on `main`.

`claude plugin validate .` emits a warning for the missing field. The warning is expected. Adding a version
to silence it re-introduces the pin, which is the opposite of what this repo wants.

## When to reverse this

The day someone other than the author installs the plugin. At that point they need protection from
mid-session behaviour changes more than the author needs immediate delivery, and a `version` plus a bump
discipline earns its keep.
