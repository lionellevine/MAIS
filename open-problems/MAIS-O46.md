# Does lower coherence imply better dictionary recovery?

*Open problem MAIS-O46 · posed in [MAIS-A4](../agendas/A4/) as [Question 5.6](../agendas/A4/MAIS-A4.tex#L405) · Status: open.*

*Tags: interpretability · training for interpretability · sparse autoencoders · superposition · statistics · harmonic analysis. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

An antipodal pair of stored features has coherence $1$ — the worst possible score on the standard legibility metric — yet a sparse autoencoder with nonnegative codes treats $W_i$ and $-W_i$ as different atoms, so the pair is plausibly recoverable. Is coherence ranking dictionaries in the wrong order?

The objects live in the ReLU toy model: features $x\in\mathbb{R}^m$ with independent coordinates, each zero with probability $S$ and otherwise uniform on $[0,1]$, stored as the columns of $W\in\mathbb{R}^{n\times m}$, activations $Wx$. (The eponymous rectifier sits in the model's readout $\mathrm{ReLU}(W^{\top}Wx+b)$ and plays no role here: the interpreter is handed only the activations $Wx$, and the only nonlinearity below is the nonnegativity of the codes, matching the features' nonnegative intensities.) The **coherence** $\mu(W)$ is the maximum of $|\langle\widehat W_i,\widehat W_j\rangle|$ over distinct nonzero columns, normalized. The interpreter fits a dictionary $D\in\mathbb{R}^{n\times d}$ with $\Vert D_j\Vert _2\le1$ by minimizing $J_{W,S,\alpha}(D)=\mathbb{E}_x \min_{a\in\mathbb{R}^d_{\ge0}}\bigl(\Vert Wx-Da\Vert _2^2+\alpha\Vert a\Vert _1\bigr)$, and the predicate $\mathrm{REC}_S(W;d,\alpha,\varepsilon)=1$ holds when every global minimizer contains, up to angle $\varepsilon$ (formally, inner product of normalized columns at least $1-\varepsilon$ under an injective matching), every nonzero column direction of $W$.

**Question ([MAIS-A4, Question 5.6](../agendas/A4/MAIS-A4.tex#L405)).** Do there exist parameters $n,m,d,\alpha,\varepsilon$, a sparsity $S\in(0,1)$, and dictionaries $W,W'\in\mathbb{R}^{n\times m}$, both with unit-norm columns, such that

$$\mu(W)<\mu(W'), \qquad \mathrm{REC}_S(W;d,\alpha,\varepsilon)=0 \quad\text{and}\quad \mathrm{REC}_S(W';d,\alpha,\varepsilon)=1\ ?$$

(The unit-norm condition blocks a cheap answer by scale alone: shrinking $W$ until the optimal code is identically zero makes every $D$ a global minimizer of $J$, killing recovery while leaving the scale-invariant $\mu$ untouched. With norms matched, $\alpha$ strikes both dictionaries equally, and the answer must come from geometry.)

In words: can a strictly more coherent dictionary be recoverable while a strictly less coherent one is not, at the same estimator settings? The agenda expects yes — the antipodal configuration versus an incoherent dictionary whose columns have strongly overlapping supports in $\mathbb{R}^n$ is the suggested pair — and a proof would be the toy world's Goodhart's law for interpretability metrics: optimize the proxy, lose the target. The empirical precedent is the [SoLU episode](https://transformer-circuits.pub/2022/solu/index.html), in which Anthropic replaced the nonlinearity of transformer language models with softmax linear units: neurons looked more legible, but superposition had partly hidden rather than vanished. Definitions and context are in [MAIS-A4](../agendas/A4/).

## References

- Elhage, N., et al. (2022). Toy models of superposition. *Transformer Circuits Thread*. [arXiv:2209.10652](https://arxiv.org/abs/2209.10652)
- Gribonval, R., Jenatton, R., and Bach, F. (2015). Sparse and spurious: dictionary learning with noise and outliers. *IEEE Transactions on Information Theory* 61(11), 6298–6319. [arXiv:1407.5155](https://arxiv.org/abs/1407.5155)
- Cui, J., Zhang, Q., Wang, Y., and Wang, Y. (2025). On the limits of sparse autoencoders: a theoretical framework and reweighted remedy. [arXiv:2506.15963](https://arxiv.org/abs/2506.15963)

*Related: [MAIS-O45](MAIS-O45.md) (recovery of the antipodal configuration, the expected witness) · [MAIS-O44](MAIS-O44.md) (training to lower coherence, the proxy in question) · [MAIS-O41](MAIS-O41.md) (two-feature phase diagram of the same estimator) · [MAIS-O3](MAIS-O3.md) (identifiability theory for the $\ell^1$ estimator).*
