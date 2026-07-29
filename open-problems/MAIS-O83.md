# Does some finite-width network favor the intended goal?

*Open problem MAIS-O83 · posed in [MAIS-A8](../agendas/A8/) as [Question 5.5](../agendas/A8/MAIS-A8.tex#L336) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · simplicity bias · probability · optimization. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Both infinite-width limits of the coin-line network walk away from a displaced coin: the kernel flow provably drives the off-distribution probe logit to $+\infty$, and the mean-field limit — the margin maximizer identified by Chizat and Bach [[CB20]](https://arxiv.org/abs/2002.04486), granted weak convergence of the representing measures — is strictly positive there. Does anything at finite width prefer to collect the coin instead?

The setting is the agenda's coin line, a one-dimensional distillation of the coin-collecting game in which Langosco et al. [[LKSP+22]](https://arxiv.org/abs/2105.14111) observed goal misgeneralization — the trained agent kept its competence but pursued the wrong objective, running past a displaced coin. An agent at position $p$ and a coin at position $c$ occupy $\lbrace 0,\dots,L\rbrace $, with the coin always at the right end during training, so that "move right" (the proxy) and "go to the coin" (the intended goal) both fit the training data perfectly. The **standard family** is the two-layer ReLU network $f_\theta(x)=\sum_{j=1}^m a_j\varphi(u_j\cdot x)$ on the encoding $x_{\mathrm a}(p,c)=(1,p,c)$, with $a_j\sim N(0,\sigma^2)$, $u_j\sim N(0,\sigma^2 I_3)$, trained by gradient descent with fixed step $\eta$ on the logistic loss for the intended action (backpropagation convention $\varphi'(0)=0$, so each initialization $\theta_0$ determines a unique trajectory $\theta_k$). At the probe state $s^{\ast }=(\lceil L/2\rceil,0)$ the coin lies at the left end and the two policies disagree; a negative logit there means the trained network steps toward the coin.

**Question ([MAIS-A8, Question 5.5](../agendas/A8/MAIS-A8.tex#L336)).** Do there exist $L\ge4$, $m$, $\sigma>0$, and a sufficiently small step size $\eta>0$ with

$$\limsup_{k\to\infty}\ \mathbb P_{\theta_0}\bigl(f_{\theta_k}(x_{\mathrm a}(s^{\ast }))<0\bigr)\ >\ \tfrac12$$

— a member of the standard family at which the trained network walks strictly toward the displaced coin with probability better than one half?

In words: is there any choice of width, initialization scale, and step size at which training selects the intended goal more often than not, the probability being over the random initialization alone? The agenda conjectures the opposite as the width grows: the misgeneralization probability tends to one. A single verified coin-lover, even at $L=4$ and width two, would show finite-width selection genuinely departs from both infinite-width limits. For those limits and the environment's exact definition, see [MAIS-A8](../agendas/A8/).

## References

- [CB20] L. Chizat and F. Bach, *Implicit bias of gradient descent for wide two-layer neural networks trained with the logistic loss*, Conference on Learning Theory 2020. [arXiv:2002.04486](https://arxiv.org/abs/2002.04486)
- [LKSP+22] L. Langosco, J. Koch, L. Sharkey, J. Pfau, L. Orseau, and D. Krueger, *Goal misgeneralization in deep reinforcement learning*, International Conference on Machine Learning 2022. [arXiv:2105.14111](https://arxiv.org/abs/2105.14111)

*Related: [MAIS-O82](MAIS-O82.md) (the opposing conjecture: wide networks select the proxy) · [MAIS-O8](MAIS-O8.md) (the full selection map this question probes) · [MAIS-O90](MAIS-O90.md) (whether finite-width training inherits the kernel flow's selection).*
