# Sharp spectral gap for some degenerate Witten Laplacians

*Summary [Del26] · L. Delande, Ann. Henri Poincaré (2026) · [arXiv:2410.21899](https://arxiv.org/abs/2410.21899).*

*Tags: probability · training dynamics · singular learning theory.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Eyring–Kramers formulas beyond the Morse case: for potentials whose critical points are isolated but degenerate, with diagonal monomial normal forms, the low-lying eigenvalues of the semiclassical Witten Laplacian — the inverse relaxation times of the corresponding Langevin dynamics — satisfy sharp asymptotics with an explicit prefactor that is a rational power of the semiclassical parameter, the exponent computed from the degeneracy orders at the well and the gate. The classical constant prefactor is the special case where every order equals two.

## Setting

The operator is the semiclassical Witten Laplacian on $\mathbb R^d$ associated to a smooth confining potential $V$ (confinement in the standard form: $|\nabla V|$ bounded below and $|\Delta V| \lesssim |\nabla V|^2$ outside a compact set). The potential need not be Morse. Instead, near each critical point there is a smooth change of coordinates, with unitary differential at the critical point, in which $V$ becomes a sum of one-variable monomials: $V - V(x^\ast) = \sum_i t_i\, x_i^{\nu_i}$ with each $\nu_i \ge 2$. Every critical point is therefore isolated, but the orders $\nu_i$ are arbitrary; $\nu_i = 2$ throughout recovers the Morse case. The eigenvalues of this operator govern metastability: each exponentially small eigenvalue is the inverse of a mean transition time between wells of the associated Langevin diffusion.

## Main results

1. **Counting.** The spectrum below a threshold of order $h^{2 - 2/\bar\nu}$ (where $\bar\nu$ is the maximal degeneracy order) consists of exactly $n_0$ eigenvalues, one per local minimum of $V$; the rest of the spectrum sits above the threshold, which quantifies the spectral gap.
2. **Sharp Eyring–Kramers formula.** Under a genericity assumption on the separating saddle points, each of the $n_0 - 1$ nonzero small eigenvalues satisfies
   $$\lambda(m,h) = v_m\, h^{\mu(m)}\, e^{-2S(m)/h}\,\bigl(1 + O(h^{\beta})\bigr),$$
   where $S(m)$ is the relevant barrier height, the exponent $\mu(m)$ is rational and computed from the degeneracy orders $\nu_i$ at the minimum and at its gate, and the constant $v_m$ is explicit in the normal-form coefficients $t_i$. When all $\nu_i = 2$ the exponent collapses to the classical value and the formula reduces to the Morse-case Eyring–Kramers law.

Degeneracy thus shows up in the *power* of $h$, not just the constant: flatter critical points shift the prefactor's exponent, in a way read off from the orders $\nu_i$ alone.

## Proof method

Adapted WKB. The main construction is a family of sharp degenerate Gaussian quasimodes, one per minimum: suitably cut off functions of the form $e^{-(V - V(m))/h}$ corrected by the normal-form Jacobian. An IMS localization splits the quadratic form into one-dimensional degenerate Witten Laplacians, one per coordinate of the normal form, each with its own scaling $h^{2-2/\nu_i}$; the one-dimensional spectral gaps and the interaction terms between quasimodes then yield the counting theorem and the prefactor.

## Why it matters for AI safety

Neural-network loss landscapes are degenerate, and the timing of noisy training — how long the dynamics dwells near one low-loss region before crossing to another — is an Eyring–Kramers question outside the Morse case. This paper is the treated case nearest the frontier: it handles arbitrary monomial degeneracy orders, but only for *isolated* critical points. The singular wells of [MAIS-A7](../agendas/A7/) are positive-dimensional — already the monomial potential $\prod_i x_i^{2k_i}$, whose zero set is a union of coordinate hyperplanes, falls outside every treated normal form, Delande's included — and the agenda conjectures that for such wells the prefactor's exponent is governed by Watanabe's local learning coefficient. Delande's result is one boundary of what is known; crossing it is [MAIS-A7](../agendas/A7/), Problems 3.4 and 3.5.

## Cited by

- [MAIS-A7](../agendas/A7/) — cited as the state of the art nearest the singular Eyring–Kramers problem: sharp prefactors for isolated wells and gates of diagonal monomial type.
- Problems [MAIS-O73](../open-problems/MAIS-O73.md) · [MAIS-O74](../open-problems/MAIS-O74.md)
