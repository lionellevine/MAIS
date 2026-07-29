# Eyring–Kramers prefactor for a singular well and Morse gate

*Open problem MAIS-O74 · posed in [MAIS-A7](../agendas/A7/) as [Conjecture 3.5](../agendas/A7/MAIS-A7.tex#L264) · Status: open.*

*Tags: generalization · singular learning theory · training dynamics · probability · algebraic geometry. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Take a double-well landscape where one well is not a point but a singular set, and the pass between the wells is an ordinary Morse saddle. The classical Eyring–Kramers formula gives the mean crossing time with a constant prefactor; this conjecture says the singular well contributes a power of the temperature, with exponent read off from Watanabe's learning coefficient.

The setting is that of [MAIS-O73](MAIS-O73.md): a real-analytic $L\colon \mathbb{T}^d \to [0,\infty)$ whose zero set is $W_0 = K_A \sqcup K_B$, two disjoint compact connected components. The local data $(\lambda_A, m_A)$ of the well $K_A$ (and likewise $(\lambda_B, m_B)$ of $K_B$) are defined by sublevel volumes: for a fixed small $\delta > 0$,

$$\mathrm{vol}\ \lbrace w : \mathrm{dist}(w, K_A) < \delta,\ L(w) \le t \rbrace\  \sim\  c_A\  t^{\lambda_A} \bigl( \log \tfrac1t \bigr)^{m_A - 1}, \qquad t \to 0,$$

with $c_A > 0$; exponent, log power, and leading coefficient are furnished by a finite resolution of singularities of $L$ along $K_A$ (in Watanabe's terms: minimal local learning coefficient, then maximal multiplicity, over the component). Consequently the well mass under the Gibbs measure $e^{-L/\varepsilon}$ has order $\varepsilon^{\lambda_A} (\log\tfrac1\varepsilon)^{m_A-1}$. The communication height $h > 0$ is the min-max of $L$ over paths from $K_A$ to $K_B$; the process $X$ is Langevin, $dX_t = -\nabla L(X_t)\ dt + \sqrt{2\varepsilon}\ dB_t$; and $\tau_B$ is the hitting time of a small $\rho$-neighborhood of $K_B$, started from $x$ in the gradient-flow basin $\mathcal{B}_A$ of $K_A$ (the points from which the gradient flow $\dot w = -\nabla L(w)$ converges into $K_A$), the expansion below being asserted uniformly for $x$ in compact subsets of the interior of $\mathcal{B}_A \cap \lbrace L < h \rbrace$. Together these are all the hypotheses of the agenda's Problem 3.4, which [MAIS-O73](MAIS-O73.md) quotes verbatim.

**Conjecture ([MAIS-A7, Conjecture 3.5](../agendas/A7/MAIS-A7.tex#L264)).** In the setting of [MAIS-A7, Problem 3.4](../agendas/A7/MAIS-A7.tex#L248), suppose additionally that the infimum $h$ is attained at a single nondegenerate index-one critical point $z^\ast$ (a Morse saddle). Then

$$\mathbb{E}_x[\tau_B] = C\  \varepsilon^{\lambda_A - d/2} \bigl( \log \tfrac1\varepsilon \bigr)^{m_A - 1} e^{h/\varepsilon}\  (1 + o(1)),$$

where $C > 0$ is explicit in the leading coefficient of the volume asymptotics of $L$ at $K_A$ and the Hessian data of $L$ at $z^\ast$.

The heuristic is a ratio: the well mass is $\varepsilon^{\lambda_A} (\log\tfrac1\varepsilon)^{m_A-1}$, the capacity through a Morse saddle (the potential-theoretic conductance between the wells, which sets the crossing rate) is of order $\varepsilon^{d/2} e^{-h/\varepsilon}$ by Bovier–Eckhoff–Gayrard–Klein, and the mean time is mass over capacity. When $K_A$ is a nondegenerate minimum $w_A$, $\lambda_A = d/2$ and $m_A = 1$, so no power of $\varepsilon$ survives and the formula reduces to classical Eyring–Kramers with $C = \tfrac{2\pi}{\mu_-} \sqrt{|\det \nabla^2 L(z^\ast)| / \det \nabla^2 L(w_A)}$, where $\mu_-$ is the absolute value of the unique negative eigenvalue of $\nabla^2 L(z^\ast)$. In general, the volume asymptotics named in the conjecture is the sublevel-volume law displayed above: the claim is that $C$ is determined by its leading coefficient $c_A$ together with the Hessian of $L$ at $z^\ast$, and identifying the closed form of $C$ is part of the problem. In words: flatter wells are stickier, by the learning coefficient's deficit from $d/2$. A first target is the monomial well $\prod_i x_i^{2k_i}$, which falls outside every treated normal form yet already displays the full prefactor; the two halves of a proof (saddle capacity, well mass) exist in the literature, and the work is to run them together. See [MAIS-A7](../agendas/A7/), Sections 3.2 and 4.

## References

- A. Bovier, M. Eckhoff, V. Gayrard, and M. Klein, *Metastability in reversible diffusion processes I: sharp asymptotics for capacities and exit times*, J. Eur. Math. Soc. 6 (2004), 399–424.
- S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- L. Delande, *Sharp spectral gap for some degenerate Witten Laplacians*, Ann. Henri Poincaré (2026). [arXiv:2410.21899](https://arxiv.org/abs/2410.21899)

*Related: [MAIS-O73](MAIS-O73.md) (the general singular Eyring–Kramers problem this instantiates) · [MAIS-O75](MAIS-O75.md) (the barrier-free, purely entropic regime) · [MAIS-O7](MAIS-O7.md) (the staircase whose plateau times such laws would predict).*
