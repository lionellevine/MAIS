# Pentagon optimality for a pure ReLU packing energy

*Open problem MAIS-O42 · posed in [MAIS-A3](../agendas/A3/) as [Problem 5.2](../agendas/A3/MAIS-A3.tex#L337) · Status: open.*

*Tags: interpretability · superposition · mechanistic interpretability · optimization · harmonic analysis. Difficulty: ★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Five points on or inside a circle, repelling one another through a ReLU: prove the regular pentagon wins. This is the pentagon conjecture for the superposition toy model ([MAIS-O40](MAIS-O40.md)) with the interaction between sparsity levels stripped away, leaving a pure packing energy.

The toy model of Elhage et al. [[EHOS+22]](../references/EHOS+22.md) is mechanistic interpretability's minimal laboratory for **superposition** — a network representing more features than it has dimensions, which is why individual neurons resist interpretation. It reconstructs a sparse vector $x\in\mathbb{R}^5$ through a two-dimensional bottleneck: the loss is $L(W,b)=\mathbb{E}\ \lVert x-\mathrm{ReLU}(W^{\top}Wx+b)\rVert^2$ over $W\in\mathbb{R}^{2\times5}$ and $b\in\mathbb{R}^5$, where $\mathrm{ReLU}(t)=\max(t,0)$ acts coordinatewise and the columns $w_1,\dots,w_5$ of $W$ are the feature directions. In the full model each coordinate of $x$ is nonzero with probability $p$ independently, uniform on $[0,1]$ when nonzero; conditioning on exactly one active coordinate removes the sparsity parameter $p$ entirely.

**Problem ([MAIS-A3, Problem 5.2](../agendas/A3/MAIS-A3.tex#L337)).** Let $L_1(W,b)$ be $L$ with $x$ conditioned on having exactly one nonzero coordinate (uniform among the five, value $\mathrm{Unif}[0,1]$); the parameter $p$ drops out. Prove that $L_1$ attains its infimum and that the columns of every global minimizer form a regular pentagon, in the sense of the agenda's Conjecture 4.10: nonzero columns of equal norm $r$ with $\langle w_{\tau(i)},w_{\tau(j)}\rangle=r^2\cos\bigl(2\pi(i-j)/5\bigr)$ for some permutation $\tau$ of $[5]$.

With one active coordinate the squared error splits into a diagonal term that tunes each column's norm and cross terms that penalize positive inner products between columns through the ReLU — the repulsion of the opening picture; the circle is part of the conclusion (a common norm for the minimizing columns), not a constraint.

The natural template is the frame-potential theorem of Benedetto and Fickus [BF03], the linear shadow of the conjecture: among $m\ge n$ unit vectors in $\mathbb{R}^n$, the minimizers of the frame potential $\sum_{i\neq j}\langle w_i,w_j\rangle^2$ are precisely the tight frames — systems with $\sum_i w_iw_i^{\top}$ proportional to the identity. Five unit vectors in the plane form many tight frames, the pentagon among them, so the linear theorem stops short of selecting it; that selection is the work left to the ReLU and the bias. The Benedetto–Fickus proof rewrites the energy as a sum of squared Gram entries and characterizes its critical points. The ReLU breaks that rewriting — the energy is piecewise rational rather than polynomial — and where the template breaks is where the new mathematics begins.

Partial progress: Chen, Lau, Mendel, Wei, and Murfet [[CLMWM23]](../references/CLMWM23.md) prove that the regular $k$-gons are critical points of the two-dimensional toy model, ruling the pentagon in as a candidate; global minimality is open, here and in the full model. For the closed-form loss at the regular $k$-gons and the surrounding critical-point theory, see [MAIS-A3](../agendas/A3/).

## References

- [[BF03]](../references/BF03.md) J. J. Benedetto and M. Fickus, *Finite normalized tight frames*, Adv. Comput. Math. **18** (2003), 357–385.
- [[EHOS+22]](../references/EHOS+22.md) N. Elhage et al., *Toy models of superposition*, Transformer Circuits Thread, Anthropic, 2022. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- [[CLMWM23]](../references/CLMWM23.md) Z. Chen, E. Lau, J. Mendel, S. Wei, and D. Murfet, *Dynamical versus Bayesian phase transitions in a toy model of superposition*, 2023. [arXiv:2310.06301](https://arxiv.org/abs/2310.06301)

*Related: [MAIS-O40](MAIS-O40.md) (the full pentagon conjecture this is a starter for) · [MAIS-O47](MAIS-O47.md) (uniqueness of toy-model minimizers up to symmetry) · [MAIS-O4](MAIS-O4.md) (the toy model's loss under a coherence constraint).*
