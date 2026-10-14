# Judging legs

A planned leg is judged exactly as a walked one — the verdict just costs less to act on before the work exists.

## Shapes to recognise (step 3)

- **The chain** — leg 2 unblocks leg 1, leg 3 unblocks leg 2, and by leg 5 the north star is out of sight.
- **Gold-plating** — a north-star item met, then extended past it: config for a value nobody asked to configure, a second variant, a generalisation for a caller that does not exist.
- **The yak-shave** — tooling, local env, test harness, CI, or a dependency upgrade taken on to make the real work possible. Where the week goes when nobody names the return point.
- **The incidental refactor** — a file touched for a real reason, then cleaned up well beyond that reason. Ask what breaks if it is reverted and the north-star change re-applied minimally.
- **The unrelated bug** — a genuine defect found in passing and fixed here. Usually its own ticket rather than this journey's leg.
- **Rebuilding what exists** — a helper, component or service written because the existing one was not found. "There was nothing to reuse" is a claim; grep for the thing before the leg counts as on-path.
- **The abandoned leg** — work started, superseded, and left sitting in the diff. Dead code holds no route to a north-star item.

"It needed doing" is not a route back to the north star.

## Pivot or creep (step 4)

Both surface the same way — a leg whose intent no north-star item holds.

- **Pivot** — a decision was taken (in a PR comment, a refinement, a stakeholder chat) that genuinely moved the goal, and nobody updated the ticket. It belongs on the ticket as a north-star item, so the next journey check measures against the real target.
- **Creep** — no decision, just momentum: the work grew because it sat adjacent to work in hand. Drop it, or split it out as its own ticket.

Point at the decision before calling something a pivot. A decision the evidence cannot produce is creep.
