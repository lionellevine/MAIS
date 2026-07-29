# Does finite-width training inherit the kernel flow's selection?

*Open problem MAIS-O90 · posed in [MAIS-A8](../agendas/A8/) as [Problem 7.3](../agendas/A8/MAIS-A8.tex#L470) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · training dynamics · probability · optimization. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

In the kernel limit the verdict on the coin line is proved: the zero-diversity kernel gradient flow drives the off-distribution probe logit to $+\infty$, so the infinite-width lazy network walks away from a displaced coin. The finite-width statement is open, and it is the one the selection question actually needs: whether a trained network of finite width follows the proxy rule "move right" or the intended rule "go to the coin" at a state where the two disagree.

The setting, from the agenda: an agent at position $p$ and a coin at position $c$, both on $\lbrace 0,\dots,L\rbrace $, are encoded as the input $x_{\mathrm a}(p,c)=(1,p,c)$ — a constant bias, then the two positions. At zero diversity the coin always sits at the right end, so the training inputs are $x_{\mathrm a}(p,L)=(1,p,L)$ for $0\le p\le L-1$, all labeled "step right"; the probe is the state $s^{\ast }=(\lceil L/2\rceil,0)$, agent mid-line and coin at the left end, with input $(1,\lceil L/2\rceil,0)$, where "move right" and "go to the coin" disagree. At diversity $\varepsilon>0$, an $\varepsilon$-fraction of training states draw the coin's position uniformly from $\lbrace 1,\dots,L\rbrace $ rather than fixing it at $L$, the agent's position is uniform on $\lbrace 0,\dots,L\rbrace $ with $p\ne c$, and each state is labeled by the intended action $\operatorname{sign}(c-p)$; the coin is never placed at $0$, so the probe stays off-distribution for every $\varepsilon$. The network is two-layer ReLU in the neural-tangent parameterization of Jacot, Gabriel, and Hongler [[JGH18]](https://arxiv.org/abs/1806.07572), $f_\theta(x)=m^{-1/2}\sum_j a_j\varphi(u_j\cdot x)$, $\varphi(z)=\max(z,0)$; all parameters $(a_j,u_j)_{j\le m}$ are independent standard Gaussians at initialization, and all are trained by full-batch gradient descent on the logistic loss with step $\eta$ (with the agenda's backpropagation convention $\varphi'(z)=\mathbf 1\lbrace z>0\rbrace $, so each initialization determines a unique trajectory); $q^{\mathrm{ntk}}_0(k;m,L,\eta)$ is the probability over the initialization that the step-$k$ probe logit is positive. The agenda's Proposition 5.3 settles the infinite-width flow by a positivity argument: some training coefficient must diverge, and the ReLU tangent kernel is positive between every training input and the probe.

**Problem ([MAIS-A8, Problem 7.3](../agendas/A8/MAIS-A8.tex#L470)).** The agenda's Proposition 5.3 settles the infinite-width $\varepsilon=0$ flow. Prove the finite-width probe statement

$$\lim_{m\to\infty}\liminf_{k\to\infty}q^{\mathrm{ntk}}_0(k;m,L,\eta)=1,$$

or identify the obstruction. The observable is the sign at this one probe; uniform-in-time convergence of the entire empirical kernel is not required and in general fails under cross-entropy training (Yu, Tian, and Chen). Separately, compute the probe sign of the kernel support-vector machine for $\varepsilon>0$ and small $L$.

The difficulty is the interchange of limits: finite-width trajectories track the kernel flow for fixed training time, but the probe verdict is a long-time statement, and the squared-loss finite-width guarantees of Arora, Du, Hu, Li, Salakhutdinov, and Wang [[ADHL+19]](https://arxiv.org/abs/1904.11955) do not cover logistic training at large times. Only one sign at one point must survive the interchange, which is why this is a project rather than a general theory. In the closing sub-problem, the kernel support-vector machine is the maximum-margin classifier in the tangent kernel's feature space, trained on the $\varepsilon>0$ data above. For the kernel-flow proof and the surrounding regime dichotomy, see [MAIS-A8](../agendas/A8/).

## References

- [YTC25] Z. Yu, S. Tian, and G. Chen, *Divergence of the empirical neural tangent kernel in classification problems*, ICLR 2025 — why uniform-in-time kernel convergence fails under cross-entropy, forcing the probe-only formulation. [arXiv:2504.11130](https://arxiv.org/abs/2504.11130)
- [ADHL+19] S. Arora, S. S. Du, W. Hu, Z. Li, R. Salakhutdinov, and R. Wang, *On exact computation with an infinitely wide neural net*, NeurIPS 2019 — the squared-loss finite-width guarantee that does not cover logistic training at large times. [arXiv:1904.11955](https://arxiv.org/abs/1904.11955)
- [JGH18] A. Jacot, F. Gabriel, and C. Hongler, *Neural tangent kernel: convergence and generalization in neural networks*, NeurIPS 2018 — the tangent kernel and the infinite-width kernel limit. [arXiv:1806.07572](https://arxiv.org/abs/1806.07572)

*Related: [MAIS-O86](MAIS-O86.md) (whether the same limit instead matches the Gaussian posterior) · [MAIS-O82](MAIS-O82.md) (the analogous conjecture in the standard parameterization) · [MAIS-O83](MAIS-O83.md) (finite-width departures from the infinite-width verdicts).*
