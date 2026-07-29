# Engineering monosemanticity in toy models

*Summary [JSH22] · A. S. Jermyn, N. Schiefer, and E. Hubinger, arXiv 2022 · [arXiv:2211.09169](https://arxiv.org/abs/2211.09169).*

*Tags: interpretability · training for interpretability · monosemanticity · superposition · training dynamics.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** In a toy sparse-feature model, the loss landscape contains both monosemantic and polysemantic local minima at essentially the same loss, so a network's legibility is decided not by what training optimizes but by which minimum it finds. The paper turns this into an engineering handle: monosemantic neurons are marked by moderate negative bias, and initializing biases negative (with weight decay) steers training into highly monosemantic basins at no cost in performance. The resulting models are interpretable enough to reverse-engineer completely, including their residual polysemantic neurons.

## Setup

Features $f\in\mathbb{R}^N$ are sparse: each coordinate is zero with some probability and otherwise uniform on $[0,1]$, with either uniform or power-law sparsity across coordinates. The network never sees $f$ directly; a fixed random projection $P$ compresses it to an input $Pf\in\mathbb{R}^d$ with $N\gg d$. The model is a one-hidden-layer network — linear map with bias, elementwise nonlinearity (ReLU by default) over $k$ hidden units, then a *linear output layer with no bias* — trained by mean squared error on one of three tasks: decode $f$ from $Pf$, re-project to $Qf$ under a second random projection, or compute a coordinatewise absolute difference. A neuron is scored by the fraction of its total positive response concentrated on its single favorite feature, and called monosemantic when that fraction exceeds $0.999$.

## Main results

1. **Loss does not see legibility.** Training runs differing only in learning rate converge to minima with identical loss but very different monosemanticity: the monosemantic–polysemantic distinction lives in the choice of basin, not in the objective.
2. **A bias signature, and a lever.** Monosemantic neurons sit at moderate negative bias, polysemantic ones at small positive bias. Initializing all biases near $-1$ and applying weight decay reliably lands training in highly monosemantic minima, with no degradation in loss.
3. **More neurons, more monosemanticity.** Widening the hidden layer makes models more monosemantic; with $k>N$ the model approaches one monosemantic neuron per feature, at increased computational cost but negligible further loss improvement.
4. **Full reverse-engineering.** The engineered models are mechanistically interpretable end to end. The few remaining polysemantic neurons implement a simple algorithm: a low-rank approximation of the identity that applies a global confidence correction to the output, rather than any feature-specific computation.

## Method

Empirical throughout: train the toy model across learning rates, sparsity levels, and widths; classify neurons by the concentration score; compare the loss and monosemanticity of the minima found; then intervene on the identified correlate (bias initialization plus weight decay) and confirm that it moves which basin training selects. The interpretability claims are cashed out by explicitly reading the learned weights, including the singular-value analysis of the polysemantic block.

## Why it matters for AI safety

If interpretable and uninterpretable networks can sit at the same loss, then legibility is a property we may get to choose — provided we understand what steers the choice. This paper is the empirical prototype of that idea, and [MAIS-A4](../agendas/A4/) sets out to make it mathematics. The agenda's privileged-basis autoencoder is motivated by (but deliberately not identical to) the architecture here: it drops the random projection and uses a ReLU output layer with bias, so the comparison isolates what the results depend on. The paper's coexisting minima become the target of [MAIS-O48](../open-problems/MAIS-O48.md) part 2, which asks for nearby monosemantic and polysemantic local minima in the agenda's architecture, and its steering phenomenon becomes the selection question of [MAIS-O50](../open-problems/MAIS-O50.md): when loss is blind to monosemanticity, what does gradient flow pick? See [MAIS-A4](../agendas/A4/).

## Cited by

- [MAIS-A4](../agendas/A4/) — the monosemanticity surrogate and its model organism are motivated by this architecture; the local-minima observation anchors the training-for-interpretability discussion.
- Problems [MAIS-O48](../open-problems/MAIS-O48.md) · [MAIS-O50](../open-problems/MAIS-O50.md)
