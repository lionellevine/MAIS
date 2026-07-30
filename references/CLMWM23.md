# Dynamical versus Bayesian phase transitions in a toy model of superposition

*Summary [CLMWM23] · Z. Chen, E. Lau, J. Mendel, S. Wei, and D. Murfet, 2023 · [arXiv:2310.06301](https://arxiv.org/abs/2310.06301).*

*Tags: interpretability · superposition · training dynamics · optimization · probability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** In the high-sparsity limit of a ReLU autoencoder toy model, the population loss has a closed formula, and with two hidden dimensions many regular $k$-gon weight configurations are critical points. Singular learning theory organizes these points by their local learning coefficients and predicts changes in which region dominates the Bayesian posterior as sample size grows. In controlled experiments, SGD trajectories pass near the same critical points in an order of decreasing loss and increasing estimated complexity.

## Setting

The model is the two-layer autoencoder of *Toy models of superposition* (Elhage et al. [[EHOS+22]](EHOS+22.md)): reconstruction is $\mathrm{ReLU}(W^{\top}Wx+b)$ with $W\in\mathbb{R}^{n\times m}$, trained by squared population loss. The paper analyzes the **high-sparsity limit**, in which an input is supported on a single coordinate axis rather than having several independently active coordinates. The columns of $W$ are feature directions; when $n<m$, trained columns can arrange themselves into polygons, such as the pentagon for $n=2$, $m=5$. The **local learning coefficient** measures the posterior volume near a critical point and replaces parameter counting when the loss is singular.

## Main results

1. **Closed-form loss.** A closed formula for the population loss in the high-sparsity limit.
2. **$k$-gons are critical.** For $n=2$, the configurations whose columns form a regular $k$-gon (together with dropped features and small variants) are critical points of the loss, with the loss at each evaluated in closed form.
3. **Bayesian phase transitions.** Supporting theory that the local learning coefficients of the $k$-gons determine phase transitions in the Bayesian posterior as the number of training samples grows: the posterior concentrates first on simple high-loss critical points, then jumps to more complex low-loss ones.
4. **SGD follows the same script (empirical).** SGD trajectories pass through the same $k$-gon critical points, supporting the conjecture that SGD learning is a sequential journey from high-loss, low-complexity regions to low-loss, high-complexity regions.

The critical-point statements are theorems; the posterior-transition picture combines theory with estimation of the learning coefficients; the SGD claims are experimental.

## Method

The closed-form loss makes the $k$-gon ansatz checkable by direct computation: symmetry reduces criticality to a finite calculation, and the loss at each $k$-gon becomes an explicit expression comparable across $k$. On the Bayesian side, singular learning theory's free-energy asymptotics weigh a critical point's loss against its local learning coefficient, so that which $k$-gon dominates the posterior changes at computable sample-size thresholds; the coefficients are estimated numerically. SGD experiments then track the training trajectory past the same critical points.

## Why it matters for AI safety

Superposition makes individual neurons hard to interpret because several features share the same activation space. This paper supplies exact critical points and losses for a tractable limiting model, giving theorem-sized targets for the polygonal geometries observed in training. It does not prove that the pentagon is globally optimal, nor that general SGD selects a particular critical point; those are the questions pursued in [MAIS-A3](../agendas/A3/) and [MAIS-A4](../agendas/A4/).

## Cited by

- [MAIS-A3](../agendas/A3/) — the critical-point theory behind the pentagon conjecture: $k$-gons critical, loss in closed form.
- [MAIS-A4](../agendas/A4/) — toy-model structure ($k$-gon critical points, phase transitions) near its frontier and monosemanticity problems.
- Problems [MAIS-O40](../open-problems/MAIS-O40.md) · [MAIS-O42](../open-problems/MAIS-O42.md) · [MAIS-O50](../open-problems/MAIS-O50.md)
