# Vanishing weight decay selects both S₃ representations

*Open problem MAIS-O56 · posed in [MAIS-A5](../agendas/A5/) as [Conjecture 5.6](../agendas/A5/MAIS-A5.tex#L289) · Status: open.*

*Tags: interpretability · mechanistic interpretability · training dynamics · universality of circuits · dynamical systems · representation theory · optimization. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

How far a mechanistic interpretation of one trained network carries to another depends on whether training selects the same circuits each time. For networks trained on group multiplication, Chughtai, Chan, and Nanda [[CCN23]](https://arxiv.org/abs/2302.03025) found universality in the weak sense only: the trained circuits are built from irreducible characters of the group, but *which* irreducibles appear varies from one random seed to the next.

A network trained to multiply in $S_3$ has four possible answers to "which irreducible representations are visible in your outputs?": the subsets of $\lbrace \mathrm{sgn}, \mathrm{std}\rbrace $, where $\mathrm{sgn}$ is the sign representation and $\mathrm{std}$ the 2-dimensional standard one. The conjecture: run training to convergence, then let the weight decay tend to zero, and the answer is the full set $\lbrace \mathrm{sgn}, \mathrm{std}\rbrace $ with probability one — deterministic selection in the limit, where at fixed decay even the existence of the limiting law is open ([MAIS-O55](MAIS-O55.md)).

The ensemble $\mathcal{T}(S_3, x^2, m, \lambda, \tau)$ is a one-hidden-layer network of $m$ quadratic neurons, with logits $f_\theta(a,b)(c) = \sum_{i=1}^m (u_i(a)+v_i(b))^2\  w_i(c)$ for $u_i,v_i,w_i \in \mathbb{R}^{S_3}$, trained by gradient flow on the cross-entropy loss over the full multiplication table plus weight decay $\lambda\Vert \theta\Vert ^2$, from independent $N(0,\tau^2)$ coordinates. The **spectral weight** of a nontrivial irreducible $\rho$ is the normalized correlation of the network's centered logits with the class function $(a,b,c) \mapsto \chi_\rho(abc^{-1})$; the **key set** $K_\varepsilon(\theta)$ collects the representations whose spectral weight is at least $\varepsilon$ in absolute value; the **selection law** at time $t$ is the distribution of $K_\varepsilon(\theta(t))$. A threshold $\varepsilon$ is **nonexceptional** if, in the limits the conjecture takes ($t \to \infty$, then $\lambda \to 0$), the law of each spectral weight puts no atom at $\varepsilon$; all but a Lebesgue-null set of small thresholds qualify. Precise definitions are in [MAIS-A5](../agendas/A5/).

**Conjecture ([MAIS-A5, Conjecture 5.6](../agendas/A5/MAIS-A5.tex#L289)).** Fix a nonexceptional threshold $\varepsilon > 0$. In $\mathcal{T}(S_3, x^2, m, \lambda, \tau)$ with $m \ge 100$, in the double limit $t \to \infty$ then $\lambda \to 0$: the selection law converges to the point mass at $\lbrace \mathrm{sgn}, \mathrm{std}\rbrace $.

The width $m \ge 100$ and the initialization scale $\tau > 0$ are fixed but arbitrary: by the agenda's convention, a proof for one explicit choice of $(m, \tau)$ is a full solution.

The motivation is a theorem one norm away. Morwani, Edelman, Oncescu, Zhao, and Kakade [[MEOZK24]](https://arxiv.org/abs/2311.07568) characterize the networks maximizing the classification margin normalized by the $\ell_{2,3}$ norm $(\sum_i \Vert \omega_i\Vert _2^3)^{1/3}$ (with $\omega_i$ the concatenated weights of neuron $i$): for $S_3$, every nonzero neuron is pure (its weights supported on a single nontrivial irreducible representation) and both nontrivial representations are present. But the ensemble here uses Euclidean squared decay, and by a theorem of Wei, Lee, Liu, and Ma [[WLLM19]](https://arxiv.org/abs/1810.05369) weak-regularization limits respect the regularizer's own norm, so the margin theorem motivates the conjecture without predicting it. A proof would require a dynamical analysis of the Euclidean norm in this double limit; see [MAIS-A5](../agendas/A5/) for what is known.

## References

- [CCN23] B. Chughtai, L. Chan, and N. Nanda, *A toy model of universality: reverse engineering how networks learn group operations*, ICML 2023. [arXiv:2302.03025](https://arxiv.org/abs/2302.03025)
- [MEOZK24] D. Morwani, B. L. Edelman, C.-A. Oncescu, R. Zhao, and S. Kakade, *Feature emergence via margin maximization: case studies in algebraic tasks*, ICLR 2024. [arXiv:2311.07568](https://arxiv.org/abs/2311.07568)
- [WLLM19] C. Wei, J. D. Lee, Q. Liu, and T. Ma, *Regularization matters: generalization and optimization of neural nets v.s. their induced kernel*, NeurIPS 2019. [arXiv:1810.05369](https://arxiv.org/abs/1810.05369)

*Related: [MAIS-O55](MAIS-O55.md) (the same selection law at fixed $\lambda$) · [MAIS-O5](MAIS-O5.md) (the headline selection law) · [MAIS-O54](MAIS-O54.md) (how neurons split between the two representations).*
