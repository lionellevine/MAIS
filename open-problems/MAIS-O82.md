# Wide networks select the proxy policy with probability one

*Open problem MAIS-O82 · posed in [MAIS-A8](../agendas/A8/) as [Conjecture 5.2](../agendas/A8/MAIS-A8.tex#L281) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · simplicity bias · probability · optimization. Difficulty: ★★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

An agent trained to collect a coin that always sat at the right end of its levels learned "move right," not "get the coin" — two rules that agree on every training level and disagree the moment the coin moves. Predicting *which* of two training-indistinguishable policies gradient descent selects is the mathematical core of goal misgeneralization.

The agenda builds a one-dimensional coin world with the degeneracy built in: states $(p,c)$ with agent position $p$ and coin position $c$ on a line of length $L$; the coin sits at the right end in all but an $\varepsilon$-fraction of training episodes, so at $\varepsilon=0$ both "move right" (the proxy) and "go to the coin" (the intended goal) fit the training data perfectly. A two-layer ReLU network of width $m$, both layers trained from Gaussian initialization of scale $\sigma$, learns by behavior cloning: gradient descent with fixed step size $\eta$ on the logistic loss of the coin-seeking action. The probe state puts the coin at the far left, where the two policies disagree, and $q_\varepsilon(k;m,\sigma,L,\eta)$ is the probability over the initialization that after $k$ training steps the network walks away from the coin. In the *linear* case the question is settled: the max-margin implicit-bias theorem of Soudry et al. [[SHNGS18]](../references/SHNGS18.md) proves the proxy wins at $\varepsilon=0$, and the verdict flips with the input encoding. The first genuinely nonlinear case is the conjecture:

**Conjecture ([MAIS-A8, Conjecture 5.2](../agendas/A8/MAIS-A8.tex#L281)).** For every $\sigma>0$, $L\ge4$, and sufficiently small $\eta>0$,

$$\lim_{m\to\infty}\ \liminf_{k\to\infty}\ q_0(k;m,\sigma,L,\eta)\ =\ 1.$$

In words: at zero training diversity, for any initialization scale and any sufficiently small step size, an infinitely wide two-layer network provably walks away from the coin. Kernel-regime and mean-field analogues are proved in the agenda (the mean-field one granted the weak convergence that the margin theory of Chizat and Bach [[CB20]](../references/CB20.md) assumes), but each rescales the network as the width grows, so neither formally implies the conjecture: here training runs at finite width in the standard parameterization, and the width limit comes only after the training limit. For the environment's exact definition and the solved linear chapter, see [MAIS-A8](../agendas/A8/).

## References

- [[SHNGS18]](../references/SHNGS18.md) D. Soudry, E. Hoffer, M. S. Nacson, S. Gunasekar, and N. Srebro, *The implicit bias of gradient descent on separable data*, JMLR 19(70):1–57, 2018. [arXiv:1710.10345](https://arxiv.org/abs/1710.10345)
- [[CB20]](../references/CB20.md) L. Chizat and F. Bach, *Implicit bias of gradient descent for wide two-layer neural networks trained with the logistic loss*, COLT 2020. [arXiv:2002.04486](https://arxiv.org/abs/2002.04486)

*Related: [MAIS-O8](MAIS-O8.md) (the selection map this conjecture would begin to compute) · [MAIS-O84](MAIS-O84.md) (how fast rare corrective examples overturn the proxy) · [MAIS-O87](MAIS-O87.md) (exploration starvation).*
