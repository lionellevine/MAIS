# Feature emergence via margin maximization: case studies in algebraic tasks

*Summary [MEOZK24] · D. Morwani, B. L. Edelman, C.-A. Oncescu, R. Zhao, and S. Kakade, ICLR 2024 (spotlight) · [arXiv:2311.07568](https://arxiv.org/abs/2311.07568).*

*Tags: interpretability · mechanistic interpretability · universality of circuits · representation theory · harmonic analysis · optimization.*

*Summarized by: Claude Fable 5 directed by Lionel Levine.*

**TL;DR.** Mechanistic interpretability found that networks trained on modular addition learn Fourier features (Nanda et al.) and networks trained on group multiplication learn irreducible representations (Chughtai et al.); this paper explains why. For one-hidden-layer networks with homogeneous polynomial activations, the maximum-margin solutions — in a norm adapted to the architecture's homogeneity — are characterized in full: on addition mod $p$, every neuron carries a single Fourier frequency and all frequencies appear; on $k$-sparse parity, every neuron lives on the $k$ relevant coordinates; on multiplication in suitable finite groups, every neuron carries a single nontrivial irreducible representation and all of them appear. Margin maximization alone specifies the features, with no appeal to training dynamics.

## Setup and hypotheses

The networks have one hidden layer, untied left and right embeddings $u, v$, an unembedding $w$, and no biases. Activations are homogeneous polynomials: $x^2$ for the group tasks, $x^k$ for $(n,k)$-sparse parity. With quadratic activation the network output is $3$-homogeneous in the parameters $\theta$, so the natural normalized margin — the worst-case gap between the correct logit and its best competitor, over the training set — divides by $\|\theta\|_{2,3}^3$, where $\|\theta\|_{2,3} = (\sum_i \|\omega_i\|_2^3)^{1/3}$ and $\omega_i$ is the concatenated weight vector of neuron $i$. The link to training is a theorem of Wei, Lee, Liu, and Ma: as the coefficient of a regularizer in this same norm tends to zero, global minimizers of the regularized cross-entropy converge in normalized margin to the maximum. Characterizing maximum-margin networks therefore describes the endpoint of weakly regularized training, provided the regularizer matches the norm and the optimizer finds global minima.

## Main results

1. **Modular addition (Theorem 7).** For addition mod $p$ with quadratic activation and width $m \ge 4(p-1)$: in every maximum-margin network, each neuron with nonzero weights is supported on a single Fourier frequency — its three weight vectors are cosines at one common frequency, with phases that add correctly — and each of the $(p-1)/2$ frequencies is used by some neuron. The prediction is *dense*: no frequency is left out.
2. **Sparse parity (Theorem 8).** For $(n,k)$-sparse parity with activation $x^k$ and width $m \ge 2^{k-1}$: every neuron of a maximum-margin network places weight only on the $k$ relevant coordinates, with magnitudes equal across those coordinates and signs consistent with its output weights.
3. **Finite groups (Theorem 9).** For multiplication in a finite group $G$ whose irreducible representations are all real and whose characters satisfy a sign condition (a $d_\rho^{3/2}$-weighted character sum over the nontrivial irreducibles must be negative on every nontrivial conjugacy class): every neuron with nonzero weights is supported on a single nontrivial irreducible representation, and every nontrivial irreducible is present. The condition holds for $S_3$, where the weighted sums are $-1$ on transpositions and $1-2\sqrt{2}$ on $3$-cycles.

Experiments confirm that networks trained with the matching $\ell_{2,3}$ regularization approach the predicted maximum margin and exhibit the predicted per-neuron structure.

## Proof method

Max–min duality with an explicit certificate. To certify that a network $\theta^*$ attains the maximum margin, exhibit a distribution $q^*$ over training pairs such that $q^*$ minimizes the expected margin against $\theta^*$ while $\theta^*$ maximizes it against $q^*$; a lemma then upgrades the pair to a global optimality certificate. The expected margin against a fixed $q^*$ decomposes neuron by neuron, reducing the network-level problem to a single-neuron optimization, which is solved by Fourier analysis in the cyclic case and by representation theory in general — this is where the single-frequency and single-irreducible structure emerges.

## Why it matters for AI safety

Interpretability is easier if trained networks are forced into predictable mechanisms, and this paper gives the sharpest available instance: an optimization principle that pins down the learned features of an algebraic task exactly, matching what reverse-engineering found empirically. But the theorem answers for one implicit bias what practice poses for another. The maximum-$\ell_{2,3}$-margin networks are dense — every frequency, every representation — whereas the standard ensembles (Euclidean squared weight decay, Gaussian initialization) exhibit sparse, run-dependent spectra, and the theorem's norm does not match that regularizer. Which representations a given training run selects, and with what probability, is the selection problem of [MAIS-A5](../agendas/A5/).

## Cited by

- [MAIS-A5](../agendas/A5/) — treats the $\ell_{2,3}$ maximum-margin characterization as the nearest theorem to its representation-selection problem, contrasting its dense prediction with the sparse spectra of the weight-decay ensemble.
- Problems [MAIS-O5](../open-problems/MAIS-O5.md) · [MAIS-O6](../open-problems/MAIS-O6.md) · [MAIS-O52](../open-problems/MAIS-O52.md) · [MAIS-O54](../open-problems/MAIS-O54.md) · [MAIS-O55](../open-problems/MAIS-O55.md) · [MAIS-O56](../open-problems/MAIS-O56.md)
