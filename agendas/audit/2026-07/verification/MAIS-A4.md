> **Historical scoped-verification record.** This report rechecks content-destructive verdicts about a pre-repair draft of [MAIS-A4](../../../A4/); it is not a second audit of the current edition. Item and line numbers may differ. See the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Verification report: `training-for-interpretability-codex-report.md`

**File audited:** `open problem supplement/training-for-interpretability.tex`
**Date:** 2026-07-15
**Verifier:** Claude Sonnet 5, scoped verification pass
**Scope note:** This pass covers only content-destructive verdicts; ill-posed and related-work verdicts were deliberately not pre-verified.

---

## Item 1 — Conjecture 5.3 ("Thermodynamic frontier"), graded RESOLVED

**Verdict: CONFIRMED**

Conjecture 5.3 (`conj:limit`) claims $P_{m,n,S}(c)/m \to p(\beta,S,c)$ along every sequence with $m\to\infty$, $n/m\to\beta\in(0,1)$, where $p$ is the Fekete limit constructed in Remark 5.2 (`rem:fekete`).

I re-derived the report's padding argument at the level of an exercise, independent of the report's own text:

- *Lower bound.* For each $j$, $\beta_j=n_j/m_j$ is rational, and the Fekete limit satisfies $p(\beta_j,S,c)=\inf_k P_{km_j,kn_j}/(km_j)\le P_{m_j,n_j}/m_j$ (the $k=1$ term of the infimum — valid regardless of which representative $(m_j,n_j)$ of the ratio is used, since Fekete's lemma gives convergence of the *full* sequence indexed by $k$, and rescaling the base pair is a subsequence of that same convergent sequence). Taking $\liminf_j$ and using continuity of $p$ (established in Remark 5.2 via the rational-convexity argument) gives $\liminf_j P_{m_j,n_j}/m_j \ge p(\beta,S,c)$.
- *Upper bound.* Fix rational $q<\beta$ and $\varepsilon>0$; Fekete supplies a block $(M,N)$, $N/M=q$, with $P_{M,N}/M \le p(q,S,c)+\varepsilon$. Tile $k_j=\lfloor m_j/M\rfloor$ copies of this block into orthogonal hidden-coordinate subspaces (valid since $k_jN\le n_j$ eventually, because $q<\beta=\lim\beta_j$), leave $r_j<M$ features unstored, paying $v(S)$ each via the dropped-feature floor (Lemma 4.1). This is a genuinely feasible point at coherence $\le c$, giving $P_{m_j,n_j}/m_j \le [k_jP_{M,N}+r_jv(S)]/m_j \to P_{M,N}/M \le p(q,S,c)+\varepsilon$ as $j\to\infty$ (since $r_j$ is bounded and $m_j\to\infty$). Let $\varepsilon\downarrow0$, then $q\uparrow\beta$ using continuity of $p$: $\limsup_j P_{m_j,n_j}/m_j \le p(\beta,S,c)$.

Matching liminf and limsup give the limit, with exactly the constant $p(\beta,S,c)$ and the normalization ($/m$, not $/n$ or unnormalized) that Conjecture 5.3 states. The argument uses only facts the file itself already proves in Remark 5.2 (subadditivity by block sums, Fekete existence of $p$ on rationals, continuous convex extension to $(0,1)$) — I independently checked those three facts and they hold (block-sum coherence is the max of the two blocks' coherences, so feasibility at $c$ is preserved; losses add because $\mathcal D_{m_1+m_2,S}$ is a product measure; the Fekete subadditive-sequence argument is the standard one). No gap found.

**Minimal repair:** Promote Conjecture 5.3 to a Proposition/Theorem with this padding argument as its proof (a few lines), and delete Remark 5.2's closing sentence "What block sums do not give is convergence along general sequences," which is exactly false once the padding step is added.

---

## Item 2 — Problem 5.7 ("Single-orbit training"), graded POSSIBLY-RESOLVED

**Verdict: CONFIRMED** (as an appropriately hedged flag, not an actual resolution)

Fetched Ivanov, Oozeer, Raval, Pejovic, Upadhyay, Abdullah, *Spectral Superposition: A Theory of Feature Geometry* (arXiv:2602.02224, Feb 2026), and read the body (Sections 1–4) plus the Limitations/Conclusion and full appendix table of contents.

Checked against Problem 5.7's two parts — (1) prove the regular pentagon is the unique global-optimum $G$-orbit for $(m,n)=(5,2)$ at high sparsity; (2) exhibit or refute a regularizer $\lambda R$ creating identifiability where $L$ alone lacks it:

- **Capacity saturation is an assumption, not a proven property of the optimum.** Theorem 1 ("Spectral Localization") opens: *"Assume the model saturates the fractional dimensionality capacity bound... Then, for every feature $i$, the spectral measure collapses to a single Dirac mass."* Section 5 (Limitations) states outright: *"To recover the geometry fully, we require capacity saturation, which we empirically verify only in toy models."* This is exactly the report's characterization — the paper classifies geometry *conditional on* capacity saturation, and only observes the assumption empirically (Figure 5, 3200 training runs), never proves it holds at a global minimizer.
- **No global-optimality or uniqueness theorem for any specific case (pentagon or otherwise).** The results (Theorem 1 localization, Theorem 3 tight-frame decomposition, Theorem 4 association-scheme classification, Corollary 5 simplex identification) classify what geometry a capacity-saturated critical point *must* have; none of them singles out the pentagon at $(m,n)=(5,2)$ as the unique optimum, and none proves global (vs. local/critical-point) optimality of anything.
- **No regularizer content anywhere in the paper.** I checked the full appendix table of contents (Feature Geometry, Spectral Theory, Localization vs Delocalization, Gradient Flow, Non-uniform Sparsity, Related Work) and the body text; there is no treatment of an added interference penalty $\lambda R$, tie-breaking, or single-orbit identifiability under regularization. Part (2) of Problem 5.7 is untouched.

So Ivanov et al. cover **neither half** of Problem 5.7 as stated: they supply a conditional structural classification tool that could in principle feed a future proof of part (1) if capacity saturation were separately established, and say nothing relevant to part (2). This matches, and is slightly more precise than, the report's own hedge ("do not plainly prove capacity saturation... human comparison is warranted"). The "possibly-resolved" tag is appropriate only as a flag for the reader to check, not as a claim of actual coverage — read that way, it is accurate.

**Minimal repair:** None needed to the report; if anything, the tag could be downgraded to "open-with-related-work" (matching Problem 5.1's treatment of the same paper) since on inspection neither sub-part is touched.

---

## Item 3 — Problem 5.8 ("Monosemanticity frontier"), graded POSSIBLY-RESOLVED

**Verdict: CONFIRMED**

**(a) Jermyn et al. attribution — confirmed to use a different architecture.** Fetched Jermyn, Schiefer, Hubinger, *Engineering Monosemanticity in Toy Models* (arXiv:2211.09169) directly. Their architecture (Section 2.3, eqs. 4–6): input $\vec x = P\cdot\vec f$ (a *fixed random projection* of the sparse feature vector down into $d$ dimensions, not the raw feature vector); $\vec e = L_1\vec x+\vec b$, $\vec h = N[\vec e]$ (nonlinearity — ReLU or GeLU); $\vec y = L_2\vec h$, and the text states explicitly: *"The second layer is a linear transformation with no bias"* — i.e. no output ReLU and no output bias. This is genuinely different from the file's Definition 4.7, $g_\theta(x)=\mathrm{ReLU}(V\ \mathrm{ReLU}(Wx+\beta)+c)$, which (i) takes the raw sparse feature vector as input, not a random projection, and (ii) has both a ReLU nonlinearity and a bias on the output layer (needed for the nonnegativity argument in Proposition 4.8). Jermyn et al.'s monosemantic/polysemantic-local-minima findings (Figure 1, Section 4.1.1) are empirical training results on their own different objective, not a theorem, and not about the file's $L'$. The report's attribution finding is correct.

**(b) Mencattini et al. — related but not a resolution for the file's architecture.** Fetched Mencattini, Montagna, Locatello, *The Rate-Distortion-Polysemanticity Tradeoff in SAEs* (arXiv:2605.14694). Their setup (Section 2, "Data Generating Process," eq. 4 and Definition 1–2): a *fixed* ground-truth concept matrix $V$ generates activations $x=\sum_{\ell\in S}v_\ell$; a separately-parameterized SAE $(\theta=(W_{enc},b_{enc},W_{dec},b_{dec}))$ is then trained *post hoc* to reconstruct $x$ through a sparse code, with a **linear** decoder ($\hat x_\theta = W_{dec}^\top z_\theta(x)+b_{dec}$, no output ReLU). Their driving mechanism for polysemanticity is concept *co-occurrence* under a fixed rate budget $K$ (number of active SAE latents), formalized in their Lemma 1 / Theorem 2 ("rate tax"); there is no architectural bottleneck analogous to $k<m$ forcing polysemanticity — dictionary size is not the scarce resource, co-occurrence probability is. This is a different problem in the same toy-model family: closer in spirit to the file's Problem 5.5 (post-hoc recovery from a fixed dictionary) than to Problem 5.8, which asks about the frontier $P'_{m,k,S}(\delta)$ for the *jointly-trained*, *bottlenecked* ($k<m$) architecture of Definition 4.7 itself. The report's own hedge ("its SAE setup and polysemanticity measure must be compared carefully... not yet an exact resolution... may cover a nearby frontier") is accurate and, if anything, slightly generous — the mechanism (co-occurrence-driven vs. bottleneck-driven) and architecture (post-hoc linear-decoder SAE on fixed activations vs. jointly-trained ReLU-output bottleneck autoencoder on raw features) are substantively different, not merely differently parameterized versions of the same object.

**(c) The missing $\delta^\ast $ convention is a genuine, minor gap.** Problem 5.8 part (1) defines $\delta^\ast (m,k,S)=\inf\lbrace \delta: P'_{m,k,S}(\delta)<P'_{m,k,S}(0)\rbrace $. Since $P'_{m,k,S}$ is non-increasing in $\delta$ (relaxing the constraint set), the set is non-empty whenever $P'_{m,k,S}(1)<P'_{m,k,S}(0)$ — plausible generically, since Theorem 4.3/Remark 4.4 (superposition beating orthogonality) suggests the true optimum can beat monosemantic storage — but the file gives no argument ruling out the degenerate case $P'_{m,k,S}(\delta)=P'_{m,k,S}(0)$ for all $\delta\in[0,1]$ (i.e., the true global optimum already being perfectly monosemantic), in which case the defining set is empty and $\delta^\ast $ is undefined by the usual $\inf\varnothing=+\infty$ convention, contradicting the implicit intent that $\delta^\ast \in[0,1]$. This is a real, if small, hole in the problem statement, correctly flagged as `minor-issues` rather than something more severe.

**Minimal repair:** (i) Correct the Jermyn attribution to note the architectural difference (random-projected input, linear unbiased output) rather than calling Def. 4.7 "the setting of" Jermyn et al.; (ii) add a sentence to Problem 5.8 fixing $\delta^\ast \in[0,1]$ with $\delta^\ast :=1$ (or $\inf\varnothing:=1$) by convention when the set is empty.

---

## Summary

1. **Conjecture 5.3 (RESOLVED):** CONFIRMED — the padding argument is a complete, correct proof from the file's own Remark 5.2; matches the conjecture's exact constant and normalization.
2. **Problem 5.7 (POSSIBLY-RESOLVED):** CONFIRMED as an accurate hedge — Ivanov et al.'s classification is conditional on unproven capacity saturation and addresses neither the pentagon-uniqueness nor the regularizer half of the problem.
3. **Problem 5.8 (POSSIBLY-RESOLVED):** CONFIRMED — Jermyn et al. verified to use a different architecture (random-projected input, linear unbiased output); Mencattini et al. verified to solve a related but architecturally and mechanistically distinct problem; the missing $\delta^\ast $ empty-set convention is a genuine minor gap.

**Recommendation:** Apply the three minimal repairs above (promote Conjecture 5.3 to a proved result with the padding argument; downgrade or caveat Problem 5.7's "possibly-resolved" tag to reflect that neither sub-part is actually touched; fix the Jermyn attribution and the $\delta^\ast $ convention in Problem 5.8) before the next revision pass.
