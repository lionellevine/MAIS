# Boundary-state residual of max-margin gradient descent

*Open problem MAIS-O89 · posed in [MAIS-A8](../agendas/A8/) as [Problem 7.1](../agendas/A8/MAIS-A8.tex#L462) · Status: open.*

*Tags: generalization · goal misgeneralization · training dynamics · optimization · dynamical systems. Difficulty: ★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

By the implicit-bias theorem of Soudry, Hoffer, Nacson, Gunasekar, and Srebro [[SHNGS18]](https://arxiv.org/abs/1710.10345), gradient descent on separable data converges in direction to the max-margin classifier. That direction predicts a trained linear classifier only to leading order, and the bounded residual it leaves behind is usually beneath notice. On the coin line the residual controls half the test return.

The setting is the agenda's coin line with the relative encoding: an agent at $p$ and a coin at $c$ on $\lbrace 0,\dots,L\rbrace $ with $L\ge4$, features $x_{\mathrm r}(p,c)=(1,c-p)$, and a linear model $f_w=w\cdot x_{\mathrm r}$ trained at zero diversity: every training state has the coin at the right end and label "step right," and training is full-batch gradient descent with constant step size $\eta>0$ on the logistic loss $\log(1+e^{-f_w(x)})$ averaged over the $L$ states $(p,L)$, $0\le p\le L-1$ (in the relative encoding, the points $x=(1,k)$ for $k=1,\dots,L$). The agenda's Proposition 4.4 shows that from any initialization, at any sufficiently small step size, $w_k/\lVert w_k\rVert\to(1,1)/\sqrt2$, so the trained policy eventually steps right when $c\ge p$ and left when $c\le p-2$ — nearly the intended goal. At the boundary states $c=p-1$ the limit direction is silent: there $(1,1)\cdot x_{\mathrm r}=0$, and the verdict falls to the residual. The stakes are concrete: a policy that deterministically steps right one step past the coin enters a two-cycle and never collects it, while a left step collects it immediately. Nor is the boundary rare: since the limiting policy steps left whenever $c\le p-2$, every episode that starts with the coin behind the agent funnels into a boundary state, and that is about half of all test episodes.

**Problem ([MAIS-A8, Problem 7.1](../agendas/A8/MAIS-A8.tex#L462)).** In this setting, the boundary logit at $c=p-1$ is $d_k=w_{0,k}-w_{1,k}$; the leading maximum-margin term cancels there. Determine whether $d_k$ converges as a function of the initialization and step size, and compute its limit $d_\infty$. Then compute the exact return of the limiting logistic policy, which steps right at a boundary state with probability $\sigma(d_\infty)$. This convention includes $d_\infty=0$ without a separate tie rule.

Here $w_{0,k},w_{1,k}$ are the two coordinates of the step-$k$ iterate and $\sigma(z)=1/(1+e^{-z})$. The return is the test return of the agenda's coin line: start position and coin position independent and uniform on $\lbrace 0,\dots,L\rbrace $, each action moving the agent one step left or right (clipped at the endpoints $0$ and $L$), and an episode succeeding if the agent reaches the coin within the horizon of $2L$ steps. The refined residual analysis of Ji and Telgarsky [[JT19]](https://arxiv.org/abs/1803.07300) for separable logistic regression is the natural tool, and no networks are involved: this is a starter problem about a two-parameter convex iteration. For the max-margin computation it refines, see [MAIS-A8](../agendas/A8/).

## References

- [SHNGS18] D. Soudry, E. Hoffer, M. S. Nacson, S. Gunasekar, and N. Srebro, *The implicit bias of gradient descent on separable data*, Journal of Machine Learning Research 19 (2018), no. 70, 1–57. [arXiv:1710.10345](https://arxiv.org/abs/1710.10345)
- [JT19] Z. Ji and M. Telgarsky, *The implicit bias of gradient descent on nonseparable data*, Conference on Learning Theory 2019, pp. 1772–1798. [arXiv:1803.07300](https://arxiv.org/abs/1803.07300)
- [LKSP+22] L. Langosco, J. Koch, L. Sharkey, J. Pfau, L. Orseau, and D. Krueger, *Goal misgeneralization in deep reinforcement learning*, International Conference on Machine Learning 2022. [arXiv:2105.14111](https://arxiv.org/abs/2105.14111)

*Related: [MAIS-O85](MAIS-O85.md) (defers to this residual when the margin score vanishes) · [MAIS-O84](MAIS-O84.md) (the other finite-time question in the linear model) · [MAIS-O8](MAIS-O8.md) (the headline selection problem).*
