# A Basin-Selection Perspective on Grokking via Singular Learning Theory

*Summary [CEDL26] · B. Cullen, S. Estan-Ruiz, R. Danait, and J. Li, 2026 · [arXiv:2603.01192](https://arxiv.org/abs/2603.01192).*

*Tags: singular learning theory · grokking · developmental interpretability · generalization · interpretability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Under genericity and non-defectiveness hypotheses, the paper computes local learning coefficients for shallow quadratic networks, including modular addition. Below the secant-saturation threshold, each active hidden unit contributes $(3p-1)/2$; above it, the coefficient saturates. These coefficients rank equal-loss regions for Bayesian learning. Their proposed connection to the fixed-data timing of grokking is empirical rather than a consequence of singular learning theory.

## Setting

The network is a two-layer quadratic model for addition mod a prime $p$: the one-hot pair of residues is a vector $x \in \mathbb{R}^{2p}$, and the output is $V\sigma(W^{\top}x)$ with $\sigma(t)=t^2$, $W\in\mathbb{R}^{2p\times K}$, and $V\in\mathbb{R}^{p\times K}$. The loss is squared error against the one-hot answer. The **local learning coefficient** $\lambda(w)$ is a volume-growth exponent for low-loss parameters near $w$. In Bayesian asymptotics, among regions with comparable loss, a smaller coefficient gives a smaller complexity penalty. This statement concerns increasing sample size, not the time evolution of SGD on a fixed dataset.

## Main results

1. **Below saturation.** Write $d=2p$ and $D=d(d+1)/2$. At a generic smooth zero-loss point with nonzero atoms and a non-defective secant variety, if $K(d+p-1)<pD$, then
   $$\lambda=\frac{K(d+p-1)}2=\frac{K(3p-1)}2.$$
2. **At and above saturation.** Under the corresponding full-span hypothesis, if $K(d+p-1)\ge pD$, then $\lambda=pD/2=p^2(2p+1)/2$. Extra width does not increase this generic coefficient.
3. **Optimization regimes.** Companion formulas give reference coefficients for linearized, lazy-feature, memorizing, and feature-learning regimes. The paper interprets grokking through competition between such regions, while explicitly separating Bayesian preference from the unproved dynamical question of when SGD moves between them.
4. **Empirics.** Coefficient trajectories estimated from training data track the onset of generalization, and their final values scale linearly in both $p$ and $K$.

## Method

Not a full resolution of singularities: the coefficients come from a rank analysis of the Jacobian of the parametrization sending $(W,V)$ to the model's quadratic forms, identifying which perturbations move the output at the optimum, and converting that local geometry into sublevel-set volume asymptotics in Watanabe's framework. The non-degeneracy hypotheses are what keep the Jacobian's rank generic.

## Why it matters for AI safety

Local learning coefficients can distinguish equal-loss parameter regions that implement different mechanisms, at least for Bayesian learning. This paper gives a generic benchmark for modular addition, while the Fourier solutions, dead units, and coincident units of special interest to interpretability lie on nongeneric strata where its formula need not apply. Computing those strata and testing whether the coefficients predict SGD's choices are the subjects of [MAIS-A6](../agendas/A6/).

## Cited by

- [MAIS-A6](../agendas/A6/) — uses the closed-form non-degenerate coefficients as the benchmark that its bounds at singular points beat.
- Problems [MAIS-O63](../open-problems/MAIS-O63.md) · [MAIS-O64](../open-problems/MAIS-O64.md)
