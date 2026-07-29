# Does penalizing average interference lower worst-case coherence?

*Open problem MAIS-O44 · posed in [MAIS-A4](../agendas/A4/) as [Problem 5.4](../agendas/A4/MAIS-A4.tex#L374) · Status: open.*

*Tags: interpretability · training for interpretability · superposition · optimization · harmonic analysis · probability. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

That a regularizer reduces the penalized quantity is a two-line fact about real numbers, true for every loss and every penalty. The mathematical content of "regularize for interpretability" lies in the distance between the penalty available to gradient-based training — a smooth average — and the quantity the interpreter cares about, a max.

The arena is the ReLU toy model of Elhage et al. [[EHOS+22]](../references/EHOS+22.md): data $x\in\mathbb{R}^m$ with independent coordinates, each zero with probability $S$ and otherwise uniform on $[0,1]$; network $f_{W,b}(x)=\mathrm{ReLU}(W^{\top}Wx+b)$ with $W\in\mathbb{R}^{n\times m}$, $b\in\mathbb{R}^m$; task loss $L=L_{m,n,S}(W,b)=\mathbb{E}\ \Vert x-f_{W,b}(x)\Vert _2^2$. The **coherence** $\mu(W)=\max_{i\neq j}|\langle \widehat W_i,\widehat W_j\rangle|$ (over distinct nonzero columns, normalized) is worst-case crosstalk; the **interference** $R(W)=\sum_{i\neq j}\langle W_i,W_j\rangle^2$ is its average-case, polynomial counterpart, hence usable as a training penalty. The two need not move together: $R$ plus the fourth powers of the column norms is the frame potential of Benedetto and Fickus [BF03], whose minimizers among unit-norm systems are tight frames, and every system of $m>n$ unit vectors, tight frame or not, has $\mu$ at least the Welch bound [W74] $\sqrt{(m-n)/(n(m-1))}$. Finally, a feature is **dropped** when its column of $W$ is zero; $v(S)=(1-S)(1+3S)/12$ is the loss a network pays per dropped feature, and since at most $n$ columns can be pairwise orthogonal, the exact cost of full orthogonality is $(m-n)\ v(S)$.

**Problem ([MAIS-A4, Problem 5.4](../agendas/A4/MAIS-A4.tex#L374)).** Let $R$ be the interference above.

1. Exhibit a quadruple $(m,n,S,\lambda)$, where $m>n\ge2$, $S\in(0,1)$, and $\lambda>0$, for which the two sets of minimizers below are nonempty, every $(W,b)\in\operatorname{argmin}(L+\lambda R)$ has task loss below the orthogonality price, i.e. $L(W,b)<(m-n)\ v(S)$, and

$$\sup\bigl\lbrace \mu(W) : (W,b)\in\operatorname{argmin}(L+\lambda R)\bigr\rbrace  \ <\  \inf\bigl\lbrace \mu(W) : (W,b)\in\operatorname{argmin} L\bigr\rbrace ,$$

   or prove that no such quadruple exists.
2. For $(m,n)=(5,2)$ and one explicit $S$ (say $S=0.999$), determine the map $\lambda \mapsto \lbrace \mu(W) : (W,b)\in\operatorname{argmin}(L+\lambda R)\rbrace $ on $\lambda\in(0,\infty)$.

In words: is there any regime where penalizing the average strictly lowers the worst case for *every* minimizer, while still storing features usefully? The task-loss clause excludes the cheap large-$\lambda$ answer of lowering coherence by shrinking columns to zero, and the strict inequality is between the worst regularized minimizer and the best unregularized one. Scalarization — the two-line fact of the opening paragraph — cannot answer it: it controls the average $R$, not the max $\mu$. At $(5,2)$ and high sparsity the unregularized optimum is observed by Elhage et al. [[EHOS+22]](../references/EHOS+22.md) (empirically, not proved) to be the regular pentagon, with $\mu=\cos 36^\circ\approx0.809$; the question is whether the minimizer passes through low-$\mu$ geometries as $\lambda$ grows or jumps straight to feature-dropping. See [MAIS-A4](../agendas/A4/) for the scalarization proposition, the frame-potential warning, and the surrounding agenda.

## References

- [[EHOS+22]](../references/EHOS+22.md) N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- [[BF03]](../references/BF03.md) J. J. Benedetto and M. Fickus, *Finite normalized tight frames*, Advances in Computational Mathematics 18(2–4), 357–385.
- [[W74]](../references/W74.md) L. R. Welch, *Lower bounds on the maximum cross correlation of signals*, IEEE Transactions on Information Theory 20(3), 397–399.

*Related: [MAIS-O4](MAIS-O4.md) (the full coherence-constrained frontier this is a first case of) · [MAIS-O46](MAIS-O46.md) (whether low coherence even helps recovery) · [MAIS-O51](MAIS-O51.md) (the same penalty analyzed in the smallest model) · [MAIS-O50](MAIS-O50.md) (the gradient-flow version).*
