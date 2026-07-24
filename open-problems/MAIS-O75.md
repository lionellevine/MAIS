# Entropic selection between two flat strata on the torus

*Open problem MAIS-O75 · posed in [MAIS-A7](../agendas/A7/MAIS-A7.pdf) as [Problem 3.6](../agendas/A7/MAIS-A7.tex#L294) · Status: open.*

*Safety: generalization — singular learning theory · training dynamics · simplicity bias. Mathematics: probability. Difficulty: ★★ project.*

Metastability concerns wells separated by loss barriers. But a singular optimal set can contain strata of *the same* loss, joined inside the zero set with no barrier between them — and noisy dynamics should still migrate from the less flat stratum to the flatter one, driven purely by transversal volume, on timescales polynomial rather than exponential in the inverse temperature. Here is the smallest test case, one trigonometric polynomial on $\mathbb{T}^2$.

The dynamics is Langevin at temperature $\varepsilon$, $dX_t = -\nabla L(X_t)\,dt + \sqrt{2\varepsilon}\,dB_t$. Flatness is measured by the local learning coefficient $\lambda$: the volume of nearby parameters at loss within $\varepsilon$ of the point scales as $\varepsilon^{\lambda}$, so smaller $\lambda$ means a wider channel of near-optimal parameters.

**Problem ([MAIS-A7, Problem 3.6](../agendas/A7/MAIS-A7.tex#L294); two-stratum entropic selection).** On $\mathbb{T}^2$, let

$$L(x, y) = \sin^2\! x \, \sin^4\! y .$$

Then $W_0 = L^{-1}(0)$ is the union of the two vertical circles $\{ x \in \{0, \pi\} \}$ and the two horizontal circles $\{ y \in \{0, \pi\} \}$; off the crossings, the vertical stratum has $\lambda = \tfrac12$ (quadratic transversal) and the horizontal stratum has $\lambda = \tfrac14$ (quartic transversal), and each crossing has $\lambda = \tfrac14$, $m = 1$. Let $X$ solve the Langevin equation with $X_0 = (0, \pi/2)$, the midpoint of a vertical stratum.

- **(a)** Let $\tau_H = \inf\{ t : \mathrm{dist}(X_t, \{ y \in \{0,\pi\} \}) \le \rho \}$ for fixed small $\rho$. Prove $\mathbb{E}[\tau_H] = \varepsilon^{-b + o(1)}$ and determine $b$. (The agenda expects $b = 1$, with the exponent set by diffusion: the noise carries the process along the flat stratum diffusively, covering order-one distance in time $\varepsilon^{-1}$; the transversal channel width $\propto \varepsilon^{1/2} / \sin^2 y$ induces an entropic drift of order $\varepsilon$ along the stratum, the same order as the diffusion, so it biases the exit law toward the crossings, the gates between strata, without changing the exponent.)
- **(b)** Prove that the relaxation time of the generator (inverse spectral gap) is $\Theta(\varepsilon^{-a})$ up to logarithmic factors, and determine $a$.
- **(c)** Replace the isotropic noise by the degenerate noise $dX = -\nabla L\, dt + \sqrt{2 \varepsilon L(X)}\, dB$, a caricature of minibatch noise vanishing at zero loss, and for this part take $X_0 = (\pi/4, \pi/2) \notin W_0$. For noise of this type ($\sigma \asymp \sqrt{L}$, dying on the zero-loss set), Wojtowytsch ([arXiv:2106.02588](https://arxiv.org/abs/2106.02588)) proves convergence to the minimizing set and a flatness preference provably different from the isotropic Langevin case; what remains open here is quantitative. Show that $X$ converges a.s. to a point of $W_0$ and determine the hitting distribution's asymptotics as $\varepsilon \to 0$. Then obtain the corresponding asymptotic uniformly for $X_0$ in compact subsets of $\mathbb{T}^2 \setminus W_0$: with noise that dies on the optimal set, how is the selection split between $\lambda$ and the basin of first arrival?

The off-zero start in part (c) is forced: at a point of $W_0$ both the drift and the (globally Lipschitz) diffusion coefficient vanish, so pathwise uniqueness leaves the process at its starting point. Parts (a) and (b) reduce to one-dimensional effective potentials with standard tools, and the agenda names this the smallest of its problems: the payoff is the first proved instance of purely entropic selection between strata of a singular optimal set. The general shape it calibrates — two maximal strata meeting along a seam, concentration on the smaller-$\lambda$ one after time $\varepsilon^{-b}$ — is in [MAIS-A7](../agendas/A7/MAIS-A7.pdf), Section 3.3.

*Related: [MAIS-O73](MAIS-O73.md) (the complementary barrier-crossing regime) · [MAIS-O76](MAIS-O76.md) (what genuine SGD noise selects on a singular zero set) · [MAIS-O7](MAIS-O7.md) (the staircase phenomenon this is the simplest instance of).*
