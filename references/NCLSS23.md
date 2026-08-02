# Progress measures for grokking via mechanistic interpretability

*Summary [NCLSS23] · N. Nanda, L. Chan, T. Lieberum, J. Smith, and J. Steinhardt, ICLR 2023 · [arXiv:2301.05217](https://arxiv.org/abs/2301.05217).*

*Tags: interpretability · mechanistic interpretability · grokking · training dynamics · harmonic analysis.*

*Summarized by: Claude Fable 5 directed by Lionel Levine.*

**TL;DR.** A one-layer transformer trained on addition mod $P=113$ is reverse-engineered in full: it embeds each residue as sines and cosines at a few "key frequencies" and computes $a+b \bmod P$ by trigonometric identities, so the learned algorithm is Fourier analysis on $\mathbb{Z}/P\mathbb{Z}$. Two progress measures derived from this mechanism show that grokking — the sudden, delayed jump from memorization to perfect generalization — is gradual underneath: training passes through memorization, then circuit formation, then cleanup, and the generalizing circuit forms *before* the visible test-accuracy jump.

## Setup and hypotheses

Inputs are $a,b\in\{0,\dots,P-1\}$, one-hot encoded. The model is a one-layer ReLU transformer with $d_{\text{model}}=128$, four attention heads of dimension 32, $d_{\text{mlp}}=512$, no LayerNorm, untied embedding and unembedding, trained on 30% of the $P^2$ input pairs by full-batch AdamW with weight decay $\lambda=1$ for 40,000 epochs. The skip connection around the MLP is empirically negligible, so the logits factor as $\mathrm{Logits}(a,b)\approx W_L\,\mathrm{MLP}(a,b)$, where $W_L=W_U W_{\text{out}}\in\mathbb{R}^{P\times 512}$ is the neuron–logit map. Write $w_k=2\pi k/P$ for the frequencies of the Fourier basis on $\mathbb{Z}/P\mathbb{Z}$.

## Main results

1. **The algorithm.** The embedding maps $a$ to $\{\sin w_k a, \cos w_k a\}$ at a sparse set of frequencies; attention and MLP compute $\cos w_k(a{+}b)$ and $\sin w_k(a{+}b)$ by the angle-addition identities; the map $W_L$ then assembles $\cos w_k(a{+}b{-}c)$ for each candidate output $c$, and summing over the five key frequencies $k\in\{14,35,41,42,52\}$ makes the logits constructively interfere precisely at $c = a+b \bmod P$.
2. **Evidence.** The embedding is Fourier-sparse (six frequencies); $W_L$ is approximated, with residual below $0.55\%$ in Frobenius norm, by a rank-10 matrix of the form $\sum_k \cos w_k\, u_k^\top + \sin w_k\, v_k^\top$; projecting MLP activations onto the directions $u_k, v_k$ recovers $\cos w_k(a{+}b)$ and $\sin w_k(a{+}b)$ at roughly 93–98% of variance explained; and 433 of the 512 neurons (84.6%) are well fit by degree-2 polynomials of a single frequency.
3. **Ablations.** Deleting any key frequency destroys performance, while deleting *all* non-key frequencies improves the loss by about 70%. Restricting the logits to the ten $W_L$ directions above halves the loss; projecting onto their orthogonal complement gives loss 5.27, worse than uniform guessing.
4. **Progress measures.** *Restricted loss* (keep only the key-frequency terms in the logits) falls well before the test loss does; *excluded loss* (remove the key frequencies) rises while ordinary train loss stays flat, separating memorization from circuit formation; the Gini coefficient of the Fourier norms of $W_E$ and $W_L$ spikes during cleanup.
5. **Three phases.** Memorization (epochs 0–1.4k), circuit formation (1.4k–9.4k: excluded loss rising, weight norm falling), cleanup (9.4k–14k: test loss abruptly drops as weight decay strips away the memorization component). In these experiments grokking requires weight decay or another form of regularization.

## Proof method

Mechanistic reverse engineering: discrete Fourier transforms over $\mathbb{Z}/P\mathbb{Z}$, least-squares fits, fraction of variance explained, and causal ablations performed in the Fourier basis. The findings are empirical rather than proved, but the ablations test the interpretation causally, not merely correlationally. The recovered algorithm is representation-theoretic in spirit: the learned features are characters of the cyclic group.

## Why it matters for AI safety

The safety worry that grokking models in miniature is emergence: a capability absent at every checkpoint we measure, then suddenly present. Here the apparent discontinuity is largely a fact about the metric — measures written in terms of the discovered mechanism reveal smooth, monitorable development well before the jump, a template for forecasting capability transitions rather than being surprised by them. Just as important for this repository, the paper is the paradigm of a fully reverse-engineered network, and what training found is recognizable mathematics: Fourier analysis on $\mathbb{Z}/P\mathbb{Z}$. That one trained network anchors two agendas here: which of the $(P-1)/2$ available frequencies training selects, with what probability, is the selection problem of [MAIS-A5](../agendas/A5/); whether the single-frequency form is forced by the singular geometry of the loss landscape is the subject of [MAIS-A6](../agendas/A6/).

## Cited by

- [MAIS-A5](../agendas/A5/) — takes this network as the founding datum for the representation-selection problem: the key frequencies vary from seed to seed, and the agenda asks for the law of that random choice.
- [MAIS-A6](../agendas/A6/) — the single-frequency Fourier fits whose local learning coefficients the agenda asks to classify are, up to a change of basis, the algorithm reverse-engineered here.
- Problems [MAIS-O6](../open-problems/MAIS-O6.md) · [MAIS-O52](../open-problems/MAIS-O52.md) · [MAIS-O53](../open-problems/MAIS-O53.md) · [MAIS-O58](../open-problems/MAIS-O58.md) · [MAIS-O60](../open-problems/MAIS-O60.md) · [MAIS-O61](../open-problems/MAIS-O61.md) · [MAIS-O63](../open-problems/MAIS-O63.md)
