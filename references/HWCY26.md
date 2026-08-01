# On the mechanism and dynamics of modular addition: Fourier features, lottery ticket, and grokking

*Summary [HWCY26] · J. He, L. Wang, S. Chen, and Z. Yang, preprint 2026 · [arXiv:2602.16849](https://arxiv.org/abs/2602.16849).*

*Tags: interpretability · mechanistic interpretability · training dynamics · dynamical systems · harmonic analysis.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** An end-to-end account of how a two-layer network learns addition mod $p$: the mechanism (single-frequency neurons whose phases satisfy a symmetry condition, so that their noisy individual votes cancel and the logits approximate the indicator of the correct sum), the dynamics (from small single-frequency initializations, gradient flow preserves the frequency and aligns the phases; when frequencies compete inside a neuron, the one with the largest initial magnitude and the best-aligned phase wins — a lottery decided at initialization), and grokking (memorization, then two generalization phases, driven by the competition between loss minimization and weight decay). The theorems live in a small-initialization, early-stage decoupled regime; the behavior at full random initialization is documented empirically.

## Setting

The network is two-layer without bias: inputs $x,y \in C_p$ are embedded as $h_x, h_y$, and the logits are $f(x,y) = \sum_{m=1}^M \xi_m\, \sigma(\langle h_x + h_y, \theta_m\rangle)$ with activation $\sigma$ quadratic or ReLU, trained by cross-entropy over the addition table (weight decay enters in the grokking experiments). Each neuron is read in Fourier coordinates: per frequency $k$, a pair of input magnitudes with phases and an output magnitude with phase, so that the training dynamics become an explicit ODE system in magnitudes and phase differences.

## Main results

1. **Mechanism (Proposition 4.2).** If the trained neurons are *fully diversified* — each frequency carried by equally many neurons, with homogeneous scaling and a phase-symmetry condition across the neurons sharing a frequency — and each neuron's phases are aligned, then the logits equal a scaled indicator of $x+y \bmod p$ plus noise terms it dominates. Each single-frequency neuron alone is a noisy voter; the phase symmetry is what makes the ensemble's majority vote exact enough for softmax to concentrate on the right answer.
2. **Single-frequency dynamics (Theorems 5.2–5.3).** From a small initialization in which each neuron carries a single frequency with random phases, gradient flow keeps the other frequencies asymptotically negligible through the initial stage, and the neuron's phase misalignment decreases monotonically to zero, with growth of the magnitudes governed by its cosine.
3. **Lottery ticket (Corollary 6.1).** From a controlled initialization in which several frequencies coexist inside a neuron, the frequency with the largest initial magnitudes and the smallest phase misalignment outgrows the others exponentially, by an ODE comparison argument. Which feature a neuron learns is decided by the random draw at initialization.
4. **Rectifier dynamics (Proposition 6.3).** The quadratic analysis extends to ReLU in the form of a growth-and-leakage estimate starting from a controlled single-frequency state.
5. **Grokking (empirical).** Training with weight decay passes through memorization, then a first generalization stage in which weight decay sparsifies the spectrum, then a slow second stage refining to perfect generalization.

## Method

Small initialization decouples the network: for early times each neuron's dynamics can be approximated by an autonomous ODE in its own Fourier magnitudes and phase differences, and cross-neuron and cross-frequency interactions are error terms. Within that approximation, phase alignment is a monotone convergence argument and frequency competition is settled by comparison lemmas between the coupled magnitude ODEs. The rigorous statements are confined to this regime — initializations that are small, single-frequency, or of controlled equal magnitudes — and the paper's experiments (gradient flow on quadratic networks, SGD on ReLU networks) supply the evidence that the same picture holds from generic random starts.

## Why it matters for AI safety

Which representation a network adopts can depend on random initialization. [MAIS-A5](../agendas/A5/) asks for the resulting probability distribution over learned mechanisms. This paper proves a rigorous winner-take-all mechanism for modular addition under small or specially controlled initial states. Unit-scale Gaussian initialization lies outside its theorems, including the small cases posed in [MAIS-O59](../open-problems/MAIS-O59.md) and [MAIS-O60](../open-problems/MAIS-O60.md) (the latter since resolved in the negative by counterexamples outside this paper's controlled regime).

## Cited by

- [MAIS-A5](../agendas/A5/) — the nearest rigorous training dynamics to the agenda's selection-law problems; its small-initialization hypotheses delimit what the agenda's problems must go beyond.
- Problems [MAIS-O59](../open-problems/MAIS-O59.md) · [MAIS-O60](../open-problems/MAIS-O60.md)
