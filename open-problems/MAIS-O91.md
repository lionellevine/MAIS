# Numerical atlas of misgeneralization across widths and diversity

*Open problem MAIS-O91 · posed in [MAIS-A8](../agendas/A8/) as [Problem 7.4](../agendas/A8/MAIS-A8.tex#L479) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · training dynamics · simplicity bias · computational · probability · empirical. Difficulty: ★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Every open problem in the coin-line agenda asks for a number a laptop can estimate: the probability, over random initialization, that a trained policy walks away from a displaced coin. Nobody has computed the table.

The setting, in brief, is the agenda's **coin line**: an agent on a line of length $L$ sees its own position and the coin's, and steps right with probability given by the logistic function of the output of a two-layer ReLU network of width $m$, Gaussian-initialized at scale $\sigma$. In training the coin sits at the right end in all but an $\varepsilon$-fraction of episodes, and the probe state (agent mid-line, coin at the left end) is where "move right" and "go to the coin" disagree — a one-dimensional miniature of the coin-collector experiments in which Langosco, Koch, Sharkey, Pfau, Orseau, and Krueger [[LKSP+22]](../references/LKSP+22.md) exhibited goal misgeneralization. Exact conventions (state encoding, backpropagation rule, training distributions) are in [MAIS-A8](../agendas/A8/).

Three numbers attach to this setting. The quantity $q_\varepsilon(k;m,\sigma,L,\eta)$ is the probability, over the initialization, that after $k$ steps of behavior cloning (logistic-loss fitting of the coin-seeking action, at step size $\eta$) the network output at the probe is positive: the policy prefers to walk away from the coin. The quantity $q^{\mathrm{RL}}_\varepsilon(k;m,\sigma,L,\eta)$ is the same probability when training instead ascends the expected return, the probability that an episode collects the coin. Because the policy is stochastic, the return is an explicit polynomial in the action probabilities (for a deterministic policy it would be piecewise constant, and the ascent undefined), and the agenda prescribes full-batch ascent on its exact gradient, so each initialization determines a unique trajectory. Each is a Monte Carlo average over initializations. Finally, $Q(L)$ is the probability of the same probe verdict under the network's infinite-width Gaussian-process prior conditioned on the zero-diversity training labels — a ratio of two orthant probabilities of an explicit Gaussian vector, and the coin line's exactly computable case of the posterior-versus-training comparison of Mingard, Valle-Pérez, Skalse, and Louis [[MVSL21]](../references/MVSL21.md) (the **Bayesian-sampler question**, [MAIS-O86](MAIS-O86.md)).

**Problem ([MAIS-A8, Problem 7.4](../agendas/A8/MAIS-A8.tex#L479)).** Compute, by simulation, the selection maps

$$q_\varepsilon(k;m,\sigma,L,\eta)\quad\text{and}\quad q^{\mathrm{RL}}_\varepsilon(k;m,\sigma,L,\eta)$$

over a grid of $(\varepsilon,m,\sigma,\eta)$ at $L\in\lbrace 4,8,16\rbrace $, together with the Gaussian conditional probability $Q(L)$ of the Bayesian-sampler question. Publish the atlas either way.

The atlas would show where the conjectured proxy selection holds, where the crossover to the intended goal happens as $\varepsilon$ grows, whether cloning and reinforcement learning part ways at small $\varepsilon$, and whether the Gaussian posterior tracks training — data against which every conjecture in the agenda can be checked before anyone proves it.

## References

- [[LKSP+22]](../references/LKSP+22.md) L. Langosco, J. Koch, L. Sharkey, J. Pfau, L. Orseau, and D. Krueger, *Goal misgeneralization in deep reinforcement learning*, ICML 2022 — the coin-collector experiments whose diversity curves (their §4.1) the atlas would miniaturize. [arXiv:2105.14111](https://arxiv.org/abs/2105.14111)
- [[MVSL21]](../references/MVSL21.md) C. Mingard, G. Valle-Pérez, J. Skalse, and A. Louis, *Is SGD a Bayesian sampler? Well, almost*, JMLR 22(79):1–64, 2021 — the posterior-versus-training comparison that $Q(L)$ makes exact. [arXiv:2006.15191](https://arxiv.org/abs/2006.15191)

*Related: [MAIS-O8](MAIS-O8.md) (the selection map this atlas estimates) · [MAIS-O88](MAIS-O88.md) (the reinforcement-learning curve it would plot) · [MAIS-O86](MAIS-O86.md) (the Bayesian-sampler comparison supplying $Q(L)$).*
