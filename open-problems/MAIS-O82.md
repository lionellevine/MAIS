# Wide networks select the proxy policy with probability one

*Open problem MAIS-O82 · posed in [MAIS-A8](../agendas/A8/) as [Conjecture 5.2](../agendas/A8/MAIS-A8.tex#L280) · Status: open.*

*Safety: generalization — goal misgeneralization · proxy goals · simplicity bias. Mathematics: probability · optimization. Difficulty: ★★★ hard.*

An agent trained to collect a coin that always sat at the right end of its levels learned "move right," not "get the coin" — two rules that agree on every training level and disagree the moment the coin moves. Predicting *which* of two training-indistinguishable policies gradient descent selects is the mathematical core of goal misgeneralization.

The agenda builds a one-dimensional coin world with the degeneracy built in: states $(p,c)$ with agent position $p$ and coin position $c$ on a line of length $L$; the coin sits at the right end in all but an $\varepsilon$-fraction of training episodes; both "move right" (the proxy) and "go to the coin" (the intended goal) fit the training data perfectly. The probe state puts the coin at the far left, where the two policies disagree. For a two-layer network of width $m$ with Gaussian initialization of scale $\sigma$, trained by behavior cloning, let $q_\varepsilon(k;m,\sigma,L,\eta)$ be the probability over the initialization that after $k$ training steps the network follows the proxy at the probe ($\eta$ is a margin threshold). In the *linear* case the question is settled: the max-margin implicit-bias theorem proves the proxy wins at $\varepsilon=0$, and the answer flips with the input encoding. The first genuinely nonlinear case is the conjecture:

**Conjecture ([MAIS-A8, Conjecture 5.2](../agendas/A8/MAIS-A8.tex#L280)).** For every $\sigma>0$, $L\ge4$, and sufficiently small $\eta>0$,

$$\lim_{m\to\infty}\ \liminf_{k\to\infty}\ q_0(k;m,\sigma,L,\eta)\ =\ 1.$$

In words: at zero training diversity, an infinitely wide two-layer network provably walks away from the coin. Kernel-regime and mean-field analogues are proved in the agenda under their own normalizations, so the conjecture asks for the missing finite-parameterization case. For the environment's exact definition and the solved linear chapter, see [MAIS-A8](../agendas/A8/).

*Related: [MAIS-O8](MAIS-O8.md) (the selection map this conjecture would begin to compute) · [MAIS-O84](MAIS-O84.md) (how fast rare corrective examples overturn the proxy) · [MAIS-O87](MAIS-O87.md) (exploration starvation).*
