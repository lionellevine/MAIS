# Are selection probabilities proportional to squared representation dimension?

*Open problem MAIS-O54 · posed in [MAIS-A5](../agendas/A5/) as [Question 5.4](../agendas/A5/MAIS-A5.tex#L273) · Status: open.*

*Tags: interpretability · mechanistic interpretability · training dynamics · universality of circuits · representation theory · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A Gaussian random function on a finite group $G$ puts mean squared mass $d_\rho^2/|G|$ in the isotypic component of each irreducible representation $\rho$ of dimension $d_\rho$ — the Artin–Wedderburn block sizes. If each neuron of a trained network is won by its initially heaviest component, the fraction of neurons landing on each representation should be proportional to $d_\rho^2$. Is it?

The setting is the conjectured law of large numbers for multiplicities ([MAIS-O53](MAIS-O53.md)). Fix a nonabelian finite group $G$. The network is one hidden layer of $m$ neurons with quadratic activation: logits $f_\theta(a,b)(c) = \sum_{i=1}^m (u_i(a)+v_i(b))^2\ w_i(c)$ with weight vectors $u_i, v_i, w_i \in \mathbb{R}^G$. Training is gradient flow on the cross-entropy loss over the full multiplication table, with no weight decay, from independent $N(0,\tau^2)$ coordinates. Write $\mathcal{R}(G)$ for the conjugation classes $[\rho] = \lbrace \rho,\bar\rho\rbrace $ of nontrivial irreducibles and $\Pi_{[\rho]}$ for the isotypic projection of $\mathbb{R}^G$ onto the matrix coefficients of $[\rho]$. Neuron $i$ is $(\delta,[\rho])$-pure if, after centering each of $u_i, v_i, w_i$ by its mean, at least a $(1-\delta)$ fraction of their combined squared norm lies in the image of $\Pi_{[\rho]}$. Conjecture 5.3 asserts that the fraction of pure neurons converges (almost surely as $t \to \infty$ at each fixed width, then in probability as $m \to \infty$) to a constant $q_{[\rho]} > 0$, the same for every $\delta \in (0,\tfrac12)$ and every initialization scale $\tau$, with $\sum_{[\rho]} q_{[\rho]} = 1$.

**Question ([MAIS-A5, Question 5.4](../agendas/A5/MAIS-A5.tex#L273)).** In the setting of [MAIS-A5, Conjecture 5.3], is $q_{[\rho]}$ proportional to $\dim \Pi_{[\rho]} = \sum_{\rho' \in [\rho]} d_{\rho'}^2$, i.e. to the dimension of the isotypic component?

Three heuristics suggest different answers, and deciding among them is part of the problem. Initial spectral mass suggests $q_{[\rho]} \propto d_\rho^2$, as above. The maximum-margin construction of Morwani et al. (margin in the $\ell_{2,3}$ norm, a theory that does not yet predict this ensemble) allocates neurons in proportions closer to $d_\rho^3$. And in the small-initialization limit, the alternating-gradient-flow picture of Kunin et al. predicts sequential acquisition ranked by initial spectral mass rather than a fixed proportion. The nearest theorem, He et al.'s uniform diversification across characters for abelian groups with no self-conjugate nontrivial character, concerns a Taylor-surrogate projected flow and one-dimensional representations only. For the definitions and the full context, see [MAIS-A5](../agendas/A5/).

## References

- D. Morwani, B. L. Edelman, C.-A. Oncescu, R. Zhao, and S. Kakade, *Feature emergence via margin maximization: case studies in algebraic tasks*, ICLR 2024. [arXiv:2311.07568](https://arxiv.org/abs/2311.07568)
- D. Kunin, G. L. Marchetti, F. Chen, D. Karkada, J. B. Simon, M. R. DeWeese, S. Ganguli, and N. Miolane, *Alternating gradient flows: a theory of feature learning in two-layer neural networks*, NeurIPS 2025. [arXiv:2506.06489](https://arxiv.org/abs/2506.06489)
- J. He, L. Wang, F. Zhang, S. Chen, and Z. Yang, *Neural networks provably learn spectral representations for group composition*, preprint, 2026. [arXiv:2606.02993](https://arxiv.org/abs/2606.02993)

*Related: [MAIS-O53](MAIS-O53.md) (the conjecture defining $q_{[\rho]}$) · [MAIS-O55](MAIS-O55.md) (the two-class case $S_3$) · [MAIS-O5](MAIS-O5.md) (the headline selection law).*
