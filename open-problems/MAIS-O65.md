# Learning coefficients of modular addition under cross-entropy

*Open problem MAIS-O65 · posed in [MAIS-A6](../agendas/A6/) as [Problem 4.10](../agendas/A6/MAIS-A6.tex#L361) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · grokking · algebraic geometry · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Singular learning theory predicts which algorithm a trained network implements before training it — provided its learning coefficients can be computed for the training setup actually used ([MAIS-O63](MAIS-O63.md)). Practice trains modular addition with softmax and cross-entropy, not squared error — but a deterministic label law is not realizable by any softmax model at finite parameters, so the realizable singular learning theory of Watanabe [W09] says nothing until the truth is smoothed. How much of the singular geometry survives the change of loss, and what happens as the smoothing is removed?

The architecture is the quadratic network of [MAIS-A6](../agendas/A6/): $f_w(a,b) = \sum_{j=1}^H V_j(u_j'(a)+u_j''(b))^2 \in \mathbb{R}^p$ on inputs $(a,b) \in (\mathbb{Z}/p\mathbb{Z})^2$ — lookup tables $u_j', u_j''$ on $\mathbb{Z}/p\mathbb{Z}$ and output columns $V_j \in \mathbb{R}^p$, so $w$ ranges over $\mathbb{R}^{3pH}$ with Euclidean norm $\Vert w\Vert$. The **softmax model** assigns to $(a,b)$ the law $\mathrm{softmax}(f_w(a,b))$ on $\mathbb{Z}/p\mathbb{Z}$, and for $\beta > 0$ the **$\beta$-smoothed truth** is $q_\beta(\cdot \mid a,b) = \mathrm{softmax}(\beta\ \delta_{a+b})$, where $\delta_{a+b}$ is the one-hot vector at $a+b$: the correct residue weighted $e^\beta$ against $1$ for each other residue. This truth is realizable — Fourier inversion gives an exact fit $w^F_H$ of the squared-error problem ($f_{w^F_H} = \delta_{a+b}$) for $H \ge 2p-1$ ([MAIS-A6, Lemma 4.2](../agendas/A6/MAIS-A6.tex#L240) has the explicit table), and scaling its output matrix by $\beta$ gives $f_w = \beta\ \delta_{a+b}$ exactly — and the resulting population loss $K_\beta$, the KL divergence from $q_\beta$ to the model's law averaged over uniform inputs, is real-analytic, no longer polynomial.

Local pairs $(\lambda, m)$ are local learning coefficient and multiplicity in the volume-growth sense of Watanabe [W09]: at a point where $K_\beta$ vanishes, the volume of nearby parameters with $K_\beta \le t$ scales as $t^{\lambda}(\log(1/t))^{m-1}$ as $t \to 0$. Set $R_p = 1 + \Vert w^F_{2p-1}\Vert$.

**Problem ([MAIS-A6, Problem 4.10](../agendas/A6/MAIS-A6.tex#L361)).** Fix odd $p \ge 3$ and $H \ge 2p-1$. Compute the common local pair of $K_\beta$ at the scaled Fourier solution for finite $\beta > 0$. Then, for the specified radius $R_\beta = (1+\beta)R_p$, determine the minimum of the local coefficient over $\lbrace w \in W_0^\beta : \Vert w\Vert  \le R_\beta\rbrace $, its multiplicity, and its asymptotics as $\beta \to \infty$, where $W_0^\beta$ is the zero set of $K_\beta$.

The word "common" is a proved reduction, not part of the problem: near the scaled Fourier solution, KL between softmax laws is comparable to squared distance between centered logits, so after writing $V = \beta\widetilde V$ one gets $K_\beta \asymp K_1$ and the local pair is independent of every finite $\beta$ (agenda Remark 4.11). The genuinely new content is the $\beta \to \infty$ asymptotics of the ball-restricted minimum along the radius schedule $R_\beta$: the honest fragment of "the deterministic task" that the realizable theory can pose. (The multiplicity asked for is the largest among the minimizing points, the one that enters the free-energy expansion.) Exact learning coefficients for softmax-output models are scarce: the closest prior work, by Aoyagi [A25], moves toward three-layer networks with ReLU units and softmax outputs. The obstructions to any more canonical formulation are discussed in Section 9 of [MAIS-A6](../agendas/A6/).

## References

- [W09] S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- [A25] M. Aoyagi, *Singular leaning [sic] coefficients and efficiency in learning theory*, 2025. [arXiv:2501.12747](https://arxiv.org/abs/2501.12747)

*Related: [MAIS-O63](MAIS-O63.md) (the squared-error version, whose answer the finite-$\beta$ pair must match) · [MAIS-O6](MAIS-O6.md) (Fourier structure of the minimizers) · [MAIS-O71](MAIS-O71.md) (another boundary of the analytic setup: ReLU with continuous inputs).*
