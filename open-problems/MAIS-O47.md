# Uniqueness of ReLU toy-model minimizers up to symmetry

*Open problem MAIS-O47 · posed in [MAIS-A4](../agendas/A4/) as [Problem 5.7](../agendas/A4/MAIS-A4.tex#L424) · Status: open.*

*Tags: interpretability · training for interpretability · superposition · universality of circuits · optimization · convex geometry. Difficulty: ★★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

If two independent training runs find genuinely different optima, two auditors will report different features. Stability of interpretation is thus a uniqueness question: is the optimum a single orbit of the problem's symmetries?

The arena is the ReLU toy model of Elhage et al. [[EHOS+22]](../references/EHOS+22.md): data $x\in\mathbb{R}^m$ with independent coordinates, each zero with probability $S$ and otherwise uniform on $[0,1]$; network $f_{W,b}(x)=\mathrm{ReLU}(W^{\top}Wx+b)$ with $W\in\mathbb{R}^{n\times m}$, $n<m$, whose columns $W_1,\dots,W_m\in\mathbb{R}^n$ are the directions in activation space where the features are stored; task loss $L=\mathbb{E}\ \Vert x-f_{W,b}(x)\Vert _2^2$; interference penalty $R(W)=\sum_{i\neq j}\langle W_i,W_j\rangle^2$. The symmetry group is $G=O(n)\times\Sigma_m$, acting by $W\mapsto QWP^{-1}$, $b\mapsto Pb$ for $Q$ orthogonal and $P$ a permutation of the features (with their biases); $L$, $R$, and the coherence $\mu$ (the worst-case normalized interference between distinct stored features; defined precisely in [MAIS-A4](../agendas/A4/)) are all $G$-invariant. At $(m,n)=(5,2)$ and high sparsity the observed optimum is the regular pentagon: five unit-ish columns at angles $72^\circ$ apart in the plane. No polytope phase of this model has ever been certified as a global optimum.

**Problem ([MAIS-A4, Problem 5.7](../agendas/A4/MAIS-A4.tex#L424)).** Call the objective $L+\lambda R$ **identifiable at** $(m,n,S,\lambda)$ if its $\operatorname{argmin}$ is nonempty and consists of a single $G$-orbit.

1. Decide identifiability for $(m,n)=(5,2)$, $\lambda=0$, at high sparsity: prove there exists $S_0<1$ such that for all $S\in(S_0,1)$ the $\operatorname{argmin}$ is a single $G$-orbit — concretely, the regular pentagon with its optimal norms and biases — or prove that no such $S_0$ exists.
2. Exhibit $(m,n,S,\lambda)$ with $\lambda>0$ such that $L+\lambda R$ is identifiable while $L$ is not, or prove that regularization by $R$ never creates identifiability where it was absent.

In words: part (1) asks whether, for all sparsities close enough to $1$, every global minimizer of the unregularized $(5,2)$ model is the regular pentagon up to rotation and relabeling; part (2) asks whether an interference penalty can break a tie between inequivalent optimal geometries, which is the precise form of "regularize for stability." The nearest prior result, by Ivanov et al. [[IORP+26]](../references/IORP+26.md), proves spectral and tight-frame structure for the optimal geometry conditional on an empirical hypothesis called capacity saturation; it proves neither that global minimizers satisfy that hypothesis nor that the pentagon is optimal. See [MAIS-A4](../agendas/A4/) for the surrounding frontier program.

## References

- [[EHOS+22]](../references/EHOS+22.md) N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- [[IORP+26]](../references/IORP+26.md) G. Ivanov, N. Oozeer, S. Raval, T. Pejovic, S. Upadhyay, and A. Abdullah, *Spectral superposition: a theory of feature geometry*. [arXiv:2602.02224](https://arxiv.org/abs/2602.02224)

*Related: [MAIS-O40](MAIS-O40.md) (the pentagon as global minimizer of a related ReLU autoencoder) · [MAIS-O42](MAIS-O42.md) (pentagon optimality for a pure packing energy, a starter toward part 1) · [MAIS-O4](MAIS-O4.md) (the coherence-constrained frontier whose $(5,2)$ case this would anchor) · [MAIS-O50](MAIS-O50.md) (when minimization does not decide, what does gradient flow select?).*
