# Worked example — the run that produced this skill

One nine-task implementation plan, executed by fresh subagents with a review after each task. **Eleven defects surfaced. Every one was in the plan, not in an implementation.** The plan's own self-review — spec coverage, placeholder scan, type consistency — had passed clean before dispatch.

Five were in test scaffolding: the part of a plan its author writes last, from memory of the codebase rather than from the codebase.

## The eleven, and how each was caught

| # | Defect | Caught by |
|---|---|---|
| 1 | Test asserted `Illuminate\Support\Carbon`; the app calls `Date::use(CarbonImmutable::class)`, so the cast returns a different class and the assertion could never pass. | Implementer, on first run. Reported as a deviation rather than silently changed. |
| 2 | Reversibility check set `TEST_DB_DATABASE`, which only the Pest bootstrap reads; `artisan migrate` resolves the default connection from `DB_DATABASE`. The command targeted the wrong database. | Implementer. Controller then verified the real database was untouched rather than trusting the report. |
| 3 | Subsidiary Target test could not go red: fixture used a template with empty defaults, so the failure mode was unreachable. | Implementer, by **deleting the line the test protected and watching the test still pass**. The single highest-value move in the run. |
| 4 | Same test's assertion was `toContain`, blind to the spurious extra row that was the actual failure mode. | Controller, tracing why #3 was unreachable. Both had to be fixed; either alone left the test blind. |
| 5 | `reframed_experience_text` set by the fixture, carried by the code, asserted by nothing. | Task reviewer, diffing the requirement's field list against the assertion chain. |
| 6 | Fixture left `target_end_point_date` null while a test asserted `isAchievedEarly()`, a helper that reads exactly that column. The assertion could never pass. | Implementer, who fixed the fixture and described it as "necessary for proper test semantics" without saying why. Controller traced the real cause. |
| 7 | `assertDontSee('more than dates and numbers')` — the same phrase sat in the explainer rendered at the top of the page under test, so the assertion failed unconditionally and its paired `assertSee` proved nothing. | Controller, in pre-flight, by grepping the page's rendered sources for the literal. |
| 8 | Two tasks' **Produces** lists named methods (`rolloverState`, `substantiveChanges`) that the plan's own component and template never called. Building them meant unused code; not building them meant failing a stated contract. | Controller pre-flight for the first; missed for the second and found at review. |
| 9 | Plan predicted "two cases will fail on the missing route". One did — the other returned early before reaching it. A count used as a filter can hide a real failure. | Controller, tracing both tests before dispatch. Replaced the count with the failure's signature. |
| 10 | A manual step instructed walking the feature end-to-end against the local database — which held live user records. | Controller pre-flight. Step removed from the implementer's scope. |
| 11 | Plan-provided code omitted a guard, so an action could stamp "consulted at" — a timestamp asserting a human had been consulted — when they had not. | Task reviewer flagged the missing guard; the controller supplied the consequence the reviewer had not named. |

## Project traps this exposed

These are the *project-specific shapes* of the classes. They belong beside their project, not in a general skill — a trap from one codebase loads uselessly in every other. Collect the equivalent set for whatever project you are in.

| Trap | The positive form |
|---|---|
| `Date::use(CarbonImmutable::class)` swaps the concrete date class | Assert `Carbon\CarbonInterface`, which both classes satisfy. |
| `TEST_DB_DATABASE` is read by the Pest bootstrap; `artisan migrate` reads `DB_DATABASE` | Match the env var to the mechanism that reads it. |
| Pint skips `*.blade.php` unless a path names one explicitly | Lint with the repo gate, `pint --parallel --test`. A blade path named directly reports failures the real gate never sees — this produced one false review finding and one phantom bug hunt. |
| Models use a `#[Fillable]` attribute, not a `$fillable` property | A column absent from it mass-assigns to nothing, silently. A test that mass-assigns is what catches it. |
| Blade components carry typed props | Open the component. `step-card` requires `title`; `autosave-input` is namespaced and requires `storageKey`; `clarity-warning` is purpose-specific, not a generic warning box. |
| `Target::branch()` re-creates rows with fresh primary keys | Identity across versions is `text`, never the id. |

## What the run says about where defects live

The implementation code the plan specified held up. The scaffolding around it did not. Three separate times an implementer was right against the plan's instruction, and said so instead of quietly complying — each time because the plan's author had written from recollection where a lookup was available.

The two most productive habits, both cheap:

- **Delete the line the test protects and watch the test fail.** If it stays green, the test is decoration.
- **When an implementer reports a deviation, trace the cause yourself.** Twice a report gave a true fix with an under-specified or wrong reason, and the real reason mattered more than the fix.
