# Regular pentagon as global minimizer of a ReLU autoencoder

*Open problem MAIS-O40 · posed in [MAIS-A3](../agendas/A3/) as [Conjecture 4.10](../agendas/A3/MAIS-A3.tex#L318) · Status: open.*

*Tags: interpretability · superposition · mechanistic interpretability · optimization · harmonic analysis. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Train a tiny autoencoder to squeeze five sparse features through two dimensions, and its five weight vectors crystallize into a regular pentagon. This is the experiment of *Toy models of superposition* (Elhage et al. [[EHOS+22]](../references/EHOS+22.md)) in which superposition — a network representing more features than it has dimensions, a central obstacle to reading off what a model has learned — was first exhibited, and the pentagon is its emblem. No theorem yet says the pentagon wins.

The model: fix $m$ features, $n<m$ dimensions, and a sparsity parameter $p\in(0,1)$. Let $x\in\mathbb{R}^m$ have independent coordinates $x_i=\zeta_i\omega_i$ with $\zeta_i\sim\mathrm{Bernoulli}(p)$ and $\omega_i\sim\mathrm{Unif}[0,1]$, and define

$$L(W,b)\ =\ \mathbb{E}\ \bigl\lVert x-\mathrm{ReLU}(W^{\top}W x+b)\bigr\rVert^2, \qquad W\in\mathbb{R}^{n\times m},\ b\in\mathbb{R}^m,$$

with $\mathrm{ReLU}(t)=\max(t,0)$ applied coordinatewise. The columns $w_1,\dots,w_m$ of $W$ are the model's feature directions, not constrained to unit norm. For the linear analogue the answer is a theorem of Benedetto and Fickus [BF03]: for $m\ge n$, the minimizers of the frame potential $\sum_{i\neq j}\langle w_i,w_j\rangle^2$ over systems of $m$ unit vectors are precisely the unit-norm tight frames, the systems with $\sum_i w_iw_i^{\top}$ a multiple of the identity. The ReLU and the bias select, among the many tight frames, the maximally spread one — empirically.

**Conjecture ([MAIS-A3, Conjecture 4.10](../agendas/A3/MAIS-A3.tex#L318)).** There is a nonempty open interval $I\subset(0,1)$ such that for every $p\in I$, the loss $L$ with $n=2$, $m=5$ attains its infimum, and every global minimizer $(W,b)$ has nonzero columns of equal norm $r>0$ satisfying, for some permutation $\tau$ of $[5]$,

$$\langle w_{\tau(i)},w_{\tau(j)}\rangle\ =\ r^2\cos\bigl(2\pi(i-j)/5\bigr) \qquad\text{for all } i,j.$$

Equivalently: up to an orthogonal transformation of $\mathbb{R}^2$ and relabeling, the columns form a regular pentagon.

Every quantity is explicit: the loss is a semialgebraic integral in fifteen variables (ten entries of $W$, five of $b$), piecewise rational because of the moving ReLU breakpoints. Critical-point theory rules the pentagon in as a candidate — the regular $k$-gons are critical with the loss in closed form (Chen et al. [[CLMWM23]](../references/CLMWM23.md)), and under a capacity-saturation hypothesis, made precise in Ivanov et al. [[IORP+26]](https://arxiv.org/abs/2602.02224), critical configurations organize into tight frames with a discrete classification. What is missing is a symmetrization technique for ReLU energies that reaches *global* minimality. For the toy-model background and the frame-theory shadow, see [MAIS-A3](../agendas/A3/).

## References

- [[BF03]](../references/BF03.md) J. J. Benedetto and M. Fickus, *Finite normalized tight frames*, Adv. Comput. Math. **18** (2003), 357–385.
- [[CLMWM23]](../references/CLMWM23.md) Z. Chen, E. Lau, J. Mendel, S. Wei, and D. Murfet, *Dynamical versus Bayesian phase transitions in a toy model of superposition*, 2023. [arXiv:2310.06301](https://arxiv.org/abs/2310.06301)
- [[EHOS+22]](../references/EHOS+22.md) N. Elhage, T. Hume, C. Olsson, N. Schiefer, et al., *Toy models of superposition*, Transformer Circuits Thread, Anthropic, 2022. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- [IORP+26] G. Ivanov, N. Oozeer, S. Raval, T. Pejovic, S. Upadhyay, and A. Abdullah, *Spectral superposition: a theory of feature geometry*, 2026. [arXiv:2602.02224](https://arxiv.org/abs/2602.02224)

*Related: [MAIS-O42](MAIS-O42.md) (the one-active-feature case, a starter) · [MAIS-O47](MAIS-O47.md) (uniqueness of minimizers of the same toy model up to symmetry) · [MAIS-O4](MAIS-O4.md) (the toy model's loss frontier under a coherence constraint).*
