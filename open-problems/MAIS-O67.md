# Learning coefficients of one-head softmax attention

*Open problem MAIS-O67 · posed in [MAIS-A6](../agendas/A6/) as [Problem 5.4](../agendas/A6/MAIS-A6.tex#L441) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · algebraic geometry · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Exact learning coefficients are known for linear networks of every depth, but for attention — the layer the transformer is built from — not a single teacher-student value has been computed. This problem asks for the first one: the attention analog of the Aoyagi–Watanabe formula, in which the coefficient of reduced-rank regression depends on the truth only through its rank.

The model is the one-head attention network of [MAIS-A6](../agendas/A6/): vocabulary size $v$, context length $T$, embedding dimension $e$, and parameter $w = (E,Q,U)$ with $E \in \mathbb{R}^{v \times e}$, $Q \in \mathbb{R}^{e \times e}$, $U \in \mathbb{R}^{e \times v}$, row $E_a$ being the embedding of token $a$; on a string $x \in [v]^T$ of tokens ($[v] = \lbrace 1,\dots,v\rbrace $) it forms scores $s_t(x) = E_{x_T} Q E_{x_t}^{\top}$, attention weights $\alpha(x) = \mathrm{softmax}(s(x))$, logits $\ell(x) = \sum_t \alpha_t(x) E_{x_t} U$, and the output law $\mathrm{softmax}(\ell(x))$ on $[v]$, with inputs uniform on $[v]^T$. A **teacher** is a parameter $w^0$ of the same model at smaller embedding dimension $e_0 < e$; its output law is the truth, realized by the student at the zero-padded point $\iota(w^0)$. Conjecture 5.3 of the agenda ([MAIS-O66](MAIS-O66.md)) posits that the local pair $(\lambda(\iota(w^0)), m(\iota(w^0)))$ — local learning coefficient and multiplicity of the student's population loss at the padded teacher — is constant off a proper analytic subset of teachers.

**Problem ([MAIS-A6, Problem 5.4](../agendas/A6/MAIS-A6.tex#L441)).** Assuming or proving Conjecture 5.3, compute the generic value $\Lambda(v, T, e, e_0)$ and its multiplicity.

The uniform truth is a solved base case and a model answer: there the attention weights drop out, the germ is reduced-rank regression with $(M,N,H,r) = (v, v-1, e, 0)$, and the Aoyagi–Watanabe theorem gives the pair in closed form, independent of $T$. A starter sized for one paper: take $(v,T,e,e_0) = (2,2,2,1)$, prove generic constancy in this four-input model, and compute the generic local pair at the padded teacher. The worked base case and what is known for attention appear in [MAIS-A6](../agendas/A6/).

*Related: [MAIS-O66](MAIS-O66.md) (the generic-constancy hypothesis this problem rests on) · [MAIS-O68](MAIS-O68.md) (linear attention, a degree-10 polynomial loss likelier to fall first) · [MAIS-O70](MAIS-O70.md) (local pairs on the reduced-rank template).*
