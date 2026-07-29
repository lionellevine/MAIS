# Numerical atlas of misgeneralization across widths and diversity

*Open problem MAIS-O91 · posed in [MAIS-A8](../agendas/A8/) as [Problem 7.4](../agendas/A8/MAIS-A8.tex#L479) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · training dynamics · simplicity bias · computational · probability · empirical. Difficulty: ★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Every open problem in the coin-line agenda asks for a number a laptop can estimate: the probability, over random initialization, that a trained policy walks away from a displaced coin. Nobody has computed the table.

The setting, from the agenda, is the **coin line**: states $(p,c)$ with agent position $p$ and coin position $c$ in $\lbrace 0,\dots,L\rbrace $, actions $\pm1$ (step left, step right), encoded as $x_{\mathrm a}(p,c)=(1,p,c)$. In training, $p$ is uniform on $\lbrace 0,\dots,L\rbrace $ and, independently, the coin sits at the right end $c=L$ with probability $1-\varepsilon$ and uniform on $\lbrace 1,\dots,L\rbrace $ with probability $\varepsilon$ — never at the left end. The policy is the two-layer ReLU network $f_\theta(x)=\sum_{j=1}^m a_j\varphi(u_j\cdot x)$, $\varphi(z)=\max(z,0)$, of width $m$, initialized with independent $a_j\sim N(0,\sigma^2)$, $u_j\sim N(0,\sigma^2 I_3)$; positive output means "step right." Training is full-batch gradient descent (ascent, for reinforcement learning) with fixed step size $\eta$ and the convention $\varphi'(0)=0$, so each initialization determines a unique trajectory. The probe state $s^{\ast }=(\lceil L/2\rceil,0)$ — agent mid-line, coin at the left end — is where "move right" and "go to the coin" disagree.

Then $q_\varepsilon(k;m,\sigma,L,\eta)$ is the probability, over the initialization, that after $k$ steps of behavior cloning — logistic-loss fitting of the coin-seeking label $\operatorname{sign}(c-p)$ on training states with $p\ne c$ — the network prefers to step right at the probe: $f_{\theta_k}(x_{\mathrm a}(s^{\ast }))>0$. The quantity $q^{\mathrm{RL}}_\varepsilon(k;m,\sigma,L,\eta)$ is the same probability when training instead ascends the return, the probability that an episode of horizon $2L$ (reward $1$ on reaching the coin, $0$ otherwise) collects it. Each is a Monte Carlo average over initializations. Finally, for a Gaussian process $g$ with the network's infinite-width covariance $K(x,x')=\mathbb E_{u\sim N(0,I_3)}[\varphi(u\cdot x)\ \varphi(u\cdot x')]$, $Q(L)$ is the probability that $g>0$ at the probe given $g>0$ at the $\varepsilon=0$ training inputs $(1,p,L)$, $0\le p\le L-1$ — a ratio of two orthant probabilities of an explicit Gaussian vector. The **Bayesian-sampler question** ([MAIS-O86](MAIS-O86.md)), after the posterior-versus-training comparison of Mingard, Valle-Pérez, Skalse, and Louis [[MVSL21]](https://arxiv.org/abs/2006.15191), asks whether trained networks deliver the proxy verdict with exactly this posterior probability.

**Problem ([MAIS-A8, Problem 7.4](../agendas/A8/MAIS-A8.tex#L479)).** Compute, by simulation, the selection maps

$$q_\varepsilon(k;m,\sigma,L,\eta)\quad\text{and}\quad q^{\mathrm{RL}}_\varepsilon(k;m,\sigma,L,\eta)$$

over a grid of $(\varepsilon,m,\sigma,\eta)$ at $L\in\lbrace 4,8,16\rbrace $, together with the Gaussian conditional probability $Q(L)$ of the Bayesian-sampler question. Publish the atlas either way.

The atlas would show where the conjectured proxy selection holds, where the crossover to the intended goal happens as $\varepsilon$ grows, whether cloning and reinforcement learning part ways at small $\varepsilon$, and whether the Gaussian posterior tracks training — data against which every conjecture in the agenda can be checked before anyone proves it. The conventions above are the agenda's; for the conjectures themselves, see [MAIS-A8](../agendas/A8/).

## References

- [LKSP+22] L. Langosco, J. Koch, L. Sharkey, J. Pfau, L. Orseau, and D. Krueger, *Goal misgeneralization in deep reinforcement learning*, ICML 2022 — the coin-collector experiments whose diversity curves (their §4.1) the atlas would miniaturize. [arXiv:2105.14111](https://arxiv.org/abs/2105.14111)
- [SHNGS18] D. Soudry, E. Hoffer, M. S. Nacson, S. Gunasekar, and N. Srebro, *The implicit bias of gradient descent on separable data*, JMLR 19(70):1–57, 2018 — the max-margin theorem behind the linear predictions the atlas would check at finite width. [arXiv:1710.10345](https://arxiv.org/abs/1710.10345)
- [MVSL21] C. Mingard, G. Valle-Pérez, J. Skalse, and A. Louis, *Is SGD a Bayesian sampler? Well, almost*, JMLR 22(79):1–64, 2021 — the posterior-versus-training comparison that $Q(L)$ makes exact. [arXiv:2006.15191](https://arxiv.org/abs/2006.15191)

*Related: [MAIS-O8](MAIS-O8.md) (the selection map this atlas estimates) · [MAIS-O88](MAIS-O88.md) (the reinforcement-learning curve it would plot) · [MAIS-O86](MAIS-O86.md) (the Bayesian-sampler comparison supplying $Q(L)$).*
