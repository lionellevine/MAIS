# Neural networks provably learn spectral representations for group composition

*Summary [HWZCY26] · J. He, L. Wang, F. Zhang, S. Chen, and Z. Yang, preprint, 2026 · [arXiv:2606.02993](https://arxiv.org/abs/2606.02993).*

*Tags: interpretability · mechanistic interpretability · training dynamics · representation theory · dynamical systems · probability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** For a two-layer network trained on group composition, an idealized training dynamics — projected gradient flow on a small-logit Taylor surrogate of the cross-entropy — becomes, in the Fourier domain, Riemannian gradient ascent on a representation-theoretic energy functional. Under random initialization each neuron converges almost surely to a single irreducible representation of the group, and for abelian groups the population diversifies uniformly across the nontrivial representations, with Haar-uniform phases and exponential convergence rates. This is the nearest rigorous theorem to the neuron-level selection laws conjectured in [MAIS-A5](../agendas/A5/) — proved for the surrogate flow, not the exact ensemble.

## Setup and hypotheses

A two-layer neural network is trained to predict the product $g_1 \star g_2$ in a finite group $G$. The training dynamics analyzed is not gradient flow on the exact cross-entropy: the authors Taylor-expand the loss to a small-logit surrogate risk and run a *projected* gradient flow on it. Lifting this flow to the Fourier domain of $G$ reveals its structure — the dynamics is a Riemannian gradient ascent on an energy functional defined through the irreducible representations of $G$. Initialization is random. Exact and surrogate trajectories are compared only on fixed finite time intervals, with an error bound that grows in time, so the asymptotic theorems below are statements about the surrogate flow and do not transfer to the exact cross-entropy as $t \to \infty$.

## Main results

1. **Per-neuron alignment.** Under random initialization, the surrogate flow drives each neuron to converge almost surely toward a single irreducible representation of $G$, while the cross-layer Fourier coefficients achieve a rotational rank-one alignment — a low-rank compression phenomenon for matrix-valued representations. This holds for general finite $G$, including nonabelian groups.
2. **Abelian landing law.** For abelian $G$ (with no self-conjugate nontrivial character), a complete population-level description: random initialization promotes uniform diversification across the nontrivial representations and induces Haar-uniform phases, and the population jointly approximates the target indicator by a majority-vote mechanism.
3. **Rates.** Both the phase alignment and the competition among representations converge exponentially fast.

For nonabelian $G$ the alignment theorem holds but the landing proportions — what fraction of neurons ends up at each irreducible — are not determined.

## Method

The engine is the change of basis. In the Fourier domain the surrogate risk becomes an energy functional on representation coefficients, and the projected flow becomes a Riemannian gradient ascent on it; the asymptotic analysis (almost-sure single-representation convergence, diversification, phase distribution) is carried out for this flow. The link back to actual training is a finite-horizon comparison between surrogate and exact trajectories.

## Why it matters for AI safety

Circuit-level interpretability rests on the observed regularity that neurons in networks trained on algebraic tasks commit to single irreducible representations. This paper proves that commitment — and, in the abelian case, the resulting allocation of neurons — as a theorem, for an idealized dynamics. It thereby marks the exact frontier of the selection problem: purity and the landing law are established for the Taylor-surrogate projected flow, while the exact-loss ensemble at fixed initialization scale, the nonabelian landing proportions, and the rectifier and weight-decay regimes all remain open. Those gaps are the open problems of [MAIS-A5](../agendas/A5/).

## Cited by

- [MAIS-A5](../agendas/A5/) — the closest theorem to the agenda's selection laws: its neuron-purity and law-of-large-numbers conjectures ask for the exact-loss analogues of the alignment and diversification results proved here for the surrogate flow.
- Problems [MAIS-O5](../open-problems/MAIS-O5.md) · [MAIS-O53](../open-problems/MAIS-O53.md) · [MAIS-O54](../open-problems/MAIS-O54.md) · [MAIS-O55](../open-problems/MAIS-O55.md) · [MAIS-O59](../open-problems/MAIS-O59.md)
