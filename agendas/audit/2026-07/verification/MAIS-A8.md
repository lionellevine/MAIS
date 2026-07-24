> **Historical scoped-verification record.** This report rechecks content-destructive verdicts about a pre-repair draft of [MAIS-A8](../../../A8/); it is not a second audit of the current edition. Item and line numbers may differ. See the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Verification of audit verdicts: ood-generalization.tex

- **File:** `open problem supplement/ood-generalization.tex` (supplement draft of July 12, 2026)
- **Audit report verified:** `audit/ood-generalization-codex-report.md` (GPT 5.6 Sol)
- **Date:** 2026-07-16
- **Verifier:** Claude Fable 5, scoped verification pass
- **Scope note:** This pass covers only content-destructive verdicts; ill-posed and related-work verdicts were deliberately not pre-verified.

Grading convention: a resolution answering a weaker/stronger/different statement than the file's precise item is graded PARTIAL with the surviving core stated; a counterexample violating a stated hypothesis would be REJECTED.

---

## 1. Conjecture 5.3 (kernel regime) graded RESOLVED — **CONFIRMED**

**Auditor's claim (Finding 2).** The kernel gradient flow trajectory can be written with nonnegative increasing coefficients; at least one coefficient diverges; strict positivity of every training–probe kernel value forces the probe value to $+\infty$, proving the conjecture's exact conclusion.

**Re-derivation against the file's setup (lines 257–267).** The conjectured conclusion is a statement about the kernel flow $\bar f_t$ alone: "almost surely $\bar f_t(x_a(s^\ast )) \to +\infty$." The flow is
$\partial_t \bar f_t(x) = -\mathbb E_{\nu_0}[\ell'(\bar f_t(x_i))\ K_{\mathrm{NTK}}(x, x_i)]$
over the $L$ training inputs $x_i = (1,p,L)$, $0 \le p \le L-1$, with weights $\omega_i = 1/L$. Since $-\ell'(z) = 1/(1+e^z) \in (0,1)$:

1. **Representation.** $\bar f_t = f_0 + \sum_i \beta_i(t) K(x_i, \cdot)$ with $\beta_i(0) = 0$ and $\beta_i'(t) = \omega_i/(1 + e^{\bar f_t(x_i)}) > 0$. Verified: the sign convention is right ($\ell' < 0$), each $\beta_i$ is strictly increasing from $0$, hence nonnegative. Well-posedness: the training values satisfy a closed finite ODE system with Lipschitz, bounded right-hand side, so a unique global solution exists — consistent with the auditor's own Finding 1, which correctly exempts this conjecture from the ReLU nonuniqueness issue.
2. **Divergence.** If all $\beta_i$ were bounded, all $L$ training values $\bar f_t(x_i) = f_0(x_i) + \sum_j \beta_j(t) K(x_j, x_i)$ would be bounded, so each $\beta_i'$ would be bounded below by a positive constant, giving $\beta_i \to \infty$ — contradiction. Since each $\beta_i$ is monotone, $\max_i \beta_i(t) \to \infty$. Verified.
3. **Kernel positivity.** The two-layer ReLU NTK is $\Sigma_1(x,x') + (x \cdot x')\ \dot\Sigma_1(x,x')$, where $\Sigma_1$ is the order-1 arc-cosine kernel ($>0$ for angle $< \pi$) and $\dot\Sigma_1 = (\pi - \vartheta)/2\pi > 0$ at acute angles. Every $x_i \cdot x^\ast  = 1 + p\ p^\ast  \ge 1 > 0$, so $K(x_i, x^\ast ) > 0$ for all $i$. Verified (the auditor is also right that no strict-positive-definiteness theorem is needed — pointwise positivity at these $L+1$ specific pairs suffices and is elementary).
4. **Conclusion.** $\bar f_t(x^\ast ) \ge f_0(x^\ast ) + \max_i \beta_i(t) \cdot \min_j K(x_j, x^\ast ) \to +\infty$, almost surely since $f_0(x^\ast )$ is a Gaussian value, finite a.s. This is the conjecture's stated conclusion, with no reformulation. The auditor is also correct that the file's own proposed route (RKHS max-margin theorem, Problem 7.3 step (a)) is unnecessary for this statement, while the finite-width interchange in Problem 7.3 remains genuinely open.

**Verdict: CONFIRMED.** The conjecture as stated is a short proposition.

**Minimal repair:** restate Conjecture 5.3 as a proposition with the four-line increasing-coefficients proof, and pare Starter Problem 7.3 to its surviving parts (finite-width $m\to\infty$, $t\to\infty$ interchange; the $\varepsilon>0$ kernel SVM computation). The Jacot/Arora convergence sentence inside the conjecture's setup is a separate attribution question (auditor Finding 7), outside this pass's scope, and does not affect the conclusion about $\bar f_t$.

---

## 2. Conjecture 5.4 (mean-field regime) graded RESOLVED — **PARTIAL**

**Auditor's claim (Finding 3).** Under the stated convergence premise, combined with the Chizat–Bach max-margin characterization, the unique variation-norm max-margin predictor is a single ReLU unit in direction $x_0 = (1,0,L)$, which is strictly positive at the probe; hence the conditional conjecture holds. Separately, the premise's "equivalently" is flagged as false.

**Re-derivation.** The mathematics is correct in every step I checked:

- **Point-evaluation bound.** For any representation $f = \int a\ \varphi(u \cdot x)\ d\mu$, at the training input $x_0 = (1,0,L)$ (the $p=0$ point): $f(x_0) \le \int |a|\ \Vert u\Vert \ \Vert x_0\Vert \ d\mu = \Vert f\Vert _{\mathrm{var}}\ \Vert x_0\Vert $, by $\varphi(u \cdot x_0) \le \Vert u\Vert \Vert x_0\Vert $. Verified.
- **Attainment.** The unit $f_0(x) = \varphi(x_0 \cdot x / \Vert x_0\Vert )$ has variation norm 1 and value $(1 + L^2)/\sqrt{1+L^2} = \sqrt{1+L^2}$ at every training input $(1,p,L)$, since $x_0 \cdot (1,p,L) = 1 + L^2$ independent of $p$. So the max margin per unit variation norm is exactly $\sqrt{1+L^2}$. Verified.
- **Uniqueness.** Any unit-variation-norm maximizer has $f(x_0) = \sqrt{1+L^2}$, and equality in the bound forces, for a.e. atom, $a \ge 0$ and $u \parallel x_0$ (Cauchy–Schwarz equality case). So the max-margin predictor is the single ray, with probe value $x_0 \cdot (1, p^\ast , 0)/\Vert x_0\Vert  = 1/\sqrt{1+L^2} > 0$. Verified.
- **False "equivalently."** The auditor is right that pointwise convergence of normalized predictors is not equivalent to weak convergence of normalized representing measures (the representation map is many-to-one, and pointwise predictor convergence alone gives neither tightness nor a distinguished measure limit). This is a genuine defect in the file's premise.

**Why PARTIAL rather than CONFIRMED.** The file's premise, as literally worded, is pointwise predictor convergence ("in the sense that the normalized predictors ... converge pointwise"), with measure convergence offered only as a (false) parenthetical gloss. The Chizat–Bach max-margin characterization that the resolution combines with applies under the measure-convergence (Chizat–Bach hypotheses) reading; under the literal pointwise-only premise, the characterization is not available by citation, so the conclusion is not established for the conjecture exactly as stated. The report resolves a mildly repaired reformulation — and to its credit says so — but its headline grade RESOLVED overstates by exactly this margin. Surviving core: under the weak-measure-convergence premise the conjecture is a proposition with the report's proof; under the literal pointwise premise the implication "limit predictor is max-margin" is an unproven (plausible, likely bridgeable by a tightness/subsequence argument on sphere-normalized measures, but not written) step.

**Minimal repair:** fix the premise to weak convergence of the normalized measures (deleting the false "equivalently"), then restate the conjecture as a conditional proposition with the single-unit uniqueness proof.

---

## 3. Problem 5.8 (which representations misgeneralize?) graded POSSIBLY-RESOLVED — **PARTIAL**

**Auditor's claim (Finding 8).** The monomial subproblem is fully resolved: all training–probe feature inner products are positive, so every max-margin KKT combination selects the proxy at the probe, for every $k$ and every $L \ge 4$; the general structural criterion remains open.

**Re-derivation.** Problem 5.8 has two deliverables: (i) for the monomial encoding $\psi_k(p,c) = (p^i c^j)_{i+j\le k}$, determine the probe sign as a function of $(k,L)$; (ii) more ambitiously, a structural criterion on arbitrary feature maps $\psi$.

For (i): the $\varepsilon = 0$ data are $\psi_k(p, L)$, $0 \le p \le L-1$, all labeled $+1$; separable via the constant feature $(i,j)=(0,0)$, so the max-margin program is feasible and its unique optimum satisfies the KKT form $\hat w = \sum_p \alpha_p \psi_k(p, L)$ with $\alpha_p \ge 0$; since the constraints force $\hat w \neq 0$, some $\alpha_p > 0$. At the probe $(p^\ast , 0)$, every monomial with $j \ge 1$ vanishes, leaving
$\psi_k(p,L) \cdot \psi_k(p^\ast ,0) = \sum_{i=0}^{k} (p\ p^\ast )^i \ge 1 > 0$
(the $i=0$ term is $1$, covering $p=0$ via $0^0 = 1$; all other terms nonnegative). Hence $\hat w \cdot \psi_k(p^\ast ,0) > 0$: the probe sign is $+$ (proxy) for every $k \ge 0$, $L \ge 4$. Verified — deliverable (i) is settled outright, not merely "possibly": the answer is that the entire monomial family misgeneralizes, with the leading-order sign never vanishing at the probe (so the problem's deferred-to-residual clause is never triggered).

For (ii): the argument says nothing about arbitrary $\psi$ (e.g., encodings mixing signs, where training–probe inner products need not be positive); the requested criterion remains open. Note the relative encoding of Proposition 4.4 already shows the phenomenon is not universal, so (ii) has genuine content.

**Verdict: PARTIAL** for the whole item: subproblem (i) is definitively resolved by the auditor's (correct) computation; subproblem (ii) stays open. The auditor's prose says exactly this, but the headline grade should read "partially resolved," not "possibly-resolved" — nothing is merely possible about (i).

**Minimal repair:** move the monomial computation into the text as a one-paragraph example extending Example 4.5, and restate Problem 5.8 as the structural-criterion question alone.

---

## 4. Problem 6.1 (linear policy gradient, no diversity) graded RESOLVED — **CONFIRMED**

**Auditor's claim (Finding 4).** A direct monotonicity argument gives $g_p \ge 0$ per training state, strictly positive at $p = L-1$; the aggregate $B = w_0 + L w_2$ is strictly increasing and diverges; the invariant $w_2 - L w_0$ and the bound $\dot w_1 \le \frac{L-1}{1+L^2}\dot B$ then give both conclusions (a) $J_0 \to 1$ and (b) probe logit $\to +\infty$, for every finite initialization.

**Re-derivation against the file's setup (lines 321–331).** With $\varepsilon = 0$ the coin is fixed at $c = L$, so $J_0$ depends on $w$ only through the logits $z_p = w \cdot (1,p,L) = w_0 + p w_1 + L w_2$ at the nonterminal states $p = 0,\dots,L-1$. Hence $\dot w = \nabla J_0(w) = \sum_p g_p\ (1,p,L)$ with $g_p = \partial J_0/\partial z_p$. ($J_0$ for the linear model is smooth with bounded gradient, so the flow is globally well-posed — no ReLU issue here, again consistent with the auditor's Finding 1 carve-out.)

1. **$g_p \ge 0$.** Let $V_t(p)$ be the probability of reaching $L$ within $t$ remaining steps under the current policy. $V_t(p)$ is nondecreasing in $t$ (success is a hitting event), and any path from $p-1$ to $L$ must first hit $p+1$, so by the strong Markov property $V_{t-1}(p-1) \le V_{t-3}(p+1) \le V_{t-1}(p+1)$. Differentiating the episode probability in $z_p$ gives a sum over visits to $p$ of (occupancy) $\times\ \sigma'(z_p) \times [V_{t-1}(p+1) - V_{t-1}(\max(p-1,0))] \ge 0$ (at $p=0$ the comparison $V_{t-1}(1) \ge V_{t-1}(0)$ holds by the same first-passage argument). Verified.
2. **$g_{L-1} > 0$ at every finite $w$.** Start $p_0 = L-1$ has probability $1/(L+1)$; a right step succeeds immediately, while after a left step the success probability is $< 1$, since under finite logits the all-left continuation has positive probability and fails. With $\sigma'(z_{L-1}) > 0$, verified.
3. **Dynamics.** $\dot B = \dot w_0 + L \dot w_2 = (1+L^2)\sum_p g_p > 0$; $\dot w_1 = \sum_p p\ g_p \in [0, \frac{L-1}{1+L^2}\dot B]$; $\frac{d}{dt}(w_2 - L w_0) = L\sum g_p - L \sum g_p = 0$. All three verified.
4. **Divergence.** If $B$ were bounded: $B$ (increasing, bounded) converges; $w_1$ (nondecreasing, with increments dominated by $B$'s) converges; $B$ and the invariant determine $(w_0, w_2)$ through a linear system with determinant $1 + L^2 \neq 0$, so $w(t)$ converges to a finite $w^\infty$; continuity of $g_{L-1}$ then keeps $\dot B \ge (1+L^2)\ g_{L-1}(w^\infty)/2 > 0$ eventually, contradicting boundedness. So $B \to +\infty$; the invariant gives $w_0 \to +\infty$ (since $B = (1+L^2)w_0 + L\ \text{const}$), and $w_1 \ge w_1(0)$. Verified.
5. **Conclusions.** Training logits $z_p = B + p w_1 \ge B + p\ w_1(0) \to +\infty$, so every right-step probability tends to 1 and $J_0 \to 1$: part (a). Probe logit $w \cdot (1, p^\ast , 0) = w_0 + p^\ast  w_1 \ge w_0 + p^\ast  w_1(0) \to +\infty$: part (b). Both hold for **every** initialization, which settles the problem's actual quantifiers ("almost every initialization," "probability one") a fortiori — the resolution is of the full stated problem, not a special case. Verified.

**Verdict: CONFIRMED.** Both parts of Problem 6.1 are settled, deterministically.

**Minimal repair:** restate Problem 6.1 as a proposition with this proof; rewrite the following paragraph ("Even part (a) is not covered by current theory...") and the Section 7 blanket openness sentence (line 379), which currently claim Problems 5.1–6.3 open as stated.

---

## Summary table

| Item | Auditor's grade | Verification | Note |
|---|---|---|---|
| Conjecture 5.3 | resolved | **CONFIRMED** | Increasing-coefficient argument fully checks; conjecture as stated is a proposition. |
| Conjecture 5.4 | resolved (minor issues) | **PARTIAL** | Math correct; resolves the measure-convergence reading of the premise, not the literal pointwise premise (whose "equivalently" is indeed false). |
| Problem 5.8 | possibly-resolved | **PARTIAL** | Monomial subproblem definitively resolved (verified); structural-criterion half stays open. |
| Problem 6.1 | resolved | **CONFIRMED** | Monotonicity/invariant argument fully checks; settles both parts for every initialization. |

**Recommendation.** Accept Findings 2 and 4 as written (Conjecture 5.3 and Problem 6.1 must be reclassified as solved and the openness claims at lines 238, 331, 349, 379 revised); accept the mathematics of Findings 3 and 8 but downgrade their headlines to partial resolutions — Conjecture 5.4 needs its premise repaired before the resolution applies as stated, and Problem 5.8 survives as its structural-criterion half.
