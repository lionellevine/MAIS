# Learning coefficients of modular addition

*Open problem MAIS-O63 · posed in [MAIS-A6](../agendas/A6/) as [Problem 4.5](../agendas/A6/MAIS-A6.tex#L295) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · grokking · algebraic geometry · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Watanabe's singular learning theory [W09] predicts where a Bayesian learner's posterior settles: on the parameters of smallest **local learning coefficient** $\lambda(w)$, a volume-growth exponent — the volume of parameters near $w$ with population loss at most $\varepsilon$ scales like $\varepsilon^{\lambda(w)}$ times $(\log\frac{1}{\varepsilon})^{m(w)-1}$, where the integer $m(w)$ is the **multiplicity**. If $\lambda$ can be computed for a real task, it predicts *which algorithm* a trained network implements, before training it. No such computation exists for any task whose learned mechanism is known.

Modular addition is the test case. For odd $p$ and width $H$, the network $f_w(a,b)=\sum_{j=1}^H V_j\bigl(u_j'(a)+u_j''(b)\bigr)^2$ — lookup tables $u_j', u_j''$ on $\mathbb{Z}/p\mathbb{Z}$, output columns $V_j \in \mathbb{R}^p$ — is trained to output the one-hot vector of $a+b \bmod p$; its population loss is an explicit degree-six polynomial in the $3pH$ weights. Fourier inversion gives an exact fit $w^F$ at width $2p-1$ in which each contributing neuron carries a single frequency ([MAIS-A6, Lemma 4.2](../agendas/A6/MAIS-A6.tex#L240) has the explicit table) — up to a change of basis, exactly the mechanism that Nanda, Chan, Lieberum, Smith, and Steinhardt [[NCLSS23]](https://arxiv.org/abs/2301.05217) found by reverse-engineering trained networks. Let $W_0(p,H)$ be the variety of exact fits, $w^F_H \in W_0(p,H)$ the Fourier solution padded with zero units, and $R_p = 1+\lVert w^F_{2p-1}\rVert$.

**Problem ([MAIS-A6, Problem 4.5](../agendas/A6/MAIS-A6.tex#L295)).** Fix an odd integer $p\ge3$ and an integer $H\ge 2p-1$.

- (a) Determine $\lambda(w^F_H)$ and $m(w^F_H)$.
- (b) For each $R\ge R_p$, determine $\lambda_{\min}(p,H;R)=\min\lbrace \lambda(w): w\in W_0(p,H),\ \lVert w\rVert\le R\rbrace $, the set of local multiplicities among the minimizers, and whether the answer depends on $R$.

A closed form in $(p,H)$ is the goal; upper and lower bounds that pin down the growth in either variable would already be progress. The ball in part (b) is forced by symmetry: the per-unit scalings $(u_j, V_j) \mapsto (t\,u_j,\ t^{-2}V_j)$ fix $f_w$, so $W_0$ is unbounded and an unrestricted minimum could escape along these orbits. Part (b) is the safety-relevant quantity: the points attaining $\lambda_{\min}$ are where the posterior settles, so a formula for the minimizers is a prediction of which implementation of modular addition Bayesian learning prefers. What is known — the closed-form local coefficients of Cullen, Estan-Ruiz, Danait, and Li [[CEDL26]](https://arxiv.org/abs/2603.01192), valid under non-degeneracy hypotheses that fail at $w^F$, and bounds on the marginal cost of width — is in [MAIS-A6](../agendas/A6/).

## References

- [W09] S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- [CEDL26] B. Cullen, S. Estan-Ruiz, R. Danait, and J. Li, *A Basin-Selection Perspective on Grokking via Singular Learning Theory*, 2026. [arXiv:2603.01192](https://arxiv.org/abs/2603.01192)
- [NCLSS23] N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, *Progress measures for grokking via mechanistic interpretability*, ICLR 2023. [arXiv:2301.05217](https://arxiv.org/abs/2301.05217)

*Related: [MAIS-O6](MAIS-O6.md) (is the Fourier mechanism forced by singular geometry?) · [MAIS-O62](MAIS-O62.md) (the minimal width for an exact fit) · [MAIS-O70](MAIS-O70.md) (local coefficients on the template).*
