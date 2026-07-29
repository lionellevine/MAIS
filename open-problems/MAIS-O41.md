# Two-feature phase diagram for ℓ¹ dictionary learning

*Open problem MAIS-O41 · posed in [MAIS-A3](../agendas/A3/) as [Problem 5.1](../agendas/A3/MAIS-A3.tex#L331) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · optimization · convex geometry. Difficulty: ★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A sparse autoencoder is interpretability's tool for extracting the concept directions a network stores in superposition; whether it recovers the true directions or blends co-occurring ones into a single reported "feature" is what decides if the extracted concepts can be trusted. Two features suffice to see it both fail and succeed. Let $v_1,v_2\in\mathbb{R}^n$ be unit vectors at angle $\theta$, and let the data be $y=v_1$, $y=v_2$, or $y=v_1+v_2$ with probabilities $a,b,c$ summing to one. The agenda proves two poles for the zero-penalty constrained limit of $\ell^1$ dictionary learning (reconstruct each data point exactly with nonnegative coefficients, at cost the expected total coefficient mass). Nesting merges: when $b=0$ (feature 2 never fires alone), the unique global minimizer places one atom at $v_1$ and one at the bisector of $v_1$ and $v_2$, and the merged atom undercuts the honest two-atom representation at every angle (agenda Proposition 3.1; Proposition 4.5 extends the merging to every penalty $\lambda\in(0,1)$ when $\theta\le\pi/2$). Solo firing recovers: when $a,b>0$, the unique global minimizer is the true pair $(v_1,v_2)$ (Proposition 3.2). Between the poles, nothing is proved.

The estimator: over dictionaries $\Psi\in U_{n,2}$ ($n\times2$ matrices with unit columns), minimize $F_\lambda(\Psi)=\mathbb{E}\ \min_{z\ge0}\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$. **Recovery** means the two atoms match the two features one-to-one, each matched pair at inner product at least $1-\varepsilon$; a **merge** is a firing atom near the positive span of both features while bounded away from each (the agenda's Definition 4.2 makes $(\varepsilon,\delta)$ precise).

**Problem ([MAIS-A3, Problem 5.1](../agendas/A3/MAIS-A3.tex#L331)).** In the setting of the two propositions above unified — support probabilities $a,b,c\ge0$ with $a+b+c=1$ (the case $b=0$ is Proposition 3.1; the case $a,b>0$ is Proposition 3.2), angle $\theta$, coefficients $\equiv1$, no noise, dictionary size $M=2$ — compute the global minimizers of the *penalized* objective $F_\lambda$ over $U_{n,2}$ exactly, as a function of $(a,b,c,\theta,\lambda)$. Output: the partition of the parameter space into recovery and merging regions in the sense of the agenda's Definition 4.2, with explicit $(\varepsilon,\delta)$, and the location of the boundary as $b$ — the probability that feature 2 fires alone — increases from 0 with the other parameters held fixed.

Everything reduces to a family of two-dimensional convex programs glued along combinatorial boundaries (which atoms are active in each of the three events). The face $b=0$ is already done; the crossing into recovery as solo firing switches on is the smallest exact instance of the phase boundary the headline problem asks for in general. The nearest prior analyses are the two-feature absorption family of Chanin et al. [[CWDB+24]](https://arxiv.org/abs/2409.14507) and Dorrell's stability conditions for local optima of the same nonnegative $\ell^1$ problem [[Dor26]](https://arxiv.org/abs/2606.02385); for the two propositions with proofs, see [MAIS-A3](../agendas/A3/).

## References

- [CWDB+24] D. Chanin, J. Wilken-Smith, T. Dulka, H. Bhatnagar, S. Golechha, and J. Bloom, *A is for absorption: studying feature splitting and absorption in sparse autoencoders*, 2024. [arXiv:2409.14507](https://arxiv.org/abs/2409.14507)
- [Dor26] W. Dorrell, *How optimality structures sparse dictionaries: a theory for understanding SAE representations*, 2026. [arXiv:2606.02385](https://arxiv.org/abs/2606.02385)

*Related: [MAIS-O3](MAIS-O3.md) (the headline problem this is the smallest case of) · [MAIS-O36](MAIS-O36.md) (recovery for many independent features) · [MAIS-O43](MAIS-O43.md) (the same diagram measured numerically) · [MAIS-O37](MAIS-O37.md) (two features smeared over caps).*
