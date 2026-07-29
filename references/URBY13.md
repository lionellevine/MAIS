# Geometry of the faithfulness assumption in causal inference

*Summary [URBY13] · C. Uhler, G. Raskutti, P. Bühlmann, and B. Yu, Ann. Statist. 41 (2013), 436–463 · [arXiv:1207.0547](https://arxiv.org/abs/1207.0547).*

*Tags: world-model discovery · causal inference · algebraic geometry · probability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Causal discovery algorithms assume faithfulness — every conditional independence in the data reflects the graph — and justify it by noting that unfaithful distributions form a measure-zero set. But finite samples require *strong* faithfulness: the relevant partial correlations must be bounded away from zero by a margin $\lambda$. This paper computes the geometry of that margin and finds that the set of distributions violating it has positive measure, which for many graph classes tends to $1$ as the graph grows. Replacing "almost every" by "every, given a margin" can silently exclude most of parameter space.

## Setting

The model is a linear Gaussian structural equation model on a DAG $G$: each variable is a linear combination of its parents plus independent standard Gaussian noise, with edge weights drawn from $[-1,1]$. A distribution is **faithful** to $G$ if its conditional independences are exactly those entailed by d-separation; it is **$\lambda$-strong-faithful** if moreover every partial correlation not forced to vanish by d-separation exceeds $\lambda$ in absolute value. Zhang and Spirtes had shown strong faithfulness suffices for uniform consistency of constraint-based algorithms such as PC; the question here is how much of parameter space the assumption costs. A weaker **restricted** strong faithfulness (adjacency- and orientation-faithfulness only) is also analyzed, since it is what the PC algorithm actually needs.

## Main results

Each partial correlation is, up to sign and normalization, a polynomial in the edge weights, so the unfaithful distributions form an arrangement of real algebraic hypersurfaces in the cube of parameters, and the not-$\lambda$-strong-faithful distributions form a thickened neighborhood of that arrangement. The paper bounds its Lebesgue measure in both directions.

1. **Upper bounds.** For any DAG, the measure of the not-strong-faithful set is bounded by a sum over the conditional-independence constraints, each term controlled by the degree of the corresponding partial-correlation polynomial — so the excluded volume shrinks as $\lambda\to 0$ at a rate governed by the number and algebraic complexity of the constraints.
2. **Lower bounds.** For explicit families — paths and trees, cycles, and bipartite graphs $K_{2,p-2}$ — the measure of the not-strong-faithful set admits lower bounds that tend to $1$ exponentially fast in the number of nodes $p$ for any fixed $\lambda>0$. Even modest graphs and tiny margins exclude a substantial fraction of parameter space, and the restricted version, while weaker, exhibits the same growth.
3. **Consequence for algorithms.** Since uniform consistency of the PC algorithm requires (restricted) strong faithfulness, these bounds are fundamental limitations for PC and, plausibly, for any method based on partial correlation testing in the Gaussian case.

## Proof method

Real algebraic geometry applied to statistics. The unfaithful locus is the zero set of the partial-correlation polynomials, whose degrees are bounded by a trek (collider-free path) expansion of conditional covariances; upper bounds on the volume of the $\lambda$-neighborhood then follow from Crofton-formula bounds on the surface area of a real algebraic hypersurface of known degree, together with Łojasiewicz-type control of how fast the polynomials can stay small away from their zero sets. The lower bounds come from exact computation in the structured families, where the partial correlations factor into products along paths and the excluded region can be integrated directly. Simulations confirm that the excluded fraction is large already at small $p$ and $\lambda$.

## Why it matters for AI safety

Identifiability theorems in causal discovery are usually generic — true for almost every parameter value — but finite data need margins, and this paper is the first to compute what a margin costs: the models excluded by strong faithfulness form a set of positive measure that can approach everything as the graph grows. The lesson generalizes to any attempt to read a world model from finite observations of behavior, which must likewise replace "almost every" by explicit checkable margins to get sample-complexity guarantees: measure what your margins exclude, because the answer can be almost everything. The margin class of [MAIS-A2](../agendas/A2/) is designed with that caution in view, and its excluded-set bound ([MAIS-O24](../open-problems/MAIS-O24.md), part 3) is posed with this paper aimed directly at it.

## Cited by

- [MAIS-A2](../agendas/A2/) — the caution that "almost every" and "every, given margins" can be far apart, informing the design of its margin class.
- Problems [MAIS-O23](../open-problems/MAIS-O23.md) · [MAIS-O24](../open-problems/MAIS-O24.md)
