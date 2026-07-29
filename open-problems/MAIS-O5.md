# Representation theory of learned circuits

*Open problem MAIS-O5 · headline problem 5 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A5](../agendas/A5/) as [Problem 5.1](../agendas/A5/MAIS-A5.tex#L235) · Status: open.*

*Tags: interpretability · mechanistic interpretability · universality of circuits · training dynamics · dynamical systems · probability · representation theory. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Train a small network to multiply in $S_5$ and read off which irreducible representations its weights use. Chughtai, Chan, and Nanda did this four times from four random initializations and got four answers: {sign, standard, standard⊗sign, a 5-dimensional}; {sign, standard}; {sign, standard, the other 5-dimensional}; {sign, standard}. The algorithm family is universal — logits are positive combinations of characters $\chi_\rho(abc^{-1})$, peaked at the correct product — but the instance is chosen by the seed. Interpretability findings transfer across training runs only to the extent that this choice is predictable, so the problem asks for its law.

The network is one hidden layer of $m$ neurons: a parameter $\theta = (u_i, v_i, w_i)_{i=1}^m$ assigns three functions in $\mathbb{R}^G$ to each neuron, and the logits are $f_\theta(a,b)(c) = \sum_{i=1}^m \sigma(u_i(a)+v_i(b))\ w_i(c)$, the answer to "what is $ab$?" being the maximizing $c$. Training is gradient flow for the cross-entropy loss over the full multiplication table plus weight decay $\lambda\Vert \theta\Vert ^2$, from independent $N(0,\tau^2)$ coordinates; $\mathcal{T}(G,\sigma,m,\lambda,\tau)$ denotes this random trajectory $(\theta(t))_{t\ge0}$. For $\sigma = \mathrm{ReLU}$ the loss is only piecewise smooth, and a trajectory means a solution of the differential inclusion $\dot\theta(t) \in -\partial L(\theta(t))$, where $L$ is the loss and $\partial$ its Clarke subdifferential; such **Clarke trajectories** exist from every initial condition but need not be unique, so statements about the ReLU ensemble are asserted for every measurable assignment of one trajectory to each initial condition.

The observable is black-box. Write $\mathcal{R}(G)$ for the conjugation classes $[\rho]=\lbrace \rho,\bar\rho\rbrace $ of nontrivial irreducible representations; the functions $\psi_\rho(a,b,c)=\chi_\rho(abc^{-1})$ are orthogonal in $L^2(G^3)$, and the **spectral weight** $b_{[\rho]}(\theta)^2$ is the fraction of the squared $L^2$ norm of the centered logits $\tilde\ell_\theta(a,b,c) = f_\theta(a,b)(c) - \frac{1}{\vert G\vert }\sum_{c'} f_\theta(a,b)(c')$ (each input pair's mean over answers subtracted, which removes the trivial representation) carried by the span of $\psi_{\rho'}$, $\rho'\in[\rho]$. The **key set** is $K_\varepsilon(\theta)=\lbrace [\rho] : b_{[\rho]}(\theta)\ge\varepsilon\rbrace $, the **selection law** at time $t$ is $\mu_t = \operatorname{Law}(K_\varepsilon(\theta(t)))$ on subsets of $\mathcal{R}(G)$, and $\mu_\infty$ is its weak limit as $t\to\infty$ when that limit exists. Statements hold for Lebesgue-almost every sufficiently small $\varepsilon$.

**Problem ([MAIS-A5, Problem 5.1](../agendas/A5/MAIS-A5.tex#L235)).** Fix a finite group $G$, $\sigma \in \lbrace x^2, \mathrm{ReLU}\rbrace $, a width $m$, and $\lambda, \tau > 0$, and consider $\mathcal{T}(G,\sigma,m,\lambda,\tau)$ (for $\sigma = \mathrm{ReLU}$, under every measurable selection of Clarke trajectories).

- (a) Prove that the limiting selection law $\mu_\infty$ exists.
- (b) Decide whether $\mu_\infty$ is a point mass.
- (c) (*Existential*, overriding the fixed data above.) Compute $\mu_\infty$ for at least one nonabelian $G$, one activation, and one explicit parameter regime $(m, \lambda, \tau, \varepsilon)$.

Parts (a) and (b) are posed for each fixed tuple separately. A point mass means deterministic selection; two explicitly charged sets with their probabilities would establish genuinely random selection. One constraint is proved for the quadratic activation: the selection law is invariant under the outer automorphism group of $G$. For $G = C_p$ with $p$ prime, that group permutes the nontrivial characters (the *frequencies*) transitively, so each frequency belongs to the key set with the same probability. The nearest theorems live in idealized regimes — maximum margin in the $\ell_{2,3}$ norm, or a Taylor-surrogate projected flow — and do not predict this ensemble; the smallest case with genuine competition, $C_5$ at width two with the decay switched off, is already open. Definitions, known results, and starter cases are collected in [MAIS-A5](../agendas/A5/).

## References

- B. Chughtai, L. Chan, and N. Nanda, *A toy model of universality: reverse engineering how networks learn group operations*, ICML 2023. [arXiv:2302.03025](https://arxiv.org/abs/2302.03025)
- N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, *Progress measures for grokking via mechanistic interpretability*, ICLR 2023. [arXiv:2301.05217](https://arxiv.org/abs/2301.05217)
- D. Morwani, B. L. Edelman, C.-A. Oncescu, R. Zhao, and S. Kakade, *Feature emergence via margin maximization: case studies in algebraic tasks*, ICLR 2024. [arXiv:2311.07568](https://arxiv.org/abs/2311.07568)

*Related: [MAIS-O59](MAIS-O59.md) (the $C_5$ width-two foothold) · [MAIS-O57](MAIS-O57.md) (random selection for $S_5$ at width 128) · [MAIS-O53](MAIS-O53.md) (neuron-level multiplicities) · [MAIS-O61](MAIS-O61.md) (pilot measurement of the law).*
