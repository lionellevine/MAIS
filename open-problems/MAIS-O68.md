# Learning coefficients of linear attention

*Open problem MAIS-O68 · posed in [MAIS-A6](../agendas/A6/) as [Problem 5.5](../agendas/A6/MAIS-A6.tex#L452) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · algebraic geometry · statistics · computational. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Singular learning theory is the mathematical backbone of developmental interpretability: the **learning coefficient** $\lambda$ of a network's loss landscape replaces the parameter count in the asymptotics of Bayesian generalization, and estimating it numerically is how that program detects phase transitions in training. Exact values against which the estimates could be calibrated exist for few model families — completely, only for reduced-rank regression, whose learning coefficients Aoyagi and Watanabe [AW05] determined in closed form. Which attention variant is closest to that solved family? Drop the softmax from a one-head attention layer and the population loss becomes an explicit polynomial of degree ten — the nearest attention analog of reduced-rank regression, and the variant most likely to fall to existing technology: Newton polyhedra and computer algebra.

The parameter is $w = (E, Q, U)$ with $E \in \mathbb{R}^{v \times e}$, $Q \in \mathbb{R}^{e \times e}$, $U \in \mathbb{R}^{e \times v}$, where $v$ is the vocabulary size, $T$ the context length, and $e$ the embedding dimension; row $E_a$ is the embedding of token $a$. **Linear attention with squared error** computes, on a string $x \in [v]^T$ of tokens ($[v] = \lbrace 1,\dots,v\rbrace $),

$$\ell^{\mathrm{lin}}(x) = \frac{1}{T} \sum_{t=1}^{T} \bigl(E_{x_T} Q E_{x_t}^{\top}\bigr)\  E_{x_t} U \in \mathbb{R}^v,$$

with Gaussian output model $y = \ell^{\mathrm{lin}}(x) + N(0, I_v)$ and inputs uniform on $[v]^T$. Each coordinate of $\ell^{\mathrm{lin}}$ is multihomogeneous of degree $(3,1,1)$ in $(E,Q,U)$, so for any teacher-generated truth the population loss $K$ is a polynomial of degree $10$. A **teacher** is a parameter $w^0$ of the same model at embedding dimension $e_0 < e$, realized by the student at the zero-padded point $\iota(w^0)$. The **local pair** $(\lambda(w^*), m(w^*))$ at a zero $w^*$ of $K$ — local learning coefficient and multiplicity — consists of the exponents in Watanabe's local free-energy expansion $\lambda \log n - (m-1)\log\log n$ [W09]; the precise definitions, via the poles of a zeta integral, are in [MAIS-A6](../agendas/A6/).

**Problem ([MAIS-A6, Problem 5.5](../agendas/A6/MAIS-A6.tex#L452)).** For the linear-attention model with the zero truth $q = N(0, I_v)$, determine $\lambda(0)$ and $m(0)$ as functions of $(v, T, e)$. Then compute the generic pair for a teacher of embedding dimension $e_0 < e$, with Conjecture 5.3 restated for this degree-$10$ polynomial and the same padding map $\iota$.

Conjecture 5.3 of the agenda ([MAIS-O66](MAIS-O66.md)) is the statement that a generic-teacher value exists: the local pair at $\iota(w^0)$ is constant off the zero set of some nonzero real-analytic function of the teacher. For the softmax model the corresponding zero-truth case is worked out in the agenda by reduction to reduced-rank regression; the polynomial setting here replaces that reduction with a direct singularity analysis. Tensor-decomposition bounds adjacent to this model exist, due to Yoshida and Watanabe [[YW23]](https://arxiv.org/abs/2303.05731), but do not supply the pairs. Setup and background are in [MAIS-A6](../agendas/A6/).

## References

- [[AW05]](../references/AW05.md) M. Aoyagi and S. Watanabe, *Stochastic complexities of reduced rank regression in Bayesian estimation*, Neural Networks 18 (2005), no. 7, 924–933.
- [[W09]](../references/W09.md) S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- [YW23] N. Yoshida and S. Watanabe, *Upper bound of real log canonical threshold of tensor decomposition and its application to Bayesian inference*, 2023. [arXiv:2303.05731](https://arxiv.org/abs/2303.05731)

*Related: [MAIS-O67](MAIS-O67.md) (the softmax version of the same teacher-student question) · [MAIS-O66](MAIS-O66.md) (generic constancy over teachers) · [MAIS-O70](MAIS-O70.md) (the reduced-rank template this model is modeled on).*
