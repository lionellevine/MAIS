# The local learning coefficient: a singularity-aware complexity measure

*Summary [LFWMW23] · E. Lau, Z. Furman, G. Wang, D. Murfet, and S. Wei, 2023 · [arXiv:2308.12108](https://arxiv.org/abs/2308.12108).*

*Tags: singular learning theory · developmental interpretability · generalization · algebraic geometry · statistics.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Deep networks are singular statistical models, so Hessian rank can miss much of their local degeneracy. The paper develops the **local learning coefficient**, a Bayesian complexity measure for a neighborhood of one parameter, and an SGLD-based estimator for it. The estimator is calibrated against exact coefficients in deep linear networks with up to 100 million parameters and used comparatively on ResNet and transformer models; its practical values remain sensitive to localization and sampling choices.

## Setup and hypotheses

Fix a compact parameter space $W\subset\mathbb R^d$ and a model–truth–prior triplet $(p(x,y\mid w),\,q(x,y),\,\varphi(w))$ satisfying the fundamental conditions of singular learning theory together with Watanabe's *relative finite variance* condition; realizability is not assumed. A model is *regular* if the parameter-to-distribution map is injective with everywhere positive-definite Fisher information, and *singular* otherwise. Let $K(w)$ be the Kullback–Leibler divergence from the truth, $K_0=\inf_W K$, and $W_0=\{w: K(w)=K_0\}$ the optimal set — an analytic variety, generically positive-dimensional. The (global) learning coefficient $\lambda$ and multiplicity $m$ are defined through the zeta function $\zeta(z)=\int_W (K(w)-K_0)^z\varphi(w)\,dw$: its largest pole is $-\lambda$, of order $m$. Geometrically, a Hironaka resolution of singularities monomializes $K-K_0$ chart by chart, and $\lambda$ is the smallest ratio $(h_j+1)/2k_j$ of Jacobian-vanishing to loss-vanishing exponents over all charts; the local coefficient $\lambda(w^*)$ restricts to the charts sitting over $w^*$. A companion invariant, the singular fluctuation $\nu$, is defined via the functional variance of a tempered posterior.

## Main results

1. **Singular free-energy asymptotic** (Watanabe's theorem, recalled as the frame). The free energy satisfies $F_n = nL_n(w_0)+\lambda\log n-(m-1)\log\log n+O_P(1)$; for regular models $\lambda=d/2$ and $m=1$, recovering the Laplace approximation and the BIC. So $\lambda$ plays the role of $d/2$ as a complexity penalty, and $\lambda\ll d/2$ is possible.
2. **Local free energy.** Under the hypotheses that $w^*$ is a local minimizer of the population loss, is maximally degenerate among nearby minimizers at the same loss, and that the localized triplet satisfies relative finite variance (assumed, not verified), the free energy of a small ball obeys the same expansion with the local invariants: $F_n(B_\gamma(w^*))=nL_n(w^*)+\lambda(w^*)\log n-(m(w^*)-1)\log\log n+O_P(1)$. Posterior concentration is thus an energy–entropy competition between $nL_n(w^*)$ and $\lambda(w^*)\log n$: a lower local coefficient favors a region only at equal loss.
3. **The LLC estimator.** Localizing with a Gaussian prior of strength $\gamma$ centered at $w^*$ and applying a local version of Watanabe's WBIC at the single inverse temperature $\beta^*=1/\log n$ gives $\hat\lambda(w^*)=\bigl(\mathbb E^{\beta^*}[\,nL_n(w)\,]-nL_n(\hat w_n^*)\bigr)/\log n$, computable by stochastic-gradient Langevin sampling.
4. **Experiments.** The estimator tracks exact learning coefficients in deep linear networks up to 100 million parameters. On ResNet18 trained on CIFAR-10, stronger implicit or explicit regularization is associated with lower estimated coefficients and higher test accuracy; a two-layer attention-only language model provides a transformer-scale demonstration. Additional appendices include monomial calibration examples and a 1.9-million-parameter MNIST comparison of SGD with entropy-SGD.

The estimator is honest about its limits: it is ordinal and biased, sensitive to the localization strength and temperature, with known failure modes (runaway loss, negative estimates, over-tight priors).

## Proof method

Resolution of singularities and zeta-function poles define the invariants; Laplace and Morse–Bott approximations bridge the regular and minimally singular cases; the WBIC identity turns the free-energy slope at $\beta^*=1/\log n$ into an estimator requiring one posterior run, and SGLD makes that run scalable. An appendix ties $\lambda$ and $\nu$ to the Bayes and Gibbs generalization errors at order $1/n$.

## Why it matters for AI safety

Two networks can fit the same data by different internal mechanisms and behave differently off distribution. The local learning coefficient offers a way to compare the Bayesian complexity of neighborhoods containing those mechanisms, and the estimator makes that comparison possible at neural-network scale. Its role in selection is rigorous for Bayesian learning; using it to explain SGD or to identify a mechanism is a hypothesis that needs separate validation. Exact calibration cases are the subject of [MAIS-A6](../agendas/A6/), while [MAIS-A7](../agendas/A7/) studies the proposed connection to training dynamics.

## Cited by

- [MAIS-A6](../agendas/A6/) — takes the local coefficient's definition and estimator as its starting point; its calibration problems idealize the estimator and seek exact coefficients (modular addition) as ground truth for it.
- [MAIS-A7](../agendas/A7/) — uses the local coefficient and the localized free-energy expansion to stratify optimal sets, and the estimator as the numerical check on its opposing-staircases conjecture.
- Problems [MAIS-O7](../open-problems/MAIS-O7.md) · [MAIS-O64](../open-problems/MAIS-O64.md) · [MAIS-O66](../open-problems/MAIS-O66.md) · [MAIS-O69](../open-problems/MAIS-O69.md) · [MAIS-O70](../open-problems/MAIS-O70.md) · [MAIS-O77](../open-problems/MAIS-O77.md) · [MAIS-O81](../open-problems/MAIS-O81.md)
