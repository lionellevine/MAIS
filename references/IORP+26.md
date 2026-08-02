# Spectral superposition: a theory of feature geometry

*Summary [IORP+26] · G. Ivanov, N. Oozeer, S. Raval, T. Pejovic, S. Upadhyay, and A. Abdullah, 2026 · [arXiv:2602.02224](https://arxiv.org/abs/2602.02224).*

*Tags: interpretability · superposition · mechanistic interpretability · optimization · harmonic analysis.*

*Summarized by: Claude Fable 5 directed by Lionel Levine.*

**TL;DR.** A spectral theory of the feature geometries that arise in superposition: analyze the frame operator $F=WW^{\top}$ of the weight matrix and the spectral measure recording how each feature's norm distributes across its eigenspaces. In the toy models of superposition, under an empirically motivated *capacity-saturation* hypothesis, the theory forces spectral localization — each feature collapses onto a single eigenspace — after which features organize into tight frames and the possible geometries admit a discrete classification via association schemes, recovering the configurations observed in training (simplices, polygons, antiprisms). The structure theory is conditional: it does not prove that global minimizers saturate capacity.

## Setting

The object of study is the feature geometry of a network in superposition — more features than dimensions, so the feature directions $w_1,\dots,w_m\in\mathbb{R}^n$ (the columns of a weight matrix $W\in\mathbb{R}^{n\times m}$, $m>n$) must interfere. Sparse dictionary methods describe such features pairwise, through inner products; this paper studies them globally, through the spectrum of the frame operator $F=WW^{\top}$ and the associated spectral measure of each feature, which records how that feature allocates its norm across the eigenspaces of $F$. The theorems are proved in the toy models of superposition of Elhage et al. [[EHOS+22]](EHOS+22.md), under the hypothesis that the trained configuration saturates capacity; the spectral-measure formalism itself applies to arbitrary weight matrices.

## Main results

1. **Spectral localization.** Capacity saturation forces each feature's spectral measure to concentrate on a single eigenspace of the frame operator.
2. **Tight-frame organization.** The localized features organize into tight frames — the same structure that the Benedetto–Fickus theorem [[BF03]](BF03.md) identifies as optimal for the linear frame potential.
3. **Discrete classification.** Via association schemes, the possible saturated geometries admit a discrete classification, which accounts for the configurations reported in prior empirical work: simplices, regular polygons, antiprisms.

What is *not* proved: that global minimizers of the toy-model loss satisfy capacity saturation, or that any particular geometry (the pentagon, say) is globally optimal. The hypothesis is empirical, and the classification is conditional on it.

## Method

Operator-theoretic. The frame operator's spectral decomposition converts a question about $m$ interacting vectors into a question about how each vector's norm is distributed across eigenspaces. Under capacity saturation, the optimality conditions force each feature's spectral measure onto one eigenspace. The resulting inner-product relations form association schemes, which organize the discrete classification of tight-frame geometries.

## Why it matters for AI safety

Superposition makes features interfere and complicates attempts to read them from a network's weights. This paper gives a conditional structure theorem for the resulting ReLU toy-model geometries: if capacity is saturated, the possible configurations are spectrally localized tight frames. It does not prove capacity saturation or global optimality of the regular pentagon in the $(5,2)$ model. Those missing steps are posed in [MAIS-A3](../agendas/A3/) and [MAIS-A4](../agendas/A4/).

## Cited by

- [MAIS-A3](../agendas/A3/) — cites the conditional tight-frame classification as the critical-point-level evidence for the pentagon conjecture.
- [MAIS-A4](../agendas/A4/) — uses the capacity-saturation hypothesis as the frontier: proving it for global minimizers, and breaking ties among classified geometries, are the agenda's problems.
- Problems [MAIS-O40](../open-problems/MAIS-O40.md) · [MAIS-O47](../open-problems/MAIS-O47.md)
