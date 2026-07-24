# Does policy gradient stay misgeneralized despite training diversity?

*Open problem MAIS-O87 · posed in [MAIS-A8](../agendas/A8/) as [Question 6.2](../agendas/A8/MAIS-A8.tex#L443) · Status: open.*

*Safety: generalization — goal misgeneralization · proxy goals · training dynamics. Mathematics: dynamical systems · probability. Difficulty: ★★ project.*

Reinforcement learning changes the coin problem in one essential way: the training data become endogenous, since the states an agent experiences depend on the policy it currently has. A policy that has already committed to "move right" receives corrective signal from a left-lying coin only on episodes where it happens to random-walk left far enough to collect it, an event whose probability the proxy itself drives toward zero. Misgeneralization protects itself. Is the protection strong enough to last forever?

On the agenda's coin line, an agent at position $p$ seeks a coin at position $c$ on $\lbrace 0,\dots,L\rbrace $; the coin sits at the right end in all but an $\varepsilon$-fraction of episodes, and the return $J_\varepsilon(w)$ is the probability that an episode played by the policy collects the coin. The linear policy steps right with probability $\sigma(w\cdot x_{\mathrm a}(s))$, where $x_{\mathrm a}(p,c)=(1,p,c)$ and $\sigma$ is the logistic function; it trains by the smooth policy-gradient flow $\dot w=\nabla J_\varepsilon(w)$ from $w(0)\sim N(0,\sigma^2I_3)$. Write $q^{\mathrm{RL}}_\varepsilon(t;\sigma,L)$ for the probability, over the initialization, that at time $t$ the policy prefers to step right at the probe state $s^{\ast }=(\lceil L/2\rceil,0)$ — coin at the left end, where the proxy and the intended goal disagree.

**Question ([MAIS-A8, Question 6.2](../agendas/A8/MAIS-A8.tex#L443)).** Fix $L\ge4$ and $\sigma>0$. Are there $\bar\varepsilon>0$ and $\delta>0$ such that for every real $\varepsilon\in(0,\bar\varepsilon]$ the linear policy-gradient flow satisfies $\limsup_{t\to\infty}q^{\mathrm{RL}}_\varepsilon(t;\sigma,L)\ge\delta$? Behavior cloning has no such $\bar\varepsilon$: there, the misgeneralization probability tends to zero for every rational $\varepsilon>0$.

In cloning, the corrective signal at diversity $\varepsilon$ has size of order $\varepsilon$; in reinforcement learning it is $\varepsilon$ times a policy-dependent exploration factor, and the question asks whether that starvation leaves a positive fraction of initializations misgeneralized for all time, uniformly in small $\varepsilon$. At $\varepsilon=0$ the agenda proves the proxy wins from every initialization; this question is the first strictly positive diversity level. For the flow's definition and the exploration-starvation heuristic made precise, see [MAIS-A8](../agendas/A8/).

*Related: [MAIS-O88](MAIS-O88.md) (the trained-to-criterion misgeneralization curve) · [MAIS-O84](MAIS-O84.md) (the cloning crossover this contrasts with) · [MAIS-O8](MAIS-O8.md) (the headline selection problem).*
