# A toy model of universality: reverse engineering how networks learn group operations

*Summary [CCN23] · B. Chughtai, L. Chan, and N. Nanda, ICML 2023 · [arXiv:2302.03025](https://arxiv.org/abs/2302.03025).*

*Tags: interpretability · mechanistic interpretability · universality of circuits · representation theory · training dynamics.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Small networks trained to compute the product in a finite group $G$ implement one algorithm family — **Group Composition via Representations** — acting through a *sparse subset* of the irreducible representations of $G$. The algorithm's correctness is a theorem of representation theory; that trained networks implement it is an empirical finding, confirmed by ablation. Universality splits in two: *weak* universality (always this algorithm family) holds across seeds, while *strong* universality (the same specific irreducible representations) fails — which irreps a network uses depends on the random initialization.

## Setup and hypotheses

Train an MLP (with untied left and right embeddings) or a one-layer transformer to map a pair $(a,b)$ to the product $ab$ in a finite group $G$, with weight decay, in the grokking regime. Groups studied: the cyclic groups $C_{113}$ and $C_{118}$ (abelian), and the dihedral $D_{59}$ and $D_{61}$, symmetric $S_5$ and $S_6$, and alternating $A_5$ (nonabelian). This generalizes Nanda et al.'s reverse engineering of modular addition, where the one-dimensional irreps of an abelian group give the Fourier "clock," to groups with genuinely higher-dimensional representations.

## Main results

For an irreducible representation $\rho: G \to GL_{d_\rho}(\mathbb{C})$, the trained network's embeddings carry the matrices $\rho(a)$ and $\rho(b)$; the hidden layer forms the product $\rho(a)\rho(b) = \rho(ab)$; and the unembedding reads off each logit as $\mathrm{tr}\,\rho(ab)\rho(c^{-1}) = \chi_\rho(abc^{-1})$, which is maximized exactly at the correct answer $c = ab$ (a character of a faithful irrep is maximized at the identity; their Theorem D.7). Several irreps run in parallel, and since characters of distinct irreps are orthogonal (their Theorem D.9), the summed logits interfere constructively at the answer. Networks genuinely use irreps with $d_\rho > 1$, such as the four-dimensional standard representation of $S_5$.

Which irreps, however, is chosen by the seed: different random initializations of the same architecture on the same group land on different sparse subsets, and transformers use fewer irreps than MLPs. The authors' candidate explanation — that networks prefer irreps of low dimension — is empirically falsified.

## Method

Representation theory proves the algorithm correct; a battery of measurements shows the networks implement it. The logits correlate with the characters $\chi_\rho$; the embeddings are low-rank in the irrep basis; neurons cluster by the irrep they serve; and ablations confirm causality — deleting the components in the used irreps destroys performance, deleting the rest does not.

## Why it matters for AI safety

Mechanistic interpretability findings transfer across training runs only to the extent that what a network learns is reproducible. This paper supplies the sharpest small-scale evidence on both sides at once: the algorithm family is stable across seeds, but the instance — the set of irreps — is a random variable whose law nobody knows. The four $S_5$ seed tables reported here are, in the framing of [MAIS-A5](../agendas/A5/), four samples from the *selection law*, and the agenda's central problem asks for that law: does it converge, is it deterministic, and can it be computed in any explicit case?

## Cited by

- [MAIS-A5](../agendas/A5/) — takes the character-based algorithm as its structural backbone and treats the paper's seed tables as samples from the selection law it seeks to compute.
- Problems [MAIS-O5](../open-problems/MAIS-O5.md) · [MAIS-O52](../open-problems/MAIS-O52.md) · [MAIS-O53](../open-problems/MAIS-O53.md) · [MAIS-O55](../open-problems/MAIS-O55.md) · [MAIS-O56](../open-problems/MAIS-O56.md) · [MAIS-O57](../open-problems/MAIS-O57.md) · [MAIS-O58](../open-problems/MAIS-O58.md) · [MAIS-O61](../open-problems/MAIS-O61.md)
