> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A7](../../../agendas/MAIS-A7/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Independent audit of `effective-loss-dynamics.tex`

## Summary verdict

The file has a sound mathematical core and several useful, genuinely open research directions, but it is not publication-ready under its claim that every formulation is precise and open as of July 2026. The most serious openness miss is Question 3.1(b): lower semicontinuity of the local RLCT is stated verbatim as Proposition 8.4(ii) of Lehalleur--Rimányi, a paper already cited elsewhere in this file. Several other numbered items are not well-posed as written: Problem 3.5(c) is trivial from the inherited initial condition because its noise and drift both vanish on the zero set; Problems 3.9 and 6.1 invoke an $n\to\infty$ asymptotic “between” fixed finite crossovers; Problem 3.6 asks for the law of a global diffusion that its cited theorem does not define on the noncompact, rank-stratified set; and Problem 3.12 leaves its limiting trajectory and comparison data undefined. The small proved results and the principal formulas are mostly correct, including Proposition 3.2 and the Saxe and Aoyagi--Watanabe formulas, but the stated Watanabe theorem omits standard analytic/statistical hypotheses, a basic background sentence falsely says singularity forces a positive-dimensional optimum set, and later deductions mishandle the parity correction in the Aoyagi--Watanabe formula. Overall verdict: **significant issues**, with high confidence.

The locations below refer to the line numbers in the supplied source. Literature was searched through arXiv, journal and conference pages, OpenReview, and targeted web searches of ML/AI-safety venues on 14 July 2026. I treated a negative search result as evidence only of “no resolution found,” not proof of openness.

## Findings ordered by severity

### 1. Question 3.1(b) is already a theorem in a source cited by the file

**Location:** Question 3.1(b), lines 180--190; bibliography lines 549--552.

The question asks whether $w\mapsto\lambda(w)$ is lower semicontinuous on the zero set of a real-analytic function, and line 190 says no reference was found. [Lehalleur and Rimányi, *Geometry of fibers of the multiplication map of deep linear neural networks*](https://arxiv.org/abs/2411.19920), Proposition 8.4(ii), states for a real-analytic manifold $X$ and real-analytic $F:X\to\mathbb R$: “The function $x\mapsto \operatorname{rlct}_{X,x}(F)$ is lower semi-continuous.” On $W_0$, the file's $\lambda(w)$ is exactly that local RLCT. This directly resolves part (b), not merely a special matrix-factorization case. The same paper is already cited in Problem 3.7, so this is both an openness and attribution/related-work miss.

The cited proposition does **not** by itself settle the finite-image and subanalytic/frontier assertions in (a) and (c), nor the unspecified multiplicity refinement. I therefore classify the multi-part Question 3.1 as `possibly-resolved`, rather than `resolved`.

### 2. Problem 3.5(c) is trivial under its stated initial condition

**Location:** Problem 3.5, especially lines 236 and 240.

The problem fixes $X_0=(0,\pi/2)\in W_0$ before parts (a)--(c), then part (c) replaces the dynamics by

\[
dX_t=-\nabla L(X_t)\,dt+\sqrt{2\varepsilon L(X_t)}\,dB_t.
\]

Here

\[
\sqrt{L(x,y)}=|\sin x|\sin^2y.
\]

This coefficient is globally Lipschitz on the torus, and the drift is smooth. At every point of $W_0$, both coefficients vanish. Consequently the constant path $X_t\equiv X_0$ is a strong solution and pathwise uniqueness makes it the only solution. Thus the requested convergence holds trivially and the “hitting distribution” is exactly $\delta_{X_0}$, for every $\varepsilon$, not merely asymptotically. The same observation holds for every initial point in $W_0$.

If “as $X_0$ varies” is intended to introduce off-zero initial conditions, that contradicts the inherited fixed $X_0$ and requires a new quantifier and a scaling regime for the distance to $W_0$. [Wojtowytsch's result](https://arxiv.org/abs/2106.02588) concerns nontrivial approach from outside the minimizing set and does not alter the absorbing-state argument here. Parts (a)--(b) remain meaningful and no direct resolution was found, but the numbered problem as a whole is `ill-posed` and `possibly-resolved` in part.

### 3. Problem 3.9 has no coherent crossover asymptotic

**Location:** crossover definition at line 287; Problem 3.9, lines 289--304.

There are two independent defects.

First, the equation

\[
\frac{n_k}{\log n_k}=\frac{2\Delta\lambda_k}{s_k^2}
\]

does not define $n_k$ without a branch and an existence condition. On $n>1$, $n/\log n$ has minimum $e$ at $n=e$. If the right-hand side is below $e$, there is no real solution; if it exceeds $e$, there are two. The intended large branch should be specified, for example using the $W_{-1}$ branch of Lambert $W$, and the regime in which Watanabe's large-$n$ expansion is valid must exclude the small root. Integer sample sizes add a further harmless rounding choice, but do not fix the missing branch.

Second, for a fixed target spectrum all $n_k$ are fixed finite constants. Therefore a sequence $n\to\infty$ satisfying the exclusion in part (a) is eventually beyond every crossover, $k^*(n)=r$, and

\[
\min_k|n-n_k|\ge c\sqrt{n\log n}
\]

eventually holds automatically. The claimed theorem then tests only ordinary eventual posterior concentration at the final rank, not the staircase near the crossovers. A meaningful asymptotic must introduce a joint family, for example $s_k=s_k(N)\to0$ so that the large crossover roots tend to infinity, and state uniformity in that family.

Part (b) also leaves “uniformly” unquantified over $H$, $r$, and spectra. Since

\[
\frac{t_k}{\log(1/u_0)}\longrightarrow \frac{\tau}{2s_k},
\]

its universal-$\phi$ question is a fixed functional-equation comparison across spectra, not an asymptotic matching of the finite schedules unless a spectrum family is supplied. Related empirical work, notably [Chen et al.](https://arxiv.org/abs/2310.06301), does not repair or prove this statement. Verdict: `ill-posed`.

### 4. Problem 6.1 repeats the same missing-limit defect, and its motivating “no window” conclusion is too strong

**Location:** saddle calculation lines 376--380; Problem 6.1, lines 382--388.

For fixed deep-linear data, the “consecutive crossovers” are fixed numbers. The assertion

\[
F_n(U_k^n)=n\inf_{U_k^n}L_n+\Lambda(C_k\cap W)\log n+o_p(\log n)
\]

“for all $n$ between consecutive crossovers” has no $n\to\infty$ sequence on which the $o_p(\log n)$ can be interpreted. As in Problem 3.9, a joint scaling that drives the crossover intervals to infinity is required, together with a uniform probabilistic statement. Without it, neither the existence nor the nonexistence branch is a mathematical proposition.

The fixed-window saddle integral itself is correct up to multiplicative constants, but the sentence “No window size makes the naive ladder literally true at a strict saddle” has a boundary-scale counterexample in the very two-dimensional Morse model used. Taking $\delta=c\beta^{-1/2}$ and rescaling $(x,y)=\beta^{-1/2}(X,Y)$ gives

\[
\int_{B_\delta}e^{-\beta L}
=e^{-\beta L(z)}\beta^{-1}\!
\int_{B_c}e^{-\mu(X^2-Y^2)/2}\,dX\,dY,
\]

so its window free energy is $\beta L(z)+\log\beta+O(1)$. In dimension two the file itself assigns the saddle $\lambda=1$, so this window does reproduce the naive $\beta L+\lambda\log\beta$ term (though not the multiplicity's $-\log\log\beta$ term). The correct conclusion is that the coefficient is schedule-dependent and generally nonintrinsic, not that no schedule can ever coincide with $\lambda$. Verdict: `ill-posed`; the calculation is `correct-with-gaps` because its universal deduction fails at the boundary scale.

### 5. Problem 3.6 asks for a law of a diffusion that has not been defined

**Location:** theorem summary line 248; geometric setup lines 250--259; Problem 3.6(a)--(c), lines 260--265.

The cited [Li--Wang--Arora theorem](https://arxiv.org/abs/2110.06914) assumes a compact smooth minimizer manifold with constant Hessian rank. The set $\Gamma$ here is open in a noncompact fiber, splits into fixed-rank-pair smooth pieces, and has the singular set $\Sigma$ as a boundary. “The hypotheses hold locally” supplies local, stopped coefficients on each piece; it does not select a global process, prevent escape to infinity, or determine a boundary law. Part (a) nevertheless refers to “the Li--Wang--Arora limiting diffusion ... started on $\Gamma$” and asks for *the* hitting law and time tail without specifying an initial point or distribution. Different starting rank-pair components and different behavior at infinity give inequivalent laws.

Part (b) correctly recognizes that transmission through $\Sigma$ needs a martingale problem or Dirichlet form, but saying only that each restriction is the Katzenberger diffusion does not determine its gluing: killing, absorption, sticky holding, and multiple transmission rules can share the same restrictions. Formulating and selecting the rule from an SGD limit is a legitimate research goal; it cannot simultaneously be treated as an already-defined object in part (a). [Shalova--Schlichting--Peletier (2024)](https://arxiv.org/abs/2404.12293) broadens noise schemes and timescales but retains a smooth minimizer-manifold framework, so it is relevant rather than resolving. Verdict: `ill-posed`, with substantial related work.

### 6. Problem 3.12 does not define its admissible instances or the data being compared

**Location:** Problem 3.12, lines 339--341.

The conditional phrase “assuming the small-initialization limit trajectory exists and visits a finite chain of critical sets” does not define the limit: no time rescaling, topology, mode of convergence over the random initialization, or rule for declaring that a trajectory “visits” a critical set is given. The invariant at a *set* could mean a pointwise function, the infimum used in Conjecture 3.8, a generic value, or an invariant of an ideal; these readings are inequivalent. Likewise, a negative Hessian spectrum generally varies along a critical set, and “identical” spectra across networks of different parameter dimensions requires conventions for zero modes and multiplicities.

The admissible-width threshold $N_0(f)$ is undefined. More seriously, fixing an arbitrary real-analytic activation includes constant or low-degree polynomial activations that cannot represent many Boolean targets at any width, making the admissible class empty for them. This can make the proposed functionhood condition vacuous. [Abbe--Boix-Adserà--Misiakiewicz](https://arxiv.org/abs/2302.11055) supplies leap-complexity dynamics under a particular model and assumptions, not the undefined singularity-data map. Verdict: `ill-posed` and open only after a substantial restatement.

### 7. “Singular” does not imply a positive-dimensional optimal set

**Location:** background, line 65.

The sentence says that if parameters are nonidentifiable or Fisher information degenerates, “then $W_0$ is a positive-dimensional analytic variety rather than a point.” A one-parameter normal model gives a counterexample:

\[
p(x\mid w)=N(w^2,1),\qquad q=N(0,1).
\]

Its KL loss is $K(w)=w^4/2$, its Fisher information is $4w^2$ and hence degenerates at the truth, and $p(\cdot\mid w)=p(\cdot\mid -w)$. Nevertheless $W_0=\{0\}$ is isolated. Singular zero sets may be positive-dimensional, nonreduced, isolated, or mixtures of these; singularity alone does not force dimension.

### 8. Theorem 2.3 omits hypotheses needed by the cited Watanabe theorem

**Location:** Theorem 2.3, lines 111--118.

The displayed expansion is standard, but “the model is real-analytic in $w$, $W$ compact, truth realizable, RFV” is not a self-contained statement of Watanabe's fundamental conditions. The cited theory also imposes structure on the compact parameter domain, the prior, common support/integrability, and analyticity of the likelihood-ratio map in an appropriate function space. See the “Fundamental Conditions” in [Watanabe's WBIC paper](https://jmlr.csail.mit.edu/papers/volume14/watanabe13a/watanabe13a.pdf), which, for example, makes $W$ basic semianalytic and factors the prior into analytic and positive smooth parts. A pointwise assertion that $p(x\mid w)$ is analytic in $w$ is not enough to justify exchanging the statistical and resolution arguments.

The global multiplicity should also be stated as the **maximum pole order among points/strata attaining the minimum $\lambda$**; “the minimal local learning coefficient ... and its multiplicity” is ambiguous when several minimizers of $\lambda$ have different multiplicities. The local statement needs the same standard hypotheses after localization and a neighborhood whose boundary excludes competing zeros. Verdict: `correct-with-gaps`, not `flawed`, because the formula is correct once the conventional conditions are restored.

### 9. Consequences drawn from the Aoyagi--Watanabe formula mishandle parity

**Location:** lines 172, 285, 287, and Problem 3.9(b), line 293.

Theorem 2.6's formula itself agrees with the reduced-rank-regression formula in [Aoyagi--Watanabe](https://www.sciencedirect.com/science/article/abs/pii/S0893608005000559). In constant width, however,

\[
\lambda_k=\frac{(H+k)(3H-k)+p_k}{8},\qquad
p_k=\mathbf 1_{3H+k\text{ odd}},
\]

so

\[
\Delta\lambda_k
=\frac{2(H-k)+1+p_k-p_{k-1}}{8}.
\]

The file sometimes says “up to parity,” but then uses parity-free consequences. In particular, the claim in line 293 that $\Delta\lambda_k$ is bounded above by $(2H-1)/8$ is false: for even $H$, $\Delta\lambda_1=2H/8$. If $k=H$ is allowed, $\Delta\lambda_H=0$, so $\lambda_{H-1}=\lambda_H$; hence line 172's statement that every lower rank has a *smaller* coefficient is false at the last step. Its further claim that the Bayesian ladder passes through all ranks is overgeneral even when $r<H$: line 287 itself later gives a near-flat-spectrum example in which a rung is skipped, so line 172 needs the well-separated-spectrum hypothesis later imposed. Problem 3.7 assumes $H>r$, which avoids $k=H$ if that assumption is intended to carry into Problem 3.9, but the incorrect upper bound remains. These are errors in deductions, not in Theorem 2.6.

### 10. The full critical-point classification is incompletely attributed

**Location:** line 144.

The special whitened, distinct-singular-value classification is plausible and the displayed stationarity conditions are correct, but Baldi--Hornik alone is not a safe citation for the broad “all critical points” formulation at arbitrary rectangular dimensions. [Zhou--Liang, *Critical Points of Neural Networks*](https://arxiv.org/abs/1710.11205) explicitly presents a necessary-and-sufficient characterization under arbitrary parameter dimensions and data matrices and describes it as generalizing Baldi--Hornik's more restrictive setting. The file should at least share attribution with this modern general result or state exactly which Baldi--Hornik hypotheses cover the special setup.

### 11. Question 3.11 and Problem 3.3 need smaller precision repairs

**Question 3.11, lines 321--327 (`minor-issues`).** The first integral questions are definite, but “lying below” is not defined for two intervals (disjoint ordering by endpoints, pointwise ordering, or merely smaller typical temperature are different). In the shadowing clause, $\delta$ has no explicit quantifier: it can be read as an arbitrary fixed value inherited from the preceding sentence, a value chosen jointly with the schedule, or $\delta=\delta(u_0)$, which materially changes the question. “Decreasing schedule” also needs enough regularity to define the nonautonomous gradient flow. [Chen--Murfet (2025)](https://arxiv.org/abs/2504.18048) is related on temperature/resolution and the 2025 plateau literature is phenomenologically related, but no theorem matching this coarse-grained ball loss was found.

**Problem 3.3, lines 209--215 (`minor-issues`).** “The subexponential prefactor is expressed in terms of finitely many local invariants” is not a falsifiable deliverable until “local invariant” and the requested asymptotic order are specified. A finite jet, a local capacity, an RLCT/multiplicity pair, or an entire normal-form germ are very different targets. The problem is nevertheless mathematically meaningful as a broad program. [Avelin--Julin--Viitasaari](https://arxiv.org/abs/2206.13206) gives very general geometric capacity estimates and transition-time bounds for degenerate wells/saddles; [Assal--Bony--Michel](https://aif.centre-mersenne.org/articles/10.5802/aif.3636/) treats Morse--Bott wells; and [Delande](https://link.springer.com/article/10.1007/s00023-026-01673-4) treats isolated diagonal-monomial normal forms. None covers an arbitrary positive-dimensional singular analytic well with an RLCT-only prefactor.

### 12. Lower-severity bibliographic and formulation points

- **Question 3.1 multiplicity sentence, line 187:** “The same questions” does not define an order on $(\lambda,m)$. At equal $\lambda$, deeper singular behavior corresponds to larger $m$, so simply copying the scalar lower-semicontinuity/frontier inequalities is not meaningful without a lexicographic convention. This is why Question 3.1 is `minor-issues` even apart from its resolved part (b).

- **Delande bibliography, lines 487--491:** the draft is dated 13 July 2026, but Delande's paper was published online in *Annales Henri Poincaré* on 5 March 2026, DOI [10.1007/s00023-026-01673-4](https://link.springer.com/article/10.1007/s00023-026-01673-4). “To appear” is stale.

- **Conjecture 3.8, lines 281--283:** the statement itself is well-posed because it uses an infimum on noncompact $C_k$. The parenthetical comparison to Question 3.1(a) should not suggest that the compact-torus question automatically supplies a uniform finite-image theorem on noncompact saddle sets. This does not alter the verdict.

## Result-by-result correctness check

| Result or calculation | Verdict | Audit note |
|---|---|---|
| Theorem 2.3 (Watanabe), lines 111--118 | `correct-with-gaps` | The expansion and localization principle are standard, but the theorem omits Watanabe's fundamental conditions and does not specify how global multiplicity is selected among minimum-$\lambda$ points. |
| Theorem 2.5 (Saxe--McClelland--Ganguli), lines 146--152 | `correct` | From the balanced aligned ansatz, $\tau\dot a=b(s-ab)$ and $\tau\dot b=a(s-ab)$; balance is preserved and $u=ab$ satisfies $\tau\dot u=2u(s-u)$. The displayed logistic solution and switch time follow. See [Saxe et al.](https://arxiv.org/abs/1312.6120). |
| Theorem 2.6 (Aoyagi--Watanabe), lines 158--170 | `correct` | The four cases, parity correction, and multiplicities match the published reduced-rank-regression formula. Later parity-free deductions are erroneous, as noted above. |
| Proposition 3.2 (Gibbs equilibrium selection), lines 196--205 | `correct` | A finite resolution cover of the compact separated part of $W_0$, followed by Laplace transformation of the sublevel-volume expansion, yields the smallest local exponent and the maximal multiplicity among ties. The cusp check is also correct: splitting at $y=\varepsilon^{1/6}$ gives two contributions of order $\varepsilon^{1/3}$. |
| Morse-saddle window calculation, lines 376--380 | `correct-with-gaps` | The fixed-$\delta$ factorization and the rim term for $0<\rho<1/2$ are correct. The deduction that no window can reproduce the naive $\lambda\log\beta$ term fails at $\rho=1/2$ in the displayed two-dimensional example. |

Other checked background computations: the local-zeta examples in lines 99--100 are correct; the Hessian-trace identity and weighted-balance minimizers in lines 257--259 are correct; the constant-width derivative without parity is algebraically correct but cannot support the parity-free bounds subsequently claimed. The broad singular-model implication in line 65 is false, as shown above.

## Per-item precision and openness verdicts

| Numbered item | Precision | Openness | Reason |
|---|---|---|---|
| Question 3.1 | `minor-issues` | `possibly-resolved` | Part (b) is exactly Proposition 8.4(ii) of Lehalleur--Rimányi; (a), (c), and the undefined multiplicity ordering remain. |
| Problem 3.3 | `minor-issues` | `open-with-related-work` | The requested class of “local invariants” is vague. Degenerate and Morse--Bott Eyring--Kramers results substantially overlap but do not cover arbitrary singular wells. |
| Conjecture 3.4 | `well-posed` | `open-with-related-work` | The mass/capacity exponent is consistent with the classical Morse check. Existing work covers Morse--Bott or specified isolated normal forms, not arbitrary analytic singular $K_A$. |
| Problem 3.5 | `ill-posed` | `possibly-resolved` | Parts (a)--(b) are meaningful and appear open; part (c) has the unique constant solution for its fixed $X_0\in W_0$. |
| Problem 3.6 | `ill-posed` | `open-with-related-work` | The global diffusion and initial law in (a), and the gluing law in (b), are not defined. Smooth-manifold limit theorems do not cross the singular locus. |
| Problem 3.7 | `well-posed` | `open-with-related-work` | Lehalleur--Rimányi and Furman--Lau give real partial progress, but no source found the full pointwise two-rank table and saddle invariants. |
| Conjecture 3.8 | `well-posed` | `open-with-related-work` | Empirical opposing-staircase work and deep-linear dynamics are related; no proof or counterexample for the two-sided local coefficients was found. |
| Problem 3.9 | `ill-posed` | `open-with-related-work` | The crossover equation has missing existence/branch conditions, and fixed crossovers do not support the asserted $n\to\infty$ staircase limit. |
| Question 3.11 | `minor-issues` | `open-with-related-work` | Interval ordering and the $\delta$/schedule quantifiers are ambiguous. Related coarse-graining and plateau work does not settle the stated integral/shadowing question. |
| Problem 3.12 | `ill-posed` | `open-with-related-work` | The limiting chain, set-level invariants, spectrum comparison, $N_0(f)$, and nonempty admissible class are not defined. |
| Problem 6.1 | `ill-posed` | `open-with-related-work` | There is no asymptotic sequence “between” fixed crossovers; existing SLT/phase-transition work does not supply the missing joint limit. |

## Per-item search-query log

The strings below are the literal searches used. Direct checks of papers already named in the file were also made from their arXiv, journal, PMLR, or OpenReview pages.

### Question 3.1

- `real log canonical threshold local function lower semicontinuity constructible resolution real analytic`
- `"real log canonical threshold" semicontinuity local`
- `local integrability index real analytic function stratification finite values`
- `2024 2025 2026 real log canonical threshold local learning coefficient stratification`
- `analytic family local zeta function poles constructible stratification resolution singularities local integrability exponent`
- `real analytic local zeta function poles finite stratification pointwise`
- `Atiyah resolution singularities integrals analytic local zeta functions theorem`
- `Bernstein Sato local poles stratification analytic function real`
- `site:arxiv.org local learning coefficient stratification singular set`
- `site:openreview.net learning coefficient stratification local RLCT`
- `site:alignmentforum.org "learning coefficient" strata`
- `site:lesswrong.com "local learning coefficient" stratification`
- `"Proposition 8.4" "lower semi-continuous" rlct Lehalleur Rimanyi`

Outcome: [Lehalleur--Rimányi](https://arxiv.org/abs/2411.19920), Proposition 8.4(ii), directly settles (b). No comparably direct source was found for the complete finite-image, subanalytic-level-set, frontier, and multiplicity package.

### Problem 3.3

- `2024 2025 2026 Eyring Kramers singular manifold minima real log canonical threshold analytic degenerate well`
- `metastability analytic singular set of minima Eyring Kramers prefactor Morse saddle`
- `Witten Laplacian degenerate wells nonisolated singular minima 2025`
- `capacity sublevel volume degenerate minima Eyring Kramers law local zeta`
- `Assal Bony Michel Metastable diffusions with degenerate drifts Morse Bott 2025`
- `Delande sharp spectral gap degenerate Witten Laplacians isolated wells gates diagonal monomial normal forms`
- `Avelin Julin Viitasaari degenerate Eyring Kramers minima saddles 2023`

Outcome: [Avelin--Julin--Viitasaari](https://arxiv.org/abs/2206.13206), [Assal--Bony--Michel](https://aif.centre-mersenne.org/articles/10.5802/aif.3636/), and [Delande](https://link.springer.com/article/10.1007/s00023-026-01673-4) are substantial neighboring results. Their assumptions do not include arbitrary positive-dimensional singular analytic wells with a prefactor expressed solely through RLCT data.

### Conjecture 3.4

The conjecture was searched jointly with Problem 3.3 because it is the proposed sharp special case; the literal queries were:

- `2024 2025 2026 Eyring Kramers singular manifold minima real log canonical threshold analytic degenerate well`
- `metastability analytic singular set of minima Eyring Kramers prefactor Morse saddle`
- `Witten Laplacian degenerate wells nonisolated singular minima 2025`
- `capacity sublevel volume degenerate minima Eyring Kramers law local zeta`
- `Assal Bony Michel Metastable diffusions with degenerate drifts Morse Bott 2025`
- `Delande sharp spectral gap degenerate Witten Laplacians isolated wells gates diagonal monomial normal forms`
- `Avelin Julin Viitasaari degenerate Eyring Kramers minima saddles 2023`

Outcome: the same three neighboring results cover Morse--Bott and specified degenerate normal forms, but none states the RLCT/multiplicity formula for an arbitrary analytic singular well with a single Morse gate.

### Problem 3.5

- `Langevin sin^2 x sin^4 y spectral gap small temperature connected zero set entropic barriers`
- `spectral gap Gibbs measure potential product x^2 y^4 degenerate connected minima`
- `diffusion along intersecting manifolds of minima small noise spectral gap stratified space`
- `2024 2025 entropic barriers Langevin connected manifold minima singular intersection`

Outcome: no direct treatment of this trigonometric example or its spectral-gap exponent was found. [Wojtowytsch](https://arxiv.org/abs/2106.02588) is relevant to multiplicative noise and flatness selection, but part (c)'s fixed zero-loss initial condition makes its stated process absorbing before those results become relevant.

### Problem 3.6

- `2024 2025 2026 SGD diffusion singular manifold minima stratified Katzenberger`
- `stochastic gradient descent near singular set of minimizers limiting diffusion rank deficient matrix factorization`
- `diffusion on stratified spaces singular optimal set SGD label noise`
- `site:openreview.net SGD singular manifold minima diffusion rank stratification`
- `Shalova Schlichting Peletier singular limit gradient descent noise injection smooth manifold 2024`

Outcome: [Li--Wang--Arora](https://arxiv.org/abs/2110.06914) and [Shalova--Schlichting--Peletier](https://arxiv.org/abs/2404.12293) give smooth-manifold limiting dynamics. No SGD-derived transmission law across a rank-stratified singular minimizer set was found.

### Problem 3.7

- `2024 2025 local real log canonical threshold matrix multiplication fiber BA Phi ranks A B`
- `"Geometry of fibers of the multiplication map" RLCT local rank pair`
- `reduced rank regression local learning coefficient every point factor ranks`
- `Aoyagi Watanabe local learning coefficient matrix factorization saddle rank`
- `2024 2025 2026 local learning coefficient matrix multiplication fiber local ranks A B Furman Lau`

Outcome: [Lehalleur--Rimányi](https://arxiv.org/abs/2411.19920) computes fiber geometry and important global/zero-target RLCT information; [Furman--Lau](https://arxiv.org/abs/2402.03698) supplies local values used to validate estimation. Neither source gives the entire pointwise $(\operatorname{rank}A,\operatorname{rank}B)$ table plus all two-sided saddle invariants requested here.

### Conjecture 3.8

- `2024 2025 2026 "opposing staircases" learning coefficient deep linear network`
- `deep linear network local learning coefficient saddle chain rank 2025`
- `RLCT critical points saddles matrix factorization local zeta two-sided`
- `site:alignmentforum.org opposing staircases singular learning theory`

Outcome: [Chen et al.](https://arxiv.org/abs/2310.06301) and [Hoogland et al.](https://arxiv.org/abs/2402.02364) give empirical/diagnostic overlap. No computation proving or refuting strict monotonicity of the two-sided saddle coefficients was found.

### Problem 3.9

- `deep linear network Bayesian phase transitions sample size learning coefficient rank ladder time sample dictionary`
- `internal model selection reduced rank regression posterior local saddle free energy`
- `2024 2025 2026 singular learning theory time sample correspondence gradient flow`
- `site:openreview.net learning coefficient training time sample size deep linear`

Outcome: [Chen et al.](https://arxiv.org/abs/2310.06301) compares Bayesian and dynamical transitions in a toy superposition model; [Hennick--De Baerdemacker](https://arxiv.org/abs/2503.22478) gives a diffusion/tempered-posterior bridge. Neither supplies the claimed deep-linear posterior schedule or a universal time--sample reparametrization, and the statement's fixed-crossover limit is defective independently of the literature.

### Question 3.11

- `local free energy ball convolution effective loss saddle becomes local minimum coarse graining`
- `log convolution e^{-V/epsilon} ball coarse grained potential strict saddle local minimum`
- `2024 2025 effective loss local free energy training plateaus saddle singular learning theory`
- `site:alignmentforum.org effective loss saddle local minimum developmental interpretability`
- `2025 effective loss local free energy saddle coarse grained neural network plateau learning coefficient`

Outcome: [Chen--Murfet](https://arxiv.org/abs/2504.18048) is related on temperature as a resolution dial, and [NeurIPS 2025 plateau work](https://proceedings.neurips.cc/paper_files/paper/2025/hash/4f06c73c45d2625f0e687f7e6a206332-Abstract-Conference.html) is phenomenologically adjacent. No source was found for this particular ball-convolution effective loss, the sets $E_k$, or the shadowing theorem.

### Problem 3.12

- `2024 2025 2026 leap complexity singular learning coefficient RLCT neural networks`
- `"leap complexity" learning coefficient`
- `saddle-to-saddle leap complexity local learning coefficient`
- `site:openreview.net "leap complexity" SGD 2025 2026`

Outcome: [Abbe--Boix-Adserà--Misiakiewicz](https://arxiv.org/abs/2302.11055) establishes the relevant leap/saddle-to-saddle program under specific assumptions. No paper connecting leap to lists of RLCT/multiplicity and unstable Hessian spectra was found.

### Problem 6.1

- `posterior mass shrinking neighborhood saddle point free energy local zeta rim term`
- `Laplace asymptotics shrinking neighborhoods saddle critical point indefinite Hessian`
- `singular learning theory free energy saddle point local learning coefficient strict saddle`
- `2024 2025 2026 Bayesian posterior around saddle shrinking window`

Outcome: no theorem of the requested form was found. [Chen et al.](https://arxiv.org/abs/2310.06301) and [Hennick--De Baerdemacker](https://arxiv.org/abs/2503.22478) are related bridges, but neither resolves shrinking-window posterior asymptotics at saddles.

### Attribution and background cross-check queries

- `Aoyagi Watanabe 2005 reduced rank regression learning coefficient formula M N H r parity`
- `"2(H+r)(M+N)" learning coefficient`
- `"M + H < N + r" learning coefficient reduced rank regression`
- `Aoyagi formula multiplicity M H N r odd`
- `Baldi Hornik 1989 all critical points BA Phi subset singular modes orthogonality classification linear network`
- `critical points matrix factorization ||BA-Phi|| all critical points truncated SVD Baldi Hornik`
- `complete characterization critical points deep linear network matrix factorization arbitrary rectangular target`
- `"all critical points" "Baldi" Hornik linear networks`
- `Zhou Liang critical points deep linear networks Baldi Hornik arbitrary dimensions data 2017`
- `Lau Furman Wang Murfet Wei local learning coefficient theorem Watanabe relatively finite variance compact semianalytic prior assumptions`
- `Watanabe singular learning theory free energy theorem fundamental conditions analytic common support prior compact semianalytic`
- `Corlouer Semler Strang Gietelink Oldenziel 2604.06366`
- `Lois Delande Sharp spectral gap for some degenerate Witten Laplacians Annales Henri Poincare published 2026`

## Machine-readable verdict

```json
{
  "file": "effective-loss-dynamics.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Theorem 2.3",
      "verdict": "correct-with-gaps",
      "note": "The Watanabe expansion is standard, but the statement omits fundamental analytic, domain, prior, support, and integrability hypotheses and does not define the global multiplicity among minimum-lambda points."
    },
    {
      "label": "Theorem 2.5",
      "verdict": "correct",
      "note": "The aligned balanced gradient equations, logistic solution, and switching-time asymptotic check directly."
    },
    {
      "label": "Theorem 2.6",
      "verdict": "correct",
      "note": "The Aoyagi-Watanabe cases, parity term, and multiplicities match the published formula; later deductions mishandle the parity term."
    },
    {
      "label": "Proposition 3.2",
      "verdict": "correct",
      "note": "Resolution-chart sublevel-volume asymptotics and their Laplace transform give the stated exponent; the cusp calculation also yields epsilon^(1/3)."
    },
    {
      "label": "Morse-saddle window calculation (lines 376-380)",
      "verdict": "correct-with-gaps",
      "note": "The fixed-window and rho<1/2 rim asymptotics are correct, but at delta=c beta^(-1/2) in dimension two the coefficient is exactly lambda=1, contradicting the blanket claim that no window reproduces the naive lambda log beta term."
    }
  ],
  "items": [
    {
      "label": "Question 3.1",
      "precision": "minor-issues",
      "openness": "possibly-resolved",
      "citations": [
        "https://arxiv.org/abs/2411.19920"
      ],
      "note": "Proposition 8.4(ii) of Lehalleur-Rimanyi directly resolves lower semicontinuity in part (b). Parts (a), (c), and the multiplicity refinement remain; the latter has no specified ordering."
    },
    {
      "label": "Problem 3.3",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2206.13206",
        "https://aif.centre-mersenne.org/articles/10.5802/aif.3636/",
        "https://link.springer.com/article/10.1007/s00023-026-01673-4"
      ],
      "note": "The class of permitted local invariants and precision of the requested prefactor are unspecified. Existing work treats broad degenerate, Morse-Bott, or diagonal-monomial cases, but not arbitrary singular analytic wells."
    },
    {
      "label": "Conjecture 3.4",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2206.13206",
        "https://aif.centre-mersenne.org/articles/10.5802/aif.3636/",
        "https://link.springer.com/article/10.1007/s00023-026-01673-4"
      ],
      "note": "The exponent follows consistently from singular well mass divided by Morse-saddle capacity and reduces to classical Eyring-Kramers; no arbitrary-singular-well theorem was found."
    },
    {
      "label": "Problem 3.5",
      "precision": "ill-posed",
      "openness": "possibly-resolved",
      "citations": [
        "https://arxiv.org/abs/2106.02588"
      ],
      "note": "Parts (a)-(b) appear open, but in part (c) the inherited X0 lies in W0, where both drift and Lipschitz diffusion vanish, so the unique solution is X_t=X0 and the hitting law is delta_X0 for every epsilon."
    },
    {
      "label": "Problem 3.6",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2110.06914",
        "https://arxiv.org/abs/2404.12293"
      ],
      "note": "Local smooth-stratum coefficients do not define a global diffusion on noncompact Gamma, no initial point or law is supplied, and restriction to strata does not determine transmission at Sigma."
    },
    {
      "label": "Problem 3.7",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2411.19920",
        "https://arxiv.org/abs/2402.03698"
      ],
      "note": "The cited works provide fiber geometry, global or zero-target RLCTs, and some local values, but no full pointwise two-rank table plus two-sided saddle table was found."
    },
    {
      "label": "Conjecture 3.8",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2310.06301",
        "https://arxiv.org/abs/2402.02364"
      ],
      "note": "The infima are defined even on noncompact saddle sets. Empirical opposing-staircase results are related, but no proof or counterexample for these two-sided coefficients was found."
    },
    {
      "label": "Problem 3.9",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2310.06301",
        "https://arxiv.org/abs/2503.22478"
      ],
      "note": "The crossover equation can have zero or two roots and no branch is chosen; with a fixed spectrum all crossovers are finite, so the n-to-infinity statement eventually tests only the final rank and not the staircase."
    },
    {
      "label": "Question 3.11",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2504.18048",
        "https://proceedings.neurips.cc/paper_files/paper/2025/hash/4f06c73c45d2625f0e687f7e6a206332-Abstract-Conference.html"
      ],
      "note": "The ordering of interval sections and the quantifiers on delta and the annealing schedule are ambiguous. No matching effective-loss or shadowing theorem was found."
    },
    {
      "label": "Problem 3.12",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2302.11055"
      ],
      "note": "The small-initialization limit, visitation rule, set-level invariants, cross-dimensional spectrum equality, N0(f), and nonempty admissible class are undefined. Leap-complexity results do not supply these definitions."
    },
    {
      "label": "Problem 6.1",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2310.06301",
        "https://arxiv.org/abs/2503.22478"
      ],
      "note": "For fixed data there is no n-to-infinity regime between finite consecutive crossovers, so the little-o-in-probability assertion is undefined without a joint scaling."
    }
  ],
  "attribution_issues": [
    "Lines 180-190 say no real-threshold lower-semicontinuity reference was found, but Proposition 8.4(ii) of the file's own cited Lehalleur-Rimanyi paper states exactly that theorem.",
    "Line 144 attributes the broad all-critical-points classification solely to Baldi-Hornik; Zhou-Liang 2017/2018 explicitly gives the necessary-and-sufficient arbitrary-dimension characterization as a generalization of Baldi-Hornik.",
    "Lines 487-491 list Delande's paper as to appear although it was published online in Annales Henri Poincare on 5 March 2026, before this draft's date."
  ],
  "confidence": "high"
}
```
