# Learning coefficients of modular addition

*Open problem MAIS-O63 · posed in [MAIS-A6](../agendas/A6/) as [Problem 4.5](../agendas/A6/MAIS-A6.tex#L295) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · grokking · algebraic geometry · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Singular learning theory predicts where a Bayesian learner's posterior settles: on the parameters of smallest **local learning coefficient** $\lambda(w)$, a volume-growth exponent. Writing $K$ for the population loss, at a point $w$ with $K(w)=0$ the volume of $\lbrace w' \in B_\delta(w) : K(w') \le \varepsilon\rbrace $ scales like a constant times $\varepsilon^{\lambda(w)}$ times $(\log\frac{1}{\varepsilon})^{m(w)-1}$ as $\varepsilon \to 0$; the integer $m(w)$ is the **multiplicity**, and the pair $(\lambda(w), m(w))$ does not depend on the radius $\delta$ once it is small enough. If $\lambda$ can be computed for a real task, it predicts *which algorithm* a trained network implements, before training it. No such computation exists for any task whose learned mechanism is known.

Modular addition is the test case. Fix an odd $p$ and a width $H$. On input $(a,b) \in (\mathbb{Z}/p\mathbb{Z})^2$ the network computes $f_w(a,b)=\sum_{j=1}^H V_j\bigl(u_j'(a)+u_j''(b)\bigr)^2 \in \mathbb{R}^p$, with lookup tables $u_j', u_j''\colon \mathbb{Z}/p\mathbb{Z} \to \mathbb{R}$ and output columns $V_j \in \mathbb{R}^p$, so the parameter $w$ ranges over $\mathbb{R}^{3pH}$; the target is the one-hot vector $\delta_{a+b} \in \mathbb{R}^p$ of the sum $a+b \bmod p$. The population loss $K(w) = \frac{1}{2p^2}\sum_{a,b}\lVert f_w(a,b)-\delta_{a+b}\rVert^2$, half the mean squared error over the $p^2$ inputs, is an explicit degree-six polynomial in the weights.

Fourier inversion on $\mathbb{Z}/p\mathbb{Z}$ gives an explicit exact fit $w^F$ at width $2p-1$: one constant unit plus, for each frequency $1 \le k \le (p-1)/2$, four units whose lookup tables are $\cos(2\pi k\,\cdot/p)$ or $\pm\sin(2\pi k\,\cdot/p)$, with output columns the inverting Fourier weights $(\cos(2\pi kc/p)/p)_c$ and $(\sin(2\pi kc/p)/p)_c$ ([MAIS-A6, Lemma 4.2](../agendas/A6/MAIS-A6.tex#L240) has the full table). Each contributing neuron carries a single frequency — up to a change of basis, exactly the mechanism found by reverse-engineering trained networks. Let $W_0(p,H) = \lbrace w \in \mathbb{R}^{3pH} : f_w(a,b) = \delta_{a+b} \text{ for all } a,b\rbrace $ be the variety of exact fits, $w^F_H \in W_0(p,H)$ the Fourier solution padded with $H-(2p-1)$ zero units, and $R_p = 1+\lVert w^F_{2p-1}\rVert$, where $\lVert \cdot \rVert$ is the Euclidean norm on $\mathbb{R}^{3pH}$.

**Problem ([MAIS-A6, Problem 4.5](../agendas/A6/MAIS-A6.tex#L295)).** Fix an odd integer $p\ge3$ and an integer $H\ge 2p-1$.

- (a) Determine $\lambda(w^F_H)$ and $m(w^F_H)$.
- (b) For each $R\ge R_p$, determine $\lambda_{\min}(p,H;R)=\min\lbrace \lambda(w): w\in W_0(p,H),\ \lVert w\rVert\le R\rbrace $, the set of local multiplicities among the minimizers, and whether the answer depends on $R$.

A closed form in $(p,H)$ is the goal; upper and lower bounds that pin down the growth in either variable would already be progress. The ball in part (b) is forced by symmetry: the per-unit scalings $(u_j, V_j) \mapsto (t\,u_j,\ t^{-2}V_j)$ fix $f_w$, so $W_0$ is unbounded and an unrestricted minimum could escape along these orbits. Part (b) is the safety-relevant quantity: the points attaining $\lambda_{\min}$ are where the posterior settles, so a formula for the minimizers is a prediction of which implementation of modular addition Bayesian learning prefers. What is known — closed-form local coefficients under non-degeneracy hypotheses that fail at $w^F$, and bounds on the marginal cost of width — is in [MAIS-A6](../agendas/A6/).

## References

- S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- B. Cullen, S. Estan-Ruiz, R. Danait, and J. Li, *Grokking as a phase transition between competing basins: a singular learning theory approach*, 2026. [arXiv:2603.01192](https://arxiv.org/abs/2603.01192)
- N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, *Progress measures for grokking via mechanistic interpretability*, ICLR 2023. [arXiv:2301.05217](https://arxiv.org/abs/2301.05217)

*Related: [MAIS-O6](MAIS-O6.md) (is the Fourier mechanism forced by singular geometry?) · [MAIS-O62](MAIS-O62.md) (the minimal width for an exact fit) · [MAIS-O70](MAIS-O70.md) (local coefficients on the template).*
