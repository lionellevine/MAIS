# Exact solutions to the nonlinear dynamics of learning in deep linear neural networks

*Summary [SMG14] · A. M. Saxe, J. L. McClelland, and S. Ganguli, ICLR 2014 · [arXiv:1312.6120](https://arxiv.org/abs/1312.6120).*

*Tags: training dynamics · dynamical systems · developmental interpretability · singular learning theory · generalization.*

*Summarized by: Claude Fable 5 directed by Lionel Levine.*

**TL;DR.** Gradient-flow training of a deep *linear* network — a product of matrix factors, so the map is linear but the loss in the factors is nonconvex — is exactly solvable. Under whitened inputs, the singular value decomposition of the input–output correlation decouples the flow into independent scalar logistic equations, one per singular mode, each with a closed-form sigmoidal trajectory. From a small initialization the modes switch on one at a time, strongest first, and the loss descends as a staircase of saddle-point plateaus.

## Setup and hypotheses

The network is $x \mapsto W_L \cdots W_1 x$, trained by gradient flow $\tau \dot W_i = -\partial E/\partial W_i$ on the square loss $E = \tfrac12 \sum_\mu \Vert y^\mu - W_L \cdots W_1 x^\mu \Vert^2$. The data enter only through the input correlation $\Sigma^{11} = \langle x x^\top \rangle$ and the input–output correlation $\Sigma^{31} = \langle y x^\top \rangle$; the standing hypothesis is **whitened inputs**, $\Sigma^{11} = I$. Write the singular value decomposition $\Sigma^{31} = \sum_\alpha s_\alpha u_\alpha v_\alpha^\top$. The exact solutions start from an **aligned initialization**: weights seeded along this singular frame at a small scale $u_0$, a form the flow preserves.

## Main results

1. **Decoupling.** In the two-layer case, the aligned flow separates into independent scalar systems $\tau \dot a = b(s - ab)$, $\tau \dot b = a(s - ab)$ per mode, with conserved quantity $a^2 - b^2$ (from the rescaling symmetry of the factorization).
2. **Closed-form trajectory.** The reconstructed mode strength $u = ab$ obeys the logistic equation $\tau \dot u = 2u(s - u)$, solved by $u(t) = s\, e^{2st/\tau} / (e^{2st/\tau} - 1 + s/u_0)$. Each mode lingers near zero, then rises sharply to $s_\alpha$ at time $t_\alpha \approx \tfrac{\tau}{2 s_\alpha} \log \tfrac{s_\alpha}{u_0}$: larger singular values are learned faster.
3. **The staircase.** As $u_0\to0$, modes are acquired sequentially, strongest first, and the loss falls in plateaus separated by sharp drops. The trajectory passes near saddles at which only the leading modes have been learned; the eventual fixed point is the best rank-constrained approximation allowed by the hidden width.
4. **Depth.** With $L$ weight matrices, as in $W_L\cdots W_1$, equal aligned factors give
   $$\tau\dot u=L\,u^{2-2/L}(s-u).$$
   The paper also studies orthogonal initializations that prevent learning time and gradient propagation from deteriorating severely with depth.

The exact statements are for linear networks with whitened inputs and aligned initialization. The paper's evidence that nonlinear networks show the same plateau-and-drop phenomenology is numerical, and the authors present the low-rank-first implicit bias as a dynamics story, not a generalization theorem.

## Proof method

Direct integration. Whitening plus alignment reduce the matrix flow to the one-dimensional logistic equation per mode, which is solved in closed form; the conserved quantity pins the two factors to a single degree of freedom. The stage times then read off from the sigmoid: exponential escape from the saddle at rate $2 s_\alpha / \tau$, hence the $\log(1/u_0)$ waiting time.

## Why it matters for AI safety

Developmental interpretability wants to read the formation of structure during training, and the deep linear network is the one model where the whole training trajectory is a formula. [MAIS-A7](../agendas/A7/) uses this theorem as the dynamical side of its calibration model: the same architecture, viewed as reduced rank regression, has an exactly computed Bayesian free-energy ladder (Aoyagi–Watanabe), and the agenda's problems ask how the dynamical staircase — stages graded by training time, with the [SMG14] schedule $t_k \approx \tfrac{\tau}{2 s_k} \log \tfrac{s_k}{u_0}$ — lines up with the Bayesian one, graded by sample size. The staircase's ordering by singular value, its saddle chain, and its explicit clock are the inputs to those comparisons; see [MAIS-A7](../agendas/A7/).

## Cited by

- [MAIS-A7](../agendas/A7/) — the dynamical half of the agenda's calibration model: the exact staircase (Section 2.4) against which the Bayesian ladder is compared.
- Problems [MAIS-O7](../open-problems/MAIS-O7.md) · [MAIS-O78](../open-problems/MAIS-O78.md) · [MAIS-O79](../open-problems/MAIS-O79.md)
