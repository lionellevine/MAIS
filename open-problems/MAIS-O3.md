# The geometry and identifiability of superposition

*Open problem MAIS-O3 · headline problem 3 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A3](../agendas/A3/) as [Problem 4.3](../agendas/A3/MAIS-A3.tex#L227) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · statistics · optimization · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The working tool for reading concepts out of a neural network is the sparse autoencoder, an $\ell^1$-penalized dictionary learner. Every safety audit built on it inherits the answer to a mathematical question: when does the estimator return the network's true feature directions, and when does it return artifacts — two co-occurring concepts fused into one direction, the *feature absorption* documented empirically by Chanin et al. [[CWDB+24]](https://arxiv.org/abs/2409.14507)? Classical dictionary-learning theory answers only for independently occurring features, and real concepts co-occur. Even for this estimator the known guarantee, a theorem of Gribonval, Jenatton, and Bach [[GJB15]](https://arxiv.org/abs/1407.5155), is local: a minimum of the penalized objective exists near the true dictionary, with no control over faraway global minima.

The model, formalizing the superposition hypothesis of Elhage et al. [[EHOS+22]](../references/EHOS+22.md): activations are $y=\Phi x+\xi$, where the columns $v_1,\dots,v_m$ of $\Phi$ are unit feature directions, $x$ is a nonnegative code whose random support $S$ has law $\pi$ (correlations allowed; **$k$-sparse** means at most $k$ features fire at once) and whose nonzero coefficients have law $\nu$, and $\xi$ is noise of level $\sigma$. The estimator minimizes reconstruction error plus $\lambda\lVert\cdot\rVert_1$ over dictionaries $\Psi$ with $M$ unit columns; write $F_\lambda$ for this objective, $\mu(\Phi)=\max_{i\neq j}\lvert\langle v_i,v_j\rangle\rvert$ for the coherence, and $r(\pi)=\max_{i\neq j}\Pr(j\in S\mid i\in S)$ for the **co-occurrence ratio**, near one when some feature almost always fires together with another. Say $\Psi$ **$\varepsilon$-recovers** $\Phi$ if some injection $\tau$ matches each $v_i$ to a column $u_{\tau(i)}$ of $\Psi$ with $\langle u_{\tau(i)},v_i\rangle\ge 1-\varepsilon$; a column is an **$(\varepsilon,\delta)$-merge** of two features if it lies within $\varepsilon$ of their positive span with both coefficients at least $\delta$, while its inner product with each feature stays below $1-\delta$ — near the fused direction, bounded away from either feature alone (exact quantifiers in the agenda). Two small propositions in [MAIS-A3](../agendas/A3/) show both behaviors occur already for two features: nested supports (one feature never firing without the other) force merging, solo firing restores recovery.

**Problem ([MAIS-A3, Problem 4.3](../agendas/A3/MAIS-A3.tex#L227)).** Fix $n,m,k$ and consider $k$-sparse superposition models $\mathcal S=(\Phi,\pi,\nu,\sigma)$ and the estimator $F_\lambda$ with $M=m$. Obtain necessary and sufficient bounds in terms of the coherence $\mu(\Phi)$, the sparsity $k$, the marginal rates $\Pr(i\in S)$, the co-occurrence ratio $r(\pi)$, the solo-firing rates $\Pr(S=\lbrace i\rbrace \mid i\in S)$, the coefficient law $\nu$, the noise level $\sigma$, and the penalty $\lambda$:

1. *(Recovery region.)* Conditions under which every global minimizer of $F_\lambda$ $\varepsilon$-recovers $\Phi$, with an explicit $\varepsilon=\varepsilon(\mu,k,\lambda,\sigma)\to0$ as $\lambda,\sigma\to0$.
2. *(Merging region.)* Conditions under which every global minimizer contains an $(\varepsilon,\delta)$-merge of some pair of features, with $\varepsilon$ explicit as in (1) and $\delta$ bounded below in terms of the pair's angle and co-occurrence; to determine *which* pairs merge, the answer may depend on the full Gram matrix of $\Phi$ and the full support law $\pi$.
3. *(Sample complexity.)* In the recovery region, a bound $N$ such that $N$ samples suffice for every global minimizer of the empirical objective to $\varepsilon$-recover $\Phi$ with probability $1-\eta$. Is $N$ polynomial in $m$ when the marginal rates are bounded below by an inverse polynomial in $m$?

For the precise model and estimator definitions and the two bracketing propositions, see [MAIS-A3](../agendas/A3/).

## References

- [GJB15] R. Gribonval, R. Jenatton, and F. Bach, *Sparse and spurious: dictionary learning with noise and outliers*, IEEE Transactions on Information Theory 61 (2015), 6298–6319. [arXiv:1407.5155](https://arxiv.org/abs/1407.5155)
- [CWDB+24] D. Chanin, J. Wilken-Smith, T. Dulka, H. Bhatnagar, S. Golechha, and J. Bloom, *A is for absorption: studying feature splitting and absorption in sparse autoencoders*, 2024. [arXiv:2409.14507](https://arxiv.org/abs/2409.14507)
- [[EHOS+22]](../references/EHOS+22.md) N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread, Anthropic, 2022. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)

*Related: [MAIS-O36](MAIS-O36.md) (recovery under independent supports) · [MAIS-O41](MAIS-O41.md) (the two-feature phase diagram, a starter) · [MAIS-O4](MAIS-O4.md) (training the network so recovery succeeds).*
