# Pentagon optimality for a pure ReLU packing energy

*Open problem MAIS-O42 · posed in [MAIS-A3](../agendas/A3/) as [Problem 5.2](../agendas/A3/MAIS-A3.tex#L336) · Status: open.*

*Safety: interpretability — superposition · mechanistic interpretability. Mathematics: optimization · harmonic analysis. Difficulty: ★★ project.*

Five points on or inside a circle, repelling one another through a ReLU: prove the regular pentagon wins. This is the pentagon conjecture for the superposition toy model ([MAIS-O40](MAIS-O40.md)) with the interaction between sparsity levels stripped away, leaving a pure packing energy.

The toy model of Elhage et al. reconstructs a sparse vector $x\in\mathbb{R}^5$ through a two-dimensional bottleneck: the loss is $L(W,b)=\mathbb{E}\ \lVert x-\mathrm{ReLU}(W^{\top}Wx+b)\rVert^2$ over $W\in\mathbb{R}^{2\times5}$ and $b\in\mathbb{R}^5$, where $\mathrm{ReLU}(t)=\max(t,0)$ acts coordinatewise and the columns $w_1,\dots,w_5$ of $W$ are the feature directions. In the full model each coordinate of $x$ is nonzero with probability $p$ independently, uniform on $[0,1]$ when nonzero; conditioning on exactly one active coordinate removes the sparsity parameter $p$ entirely.

**Problem ([MAIS-A3, Problem 5.2](../agendas/A3/MAIS-A3.tex#L336)).** Let $L_1(W,b)$ be $L$ with $x$ conditioned on having exactly one nonzero coordinate (uniform among the five, value $\mathrm{Unif}[0,1]$); the parameter $p$ drops out. Prove that $L_1$ attains its infimum and that the columns of every global minimizer form a regular pentagon, in the sense of the agenda's Conjecture 4.10: nonzero columns of equal norm $r$ with $\langle w_{\tau(i)},w_{\tau(j)}\rangle=r^2\cos\bigl(2\pi(i-j)/5\bigr)$ for some permutation $\tau$ of $[5]$.

The natural template is the Benedetto–Fickus frame-potential theorem, the linear shadow of the conjecture: rewrite the energy as a sum of squared Gram entries and characterize its critical points. The ReLU breaks that rewriting — the energy is piecewise rational rather than polynomial — and where the template breaks is where the new mathematics begins. For the closed-form loss at the regular $k$-gons and the surrounding critical-point theory, see [MAIS-A3](../agendas/A3/).

*Related: [MAIS-O40](MAIS-O40.md) (the full pentagon conjecture this is a starter for) · [MAIS-O47](MAIS-O47.md) (uniqueness of toy-model minimizers up to symmetry) · [MAIS-O4](MAIS-O4.md) (the toy model's loss under a coherence constraint).*
