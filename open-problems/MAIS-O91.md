# Numerical atlas of misgeneralization across widths and diversity

*Open problem MAIS-O91 · posed in [MAIS-A8](../agendas/A8/MAIS-A8.pdf) as [Problem 7.4](../agendas/A8/MAIS-A8.tex#L478) · Status: open.*

*Safety: generalization — goal misgeneralization · proxy goals · training dynamics · simplicity bias. Mathematics: computational · probability. Difficulty: ★ starter.*

Every open problem in the coin-line agenda asks for a number a laptop can estimate: the probability, over random initialization, that a trained policy walks away from a displaced coin. Nobody has computed the table.

The quantities, from the agenda: on a line of length $L$, with the coin at the right end in all but an $\varepsilon$-fraction of training episodes, $q_\varepsilon(k;m,\sigma,L,\eta)$ is the probability that a width-$m$ two-layer ReLU network with Gaussian initialization of scale $\sigma$, trained for $k$ steps of behavior cloning at step size $\eta$, prefers to step right at the probe state (agent mid-line, coin at the left end); $q^{\mathrm{RL}}_\varepsilon(k;m,\sigma,L,\eta)$ is the same probability for policy-gradient training on the return; and $Q(L)$ is the Gaussian-process posterior probability of the same verdict, conditioning the infinite-width prior on the training labels. Each is a Monte Carlo average over initializations; $Q(L)$ is a ratio of two orthant probabilities of an explicit Gaussian vector.

**Problem ([MAIS-A8, Problem 7.4](../agendas/A8/MAIS-A8.tex#L478)).** Compute, by simulation, the selection maps

$$q_\varepsilon(k;m,\sigma,L,\eta)\quad\text{and}\quad q^{\mathrm{RL}}_\varepsilon(k;m,\sigma,L,\eta)$$

over a grid of $(\varepsilon,m,\sigma,\eta)$ at $L\in\{4,8,16\}$, together with the Gaussian conditional probability $Q(L)$ of the Bayesian-sampler question. Publish the atlas either way.

The atlas would show where the conjectured proxy selection holds, where the crossover to the intended goal happens as $\varepsilon$ grows, whether cloning and reinforcement learning part ways at small $\varepsilon$, and whether the Gaussian posterior tracks training — data against which every conjecture in the agenda can be checked before anyone proves it. For the exact conventions (the deterministic backpropagation rule, the probe, the training distributions), see [MAIS-A8](../agendas/A8/MAIS-A8.pdf).

*Related: [MAIS-O8](MAIS-O8.md) (the selection map this atlas estimates) · [MAIS-O88](MAIS-O88.md) (the reinforcement-learning curve it would plot) · [MAIS-O86](MAIS-O86.md) (the Bayesian-sampler comparison supplying $Q(L)$).*
