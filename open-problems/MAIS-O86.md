# Does gradient descent match the Gaussian process posterior?

*Open problem MAIS-O86 · posed in [MAIS-A8](../agendas/A8/MAIS-A8.pdf) as [Question 5.10](../agendas/A8/MAIS-A8.tex#L391) · Status: open.*

*Safety: generalization — goal misgeneralization · proxy goals · simplicity bias · singular learning theory. Mathematics: probability · statistics. Difficulty: ★★★ hard.*

Two candidate theories predict what a trained network does off-distribution: the implicit bias of gradient descent, and the Bayesian posterior of the infinite-width Gaussian process prior. On the coin line both make a prediction about the same single number — the probability that the trained agent walks away from a displaced coin — so the theories can be made to disagree, or agree, in a box.

The setting is the agenda's coin line at zero training diversity: training inputs $x_{\mathrm a}(p,L)=(1,p,L)$ for $0\le p\le L-1$, all labeled "step right," and the probe $s^{\ast }=(\lceil L/2\rceil,0)$, an off-distribution state where "move right" and "go to the coin" disagree. The network is the two-layer ReLU model in the neural-tangent parameterization $f_\theta(x)=m^{-1/2}\sum_j a_j\varphi(u_j\cdot x)$, $\varphi(z)=\max(z,0)$, with unit Gaussian initialization, trained by full-batch gradient descent with step $\eta$; a positive probe logit is the proxy verdict.

**Question ([MAIS-A8, Question 5.10](../agendas/A8/MAIS-A8.tex#L391)).** Valle-Pérez et al. and Mingard et al. argue that the function distribution produced by stochastic gradient descent can resemble a Bayesian posterior under the corresponding infinite-width Gaussian-process prior. The iteration here is full-batch and deterministic after initialization, so the comparison tests random initialization plus gradient descent, not SGD itself. Bernstein and Yue make this comparison directly and find an additional large-margin bias. The coin line makes one marginal exactly computable. Let $K(x,x')=\mathbb E_{u\sim N(0,I_3)}[\varphi(u\cdot x)\ \varphi(u\cdot x')]$ (in closed form, $\frac{\lVert x\rVert\lVert x'\rVert}{2\pi}(\sin\vartheta+(\pi-\vartheta)\cos\vartheta)$ with $\vartheta$ the angle between $x,x'$), let $g\sim\mathrm{GP}(0,K)$, and set

$$Q(L)=\mathbb P\bigl(g(x_{\mathrm a}(s^{\ast }))>0\ \big|\ g(x_{\mathrm a}(p,L))>0\text{ for }0\le p\le L-1\bigr),$$

the posterior probability of the proxy verdict at the probe. Provided the Gram matrix on the $L$ training inputs together with the probe is nonsingular, the conditional variance at the probe is positive and $Q(L)<1$. The prior is the $m\to\infty$ law of the unit-scale parameterization. Write $q^{\mathrm{ntk}}_0(k;m,L,\eta)$ for the finite-width backpropagation probability of the proxy verdict in that parameterization. Determine whether

$$\lim_{m\to\infty}\liminf_{k\to\infty}q^{\mathrm{ntk}}_0(k;m,L,\eta)$$

equals $Q(L)$, equals $1$, or equals neither.

The agenda's Proposition 5.3 gives the kernel-flow answer: the infinite-width flow drives the probe logit to $+\infty$, suggesting the value $1$; the Gaussian posterior says strictly less than $1$. Whichever value the finite-width limit takes, one candidate theory is refuted on this marginal. For the kernel-flow proof and a caveat relating this comparison to singular learning theory, see [MAIS-A8](../agendas/A8/MAIS-A8.pdf).

*Related: [MAIS-O90](MAIS-O90.md) (the gradient-descent side of this comparison, isolated) · [MAIS-O50](MAIS-O50.md) (which minima gradient flow selects from random initialization, in a toy autoencoder) · [MAIS-O91](MAIS-O91.md) (computes $Q(L)$ and the training curves numerically).*
