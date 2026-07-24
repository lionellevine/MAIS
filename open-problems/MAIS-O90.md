# Does finite-width training inherit the kernel flow's selection?

*Open problem MAIS-O90 · posed in [MAIS-A8](../agendas/A8/) as [Problem 7.3](../agendas/A8/MAIS-A8.tex#L469) · Status: open.*

*Safety: generalization — goal misgeneralization · proxy goals · training dynamics. Mathematics: probability · optimization. Difficulty: ★★ project.*

In the kernel limit the verdict on the coin line is proved: the zero-diversity kernel gradient flow drives the off-distribution probe logit to $+\infty$, so the infinite-width lazy network walks away from a displaced coin. The finite-width statement is open, and it is the one the selection problem actually needs.

The setting, from the agenda: training inputs $x_{\mathrm a}(p,L)=(1,p,L)$ for $0\le p\le L-1$, all labeled "step right" (the coin always at the right end), and the probe $s^{\ast }=(\lceil L/2\rceil,0)$, where "move right" and "go to the coin" disagree. The network is two-layer ReLU in the neural-tangent parameterization $f_\theta(x)=m^{-1/2}\sum_j a_j\varphi(u_j\cdot x)$, $\varphi(z)=\max(z,0)$, with unit Gaussian initialization, trained by full-batch gradient descent on the logistic loss with step $\eta$; $q^{\mathrm{ntk}}_0(k;m,L,\eta)$ is the probability over the initialization that the step-$k$ probe logit is positive. The agenda's Proposition 5.3 settles the infinite-width flow by a positivity argument: some training coefficient must diverge, and the ReLU tangent kernel is positive between every training input and the probe.

**Problem ([MAIS-A8, Problem 7.3](../agendas/A8/MAIS-A8.tex#L469)).** The agenda's Proposition 5.3 settles the infinite-width $\varepsilon=0$ flow. Prove the finite-width probe statement

$$\lim_{m\to\infty}\liminf_{k\to\infty}q^{\mathrm{ntk}}_0(k;m,L,\eta)=1,$$

or identify the obstruction. The observable is the sign at this one probe; uniform-in-time convergence of the entire empirical kernel is not required and in general fails under cross-entropy training (Yu, Tian, and Chen). Separately, compute the probe sign of the kernel support-vector machine for $\varepsilon>0$ and small $L$.

The difficulty is the interchange of limits: finite-width trajectories track the kernel flow for fixed training time, but the probe verdict is a long-time statement, and the squared-loss finite-width guarantees of Arora et al. do not cover logistic training at large times. Only one sign at one point must survive the interchange, which is why this is a project rather than a general theory. For the kernel-flow proof and the surrounding regime dichotomy, see [MAIS-A8](../agendas/A8/).

*Related: [MAIS-O86](MAIS-O86.md) (whether the same limit instead matches the Gaussian posterior) · [MAIS-O82](MAIS-O82.md) (the analogous conjecture in the standard parameterization) · [MAIS-O83](MAIS-O83.md) (finite-width departures from the infinite-width verdicts).*
