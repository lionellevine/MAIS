# Exchangeability of learned frequencies beyond multiplicative symmetry

*Open problem MAIS-O58 · posed in [MAIS-A5](../agendas/A5/) as [Question 5.8](../agendas/A5/MAIS-A5.tex#L306) · Status: open.*

*Tags: interpretability · mechanistic interpretability · training dynamics · universality of circuits · probability · harmonic analysis · dynamical systems. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

When a network learns addition mod $p$, it expresses its outputs through a sparse random set of the $(p-1)/2$ Fourier frequencies. One symmetry of that random set is a theorem: the automorphisms of $C_p$ act on frequencies by $\zeta \mapsto t\zeta$ for $t \in (\mathbb{Z}/p\mathbb{Z})^\times$, the training ensemble is invariant under them, and they act transitively, so every frequency is learned with the same probability. But multiplication does not act transitively on *pairs* or on $k$-element sets of frequencies. Could training prefer multiplicatively structured sets, say geometric progressions $\lbrace \zeta, 2\zeta, 4\zeta, \dots\rbrace $?

The setting is the selection-law problem ([MAIS-O5](MAIS-O5.md)): a one-hidden-layer network of width $m$ with activation $\sigma$, logits $f_\theta(a,b)(c) = \sum_{i=1}^m \sigma(u_i(a)+v_i(b))\ w_i(c)$ for $u_i,v_i,w_i \in \mathbb{R}^{C_p}$, trained by gradient flow on the cross-entropy loss over the full addition table plus weight decay $\lambda\Vert \theta\Vert ^2$, from independent $N(0,\tau^2)$ coordinates. Here the width $m$ and the constants $\lambda, \tau > 0$ are fixed but arbitrary: no limit in $m$, $\lambda$, or $\tau$ is taken, the question is posed for each choice separately, and an answer for a single explicit choice is a full solution. (For $\sigma = \mathrm{ReLU}$ the loss is only piecewise smooth; the flow then means a Clarke trajectory, and the question is asserted for every measurable selection of one trajectory per initial condition.)

The irreducible characters of $C_p$ are $\rho_\zeta(a) = e^{2\pi i \zeta a/p}$, paired into frequency classes $[\rho_\zeta] = \lbrace \rho_\zeta, \rho_{-\zeta}\rbrace $ with $1 \le \zeta \le (p-1)/2$. Let $\tilde\ell_\theta(a,b,c) = f_\theta(a,b)(c) - \frac{1}{p}\sum_{c'} f_\theta(a,b)(c')$ be the centered logits and $\psi_\zeta(a,b,c) = e^{2\pi i \zeta (a+b-c)/p}$ the character $\rho_\zeta$ evaluated at $a+b-c$, both in $L^2(C_p^3)$ with counting measure (so $\Vert \psi_\zeta\Vert ^2 = p^3$). The **key set** is

$$K_\varepsilon(\theta) \ =\ \bigl\lbrace \, [\rho_\zeta] \ :\ |\langle \tilde\ell_\theta, \psi_\zeta\rangle |^2 + |\langle \tilde\ell_\theta, \psi_{-\zeta}\rangle |^2 \ \ge\ \varepsilon^2\, p^3\, \Vert \tilde\ell_\theta\Vert ^2 \,\bigr\rbrace$$

(empty when $\tilde\ell_\theta = 0$): the classes whose pair of characters captures at least an $\varepsilon$ fraction of the centered logits' $L^2$ norm. The selection law $\mu_t$ is the law of the random set $K_\varepsilon(\theta(t))$, for Lebesgue-almost every small $\varepsilon$.

**Question ([MAIS-A5, Question 5.8](../agendas/A5/MAIS-A5.tex#L306)).** Fix $G = C_p$ with $p \ge 7$, an activation $\sigma \in \lbrace x^2, \mathrm{ReLU}\rbrace $, and $m, \lambda, \tau$ as in the selection-law problem. Is every limit point of the selection laws $(\mu_t)_{t \ge 0}$ invariant under *all* permutations of the $(p-1)/2$ frequency classes, or only under the multiplicative action? Equivalently: conditioned on $|K_\varepsilon| = k$, is $K_\varepsilon$ asymptotically a uniformly random $k$-set?

A negative answer would mean training feels the multiplicative structure of $(\mathbb{Z}/p\mathbb{Z})^\times$ when choosing frequencies — for instance, preferring or avoiding sets closed under doubling — something no published experiment has tested. The question starts at $p = 7$: for $p \le 5$ there are at most two frequency classes, and the multiplicative action already realizes every permutation of them. For the proved symmetry and the ensemble conventions, see [MAIS-A5](../agendas/A5/).

## References

- B. Chughtai, L. Chan, and N. Nanda, *A toy model of universality: reverse engineering how networks learn group operations*, ICML 2023. [arXiv:2302.03025](https://arxiv.org/abs/2302.03025)
- N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, *Progress measures for grokking via mechanistic interpretability*, ICLR 2023. [arXiv:2301.05217](https://arxiv.org/abs/2301.05217)
- D. Morwani, B. L. Edelman, C.-A. Oncescu, R. Zhao, and S. Kakade, *Feature emergence via margin maximization: case studies in algebraic tasks*, ICLR 2024. [arXiv:2311.07568](https://arxiv.org/abs/2311.07568)

*Related: [MAIS-O5](MAIS-O5.md) (the selection law itself) · [MAIS-O52](MAIS-O52.md) (how many frequencies, rather than which sets) · [MAIS-O61](MAIS-O61.md) (an experimental pipeline that could test small cases).*
