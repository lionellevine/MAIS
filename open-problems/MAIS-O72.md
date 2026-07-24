# Finiteness and frontier condition for learning-coefficient strata

*Open problem MAIS-O72 · posed in [MAIS-A7](../agendas/A7/MAIS-A7.pdf) as [Question 3.1](../agendas/A7/MAIS-A7.tex#L215) · Status: open.*

*Safety: generalization — singular learning theory · developmental interpretability. Mathematics: algebraic geometry. Difficulty: ★★★ hard.*

Singular learning theory predicts that Bayesian learning selects, among the zero-loss parameters of a network, the flattest ones — those of smallest learning coefficient. Any theorem about "effective dynamics on the strata" of the optimal set presupposes that the level sets of the learning coefficient are honest geometric objects. Are they?

For $L$ real-analytic near $w^\ast$ and not locally constant there, the **local learning coefficient** $\lambda(w^\ast) \in \mathbb{Q}_{>0}$ and its **multiplicity** $m(w^\ast) \ge 1$ are the volume exponents

$$\mathrm{vol}\bigl\lbrace  w \in B_\delta(w^\ast) : |L(w) - L(w^\ast)| < \varepsilon \bigr\rbrace  \asymp \varepsilon^{\lambda(w^\ast)} \bigl( \log \tfrac1\varepsilon \bigr)^{m(w^\ast)-1},$$

so a small $\lambda$ means near-level parameters are plentiful; at a local minimum, $\lambda$ is Watanabe's real log canonical threshold. On the optimal set $W_0 = L^{-1}(0)$, the level sets $S_c = \lbrace  w \in W_0 : \lambda(w) = c \rbrace $ partition $W_0$; the agenda calls this the $\lambda$-stratification, and the name is aspirational. The question is closely related to Conjecture 5 of Lin (*J. Algebraic Stat.* 2017).

**Question ([MAIS-A7, Question 3.1](../agendas/A7/MAIS-A7.tex#L215)).** Let $L\colon \mathbb{T}^d \to [0,\infty)$ be real-analytic and not identically zero, with $W_0 = L^{-1}(0) \neq \emptyset$. (Since $\mathbb{T}^d$ is connected, analyticity then forbids $L$ from vanishing on any open set, so the local learning coefficient is defined at every point of $W_0$; for $L \equiv 0$ the map below is undefined everywhere.) Let $\lambda\colon W_0 \to \mathbb{Q}_{>0}$ be the local learning coefficient.

- **(a)** Does $\lambda$ take only finitely many values on $W_0$?
- **(b)** Is each level set $S_c$ a locally closed subanalytic subset of $\mathbb{T}^d$, and does the partition satisfy the frontier condition $\overline{S_c} \setminus S_c \subseteq \bigcup_{c' < c} S_{c'}$?

For the refinement by multiplicity, order pairs by declaring $(\lambda', m')$ deeper than $(\lambda, m)$ when $\lambda' < \lambda$, or when $\lambda' = \lambda$ and $m' > m$. Does the finite-image assertion and the corresponding locally closed subanalytic frontier condition hold for this ordered pair?

Part of the frontier picture is now known: Lehalleur and Rimányi ([arXiv:2411.19920](https://arxiv.org/abs/2411.19920), Proposition 8.4(ii)) prove $\lambda$ is lower semicontinuous, so $\lbrace  w \in W_0 : \lambda(w) \le c \rbrace $ is closed in $W_0$. Finiteness of the image, subanalyticity of the pieces, and the multiplicity-refined version remain open. The real case has behavior absent from its complexification, including parity effects visible in the Aoyagi–Watanabe formula for reduced rank regression. For the surrounding program, see [MAIS-A7](../agendas/A7/MAIS-A7.pdf).

*Related: [MAIS-O7](MAIS-O7.md) (the headline conjecture whose staircase runs over these strata) · [MAIS-O77](MAIS-O77.md) (computing the stratification for a concrete fiber) · [MAIS-O73](MAIS-O73.md) (metastable timescales built from stratum data).*
