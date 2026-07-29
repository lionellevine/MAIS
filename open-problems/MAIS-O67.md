# Learning coefficients of one-head softmax attention

*Open problem MAIS-O67 · posed in [MAIS-A6](../agendas/A6/) as [Problem 5.4](../agendas/A6/MAIS-A6.tex#L442) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · algebraic geometry · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Exact learning coefficients are known for linear networks of every depth, but for attention — the layer the transformer is built from — not a single teacher-student value has been computed. This problem asks for the first one: the attention analog of the Aoyagi–Watanabe formula [AW05], in which the coefficient of reduced-rank regression depends on the truth only through its rank. The safety stake is calibration: developmental interpretability estimates these coefficients by sampling to detect phase transitions as transformers train, and such estimates already track the specialization of attention heads [WHVFM24], but there is no exact attention value to test the estimators against.

The model is the one-head attention network of [MAIS-A6](../agendas/A6/): vocabulary size $v$, context length $T$, embedding dimension $e$, and parameter $w = (E,Q,U)$ with $E \in \mathbb{R}^{v \times e}$, $Q \in \mathbb{R}^{e \times e}$, $U \in \mathbb{R}^{e \times v}$, row $E_a$ being the embedding of token $a$; on a string $x \in [v]^T$ of tokens ($[v] = \lbrace 1,\dots,v\rbrace $) it forms scores $s_t(x) = E_{x_T} Q E_{x_t}^{\top}$, attention weights $\alpha(x) = \mathrm{softmax}(s(x))$, logits $\ell(x) = \sum_t \alpha_t(x) E_{x_t} U$, and the output law $\mathrm{softmax}(\ell(x))$ on $[v]$, with inputs uniform on $[v]^T$. A **teacher** is a parameter $w^0$ of the same model at smaller embedding dimension $e_0 < e$; its output law is the truth, realized by the student at the zero-padded point $\iota(w^0)$. The student's **population loss** $K(w)$ is the Kullback–Leibler divergence from the truth's output law to the student's, averaged over the uniform input. The **local pair** at a zero $w^*$ of $K$ — local learning coefficient $\lambda(w^*)$ and multiplicity $m(w^*)$ — measures the volume of near-fits, $\mathrm{vol}\lbrace K \le \varepsilon\rbrace \asymp \varepsilon^{\lambda}(\log(1/\varepsilon))^{m-1}$ near $w^*$, and replaces the parameter count in Watanabe's expansion of the Bayesian free energy [W09]; the exact definitions, via the poles of a local zeta integral, are in [MAIS-A6](../agendas/A6/). Conjecture 5.3 of the agenda ([MAIS-O66](MAIS-O66.md)) posits that the local pair $(\lambda(\iota(w^0)), m(\iota(w^0)))$ at the padded teacher is constant off a proper analytic subset of teachers.

**Problem ([MAIS-A6, Problem 5.4](../agendas/A6/MAIS-A6.tex#L442)).** Assuming or proving Conjecture 5.3, compute the generic value $\Lambda(v, T, e, e_0)$ and its multiplicity.

The uniform truth is a solved base case and a model answer: there the attention weights drop out, and the germ is that of reduced-rank regression — the two-layer linear model $y = BAx + \text{noise}$ — at output, input, inner, and rank dimensions $(M,N,H,r) = (v, v-1, e, 0)$, the $v-1$ because a softmax output law depends only on the centered logits. The Aoyagi–Watanabe theorem [AW05] then gives the pair in closed form, independent of $T$. A starter sized for one paper: take $(v,T,e,e_0) = (2,2,2,1)$, prove generic constancy in this four-input model, and compute the generic local pair at the padded teacher. The worked base case and what is known for attention appear in [MAIS-A6](../agendas/A6/).

## References

- [[AW05]](../references/AW05.md) M. Aoyagi and S. Watanabe, *Stochastic complexities of reduced rank regression in Bayesian estimation*, Neural Networks 18 (2005), no. 7, 924–933.
- [[W09]](../references/W09.md) S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- [WHVFM24] G. Wang, J. Hoogland, S. van Wingerden, Z. Furman, and D. Murfet, *Differentiation and specialization of attention heads via the refined local learning coefficient*, 2024. [arXiv:2410.02984](https://arxiv.org/abs/2410.02984)

*Related: [MAIS-O66](MAIS-O66.md) (the generic-constancy hypothesis this problem rests on) · [MAIS-O68](MAIS-O68.md) (linear attention, a degree-10 polynomial loss likelier to fall first) · [MAIS-O70](MAIS-O70.md) (local pairs on the reduced-rank template).*
