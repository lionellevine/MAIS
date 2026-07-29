# Misgeneralization versus diversity for reinforcement learning

*Open problem MAIS-O88 · posed in [MAIS-A8](../agendas/A8/) as [Problem 6.3](../agendas/A8/MAIS-A8.tex#L448) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · training dynamics · probability · dynamical systems. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Langosco et al. plotted how often their trained coin collector ignores a displaced coin against the percentage of training levels with a randomized coin, and found the failure rate falls steeply: about 2% diversity largely restores the intended behavior. The coin line is small enough to ask for that curve as a theorem.

The setting, from the agenda's coin line: an agent at position $p$ and a coin at position $c$, both on $\lbrace 0,\dots,L\rbrace $ with $L\ge4$, both visible to the agent. Each step the agent moves one cell left or right, clamped at the endpoints; the coin does not move. An episode starts with $p$ uniform on $\lbrace 0,\dots,L\rbrace $ and the coin drawn independently from $\mu_\varepsilon=(1-\varepsilon)\,\delta_L+\varepsilon\,\mathrm{Unif}\lbrace 1,\dots,L\rbrace $ — at the right end in all but an $\varepsilon$-fraction of episodes, and never at $0$ — and ends with reward $1$ the first time $p=c$, or reward $0$ if that has not happened within $2L$ steps. The return $J_\varepsilon(\theta)$ is the probability that an episode played by the policy collects the coin. The policy steps right with probability $\sigma(f_\theta(x_{\mathrm a}(s)))$, where $\sigma(z)=1/(1+e^{-z})$, $x_{\mathrm a}(p,c)=(1,p,c)$, and $f_\theta$ is a two-layer ReLU network of width $m$ whose weights are initialized as independent Gaussians of scale $\sigma$ (the agenda reuses the letter; the $\sigma$ in the problem's parameter list is this initialization scale). Training is ascent on the exact return with fixed step $\eta$: $\theta_{k+1}=\theta_k+\eta\,\nabla J_\varepsilon(\theta_k)$, the gradient computed by backpropagation with the ReLU derivative taken as $1$ at positive preactivations and $0$ otherwise, so the update is single-valued and the initialization fixes the trajectory $\theta_k$. The probe state $s^{\ast }=(\lceil L/2\rceil,0)$ puts the agent mid-line and the coin at the left end (a state outside the training support for every $\varepsilon$), where "move right" and "go to the coin" disagree; a positive logit there is the misgeneralized verdict. Experiments train to a performance criterion rather than forever, so the problem reads the probe at the first time the return is nearly perfect.

**Problem ([MAIS-A8, Problem 6.3](../agendas/A8/MAIS-A8.tex#L448)).** For the two-layer policy and each $\delta\in(0,\tfrac12)$, let $\tau_\delta=\inf\lbrace k:J_\varepsilon(\theta_k)\ge1-\delta\rbrace $, with $\tau_\delta=\infty$ if the set is empty. Determine

$$\varepsilon\ \longmapsto\ \mathbb P\bigl(\tau_\delta<\infty,\ \ f_{\theta_{\tau_\delta}}(x_{\mathrm a}(s^{\ast }))>0\bigr)$$

as a function of $(\varepsilon,m,\sigma,L,\delta,\eta)$, together with $\Pr(\tau_\delta<\infty)$, and compare their shapes with the empirical diversity curves of Langosco et al.

In words: over the random initialization, what is the probability that training reaches return at least $1-\delta$ in finite time and the first policy to do so still walks away from the displaced coin? That function of $\varepsilon$ is the toy model's misgeneralization curve, and matching its shape to the experiments is the test of the theory. For the environment, the training rule, and the neighboring linear results, see [MAIS-A8](../agendas/A8/).

## References

- L. Langosco, J. Koch, L. Sharkey, J. Pfau, L. Orseau, and D. Krueger, *Goal misgeneralization in deep reinforcement learning*, ICML 2022 — the empirical diversity curves (their §4.1) this problem asks the theory to match. [arXiv:2105.14111](https://arxiv.org/abs/2105.14111)
- J. Mei, C. Xiao, C. Szepesvári, and D. Schuurmans, *On the global convergence rates of softmax policy gradient methods*, ICML 2020 — the convergence theory nearest to this training rule; it does not contain the coin line. [arXiv:2005.06392](https://arxiv.org/abs/2005.06392)
- N. Razin, H. Zhou, O. Saremi, V. Thilak, A. Bradley, P. Nakkiran, J. Susskind, and E. Littwin, *Vanishing gradients in reinforcement finetuning of language models*, ICLR 2024 — the vanishing-signal mechanism, proved in a neighboring setting. [arXiv:2310.20703](https://arxiv.org/abs/2310.20703)

*Related: [MAIS-O87](MAIS-O87.md) (exploration starvation, the mechanism shaping this curve) · [MAIS-O91](MAIS-O91.md) (the simulation atlas that would plot it) · [MAIS-O8](MAIS-O8.md) (the behavior-cloning selection map).*
