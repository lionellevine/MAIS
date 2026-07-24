# Does a saddle have a well-defined free energy?

*Open problem MAIS-O81 · posed in [MAIS-A7](../agendas/A7/MAIS-A7.pdf) as [Problem 6.1](../agendas/A7/MAIS-A7.tex#L544) · Status: open.*

*Safety: generalization — singular learning theory · developmental interpretability. Mathematics: statistics · algebraic geometry. Difficulty: ★★★ hard.*

The Bayesian free-energy ladder assigns a region around a critical set at loss $L_C$ with learning coefficient $\lambda_C$ the free energy $n L_C + \lambda_C \log n$ at sample size $n$. This is a theorem when the rungs are minimizers at the same loss, and conditional already when they are local minimizers at distinct positive levels; the rungs of the dynamical staircase are saddles, and transcribing the ladder to saddles is the step everyone takes informally. It is not innocent. For a Morse saddle $z$ in dimension $2$, $L = L(z) + \tfrac{\mu}{2}(x^2 - y^2)$, the Gibbs mass of a $\delta$-ball at inverse temperature $\beta$ (the population proxy for sample size $n$) satisfies

$$\int_{B_\delta(z)} e^{-\beta L} \asymp e^{-\beta L(z)} \cdot \beta^{-1/2} \cdot \frac{e^{\beta \mu \delta^2 / 2}}{\beta \mu \delta} ,$$

so the window free energy is $\beta \bigl( L(z) - \tfrac{\mu \delta^2}{2} \bigr) + O(\log \beta)$: it is set by the *rim*, in the escape direction, not by the saddle. Shrinking the window, $\delta = \beta^{-\rho}$ with $0 < \rho < \tfrac12$, still leaves an intermediate power $\beta^{1 - 2\rho}$ that swamps $\log \beta$; at the boundary scale $\delta = c \beta^{-1/2}$ the free energy becomes $\beta L(z) + \log \beta + O(1)$, and for $\rho > \tfrac12$ the coefficient of $\log\beta$ is $d\rho$ instead, with $d$ the ambient dimension (here $2$). The conclusion is schedule-dependence, not universal nonexistence: a chosen window scale may happen to reproduce the two-sided learning coefficient, but no intrinsic window exponent has emerged. The problem asks whether one exists.

The test bed is the deep linear network of the agenda's Problem 3.11(a) ([MAIS-O78](MAIS-O78.md)): rank-$r$ targets $\Phi(q)$ with well-separated spectra, i.i.d. Gaussian regression data, a smooth positive prior on one compact domain $W$ meeting every saddle set $C_k(q)$ ($0 \le k \le r$, the critical sets where only the top $k$ modes are fit), and Bayesian crossovers $n_k(q) \to \infty$.

**Problem ([MAIS-A7, Problem 6.1](../agendas/A7/MAIS-A7.tex#L544)).** Use the well-separated target family $\Phi(q)$ and the compact parameter domain $W$ of Problem 3.11(a), with moving crossovers $n_k(q) \to \infty$, and put $J_q = \bigl[ \sqrt{n_1(q)},\, 2 n_r(q) \bigr] \cap \mathbb{N}$. Let $F_{q,n}$ and $L_{q,n}$ denote the free energy and empirical loss for the model with target $\Phi(q)$. Define a functional $\Lambda(C) \in \mathbb{Q}_{>0}$ on compact critical sets $C$ of real-analytic losses, agreeing with the local learning coefficient when $C$ consists of local minimizers, and an explicit window schedule $\delta_{q,n} > 0$ with $\sup_{n \in J_q} \delta_{q,n} \to 0$. For $U_k^{q,n} = \{ w \in W : \mathrm{dist}(w, C_k(q) \cap W) < \delta_{q,n} \}$, prove the uniform expansion

$$\sup_{n \in J_q} \frac{\bigl| F_{q,n}(U_k^{q,n}) - n \inf_{U_k^{q,n}} L_{q,n} - \Lambda(C_k(q) \cap W) \log n \bigr|}{\log n} \;\xrightarrow[q \to \infty]{p}\; 0$$

for every $0 \le k \le r$, or prove that no such pair $(\Lambda, \delta_{q,n})$ exists. In the latter case identify the schedule-dependent correction terms, such as the rim term above, that any true ladder must carry. The moving interval $J_q$ contains every crossover while tending to infinity, and the $o_p(\log n)$ precision prevents an unconstrained error from absorbing the discrepancy.

Until this is settled, "stratified by learning coefficient" is fully meaningful on the optimal set itself, and only heuristically meaningful on the saddle chains above it, where the interesting dynamics happens — the sharpest obstruction the agenda has to report. See [MAIS-A7](../agendas/A7/MAIS-A7.pdf), Section 6.1.

*Related: [MAIS-O78](MAIS-O78.md) (the time–sample dictionary whose part (a) presupposes this expansion) · [MAIS-O79](MAIS-O79.md) (the effective-loss window where the same rim term appears) · [MAIS-O77](MAIS-O77.md) (the two-sided invariants that a successful $\Lambda$ should reproduce).*
