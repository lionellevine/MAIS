# Spectral superposition: a theory of feature geometry

*Summary [IORP+26] · G. Ivanov, N. Oozeer, S. Raval, T. Pejovic, S. Upadhyay, and A. Abdullah, 2026 · [arXiv:2602.02224](https://arxiv.org/abs/2602.02224).*

*Tags: interpretability · superposition · mechanistic interpretability · optimization · harmonic analysis.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** A spectral theory of the feature geometries that arise in superposition: analyze the frame operator $F=WW^{\top}$ of the weight matrix and the spectral measure recording how each feature's norm distributes across its eigenspaces. In the toy models of superposition, under an empirically motivated *capacity-saturation* hypothesis, the theory forces spectral localization — each feature collapses onto a single eigenspace — after which features organize into tight frames and the possible geometries admit a discrete classification via association schemes, recovering the configurations observed in training (simplices, polygons, antiprisms). The structure theory is conditional: it does not prove that global minimizers saturate capacity.

## Setting

The object of study is the feature geometry of a network in superposition — more features than dimensions, so the feature directions $w_1,\dots,w_m\in\mathbb{R}^n$ (the columns of a weight matrix $W\in\mathbb{R}^{n\times m}$, $m>n$) must interfere. Sparse dictionary methods describe such features pairwise, through inner products; this paper studies them globally, through the spectrum of the frame operator $F=WW^{\top}$ and the associated spectral measure of each feature, which records how that feature allocates its norm across the eigenspaces of $F$. The theorems are proved in the toy models of superposition of Elhage et al. [[EHOS+22]](EHOS+22.md), under the hypothesis that the trained configuration saturates capacity; the spectral-measure formalism itself applies to arbitrary weight matrices.

## Main results

1. **Spectral localization.** Capacity saturation forces each feature's spectral measure to concentrate on a single eigenspace of the frame operator.
2. **Tight-frame organization.** The localized features organize into tight frames — the same structure that the Benedetto–Fickus theorem [[BF03]](BF03.md) identifies as optimal for the linear frame potential.
3. **Discrete classification.** Via association schemes, the possible saturated geometries admit a discrete classification, which accounts for the configurations reported in prior empirical work: simplices, regular polygons, antiprisms.

What is *not* proved: that global minimizers of the toy-model loss satisfy capacity saturation, or that any particular geometry (the pentagon, say) is globally optimal. The hypothesis is empirical, and the classification is conditional on it.

## Method

Operator-theoretic. The frame operator's spectral decomposition converts a question about $m$ interacting vectors into a question about how norm distributes over few eigenspaces; capacity saturation is the input that pins each feature to one eigenspace, and the combinatorics of the resulting tight frames is organized by association schemes. (This summary is written from the abstract and the citing agendas' statements of the results; the proofs were not checked against the full text.)

## Why it matters for AI safety

Superposition is a central obstacle to reading off what a model has learned, and the toy-model geometries are its emblem. This paper is the nearest nonlinear analogue to date of the Benedetto–Fickus theorem: a structure theory for the geometries a ReLU model can adopt, at the level of a conditional classification rather than global optimality. The gap it leaves open is precisely where the agendas dig. Conjecture 4.10 of [MAIS-A3](../agendas/A3/) asks for the missing global statement — that the regular pentagon *wins* in the $(5,2)$ model — with this classification ruling the pentagon in as a candidate; [MAIS-A4](../agendas/A4/) asks whether global minimizers saturate capacity at all, and whether minimizers are unique up to symmetry, turning the paper's empirical hypothesis into the open problem.

## Cited by

- [MAIS-A3](../agendas/A3/) — cites the conditional tight-frame classification as the critical-point-level evidence for the pentagon conjecture.
- [MAIS-A4](../agendas/A4/) — uses the capacity-saturation hypothesis as the frontier: proving it for global minimizers, and breaking ties among classified geometries, are the agenda's problems.
- Problems [MAIS-O40](../open-problems/MAIS-O40.md) · [MAIS-O47](../open-problems/MAIS-O47.md)
