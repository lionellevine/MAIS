# Boundary-state residual of max-margin gradient descent

*Open problem MAIS-O89 · posed in [MAIS-A8](../agendas/A8/MAIS-A8.pdf) as [Problem 7.1](../agendas/A8/MAIS-A8.tex#L461) · Status: open.*

*Safety: generalization — goal misgeneralization · training dynamics. Mathematics: optimization · dynamical systems. Difficulty: ★ starter.*

The max-margin direction predicts a trained linear classifier only to leading order, and the bounded residual it leaves behind is usually beneath notice. On the coin line the residual controls half the test return.

The setting is the agenda's coin line with the relative encoding: an agent at $p$ and a coin at $c$ on $\{0,\dots,L\}$, features $x_{\mathrm r}(p,c)=(1,c-p)$, and a linear model $f_w=w\cdot x_{\mathrm r}$ trained by gradient descent on the logistic loss at zero diversity, where every training state has the coin at the right end and label "step right." The agenda's Proposition 4.4 shows $w_k/\lVert w_k\rVert\to(1,1)/\sqrt2$, so the trained policy eventually steps right when $c\ge p$ and left when $c\le p-2$ — nearly the intended goal. At the boundary states $c=p-1$ the limit direction is silent: there $(1,1)\cdot x_{\mathrm r}=0$, and the verdict falls to the residual. The stakes are concrete: a policy that deterministically steps right one step past the coin enters a two-cycle and never collects it, while a left step collects it immediately.

**Problem ([MAIS-A8, Problem 7.1](../agendas/A8/MAIS-A8.tex#L461)).** In this setting, the boundary logit at $c=p-1$ is $d_k=w_{0,k}-w_{1,k}$; the leading maximum-margin term cancels there. Determine whether $d_k$ converges as a function of the initialization and step size, and compute its limit $d_\infty$. Then compute the exact return of the limiting logistic policy, which steps right at a boundary state with probability $\sigma(d_\infty)$. This convention includes $d_\infty=0$ without a separate tie rule.

Here $w_{0,k},w_{1,k}$ are the two coordinates of the step-$k$ iterate, $\sigma(z)=1/(1+e^{-z})$, and the return is the probability of collecting the coin when start and coin positions are uniform. The refined residual analysis of Ji and Telgarsky for separable logistic regression is the natural tool, and no networks are involved: this is a starter problem about a two-parameter convex iteration. For the max-margin computation it refines, see [MAIS-A8](../agendas/A8/MAIS-A8.pdf).

*Related: [MAIS-O85](MAIS-O85.md) (defers to this residual when the margin score vanishes) · [MAIS-O84](MAIS-O84.md) (the other finite-time question in the linear model) · [MAIS-O8](MAIS-O8.md) (the headline selection problem).*
