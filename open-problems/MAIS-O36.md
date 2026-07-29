# Global ℓ¹ dictionary recovery under independent supports

*Open problem MAIS-O36 · posed in [MAIS-A3](../agendas/A3/) as [Conjecture 4.4](../agendas/A3/MAIS-A3.tex#L238) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · probability · optimization · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

When a sparse autoencoder converges, is the dictionary it finds the one that generated the data? The known guarantee for the $\ell^1$-penalized estimator is local: Gribonval, Jenatton, and Bach [[GJB15]](../references/GJB15.md) proved that a minimum exists *near* the true dictionary, leaving open whether a merged or rotated dictionary far away scores even better. This conjecture asserts that in the cleanest population case — features firing independently, dictionary incoherent — no such faraway global minimizer exists.

The model: data $y=\Phi x+\xi$, where $\Phi$ belongs to $U_{n,m}$, the set of $n\times m$ matrices with unit columns $v_1,\dots,v_m$, with coherence $\mu(\Phi)=\max_{i\neq j}\lvert\langle v_i,v_j\rangle\rvert$; the support $S\subseteq[m]$ of the nonnegative code $x$ has law $\pi$; the nonzero coefficients are drawn independently from a law $\nu$ on $(0,\infty)$; and $\xi$ is Gaussian noise of level $\sigma\ge0$. The estimator minimizes the population objective $F_\lambda(\Psi)=\mathbb{E}\ \min_{z\ge0}\bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\bigr]$ over $\Psi\in U_{n,m}$ with columns $u_1,\dots,u_m$. Say $\Psi$ **$\varepsilon$-recovers** $\Phi$ if some injection $\tau$ has $\langle u_{\tau(i)},v_i\rangle\ge1-\varepsilon$ for all $i$.

**Conjecture ([MAIS-A3, Conjecture 4.4](../agendas/A3/MAIS-A3.tex#L238)).** There exist absolute constants $c,C>0$ with $Cc<1$ and the following property. Let $m>n$, let $\Phi\in U_{n,m}$ have coherence $\mu$, let $\pi$ be the product distribution in which each $i\in[m]$ belongs to $S$ independently with probability $p>0$, let $\nu=\mathrm{Unif}[1,2]$, and let $\sigma=0$. If

$$\mu\ \bigl(pm+\log m\bigr)\ \le\ c \qquad\text{and}\qquad pm+\log m\ \le\ c\ \sqrt{n/\log m},$$

then for every $\lambda\in(0,c)$, every global minimizer of $F_\lambda$ over $U_{n,m}$ $(C\lambda)$-recovers $\Phi$.

In words: if the expected number of active features per sample, $pm$ (plus $\log m$), is small compared to $\sqrt{n/\log m}$, and the coherence is small compared to $1/(pm+\log m)$, then every global minimizer places an atom within angle $\arccos(1-C\lambda)$ of each true feature. For a uniformly random $\Phi$ the coherence is $O(\sqrt{(\log m)/n})$ with high probability, so both conditions reduce to the density bound alone. The overcompleteness hypothesis $m>n$ is necessary: the agenda's Remark 4.6 gives a two-feature orthonormal counterexample in which slanted atoms beat the true dictionary at every small penalty.

For the full model, the local-minimum literature, and the globally identifiable volume-regularized alternative of Hu and Huang [HH23], extended to overcomplete dictionaries by Sun and Huang [SH25], see [MAIS-A3](../agendas/A3/).

## References

- [[GJB15]](../references/GJB15.md) R. Gribonval, R. Jenatton, and F. Bach, *Sparse and spurious: dictionary learning with noise and outliers*, IEEE Transactions on Information Theory 61 (2015), 6298–6319. [arXiv:1407.5155](https://arxiv.org/abs/1407.5155)
- [HH23] J. Hu and K. Huang, *Global identifiability of $\ell^1$-based dictionary learning via matrix volume optimization*, Advances in Neural Information Processing Systems 36 (2023), 36165–36186.
- [SH25] Y. Sun and K. Huang, *Global identifiability of overcomplete dictionary learning via $\ell^1$ and volume minimization*, International Conference on Learning Representations (ICLR) 2025.

*Related: [MAIS-O3](MAIS-O3.md) (the headline problem: correlated supports) · [MAIS-O41](MAIS-O41.md) (the exact two-feature phase diagram, a starter) · [MAIS-O39](MAIS-O39.md) (does the same conclusion hold for the amortized encoder?) · [MAIS-O43](MAIS-O43.md) (measure the thresholds numerically).*
