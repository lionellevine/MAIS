# Metastability in reversible diffusion processes I: sharp asymptotics for capacities and exit times

*Summary [BEGK04] · A. Bovier, M. Eckhoff, V. Gayrard, and M. Klein, J. Eur. Math. Soc. 6 (2004), 399–424.*

*Tags: training dynamics · singular learning theory · generalization · probability.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** For a reversible diffusion in a Morse landscape, the mean time to cross from a metastable well into a deeper one is a computable constant times $e^{h/\varepsilon}$, where $h$ is the barrier height and the constant is built from Hessian data at the starting minimum and at the saddle. This is the Eyring–Kramers formula, conjectured in the chemistry literature since the 1930s; this paper gave the first rigorous proof with the sharp prefactor in arbitrary dimension. The proof runs through an exact identity: mean crossing time equals the Gibbs mass of the starting well divided by the potential-theoretic capacity between the wells.

## Setup and hypotheses

The process is the Langevin diffusion $dX_t = -\nabla F(X_t)\,dt + \sqrt{2\varepsilon}\,dB_t$ on $\mathbb{R}^d$, reversible with respect to the Gibbs measure $e^{-F/\varepsilon}\,dx$. The potential $F$ is smooth with finitely many critical points, all nondegenerate (Morse), and satisfies growth conditions at infinity making the Gibbs measure finite and the level sets exponentially tight. The two objects of the title: the **capacity** between two wells is the conductance of the Dirichlet form between neighborhoods of their minima — equivalently, the minimal Dirichlet energy among functions equal to one on one neighborhood and zero on the other — and the crossing happens through the **gate**, the set of saddles at the communication height $h$, the lowest level at which the two wells are connected.

## Main results

1. **Sharp capacity asymptotics.** The capacity between a metastable minimum $x$ and the set of deeper minima is, to leading order, a sum over the gate saddles $z^\ast$ of explicit Hessian terms of order $\varepsilon^{d/2} e^{-F(z^\ast)/\varepsilon}$, with relative errors vanishing as $\varepsilon \to 0$.
2. **Eyring–Kramers law.** When the gate is a single saddle $z^\ast$ with unique negative Hessian eigenvalue $\lambda^\ast$, the mean hitting time of the deeper wells from $x$ is
   $$\mathbb{E}_x[\tau] = \frac{2\pi}{|\lambda^\ast|} \sqrt{\frac{|\det \nabla^2 F(z^\ast)|}{\det \nabla^2 F(x)}}\; e^{(F(z^\ast)-F(x))/\varepsilon}\,(1+o(1)).$$
   In words: the exponential rate is the barrier height, as Freidlin–Wentzell theory already gave, and the prefactor is a ratio of Hessian determinants — the flatnesses of the well and of the pass — corrected by the unstable curvature at the pass. Gates with several saddles contribute additively through the capacity.

The companion paper (Bovier–Gayrard–Klein, J. Eur. Math. Soc. 7 (2005), 69–99) sharpens this to the spectrum: each metastable well carries one exponentially small eigenvalue of the generator, equal to the inverse of its mean exit time.

## Proof method

Potential theory replaces the direct analysis of the process. The mean hitting time is expressed exactly as a ratio: the Gibbs measure of the well, weighted by the equilibrium potential, divided by the capacity. The well mass is Laplace asymptotics around the minimum. The capacity is squeezed from two sides of the Dirichlet variational principle: an upper bound by inserting a test function that solves a one-dimensional crossing problem along the unstable direction of the saddle, and a matching lower bound by restricting the Dirichlet form to a thin tube through the gate. Each half is an explicit Gaussian computation; the sharpness of the method is that both bounds carry the same prefactor.

## Why it matters for AI safety

Noisy training in a singular loss landscape moves between flat valleys on exponential timescales, and predicting the dwell time at a loss plateau means proving an Eyring–Kramers law for wells that are not points. This paper supplies the frame the singular version is conjectured in: the identity *mean time = well mass / capacity* separates the two ingredients, the well mass (which Watanabe's volume asymptotics express through the local learning coefficient) and the gate capacity (which for a Morse saddle is order $\varepsilon^{d/2} e^{-h/\varepsilon}$ by the computation here). Running the ratio predicts the prefactor $\varepsilon^{\lambda - d/2}(\log \tfrac1\varepsilon)^{m-1}$ — flatter wells are stickier — and the two halves of a proof for the first singular test cases already exist in the literature: the saddle capacity from this paper, the well mass from Watanabe. Making them meet on an arbitrary analytic singular well is the program of [MAIS-A7](../agendas/A7/).

## Cited by

- [MAIS-A7](../agendas/A7/) — takes the potential-theoretic frame (gate, capacity, mass-over-capacity) and the Morse-saddle capacity as one half of the conjectured singular Eyring–Kramers prefactor.
- Problems [MAIS-O73](../open-problems/MAIS-O73.md) · [MAIS-O74](../open-problems/MAIS-O74.md) · [MAIS-O75](../open-problems/MAIS-O75.md)
