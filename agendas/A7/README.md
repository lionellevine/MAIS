# Effective loss and learning dynamics

**Claude Fable 5**, audited by **GPT 5.6 Sol** · Draft, July 2026 · MAIS-A7

**[Full text (PDF)](MAIS-A7.pdf)** · [TeX source](MAIS-A7.tex) · [Provenance](PROVENANCE.md) · expands [MAIS-O7](../../open-problems/MAIS-O7.md)

## Abstract

For a singular statistical model, Watanabe's free-energy asymptotics predict which solutions Bayesian learning prefers: the posterior concentrates on the parts of the optimal set with the smallest learning coefficient. Gradient descent is not Bayesian, yet in solvable cases it exhibits a superficially similar stagewise progression, unfolding in training time rather than in sample size. This research agenda develops several routes toward a bridge: the structure of the stratification of the optimal set by local learning coefficient; an Eyring–Kramers law whose subexponential prefactor is governed by real log canonical thresholds; a coarse-grained *effective loss* at which a degenerate saddle can register as a local minimum; entropic selection within a connected optimal set, with a two-variable trigonometric polynomial as the first test case; the extension of the Katzenberger–Li–Wang–Arora effective diffusion from smooth manifolds of minimizers to singular ones, with matrix factorization as the concrete instance; and a time–sample dictionary calibrated on the deep linear network, where a heuristic computation gives training time $t \asymp \sqrt{n/\log n}$ against sample size $n$. It also isolates two obstructions: the free energy of a saddle is not an invariant of the naive kind, and the learning coefficient alone cannot set the clock of the dynamics.

---

Problems posed here are registered as [MAIS-O7](../../open-problems/MAIS-O7.md) and [MAIS-O72–O81](../../open-problems/README.md).
