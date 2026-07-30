# Sparse and spurious: dictionary learning with noise and outliers

*Summary [GJB15] · R. Gribonval, R. Jenatton, and F. Bach, IEEE Transactions on Information Theory 61(11) (2015), 6298–6319 · [arXiv:1407.5155](https://arxiv.org/abs/1407.5155).*

*Tags: interpretability · sparse autoencoders · superposition · probability · optimization.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Sparse coding learns a dictionary by minimizing a non-convex $\ell^1$-penalized objective, and before this paper its minima had little theory behind them. Gribonval, Jenatton, and Bach prove that under a probabilistic sparse-signal model, with high probability, the empirical objective admits a local minimum within a controlled radius of the dictionary that generated the data — non-asymptotically, for overcomplete dictionaries, with noise and even a fraction of outliers. The guarantee is local: it places a good minimum near the truth without excluding better minima far away.

## Setup and hypotheses

Signals are generated as $y=\Phi x+\xi$: a dictionary $\Phi$ with unit-norm columns (overcomplete allowed, $m\ge n$), a sparse coefficient vector $x$ whose support is random and whose nonzero entries are sign-symmetric and bounded, and bounded noise $\xi$; a small proportion of samples may be arbitrary outliers. The learner minimizes the empirical $\ell^1$-penalized objective — average over samples of $\min_z\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$ — over dictionaries $\Psi$ with unit-norm columns. The hypotheses are coherence-type conditions on $\Phi$ relative to the sparsity level, plus bounds relating the penalty $\lambda$, the noise level, and the outlier energy.

## Main results

1. **Local minimum near the truth.** With high probability over the draw of polynomially many samples, the empirical objective has a local minimum within a ball of explicitly controlled radius around $\Phi$; the radius shrinks with the penalty and the noise, so the recovered dictionary converges to the generating one in the small-$\lambda$, small-noise limit.
2. **Robustness.** The guarantee tolerates noisy signals and outliers whose total energy is small relative to the inliers, extending prior work confined to noiseless or undercomplete settings.
3. **Non-asymptotic scaling.** The analysis makes explicit how coherence, sparsity, signal dimension, number of atoms, and sample size trade off against one another.

## Proof method

The population objective is shown to decrease in the direction of $\Phi$ on a sphere of appropriate radius around it: closed-form analysis of the penalized least-squares inner problem under the coherence and sparsity hypotheses controls the objective's behavior on that sphere, forcing a minimum inside the ball. Uniform concentration over the compact set of unit-norm dictionaries then transfers the statement from the population objective to the empirical one at a polynomial sample size, with outliers handled by budgeting their total contribution to the objective.

## Why it matters for AI safety

The paper analyzes a close mathematical analogue of the sparse-coding objective used by sparse autoencoders: an $\ell^1$-penalized reconstruction loss over a learned dictionary. It guarantees a good local minimum near the generating dictionary, but does not rule out a merged or rotated dictionary with lower loss far away. Global recovery, first for independent supports and then for correlated feature activations, is the subject of [MAIS-A3](../agendas/A3/).

## Cited by

- [MAIS-A3](../agendas/A3/) — takes the local guarantee as the state of the art to be surpassed: its central conjectures ask for global recovery for the same $\ell^1$-penalized estimator.
- Problems [MAIS-O3](../open-problems/MAIS-O3.md) · [MAIS-O36](../open-problems/MAIS-O36.md) · [MAIS-O46](../open-problems/MAIS-O46.md)
