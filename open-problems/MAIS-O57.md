# Does gradient flow on S₅ select randomly among representation sets?

*Open problem MAIS-O57 · posed in [MAIS-A5](../agendas/A5/) as [Problem 5.7](../agendas/A5/MAIS-A5.tex#L297) · Status: open.*

*Tags: interpretability · mechanistic interpretability · universality of circuits · training dynamics · probability · dynamical systems · representation theory. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Chughtai, Chan, and Nanda trained the same width-128 network on multiplication in $S_5$ from four random seeds and read off the irreducible representations visible in its outputs: two seeds gave {sign, standard}, one added a 5-dimensional representation, one added standard⊗sign and a 5-dimensional. Is that variation genuine randomness in the limiting ensemble, or a finite-training artifact that longer runs would wash out? No symmetry can force the variation: the outer automorphism group of $S_5$ is trivial, so no automorphism identifies one candidate outcome with another.

The ensemble $\mathcal{T}(S_5, \mathrm{ReLU}, 128, \lambda, \tau)$ is the fully connected setting of those experiments: one hidden layer of 128 neurons, logits $f_\theta(a,b)(c) = \sum_{i=1}^{128} \mathrm{ReLU}(u_i(a)+v_i(b))\ w_i(c)$ with $u_i,v_i,w_i \in \mathbb{R}^{S_5}$, trained by gradient flow on the loss $L_\lambda$ (cross-entropy over the full multiplication table, plus weight decay $\lambda\Vert \theta\Vert ^2$) from independent $N(0,\tau^2)$ coordinates. Since ReLU is only piecewise smooth, gradient flow means the differential inclusion $\dot\theta(t) \in -\partial L_\lambda(\theta(t))$, where $\partial$ is the Clarke subdifferential. Its trajectories exist from every initial condition but need not be unique; the problem is asserted for every measurable assignment of one complete trajectory to each initialization (such assignments exist).

Write $\mathcal{R}(S_5)$ for the six nontrivial irreducible representations of $S_5$, and for each such $\rho$ define $\psi_\rho(a,b,c) = \chi_\rho(abc^{-1})$; these functions are mutually orthogonal in $L^2(S_5^3)$. With $\tilde\ell_\theta(a,b,c) = f_\theta(a,b)(c) - \frac{1}{120}\sum_{c'} f_\theta(a,b)(c')$ the logits centered in the output coordinate, the **key set** is

$$K_\varepsilon(\theta) = \lbrace \rho \in \mathcal{R}(S_5) : \vert \langle \tilde\ell_\theta, \psi_\rho \rangle \vert \geq \varepsilon \Vert \tilde\ell_\theta\Vert \Vert \psi_\rho\Vert \rbrace$$

(empty when $\tilde\ell_\theta = 0$): the representations whose characters, evaluated at $abc^{-1}$, carry at least an $\varepsilon$ fraction of the centered logits' $L^2$ norm. Then $\mu_t$ is the distribution of $K_\varepsilon(\theta(t))$; the problem is asserted for Lebesgue-almost every small $\varepsilon$.

**Problem ([MAIS-A5, Problem 5.7](../agendas/A5/MAIS-A5.tex#L297)).** Consider the ensembles $\mathcal{T}(S_5, \mathrm{ReLU}, 128, \lambda, \tau)$. Prove or refute: for some $\lambda, \tau > 0$ there exist two subsets $S \neq S'$ of $\mathcal{R}(S_5)$ with

$$\liminf_{t \to \infty} \mu_t(\lbrace S\rbrace ) > 0 \quad\text{and}\quad \liminf_{t \to \infty} \mu_t(\lbrace S'\rbrace ) > 0.$$

In words: at some decay strength and initialization scale, training charges at least two distinct representation sets with probability bounded away from zero for all late times. The seed data suggest the candidates $S = \lbrace \mathrm{sgn}, \mathrm{std}\rbrace $ and $S' = S \cup \lbrace \text{a 5-dimensional}\rbrace $. The static half of non-identifiability is known in a neighboring regime: for quadratic activation and squared loss on abelian tasks, Tian constructs abundant inequivalent zero-loss circuits. The dynamical half — that gradient flow from Gaussian initialization actually charges two key sets — is proved for no group and no architecture. For the surrounding definitions and results, see [MAIS-A5](../agendas/A5/).

## References

- B. Chughtai, L. Chan, and N. Nanda, *A toy model of universality: reverse engineering how networks learn group operations*, Proceedings of the 40th International Conference on Machine Learning (ICML), 2023. [arXiv:2302.03025](https://arxiv.org/abs/2302.03025)
- Y. Tian, *Composing global solutions to reasoning tasks via algebraic objects in neural nets*, Advances in Neural Information Processing Systems (NeurIPS), 2025. [arXiv:2410.01779](https://arxiv.org/abs/2410.01779)
- J. He, L. Wang, F. Zhang, S. Chen, and Z. Yang, *Neural networks provably learn spectral representations for group composition*, preprint, 2026. [arXiv:2606.02993](https://arxiv.org/abs/2606.02993)

*Related: [MAIS-O5](MAIS-O5.md) (part (b) asks whether the limiting law is a point mass) · [MAIS-O55](MAIS-O55.md) (the $S_3$ warm-up) · [MAIS-O59](MAIS-O59.md) (randomness of selection in the smallest case).*
