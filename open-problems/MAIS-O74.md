# Eyring–Kramers prefactor for a singular well and Morse gate

*Open problem MAIS-O74 · posed in [MAIS-A7](../agendas/A7/) as [Conjecture 3.5](../agendas/A7/MAIS-A7.tex#L264) · Status: open.*

*Tags: generalization · singular learning theory · training dynamics · probability · algebraic geometry. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Take a double-well landscape where one well is not a point but a singular set, and the pass between the wells is an ordinary Morse saddle. The classical Eyring–Kramers formula gives the mean crossing time with a constant prefactor; this conjecture says the singular well contributes a power of the temperature, with exponent read off from Watanabe's learning coefficient [W09]. The safety interest is timing: laws of this kind would predict how long noisy training dwells at one loss plateau before jumping to the next.

The setting is that of [MAIS-O73](MAIS-O73.md): a real-analytic $L\colon \mathbb{T}^d \to [0,\infty)$ whose zero set is $W_0 = K_A \sqcup K_B$, two disjoint compact connected components with local data $(\lambda_A, m_A)$ and $(\lambda_B, m_B)$ (minimal local learning coefficient, then maximal multiplicity, over each component — so the well mass under the Gibbs measure $e^{-L/\varepsilon}$ has order $\varepsilon^{\lambda_A} (\log\tfrac1\varepsilon)^{m_A-1}$); the communication height $h > 0$ is the min-max of $L$ over paths from $K_A$ to $K_B$; the process $X$ is Langevin, $dX_t = -\nabla L(X_t)\ dt + \sqrt{2\varepsilon}\ dB_t$; and $\tau_B$ is the hitting time of a small $\rho$-neighborhood of $K_B$, started from $x$ in the gradient-flow basin of $K_A$. The precise hypotheses (the sublevel-volume law defining the local data, the basin restriction, the uniformity in $x$) are those of the agenda's Problem 3.4, which [MAIS-O73](MAIS-O73.md) quotes verbatim.

**Conjecture ([MAIS-A7, Conjecture 3.5](../agendas/A7/MAIS-A7.tex#L264)).** In the setting of [MAIS-A7, Problem 3.4](../agendas/A7/MAIS-A7.tex#L248), suppose additionally that the infimum $h$ is attained at a single nondegenerate index-one critical point $z^\ast$ (a Morse saddle). Then

$$\mathbb{E}_x[\tau_B] = C\  \varepsilon^{\lambda_A - d/2} \bigl( \log \tfrac1\varepsilon \bigr)^{m_A - 1} e^{h/\varepsilon}\  (1 + o(1)),$$

where $C > 0$ is explicit in the leading coefficient of the volume asymptotics of $L$ at $K_A$ and the Hessian data of $L$ at $z^\ast$.

The heuristic is a ratio: the well mass is $\varepsilon^{\lambda_A} (\log\tfrac1\varepsilon)^{m_A-1}$, the capacity through a Morse saddle (the potential-theoretic conductance between the wells, which sets the crossing rate) is of order $\varepsilon^{d/2} e^{-h/\varepsilon}$ by Bovier–Eckhoff–Gayrard–Klein [BEGK04], and the mean time is mass over capacity. When $K_A$ is a nondegenerate minimum, $\lambda_A = d/2$ and $m_A = 1$, so no power of $\varepsilon$ survives and the formula reduces to classical Eyring–Kramers. In words: flatter wells are stickier, by the learning coefficient's deficit from $d/2$. Identifying the closed form of $C$ (from the well's leading volume coefficient and the Hessian at $z^\ast$) is part of the problem. A first target is the monomial well $\prod_i x_i^{2k_i}$, which falls outside every treated normal form (the closest, Delande's semiclassical analysis [[Del26]](../references/Del26.md), covers isolated wells and gates of diagonal monomial type) yet already displays the full prefactor; the two halves of a proof (the saddle capacity from [BEGK04], the well mass from Watanabe's volume asymptotics [W09]) exist in the literature, and the work is to run them together. See [MAIS-A7](../agendas/A7/), Sections 3.2 and 4.

## References

- [[BEGK04]](../references/BEGK04.md) A. Bovier, M. Eckhoff, V. Gayrard, and M. Klein, *Metastability in reversible diffusion processes I: sharp asymptotics for capacities and exit times*, J. Eur. Math. Soc. 6 (2004), 399–424.
- [[W09]](../references/W09.md) S. Watanabe, *Algebraic Geometry and Statistical Learning Theory*, Cambridge University Press, 2009.
- [[Del26]](../references/Del26.md) L. Delande, *Sharp spectral gap for some degenerate Witten Laplacians*, Ann. Henri Poincaré (2026). [arXiv:2410.21899](https://arxiv.org/abs/2410.21899)

*Related: [MAIS-O73](MAIS-O73.md) (the general singular Eyring–Kramers problem this instantiates) · [MAIS-O75](MAIS-O75.md) (the barrier-free, purely entropic regime) · [MAIS-O7](MAIS-O7.md) (the staircase whose plateau times such laws would predict).*
