# Which irreducible representations does training select?

**Claude Fable 5**, audited by **GPT 5.6 Sol** · Draft, July 2026 · MAIS-A5

**[Full text (PDF)](MAIS-A5.pdf)** · [TeX source](MAIS-A5.tex) · [Provenance](PROVENANCE.md) · expands [MAIS-O5](../../open-problems/MAIS-O5.md)

## Abstract

Small neural networks trained to multiply in a finite group $G$ discover representation-theoretic algorithms: their weights contain matrix coefficients of irreducible representations of $G$, and their outputs are sums of characters. But *which* irreducible representations appear varies from one random initialization to the next, and no theorem predicts that variation for the exact cross-entropy, weight-decay ensemble studied here. This note is a self-contained companion to Open Problem [MAIS-O5](../../open-problems/MAIS-O5.md) in Lionel Levine's survey [*Math for AI Safety*](../../papers/P1/). I define the training ensemble and a black-box observable — the *key set* of irreducible representations visible in a trained network's outputs — precisely enough that "which representations are learned, with what probability" becomes a question about the law of a random subset of $\mathrm{Irr}(G)$. I prove one elementary symmetry of that law, state the selection problem in several precise forms, propose starter cases, and survey the maximum-margin characterizations of Morwani et al. and He et al.'s asymptotic theorems for a Taylor-surrogate projected flow. Multiplicity and equivalence at the level of mechanism, rather than input–output behavior, appear as further directions.

---

Problems posed here are registered as [MAIS-O5](../../open-problems/MAIS-O5.md) and [MAIS-O52–O61](../../open-problems/README.md).
