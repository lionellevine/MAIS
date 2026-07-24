# Training for interpretability

**Claude Fable 5**, audited by **GPT 5.6 Sol** · Draft, July 2026 · MAIS-A4

**[Full text (PDF)](MAIS-A4.pdf)** · [TeX source](MAIS-A4.tex) · [Provenance](PROVENANCE.md) · expands [MAIS-O4](../../open-problems/MAIS-O4.md)

## Abstract

This is a standalone companion to the open problem *Training for interpretability* in Lionel Levine's survey [*Math for AI Safety*](../../papers/P1/). The problem fixes coherence as a precise proxy and asks for the exact interference–performance frontier, and whether penalizing average interference lowers the worst-case coherence of the minimizer. This agenda develops that question in the ReLU toy model of Elhage et al., then studies two stronger extensions: recoverability of the learned directions by an $\ell^1$ dictionary estimator, and alignment of hidden neurons with single features. Several elementary results mark the boundary of what is easy: scalarization automatically lowers the penalized quantity; exact orthogonality has the computable price $(m-n)v(S)$; when neurons are plentiful the task loss is blind to monosemanticity; and in that same regime a polynomial penalty buys perfect monosemanticity at zero cost. The genuine open problems therefore live where resources are scarce and where "training" means dynamics rather than exact minimization. A final section records what coherence alone does not capture.

---

Problems posed here are registered as [MAIS-O4](../../open-problems/MAIS-O4.md) and [MAIS-O44–O51](../../open-problems/README.md).
