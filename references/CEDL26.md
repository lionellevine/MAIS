# A Basin-Selection Perspective on Grokking via Singular Learning Theory

*Summary [CEDL26] · B. Cullen, S. Estan-Ruiz, R. Danait, and J. Li, 2026 · [arXiv:2603.01192](https://arxiv.org/abs/2603.01192).*

*Tags: singular learning theory · grokking · developmental interpretability · generalization · interpretability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Closed-form local learning coefficients for shallow quadratic networks on modular addition, in both the over- and under-parametrized regimes, under explicit non-degeneracy hypotheses; in the under-parametrized regime each active unit charges $(3p-1)/2$. On this foundation the paper reads grokking as basin selection: competing near-zero-loss basins are ranked by their local learning coefficients, and the delayed jump to generalization is a passage from a higher-coefficient memorizing basin to a lower-coefficient generalizing one. Empirically, the coefficient estimated from training data alone drops at the onset of generalization.

## Setting

The network is a two-layer quadratic model for addition mod a prime $p$: the one-hot pair of residues is a vector $x \in \mathbb{R}^{2p}$, and the output is $V\sigma(W^{\top}x)$ with $\sigma(t) = t^2$ applied entrywise, where $W \in \mathbb{R}^{2p \times K}$ and $V \in \mathbb{R}^{p \times K}$ for hidden width $K$; the loss is squared error against the one-hot answer. The quantity computed is the **local learning coefficient** $\lambda(w)$, the volume-growth exponent of the loss sublevel sets near a parameter $w$ — in Watanabe's singular learning theory, the basin with the smallest coefficient is where the Bayesian posterior concentrates, and smaller coefficients mean lower expected generalization error.

## Main results

1. **Under-parametrized regime** (width below the span threshold $d(d+1)/2$ with $d = 2p$): at a zero-loss parameter where every unit is active, the units' rank-one matrices are linearly independent, and a genericity condition on tangent directions holds, the coefficient is exactly $\lambda = K(3p-1)/2$ — a charge of $(3p-1)/2$ per active unit, below the $3p/2$ that parameter counting would assess.
2. **Over-parametrized regime** (width at or above the threshold, with a corresponding span condition): $\lambda = p \cdot d(d+1)/4$, which for modular addition is $p^2(2p+1)/2$ — the coefficient saturates and further width is free.
3. **Basin-selection account of grokking.** Companion formulas cover the lazy (memorizing) regime and the feature-learning regime, the latter charging by an effective width that counts active units; grokking is the transition from the memorizing basin to the generalizing basin that dominates the posterior.
4. **Empirics.** Coefficient trajectories estimated from training data track the onset of generalization, and their final values scale linearly in both $p$ and $K$.

## Method

Not a full resolution of singularities: the coefficients come from a rank analysis of the Jacobian of the parametrization sending $(W,V)$ to the model's quadratic forms, identifying which perturbations move the output at the optimum, and converting that local geometry into sublevel-set volume asymptotics in Watanabe's framework. The non-degeneracy hypotheses are what keep the Jacobian's rank generic.

## Why it matters for AI safety

If local learning coefficients can be computed for a task whose learned mechanism is known, they predict which algorithm Bayesian learning prefers — an interpretability tool that runs before training rather than after. This paper is the closest existing computation for modular addition, and the hypotheses that make its formulas exact are precisely what the open questions relax: the non-degenerate value $(2p-1)(3p-1)/2$ at width $2p-1$ is beaten by the bound $3p^2-3p+1$ at the Fourier point, where the hypotheses fail, and they fail again at the dead-unit and coinciding-unit strata that the posterior may prefer. So [CEDL26] settles the generic stratum, and the singular strata below it — the Fourier fits and the price of an idle unit — are the subject of [MAIS-A6](../agendas/A6/).

## Cited by

- [MAIS-A6](../agendas/A6/) — uses the closed-form non-degenerate coefficients as the benchmark that its bounds at singular points beat.
- Problems [MAIS-O63](../open-problems/MAIS-O63.md) · [MAIS-O64](../open-problems/MAIS-O64.md)
