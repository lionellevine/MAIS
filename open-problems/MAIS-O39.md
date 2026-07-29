# Does the amortized encoder change the learned dictionary?

*Open problem MAIS-O39 · posed in [MAIS-A3](../agendas/A3/) as [Problem 4.9](../agendas/A3/MAIS-A3.tex#L298) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · optimization · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A sparse autoencoder never solves the sparse-coding program it is named for. Instead of computing the optimal code for each data point, it applies one learned affine-plus-ReLU map — cheap, but not optimal. O'Neill, Gumran, and Klindt proved this shortcut can produce inaccurate *codes*; whether it moves the minimizing *dictionary*, the object interpretability actually reads off, is open.

A **superposition model** $\mathcal S=(\Phi,\pi,\nu,\sigma)$ generates data $y=\Phi x+\xi$: the dictionary $\Phi$ belongs to $U_{n,m}$, the set of $n\times m$ matrices with unit columns (here $v_1,\dots,v_m$); the support $S\subseteq[m]$ of the nonnegative code $x$ is drawn from a law $\pi$ on subsets; the nonzero coefficients are drawn independently from a law $\nu$ on $(0,\infty)$ with finite second moment; and $\xi$ is Gaussian noise of level $\sigma\ge0$. Part 2 below quantifies over exactly this class of models. Two objectives over dictionaries $\Psi\in U_{n,M}$, with unit columns $u_1,\dots,u_M$, compete. Exact coding: $F_\lambda(\Psi)=\mathbb{E}\ \min_{z\ge0}\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$. Amortized coding: $G_\lambda(\Psi,W,b)=\mathbb{E}\bigl[\tfrac12\lVert y-\Psi\ c(y)\rVert^2+\lambda\lVert c(y)\rVert_1\bigr]$ with $c(y)=\mathrm{ReLU}(Wy+b)$, the encoder $W\in\mathbb{R}^{M\times n}$ and $b\in\mathbb{R}^M$ optimized jointly with $\Psi$. Say $\Psi$ **$\varepsilon$-recovers** $\Phi$ if some injection $\tau$ has $\langle u_{\tau(i)},v_i\rangle\ge1-\varepsilon$ for all $i$. Call an atom $u_j$ of $\Psi$ **live** if, with positive probability in $y$, some minimizer $z$ of the exact program $\min_{z\ge0}\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$ has $z_j>0$; liveness is judged by this exact code for every dictionary, including one obtained as a limit of amortized training, so the learned encoder plays no role in the definition. A live atom is an **$(\varepsilon,\delta)$-merge** of two features if it lies within $\varepsilon$ of a combination $\alpha v_i+\beta v_{i'}$ with $\alpha,\beta\ge\delta$ while its inner product with each feature stays at most $1-\delta$.

Part 1 below assumes the hypotheses of the agenda's recovery conjecture ([MAIS-O36](MAIS-O36.md)): $m>n$; each feature belongs to the support independently with probability $p>0$; $\nu=\mathrm{Unif}[1,2]$; $\sigma=0$; and, for an absolute constant $c$, the coherence $\mu=\max_{i\neq j}\lvert\langle v_i,v_j\rangle\rvert$ and the density satisfy $\mu\,(pm+\log m)\le c$ and $pm+\log m\le c\sqrt{n/\log m}$, with penalty $\lambda\in(0,c)$. The conjecture asserts that these conditions force every global minimizer of $F_\lambda$ to $(C\lambda)$-recover $\Phi$ for an absolute constant $C$; part 1 asks whether the amortized limits obey the same bound with a possibly different constant.

**Problem ([MAIS-A3, Problem 4.9](../agendas/A3/MAIS-A3.tex#L298)).** Fix a superposition model $\mathcal S$ and $\lambda>0$. Let $\mathcal M_F=\operatorname{argmin}_{U_{n,M}}F_\lambda$, and let $\mathcal A_G$ be the set of dictionaries $\Psi\in U_{n,M}$ for which some minimizing sequence $(\Psi_r,W_r,b_r)$ for $G_\lambda$ has $\Psi_r\to\Psi$. Compare $\mathcal M_F$ with $\mathcal A_G$.

1. Under the hypotheses of the agenda's Conjecture 4.4 ([MAIS-O36](MAIS-O36.md): independent Bernoulli($p$) supports, coefficients $\mathrm{Unif}[1,2]$, no noise, coherence and density bounds), is there an absolute constant $C'$ such that every $\Psi\in\mathcal A_G$ $(C'\lambda)$-recovers $\Phi$?
2. Exhibit a superposition model, or prove none exists, for which — for some $\varepsilon,\delta>0$ — some $\Psi\in\mathcal A_G$ contains an $(\varepsilon,\delta)$-merge while no $\Psi\in\mathcal M_F$ does (with the same $M$, $\lambda$).

The compactness of $U_{n,M}$ makes $\mathcal A_G$ nonempty even when the unconstrained encoder parameters diverge; settling attainment of $G_\lambda$ remains part of the problem.

Part 2 asks whether amortization can *create* a failure mode absent from exact coding: a merged atom the ideal estimator would never produce. Sun, Wang, and Hu document such dictionary distortions empirically across amortized architectures; the exact comparison of the population sets $\mathcal M_F$ and $\mathcal A_G$ is untouched. For the estimator definitions and the amortization literature, see [MAIS-A3](../agendas/A3/).

## References

- C. O'Neill, A. Gumran, and D. Klindt, *Compute optimal inference and provable amortisation gap in sparse autoencoders*, International Conference on Machine Learning (ICML) 2025. [arXiv:2411.13117](https://arxiv.org/abs/2411.13117)
- Y. Sun, Z. Wang, and W. Hu, *The price of amortized inference in sparse autoencoders*, International Conference on Learning Representations (ICLR) 2026.
- R. Gribonval, R. Jenatton, and F. Bach, *Sparse and spurious: dictionary learning with noise and outliers*, IEEE Transactions on Information Theory 61 (2015), 6298–6319. [arXiv:1407.5155](https://arxiv.org/abs/1407.5155)

*Related: [MAIS-O36](MAIS-O36.md) (the exact-coding recovery conjecture that part 1 extends) · [MAIS-O3](MAIS-O3.md) (the headline identifiability problem) · [MAIS-O43](MAIS-O43.md) (numerics run on the amortized objective $G_\lambda$).*
