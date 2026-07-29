# Two smeared features: recover, merge, or split

*Open problem MAIS-O37 · posed in [MAIS-A3](../agendas/A3/) as [Problem 4.7](../agendas/A3/MAIS-A3.tex#L280) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · optimization · probability · convex geometry. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

When a sparse autoencoder reports several atoms for one concept, has it failed, or has it faithfully tiled a feature that was never a single direction? Practitioners call the phenomenon feature splitting (Chanin et al. [[CWDB+24]](https://arxiv.org/abs/2409.14507)), but in the standard generative model a feature *is* one direction, so splitting cannot even be stated there. This problem smears each feature over a spherical cap and asks for the full phase diagram: recovery, splitting, and merging in one two-feature model.

The estimator is $\ell^1$-penalized dictionary learning: over dictionaries $\Psi\in U_{n,M}$ ($n\times M$ matrices with unit columns), minimize the population objective $F_\lambda(\Psi)=\mathbb{E}\ \min_{z\ge0}\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$. An atom of $\Psi$ is **live** if, with positive probability in $y$, some minimizing code puts mass on it; a dead atom can be parked anywhere without changing the objective, so only live atoms count.

**Problem ([MAIS-A3, Problem 4.7](../agendas/A3/MAIS-A3.tex#L280)).** Let $n\ge3$, and for a unit vector $v$ and $\tau\in(0,\pi/2)$ let $\mathcal C(v,\tau)=\lbrace u\in\mathbb{R}^n:\lVert u\rVert=1,\ \langle u,v\rangle\ge\cos\tau\rbrace $ be the spherical cap of angular radius $\tau$ about $v$. Fix unit vectors $v_1,v_2$ at angle $\theta$, a cap radius $\tau<\theta/4$, support probabilities $\pi(\lbrace 1\rbrace )=a$, $\pi(\lbrace 2\rbrace )=b$, $\pi(\lbrace 1,2\rbrace )=c$ with $a+b+c=1$, and a dictionary size $M$. Data: draw $S\sim\pi$ and, independently for each $i\in S$, a direction $g_i$ uniform (normalized surface measure) on $\mathcal C(v_i,\tau)$; output $y=\sum_{i\in S}g_i$. For the estimator $F_\lambda$ over $U_{n,M}$, determine, as a function of $(n,\theta,\tau,\lambda,a,b,c,M)$: the number of live atoms of the global minimizers; how many of them lie in $\mathcal C(v_1,2\tau)$, how many in $\mathcal C(v_2,2\tau)$, and how many in neither cap; and the boundaries in parameter space between the three behaviors: one live atom per cap (recovery), several live atoms in one cap (splitting), and live atoms in neither cap (merging).

For a single smeared feature ($b=c=0$) and $M\to\infty$, the question is a relative of quantization of a measure on the sphere, with Zador-type asymptotics as a guide: by Zador's theorem (Graf and Luschgy [GL00]), the best mean squared error of $M$ points quantizing a nice $d$-dimensional measure decays like $M^{-2/d}$, with the optimal points distributed according to a power of the underlying density. Only a relative, not an instance, because the $\ell^1$ coding cost lets several atoms jointly reconstruct a point, which nearest-point quantization does not. On that reading, splitting is the estimator quantizing a feature that was never one direction. In a related model, Dalili and Mahdavi [[DM26]](https://arxiv.org/abs/2606.06333) prove that multidimensional features can force many single-direction atoms, with an objective-decreasing path toward a split dictionary. The coupled two-cap problem is the open part: one dictionary must quantize both caps while unmixing their co-occurrence. See [MAIS-A3](../agendas/A3/) for the atomic model this smears and the empirical literature on splitting.

## References

- [GL00] S. Graf and H. Luschgy, *Foundations of Quantization for Probability Distributions*, Lecture Notes in Mathematics 1730, Springer, 2000.
- [DM26] S. A. Dalili and M. Mahdavi, *Subspace-Aware Sparse Autoencoders for Effective Mechanistic Interpretability*, preprint, 2026. [arXiv:2606.06333](https://arxiv.org/abs/2606.06333)
- [CWDB+24] D. Chanin, J. Wilken-Smith, T. Dulka, H. Bhatnagar, S. Golechha, and J. Bloom, *A is for absorption: studying feature splitting and absorption in sparse autoencoders*, preprint, 2024. [arXiv:2409.14507](https://arxiv.org/abs/2409.14507)

*Related: [MAIS-O3](MAIS-O3.md) (the headline problem, where features are atomic) · [MAIS-O41](MAIS-O41.md) (the atomic two-feature phase diagram) · [MAIS-O43](MAIS-O43.md) (splits measured numerically).*
