# How many Fourier frequencies do modular-addition networks use?

*Open problem MAIS-O52 · posed in [MAIS-A5](../agendas/A5/) as [Problem 5.2](../agendas/A5/MAIS-A5.tex#L252) · Status: open.*

*Tags: interpretability · mechanistic interpretability · universality of circuits · training dynamics · probability · dynamical systems · harmonic analysis. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

A network trained on addition mod 113 expressed its outputs through five of the 56 available Fourier frequencies. Yet Morwani, Edelman, Oncescu, Zhao, and Kakade [[MEOZK24]](https://arxiv.org/abs/2311.07568) proved that for a quadratic activation, the networks maximizing the margin in the $\ell_{2,3}$ norm adapted to the architecture (take the $\ell^2$ norm of each neuron's concatenated weights, then the $\ell^3$ norm across neurons) use *all* the frequencies, one per neuron. Sparse or dense: which regime does actual training occupy as the modulus grows? Whether trained networks are compressible into a few interpretable features, or spread over extensively many, is a basic quantitative question for mechanistic interpretability.

Take $G = C_p = \mathbb{Z}/p\mathbb{Z}$ and the one-hidden-layer network of width $m$ with activation $\sigma = \mathrm{ReLU}$ and logits $f_\theta(a,b)(c) = \sum_{i=1}^m \sigma(u_i(a)+v_i(b))\ w_i(c)$, where each neuron carries three functions $u_i, v_i, w_i \in \mathbb{R}^G$. Training is gradient flow for the cross-entropy loss over the full addition table plus weight decay $\lambda\Vert \theta\Vert ^2$, from independent $N(0,\tau^2)$ coordinates; since the rectifier is only piecewise smooth, the flow is read as a differential inclusion: a Clarke trajectory is an absolutely continuous path with $\dot\theta(t) \in -\partial L(\theta(t))$ for almost every $t$, where $L$ is the regularized loss and $\partial$ its Clarke subdifferential (the convex hull of limits of gradients at nearby points of differentiability). Such trajectories exist from every initial condition but need not be unique, so statements are asserted for every measurable selection of Clarke trajectories. The logits are centered by subtracting, for each input pair $(a,b)$, their mean over $c$. Each frequency $\zeta \in \lbrace 1,\dots,(p-1)/2\rbrace $ has a spectral weight $b_\zeta(\theta)^2$: the squared $L^2(G^3)$ norm of the orthogonal projection of the centered logits onto the span of the two conjugate characters $(a,b,c) \mapsto e^{\pm 2\pi i \zeta(a+b-c)/p}$, divided by the squared norm of the centered logits. The **spectral count** $N_\delta(\theta)$ is the smallest cardinality of a set $S$ of frequencies with $\sum_{\zeta \in S} b_\zeta(\theta)^2 \ge (1-\delta) \sum_\zeta b_\zeta(\theta)^2$: the number of frequencies needed to capture a $(1-\delta)$ fraction of the spectral mass. Statements hold for Lebesgue-almost every small $\delta$.

**Problem ([MAIS-A5, Problem 5.2](../agendas/A5/MAIS-A5.tex#L252)).** Let $p \to \infty$ through odd primes, $G = C_p$, $\sigma = \mathrm{ReLU}$, $m = \lceil C_0\  p \rceil$, $\lambda = \lambda_0 > 0$, and $\tau = \tau_0 p^{-1/2}$ with $C_0, \lambda_0, \tau_0 > 0$ fixed. Fix a small $\delta$ and determine

$$\limsup_{p \to \infty} \  \limsup_{t \to \infty} \  \frac{\mathbb{E}\  N_\delta(\theta(t))}{p}\ :$$

is it zero (*sparse* regime, as observed experimentally) or positive (*dense* regime, as in the $\ell_{2,3}$ maximum-margin model and quadratic experiments of Morwani et al.)? In the sparse case, determine the growth rate of $\limsup_t \mathbb{E} N_\delta$ in $p$. (Posed per measurable selection of Clarke trajectories; whether the answer depends on the selection is part of the problem.)

The empirical record is too thin even to conjecture the growth rate: essentially $N_{0.05} \approx 5$ at $p = 113$ for the transformer of Nanda et al. [[NCLSS23]](https://arxiv.org/abs/2301.05217), and 3–15 key frequencies across the networks of Chughtai et al. [[CCN23]](https://arxiv.org/abs/2302.03025). A coset-based heuristic of McCracken et al. [[MMLPL25]](https://arxiv.org/abs/2505.18266) suggests order $\log p$ features for deeper networks; whether shallow trained networks track any such rate is open. For the ensemble conventions and the surrounding results, see [MAIS-A5](../agendas/A5/).

## References

- [MEOZK24] D. Morwani, B. L. Edelman, C.-A. Oncescu, R. Zhao, and S. Kakade, *Feature emergence via margin maximization: case studies in algebraic tasks*, ICLR 2024. [arXiv:2311.07568](https://arxiv.org/abs/2311.07568)
- [NCLSS23] N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, *Progress measures for grokking via mechanistic interpretability*, ICLR 2023. [arXiv:2301.05217](https://arxiv.org/abs/2301.05217)
- [CCN23] B. Chughtai, L. Chan, and N. Nanda, *A toy model of universality: reverse engineering how networks learn group operations*, ICML 2023. [arXiv:2302.03025](https://arxiv.org/abs/2302.03025)
- [MMLPL25] G. McCracken, G. Moisescu-Pareja, V. Letourneau, D. Precup, and J. Love, *Uncovering a universal abstract algorithm for modular addition in neural networks*, preprint, 2025. [arXiv:2505.18266](https://arxiv.org/abs/2505.18266)

*Related: [MAIS-O5](MAIS-O5.md) (the full selection law this counts) · [MAIS-O58](MAIS-O58.md) (which $k$-sets of frequencies, not how many) · [MAIS-O61](MAIS-O61.md) (measure the counts at small $p$).*
