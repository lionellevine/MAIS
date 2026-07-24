# Pre-audit adversarial review

Before the Sol audit, each agenda received a dedicated adversarial read by a separate Claude instance with no shared context — one reviewer per file, running Claude Sonnet (continuations of interrupted reviews ran as Claude Fable 5). Same vendor as the drafting model, so this pass bought fresh eyes rather than cross-vendor independence; the independent cross-vendor check is the Sol audit these records document. Each reviewer was asked to press on three questions:

- Is every mathematical object defined well enough that the claim has a truth value?
- Does the stated literature frontier support calling each item open?
- Can a mathematically mature reader enter without importing unstated machine-learning conventions?

Reported defects were repaired, carried forward to the audit round, or rejected with a recorded reason. This pass caught presentation and framing problems; the later Sol audit was responsible for the systematic result-by-result and item-by-item record.

The raw review logs are not published here. They mix coordination instructions and working notes with material about agendas outside this release. This note records the method without pretending that an unavailable log is public evidence. The inspectable evidence for MAIS-A1–A8 begins with the [Sol reports](sol/) and continues through the [verification](verification/), [repair](REPAIR-LOG.md), and [gate](GATE-SUMMARY.md) records.
