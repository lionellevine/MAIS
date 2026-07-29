# Are selection probabilities proportional to squared representation dimension?

*Open problem MAIS-O54 · posed in [MAIS-A5](../agendas/A5/) as [Question 5.4](../agendas/A5/MAIS-A5.tex#L273) · Status: open.*

*Tags: interpretability · mechanistic interpretability · training dynamics · universality of circuits · representation theory · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A Gaussian random function on a finite group $G$ puts mean squared mass $d_\rho^2/|G|$ in the isotypic component of each irreducible representation $\rho$ of dimension $d_\rho$ — the Artin–Wedderburn block sizes. If each neuron of a trained network is won by its initially heaviest component, the fraction of neurons landing on each representation should be proportional to $d_\rho^2$. Is it? A yes would make the census of circuits in a trained network predictable in advance from the symmetry of the task — universality in its most quantitative form.

The setting is the conjectured law of large numbers for multiplicities ([MAIS-O53](MAIS-O53.md)): a nonabelian finite group $G$, one hidden layer of $m$ neurons with quadratic activation, gradient flow on the cross-entropy loss over the full multiplication table with no weight decay, Gaussian initialization. Write $[\rho] = \lbrace \rho,\bar\rho\rbrace $ for the conjugation classes of nontrivial irreducibles and $\Pi_{[\rho]}$ for the isotypic projection of $\mathbb{R}^G$ onto the matrix coefficients of $[\rho]$. The conjectured constant $q_{[\rho]}$ is the large-width, late-time limit of the fraction of neurons whose weights are, up to a small fraction of their centered energy, matrix coefficients of $[\rho]$ alone; the exact model and purity quantifiers are in [MAIS-A5, Conjecture 5.3](../agendas/A5/MAIS-A5.tex#L264).

**Question ([MAIS-A5, Question 5.4](../agendas/A5/MAIS-A5.tex#L273)).** In the setting of [MAIS-A5, Conjecture 5.3], is $q_{[\rho]}$ proportional to $\dim \Pi_{[\rho]} = \sum_{\rho' \in [\rho]} d_{\rho'}^2$, i.e. to the dimension of the isotypic component?

Three heuristics suggest different answers, and deciding among them is part of the problem. Initial spectral mass suggests $q_{[\rho]} \propto d_\rho^2$, as above. The maximum-margin construction of Morwani et al. [[MEOZK24]](../references/MEOZK24.md) (margin in the $\ell_{2,3}$ norm, a theory that does not yet predict this ensemble) allocates neurons in proportions closer to $d_\rho^3$. And in the small-initialization limit, the alternating-gradient-flow picture of Kunin et al. [[KMCK+25]](https://arxiv.org/abs/2506.06489) predicts sequential acquisition ranked by initial spectral mass rather than a fixed proportion. The nearest theorem, He et al.'s uniform diversification across characters [[HWZCY26]](../references/HWZCY26.md) for abelian groups with no self-conjugate nontrivial character, concerns a Taylor-surrogate projected flow and one-dimensional representations only. For the definitions and the full context, see [MAIS-A5](../agendas/A5/).

## References

- [[MEOZK24]](../references/MEOZK24.md) D. Morwani, B. L. Edelman, C.-A. Oncescu, R. Zhao, and S. Kakade, *Feature emergence via margin maximization: case studies in algebraic tasks*, ICLR 2024. [arXiv:2311.07568](https://arxiv.org/abs/2311.07568)
- [KMCK+25] D. Kunin, G. L. Marchetti, F. Chen, D. Karkada, J. B. Simon, M. R. DeWeese, S. Ganguli, and N. Miolane, *Alternating gradient flows: a theory of feature learning in two-layer neural networks*, NeurIPS 2025. [arXiv:2506.06489](https://arxiv.org/abs/2506.06489)
- [[HWZCY26]](../references/HWZCY26.md) J. He, L. Wang, F. Zhang, S. Chen, and Z. Yang, *Neural networks provably learn spectral representations for group composition*, preprint, 2026. [arXiv:2606.02993](https://arxiv.org/abs/2606.02993)

*Related: [MAIS-O53](MAIS-O53.md) (the conjecture defining $q_{[\rho]}$) · [MAIS-O55](MAIS-O55.md) (the two-class case $S_3$) · [MAIS-O5](MAIS-O5.md) (the headline selection law).*
