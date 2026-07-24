# Marginal cost of width for modular-addition networks

*Open problem MAIS-O64 · posed in [MAIS-A6](../agendas/A6/MAIS-A6.pdf) as [Conjecture 4.7](../agendas/A6/MAIS-A6.tex#L333) · Status: open.*

*Safety: interpretability, generalization — singular learning theory · developmental interpretability · grokking. Mathematics: algebraic geometry · statistics. Difficulty: ★★★ hard.*

What does one idle neuron cost, as learning theory counts cost? Parameter counting charges half the parameter count, $3p/2$ per unit; singular geometry charges less, and the discount measures how strongly Bayesian learning prefers degenerate networks — the same preference conjectured to select legible mechanisms in [MAIS-O6](MAIS-O6.md).

The model is the quadratic modular-addition network of [MAIS-A6](../agendas/A6/MAIS-A6.pdf): on input $(a,b) \in (\mathbb{Z}/p\mathbb{Z})^2$ it computes $f_w(a,b) = \sum_{j=1}^H V_j (u_j'(a)+u_j''(b))^2 \in \mathbb{R}^p$, the population loss $K$ is half the mean squared error against the one-hot target $\delta_{a+b}$, and $W_0(p,H)$ is its zero set. Write $\lambda(w)$ for the local learning coefficient of $K$ at $w$ (the volume-growth exponent of $\lbrace K \le \varepsilon\rbrace $ near $w$), $R_p = 1 + \Vert w^F\Vert $ for the norm scale of the width-$(2p-1)$ Fourier fit $w^F$, and $\lambda_{\min}(p,H;R) = \min\lbrace \lambda(w) : w \in W_0(p,H),\ \Vert w\Vert  \le R\rbrace $.

Two facts frame the conjecture. Padding any exact fit with a dead unit raises its local coefficient by at most $(2p-1)/4$ (agenda Proposition 4.6, by a Cauchy–Schwarz splitting). And the increments cannot accumulate forever: once $H \ge 2p-1+p^2$ the variety contains submersion points, giving $\lambda_{\min}(p,H;R) \le p^3/2$ for all larger widths — extra width is eventually free. The conjecture says the ramp is exactly linear until it hits that ceiling.

**Conjecture ([MAIS-A6, Conjecture 4.7](../agendas/A6/MAIS-A6.tex#L333)).** For every odd $p \ge 3$, every $R \ge R_p$, and every $H \ge 2p-1$ with $\lambda_{\min}(p,H;R) + \frac{2p-1}{4} \le \frac{p^3}{2}$,

$$\lambda_{\min}(p, H+1; R) \ =\  \lambda_{\min}(p, H; R) + \frac{2p-1}{4}.$$

In words: as long as the running minimum plus one increment stays below the ceiling $p^3/2$, each added unit raises the smallest local learning coefficient in the ball by exactly $(2p-1)/4$ — the cost of killing the unit, and about a third of the parameter-counting charge. A first step sized for one paper: settle the case of a single added unit, computing the exact local coefficient at the padded Fourier point $(w^F, 0) \in W_0(p, 2p)$, where the cross terms discarded by Cauchy–Schwarz must be confronted. The padding proposition and the ceiling argument are in [MAIS-A6](../agendas/A6/MAIS-A6.pdf).

*Related: [MAIS-O63](MAIS-O63.md) (the base values $\lambda_{\min}(p,H;R)$ this recursion starts from) · [MAIS-O6](MAIS-O6.md) (structure of the minimizers) · [MAIS-O62](MAIS-O62.md) (where the variety becomes nonempty).*
