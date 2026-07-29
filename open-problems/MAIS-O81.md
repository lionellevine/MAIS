# Does a saddle have a well-defined free energy?

*Open problem MAIS-O81 · posed in [MAIS-A7](../agendas/A7/) as [Problem 6.1](../agendas/A7/MAIS-A7.tex#L545) · Status: open.*

*Tags: generalization · singular learning theory · developmental interpretability · statistics · algebraic geometry. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Developmental interpretability reads a training run as a descent down a staircase of saddles and prices each rung by the Bayesian free-energy ladder of singular learning theory: Watanabe's asymptotics [W09], localized to regions at positive loss by Lau, Furman, Wang, Murfet, and Wei [[LFWMW23]](../references/LFWMW23.md), assign a region around a critical set at loss $L_C$ with learning coefficient $\lambda_C$ the free energy $n L_C + \lambda_C \log n$ at sample size $n$. Here $\lambda_C$ is a volume exponent: the volume of nearby parameters whose loss lies within $\varepsilon$ of $L_C$ scales as $\varepsilon^{\lambda_C}$. The ladder is a theorem when the rungs are minimizers at the same loss, and conditional already when they are local minimizers at distinct positive levels; the rungs of the dynamical staircase (the chain of plateaus, one per saddle, that gradient descent traverses in training) are saddles, and transcribing the ladder to saddles is the step everyone takes informally.

That step is not innocent, because a saddle has no canonical free energy. Already for a Morse saddle in the plane, the Gibbs mass of a small ball around the saddle is set by the *rim* of the ball in the escape direction, not by the saddle itself, so the coefficient of $\log n$ depends on how the ball's radius shrinks with $n$: different window schedules give different coefficients, a particular boundary scale can happen to match the two-sided learning coefficient of [MAIS-O77](MAIS-O77.md), and no intrinsic choice has emerged (the computation and the window conventions are in [MAIS-A7, Section 6.1](../agendas/A7/)). So far this is schedule-dependence, not proven nonexistence; the problem asks whether an intrinsic exponent exists.

The test bed is the two-layer linear network of the agenda's Problem 3.11(a) ([MAIS-O78](MAIS-O78.md)): targets $\Phi(q)$ of fixed rank $r$ with well-separated singular values, i.i.d. Gaussian regression data, and a smooth positive prior $\varphi$ on one compact domain $W$ meeting every critical set $C_k(q)$, the set of parameters that fit exactly the top $k$ target modes (a saddle set for $k < r$; $C_r$ is the optimal set). The free energy of a region $U \subseteq W$ is $F_{q,n}(U) = -\log \int_U \varphi(w) \prod_{i \le n} p(X_i \mid w)\, dw$, so regions of small free energy carry the posterior mass; $L_{q,n}$ is the matching empirical loss. The $k$th Bayesian crossover $n_k(q)$ is the sample size at which the ladder's preferred rung moves from rank $k-1$ to rank $k$, computed from the Aoyagi–Watanabe learning coefficients of this model [AW05] (exact formulas in the agenda); *well-separated spectra* means $n_1(q) < \dots < n_r(q)$ with every $n_k(q) \to \infty$.

**Problem ([MAIS-A7, Problem 6.1](../agendas/A7/MAIS-A7.tex#L545)).** Use the well-separated target family $\Phi(q)$ and the compact parameter domain $W$ of Problem 3.11(a), with moving crossovers $n_k(q) \to \infty$, and put $J_q = \bigl[ \sqrt{n_1(q)},\  2 n_r(q) \bigr] \cap \mathbb{N}$. Let $F_{q,n}$ and $L_{q,n}$ denote the free energy and empirical loss for the model with target $\Phi(q)$. Define a functional $\Lambda(C) \in \mathbb{Q}_{>0}$ on compact critical sets $C$ of real-analytic losses, agreeing with the local learning coefficient when $C$ consists of local minimizers, and an explicit window schedule $\delta_{q,n} > 0$ with $\sup_{n \in J_q} \delta_{q,n} \to 0$. For $U_k^{q,n} = \lbrace  w \in W : \mathrm{dist}(w, C_k(q) \cap W) < \delta_{q,n} \rbrace $, prove the uniform expansion

$$\sup_{n \in J_q} \frac{\bigl| F_{q,n}(U_k^{q,n}) - n \inf_{U_k^{q,n}} L_{q,n} - \Lambda(C_k(q) \cap W) \log n \bigr|}{\log n} \ \xrightarrow[q \to \infty]{p}\  0$$

for every $0 \le k \le r$, or prove that no such pair $(\Lambda, \delta_{q,n})$ exists. In the latter case identify the schedule-dependent correction terms, such as the rim term above, that any true ladder must carry. The moving interval $J_q$ contains every crossover while tending to infinity, and the $o_p(\log n)$ precision prevents an unconstrained error from absorbing the discrepancy.

Until this is settled, "stratified by learning coefficient" is fully meaningful on the optimal set itself, and only heuristically meaningful on the saddle chains above it, where the interesting dynamics happens — the sharpest obstruction the agenda has to report. See [MAIS-A7](../agendas/A7/), Section 6.1.

## References

- [[W09]](../references/W09.md) S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge Monographs on Applied and Computational Mathematics 25, Cambridge University Press, 2009.
- [[LFWMW23]](../references/LFWMW23.md) E. Lau, Z. Furman, G. Wang, D. Murfet, S. Wei, *The local learning coefficient: a singularity-aware complexity measure*, 2023. [arXiv:2308.12108](https://arxiv.org/abs/2308.12108)
- [[AW05]](../references/AW05.md) M. Aoyagi, S. Watanabe, *Stochastic complexities of reduced rank regression in Bayesian estimation*, Neural Networks 18 (2005), 924–933.

*Related: [MAIS-O78](MAIS-O78.md) (the time–sample dictionary whose part (a) presupposes this expansion) · [MAIS-O79](MAIS-O79.md) (the effective-loss window where the same rim term appears) · [MAIS-O77](MAIS-O77.md) (the two-sided invariants that a successful $\Lambda$ should reproduce).*
