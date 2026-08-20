# Shapes overreach takes

One entry per shape that has reached a finished artefact. The sentence that carried it, the lens that
catches it, and what it was rewritten to. Read this when a claim feels solid and you want to know which
way solid-feeling claims have failed before.

The examples here are invented. Real ones you catch go in your own log — see *Keep your own log* at the
bottom.

## Three columns claiming every column

**Carried by:** *"1,204 `orders` rows byte-identical to the ones on the replica"*, in a report to a data owner.
**Lens:** coverage.
**What was true:** the extract held `order_id`, `customer_id`, `placed_at`. All three matched on all 1,204 rows.
The table has more columns than that.
**Rewritten to:** *"same id, customer and placed-at date on every one"*, with *"every field identical"* attributed
to whoever ran the full comparison.

## A column that exists standing in for values nobody read

**Carried by:** *"Those rows carry `billing_address`, personal data under the policy"*.
**Lens:** coverage.
**What was true:** the `orders` table has a `billing_address` column, at `schema/orders.sql:41-43`. The extract
had no such column, so what those 1,204 rows hold there is unmeasured.
**Rewritten to:** *"`orders` carries `billing_address`"* — the schema fact, asserting nothing about the rows.

## A snapshot that has been edited since

**Carried by:** *"The reporting database's `customers` table is a 2019 snapshot"*.
**Lens:** kind — an inference stated as a measurement.
**What was true:** it began as a copy and has changed since; records were removed and new ids added.
**Rewritten to:** the measured consequence on its own — *"812 of its 900 rows have no `customers` row, so
`customer_status` there cannot gate a delete"*.

## A purpose read off a co-occurrence

**Carried by:** *"The copy was taken in order to split that account onto its own instance"*.
**Lens:** kind.
**What was true:** one account's activity stops on the source and continues on the copy from that point. Why
the copy was made is unevidenced.
**Rewritten to:** *"when that account's activity moved to the second instance"*.

## Clock times from a timezone nobody checked

**Carried by:** *"between 17 October 2019 13:41 and 21 October 2019 07:49"*.
**Lens:** derivation.
**What was true:** the timestamps are Unix epochs rendered in UTC. The server's timezone is unknown, so the
hours are unowned.
**Rewritten to:** *"between 17 and 21 October 2019"* — the part the row ids prove.

## An ask that named more rows than it could act on

**Carried by:** *"are those 1,204 rows ours to delete under the retention rule?"*
**Lens:** scope.
**What was true:** 1,180 had passed the retention period. 24 had not.
**Rewritten to:** *"1,180 of the 1,204 have already passed retention — are they ours to delete as they expire?"*

## A verb with no action behind it

**Carried by:** *"Watch `migration-2.sql:66`"*, in a message to a colleague.
**Lens:** none of the five — found by a reader asking what the sentence wanted from them.
**What was true:** they had never been sent that file, so watching it was not something they could do.
**Rewritten to:** *"Do not apply it — it never went to you."*
**Why it is here:** an instruction is a claim about what the reader can do. The five lenses test claims about
the world; this one shows they need pointing at the ask as well as the evidence, which is why step 1 says the
ask counts.

## An absence claim about other people's thinking

**Carried by:** *"Nobody has thought about what the retention rule does to the reporting copy"*.
**Lens:** coverage, applied to an absence — no file holds what a room has or has not thought about.
**What was true:** `docs/decisions.md` records no decision about the reporting copy, on a search whose control
passed. What anyone has considered in a meeting or in their own head is outside every artefact available.
**Rewritten to:** *"No decision on record covers the reporting copy."*
**Why it is here:** an absence claim inherits the reach of the thing searched. A file search can retire *"it
is not written down"* and can never retire *"nobody thought about it"*.

## A figure that decays with the calendar

**Carried by:** *"1,180 of the 1,204 have already passed retention"*, in a draft that then sat unsent.
**Lens:** derivation — today's date.
**What was true:** 1,180 on the day it ran, 1,182 the next day, 1,196 four days later. A rolling cutoff moves
the count every day the draft waits.
**Rewritten to:** *"1,180 of the 1,204 had passed retention on 20 August"*.
**Why it is here:** a figure computed from `CURDATE()` is a measurement of the day it ran. In a draft that may
wait, the date it ran is part of the figure.

## Keep your own log

The shapes above are the ones that generalise. The ones you catch in your own work carry the schema, the
counts and the recipient of whatever you were writing, so they belong on your machine and not in a
distributed skill.

Append them to `~/.claude/double-check/overreach-log.md`, in the format above — the sentence that carried it,
the lens that catches it, what was true, and what it was rewritten to. Create the file the first time you
need it. Read it alongside this one whenever a claim feels solid.
