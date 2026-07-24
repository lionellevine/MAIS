# Learning coefficients on the matrix factorization fiber and saddles

*Open problem MAIS-O77 · posed in [MAIS-A7](../agendas/A7/MAIS-A7.pdf) as [Problem 3.9](../agendas/A7/MAIS-A7.tex#L358) · Status: open.*

*Safety: generalization — singular learning theory · developmental interpretability. Mathematics: algebraic geometry. Difficulty: ★★ project.*

The two-layer linear network $x \mapsto BAx$, with $A \in \mathbb{R}^{H \times M}$, $B \in \mathbb{R}^{N \times H}$, and population loss $L(A,B) = \tfrac12 \Vert  BA - \Phi \Vert _F^2$ against a rank-$r$ target $\Phi$, is the one model where both the Bayesian and the dynamical accounts of training are explicit. Its optimal set is the fiber $F_\Phi = \lbrace  (A,B) : BA = \Phi \rbrace $; its non-minimal critical points are all saddles, organized into the chain $C_0, C_1, \dots$ that gradient flow visits in order, where $C_k$ is the critical set at which $BA$ equals the top-$k$ singular truncation of $\Phi$ (with the discarded singular directions annihilated by $A$ and $B^\top$). This problem asks for the full table of singularity invariants over both the fiber and the saddles — commutative algebra and blow-ups, no probability at all.

The invariant is the **two-sided local pair** $(\lambda(w), m(w))$, defined at any point $w^\ast$ where $L$ is not locally constant by the volume asymptotics

$$\mathrm{vol}\bigl\lbrace  w \in B_\delta(w^\ast) : |L(w) - L(w^\ast)| < \varepsilon \bigr\rbrace  \asymp \varepsilon^{\lambda(w^\ast)} \bigl( \log \tfrac1\varepsilon \bigr)^{m(w^\ast)-1}.$$

At a local minimum this is the local learning coefficient of Lau et al. ([arXiv:2308.12108](https://arxiv.org/abs/2308.12108)), Watanabe's real log canonical threshold; at a saddle the two-sided absolute value is one of several inequivalent choices, deliberately fixed here.

**Problem ([MAIS-A7, Problem 3.9](../agendas/A7/MAIS-A7.tex#L358); λ-stratification of the fiber and its saddles).** For the loss $L(A,B) = \tfrac12 \Vert  BA - \Phi \Vert _F^2$ with $H > r$:

- **(a)** Compute the local invariants $(\lambda(w), m(w))$ at every point $w \in F_\Phi$, and identify the minimal stratum. Determine whether the invariants depend only on the pair $(\mathrm{rank}\  A, \mathrm{rank}\  B)$. The minimal value is the Aoyagi–Watanabe theorem (the learning coefficient of reduced rank regression). There is partial progress: Lehalleur and Rimányi ([arXiv:2411.19920](https://arxiv.org/abs/2411.19920)) determine the components and codimensions of such fibers at any depth and compute the threshold of the zero-target fiber, and Lau et al. give closed-form local values at parameters of each product rank as ground truth for their estimator. These results do not determine the dependence on the two ranks separately, the edge cases, or any of part (b). Aoyagi's recursive blow-ups are the natural tool.
- **(b)** Compute the two-sided invariants $(\lambda(w), m(w))$ at every point of each saddle set $C_k$, $0 \le k < r$.

The table is what the rest of the agenda consumes: the SGD limit theorem ([MAIS-O76](MAIS-O76.md)) and the time–sample dictionary ([MAIS-O78](MAIS-O78.md)) both take it as input, and part (b) is the substance of the opposing-staircases conjecture, which asserts that $\lambda_k = \inf_{C_k} \lambda$ strictly increases along the saddle chain while the loss decreases. A weekend's preliminary: run the estimator of Lau et al. along a simulated staircase and check numerically before proving. See [MAIS-A7](../agendas/A7/MAIS-A7.pdf), Sections 2.4 and 3.5.

*Related: [MAIS-O7](MAIS-O7.md) (opposing staircases, whose invariants this problem computes) · [MAIS-O70](MAIS-O70.md) (local learning coefficients of reduced-rank regression, the same object from the estimation side) · [MAIS-O76](MAIS-O76.md) (the SGD diffusion on this fiber) · [MAIS-O78](MAIS-O78.md) (the dictionary that consumes the table).*
