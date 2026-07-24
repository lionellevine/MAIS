# Learning coefficients of modular addition

*Open problem MAIS-O63 · posed in [MAIS-A6](../agendas/A6/MAIS-A6.pdf) as [Problem 4.5](../agendas/A6/MAIS-A6.tex#L294) · Status: open.*

*Safety: interpretability, generalization — singular learning theory · developmental interpretability · grokking. Mathematics: algebraic geometry · statistics. Difficulty: ★★★ hard.*

Singular learning theory predicts where a Bayesian learner's posterior settles: on the parameters of smallest **learning coefficient** $\lambda$, a volume-growth exponent — the volume of parameters within $\varepsilon$ of the minimal loss near $w$ scales like $\varepsilon^{\lambda(w)}$ times $(\log\frac{1}{\varepsilon})^{m(w)-1}$, where the integer $m(w)$ is the multiplicity. If $\lambda$ can be computed for a real task, it predicts *which algorithm* a trained network implements, before training it. No such computation exists for any task whose learned mechanism is known.

Modular addition is the test case. For odd $p$ and width $H$, the network $f_w(a,b)=\sum_{j=1}^H V_j\bigl(u_j'(a)+u_j''(b)\bigr)^2$ is trained to compute $a+b \bmod p$; its population loss is an explicit degree-six polynomial in the weights. Fourier inversion gives exact fits $w^F$ in which each contributing neuron carries a single frequency — up to a change of basis, exactly the mechanism found by reverse-engineering trained networks. Let $W_0(p,H)$ be the set of exact fits, $w^F_H$ the Fourier solution padded with dead units, and $R_p = 1+\lVert w^F_{2p-1}\rVert$.

**Problem ([MAIS-A6, Problem 4.5](../agendas/A6/MAIS-A6.tex#L294)).** Fix an odd integer $p\ge3$ and an integer $H\ge 2p-1$.

- (a) Determine $\lambda(w^F_H)$ and $m(w^F_H)$.
- (b) For each $R\ge R_p$, determine $\lambda_{\min}(p,H;R)=\min\lbrace \lambda(w): w\in W_0(p,H),\ \lVert w\rVert\le R\rbrace $, the set of local multiplicities among the minimizers, and whether the answer depends on $R$.

A closed form in $(p,H)$ is the goal; upper and lower bounds that pin down the growth in either variable would already be progress. Part (b) is the safety-relevant quantity: the points attaining $\lambda_{\min}$ are where the posterior settles, so a formula for the minimizers is a prediction of which implementation of modular addition Bayesian learning prefers. For the definition of the local coefficient and what is known near the non-degenerate regime, see [MAIS-A6](../agendas/A6/MAIS-A6.pdf).

*Related: [MAIS-O6](MAIS-O6.md) (is the Fourier mechanism forced by singular geometry?) · [MAIS-O62](MAIS-O62.md) (the minimal width for an exact fit) · [MAIS-O70](MAIS-O70.md) (local coefficients on the template).*
