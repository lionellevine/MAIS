# Exact cost of weight sparsity in the ReLU toy model

*Open problem MAIS-O49 · posed in [MAIS-A4](../agendas/A4/MAIS-A4.pdf) as [Problem 5.9](../agendas/A4/MAIS-A4.tex#L459) · Status: open.*

*Safety: interpretability — training for interpretability · mechanistic interpretability · superposition. Mathematics: optimization · probability · combinatorics. Difficulty: ★★ project.*

A network in which each feature is wired to a single neuron is legible by inspection: every activation coordinate is an explicit signed combination of named features. Gao et al. found empirically that training transformers with almost all weights zeroed buys interpretable circuits at a measured capability cost. In the toy model, that cost can be asked for exactly.

The model: data $x\in\mathbb{R}^m$ with independent coordinates, each zero with probability $S$ and otherwise uniform on $[0,1]$; network $f_{W,b}(x)=\mathrm{ReLU}(W^{\top}Wx+b)$ with $W\in\mathbb{R}^{n\times m}$ (columns $W_1,\dots,W_m$), $n<m$; loss $L_{m,n,S}=\mathbb{E}\ \Vert x-f_{W,b}(x)\Vert _2^2$. Write $v(S)=(1-S)(1+3S)/12$ for the cost of dropping one feature. The agenda proves two calibration points among column-1-sparse matrices (each column of $W$ has at most one nonzero entry): storing $n$ features orthogonally and dropping the rest costs $(m-n)\ v(S)$, while storing $2n$ features in antipodal pairs costs $\tfrac{n(1-S)^2}{3}+(m-2n)\ v(S)$, which is strictly cheaper when $S>3/7$. Whether anything beats these two is open.

**Problem ([MAIS-A4, Problem 5.9](../agendas/A4/MAIS-A4.tex#L459)).** For $m\ge 2n\ge2$ and $S\in(0,1)$, determine

$$Q_{m,n,S} \ =\  \inf\bigl\lbrace \ L_{m,n,S}(W,b)\ :\ \Vert W_i\Vert _0\le 1 \text{ for all } i\ \bigr\rbrace $$

exactly; here $\Vert v\Vert _0$ denotes the number of nonzero entries of $v$, so the constraint is column-1-sparsity. (Conjecturally $Q_{m,n,S}=\min\bigl\lbrace (m-n)\ v(S),\ \tfrac{n(1-S)^2}{3}+(m-2n)\ v(S)\bigr\rbrace $, the orthogonal value winning for $S<3/7$ and the antipodal one for $S>3/7$, with equality at $S=3/7$; the content is to rule out three or more same-axis features aided by biases.) More generally, determine and compare the recovery-constrained frontiers $Q^{\mathrm{rec}}(k_0)$ and $P^{\mathrm{rec}}(c)$: with $\mathrm{REC}_S(W;d,\alpha,\varepsilon)$ the agenda's dictionary-recovery predicate (every global minimizer of the $\ell^1$ sparse-coding objective on the activations $Wx$ contains, for each stored direction, an atom whose normalized inner product with it is at least $1-\varepsilon$), with $\mu(W)$ the coherence (the largest $|\langle W_i,W_j\rangle|/(\Vert W_i\Vert _2\Vert W_j\Vert _2)$ over distinct nonzero columns), and fixed $(d,\alpha,\varepsilon)$,

$$Q^{\mathrm{rec}}(k_0)=\inf\lbrace L(W,b):\Vert W_i\Vert _0\le k_0\ \text{for all } i,\ \mathrm{REC}_S(W;d,\alpha,\varepsilon)=1\rbrace ,\qquad P^{\mathrm{rec}}(c)=\inf\lbrace L(W,b):\mu(W)\le c,\ \mathrm{REC}_S(W;d,\alpha,\varepsilon)=1\rbrace ,$$

compared pointwise as the wiring budget $k_0$ and coherence budget $c$ vary.

In words: among networks whose every feature is wired to one neuron, is the best strategy always either "orthogonal storage plus dropping" or "antipodal pairs plus dropping," with the switch at sparsity $3/7$? The final comparison asks which legibility currency — sparse wiring or low coherence — buys recoverable features more cheaply. The calibration proofs and the recovery predicate are in [MAIS-A4](../agendas/A4/MAIS-A4.pdf).

*Related: [MAIS-O4](MAIS-O4.md) (the coherence-constrained frontier, the other currency) · [MAIS-O48](MAIS-O48.md) (alignment constraints in the privileged-basis model) · [MAIS-O45](MAIS-O45.md) (the recovery predicate applied to trained dictionaries).*
