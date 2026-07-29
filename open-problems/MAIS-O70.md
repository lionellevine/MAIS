# Local learning coefficients of reduced-rank regression

*Open problem MAIS-O70 · posed in [MAIS-A6](../agendas/A6/) as [Problem 6.3](../agendas/A6/MAIS-A6.tex#L491) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · algebraic geometry · statistics. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The one singular model family solved completely — reduced-rank regression — was solved globally: Aoyagi and Watanabe computed the minimum of the local learning coefficient over the whole set of exact fits, as a closed form in four integers. But the estimators now used on neural networks are local, evaluated at a point, and the pointwise values on this benchmark family have never been tabulated. The benchmark is missing its own answer key.

**Reduced-rank regression** is the model $y = BAx + \text{noise}$: standard Gaussian output density with mean $BAx$, input $x \sim N(0, I_N)$ in $\mathbb{R}^N$, output in $\mathbb{R}^M$, and parameter $w = (A, B)$ with $A \in \mathbb{R}^{H \times N}$, $B \in \mathbb{R}^{M \times H}$ — a two-layer linear network whose exact-fit set for a rank-$r$ truth $B_0 A_0$ is the fiber $W_0 = \lbrace (A,B) : BA = B_0 A_0\rbrace $. The population loss is $K(A,B) = \tfrac12\  \mathbb{E}\lVert (BA - B_0 A_0)\ x \rVert^2$. The local pair $(\lambda(w^\ast ), m(w^\ast ))$ at a point $w^\ast  \in W_0$ is the local learning coefficient and multiplicity: the volume of $\lbrace K \le \varepsilon\rbrace $ in a small ball around $w^\ast $ scales as $\varepsilon^{\lambda(w^\ast )}(\log(1/\varepsilon))^{m(w^\ast )-1}$. Different points of the fiber can be differently singular; the Aoyagi–Watanabe formula (agenda Theorem 3.1) is the minimum over the fiber. In the main case, where $M + r \le N + H$, $N + r \le M + H$, and $H + r \le M + N$, that minimum is $\lambda = (2(H+r)(M+N) - (M-N)^2 - (H+r)^2)/8$ when $M + N + H + r$ is even (with $m = 1$), and $1/8$ more when it is odd (with $m = 2$); if one of the three inequalities fails, the minimum is instead $(HN - Hr + Mr)/2$, $(HM - Hr + Nr)/2$, or $MN/2$ according as the first, second, or third fails, with $m = 1$. For $N = M = H = 2$ and $r = 0$ the even case gives $\lambda = (16 - 4)/8 = 3/2$.

**Problem ([MAIS-A6, Problem 6.3](../agendas/A6/MAIS-A6.tex#L491)).** For reduced-rank regression with parameters $(N, M, H, r)$, prove that the local pair $(\lambda(w^\ast ), m(w^\ast ))$ at a factorization $w^\ast  = (A, B) \in W_0$ depends only on $(\operatorname{rank} A, \operatorname{rank} B)$, and compute the resulting table. Hence characterize the strata on which $\lambda(w^\ast )$ equals the minimum in the Aoyagi–Watanabe theorem. For example, when $N = M = H = 2$ and $r = 0$, a neighborhood of $(I_2, 0)$ has local coefficient $2$, whereas the table gives $3/2$.

In the statement's last sentence, "the table" is the Aoyagi–Watanabe case list, whose value for these parameters is the $3/2$ just computed. The example shows the stratification is genuine: at $(I_2, 0)$ the equation $BA = 0$ reduces to $B = 0$, a smooth point of the fiber, and the local coefficient $2$ exceeds the global minimum $3/2$. The convergence theory for the estimator at a point is already available via Watanabe's widely applicable Bayesian information criterion (WBIC): restricted to a small ball around $w^\ast $, the WBIC estimate converges in probability to $\lambda(w^\ast )$ (agenda Remark 6.4). What is missing is the table itself. A starter sized for one paper: the case $N = M = H = 2$, listing the local pair on each rank stratum of $\lbrace (A,B) : BA = C\rbrace $. Background and the global theorem are in [MAIS-A6](../agendas/A6/).

## References

- Aoyagi, M., and Watanabe, S. (2005). Stochastic complexities of reduced rank regression in Bayesian estimation. *Neural Networks* 18(7), 924–933.
- Lehalleur, S. P., and Rimányi, R. (2024). Geometry of fibers of the multiplication map of deep linear neural networks. [arXiv:2411.19920](https://arxiv.org/abs/2411.19920).
- Lau, E., Furman, Z., Wang, G., Murfet, D., and Wei, S. (2023). The local learning coefficient: a singularity-aware complexity measure. [arXiv:2308.12108](https://arxiv.org/abs/2308.12108).

*Related: [MAIS-O69](MAIS-O69.md) (the localization question this table would calibrate) · [MAIS-O77](MAIS-O77.md) (learning coefficients on the matrix factorization fiber and its saddles) · [MAIS-O67](MAIS-O67.md) (the attention analog of the global formula).*
