# Law of large numbers for neuron representation multiplicities

*Open problem MAIS-O53 · posed in [MAIS-A5](../agendas/A5/) as [Conjecture 5.3](../agendas/A5/MAIS-A5.tex#L264) · Status: open.*

*Tags: interpretability · mechanistic interpretability · training dynamics · universality of circuits · monosemanticity · probability · representation theory · dynamical systems. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

In networks trained on group multiplication, individual neurons commit: in Nanda et al.'s mod-113 network [[NCLSS23]](https://arxiv.org/abs/2301.05217), 84.6% of neurons have at least 85% of their weight energy on a single Fourier frequency, and Chughtai, Chan, and Nanda's nonabelian networks [[CCN23]](https://arxiv.org/abs/2302.03025) cluster neuron-by-neuron around single irreducible representations. Circuit-level interpretability implicitly bets that this commitment is lawful: reading one network should tell you about the next. As the width grows, does the fraction of neurons committed to each irreducible converge — a law of large numbers for how training allocates its neurons among the irreducibles of $G$?

The network is one hidden layer of $m$ neurons with quadratic activation $\sigma(x) = x^2$: logits $f_\theta(a,b)(c) = \sum_{i=1}^m (u_i(a)+v_i(b))^2\  w_i(c)$ with $u_i, v_i, w_i \in \mathbb{R}^G$. Training is gradient flow for the cross-entropy loss over the full multiplication table, with no weight decay ($\lambda = 0$), from independent $N(0,\tau^2)$ coordinates ($\tau$ is the initialization scale); $\mathcal{T}(G, x^2, m, 0, \tau)$ denotes this random trajectory. Write $\mathcal{R}(G)$ for the conjugation classes $[\rho] = \lbrace \rho, \bar\rho\rbrace $ of nontrivial irreducible representations, and $\Pi_{[\rho]}$ for the isotypic projection of $\mathbb{R}^G$ onto the span of the matrix coefficients of $[\rho]$. Neuron $i$ is **$(\delta,[\rho])$-pure** if, after centering $u_i, v_i, w_i$, at least a $(1-\delta)$ fraction of their combined squared norm lies in the image of $\Pi_{[\rho]}$; a dead neuron (all three weight vectors constant) is pure for no class. The **multiplicity** $\nu_{[\rho],\delta}(\theta)$ is the fraction of the $m$ neurons that are $(\delta,[\rho])$-pure.

**Conjecture ([MAIS-A5, Conjecture 5.3](../agendas/A5/MAIS-A5.tex#L264)).** Fix a nonabelian finite group $G$, $\sigma(x) = x^2$, $\lambda = 0$, $\tau > 0$. There exist constants $q_{[\rho]} \ge 0$ with $\sum_{[\rho] \in \mathcal{R}(G)} q_{[\rho]} = 1$, not depending on $\tau$, such that for every $\delta \in (0, \tfrac12)$ and every $[\rho] \in \mathcal{R}(G)$,

$$\lim_{m \to \infty} \  \lim_{t \to \infty} \  \nu_{[\rho],\delta}\bigl(\theta_m(t)\bigr) \ =\  q_{[\rho]} \qquad \text{in probability},$$

where $\theta_m$ denotes the trajectory of $\mathcal{T}(G, x^2, m, 0, \tau)$, and $q_{[\rho]} > 0$ for every $[\rho]$. Existence of the inner limit, almost surely for each fixed $m$, is part of the conjecture.

In words: train to convergence, then widen; the empirical proportion of neurons pure for each class settles at a constant $q_{[\rho]}$, positive for every class and independent of the initialization scale. The conjecture asserts convergence of proportions only, not that neurons land independently. The closest theorem is for an idealized dynamics: He, Wang, Zhang, Chen, and Yang [[HWZCY26]](https://arxiv.org/abs/2606.02993) Taylor-expand the cross-entropy to a small-logit surrogate and run a projected gradient flow, and prove for abelian groups with no self-conjugate nontrivial character that each neuron converges to a single character, with uniform diversification across the nontrivial ones. For nonabelian $G$ they prove alignment under the same surrogate flow but not the landing proportions; and surrogate and exact trajectories are compared only on finite time horizons, so their theorems do not transfer to this ensemble as $t \to \infty$. What the constants should be is a separate question with competing heuristics. See [MAIS-A5](../agendas/A5/) for the surrounding theory.

## References

- [HWZCY26] J. He, L. Wang, F. Zhang, S. Chen, and Z. Yang, *Neural networks provably learn spectral representations for group composition*, preprint, 2026. [arXiv:2606.02993](https://arxiv.org/abs/2606.02993)
- [NCLSS23] N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, *Progress measures for grokking via mechanistic interpretability*, ICLR 2023. [arXiv:2301.05217](https://arxiv.org/abs/2301.05217)
- [CCN23] B. Chughtai, L. Chan, and N. Nanda, *A toy model of universality: reverse engineering how networks learn group operations*, ICML 2023. [arXiv:2302.03025](https://arxiv.org/abs/2302.03025)

*Related: [MAIS-O54](MAIS-O54.md) (the conjectured value of $q_{[\rho]}$) · [MAIS-O55](MAIS-O55.md) (purity for $S_3$, the smallest nonabelian case) · [MAIS-O5](MAIS-O5.md) (the output-level selection law).*
