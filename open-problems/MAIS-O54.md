# Are selection probabilities proportional to squared representation dimension?

*Open problem MAIS-O54 · posed in [MAIS-A5](../agendas/A5/MAIS-A5.pdf) as [Question 5.4](../agendas/A5/MAIS-A5.tex#L272) · Status: open.*

*Safety: interpretability — mechanistic interpretability · training dynamics · universality of circuits. Mathematics: representation theory · probability. Difficulty: ★★★ hard.*

A Gaussian random function on a finite group $G$ puts mean squared mass $d_\rho^2/|G|$ in the isotypic component of each irreducible representation $\rho$ of dimension $d_\rho$ — the Artin–Wedderburn block sizes. If each neuron of a trained network is won by its initially heaviest component, the fraction of neurons landing on each representation should be proportional to $d_\rho^2$. Is it?

The setting is the conjectured law of large numbers for multiplicities ([MAIS-O53](MAIS-O53.md)): a nonabelian finite group $G$, one hidden layer of $m$ neurons with quadratic activation, gradient flow on the cross-entropy loss over the full multiplication table with no weight decay, Gaussian initialization. Write $\mathcal{R}(G)$ for the conjugation classes $[\rho] = \lbrace \rho,\bar\rho\rbrace $ of nontrivial irreducibles and $\Pi_{[\rho]}$ for the isotypic projection of $\mathbb{R}^G$ onto the matrix coefficients of $[\rho]$. The conjectured constant $q_{[\rho]}$ is the large-width, late-time limit of the fraction of neurons whose weights are, up to a $\delta$ fraction of their centered energy, matrix coefficients of $[\rho]$ alone.

**Question ([MAIS-A5, Question 5.4](../agendas/A5/MAIS-A5.tex#L272)).** In the setting of [MAIS-A5, Conjecture 5.3], is $q_{[\rho]}$ proportional to $\dim \Pi_{[\rho]} = \sum_{\rho' \in [\rho]} d_{\rho'}^2$, i.e. to the dimension of the isotypic component?

Three heuristics suggest different answers, and deciding among them is part of the problem. Initial spectral mass suggests $q_{[\rho]} \propto d_\rho^2$, as above. The maximum-margin construction of Morwani et al. (for the $\ell_{2,3}$ norm, a different regularizer than this ensemble's) allocates neurons in proportions closer to $d_\rho^3$. And in the small-initialization limit, the alternating-gradient-flow picture of Kunin et al. predicts sequential acquisition ranked by initial spectral mass rather than a fixed proportion. The nearest theorem, He et al.'s uniform diversification across characters for abelian groups with no self-conjugate nontrivial character, concerns a Taylor-surrogate projected flow and one-dimensional representations only. For the definitions and the full context, see [MAIS-A5](../agendas/A5/MAIS-A5.pdf).

*Related: [MAIS-O53](MAIS-O53.md) (the conjecture defining $q_{[\rho]}$) · [MAIS-O55](MAIS-O55.md) (the two-class case $S_3$) · [MAIS-O5](MAIS-O5.md) (the headline selection law).*
