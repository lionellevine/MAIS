# Does penalizing interference make features recoverable by dictionary learning?

*Open problem MAIS-O45 · posed in [MAIS-A4](../agendas/A4/) as [Problem 5.5](../agendas/A4/MAIS-A4.tex#L395) · Status: open.*

*Tags: interpretability · training for interpretability · sparse autoencoders · superposition · mechanistic interpretability · statistics · optimization · probability. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Coherence, the worst-case overlap between stored features, is a property of the weights; the post-hoc interpreter never sees the weights. She sees only activations, and runs a dictionary-learning estimator on them. Does training with an interference penalty actually help her?

The setting is the ReLU toy model of Elhage et al. [[EHOS+22]](https://arxiv.org/abs/2209.10652): $x\in\mathbb{R}^m$ has independent coordinates, each zero with probability $S$ and otherwise uniform on $[0,1]$; the network $f_{W,b}(x)=\mathrm{ReLU}(W^{\top}Wx+b)$, $W\in\mathbb{R}^{n\times m}$ with $n<m$, has task loss $L=\mathbb{E}\ \Vert x-f_{W,b}(x)\Vert _2^2$, and $R(W)=\sum_{i\neq j}\langle W_i,W_j\rangle^2$ is the interference penalty, the smooth average-case counterpart of the worst-case coherence. The interpreter is handed the activations $h=Wx$ and fits a dictionary $D\in\mathbb{R}^{n\times d}$, columns constrained to $\Vert D_j\Vert _2\le1$, minimizing the sparse-coding objective $J_{W,S,\alpha}(D)=\mathbb{E}_x \min_{a\in\mathbb{R}^d_{\ge0}} \bigl(\Vert Wx-Da\Vert _2^2+\alpha\Vert a\Vert _1\bigr)$ — a sparse autoencoder with the learned encoder replaced by exact minimization. Say $D$ **$\varepsilon$-recovers** $W$ if some injective map $\pi$ sends each nonzero column $i$ of $W$ to a nonzero column of $D$ with $\langle\widehat W_i,\widehat D_{\pi(i)}\rangle\ge1-\varepsilon$ (hats normalize columns to unit length), and write $\mathrm{REC}_S(W;d,\alpha,\varepsilon)=1$ if every global minimizer of $J_{W,S,\alpha}$ $\varepsilon$-recovers $W$.

**Problem ([MAIS-A4, Problem 5.5](../agendas/A4/MAIS-A4.tex#L395)).**

1. (*Antipodal warm-up.*) Let $(m,n)=(4,2)$ and let $W^\ast $ be the antipodal configuration, with columns $e_1,-e_1,e_2,-e_2$. Determine, for each $S\in(0,1)$, the set of triples $(d,\alpha,\varepsilon)$, with $d\ge4$, $\alpha>0$, and $\varepsilon\in(0,\tfrac12)$, for which $\mathrm{REC}_S(W^\ast ;d,\alpha,\varepsilon)=1$.
2. (*Transfer.*) Exhibit $(m,n,S,\lambda)$ and $(d,\alpha,\varepsilon)$ with $\varepsilon<\tfrac12$ such that both $\operatorname{argmin}(L+\lambda R)$ and $\operatorname{argmin}L$ are nonempty, every $(W_\lambda,b_\lambda)\in\operatorname{argmin}(L+\lambda R)$ satisfies $\mathrm{REC}_S(W_\lambda;d,\alpha,\varepsilon)=1$, and some $(W_0,b_0)\in\operatorname{argmin} L$ satisfies $\mathrm{REC}_S(W_0;d,\alpha,\varepsilon)=0$. Or prove no such tuple exists.

Part (1) asks, in the lowest dimension where the question makes sense, whether the standard estimator at its global optimum splits each axis into two signed atoms: the activation distribution is just $(x_1-x_2,\ x_3-x_4)$ with sparse uniform coordinates, all the probability explicit. Even this is unproved; the closest theory, due to Cui, Zhang, Wang, and Wang [[CZWW25]](https://arxiv.org/abs/2506.15963), computes closed-form sparse-autoencoder behavior in a different asymptotic regime and finds recovery generically fails without reweighting. Part (2) asks for a genuine transfer theorem — regularized training provably recoverable, unregularized training provably not — and would require an identifiability theorem for the $\ell^1$ estimator on a structured dictionary along the way. Definitions and the surrounding program are in [MAIS-A4](../agendas/A4/).

## References

- [CZWW25] J. Cui, Q. Zhang, Y. Wang, and Y. Wang, *On the limits of sparse autoencoders: a theoretical framework and reweighted remedy*, 2025. [arXiv:2506.15963](https://arxiv.org/abs/2506.15963)
- [EHOS+22] N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread, 2022. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)

*Related: [MAIS-O46](MAIS-O46.md) (does coherence even rank recoverability?) · [MAIS-O3](MAIS-O3.md) (identifiability of the $\ell^1$ dictionary estimator itself) · [MAIS-O44](MAIS-O44.md) (the coherence-level version of transfer) · [MAIS-O43](MAIS-O43.md) (measure the recovery–merging phase diagram numerically).*
