# Wide networks select the proxy policy with probability one

*Open problem MAIS-O82 · posed in [MAIS-A8](../agendas/A8/) as [Conjecture 5.2](../agendas/A8/MAIS-A8.tex#L281) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · simplicity bias · probability · optimization. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

An agent trained to collect a coin that always sat at the right end of its levels learned "move right," not "get the coin" — two rules that agree on every training level and disagree the moment the coin moves. Predicting *which* of two training-indistinguishable policies gradient descent selects is the mathematical core of goal misgeneralization.

The agenda builds a one-dimensional coin world with the degeneracy built in: states $(p,c)$ with agent position $p$ and coin position $c$ in $\lbrace 0,\dots,L\rbrace $, actions $\pm1$ (step left, step right), reward for reaching the coin. A training state has $p$ uniform on $\lbrace 0,\dots,L\rbrace $ and, independently, the coin at the right end $c=L$ with probability $1-\varepsilon$ and uniform on $\lbrace 1,\dots,L\rbrace $ with probability $\varepsilon$, conditioned on $p\ne c$; its label is the coin-seeking action $y=\operatorname{sign}(c-p)$. At $\varepsilon=0$ the coin always sits at the right end, so both "move right" (the proxy) and "go to the coin" (the intended goal) fit the training data perfectly. Encode the state as $x_{\mathrm a}(p,c)=(1,p,c)$, with positive output read as "step right." Behavior cloning then fits a two-layer ReLU network $f_\theta(x)=\sum_{j=1}^m a_j\varphi(u_j\cdot x)$, $\varphi(z)=\max(z,0)$, of width $m$, both layers trained, initialized with independent $a_j\sim N(0,\sigma^2)$ and $u_j\sim N(0,\sigma^2 I_3)$, by full-batch gradient descent with fixed step size $\eta$ on the population logistic loss $\mathbb E\,\log\bigl(1+e^{-y f_\theta(x_{\mathrm a}(p,c))}\bigr)$, with the convention $\varphi'(0)=0$ so the initialization determines a unique trajectory. The probe state $s^{\ast }=(\lceil L/2\rceil,0)$ puts the coin at the far left, where the two policies disagree, and $q_\varepsilon(k;m,\sigma,L,\eta)$ is the probability over the initialization that $f_{\theta_k}(x_{\mathrm a}(s^{\ast }))>0$: that after $k$ training steps the network walks away from the coin. In the *linear* case the question is settled: the max-margin implicit-bias theorem of Soudry et al. [[SHNGS18]](https://arxiv.org/abs/1710.10345) proves the proxy wins at $\varepsilon=0$, and the verdict flips when $(1,p,c)$ is replaced by the relative encoding $(1,c-p)$. The first genuinely nonlinear case is the conjecture:

**Conjecture ([MAIS-A8, Conjecture 5.2](../agendas/A8/MAIS-A8.tex#L281)).** For every $\sigma>0$, $L\ge4$, and sufficiently small $\eta>0$,

$$\lim_{m\to\infty}\ \liminf_{k\to\infty}\ q_0(k;m,\sigma,L,\eta)\ =\ 1.$$

In words: at zero training diversity, for any initialization scale and any sufficiently small step size, an infinitely wide two-layer network provably walks away from the coin. Kernel-regime and mean-field analogues are proved in the agenda (the mean-field one granted the weak convergence that the margin theory of Chizat and Bach [[CB20]](https://arxiv.org/abs/2002.04486) assumes), but each rescales the network as the width grows, by $m^{-1/2}$ and $m^{-1}$ respectively, so neither formally implies the conjecture: here the parameterization is the standard one above, training runs at finite width, and the width limit comes only after the training limit. For the environment's exact definition and the solved linear chapter, see [MAIS-A8](../agendas/A8/).

## References

- [SHNGS18] D. Soudry, E. Hoffer, M. S. Nacson, S. Gunasekar, and N. Srebro, *The implicit bias of gradient descent on separable data*, JMLR 19(70):1–57, 2018. [arXiv:1710.10345](https://arxiv.org/abs/1710.10345)
- [LL20] K. Lyu and J. Li, *Gradient descent maximizes the margin of homogeneous neural networks*, ICLR 2020. [arXiv:1906.05890](https://arxiv.org/abs/1906.05890)
- [CB20] L. Chizat and F. Bach, *Implicit bias of gradient descent for wide two-layer neural networks trained with the logistic loss*, COLT 2020. [arXiv:2002.04486](https://arxiv.org/abs/2002.04486)

*Related: [MAIS-O8](MAIS-O8.md) (the selection map this conjecture would begin to compute) · [MAIS-O84](MAIS-O84.md) (how fast rare corrective examples overturn the proxy) · [MAIS-O87](MAIS-O87.md) (exploration starvation).*
