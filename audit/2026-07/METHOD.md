# Audit method

The July 2026 review had four layers.

1. **Adversarial review before audit.** A separate AI reviewing agent read each agenda for mathematical precision, accessibility to mathematicians outside machine learning, and whether the literature discussion supported the claimed frontier. See the [review note](PRE-AUDIT-REVIEW.md).
2. **Full audit.** GPT 5.6 Sol checked each displayed proof and substantial background result; classified each numbered research item for precision and apparent open status; and recorded searches for related work. The eight reports cover 55 proved or background results and 97 numbered items.
3. **Scoped verification.** A separate Claude pass re-derived the findings whose acceptance could remove, settle, refute, or substantially rewrite mathematical content. Of 19 such findings, 16 were confirmed, three were narrowed, and none was rejected. This was deliberately narrower than a second full audit.
4. **Repair and gate.** GPT 5.6 Sol implemented the accepted repairs. A final Claude gate checked the repaired TeX against the dispositions, checked house style and references, and compiled each agenda. Lionel Levine directed the project and made the publication decisions.

## What the records mean

The reports in [`sol/`](sol/) are snapshots of pre-repair drafts. Their objections should be read together with the [repair log](REPAIR-LOG.md), not as descriptions of the current files. The reports in [`verification/`](verification/) independently check selected audit verdicts, not the whole agenda. The [gate summary](GATE-SUMMARY.md) records that the accepted repairs were present and that the files built; it is not an independent proof of every current statement.

Open-status searches were broad but cannot prove a negative. “No resolution found” means no resolution was located in the recorded search, as of the date in the report. It does not mean that no resolution exists.

## Limits

Every substantive pass described here was performed by an AI system. Model agreement is useful evidence against easy-to-miss errors, but the systems are not statistically independent and this process is not conventional peer review. No human has verified every line. Readers should treat the agendas as research invitations with an unusually visible error-correction trail, not as certified reference works.
