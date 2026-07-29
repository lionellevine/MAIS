# Is SGD a Bayesian sampler? Well, almost

*Summary [MVSL21] · C. Mingard, G. Valle-Pérez, J. Skalse, and A. Louis, JMLR 22(79):1–64, 2021 · [arXiv:2006.15191](https://arxiv.org/abs/2006.15191).*

*Tags: generalization · training dynamics · simplicity bias · probability · empirical.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** For a range of architectures and datasets, the probability that a network trained by SGD lands on a given function $f$ consistent with the training set correlates remarkably well with the Bayesian posterior probability of $f$ under random sampling of the parameters — estimated via the network's Gaussian-process limit — and that posterior is strongly biased toward low-error, low-complexity functions. The conclusion is empirical, not a theorem: the inductive bias behind generalization lives chiefly in the parameter-function map, with SGD contributing only second-order, hyperparameter-sensitive corrections.

## Setting

An overparameterized network can fit a training set $S$ with zero error in a vast number of ways, almost all of which generalize badly; that trained networks nonetheless generalize suggests a strong inductive bias toward the good ones. The paper asks where that bias resides. Two function distributions are compared: $P_{\mathrm{SGD}}(f\mid S)$, the probability that a network trained with SGD (or a variant) converges to $f$ among the functions consistent with $S$, and $P_{\mathrm B}(f\mid S)$, the Bayesian posterior probability of $f$ when the parameters are sampled at random conditioned on fitting $S$, estimated using the Gaussian process corresponding to the architecture.

## Main results

1. **First-order agreement.** Across the architectures and datasets tested, $P_{\mathrm{SGD}}(f\mid S)$ correlates closely with $P_{\mathrm B}(f\mid S)$: to first order, SGD samples functions in proportion to their posterior probability under the random-parameter prior.
2. **Simplicity bias of the prior.** The posterior $P_{\mathrm B}(f\mid S)$ is itself strongly biased toward low-error and low-complexity functions, so the agreement in (1) transfers this simplicity bias to trained networks.
3. **Second-order deviations.** The match is not exact — hence "well, almost." Residual differences between the two distributions are sensitive to batch size, learning rate, and optimiser choice, and the function-probability picture organizes how such hyperparameters shift performance.

Together these support the thesis of the companion work [[VCL19]](https://arxiv.org/abs/1805.08522): deep learning generalizes primarily because the parameter-function map is biased toward simple functions, not because of a special property of SGD.

## Method

Direct estimation of both distributions on tasks small enough that individual functions recur. Networks are trained repeatedly from independent initializations to build an empirical histogram of $P_{\mathrm{SGD}}(f\mid S)$; the Bayesian side $P_{\mathrm B}(f\mid S)$ is computed from the architecture's Gaussian-process limit, conditioning on the training labels. The two histograms are then compared function by function across architectures, datasets, and optimiser variants.

## Why it matters for AI safety

Whether a trained agent's off-distribution behavior is predicted by the optimizer's dynamics or by the random-parameter posterior is precisely the question a theory of goal misgeneralization must settle, and this paper is the empirical case for the posterior. [MAIS-A8](../agendas/A8/) puts the two theories in a box where they can be forced to disagree about a single number: on the coin line, the Gaussian-process posterior probability of the proxy verdict at the probe is strictly less than one, while the agenda's kernel-flow analysis (its Proposition 5.3) drives the probe logit to $+\infty$, suggesting the value one. Question 5.10 asks which prediction the finite-width limit of full-batch gradient descent actually matches — a marginal on which the Mingard–Valle-Pérez–Skalse–Louis picture is exactly testable; see [MAIS-A8](../agendas/A8/).

## Cited by

- [MAIS-A8](../agendas/A8/) — the SGD-as-Bayesian-sampler thesis is one of the two candidate theories its Question 5.10 pits against each other on the coin line.
- Problems [MAIS-O86](../open-problems/MAIS-O86.md) · [MAIS-O91](../open-problems/MAIS-O91.md)
