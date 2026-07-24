# Saddles as effective minima under coarse-graining

*Open problem MAIS-O79 · posed in [MAIS-A7](../agendas/A7/) as [Question 3.13](../agendas/A7/MAIS-A7.tex#L449) · Status: open.*

*Safety: generalization — developmental interpretability · singular learning theory · training dynamics. Mathematics: dynamical systems · algebraic geometry. Difficulty: ★★★ hard.*

Can a training plateau turn a saddle into a local minimum at the resolution visible to the dynamics? Researchers who study how a network's internal structure emerges during training say that during a plateau *the saddle is a local minimum of an effective loss*. Here is one way to make the slogan precise. For $\varepsilon, \delta > 0$ define the **effective loss**

$$L_{\varepsilon, \delta}(w) = -\varepsilon \log \int_{B_\delta(w)} e^{-L(u)/\varepsilon} \  du ,$$

the free energy of a $\delta$-window at $w$, trading the depth of the loss in the window against its volume; a compact set $C$ is an **effective local minimum at resolution $(\varepsilon, \delta)$** if $\sup_{w \in C} L_{\varepsilon,\delta}(w) < \inf \lbrace  L_{\varepsilon,\delta}(w) : \mathrm{dist}(w, C) = 2\delta \rbrace $. A degenerate saddle, poor in depth but rich in volume, can beat its own rim. As $\varepsilon \to 0$ at fixed $\delta$, $L_{\varepsilon,\delta}(w) \to \min_{B_\delta(w)} L$ and no strict saddle is an effective minimum; at large $\varepsilon$, volume dominates. The slogan lives, if anywhere, in a window.

The test model is the two-layer linear network $L(A,B) = \tfrac12 \Vert  BA - \Phi \Vert _F^2$ with singular values $s_1 > \dots > s_r$ of $\Phi$, whose gradient flow from a small aligned initialization of scale $u_0$ passes along the saddle chain $C_0, C_1, \dots, C_r$ ($C_k$: only the top $k$ modes learned), leaving $C_k$ at the time $t_k$ of Saxe–McClelland–Ganguli.

**Question ([MAIS-A7, Question 3.13](../agendas/A7/MAIS-A7.tex#L449)).** For the deep linear network with the spectrum $s_1 > \dots > s_r$, fix $R$ large enough that the ball $\Vert  A \Vert _F^2 + \Vert  B \Vert _F^2 \le R$ meets every $C_k$, and let $C_k^R = C_k \cap \lbrace  \Vert  A \Vert _F^2 + \Vert  B \Vert _F^2 \le R \rbrace $. The truncation is forced, not cosmetic: the definition requires $C$ compact, and along the noncompact $C_k$ with $\Vert  A \Vert _F \to \infty$ the fiber directions steepen, the window mass shrinks, and $\sup_{C_k} L_{\varepsilon,\delta} = +\infty$, so no untruncated $C_k$ is an effective minimum. Determine for each $k$ the set $E_k \subseteq (0,\infty)^2$ of resolutions $(\varepsilon, \delta)$ at which $C_k^R$ is an effective local minimum. For fixed $\delta > 0$, write $I_k(\delta) = \lbrace  \varepsilon > 0 : (\varepsilon, \delta) \in E_k \rbrace $. Does there exist $\delta$ for which every $I_k(\delta)$ is a nonempty interval and

$$\sup I_k(\delta) < \inf I_{k-1}(\delta), \qquad 1 \le k \le r \  ?$$

This is the precise claim that decreasing $\varepsilon$ makes the effective minima pass through $C_0^R, C_1^R, \dots, C_r^R$ in order. Finally, fix such a $\delta$. Write $w(t)$ for the gradient flow of $L$ from the aligned initialization at scale $u_0$, and define $w_{\mathrm{eff}}$ by $\dot w_{\mathrm{eff}}(t) = -\nabla L_{\varepsilon_{u_0}(t), \delta}(w_{\mathrm{eff}}(t))$ from the same initialization. Is there, for each small $u_0$, a positive $C^1$ decreasing schedule $\varepsilon_{u_0}$ and a horizon $T(u_0) \ge t_r$ covering all $r$ stage transitions, such that

$$\sup_{t \le T(u_0)} \mathrm{dist}\bigl( w_{\mathrm{eff}}(t),\  w(t) \bigr) \to 0 \qquad \text{as } u_0 \to 0 \  ?$$

That is the precise sense of shadowing asked for here.

The first two clauses are concrete finite-dimensional questions about explicit integrals. The last clause is the actual bridge — annealing in $\varepsilon$ as a proxy for training time — and the agenda states it as a question rather than a conjecture because no principled derivation of the schedule $\varepsilon(t)$ is in sight; finding one, or proving none exists, is the point. The Bayesian counterpart of the resolution dial is developed by Chen and Murfet ([arXiv:2504.18048](https://arxiv.org/abs/2504.18048)). See [MAIS-A7](../agendas/A7/), Section 3.6.

*Related: [MAIS-O81](MAIS-O81.md) (the rim obstruction to assigning a saddle a free energy) · [MAIS-O78](MAIS-O78.md) (the time–sample dictionary for the same staircase) · [MAIS-O7](MAIS-O7.md) (the headline conjecture about this saddle chain).*
