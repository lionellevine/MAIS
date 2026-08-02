# Toy models of superposition

*Summary [EHOS+22] · N. Elhage, T. Hume, C. Olsson, N. Schiefer, et al., Transformer Circuits Thread, 2022 · [arXiv:2209.10652](https://arxiv.org/abs/2209.10652).*

*Tags: interpretability · mechanistic interpretability · superposition · optimization · convex geometry · probability.*

*Summarized by: Claude Fable 5 directed by Lionel Levine.*

**TL;DR.** Small ReLU networks trained to reconstruct sparse synthetic feature vectors will represent *more features than they have dimensions*, storing them along nearly orthogonal directions and tolerating the interference because sparsity makes collisions rare — the phenomenon the paper names **superposition**. Whether a feature is dropped, stored in superposition, or given a dedicated dimension is governed by a first-order phase change with feature importance and sparsity as control parameters, and superposed features organize themselves into uniform polytopes: antipodal pairs, triangles, pentagons, tetrahedra.

## Setup and hypotheses

The input $x\in\mathbb{R}^n$ has independent coordinates ("features"), each zero with probability $S$ (the sparsity) and otherwise uniform on $[0,1]$; feature $i$ carries an importance weight $I_i$. Two autoencoders compress to $h=Wx\in\mathbb{R}^m$ with $m<n$: the **linear model** $x'=W^{\top}Wx+b$ and the **ReLU-output model** $x'=\mathrm{ReLU}(W^{\top}Wx+b)$, both trained on the importance-weighted squared error $\sum_i I_i(x_i-x'_i)^2$. The columns $W_i$ are the directions in activation space where features are stored, and the representation is in superposition when $W^{\top}W$ is not invertible — more features survive than dimensions can hold orthogonally. Two background hypotheses are articulated along the way: *linear representation* (features correspond to directions in activation space) and *privileged basis* (nonlinearities break rotational symmetry, making individual neurons candidates for meaning).

## Main results

1. **Linear versus ReLU.** The linear model learns the top-$m$ principal components — the classical optimum — and never superposes. The ReLU model matches it when features are dense, but develops superposition as $S\to 1$.
2. **A Thomson problem in disguise.** Decomposing the loss by which features are active, the one-active-feature term reduces (for unit-norm features and zero bias) to a generalized Thomson problem: mutually repelling points on a sphere, with a benefit term for representing each feature and an interference penalty $\sum_{i\neq j}(W_i\cdot W_j)^2$. The ReLU makes negative interference free in this one-sparse case.
3. **Phase change.** A genuine first-order phase change — confirmed analytically by the crossover of closed-form loss curves for competing configurations — separates a feature's three possible fates: not learned, stored in superposition, given a dedicated dimension.
4. **Polytope geometry.** The aggregate "dimensions per feature" $m/\lVert W\rVert_F^2$ sticks at rational plateaus as sparsity varies, notably $\tfrac12$ (antipodal pairs), and a per-feature dimensionality clusters at $\tfrac34$ (tetrahedron), $\tfrac23$ (triangle), $\tfrac12$ (antipodal pair), $\tfrac25$ (pentagon), $\tfrac38$ (square antiprism) — all uniform-polytope solutions of Thomson type, often tegum products of low-dimensional factors.
5. **Correlations.** Correlated features prefer orthogonal or locally aligned arrangements and collapse to a shared principal component when crowded; anti-correlated features prefer antipodal placement.
6. **Adversarial vulnerability.** Sensitivity to $L_2$ adversarial perturbations more than triples as superposition forms, tracking the number of features per dimension.

## Proof method

A mix of empirical training (many random seeds, lowest loss retained) and analytic toy-models-of-the-toy-model: closed-form losses for candidate weight geometries, compared to locate the phase boundaries. An appendix makes the connection to compressed sensing rigorous: recovering $k$-sparse inputs requires $m=\Omega(k\log(n/k))$ hidden dimensions, which translates into an upper bound on how much superposition is possible — linear in $m$, modulated by sparsity.

## Why it matters for AI safety

The superposition hypothesis is the working ontology of mechanistic interpretability. If a network's concepts are nearly orthogonal directions activated sparsely, then interpreting the network means recovering those directions — which is why sparse autoencoders ($\ell^1$-penalized dictionary learners) became the field's tool of choice, and why their failure modes matter. The paper frames "solving superposition" as the obstruction standing between current practice and enumerative safety arguments of the form "this model contains no deception circuit": individual neurons are polysemantic precisely because features outnumber dimensions. And it distills the phenomenon into a model small enough for theorems — compressed sensing, frame theory, the Thomson problem — while almost none of its striking observations (the pentagon, the phase diagram, the sticky plateaus) has yet been proved. Turning those observations into theorems is the business of [MAIS-A3](../agendas/A3/) (when can the stored dictionary be provably recovered?) and [MAIS-A4](../agendas/A4/) (can training buy legible geometry, and at what price?).

## Cited by

- [MAIS-A3](../agendas/A3/) — source of the superposition hypothesis whose generative model A3 formalizes, and of the polytope geometry behind its closing problem.
- [MAIS-A4](../agendas/A4/) — the ReLU toy model is A4's arena: the interference–performance frontier and the phase diagram under regularization are posed there as exact optimization problems.
- Problems [MAIS-O3](../open-problems/MAIS-O3.md) · [MAIS-O4](../open-problems/MAIS-O4.md) · [MAIS-O40](../open-problems/MAIS-O40.md) · [MAIS-O42](../open-problems/MAIS-O42.md) · [MAIS-O43](../open-problems/MAIS-O43.md) · [MAIS-O44](../open-problems/MAIS-O44.md) · [MAIS-O45](../open-problems/MAIS-O45.md) · [MAIS-O46](../open-problems/MAIS-O46.md) · [MAIS-O47](../open-problems/MAIS-O47.md) · [MAIS-O48](../open-problems/MAIS-O48.md) · [MAIS-O49](../open-problems/MAIS-O49.md) · [MAIS-O50](../open-problems/MAIS-O50.md) · [MAIS-O51](../open-problems/MAIS-O51.md)
