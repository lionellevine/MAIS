# Misgeneralization versus diversity for reinforcement learning

*Open problem MAIS-O88 · posed in [MAIS-A8](../agendas/A8/) as [Problem 6.3](../agendas/A8/MAIS-A8.tex#L447) · Status: open.*

*Safety: generalization — goal misgeneralization · proxy goals · training dynamics. Mathematics: probability · dynamical systems. Difficulty: ★★★ hard.*

Langosco et al. plotted how often their trained coin collector ignores a displaced coin against the percentage of training levels with a randomized coin, and found the failure rate falls steeply: about 2% diversity largely restores the intended behavior. The coin line is small enough to ask for that curve as a theorem.

The setting, from the agenda: an agent at position $p$ and a coin at position $c$ on $\lbrace 0,\dots,L\rbrace $; the coin sits at the right end in all but an $\varepsilon$-fraction of episodes; the return $J_\varepsilon(\theta)$ is the probability that an episode played by the policy collects the coin. The policy steps right with probability $\sigma(f_\theta(x_{\mathrm a}(s)))$, where $\sigma(z)=1/(1+e^{-z})$, $x_{\mathrm a}(p,c)=(1,p,c)$, and $f_\theta$ is a two-layer ReLU network of width $m$ with Gaussian initialization of scale $\sigma$, trained by policy-gradient ascent with fixed step $\eta$ (the agenda's deterministic backpropagation rule, so the initialization fixes the trajectory $\theta_k$). The probe state $s^{\ast }=(\lceil L/2\rceil,0)$ puts the coin at the left end, where "move right" and "go to the coin" disagree; a positive logit there is the misgeneralized verdict. Experiments train to a performance criterion rather than forever, so the problem reads the probe at the first time the return is nearly perfect.

**Problem ([MAIS-A8, Problem 6.3](../agendas/A8/MAIS-A8.tex#L447)).** For the two-layer policy and each $\delta\in(0,\tfrac12)$, let $\tau_\delta=\inf\lbrace k:J_\varepsilon(\theta_k)\ge1-\delta\rbrace $, with $\tau_\delta=\infty$ if the set is empty. Determine

$$\varepsilon\ \longmapsto\ \mathbb P\bigl(\tau_\delta<\infty,\ \ f_{\theta_{\tau_\delta}}(x_{\mathrm a}(s^{\ast }))>0\bigr)$$

as a function of $(\varepsilon,m,\sigma,L,\delta,\eta)$, together with $\Pr(\tau_\delta<\infty)$, and compare their shapes with the empirical diversity curves of Langosco et al.

In words: over the random initialization, what is the probability that training reaches return at least $1-\delta$ in finite time and the first policy to do so still walks away from the displaced coin? That function of $\varepsilon$ is the toy model's misgeneralization curve, and matching its shape to the experiments is the test of the theory. For the environment, the training rule, and the neighboring linear results, see [MAIS-A8](../agendas/A8/).

*Related: [MAIS-O87](MAIS-O87.md) (exploration starvation, the mechanism shaping this curve) · [MAIS-O91](MAIS-O91.md) (the simulation atlas that would plot it) · [MAIS-O8](MAIS-O8.md) (the behavior-cloning selection map).*
