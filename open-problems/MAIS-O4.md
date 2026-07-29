# Training for interpretability

*Open problem MAIS-O4 · headline problem 4 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A4](../agendas/A4/) as [Problem 5.1](../agendas/A4/MAIS-A4.tex#L323) · Status: open.*

*Tags: interpretability · training for interpretability · superposition · optimization · convex geometry · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A network asked to store more features than it has dimensions must let them interfere. Post-hoc interpretability deciphers whatever storage scheme training happened to invent; the complementary problem is to train networks whose features are legible in the first place, and to know what that legibility costs in performance.

In the **ReLU toy model** of Elhage et al., the trade-off can be made exact because the features exist by construction. The data $x\in\mathbb{R}^m$ has independent coordinates, each zero with probability $S$ (the **sparsity**) and otherwise uniform on $[0,1]$; the network compresses into $n<m$ dimensions and reconstructs, $f_{W,b}(x)=\mathrm{ReLU}(W^{\top}Wx+b)$ with $W\in\mathbb{R}^{n\times m}$ and $b\in\mathbb{R}^m$, and the task loss is $L_{m,n,S}(W,b)=\mathbb{E}\ \Vert x-f_{W,b}(x)\Vert _2^2$. Column $W_i$ is the direction where feature $i$ is stored, and the **coherence** $\mu(W)=\max_{i\neq j}|\langle \widehat W_i,\widehat W_j\rangle|$ (maximum over distinct nonzero columns, normalized) is the worst-case crosstalk between two stored features. Two anchors are proved in the agenda. A dropped feature ($W_i=0$) can be reconstructed only by the constant $\mathrm{ReLU}(b_i)$, and the best constant leaves squared error exactly $v(S)=(1-S)(1+3S)/12$: the cost of dropping one feature. First anchor: the least loss subject to full orthogonality $\mu(W)=0$ is exactly $(m-n)\ v(S)$, attained by storing $n$ features on orthogonal axes and dropping the rest. Second: any cap $c<1/\sqrt n$ permits at most $m_\ast (c)=n(1-c^2)/(1-nc^2)$ nonzero columns (by the Welch bound), hence forces a loss of at least $(m-m_\ast (c))\ v(S)$. The object of the problem is the entire curve between these anchors and the unconstrained optimum.

**Problem ([MAIS-A4, Problem 5.1](../agendas/A4/MAIS-A4.tex#L323)).** For $m>n\ge2$, $S\in(0,1)$, $c\in[0,1]$, define

$$P_{m,n,S}(c) \ =\  \inf\bigl\lbrace \ L_{m,n,S}(W,b)\ :\ \mu(W)\le c\ \bigr\rbrace .$$

1. Determine $P_{3,2,S}(c)$ and $P_{5,2,S}(c)$ for all $S\in(0,1)$ and $c\in[0,1]$.
2. Prove or disprove: for each fixed $(m,n,S)$ there are finitely many points $0=c_0<c_1<\cdots<c_r=1$ such that on each interval $(c_{i-1},c_i)$ the function $c\mapsto P_{m,n,S}(c)$ agrees with a function real-analytic on a neighborhood of $[c_{i-1},c_i]$. ($P_{m,n,S}$ is nonincreasing in $c$, so one-sided limits exist everywhere; whether it is continuous is part of the question.)
3. Determine $c^\ast (m,n,S)=\inf\lbrace c: P_{m,n,S}(c)=P_{m,n,S}(1)\rbrace $, the smallest coherence budget at which interpretability (in this surrogate) becomes free.

In words: how small can the task loss be among weight matrices whose worst-case interference is at most $c$ — the exact price of each increment of legibility. In this notation the anchors read $P_{m,n,S}(0)=(m-n)\ v(S)$ and $P_{m,n,S}(c)\ge(m-m_\ast (c))\ v(S)$ for $c<1/\sqrt n$, while the unconstrained value $P_{m,n,S}(1)$ is not known in closed form for general $(m,n,S)$. Empirically the optimizer jumps between regular-polytope configurations (antipodal pairs, triangles, pentagons) as sparsity varies, which suggests the frontier is piecewise smooth with kinks at changes of optimal geometry; part (2) asks for that picture as a theorem. The survey's stated first case — whether penalizing the *average* interference lowers the *worst-case* coherence of the minimizer — is [MAIS-O44](MAIS-O44.md). For the proved anchors, a subadditivity argument giving a thermodynamic limit of the frontier, and the surrounding program, see [MAIS-A4](../agendas/A4/).

## References

- Elhage, N., et al. (2022). Toy models of superposition. *Transformer Circuits Thread*. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- Welch, L. R. (1974). Lower bounds on the maximum cross correlation of signals. *IEEE Transactions on Information Theory* 20(3), 397–399.
- Cowsik, A., Dolev, K., and Infanger, A. (2024). The Persian rug: solving toy models of superposition using large-scale symmetries. [arXiv:2410.12101](https://arxiv.org/abs/2410.12101)

*Related: [MAIS-O44](MAIS-O44.md) (the survey's first case: average vs. worst-case interference) · [MAIS-O51](MAIS-O51.md) (the same frontier in the smallest model, a starter) · [MAIS-O47](MAIS-O47.md) (uniqueness of the $(5,2)$ minimizer, needed for part 1) · [MAIS-O49](MAIS-O49.md) (the analogous frontier for weight sparsity).*
