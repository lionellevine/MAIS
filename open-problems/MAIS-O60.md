# Does a single ReLU neuron align to one frequency?

*Open problem MAIS-O60 · posed in [MAIS-A5](../agendas/A5/) as [Problem 6.2](../agendas/A5/MAIS-A5.tex#L320) · Status: **resolved in the negative** (August 2026).*

*Tags: interpretability · mechanistic interpretability · training dynamics · monosemanticity · dynamical systems · probability · harmonic analysis. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol · Resolved by: Gautam Neelakantan Memana, with a strengthening by GPT 5.6 Sol.*

Strip the network down to a single rectifier neuron on addition mod $p$. Trained wide networks on this task end up with neurons each committed to one Fourier frequency, as Nanda, Chan, Lieberum, Smith, and Steinhardt observed [[NCLSS23]](../references/NCLSS23.md); here the question is isolated in one neuron: started from a unit-scale Gaussian, does its direction converge, and is the limit a single frequency?

The parameters are three functions $u_1, v_1, w_1 \in \mathbb{R}^{C_p}$ — a single neuron, width $m = 1$ in the agenda's notation — and the logits are $f_\theta(a,b)(c) = \mathrm{ReLU}(u_1(a)+v_1(b))\ w_1(c)$. Training is gradient flow on the cross-entropy loss over the full addition table, with no weight decay (coefficient $\lambda = 0$), from independent standard Gaussian coordinates (initialization scale $\tau = 1$); since the rectifier is only piecewise smooth, the flow is a differential inclusion and the statement is asserted for every measurable selection of Clarke trajectories. The frequency classes of $C_p$ are $[\rho_\zeta] = \lbrace \rho_\zeta, \rho_{-\zeta}\rbrace $ where $\rho_\zeta(a) = e^{2\pi i \zeta a/p}$, and the triple $(u_1,v_1,w_1)$ is **$(\delta,[\rho_\zeta])$-pure** if, after centering, at least a $(1-\delta)$ fraction of its combined squared norm lies in the isotypic component of $[\rho_\zeta]$ — that is, along the functions $\cos(2\pi\zeta \cdot/p)$ and $\sin(2\pi\zeta \cdot/p)$.

**Problem ([MAIS-A5, Problem 6.2](../agendas/A5/MAIS-A5.tex#L320)).** Let $G = C_p$, $\sigma = \mathrm{ReLU}$, $m = 1$, $\lambda = 0$, $\tau = 1$, and condition on the event that the neuron is active at initialization — $u_1(a) + v_1(b) > 0$ for some $(a,b)$. (On the complementary event the gradient vanishes almost surely; equality at a ReLU kink is a Gaussian null event.) Prove or refute: almost surely on the active event, the normalized weights $(u_1, v_1, w_1)/\Vert \cdot\Vert $ converge, and the limit is $(\delta, [\rho_\zeta])$-pure for every $\delta > 0$, for some frequency $\zeta$.

In words: with a single neuron there is no competition for neurons, only the question of whether the rectifier dynamics themselves concentrate a random initial spectrum onto one frequency. For the Clarke-trajectory convention and the surrounding results, see [MAIS-A5](../agendas/A5/).

## Resolution

**The answer is no** — the almost-sure claim fails, for every odd prime $p \ge 5$, on explicit positive-probability events. Resolved by Gautam Neelakantan Memana ([issue #1](https://github.com/lionellevine/MAIS/issues/1), August 2026), with a strengthening by GPT-5.6 Sol; both proofs were verified independently for this repository, and the constructions reproduce numerically to machine precision.

**The dead-neuron counterexample (Memana).** Take $u(0)=v(0)=\varepsilon/2$ and $u(a)=v(a)=-B$ for $a\neq 0$, with $B>\varepsilon/2$; take $w(0)=-A$ with $A^2 > \tfrac{p}{2(p-1)}\varepsilon^2$ and $w=0$ elsewhere. Exactly one gate is active, its example is correctly labeled but its correct logit weight is depressed, and the flow reduces to two variables: the active preactivation $s$ and the logit gap $g$, which obey the conservation law $g^2-\tfrac{p}{2(p-1)}s^2 = \mathrm{const} > 0$. The gap stays bounded below, so $\dot s$ is bounded away from zero and $s$ hits the kink transversely in finite time; choosing the zero Clarke slope there freezes the weights forever. The frozen centered triple is a multiple of the point mass $e_0-\tfrac1p\mathbf 1$, whose Fourier energy is exactly $\tfrac{2}{p-1}$ in *every* nonzero frequency class — flat, so not $(\delta,[\rho_\zeta])$-pure for any $\delta < 1-\tfrac{2}{p-1}$. The trajectory to the kink lives in an open chamber where the flow is smooth and the hit is transverse, so an open neighborhood of initializations does the same, and open sets have positive Gaussian probability.

**The strengthening (Sol).** The failure is not an artifact of the dead-neuron loophole or of the freedom to choose Clarke trajectories. There is an open set of active initializations on which the Clarke trajectory is *unique* (via local semiconvexity of the loss at positive-slope kinks), stays active forever, captures the cross-gates onto sliding kink faces one by one, memorizes a single table entry with $\lVert\theta\rVert\to\infty$ — and its normalized limit has the same flat $\tfrac{2}{p-1}$ spectrum. Companion theorems give an open set where *every* Clarke trajectory dies in finite time, and carry the failure to $C^\infty$ dead-zone smoothings of the ReLU and to fixed-step full-batch gradient descent. The result does not extend to everywhere-positive activations such as softplus, where both mechanisms are unavailable.

**What survives.** Both counterexamples occupy constructed corners of initialization space; the typical behavior from unit-scale Gaussian initialization — and whether alignment occurs with any positive probability at all — is untouched, and is now posed as [MAIS-O92](MAIS-O92.md). The nearest positive result remains the controlled-initialization leakage estimate of He, Wang, Chen, and Yang [[HWCY26]](../references/HWCY26.md).

Resolution documents: [Memana's note](https://github.com/user-attachments/files/30615776/MAIS_60-2.pdf) · [Sol's strengthened counterexamples](https://github.com/user-attachments/files/30615797/MAIS_O60_strengthened_counterexamples.pdf) · discussion in [issue #1](https://github.com/lionellevine/MAIS/issues/1).

## References

- [[HWCY26]](../references/HWCY26.md) J. He, L. Wang, S. Chen, and Z. Yang, *On the mechanism and dynamics of modular addition: Fourier features, lottery ticket, and grokking*, preprint, 2026. [arXiv:2602.16849](https://arxiv.org/abs/2602.16849)
- [[NCLSS23]](../references/NCLSS23.md) N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, *Progress measures for grokking via mechanistic interpretability*, ICLR, 2023. [arXiv:2301.05217](https://arxiv.org/abs/2301.05217)

*Related: [MAIS-O92](MAIS-O92.md) (the successor: the outcome law this resolution leaves open) · [MAIS-O59](MAIS-O59.md) (two quadratic neurons: alignment plus competition) · [MAIS-O53](MAIS-O53.md) (multiplicities when many neurons compete) · [MAIS-O5](MAIS-O5.md) (the headline selection law).*
