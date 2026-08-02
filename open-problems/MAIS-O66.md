# Generic constancy of learning coefficients over attention teachers

*Open problem MAIS-O66 · posed in [MAIS-A6](../agendas/A6/) as [Conjecture 5.3](../agendas/A6/MAIS-A6.tex#L438) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · algebraic geometry · statistics. Difficulty: ★★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The **local learning coefficient**, in the pointwise sense of Lau, Furman, Wang, Murfet, and Wei [[LFWMW23]](../references/LFWMW23.md), is the complexity measure that developmental interpretability estimates inside trained networks to watch structure form during training. In Watanabe's singular learning theory [W09] it replaces the parameter count: for a localized prior it sets the complexity penalty in the Bayes free energy and the $\lambda/n$ decay of the generalization error. Exact values, against which the estimators can be calibrated, are known only for a short list of classical models.

For reduced-rank regression, the learning coefficient depends on the truth only through one integer, the rank — which is why a closed form exists at all. For a one-head attention model, the analog of "the truth has rank $r$" is "the truth is a smaller transformer," and the honest first question is whether a generic-teacher value of the learning coefficient exists at all.

The model: fix a vocabulary size $v \ge 2$, context length $T \ge 2$, and embedding dimension $e \ge 1$. An input is a string $x \in [v]^T$ of tokens, where $[v] = \lbrace 1, \dots, v\rbrace $; the parameter is $w = (E, Q, U)$ with $E \in \mathbb{R}^{v \times e}$, $Q \in \mathbb{R}^{e \times e}$, $U \in \mathbb{R}^{e \times v}$, so $d = ve + e^2 + ev$; row $E_a \in \mathbb{R}^e$ is the embedding of token $a$. The model computes scores $s_t(x) = E_{x_T} Q E_{x_t}^{\top}$, attention weights $\alpha(x) = \mathrm{softmax}(s_1(x),\dots,s_T(x))$, logits $\ell(x) = \sum_{t=1}^T \alpha_t(x)\ E_{x_t} U$, and outputs the law $\mathrm{softmax}(\ell(x))$ on $[v]$; inputs are uniform on $[v]^T$. For $1 \le e_0 < e$, a **teacher** $w^0 \in \mathbb{R}^{d_0}$ ($d_0 = ve_0 + e_0^2 + e_0 v$) is a parameter of the dimension-$e_0$ model; its output law is the truth, realized by the student at the zero-padded point $\iota(w^0)$, where $\iota$ places $E^0, Q^0, U^0$ in the leading blocks. The student's **population loss** $K$ is the input-averaged Kullback–Leibler divergence from the teacher's output law; it is real-analytic and vanishes at $\iota(w^0)$. Write $\lambda(\iota(w^0))$, $m(\iota(w^0))$ for the local learning coefficient and **multiplicity** of $K$ there — a positive rational and a positive integer measuring how degenerately $K$ vanishes; the exact zeta-function definitions are in [MAIS-A6](../agendas/A6/).

**Conjecture ([MAIS-A6, Conjecture 5.3](../agendas/A6/MAIS-A6.tex#L438)).** For each $(v, T, e, e_0)$ with $1 \le e_0 < e$ there is a real-analytic function $h \colon \mathbb{R}^{d_0} \to \mathbb{R}$, not identically zero, such that $\bigl(\lambda(\iota(w^0)),\  m(\iota(w^0))\bigr)$ is constant on $\lbrace w^0 : h(w^0) \neq 0\rbrace $.

In words: away from a proper analytic subset of teachers, the local pair takes a single value — the precondition for any closed-form theory of attention learning coefficients. The base case is worked out in the agenda: for the uniform truth, the attention weights drop out of the singularity calculation and the germ is reduced-rank regression at zero truth, with the formula of Aoyagi and Watanabe [AW05] giving the pair explicitly. The smallest open instance is $(v,T,e,e_0) = (2,2,2,1)$, a four-input model. The worked example and conventions are in [MAIS-A6](../agendas/A6/).

## References

- [[AW05]](../references/AW05.md) M. Aoyagi and S. Watanabe, *Stochastic complexities of reduced rank regression in Bayesian estimation*, Neural Networks 18 (2005), no. 7, 924–933.
- [[W09]](../references/W09.md) S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- [[LFWMW23]](../references/LFWMW23.md) E. Lau, Z. Furman, G. Wang, D. Murfet, and S. Wei, *The local learning coefficient: a singularity-aware complexity measure*, 2023. [arXiv:2308.12108](https://arxiv.org/abs/2308.12108)

*Related: [MAIS-O67](MAIS-O67.md) (compute the generic value this conjecture posits) · [MAIS-O68](MAIS-O68.md) (the polynomial linear-attention variant) · [MAIS-O70](MAIS-O70.md) (the local strata of the reduced-rank template).*
