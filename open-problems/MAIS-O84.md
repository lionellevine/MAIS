# The crossover time and its asymptotics

*Open problem MAIS-O84 · posed in [MAIS-A8](../agendas/A8/) as [Problem 5.7](../agendas/A8/MAIS-A8.tex#L352) and [Problem 7.2](../agendas/A8/MAIS-A8.tex#L466) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · training dynamics · dynamical systems · optimization · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Randomizing the coin's position in as little as 2% of training levels largely cured Langosco et al.'s coin collector of running past a displaced coin. Why 2%? In the max-margin theory the diversity level $\varepsilon$ is absent from the endpoint: for every $\varepsilon>0$ the limiting linear classifier is the intended goal. The empirical phenomenon must therefore live at finite time — in how long the rare corrective examples take to overturn the proxy.

On the agenda's coin line, the state is an agent position $p$ and coin position $c$ in $\lbrace 0,\dots,L\rbrace $, with $L\ge4$ fixed, encoded as $x_{\mathrm a}(p,c)=(1,p,c)$. The coin sits at the right end in all but an $\varepsilon$-fraction of training episodes: a training state has $p$ uniform on $\lbrace 0,\dots,L\rbrace $ and, independently, $c=L$ with probability $1-\varepsilon$ or $c$ uniform on $\lbrace 1,\dots,L\rbrace $ with probability $\varepsilon$, conditioned on $p\ne c$; the displaced coin is deliberately never placed at $0$, so states with the coin at the left end lie outside the training distribution for every $\varepsilon$. The loss $\mathcal L_\varepsilon$ is the expectation, over this distribution, of the logistic loss $\log(1+e^{-z})$ at the margin $z=\operatorname{sign}(c-p)\,f(x_{\mathrm a}(p,c))$, small when the model agrees confidently with the intended action $\operatorname{sign}(c-p)$. The diversity level $\varepsilon$ is taken rational, so that $\mathcal L_\varepsilon$ is a finite sum with rational weights and the max-margin theorem applies verbatim.

That theorem, due to Soudry et al. (see References), says that for linearly separable data, gradient descent on the logistic loss with any initialization and any sufficiently small constant step size sends $\lVert w_k\rVert$ to infinity while $w_k/\lVert w_k\rVert$ converges to the maximum-margin direction — the direction of the minimum-norm vector classifying every training example with margin at least one. For the linear model $f_w=w\cdot x_{\mathrm a}$, the agenda's Proposition 4.3 computes this direction to be $(0,-1,1)/\sqrt2$ for every $\varepsilon\in(0,1]$, so the logit at the probe state $s^{\ast }=(\lceil L/2\rceil,0)$ — coin at the left end, where proxy and goal disagree — tends to $-\infty$. But it starts by growing positive along the proxy direction $(1,0,L)/\sqrt{1+L^2}$, the max-margin direction of the $\varepsilon=0$ data (the agenda's Proposition 4.2), whose probe logit is positive. The question is when it turns.

**Problem ([MAIS-A8, Problem 5.7](../agendas/A8/MAIS-A8.tex#L352)).** In the linear model above, run gradient descent on $\mathcal L_\varepsilon$ from $w_0=0$ with a sufficiently small constant step size, so that the max-margin theorem of Soudry et al. applies, and let

$$k^{\ast }(\varepsilon)=\inf\lbrace k:\ f_{w_k}(x_{\mathrm a}(s^{\ast }))<0\rbrace $$

be the first step at which the probe verdict flips from proxy to goal; $k^{\ast }(\varepsilon)$ is finite because the probe value tends to $-\infty$. Determine its asymptotics as $\varepsilon\to0$ with $L$ and the step size fixed. A balance between logarithmic growth along the proxy direction and an $\varepsilon$-weighted corrective drift suggests $k^{\ast }(\varepsilon)=\varepsilon^{-1+o(1)}$. For the two-layer iteration define $K^{\ast }_\varepsilon=\inf\lbrace k:f_{\theta_k}(x_{\mathrm a}(s^{\ast }))<0\rbrace $, with $K^{\ast }_\varepsilon=\infty$ if the set is empty, and determine $\Pr(K^{\ast }_\varepsilon>N)$ as a function of $(\varepsilon,m,\sigma,\eta,L)$.

Here the two-layer iteration is gradient descent with step $\eta$, on the same loss with the same encoding, for the width-$m$ ReLU network $f_\theta(x)=\sum_{j=1}^{m}a_j\max(u_j\cdot x,0)$, all of whose parameters $(a_1,\dots,a_m,u_1,\dots,u_m)$ are trained, initialized independently with $a_j\sim N(0,\sigma^2)$ and $u_j\sim N(0,\sigma^2 I_3)$. Backpropagation takes the derivative of $\max(z,0)$ at zero to be zero, so each initialization determines a unique trajectory; the probability is over that initialization. The agenda's starter section sharpens the linear part:

**Problem ([MAIS-A8, Problem 7.2](../agendas/A8/MAIS-A8.tex#L466)).** Prove $k^{\ast }(\varepsilon)=\varepsilon^{-1+o(1)}$, or refute it, in the setting of the problem above. The tools are those of Soudry et al. plus a two-phase analysis; no network is involved.

The crossover time is the theory's answer to the 2%: Langosco et al.'s agents were trained for a fixed compute budget, so the empirical misgeneralization frequency should be read at a fixed iteration budget, and the curve it traces is the distribution of $k^{\ast }$. For the max-margin computations this problem builds on, see [MAIS-A8](../agendas/A8/).

## References

- Soudry, Hoffer, Nacson, Gunasekar, and Srebro, *The implicit bias of gradient descent on separable data*, J. Mach. Learn. Res. 19(70):1–57, 2018. [arXiv:1710.10345](https://arxiv.org/abs/1710.10345)
- Ji and Telgarsky, *The implicit bias of gradient descent on nonseparable data*, COLT 2019 — the refined residual and rate analysis for the linear case. [arXiv:1803.07300](https://arxiv.org/abs/1803.07300)
- Langosco, Koch, Sharkey, Pfau, Orseau, and Krueger, *Goal misgeneralization in deep reinforcement learning*, ICML 2022 — the 2% experiment. [arXiv:2105.14111](https://arxiv.org/abs/2105.14111)

*Related: [MAIS-O8](MAIS-O8.md) (the selection map whose finite-time structure this is) · [MAIS-O89](MAIS-O89.md) (the other linear-model residual question) · [MAIS-O88](MAIS-O88.md) (the reinforcement-learning diversity curve).*
