# Dynamical versus Bayesian phase transitions in a toy model of superposition

*Summary [CLMWM23] · Z. Chen, E. Lau, J. Mendel, S. Wei, and D. Murfet, 2023 · [arXiv:2310.06301](https://arxiv.org/abs/2310.06301).*

*Tags: interpretability · superposition · training dynamics · optimization · probability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** In the toy model of superposition — a ReLU autoencoder squeezing $m$ sparse features through $n<m$ dimensions — the population loss admits a closed formula, and for $n=2$ the regular $k$-gon weight configurations are critical points. Singular learning theory then organizes these critical points by their local learning coefficients, predicting phase transitions in the Bayesian posterior as sample size grows; empirically, SGD training visits the same $k$-gons, in the same order, moving from high loss and low complexity toward low loss and high complexity.

## Setting

The model is the two-layer autoencoder of *Toy models of superposition* (Elhage et al. [[EHOS+22]](EHOS+22.md)): inputs $x\in\mathbb{R}^m$ with independent sparse coordinates, reconstruction $\mathrm{ReLU}(W^{\top}Wx+b)$ with $W\in\mathbb{R}^{n\times m}$, squared-error population loss. The columns of $W$ are the feature directions; the interesting regime is $n<m$, where the trained columns arrange themselves into polygons — the pentagon at $n=2$, $m=5$ is the emblem. The analytical tool is singular learning theory: because the loss landscape is degenerate, the effective complexity of a critical point is measured not by a parameter count but by its **local learning coefficient**, a geometric invariant governing the posterior volume near the point.

## Main results

1. **Closed-form loss.** A closed formula for the theoretical (population) loss of the toy model.
2. **$k$-gons are critical.** For $n=2$, the configurations whose columns form a regular $k$-gon (together with dropped features and small variants) are critical points of the loss, with the loss at each evaluated in closed form.
3. **Bayesian phase transitions.** Supporting theory that the local learning coefficients of the $k$-gons determine phase transitions in the Bayesian posterior as the number of training samples grows: the posterior concentrates first on simple high-loss critical points, then jumps to more complex low-loss ones.
4. **SGD follows the same script (empirical).** SGD trajectories pass through the same $k$-gon critical points, supporting the conjecture that SGD learning is a sequential journey from high-loss, low-complexity regions to low-loss, high-complexity regions.

The critical-point statements are theorems; the posterior-transition picture combines theory with estimation of the learning coefficients; the SGD claims are experimental.

## Method

The closed-form loss makes the $k$-gon ansatz checkable by direct computation: symmetry reduces criticality to a finite calculation, and the loss at each $k$-gon becomes an explicit expression comparable across $k$. On the Bayesian side, singular learning theory's free-energy asymptotics weigh a critical point's loss against its local learning coefficient, so that which $k$-gon dominates the posterior changes at computable sample-size thresholds; the coefficients are estimated numerically. SGD experiments then track the training trajectory past the same critical points.

## Why it matters for AI safety

Superposition is a central obstacle to reading a network's features off its weights, and this paper is the furthest the mathematics of the toy model has been pushed: it turns the empirical polygons of [[EHOS+22]](EHOS+22.md) into named critical points with exact losses. That rules the pentagon *in* as a candidate global minimizer — the missing global statement is [MAIS-O40](../open-problems/MAIS-O40.md) — and its phase-transition experiments are the closest prior study of which minimizer training actually selects, the question quantified in [MAIS-O50](../open-problems/MAIS-O50.md). The surrounding programs are [MAIS-A3](../agendas/A3/) (superposition geometry and sparse coding) and [MAIS-A4](../agendas/A4/) (quantitative interpretability).

## Cited by

- [MAIS-A3](../agendas/A3/) — the critical-point theory behind the pentagon conjecture: $k$-gons critical, loss in closed form.
- [MAIS-A4](../agendas/A4/) — toy-model structure ($k$-gon critical points, phase transitions) near its frontier and monosemanticity problems.
- Problems [MAIS-O40](../open-problems/MAIS-O40.md) · [MAIS-O42](../open-problems/MAIS-O42.md) · [MAIS-O50](../open-problems/MAIS-O50.md)
