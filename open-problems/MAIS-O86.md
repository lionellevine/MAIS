# Does gradient descent match the Gaussian process posterior?

*Open problem MAIS-O86 · posed in [MAIS-A8](../agendas/A8/) as [Question 5.10](../agendas/A8/MAIS-A8.tex#L392) · Status: open.*

*Tags: generalization · goal misgeneralization · proxy goals · simplicity bias · singular learning theory · probability · statistics. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Two candidate theories predict what a trained network does off-distribution: the implicit bias of gradient descent, and the Bayesian posterior of the infinite-width Gaussian process prior. On the coin line both make a prediction about the same single number — the probability that the trained agent walks away from a displaced coin — so the theories can be made to disagree, or agree, in a box.

The setting is the agenda's coin line at zero training diversity: an agent at position $p$ and a coin at position $c$ on the line $\lbrace 0,\dots,L\rbrace $ are encoded as $x_{\mathrm a}(p,c)=(1,p,c)$; the training inputs are $x_{\mathrm a}(p,L)$ for $0\le p\le L-1$, all labeled "step right," and the probe $s^{\ast }=(\lceil L/2\rceil,0)$ displaces the coin to the left end, an off-distribution state where "move right" and "go to the coin" disagree. The network is the two-layer ReLU model in the neural-tangent parameterization $f_\theta(x)=m^{-1/2}\sum_j a_j\varphi(u_j\cdot x)$, $\varphi(z)=\max(z,0)$, with unit Gaussian initialization (the agenda's "unit-scale" parameterization; its $m\to\infty$ law at initialization is the Gaussian-process prior appearing below), trained by full-batch gradient descent with step $\eta$ on the logistic loss; the exact training conventions are in [MAIS-A8](../agendas/A8/). A positive probe logit is the proxy verdict, and $q^{\mathrm{ntk}}_0(k;m,L,\eta)$ is the probability, over the random initialization, that the width-$m$ network delivers it after $k$ steps (the subscript records zero training diversity).

**Question ([MAIS-A8, Question 5.10](../agendas/A8/MAIS-A8.tex#L392)).** Valle-Pérez et al. [[VCL19]](https://arxiv.org/abs/1805.08522) and Mingard et al. [[MVSL21]](../references/MVSL21.md) argue that the function distribution produced by stochastic gradient descent can resemble a Bayesian posterior under the corresponding infinite-width Gaussian-process prior. The iteration here is full-batch and deterministic after initialization, so the comparison tests random initialization plus gradient descent, not SGD itself. Bernstein and Yue [[BY22]](https://openreview.net/forum?id=eOdSD0B5TE) make this comparison directly and find an additional large-margin bias. The coin line makes one marginal exactly computable. Let $K(x,x')=\mathbb E_{u\sim N(0,I_3)}[\varphi(u\cdot x)\ \varphi(u\cdot x')]$ (in closed form, $\frac{\lVert x\rVert\lVert x'\rVert}{2\pi}(\sin\vartheta+(\pi-\vartheta)\cos\vartheta)$ with $\vartheta$ the angle between $x,x'$), let $g\sim\mathrm{GP}(0,K)$, and set

$$Q(L)=\mathbb P\bigl(g(x_{\mathrm a}(s^{\ast }))>0\ \big|\ g(x_{\mathrm a}(p,L))>0\text{ for }0\le p\le L-1\bigr),$$

the posterior probability of the proxy verdict at the probe. Provided the Gram matrix on the $L$ training inputs together with the probe is nonsingular, the conditional variance at the probe is positive and $Q(L)<1$. The prior is the $m\to\infty$ law of the unit-scale parameterization. Write $q^{\mathrm{ntk}}_0(k;m,L,\eta)$ for the finite-width backpropagation probability of the proxy verdict in that parameterization. Determine whether

$$\lim_{m\to\infty}\liminf_{k\to\infty}q^{\mathrm{ntk}}_0(k;m,L,\eta)$$

equals $Q(L)$, equals $1$, or equals neither.

The agenda's Proposition 5.3 gives the kernel-flow answer: the infinite-width flow drives the probe logit to $+\infty$, suggesting the value $1$; the Gaussian posterior says strictly less than $1$. Whichever value the finite-width limit takes, one candidate theory is refuted on this marginal. For the kernel-flow proof and a caveat relating this comparison to singular learning theory, see [MAIS-A8](../agendas/A8/).

## References

- [VCL19] G. Valle-Pérez, C. Camargo, and A. Louis, *Deep learning generalizes because the parameter-function map is biased towards simple functions*, ICLR 2019. [arXiv:1805.08522](https://arxiv.org/abs/1805.08522)
- [[MVSL21]](../references/MVSL21.md) C. Mingard, G. Valle-Pérez, J. Skalse, and A. Louis, *Is SGD a Bayesian sampler? Well, almost*, JMLR 22(79):1–64, 2021. [arXiv:2006.15191](https://arxiv.org/abs/2006.15191)
- [BY22] J. Bernstein and Y. Yue, *On the implicit biases of architecture and gradient descent*, ICLR 2022. [OpenReview](https://openreview.net/forum?id=eOdSD0B5TE)

*Related: [MAIS-O90](MAIS-O90.md) (the gradient-descent side of this comparison, isolated) · [MAIS-O50](MAIS-O50.md) (which minima gradient flow selects from random initialization, in a toy autoencoder) · [MAIS-O91](MAIS-O91.md) (computes $Q(L)$ and the training curves numerically).*
