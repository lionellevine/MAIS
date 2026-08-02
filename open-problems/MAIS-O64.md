# Marginal cost of width for modular-addition networks

*Open problem MAIS-O64 · posed in [MAIS-A6](../agendas/A6/) as [Conjecture 4.7](../agendas/A6/MAIS-A6.tex#L334) · Status: open.*

*Tags: interpretability · generalization · singular learning theory · developmental interpretability · grokking · algebraic geometry · statistics. Difficulty: ★★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

What does one idle neuron cost, as learning theory counts cost? The ledger here is Watanabe's singular learning theory [W09], which prices a solution by the geometry of the loss near it rather than by counting parameters. Parameter counting charges half the parameter count, $3p/2$ per unit; singular geometry charges less, and the discount measures how strongly Bayesian learning prefers degenerate networks — the same preference conjectured to select legible mechanisms in [MAIS-O6](MAIS-O6.md).

The model is the quadratic modular-addition network of [MAIS-A6](../agendas/A6/): on input $(a,b) \in (\mathbb{Z}/p\mathbb{Z})^2$ it computes $f_w(a,b) = \sum_{j=1}^H V_j (u_j'(a)+u_j''(b))^2 \in \mathbb{R}^p$, where hidden unit $j$ carries a pair of trainable lookup tables $u_j', u_j'' : \mathbb{Z}/p\mathbb{Z} \to \mathbb{R}$ and an output column $V_j \in \mathbb{R}^p$, so the parameter $w$ ranges over $\mathbb{R}^{3pH}$ with its Euclidean norm $\Vert \cdot \Vert $. The population loss $K$ is half the mean squared error against the one-hot target $\delta_{a+b}$ (an explicit polynomial of degree six in $w$), and $W_0(p,H)$ is its zero set; for width $2p-1$, discrete Fourier inversion gives an exact fit $w^F \in W_0(p,2p-1)$, one hidden unit per cosine and sine frequency ([agenda Lemma 4.2](../agendas/A6/MAIS-A6.tex#L240)). Write $\lambda(w)$ for the local learning coefficient of $K$ at $w$ (the volume-growth exponent of $\lbrace K \le \varepsilon\rbrace $ near $w$, the pointwise refinement of Watanabe's coefficient introduced by Lau, Furman, Wang, Murfet, and Wei [[LFWMW23]](../references/LFWMW23.md)), $R_p = 1 + \Vert w^F\Vert $ for the norm scale of $w^F$, and $\lambda_{\min}(p,H;R) = \min\lbrace \lambda(w) : w \in W_0(p,H),\ \Vert w\Vert  \le R\rbrace $.

Two facts frame the conjecture. Padding any exact fit with a dead unit raises its local coefficient by at most $(2p-1)/4$ ([agenda Proposition 4.6](../agendas/A6/MAIS-A6.tex#L308), by a Cauchy–Schwarz splitting). And the increments cannot accumulate forever: once $H \ge 2p-1+p^2$, the ball $\Vert w\Vert \le R$ contains points of $W_0(p,H)$ at which the parametrization $w \mapsto f_w$ is a submersion, forcing $\lambda_{\min}(p,H;R) \le p^3/2$ at all these widths — extra width is eventually free. The conjecture says the ramp is exactly linear until it hits that ceiling.

**Conjecture ([MAIS-A6, Conjecture 4.7](../agendas/A6/MAIS-A6.tex#L334)).** For every odd $p \ge 3$, every $R \ge R_p$, and every $H \ge 2p-1$ with $\lambda_{\min}(p,H;R) + \frac{2p-1}{4} \le \frac{p^3}{2}$,

$$\lambda_{\min}(p, H+1; R) \ =\  \lambda_{\min}(p, H; R) + \frac{2p-1}{4}.$$

In words: as long as the running minimum plus one increment stays below the ceiling $p^3/2$, each added unit raises the smallest local learning coefficient in the ball by exactly $(2p-1)/4$ — the cost of killing the unit, and about a third of the parameter-counting charge. For comparison, Cullen, Estan-Ruiz, Danait, and Li [[CEDL26]](../references/CEDL26.md) compute local coefficients for these networks in closed form under non-degeneracy hypotheses charging $(3p-1)/2$ per active unit; those hypotheses fail at the dead-unit points this conjecture prices. A first step sized for one paper: settle the case of a single added unit, computing the exact local coefficient at the padded Fourier point $(w^F, 0) \in W_0(p, 2p)$, where the cross terms discarded by Cauchy–Schwarz must be confronted. The padding proposition and the ceiling argument are in [MAIS-A6](../agendas/A6/).

## References

- [[W09]](../references/W09.md) S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- [[LFWMW23]](../references/LFWMW23.md) E. Lau, Z. Furman, G. Wang, D. Murfet, and S. Wei, *The local learning coefficient: a singularity-aware complexity measure*, 2023. [arXiv:2308.12108](https://arxiv.org/abs/2308.12108)
- [[CEDL26]](../references/CEDL26.md) B. Cullen, S. Estan-Ruiz, R. Danait, and J. Li, *A Basin-Selection Perspective on Grokking via Singular Learning Theory*, 2026. [arXiv:2603.01192](https://arxiv.org/abs/2603.01192)

*Related: [MAIS-O63](MAIS-O63.md) (the base values $\lambda_{\min}(p,H;R)$ this recursion starts from) · [MAIS-O6](MAIS-O6.md) (structure of the minimizers) · [MAIS-O62](MAIS-O62.md) (where the variety becomes nonempty).*
