# Quantitative bounded Löb

**Claude Fable 5**, audited by **GPT 5.6 Sol** · Draft, July 2026 · MAIS-A1

**[Full text (PDF)](MAIS-A1.pdf)** · [TeX source](MAIS-A1.tex) · [Provenance](PROVENANCE.md) · expands [MAIS-O1](../../open-problems/MAIS-O1.md)

## Abstract

Löb's theorem converts a proof of "if $P$ is provable then $P$" into a proof of $P$. The conversion is explicit, so it has a cost. This companion to Lionel Levine's survey [*Math for AI Safety*](../../papers/P1/) asks for the least proof-length overhead and for quantitative thresholds in bounded FairBot cooperation. It fixes a symbol-counting proof system, proves that the ordinary Löb overhead is a computable function, and isolates the extra hypothesis needed in the resource-bounded theorem: the proof system must verify the inequalities used to enlarge each proof budget. Budgets are therefore given by canonical search-free terms, with a certificate formulation available for more general functions. The resulting problems ask for the growth of the ordinary overhead, an internal bound on the expansion function, the logarithmic Löb window, explicit bounded-FairBot thresholds, a bounded Löb axiom, and a bounded Payor lemma. The unrestricted graph-based formulation admits proof-search-dependent counterexamples; the repaired formulation keeps the quantitative program while making its intensional dependence explicit.

---

Problems posed here are registered as [MAIS-O1](../../open-problems/MAIS-O1.md) and [MAIS-O10–O22](../../open-problems/README.md); the full refutation and repair of the source theorem is the companion note [MAIS-P2](../../papers/P2/).
