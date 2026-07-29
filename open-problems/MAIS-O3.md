# The geometry and identifiability of superposition

*Open problem MAIS-O3 · headline problem 3 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A3](../agendas/A3/) as [Problem 4.3](../agendas/A3/MAIS-A3.tex#L227) · Status: open.*

*Tags: interpretability · sparse autoencoders · mechanistic interpretability · superposition · statistics · optimization · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The working tool for reading concepts out of a neural network is the sparse autoencoder, an $\ell^1$-penalized dictionary learner. Every safety audit built on it inherits the answer to a mathematical question: when does the estimator return the network's true feature directions, and when does it return artifacts — two co-occurring concepts fused into one direction, the *feature absorption* documented empirically by Chanin et al. [[CWDB+24]](https://arxiv.org/abs/2409.14507)? Classical dictionary-learning theory answers only for independently occurring features, and real concepts co-occur. Even for this estimator the known guarantee, a theorem of Gribonval, Jenatton, and Bach [[GJB15]](https://arxiv.org/abs/1407.5155), is local: a minimum of the penalized objective exists near the true dictionary, with no control over faraway global minima.

The model, formalizing the superposition hypothesis of Elhage et al. [[EHOS+22]](https://arxiv.org/abs/2209.10652): activations are $y=\Phi x+\xi$ in $\mathbb{R}^n$, where the columns $v_1,\dots,v_m$ of $\Phi$ are unit feature directions; $x$ is a nonnegative code whose random support $S\subseteq\lbrace 1,\dots,m\rbrace$ has law $\pi$ (correlations allowed; the model is **$k$-sparse** if $\lvert S\rvert\le k$ almost surely), with nonzero coefficients drawn independently from a law $\nu$ on $(0,\infty)$; and $\xi$ is Gaussian noise with covariance $\sigma^2 I_n$. Write $\mu(\Phi)=\max_{i\neq j}\lvert\langle v_i,v_j\rangle\rvert$ for the coherence and $r(\pi)=\max_{i\neq j}\Pr(j\in S\mid i\in S)$ for the **co-occurrence ratio**, near one when some feature almost always fires together with another. The estimator learns a dictionary $\Psi$ with $M$ unit columns $u_1,\dots,u_M$ by minimizing reconstruction error plus an $\ell^1$ penalty on the best nonnegative code,

$$F_\lambda(\Psi)\;=\;\mathbb{E}\,\min_{z\in\mathbb{R}^M_{\ge 0}}\Bigl[\tfrac12\lVert y-\Psi z\rVert^2+\lambda\lVert z\rVert_1\Bigr],$$

and the empirical objective replaces the expectation by an average over $N$ samples. Say $\Psi$ **$\varepsilon$-recovers** $\Phi$ if some injection $\tau$ has $\langle u_{\tau(i)},v_i\rangle\ge 1-\varepsilon$ for all $i$. Call an atom **live** if with positive probability some minimizing code gives it positive mass; a live atom $u_j$ is an **$(\varepsilon,\delta)$-merge** of features $i\neq i'$ if $\lVert u_j-\alpha v_i-\beta v_{i'}\rVert\le\varepsilon$ for some $\alpha,\beta\ge\delta$ while $\langle u_j,v_i\rangle\le 1-\delta$ and $\langle u_j,v_{i'}\rangle\le 1-\delta$: near the positive span of the two features, bounded away from each. Two small propositions in the agenda show both behaviors occur already for two features: nested supports (one feature never firing without the other) force merging, solo firing restores recovery.

**Problem ([MAIS-A3, Problem 4.3](../agendas/A3/MAIS-A3.tex#L227)).** Fix $n,m,k$ and consider $k$-sparse superposition models $\mathcal S=(\Phi,\pi,\nu,\sigma)$ and the estimator $F_\lambda$ with $M=m$. Obtain necessary and sufficient bounds in terms of the coherence $\mu(\Phi)$, the sparsity $k$, the marginal rates $\Pr(i\in S)$, the co-occurrence ratio $r(\pi)$, the solo-firing rates $\Pr(S=\lbrace i\rbrace \mid i\in S)$, the coefficient law $\nu$, the noise level $\sigma$, and the penalty $\lambda$:

1. *(Recovery region.)* Conditions under which every global minimizer of $F_\lambda$ $\varepsilon$-recovers $\Phi$, with an explicit $\varepsilon=\varepsilon(\mu,k,\lambda,\sigma)\to0$ as $\lambda,\sigma\to0$.
2. *(Merging region.)* Conditions under which every global minimizer contains an $(\varepsilon,\delta)$-merge of some pair of features, with $\varepsilon$ explicit as in (1) and $\delta$ bounded below in terms of the pair's angle and co-occurrence; to determine *which* pairs merge, the answer may depend on the full Gram matrix of $\Phi$ and the full support law $\pi$.
3. *(Sample complexity.)* In the recovery region, a bound $N$ such that $N$ samples suffice for every global minimizer of the empirical objective to $\varepsilon$-recover $\Phi$ with probability $1-\eta$. Is $N$ polynomial in $m$ when the marginal rates are bounded below by an inverse polynomial in $m$?

For the precise model and estimator definitions and the two bracketing propositions, see [MAIS-A3](../agendas/A3/).

## References

- [GJB15] R. Gribonval, R. Jenatton, and F. Bach, *Sparse and spurious: dictionary learning with noise and outliers*, IEEE Transactions on Information Theory 61 (2015), 6298–6319. [arXiv:1407.5155](https://arxiv.org/abs/1407.5155)
- [CWDB+24] D. Chanin, J. Wilken-Smith, T. Dulka, H. Bhatnagar, S. Golechha, and J. Bloom, *A is for absorption: studying feature splitting and absorption in sparse autoencoders*, 2024. [arXiv:2409.14507](https://arxiv.org/abs/2409.14507)
- [EHOS+22] N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread, Anthropic, 2022. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)

*Related: [MAIS-O36](MAIS-O36.md) (recovery under independent supports) · [MAIS-O41](MAIS-O41.md) (the two-feature phase diagram, a starter) · [MAIS-O4](MAIS-O4.md) (training the network so recovery succeeds).*
