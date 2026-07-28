# Law of large numbers for neuron representation multiplicities

*Open problem MAIS-O53 · posed in [MAIS-A5](../agendas/A5/) as [Conjecture 5.3](../agendas/A5/MAIS-A5.tex#L263) · Status: open.*

*Tags: interpretability · mechanistic interpretability · training dynamics · universality of circuits · monosemanticity · probability · representation theory · dynamical systems. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

In networks trained on group multiplication, individual neurons commit: in Nanda et al.'s mod-113 network, 84.6% of neurons have at least 85% of their weight energy on a single Fourier frequency, and Chughtai et al.'s nonabelian networks cluster neuron-by-neuron around single irreducible representations. As the width grows, does the fraction of neurons committed to each irreducible converge — a law of large numbers for how training allocates its neurons among the irreducibles of $G$?

The network is one hidden layer of $m$ neurons with quadratic activation: logits $f_\theta(a,b)(c) = \sum_{i=1}^m (u_i(a)+v_i(b))^2\  w_i(c)$ with $u_i, v_i, w_i \in \mathbb{R}^G$. Training is gradient flow for the cross-entropy loss over the full multiplication table, with no weight decay, from independent $N(0,\tau^2)$ coordinates; $\mathcal{T}(G, x^2, m, 0, \tau)$ denotes this random trajectory. Write $\mathcal{R}(G)$ for the conjugation classes $[\rho] = \lbrace \rho, \bar\rho\rbrace $ of nontrivial irreducible representations, and $\Pi_{[\rho]}$ for the isotypic projection of $\mathbb{R}^G$ onto the span of the matrix coefficients of $[\rho]$. Neuron $i$ is **$(\delta,[\rho])$-pure** if, after centering $u_i, v_i, w_i$, at least a $(1-\delta)$ fraction of their combined squared norm lies in the image of $\Pi_{[\rho]}$; a dead neuron (all three weight vectors constant) is pure for no class. The **multiplicity** $\nu_{[\rho],\delta}(\theta)$ is the fraction of the $m$ neurons that are $(\delta,[\rho])$-pure.

**Conjecture ([MAIS-A5, Conjecture 5.3](../agendas/A5/MAIS-A5.tex#L263)).** Fix a nonabelian finite group $G$, $\sigma(x) = x^2$, $\lambda = 0$, $\tau > 0$. There exist constants $q_{[\rho]} \ge 0$ with $\sum_{[\rho] \in \mathcal{R}(G)} q_{[\rho]} = 1$, not depending on $\tau$, such that for every $\delta \in (0, \tfrac12)$ and every $[\rho] \in \mathcal{R}(G)$,

$$\lim_{m \to \infty} \  \lim_{t \to \infty} \  \nu_{[\rho],\delta}\bigl(\theta_m(t)\bigr) \ =\  q_{[\rho]} \qquad \text{in probability},$$

where $\theta_m$ denotes the trajectory of $\mathcal{T}(G, x^2, m, 0, \tau)$, and $q_{[\rho]} > 0$ for every $[\rho]$. Existence of the inner limit, almost surely for each fixed $m$, is part of the conjecture.

In words: train to convergence, then widen; the empirical proportion of neurons pure for each class settles at a constant $q_{[\rho]}$, positive for every class and independent of the initialization scale. The conjecture asserts convergence of proportions only, not that neurons land independently. For abelian groups with no self-conjugate nontrivial character, He et al. prove the analogue for a projected flow under a Taylor-surrogate risk, with uniform diversification across characters; the nonabelian landing law is open even in that idealized regime. What the constants should be is a separate question with competing heuristics. See [MAIS-A5](../agendas/A5/) for the surrounding theory.

*Related: [MAIS-O54](MAIS-O54.md) (the conjectured value of $q_{[\rho]}$) · [MAIS-O55](MAIS-O55.md) (purity for $S_3$, the smallest nonabelian case) · [MAIS-O5](MAIS-O5.md) (the output-level selection law).*
