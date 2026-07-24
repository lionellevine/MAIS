# The crossover time and its asymptotics

*Open problem MAIS-O84 · posed in [MAIS-A8](../agendas/A8/MAIS-A8.pdf) as [Problem 5.7](../agendas/A8/MAIS-A8.tex#L351) and [Problem 7.2](../agendas/A8/MAIS-A8.tex#L465) · Status: open.*

*Safety: generalization — goal misgeneralization · proxy goals · training dynamics. Mathematics: dynamical systems · optimization · probability. Difficulty: ★★★ hard.*

Randomizing the coin's position in as little as 2% of training levels largely cured Langosco et al.'s coin collector of running past a displaced coin. Why 2%? In the max-margin theory the diversity level $\varepsilon$ is absent from the endpoint: for every $\varepsilon>0$ the limiting linear classifier is the intended goal. The empirical phenomenon must therefore live at finite time — in how long the rare corrective examples take to overturn the proxy.

On the agenda's coin line, the state is an agent position $p$ and coin position $c$ in $\lbrace 0,\dots,L\rbrace $, encoded as $x_{\mathrm a}(p,c)=(1,p,c)$; the coin sits at the right end in all but an $\varepsilon$-fraction of training episodes, and $\mathcal L_\varepsilon$ is the logistic loss for the intended action $\operatorname{sign}(c-p)$, averaged over the training distribution. For the linear model $f_w=w\cdot x_{\mathrm a}$, the agenda's Proposition 4.3 shows that gradient descent on $\mathcal L_\varepsilon$ converges in direction to $(0,-1,1)/\sqrt2$ for every $\varepsilon\in(0,1]$, so the logit at the probe state $s^{\ast }=(\lceil L/2\rceil,0)$ — coin at the left end, where proxy and goal disagree — tends to $-\infty$. But it starts by growing positive along the proxy direction. The question is when it turns.

**Problem ([MAIS-A8, Problem 5.7](../agendas/A8/MAIS-A8.tex#L351)).** In the linear model above, run gradient descent on $\mathcal L_\varepsilon$ from $w_0=0$ with a sufficiently small constant step size, so that the max-margin theorem of Soudry et al. applies, and let

$$k^{\ast }(\varepsilon)=\inf\lbrace k:\ f_{w_k}(x_{\mathrm a}(s^{\ast }))<0\rbrace $$

be the first step at which the probe verdict flips from proxy to goal; $k^{\ast }(\varepsilon)$ is finite because the probe value tends to $-\infty$. Determine its asymptotics as $\varepsilon\to0$ with $L$ and the step size fixed. A balance between logarithmic growth along the proxy direction and an $\varepsilon$-weighted corrective drift suggests $k^{\ast }(\varepsilon)=\varepsilon^{-1+o(1)}$. For the two-layer iteration define $K^{\ast }_\varepsilon=\inf\lbrace k:f_{\theta_k}(x_{\mathrm a}(s^{\ast }))<0\rbrace $, with $K^{\ast }_\varepsilon=\infty$ if the set is empty, and determine $\Pr(K^{\ast }_\varepsilon>N)$ as a function of $(\varepsilon,m,\sigma,\eta,L)$.

Here the two-layer iteration is gradient descent with step $\eta$ for a width-$m$ ReLU network from Gaussian initialization of scale $\sigma$, and the probability is over that initialization. The agenda's starter section sharpens the linear part:

**Problem ([MAIS-A8, Problem 7.2](../agendas/A8/MAIS-A8.tex#L465)).** Prove $k^{\ast }(\varepsilon)=\varepsilon^{-1+o(1)}$, or refute it, in the setting of the problem above. The tools are those of Soudry et al. plus a two-phase analysis; no network is involved.

The crossover time is the theory's answer to the 2%: Langosco et al.'s agents were trained for a fixed compute budget, so the empirical misgeneralization frequency should be read at a fixed iteration budget, and the curve it traces is the distribution of $k^{\ast }$. For the max-margin computations this problem builds on, see [MAIS-A8](../agendas/A8/MAIS-A8.pdf).

*Related: [MAIS-O8](MAIS-O8.md) (the selection map whose finite-time structure this is) · [MAIS-O89](MAIS-O89.md) (the other linear-model residual question) · [MAIS-O88](MAIS-O88.md) (the reinforcement-learning diversity curve).*
