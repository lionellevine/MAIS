# The regularized phase diagram of the smallest model

*Open problem MAIS-O51 · posed in [MAIS-A4](../agendas/A4/) as [Example 6.1](../agendas/A4/MAIS-A4.tex#L505) · Status: open.*

*Tags: interpretability · training for interpretability · superposition · optimization · probability. Difficulty: ★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Two features, one dimension: the smallest network that must choose what to forget. Elhage et al. [[EHOS+22]](https://arxiv.org/abs/2209.10652) solved the unregularized case; nobody has analyzed it with the interference penalty that "training for interpretability" would actually add.

The data has two independent coordinates, each zero with probability $S\in(0,1)$ and otherwise uniform on $[0,1]$; feature 2 carries an importance weight $I>0$ multiplying its share of the loss. The network stores both features in one dimension via weights $(w_1,w_2)$ and reconstructs through a ReLU; in the toy model's notation this is $m=2$ features in $n=1$ hidden dimension. Elhage et al. [[EHOS+22]](https://arxiv.org/abs/2209.10652) treat the unpenalized problem and find three phases with closed-form losses and a first-order transition: ignore the weak feature; dedicate the dimension to it; or store the pair in antipodal superposition, $w_2=-w_1$. The open case adds the interference penalty $R=2w_1^2w_2^2$, twice the squared inner product of the two stored directions, with coefficient $\lambda>0$.

**Problem ([MAIS-A4, Example 6.1](../agendas/A4/MAIS-A4.tex#L505)).** Take $m=2$, $n=1$, importance weights $(1,I)$: the loss is

$$L(w_1,w_2,b) = \mathbb{E}\Bigl[\bigl(x_1-\mathrm{ReLU}(w_1^2x_1+w_1w_2x_2+b_1)\bigr)^2 + I\bigl(x_2-\mathrm{ReLU}(w_1w_2x_1+w_2^2x_2+b_2)\bigr)^2\Bigr]$$

with $(w_1,w_2)\in\mathbb{R}^2$, biases $(b_1,b_2)\in\mathbb{R}^2$, and $R = 2w_1^2w_2^2$. Determine exactly the global-minimizer phase diagram of $L+\lambda R$ in the octant of parameters $(I,S,\lambda)$, including the critical surface $\lambda_c(I,S)$ above which the antipodal phase disappears.

In words: partition the parameter octant into the regions where each of the three geometries (drop, dedicate, antipodal) is the global minimizer, and find the exact surface where the penalty kills superposition. Everything reduces to one-dimensional integrals of piecewise polynomials; the work is a careful case analysis. The point is not *that* the penalty reduces interference — scalarization gives that for free (for any functions $L$ and $R$ whatsoever, a minimizer of $L+\lambda R$ has $R$ no larger, and $L$ no smaller, than a minimizer of $L$ alone) — but *which phase* it selects, at what task cost, with the constants. See [MAIS-A4](../agendas/A4/) for the scalarization proposition and the unregularized phase story.

## References

- [EHOS+22] N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- [CLMWM23] Z. Chen, E. Lau, J. Mendel, S. Wei, and D. Murfet, *Dynamical versus Bayesian phase transitions in a toy model of superposition*. [arXiv:2310.06301](https://arxiv.org/abs/2310.06301)
- [SSJBS22] A. Scherlis, K. Sachan, A. Jermyn, J. Benton, and B. Shlegeris, *Polysemanticity and capacity in neural networks*. [arXiv:2210.01892](https://arxiv.org/abs/2210.01892)

*Related: [MAIS-O4](MAIS-O4.md) (the full interference–performance frontier this is the smallest case of) · [MAIS-O50](MAIS-O50.md) (gradient flow on the same $(2,1)$ model) · [MAIS-O44](MAIS-O44.md) (average-vs-worst-case interference at larger sizes).*
