# Does a single ReLU neuron align to one frequency?

*Open problem MAIS-O60 · posed in [MAIS-A5](../agendas/A5/MAIS-A5.pdf) as [Problem 6.2](../agendas/A5/MAIS-A5.tex#L319) · Status: open.*

*Safety: interpretability — mechanistic interpretability · training dynamics · monosemanticity. Mathematics: dynamical systems · probability · harmonic analysis. Difficulty: ★★ project.*

Strip the network down to a single rectifier neuron on addition mod $p$. Trained wide networks on this task end up with neurons each committed to one Fourier frequency; here the question is isolated in one neuron: started from a unit-scale Gaussian, does its direction converge, and is the limit a single frequency?

The parameters are three functions $u_1, v_1, w_1 \in \mathbb{R}^{C_p}$, and the logits are $f_\theta(a,b)(c) = \mathrm{ReLU}(u_1(a)+v_1(b))\ w_1(c)$. Training is gradient flow on the cross-entropy loss over the full addition table, no weight decay, from independent standard Gaussian coordinates; since the rectifier is only piecewise smooth, the flow is a differential inclusion and the statement is asserted for every measurable selection of Clarke trajectories. The frequency classes of $C_p$ are $[\rho_\zeta] = \lbrace \rho_\zeta, \rho_{-\zeta}\rbrace $ where $\rho_\zeta(a) = e^{2\pi i \zeta a/p}$, and the triple $(u_1,v_1,w_1)$ is **$(\delta,[\rho_\zeta])$-pure** if, after centering, at least a $(1-\delta)$ fraction of its combined squared norm lies in the isotypic component of $[\rho_\zeta]$ — that is, along the functions $\cos(2\pi\zeta \cdot/p)$ and $\sin(2\pi\zeta \cdot/p)$.

**Problem ([MAIS-A5, Problem 6.2](../agendas/A5/MAIS-A5.tex#L319)).** Let $G = C_p$, $\sigma = \mathrm{ReLU}$, $m = 1$, $\lambda = 0$, $\tau = 1$, and condition on the event that the neuron is active at initialization — $u_1(a) + v_1(b) > 0$ for some $(a,b)$. (On the complementary event the gradient vanishes almost surely; equality at a ReLU kink is a Gaussian null event.) Prove or refute: almost surely on the active event, the normalized weights $(u_1, v_1, w_1)/\Vert \cdot\Vert $ converge, and the limit is $(\delta, [\rho_\zeta])$-pure for every $\delta > 0$, for some frequency $\zeta$.

In words: with a single neuron there is no competition for neurons, only the question of whether the rectifier dynamics themselves concentrate a random initial spectrum onto one frequency. The nearest rectifier result, a leakage-rate estimate of He et al., starts from a controlled single-frequency state rather than random initialization, so even this one-neuron case is open. For the Clarke-trajectory convention and the surrounding results, see [MAIS-A5](../agendas/A5/MAIS-A5.pdf).

*Related: [MAIS-O59](MAIS-O59.md) (two quadratic neurons: alignment plus competition) · [MAIS-O53](MAIS-O53.md) (multiplicities when many neurons compete) · [MAIS-O5](MAIS-O5.md) (the headline selection law).*
