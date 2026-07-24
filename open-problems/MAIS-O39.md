# Does the amortized encoder change the learned dictionary?

*Open problem MAIS-O39 · posed in [MAIS-A3](../agendas/A3/MAIS-A3.pdf) as [Problem 4.9](../agendas/A3/MAIS-A3.tex#L297) · Status: open.*

*Safety: interpretability — sparse autoencoders · mechanistic interpretability · superposition. Mathematics: optimization · statistics. Difficulty: ★★★ hard.*

A sparse autoencoder never solves the sparse-coding program it is named for. Instead of computing the optimal code for each data point, it applies one learned affine-plus-ReLU map — cheap, but not optimal. O'Neill, Gumran, and Klindt proved this shortcut can produce inaccurate *codes*; whether it moves the minimizing *dictionary*, the object interpretability actually reads off, is open.

The setting is a superposition model: data $y=\Phi x+\xi$ with $\Phi\in U_{n,m}$, the set of $n\times m$ matrices with unit columns (here $v_1,\dots,v_m$), sparse nonnegative codes $x$, and Gaussian noise $\xi$. Two objectives over dictionaries $\Psi\in U_{n,M}$, with unit columns $u_1,\dots,u_M$, compete. Exact coding: $F_\lambda(\Psi)=\mathbb{E}\ \min_{z\ge0}\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$. Amortized coding: $G_\lambda(\Psi,W,b)=\mathbb{E}\bigl[\tfrac12\lVert y-\Psi\ c(y)\rVert^2+\lambda\lVert c(y)\rVert_1\bigr]$ with $c(y)=\mathrm{ReLU}(Wy+b)$, the encoder $W\in\mathbb{R}^{M\times n}$ and $b\in\mathbb{R}^M$ optimized jointly with $\Psi$. Say $\Psi$ **$\varepsilon$-recovers** $\Phi$ if some injection $\tau$ has $\langle u_{\tau(i)},v_i\rangle\ge1-\varepsilon$ for all $i$; a firing atom (one that carries code mass with positive probability) is an **$(\varepsilon,\delta)$-merge** of two features if it lies within $\varepsilon$ of a combination $\alpha v_i+\beta v_{i'}$ with $\alpha,\beta\ge\delta$ while its inner product with each feature stays at most $1-\delta$.

**Problem ([MAIS-A3, Problem 4.9](../agendas/A3/MAIS-A3.tex#L297)).** Fix a superposition model $\mathcal S$ and $\lambda>0$. Let $\mathcal M_F=\operatorname{argmin}_{U_{n,M}}F_\lambda$, and let $\mathcal A_G$ be the set of dictionaries $\Psi\in U_{n,M}$ for which some minimizing sequence $(\Psi_r,W_r,b_r)$ for $G_\lambda$ has $\Psi_r\to\Psi$. Compare $\mathcal M_F$ with $\mathcal A_G$.

1. Under the hypotheses of the agenda's Conjecture 4.4 ([MAIS-O36](MAIS-O36.md): independent Bernoulli($p$) supports, coefficients $\mathrm{Unif}[1,2]$, no noise, coherence and density bounds), is there an absolute constant $C'$ such that every $\Psi\in\mathcal A_G$ $(C'\lambda)$-recovers $\Phi$?
2. Exhibit a superposition model, or prove none exists, for which — for some $\varepsilon,\delta>0$ — some $\Psi\in\mathcal A_G$ contains an $(\varepsilon,\delta)$-merge while no $\Psi\in\mathcal M_F$ does (with the same $M$, $\lambda$).

The compactness of $U_{n,M}$ makes $\mathcal A_G$ nonempty even when the unconstrained encoder parameters diverge; settling attainment of $G_\lambda$ remains part of the problem.

Part 2 asks whether amortization can *create* a failure mode absent from exact coding: a merged atom the ideal estimator would never produce. Sun, Wang, and Hu document such dictionary distortions empirically across amortized architectures; the exact comparison of the population sets $\mathcal M_F$ and $\mathcal A_G$ is untouched. For the estimator definitions and the amortization literature, see [MAIS-A3](../agendas/A3/MAIS-A3.pdf).

*Related: [MAIS-O36](MAIS-O36.md) (the exact-coding recovery conjecture that part 1 extends) · [MAIS-O3](MAIS-O3.md) (the headline identifiability problem) · [MAIS-O43](MAIS-O43.md) (numerics run on the amortized objective $G_\lambda$).*
