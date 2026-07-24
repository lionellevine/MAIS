# The geometry and identifiability of superposition

*Open problem MAIS-O3 · headline problem 3 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A3](../agendas/A3/) as [Problem 4.3](../agendas/A3/MAIS-A3.tex#L226) · Status: open.*

*Safety: interpretability — sparse autoencoders · mechanistic interpretability · superposition. Mathematics: statistics · optimization · probability. Difficulty: ★★★ hard.*

The working tool for reading concepts out of a neural network is the sparse autoencoder, an $\ell^1$-penalized dictionary learner. Every safety audit built on it inherits the answer to a mathematical question: when does the estimator return the network's true feature directions, and when does it return artifacts — two co-occurring concepts fused into one direction? Classical dictionary-learning theory answers only for independently occurring features, and real concepts co-occur.

The model: activations are $y=\Phi x+\xi$, where the columns $v_1,\dots,v_m$ of $\Phi$ are unit feature directions, $x$ is a sparse nonnegative code whose random support $S$ has law $\pi$ (correlations allowed) and whose nonzero coefficients have law $\nu$, and $\xi$ is noise of level $\sigma$. The estimator minimizes reconstruction error plus $\lambda \lVert\cdot\rVert_1$ over dictionaries $\Psi$ with unit columns; write $F_\lambda$ for this objective and $\mu(\Phi)=\max_{i\neq j}\lvert\langle v_i,v_j\rangle\rvert$ for the coherence. Say $\Psi$ **$\varepsilon$-recovers** $\Phi$ if some injection $\tau$ has $\langle u_{\tau(i)},v_i\rangle\ge 1-\varepsilon$ for all $i$; an atom is a **merge** of two features if it lies near their positive span while staying bounded away from each. Two small propositions in the agenda show both behaviors occur already for two features: nested supports force merging, solo firing restores recovery.

**Problem ([MAIS-A3, Problem 4.3](../agendas/A3/MAIS-A3.tex#L226)).** Fix $n,m,k$ and consider $k$-sparse superposition models $\mathcal S=(\Phi,\pi,\nu,\sigma)$ and the estimator $F_\lambda$ with $M=m$. Obtain necessary and sufficient bounds in terms of the coherence $\mu(\Phi)$, the sparsity $k$, the marginal rates $\Pr(i\in S)$, the co-occurrence ratio $r(\pi)$, the solo-firing rates $\Pr(S=\lbrace i\rbrace \mid i\in S)$, the coefficient law $\nu$, the noise level $\sigma$, and the penalty $\lambda$:

1. *(Recovery region.)* Conditions under which every global minimizer of $F_\lambda$ $\varepsilon$-recovers $\Phi$, with an explicit $\varepsilon=\varepsilon(\mu,k,\lambda,\sigma)\to0$ as $\lambda,\sigma\to0$.
2. *(Merging region.)* Conditions under which every global minimizer contains a merge of some pair of features, with the merge quantified in terms of the pair's angle and co-occurrence; to determine *which* pairs merge, the answer may depend on the full Gram matrix of $\Phi$ and the full support law $\pi$.
3. *(Sample complexity.)* In the recovery region, a bound $N$ such that $N$ samples suffice for every global minimizer of the empirical objective to $\varepsilon$-recover $\Phi$ with probability $1-\eta$. Is $N$ polynomial in $m$ when the marginal rates are bounded below by an inverse polynomial in $m$?

For the precise model and estimator definitions and the two bracketing propositions, see [MAIS-A3](../agendas/A3/).

*Related: [MAIS-O36](MAIS-O36.md) (recovery under independent supports) · [MAIS-O41](MAIS-O41.md) (the two-feature phase diagram, a starter) · [MAIS-O4](MAIS-O4.md) (training the network so recovery succeeds).*
