# Neuron purity and representation selection for S₃ networks

*Open problem MAIS-O55 · posed in [MAIS-A5](../agendas/A5/) as [Problem 5.5](../agendas/A5/MAIS-A5.tex#L280) · Status: open.*

*Tags: interpretability · mechanistic interpretability · training dynamics · universality of circuits · monosemanticity · dynamical systems · representation theory · probability. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The smallest nonabelian group keeps the whole selection question on one line: $S_3$ has two nontrivial irreducible representations, the sign $\mathrm{sgn}$ (dimension 1) and the standard $\mathrm{std}$ (dimension 2, the only faithful one), so a trained network's visible representations form one of just four subsets of $\lbrace \mathrm{sgn}, \mathrm{std}\rbrace $. Which subset does training choose, and does every neuron commit to a single representation?

The network is one hidden layer of $m$ neurons: logits $f_\theta(a,b)(c) = \sum_{i=1}^m \sigma(u_i(a)+v_i(b))\ w_i(c)$ with $u_i,v_i,w_i \in \mathbb{R}^{S_3}$, trained by gradient flow on the cross-entropy loss over the full multiplication table plus weight decay $\lambda\Vert \theta\Vert ^2$, from independent $N(0,\tau^2)$ coordinates; this ensemble is $\mathcal{T}(S_3,\sigma,m,\lambda,\tau)$, and for the rectifier the flow is read as a differential inclusion with a measurable selection of Clarke trajectories. Neuron $i$ is **$(\delta,[\rho])$-pure** if, after centering, at least a $(1-\delta)$ fraction of the combined squared norm of $u_i,v_i,w_i$ lies in the isotypic component of $[\rho]$. The **key set** $K_\varepsilon(\theta)$ is the set of classes whose characters, evaluated at $abc^{-1}$, carry at least an $\varepsilon$ fraction of the centered logits' $L^2$ norm; the **selection law** $\mu_t$ is the distribution of $K_\varepsilon(\theta(t))$, with weak limit $\mu_\infty$, asserted for Lebesgue-almost every small $\varepsilon$.

**Problem ([MAIS-A5, Problem 5.5](../agendas/A5/MAIS-A5.tex#L280)).** Consider $\mathcal{T}(S_3, \sigma, m, \lambda, \tau)$ with $\sigma \in \lbrace x^2, \mathrm{ReLU}\rbrace $, $m \ge 100$, $\lambda > 0$, $\tau > 0$.

- (a) (*Purity.*) For $\sigma = \mathrm{ReLU}$: prove or refute that almost surely every neuron ends pure or silent. Precisely: each neuron $i$ either is eventually *inactive* — $u_i(a) + v_i(b) < 0$ for all $(a,b)$, so that it contributes to no logit — or there is a class $[\rho] \in \lbrace \mathrm{sgn}, \mathrm{std}\rbrace $ such that, for every $\delta \in (0,\tfrac12)$, neuron $i$ is $(\delta,[\rho])$-pure for all large $t$.
- (b) (*Selection.*) For each $\sigma \in \lbrace x^2, \mathrm{ReLU}\rbrace $: prove that the limiting selection law $\mu_\infty$ exists, and determine it as a measure on the four subsets of $\lbrace \mathrm{sgn}, \mathrm{std}\rbrace $. In particular, decide whether $\mu_\infty(\lbrace S : \mathrm{std} \in S\rbrace ) = 1$ and whether $\mu_\infty(\lbrace S : \mathrm{sgn} \in S\rbrace ) < 1$.

Neither hypothesis in (a) can be dropped: with positive probability a neuron is inactive at initialization, and then its gradient is pure weight decay, so it shrinks radially and stays inactive, and impure, forever; and at $\delta \ge \tfrac12$ one neuron can be pure for both classes at once. For maximum margin in the $\ell_{2,3}$ norm, Morwani et al. prove every nonzero neuron pure with both representations present — a different regularizer, so a motivation rather than a prediction here. For the exact-loss, rectifier, and weight-decay regimes nothing is proved; see [MAIS-A5](../agendas/A5/).

*Related: [MAIS-O56](MAIS-O56.md) (the vanishing-decay limit of this selection law) · [MAIS-O53](MAIS-O53.md) (multiplicities at large width) · [MAIS-O61](MAIS-O61.md) (measure the $S_3$ law numerically) · [MAIS-O5](MAIS-O5.md) (the headline problem).*
