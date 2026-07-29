# Two-feature phase diagram for ℓ¹ dictionary learning

*Open problem MAIS-O41 · posed in [MAIS-A3](../agendas/A3/) as [Problem 5.1](../agendas/A3/MAIS-A3.tex#L331) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · optimization · convex geometry. Difficulty: ★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Two features suffice to see the sparse autoencoder both fail and succeed. Let $v_1,v_2\in\mathbb{R}^n$ be unit vectors at angle $\theta$, and let the data be $y=v_1$, $y=v_2$, or $y=v_1+v_2$ with probabilities $a,b,c$ summing to one. The agenda proves two poles for the zero-penalty constrained limit of $\ell^1$ dictionary learning (reconstruct each data point exactly with nonnegative coefficients, at cost the expected total coefficient mass: the objective $F_0$ below). Nesting merges: when $b=0$ (feature 2 never fires alone), the unique global minimizer places one atom at $v_1$ and one at the bisector of $v_1$ and $v_2$, and the merged atom undercuts the honest two-atom representation at every angle (agenda Proposition 3.1; Proposition 4.5 extends the merging to every penalty $\lambda\in(0,1)$ when $\theta\le\pi/2$). Solo firing recovers: when $a,b>0$, the unique global minimizer is the true pair $(v_1,v_2)$ (Proposition 3.2). Between the poles, nothing is proved.

The estimator: over dictionaries $\Psi\in U_{n,2}$ ($n\times2$ matrices with unit columns), minimize $F_\lambda(\Psi)=\mathbb{E}\ \min_{z\ge0}\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$; its zero-penalty constrained limit is $F_0(\Psi)=\mathbb{E}\,\inf\lbrace\lVert z\rVert_1:z\ge0,\ \Psi z=y\rbrace$, the objective of the two propositions above. Call an atom **live** if, with positive probability in $y$, some optimal code puts positive mass on it (a dead atom can sit anywhere at no cost). **Recovery** at tolerance $\varepsilon$ means the two atoms can be matched one-to-one to the two features so that each matched pair has inner product at least $1-\varepsilon$; a live atom $u$ is an $(\varepsilon,\delta)$-**merge** of the two features if $\lVert u-\alpha v_1-\beta v_2\rVert\le\varepsilon$ for some $\alpha,\beta\ge\delta$ while $\langle u,v_i\rangle\le1-\delta$ for both $i$: near the positive span of both features, bounded away from each (the agenda's Definitions 4.1 and 4.2).

**Problem ([MAIS-A3, Problem 5.1](../agendas/A3/MAIS-A3.tex#L331)).** In the setting of the two propositions above unified — support probabilities $a,b,c\ge0$ with $a+b+c=1$ (the case $b=0$ is Proposition 3.1; the case $a,b>0$ is Proposition 3.2), angle $\theta$, coefficients $\equiv1$, no noise, dictionary size $M=2$ — compute the global minimizers of the *penalized* objective $F_\lambda$ over $U_{n,2}$ exactly, as a function of $(a,b,c,\theta,\lambda)$. Output: the partition of the parameter space into recovery and merging regions in the sense of the agenda's Definition 4.2, with explicit $(\varepsilon,\delta)$, and the location of the boundary as $b$ — the probability that feature 2 fires alone — increases from 0 with the other parameters held fixed.

Everything reduces to a family of two-dimensional convex programs glued along combinatorial boundaries (which atoms are active in each of the three events). The face $b=0$ is already done; the crossing into recovery as solo firing switches on is the smallest exact instance of the phase boundary the headline problem asks for in general. For the two propositions with proofs and the nearest prior analyses, see [MAIS-A3](../agendas/A3/).

## References

- D. Chanin, J. Wilken-Smith, T. Dulka, H. Bhatnagar, S. Golechha, and J. Bloom, *A is for absorption: studying feature splitting and absorption in sparse autoencoders*, 2024. [arXiv:2409.14507](https://arxiv.org/abs/2409.14507)
- W. Dorrell, *How optimality structures sparse dictionaries: a theory for understanding SAE representations*, 2026. [arXiv:2606.02385](https://arxiv.org/abs/2606.02385)

*Related: [MAIS-O3](MAIS-O3.md) (the headline problem this is the smallest case of) · [MAIS-O36](MAIS-O36.md) (recovery for many independent features) · [MAIS-O43](MAIS-O43.md) (the same diagram measured numerically) · [MAIS-O37](MAIS-O37.md) (two features smeared over caps).*
