> **Historical scoped-verification record.** This report rechecks content-destructive verdicts about a pre-repair draft of [MAIS-A7](../../../agendas/MAIS-A7/); it is not a second audit of the current edition. Item and line numbers may differ. See the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Scoped verification: effective-loss-dynamics.tex

File: `open problem supplement/effective-loss-dynamics.tex`
Date: 2026-07-15
Verifier: Claude Sonnet 5, scoped verification pass
Scope note: This pass covers only content-destructive verdicts; ill-posed and related-work verdicts were deliberately not pre-verified.

## 1. Question 3.1(b) — POSSIBLY-RESOLVED

**Verdict: CONFIRMED**

Primary source checked: Lehalleur–Rimányi, *Geometry of fibers of the multiplication map of deep linear neural networks*, arXiv:2411.19920v2, Section 8.

- Definition 8.1 defines $\mathrm{rlct}_x(F)$ for an **arbitrary** real-analytic manifold $X$ and **arbitrary** real-analytic $F:X\to\mathbb R$, via local integrability of $|F|^{-s}$ (equivalently, the largest pole of the local zeta function $\zeta_{F,U}(s)=\int_U|F|^s\,d\mathrm{vol}$, Prop-Def 8.2) — the identical construction as the file's Definition 1.1 ($Z(z;w^*,\delta)=\int_{B_\delta(w^*)}|L(w)-L(w^*)|^z\,dw$, pole at $-\lambda(w^*)$).
- Proposition 8.4(ii) states exactly: "The function $x\mapsto\mathrm{rlct}_{X,x}(F)$ is lower semi-continuous," with **no restriction** to the paper's multiplication-map/fiber setting — that specialization (Theorem 8.6) comes later in the same section and is a separate, additional result.
- For $w^*\in W_0$, $L(w^*)=0$, so the file's two-sided $|L(w)-L(w^*)|$ collapses to $L(w)$ and $\lambda(w)=\mathrm{rlct}_{X,w}(L)$ exactly, with $X=\mathbb T^d$, $F=L$. Lower semicontinuity of $\mathrm{rlct}_{X,\cdot}(L)$ on all of $X$ restricts to lower semicontinuity of $\lambda|_{W_0}$ in the subspace topology, which is precisely Question 3.1(b) as stated (lines 180–190 of the file).

This is a direct hit in the file's own setting, not a variant requiring translation. The file's line 190 ("for the real threshold... I do not know a reference for either property") is therefore inaccurate regarding semicontinuity specifically — a reference exists, in a paper the file already cites elsewhere (Problem 3.7, for a different result). Parts (a) (finiteness of the image) and (c) (subanalyticity/frontier condition, and the multiplicity-refined version) are untouched by Prop 8.4(ii) and remain open as the report says; a resolution of only part (b) is a partial resolution of the three-part question, matching the "possibly-resolved" grading.

**Minimal repair:** Cite Lehalleur–Rimányi Prop. 8.4(ii) as resolving part (b) directly; restate Question 3.1 as open only in (a) and (c) (plus the multiplicity-ordering ambiguity the audit separately flags), and cross-reference the existing citation of the same paper in Problem 3.7.

## 2. Problem 3.5(c) — POSSIBLY-RESOLVED

**Verdict: CONFIRMED**

The shared preamble to Problem 3.5 (line 236) fixes "$X_0=(0,\pi/2)$, the midpoint of a vertical stratum" once, before parts (a)–(c) branch off it. Checking directly against $W_0=\{x\in\{0,\pi\}\}\cup\{y\in\{0,\pi\}\}$: $x=0$ places $X_0$ on the vertical stratum, so $X_0\in W_0$.

For part (c)'s dynamics $dX_t=-\nabla L(X_t)\,dt+\sqrt{2\varepsilon L(X_t)}\,dB_t$ with $L=\sin^2x\sin^4y$:
- $L(0,\pi/2)=\sin^2(0)\sin^4(\pi/2)=0$, so the diffusion coefficient $\sqrt{2\varepsilon L(X_0)}=0$.
- $\nabla L(0,y)=(\sin(2\cdot 0)\sin^4y,\ 4\sin^2(0)\sin^3y\cos y)=(0,0)$, so the drift also vanishes at $X_0$.
- The diffusion coefficient $\sqrt{2\varepsilon}\,|\sin x|\sin^2y$ is a product of bounded Lipschitz functions on the compact torus $\mathbb T^2$, hence globally Lipschitz; the drift is smooth on a compact manifold, hence also globally Lipschitz.

By the standard global-Lipschitz existence/uniqueness theorem for SDEs, these coefficients admit a unique strong solution from $X_0$, and the constant path $X_t\equiv X_0$ satisfies the equation trivially (both coefficients vanish identically along it). Pathwise uniqueness then forces $X_t\equiv X_0$ to be the *only* solution — the hitting distribution is $\delta_{X_0}$ for every $\varepsilon>0$, not merely in an asymptotic limit. This matches the report's derivation exactly.

The phrase "as $X_0$ varies" inside part (c)'s prompt is in genuine tension with the fixed $X_0$ inherited from the shared preamble: read literally (fixed $X_0=(0,\pi/2)$), part (c) is settled trivially by the above; read as intending a general/varying initial condition, it silently overrides the stated setup without new quantifiers. Either reading is a real defect, and the report's characterization ("trivializing or settling that part," with (a)–(b) unaffected and open) is accurate.

**Minimal repair:** Restate part (c) with its own explicit initial condition (e.g. "for $X_0\in\mathbb T^2$ ranging over a neighborhood of $W_0$" or an off-$W_0$ basepoint), overriding rather than silently reinterpreting the shared preamble's $X_0=(0,\pi/2)$.

## Summary

1. Question 3.1(b) — **CONFIRMED**. Lehalleur–Rimányi Prop. 8.4(ii) is a fully general lower-semicontinuity theorem for the local RLCT that specializes exactly (not as a variant) to the file's $\lambda$ on $W_0$; parts (a), (c) remain open.
2. Problem 3.5(c) — **CONFIRMED**. The inherited $X_0=(0,\pi/2)\in W_0$ makes both drift and the globally-Lipschitz diffusion vanish identically, so pathwise uniqueness forces the trivial constant solution; parts (a)–(b) are unaffected.

**Recommendation:** Both flagged repairs are small, textual fixes (add one citation; add one initial-condition clause) — apply them; they do not require restructuring the surrounding problems.
