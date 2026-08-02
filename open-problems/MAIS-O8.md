# A predictive theory of out-of-distribution generalization

*Open problem MAIS-O8 · headline problem 8 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A8](../agendas/A8/) as [Problem 5.1](../agendas/A8/MAIS-A8.tex#L268) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · simplicity bias · training dynamics · probability · optimization · dynamical systems. Difficulty: ★★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

In 2022, Langosco et al. [[LKSP+22]](../references/LKSP+22.md) trained a reinforcement-learning agent to collect a coin in a side-scrolling video game. In every training level the coin sat at the far right end; when the experimenters moved it, the agent ran right past it to the end of the level. It had learned "move right," not "get the coin" — two policies that agree on every training level, so the data could not distinguish them. Yet training reliably produced one and not the other. Something chose, and it was not the data.

The agenda reduces the episode to a **coin line**: states $(p,c)$ with agent position $p$ and coin position $c$ in $\lbrace 0,\dots,L\rbrace $, actions $\pm1$, reward for reaching the coin. The coin sits at the right end in all but an $\varepsilon$-fraction of training episodes, so at $\varepsilon=0$ both "move right" and "go to the coin" are perfect policies. Encode the state as $x_{\mathrm a}(p,c)=(1,p,c)$ and train a two-layer ReLU network $f_\theta(x)=\sum_{j=1}^m a_j\varphi(u_j\cdot x)$, $\varphi(z)=\max(z,0)$, with $a_j\sim N(0,\sigma^2)$, $u_j\sim N(0,\sigma^2 I_3)$, by gradient descent with fixed step $\eta$ on the logistic loss for the intended action; the exact training distribution and the conventions that make the trajectory unique are fixed in [MAIS-A8](../agendas/A8/). The probe state $s^{\ast }=(\lceil L/2\rceil,0)$ puts the coin at the left end, where the two policies disagree, and $q_\varepsilon(k;m,\sigma,L,\eta)$ is the probability over the initialization that $f_{\theta_k}(x_{\mathrm a}(s^{\ast }))>0$ — that after $k$ steps the network walks away from the coin.

**Problem ([MAIS-A8, Problem 5.1](../agendas/A8/MAIS-A8.tex#L268)).** Determine whether the limit

$$\bar q_\varepsilon(m,\sigma,L,\eta)=\lim_{k\to\infty}q_\varepsilon(k;m,\sigma,L,\eta)$$

exists and, if it does, compute it. At finite width the probe sign may change more than once; the first case is $\varepsilon=0$, $m=2$.

For linear policies the answer is a theorem: the maximum-margin implicit bias theorem of Soudry et al. [[SHNGS18]](../references/SHNGS18.md) proves the proxy wins at $\varepsilon=0$, the goal wins for every $\varepsilon>0$, and the verdict flips when the encoding $(1,p,c)$ is replaced by $(1,c-p)$ — the encoding, not the initialization, decides. The two standard infinite-width limits also select the proxy at $\varepsilon=0$: the kernel (lazy) limit, in which the network barely moves from its initialization and behaves as a linear model with a fixed kernel, and the mean-field (rich) limit, in which neurons travel far and the data reorganize the function the network represents (granted the weak convergence the margin theory of Chizat and Bach [[CB20]](../references/CB20.md) assumes). At finite width the problem is open at every $\varepsilon$, including $\varepsilon=0$ at width two; the agenda's Problem 5.6 restates the $\varepsilon>0$ slice of this problem at the level of networks. For the solved linear chapter and the infinite-width propositions, see [MAIS-A8](../agendas/A8/).

## References

- [[LKSP+22]](../references/LKSP+22.md) L. Langosco, J. Koch, L. Sharkey, J. Pfau, L. Orseau, and D. Krueger, *Goal misgeneralization in deep reinforcement learning*, ICML 2022. [arXiv:2105.14111](https://arxiv.org/abs/2105.14111)
- [[SHNGS18]](../references/SHNGS18.md) D. Soudry, E. Hoffer, M. S. Nacson, S. Gunasekar, and N. Srebro, *The implicit bias of gradient descent on separable data*, JMLR 19(70):1–57, 2018. [arXiv:1710.10345](https://arxiv.org/abs/1710.10345)
- [[CB20]](../references/CB20.md) L. Chizat and F. Bach, *Implicit bias of gradient descent for wide two-layer neural networks trained with the logistic loss*, COLT 2020. [arXiv:2002.04486](https://arxiv.org/abs/2002.04486)

*Related: [MAIS-O82](MAIS-O82.md) (the conjectured answer as width grows at $\varepsilon=0$) · [MAIS-O83](MAIS-O83.md) (does any finite width favor the intended goal?) · [MAIS-O84](MAIS-O84.md) (the finite-time crossover behind "2% diversity suffices") · [MAIS-O91](MAIS-O91.md) (the numerical atlas of this selection map).*
