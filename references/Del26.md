# Sharp spectral gap for some degenerate Witten Laplacians

*Summary [Del26] · L. Delande, Ann. Henri Poincaré (2026) · [arXiv:2410.21899](https://arxiv.org/abs/2410.21899).*

*Tags: probability · training dynamics · singular learning theory.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** Eyring–Kramers spectral formulas beyond the Morse case: for potentials whose critical points are isolated but degenerate, with diagonal monomial normal forms, the low-lying eigenvalues of the semiclassical Witten Laplacian satisfy sharp asymptotics with an explicit prefactor that is a rational power of the semiclassical parameter. The exponent is computed from the degeneracy orders at the well and gate. Relating these eigenvalues to mean transition times in the same degenerate setting requires an additional result not proved here.

## Setting

The operator is the semiclassical Witten Laplacian on $\mathbb R^d$ associated to a smooth confining potential $V$ (confinement in the standard form: $|\nabla V|$ bounded below and $|\Delta V| \lesssim |\nabla V|^2$ outside a compact set). The potential need not be Morse. Instead, near each critical point there is a smooth change of coordinates, with unitary differential at the critical point, in which $V$ becomes a sum of one-variable monomials: $V - V(x^\ast) = \sum_i t_i\, x_i^{\nu_i}$ with each $\nu_i \ge 2$. Every critical point is therefore isolated, but the orders $\nu_i$ are arbitrary; $\nu_i = 2$ throughout recovers the Morse case. The low-lying spectrum determines long relaxation scales for the conjugate Langevin generator. In the Morse case, corresponding eigenvalues are known to agree with inverse mean exit times; the paper notes that this link is not yet proved under its degenerate hypotheses.

## Main results

1. **Counting.** The spectrum below a threshold of order $h^{2 - 2/\bar\nu}$ (where $\bar\nu$ is the maximal degeneracy order) consists of exactly $n_0$ eigenvalues, one per local minimum of $V$; the rest of the spectrum sits above the threshold, which quantifies the spectral gap.
2. **Sharp Eyring–Kramers formula.** Under a genericity assumption on the separating saddle points, each of the $n_0 - 1$ nonzero small eigenvalues satisfies
   $$\lambda(m,h) = v_m\, h^{\mu(m)}\, e^{-2S(m)/h}\,\bigl(1 + O(h^{\beta})\bigr),$$
   where $S(m)$ is the relevant barrier height, the exponent $\mu(m)$ is rational and computed from the degeneracy orders $\nu_i$ at the minimum and at its gate, and the constant $v_m$ is explicit in the normal-form coefficients $t_i$. When all $\nu_i = 2$ the exponent collapses to the classical value and the formula reduces to the Morse-case Eyring–Kramers law.

Degeneracy thus shows up in the *power* of $h$, not just the constant: flatter critical points shift the prefactor's exponent, in a way read off from the orders $\nu_i$ alone.

## Proof method

Adapted WKB. The main construction is a family of sharp degenerate Gaussian quasimodes, one per minimum: suitably cut off functions of the form $e^{-(V - V(m))/h}$ corrected by the normal-form Jacobian. An IMS localization splits the quadratic form into one-dimensional degenerate Witten Laplacians, one per coordinate of the normal form, each with its own scaling $h^{2-2/\nu_i}$; the one-dimensional spectral gaps and the interaction terms between quasimodes then yield the counting theorem and the prefactor.

## Why it matters for AI safety

Neural-network loss landscapes are degenerate, and noisy training can remain near one low-loss region before crossing to another. This paper computes the relevant small eigenvalues for isolated critical points with monomial degeneracy, but it does not prove the corresponding mean exit-time formula, and it does not cover positive-dimensional sets of minima. Even the potential $\prod_i x_i^{2k_i}$, whose zero set is a union of coordinate hyperplanes, lies outside its normal forms. [MAIS-A7](../agendas/A7/) asks whether Watanabe's local learning coefficient controls the prefactor for such non-isolated wells.

## Cited by

- [MAIS-A7](../agendas/A7/) — cited as the state of the art nearest the singular Eyring–Kramers problem: sharp prefactors for isolated wells and gates of diagonal monomial type.
- Problems [MAIS-O73](../open-problems/MAIS-O73.md) · [MAIS-O74](../open-problems/MAIS-O74.md)
