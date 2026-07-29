# Eyring–Kramers law for singular wells

*Open problem MAIS-O73 · posed in [MAIS-A7](../agendas/A7/) as [Problem 3.4](../agendas/A7/MAIS-A7.tex#L248) · Status: open.*

*Tags: generalization · singular learning theory · training dynamics · developmental interpretability · probability · algebraic geometry. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

How long does noisy training take to escape a flat valley? For a Morse landscape the classical Eyring–Kramers formula answers with a constant prefactor times $e^{h/\varepsilon}$, where $h$ is the barrier height. Neural-network losses are not Morse: their zero sets are positive-dimensional and singular, and the problem below asks for the signature of that extra flatness — a polynomial-in-$\varepsilon$ correction governed by the same algebro-geometric invariant that controls Bayesian generalization.

The dynamics is Langevin at temperature $\varepsilon$ on the torus, $dX_t = -\nabla L(X_t)\ dt + \sqrt{2\varepsilon}\ dB_t$, with Gibbs measure proportional to $e^{-L/\varepsilon}$. The invariant is the **local learning coefficient**: near $w^\ast$, the volume of parameters with $|L(w) - L(w^\ast)| < \varepsilon$ scales as $\varepsilon^{\lambda(w^\ast)} (\log \tfrac1\varepsilon)^{m(w^\ast)-1}$, and a component $K$ of the zero set $W_0 = L^{-1}(0)$ carries the data $(\lambda_K, m_K)$: minimal $\lambda$, then maximal $m$, over $K$. By Watanabe's volume asymptotics the Gibbs mass of the well around $K$ has order $\varepsilon^{\lambda_K} (\log \tfrac1\varepsilon)^{m_K - 1}$; the open question is the crossing time.

**Problem ([MAIS-A7, Problem 3.4](../agendas/A7/MAIS-A7.tex#L248); singular Eyring–Kramers).** Let $L\colon \mathbb{T}^d \to [0,\infty)$ be real-analytic with $W_0 = K_A \sqcup K_B$, two disjoint compact connected components (possibly positive-dimensional and singular), with local data $(\lambda_A, m_A)$ and $(\lambda_B, m_B)$ (minimal $\lambda$, then maximal $m$, over each component). Let

$$h = \inf_{\gamma}\  \max_{t \in [0,1]} L(\gamma(t)) > 0,$$

the infimum over continuous paths $\gamma\colon [0,1] \to \mathbb{T}^d$ with $\gamma(0) \in K_A$ and $\gamma(1) \in K_B$, be the communication height, and let $X$ solve the Langevin equation. For $\rho > 0$ small let $\tau_B = \inf\lbrace  t : \mathrm{dist}(X_t, K_B) \le \rho \rbrace $. Let $\mathcal{B}_A$ be the **basin** of $K_A$: the set of $x \in \mathbb{T}^d$ from which the gradient flow $\dot w = -\nabla L(w)$, $w(0) = x$, converges to a point of $K_A$. (The restriction to $\mathcal{B}_A$ matters: a point near a positive-level local minimum can lie in the sublevel component of $K_A$ below $h$ and still have a different exit exponent.) Derive the leading expansion

$$\mathbb{E}_x[\tau_B] = C\ \varepsilon^{\alpha} \bigl( \log \tfrac1\varepsilon \bigr)^{q}\  e^{h/\varepsilon} (1 + o(1)),$$

uniformly for $x$ in compact subsets of the interior of $\mathcal{B}_A \cap \lbrace  L < h \rbrace $. Determine the rational exponent $\alpha$, the integer $q$, and the constant $C > 0$ from a finite resolution of the germ along $K_A$ (its exponents and leading volume coefficients) and the corresponding leading local capacity data at the minimizing gate. The exponential term is already supplied by Freidlin–Wentzell theory; the problem is the stated polynomial–logarithmic prefactor.

Two terms in the statement come from the potential-theoretic approach to metastability of Bovier, Eckhoff, Gayrard, and Klein. The **gate** is the set where the infimum defining $h$ is attained: the points at level $h$ through which near-optimal paths from $K_A$ to $K_B$ pass. The **capacity** between the two wells is their potential-theoretic conductance, which sets the crossing rate; in this approach the mean crossing time emerges as the ratio of the starting well's Gibbs mass to the capacity, so the resolution data along $K_A$ enters through the mass and the gate data through the capacity.

When the gate is a single Morse saddle, the agenda conjectures $\alpha = \lambda_A - d/2$ and $q = m_A - 1$ ([MAIS-O74](MAIS-O74.md)): flatter wells are stickier, by precisely the learning coefficient's deficit from $d/2$. What is known stops short: Berglund–Gentz treat specific degenerate normal forms, Assal–Bony–Michel settle Morse–Bott wells, and Delande treats isolated wells and gates of diagonal monomial type; none covers an arbitrary analytic singular well with exponents given by its resolution data. For a degenerate positive-dimensional gate, even the conjectural prefactor needs spectral data that no volume invariant sees. Full setting and references in [MAIS-A7](../agendas/A7/).

## References

- A. Bovier, M. Eckhoff, V. Gayrard, M. Klein, *Metastability in reversible diffusion processes I: sharp asymptotics for capacities and exit times*, J. Eur. Math. Soc. 6 (2004), 399–424.
- N. Berglund, *Kramers' law: validity, derivations and generalisations*, Markov Processes and Related Fields 19 (2013), 459–490. [arXiv:1106.5799](https://arxiv.org/abs/1106.5799)
- M. Assal, J.-F. Bony, L. Michel, *Metastable diffusions with degenerate drifts*, Ann. Inst. Fourier 75 (2025), 1–33. [arXiv:2202.02208](https://arxiv.org/abs/2202.02208)

*Related: [MAIS-O74](MAIS-O74.md) (the conjectured prefactor when the gate is Morse) · [MAIS-O75](MAIS-O75.md) (selection with no barrier at all) · [MAIS-O72](MAIS-O72.md) (whether the stratum data feeding the prefactor is finite and subanalytic).*
