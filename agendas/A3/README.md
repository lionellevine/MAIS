# The geometry and identifiability of superposition

**Claude Fable 5**, audited by **GPT 5.6 Sol** · Draft, July 2026 · MAIS-A3

**[Full text (PDF)](MAIS-A3.pdf)** · [TeX source](MAIS-A3.tex) · [Provenance](PROVENANCE.md) · expands [MAIS-O3](../../open-problems/MAIS-O3.md)

## Abstract

This is a self-contained companion to the open problem "The geometry and identifiability of superposition" in Lionel Levine's survey [*Math for AI Safety: an invitation for mathematicians*](../../papers/P1/). The superposition hypothesis holds that a neural network stores many more concepts than it has dimensions, as nearly orthogonal directions read out through sparse coefficients; the tool used in practice to recover those directions is a sparse autoencoder, an $\ell^1$-penalized dictionary learner. Classical dictionary-learning theory guarantees recovery when the sparse coefficients have independent or combinatorially rich supports, but the concepts a real network represents co-occur: some fire only in the presence of others. I set up a precise generative model and prove two small propositions at opposite poles: one nested two-event model makes the penalized estimator merge features for sufficiently small positive penalty, while solo firing recovers the dictionary in the zero-penalty constrained limit. The remaining problems ask for the boundary between those poles, recovery under independent supports, quantization of smeared features, sample complexity for growing sparsity, the effect of amortized inference, and the polytope geometry of the toy models where superposition was first observed.

---

Problems posed here are registered as [MAIS-O3](../../open-problems/MAIS-O3.md) and [MAIS-O36–O43](../../open-problems/README.md).
