> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A3](../../../agendas/MAIS-A3/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Audit of `superposition-geometry.tex`

## Summary verdict

This file has significant issues and is not publication-ready in its current form, although its two displayed proofs (Propositions 3.1 and 3.2) and its classical geometric/compressed-sensing theorems check out. The most serious problems are internal rather than merely bibliographic: Conjecture 4.4 is false under its stated hypotheses (an explicit orthogonal two-feature, all-on counterexample satisfies both displayed bounds), while Conjecture 4.5 is already an elementary theorem, with the stronger values \(\lambda _0=1\) and \(C=0\). Problem 4.3 cannot characterize “which pairs merge” from the listed scalar summaries, Problem 4.7's claim of openness “even for \(k=\lceil\log m\rceil\)” ignores polynomial-identifiability/recovery results going back at least to Spielman--Wang--Wright and Awasthi--Vijayaraghavan, and the 2026 related-work account misses direct work on feature splitting and dictionary-level amortization. Several global prose claims also overgeneralize the very special two-feature, constant-coefficient propositions, and the statement that a learned ReLU encoder is one ISTA step is false without tying \(W,b\) to the decoder and step size. The TeX compiles successfully, but the mathematical/open-status defects require revision before publication.

## Findings, ordered by severity

### 1. Conjecture 4.4 is false: its second inequality does not exclude dense all-on supports

**Location:** lines 222--232, especially the hypotheses at lines 223--229 and the claimed explanation at line 232.

Take \(m=2\), choose any sufficiently large \(n\), let \(v_1=e_1,v_2=e_2\), and take \(p=1\). Then \(\mu=0\), so the first displayed condition is automatic, and for every proposed absolute \(c>0\) the second holds once
\[
n\ge \log 2\,\bigl((2+\log 2)/c\bigr)^2.
\]
The data are \(y=a e_1+b e_2\), with independent \(a,b\sim\mathrm{Unif}[1,2]\). Define
\[
u_1=(2e_1+e_2)/\sqrt5,\qquad u_2=(e_1+2e_2)/\sqrt5.
\]
Every such \(y\) has the nonnegative exact code
\[
z={\sqrt5\over3}(2a-b,\,2b-a),
\qquad \|z\|_1={\sqrt5\over3}(a+b),
\]
so \(F_\lambda(u_1,u_2)\le\sqrt5\lambda\). At the true dictionary, for \(0<\lambda<1\), coordinatewise soft thresholding gives \(F_\lambda(\Phi)=3\lambda-\lambda^2\). More strongly, any dictionary that \(C\lambda\)-recovers \(\Phi\) has columns within \(O(\sqrt\lambda)\) of \(e_1,e_2\); projecting a candidate reconstruction onto \(e_1+e_2\) gives uniformly
\[
F_\lambda(\Psi)/\lambda\ge 3-O(\sqrt\lambda),
\]
whereas the slanted dictionary has quotient at most \(\sqrt5\). Thus, for all sufficiently small \(\lambda\), no global minimizer can \(C\lambda\)-recover \(\Phi\). This refutes the conjecture for every proposed pair of constants \(c,C\).

The prose at line 232 notices the \(p=1\) obstruction but incorrectly says the second inequality removes it. It removes it only in some overcomplete scalings; because the conjecture allows \(m\le n\) and arbitrarily large unused ambient dimension, the right-hand side grows with \(n\). A repair needs a direct upper bound on \(p\) or expected support size that does not weaken when unused dimensions are added (and probably an explicit \(m>n\) regime).

### 2. Conjecture 4.5 is already proved by a pointwise radial lower bound

**Location:** lines 234--242; repeated as allegedly open at lines 220, 303, 315, 325, and 339.

For a unit-column dictionary \(\Psi\), any nonnegative code \(z\), \(r=\|y\|\), and \(t=\|z\|_1\),
\[
\|\Psi z\|\le t,
\qquad
\|y-\Psi z\|\ge (r-t)_+.
\]
Consequently
\[
\ell_\lambda(y,\Psi)
\ge \min_{t\ge0}\left\{\tfrac12(r-t)_+^2+\lambda t\right\}
=
\begin{cases}
\lambda r-\lambda^2/2,&0<\lambda<r,\\
r^2/2,&\lambda\ge r.
\end{cases}
\]
In Conjecture 4.5 the two nonzero data rays are \(v_1\), of norm 1, and \(v_1+v_2\), of norm \(2\cos(\theta/2)\ge\sqrt2\). For every \(0<\lambda<1\), the dictionary \(\{v_1,w\}\) attains this lower bound separately on both events by radial soft thresholding. Equality on two positive-probability, distinct rays forces one atom on each ray, so \(\{v_1,w\}\) is the unique global minimizer up to permutation. Since \(\theta\le\pi/2\),
\[
\max_j\langle u_j,v_2\rangle
=\max\{\cos\theta,\cos(\theta/2)\}
=\cos(\theta/2).
\]
Thus the conjecture holds with the strictly stronger constants
\[
\lambda_0=1,\qquad C=0.
\]
No compactness or limiting argument is needed. This also settles the \(b=0\) face of Problem 5.1 exactly, contrary to line 303's suggestion that the starter calculation is needed to prove or refute the conjecture.

### 3. The claimed “support-statistics characterization” in Problem 4.3 is not determined by its inputs

**Location:** lines 211--218; also abstract line 30, survey quotation line 40, and summary line 339.

Problem 4.3 asks for recovery, merging, and “which pairs merge” as a function of coherence, marginal rates, the single maximum \(r(\pi)\), and solo-firing rates. These statistics discard the pairwise and higher-order information needed for that answer. For example, with four equally frequent features, give equal mass to every singleton and equal mass either to the paired supports \(\{1,2\},\{3,4\}\) or to \(\{1,3\},\{2,4\}\). The two laws have identical labeled marginals, identical labeled solo rates, identical sparsity, and identical maximum co-occurrence ratio, but different pairs co-occur/nest. A scalar coherence likewise discards the full Gram matrix and cannot identify which geometric pair is favored. Hence an exact “which pairs” characterization cannot be a function of the displayed arguments.

The problem can be made well-posed by asking for sufficient/necessary bounds based on these summaries, or by admitting the full pairwise conditional matrix/full support law and full Gram matrix. As written, part (2) makes the headline problem ill-posed as a requested characterization.

### 4. The file overstates what Propositions 3.1 and 3.2 prove

**Location:** abstract line 30 and conclusion line 339; compare the actual hypotheses at lines 146--184.

The propositions are correct, but they concern exactly two atoms, exactly two or three support events, deterministic unit coefficients, no noise, \(M=m=2\), and the constrained objective. They do not prove that nested supports “whenever” present force merging throughout Definition 2.2's model class, nor that support correlations “alone decide identifiability.” Coefficient-law support can change even feasibility. For example, retain supports \(\{1\}\) and \(\{1,2\}\) but use an unbounded positive coefficient law with finite second moment (e.g. exponential). Joint-event directions approach both boundary rays because the coefficient ratio has support \((0,\infty)\); any two-ray cone of finite constrained cost must contain that full limiting sector, and the same angular monotonicity used in Proposition 3.2 favors the true boundary rays. Feature 2 remains nested, but Proposition 3.1's fixed joint ray and forced merged atom disappear.

The honest claim is that one particular nested-support model merges and one particular solo-firing model recovers. Lines 30 and 339 turn examples into a universal theorem.

### 5. Problem 4.7's openness account omits older polynomial identifiability results

**Location:** lines 258--262 and the classical/algorithmic survey at lines 319--321.

The blanket statement “open even for \(k=\lceil\log m\rceil\)” is untenable without a much narrower quantifier. [Spielman--Wang--Wright](https://proceedings.mlr.press/v23/spielman12.html) prove polynomial-sample uniqueness/recovery for arbitrary square invertible dictionaries under sparse random coefficients. Choosing a Bernoulli rate below \(k/m\) and conditioning on the positive-probability event that all polynomially many sampled columns have support at most \(k=\lceil\log m\rceil\) gives existential polynomial-size, \(k\)-sparse datasets in the allowed square regime. More directly for overcomplete dictionaries, [Awasthi--Vijayaraghavan, FOCS 2018](https://arxiv.org/abs/1804.08603) state polynomial identifiability for near-linear sparsity under RIP and mild triple-occurrence support conditions; their paper explicitly contrasts this with the earlier \(n^{O(k)}\) bounds.

Those results do not obviously settle the strongest possible reading—every dimension \(n\ge2k\), almost every merely-spark dictionary, exact uniqueness against every unrestricted competing \(B\)—so I classify the item `possibly-resolved`, not cleanly `resolved`. The file must specify whether the quantifier is “for every \(n\ge2k\),” whether genuine overcompleteness/minimal dimension is required, and why the cited random/polynomial-identifiability results do not meet its definition. In its present form the square case and the sentence “even for log m” make the claimed novelty misleading.

### 6. The June 2026 splitting theorem substantially overlaps Problem 4.6

**Location:** lines 244--252, especially “nothing is known” at line 252; related-work lines 325 and 335.

[Dalili--Mahdavi, *Subspace-Aware Sparse Autoencoders* (arXiv:2606.06333)](https://arxiv.org/abs/2606.06333) proves that multidimensional features force exponentially many single-direction atoms for small reconstruction error and, more directly, that the end-to-end \(\ell^1\)-regularized SAE objective has a continuous descent path from the true basis to a lower-risk split dictionary. This does not solve the exact two-cap, nonnegative-lasso population problem in 4.6, but it is direct theory of splitting as geometric quantization/objective preference and contradicts the broad statement that nothing is known.

There is also a precision omission: the requested answer is said to be a function of \((\theta,\tau,\lambda,a,b,c,M)\), but spherical-cap quantization and normalized surface measure depend essentially on the ambient dimension \(n\), introduced in the first sentence and then omitted from the parameter list.

### 7. The dictionary-level amortization comparison has been examined, contrary to line 275

**Location:** Problem 4.8, lines 266--275; related-work line 325.

[Sun--Wang--Hu, *The Price of Amortized Inference in Sparse Autoencoders*, ICLR 2026](https://openreview.net/forum?id=33wY6AI13k) explicitly studies how a shared amortized encoder distorts learned features and ties amortization to absorption, splitting, dead, and dense latents, comparing amortized, semi-amortized, and non-amortized methods. [O'Neill--Gumran--Klindt](https://proceedings.mlr.press/v267/o-neill25a.html) remains the clean code-level impossibility result. The ICLR paper does not appear to prove the exact population-global-minimizer separation requested in 4.8(2), so the precise problem remains open-with-related-work, but “That dictionary-level comparison ... remains unexamined” is false.

The nonattainment fallback at line 272 is also not mathematically adequate. If \((W,b)\) diverges, a minimizing sequence need not have a limit point in the full domain. Compactness only guarantees a subsequential limit of the dictionary component \(\Psi\). The statement should define the set of projected dictionary accumulation points of minimizing sequences, and specify whether “every” or “some” minimizing sequence is intended.

### 8. A generic learned ReLU encoder is not “one ISTA step”

**Location:** lines 128--132 and repeated at line 275.

For decoder \(\Psi\), step size \(\eta\), and zero initialization, one nonnegative ISTA step is
\[
z^{(1)}=\operatorname{ReLU}(\eta\Psi^\top y-\eta\lambda\mathbf1).
\]
Thus \(\operatorname{ReLU}(Wy+b)\) is literally that step only when \(W=\eta\Psi^\top\) and \(b=-\eta\lambda\mathbf1\). The file learns arbitrary \(W,b\) jointly and imposes neither relation. It is more accurate to call the encoder a one-layer learned-thresholding/LISTA-style amortizer. Daubechies--Defrise--De Mol establishes iterative thresholding, but does not justify identifying arbitrary encoder weights and biases with a decoder-tied ISTA step.

The phrase “an SAE is the same objective” also suppresses the learned decoder/output bias used in standard vanilla SAE formulations. A centered idealization is defensible, but it must be labeled as such rather than attributed literally to all practical SAEs.

### 9. The 2026 “global frontier” prose conflicts with the file's own Tang citation

**Location:** lines 323--325.

Line 323 says “no theorem locates the global minimizers” of reconstruction-plus-sparsity objectives. Yet the next paragraph cites [Tang et al., arXiv:2512.05534](https://arxiv.org/abs/2512.05534), whose abstract explicitly says it “characterize[s] its global solution set, non-identifiability, and spurious optima” for a unified sparse-dictionary-learning formulation. The objectives/hypotheses may differ from the population nonnegative lasso value function \(F_\lambda\), in which case the file should state the exact distinction. As written, “locality remains the frontier” and the cited global-solution characterization appear contradictory.

The same paragraph omits the ICLR 2026 amortization paper and the June 2026 subspace/splitting theorem above. O'Neill et al. is also now an ICML 2025 paper, not only an arXiv preprint.

### 10. Problem 5.3 is not a reproducible numbered empirical problem and substantially overlaps existing experiments

**Location:** lines 311--315.

The item leaves undefined the distribution meant by “uniformly random dictionary,” the interpolation law beyond an example, the grids for \(\gamma,\lambda,M\), the merge tolerances \((\varepsilon,\delta)\), the split tolerance, optimizer/schedule/stopping rule, sample sizes, number of seeds, and uncertainty estimates. “Standard optimizers” and “many random initializations” do not determine an experiment, and \(\lfloor\gamma m/2\rfloor\) gives a stepwise rather than smooth interpolation. Consequently the requested table is not reproducible as written.

It also overlaps the hierarchical synthetic experiments in [Matryoshka SAEs](https://proceedings.mlr.press/v267/bussmann25a.html), which use child-implies-parent feature trees and measure absorption, as well as newer controlled ground-truth benchmarks such as [Sanity Checks for SAEs](https://openreview.net/forum?id=bEYHoD7fCj). A particular preregistered sweep could still be useful, but “publishable” and novelty cannot be asserted from this underspecified recipe.

### 11. Minor background/technical qualifications

**Locations:** lines 55, 70, 126, 242, 284--295, 319--327, and 341--425.

- Line 55 calls ReLU “the standard” nonlinearity, although modern transformers commonly use GELU/SiLU. This is harmless for the formal model but inaccurate motivation.
- “Every 2k columns are linearly independent” is vacuous when fewer than \(2k\) columns exist; the standard formulation is \(\operatorname{spark}(\Phi)>2k\), or independence of every subset of at most \(2k\) columns.
- For \(F_0\), “some minimizing code” is undefined on samples outside the cone (where the infimum is \(+\infty\)); liveness should be restricted to dictionaries/samples with a finite constrained cost.
- Line 295's “piecewise-polynomial integral” is false in parameters. Already \(\int_0^1\operatorname{ReLU}(wx+b)^2dx\) contains a \(b^3/w\) term when the threshold lies inside \([0,1]\); the loss is piecewise rational/semialgebraic, not generally polynomial.
- The classical packing, Welch, RIP, dictionary-learning, and frame-potential claims are broadly correct. Johnson--Lindenstrauss is an indirect citation for the spherical packing proposition rather than a direct statement of it, and the Gaussian RIP sentence in Theorem 2.5 is a separate standard result rather than something established by the two sharp-constant citations alone.
- `latexmk` completed successfully. Remaining warnings are overfull boxes (notably lines 47--48 and 105--109) and underfull bibliography/vbox warnings, not correctness failures.

## Proof and background-claim ledger

| Result or claim | Verdict | Audit note |
|---|---|---|
| Proposition 2.3 (almost-orthogonal packing), lines 89--93 | `correct` | The exponential \(e^{c\varepsilon^2 n}\) packing follows from spherical concentration and a union bound; for small \(\varepsilon^2n\), the floor permits the trivial one-vector case. The JL citation is indirect. |
| Theorem 2.4 (Welch), lines 95--100 | `correct` | Bound and ETF equality description are correct. |
| Theorem 2.5 (compressed sensing), lines 102--106 | `correct` | \(\delta_{2s}<1/\sqrt2\) is the sharp uniform basis-pursuit threshold; normalized Gaussian matrices satisfy the stated order of measurements with the usual fixed-distortion/high-probability constants. |
| Coding-cost minimizer claim, lines 112--126 | `correct-with-gaps` | For \(\lambda>0\), coercivity from \(\lambda\|z\|_1\) gives a nonempty compact convex argmin. The analogous liveness convention for \(F_0\) needs a finite-feasibility qualification. |
| “SAE is one ISTA step,” lines 128--132 | `flawed` | Only true under \(W=\eta\Psi^\top\), \(b=-\eta\lambda\mathbf1\); arbitrary learned \(W,b\) is not an ISTA iterate. |
| Proposition 3.1 (nesting forces merging), lines 146--162 | `correct` | The triangle inequality, equality condition, uniqueness of the two ray atoms, and value comparison all check. |
| Coherence comparison/absorption discussion, line 164 | `correct-with-gaps` | The equality threshold \(\theta=2\pi/3\) is correct and the two-feature analogy to absorption is apt; it should not be generalized to all nested-support models. |
| Proposition 3.2 (solo firing), lines 168--184 | `correct` | Cone parametrization, Cramer's-rule formula, both derivatives, strictness from \(a,b>0\), and boundary minimum are correct. |
| Separability/anchor-word analogy, line 186 | `correct` | Solo pure events are the relevant NMF/topic-model anchor condition. |
| Merge example, line 207 | `correct` | For \(w\), coefficients \(\alpha=\beta=(2\cos(\theta/2))^{-1}>1/2\), and the proposed \(\delta\) meets all inequalities. |
| Random coherence scaling, line 232 | `correct` | IID Haar columns have \(\mu=O(\sqrt{\log m/n})\) in the normal parameter range; the subsequent claim that the bound excludes \(p=1\) is false. |
| Penalized radial-zero threshold, line 242 | `correct` | A single-ray nonnegative lasso codes zero exactly when \(\lambda\ge\|y\|\). The same radial calculation actually proves Conjecture 4.5. |
| Classical uniqueness counts, lines 319 and 262 | `correct-with-gaps` | The cited exhaustive-support counts and stability claims track Aharon--Elad--Bruckstein, Hillar--Sommer, and Garfinkle--Hillar, but they are not the full state of polynomial identifiability. |
| Efficient-algorithm survey, line 321 | `correct-with-gaps` | Spielman, Sun--Qu--Wright, Arora/Agarwal, Barak et al., and Novikov--White support the broad regimes stated. “Every” result having independent feature supports is too broad, and Awasthi--Vijayaraghavan explicitly treats largely arbitrary supports plus a small random portion. |
| Penalized-estimator survey, line 323 | `correct-with-gaps` | Gribonval--Jenatton--Bach is a local-minimum result and Hu/Sun use a different volume criterion. The blanket global-frontier sentence needs reconciliation with Tang et al.'s claimed global solution-set theorem. |
| Interpretability survey, line 325 | `correct-with-gaps` | Most attributions match the cited abstracts/results. It omits direct 2026 splitting/amortization work and overstates Matryoshka as “the standard” remedy. |
| Frame-potential claim, lines 284 and 309 | `correct` | Unit-norm tight frames are exactly the global minimizers of the frame potential for \(m\ge n\). |
| Piecewise-polynomial loss claim, line 295 | `flawed` | Parametric integration across moving ReLU breakpoints introduces denominators; it is generally piecewise rational/semialgebraic. |

## Per-item precision and openness

| Numbered item | Precision | Openness verdict | Reason |
|---|---|---|---|
| Problem 4.3 | `ill-posed` | `open-with-related-work` | The listed summaries do not determine pair identities or full geometry; no exact repaired characterization was found. Tang 2026, Dorrell 2026, and current SAE identifiability work overlap. |
| Conjecture 4.4 | `well-posed` | `resolved` | Resolved negatively by the explicit \(m=2,p=1\) orthogonal counterexample above. |
| Conjecture 4.5 | `well-posed` | `resolved` | Resolved positively by the radial lower bound, with \(\lambda_0=1,C=0\). |
| Problem 4.6 | `minor-issues` | `open-with-related-work` | Ambient dimension is omitted from the answer's parameter list. Dalili--Mahdavi directly proves objective-driven multidimensional feature splitting, but not this exact two-cap phase diagram. |
| Problem 4.7 | `minor-issues` | `possibly-resolved` | The quantifier over \(n\) and intended overcomplete regime are unclear; polynomial identifiability/recovery results cover important allowed regimes, including log sparsity. |
| Problem 4.8 | `minor-issues` | `open-with-related-work` | Projected limits under nonattainment need definition. ICLR 2026 directly studies dictionary distortion from amortization, but the exact global-minimizer separation was not found. |
| Conjecture 4.9 | `well-posed` | `open-with-related-work` | Critical-point/tight-frame and large-size results overlap; no global pentagon theorem was found. |
| Problem 5.1 | `well-posed` | `open-with-related-work` | The \(b=0\) face is exactly solved above; Dorrell and Chanin give local/two-feature analyses, but no complete five-parameter global diagram was found. |
| Problem 5.2 | `well-posed` | `open-with-related-work` | No source proving global one-active-feature pentagon optimality was found; Chen et al. proves regular polygons are critical, not globally minimal. |
| Problem 5.3 | `ill-posed` | `open-with-related-work` | The experiment is not reproducibly specified and overlaps existing hierarchical synthetic/ground-truth SAE benchmarks. |

## Per-item search-query log

Searches were run on 2026-07-15. The strings below are literal queries. Each item deliberately used mathematical, arXiv, ML-venue/OpenReview, and Alignment Forum vocabularies; 2024--2026 was included explicitly.

### Problem 4.3

- `2024 2025 2026 global minimizers reconstruction l1 dictionary learning correlated supports identifiability merging sparse autoencoder`
- `site:arxiv.org sparse autoencoder global optimum feature recovery correlated supports dictionary learning 2024 2025 2026`
- `site:openreview.net sparse autoencoder theory global minima dictionary learning feature recovery absorption`
- `site:alignmentforum.org sparse autoencoder identifiability dictionary learning absorption open problem`

Evidence: [Tang et al. 2026](https://arxiv.org/abs/2512.05534) claims a unified global-solution/nonidentifiability framework; [Dorrell 2026](https://arxiv.org/abs/2606.02385) gives local optimality constraints; [Toward Identifiable SAEs, ICML 2026](https://openreview.net/forum?id=miLK9YcxtA) studies instability/near-identifiability. None supplies the requested repaired full characterization.

### Conjecture 4.4

- `2024 2025 2026 global feature recovery sparse autoencoder independent Bernoulli supports nonnegative l1 population objective`
- `site:arxiv.org "feature recovery" "sparse autoencoder" independent supports theorem global minimizer`
- `site:openreview.net sparse autoencoder provable recovery independent support dictionary global optimum 2025 2026`
- `site:alignmentforum.org sparse autoencoder feature recovery theorem independent supports`

Evidence: [Chen et al.](https://arxiv.org/abs/2506.14002) proves recovery for a modified bias-adaptation algorithm, not this objective; [Cui et al., ICLR 2026](https://openreview.net/pdf?id=DSOTgzeH3w) proves strong limits of standard SAEs; [Tang et al.](https://arxiv.org/abs/2512.05534) is adjacent. The conjecture is independently refuted above.

### Conjecture 4.5

- `2024 2025 2026 sparse autoencoder nested supports hierarchical features absorption positive l1 penalty global minima two feature`
- `site:arxiv.org sparse dictionary learning nested support feature absorption two-feature l1 global optimum`
- `site:openreview.net hierarchical activation patterns sparse autoencoder absorption theory global minimum 2025 2026`
- `site:alignmentforum.org feature absorption nested hierarchical sparse autoencoder theory`

Evidence: [Chanin et al.](https://arxiv.org/abs/2409.14507), [Matryoshka SAEs](https://proceedings.mlr.press/v267/bussmann25a.html), [Tang et al.](https://arxiv.org/abs/2512.05534), and [Dorrell](https://arxiv.org/abs/2606.02385) overlap absorption/hierarchy, but the stated conjecture is resolved more directly by the radial bound above.

### Problem 4.6

- `2024 2025 2026 sparse autoencoder feature splitting quantization spherical cap dictionary learning measure global minimizer`
- `site:arxiv.org sparse autoencoder feature splitting theory quantization manifold dictionary atoms 2025 2026`
- `site:openreview.net sparse autoencoder "feature splitting" theory geometry dictionary size 2024 2025 2026`
- `site:alignmentforum.org sparse autoencoder feature splitting quantization dictionary width`

Evidence: [Dalili--Mahdavi 2026](https://arxiv.org/abs/2606.06333) is substantial direct overlap; [Matryoshka SAEs](https://proceedings.mlr.press/v267/bussmann25a.html), [Interpretability as Compression](https://openreview.net/forum?id=OvmW8HnGzK), and Alignment Forum discussions document width-driven splitting.

### Problem 4.7

- `2024 2025 2026 polynomial sample complexity global uniqueness dictionary learning growing sparsity k log m arbitrary competing dictionary`
- `site:arxiv.org dictionary learning "polynomial" samples "growing" sparsity uniqueness identifiability 2024 2025 2026`
- `site:openreview.net dictionary learning global identifiability sample complexity sparse codes 2025 2026`
- `site:alignmentforum.org dictionary learning sample complexity uniqueness sparse autoencoder theory`

Follow-up queries used to check the older candidate resolution:

- `"Towards Learning Sparsely Used Dictionaries with Arbitrary Supports" theorem information theoretically recovered polynomial samples almost linear sparsity`
- `"minimal set of conditions on the supports" dictionary polynomial samples almost linear sparsity uniqueness`
- `site:arxiv.org/abs/1804.08603 uniqueness dictionary learning arbitrary supports polynomial samples theorem`
- `site:proceedings.mlr.press "Towards Learning Sparsely Used Dictionaries with Arbitrary Supports"`

Evidence: [Awasthi--Vijayaraghavan](https://arxiv.org/abs/1804.08603) explicitly proves polynomial identifiability for near-linear sparsity under RIP/triple-occurrence assumptions; [Spielman--Wang--Wright](https://proceedings.mlr.press/v23/spielman12.html) covers arbitrary square dictionaries. [Sun--Huang, ICLR 2025](https://proceedings.iclr.cc/paper_files/paper/2025/hash/84409c45a0defe347c895b004b1c675b-Abstract-Conference.html) is related global identifiability for a different criterion.

### Problem 4.8

- `2024 2025 2026 sparse autoencoder dictionary-level amortization gap optimal dictionary encoder changes global minimizer`
- `site:arxiv.org "amortization gap" sparse autoencoder dictionary global minimizer 2024 2025 2026`
- `site:openreview.net sparse autoencoder amortisation gap dictionary learning encoder global optimum 2025 2026`
- `site:alignmentforum.org sparse autoencoder amortization gap encoder dictionary`

Evidence: [O'Neill--Gumran--Klindt, ICML 2025](https://proceedings.mlr.press/v267/o-neill25a.html) proves code-level insufficiency; [Sun--Wang--Hu, ICLR 2026](https://openreview.net/forum?id=33wY6AI13k) studies the induced feature/dictionary pathologies and compares amortization levels. The exact global-population question remains open.

### Conjecture 4.9

- `2024 2025 2026 toy model superposition regular pentagon global minimizer ReLU tied autoencoder theorem`
- `site:arxiv.org toy models superposition pentagon global minima geometry 2024 2025 2026`
- `site:openreview.net superposition regular polygon pentagon global minimum toy model ReLU`
- `site:alignmentforum.org toy model superposition pentagon geometry proof`

Follow-up geometry queries:

- `"Spectral superposition: a theory of feature geometry" pentagon global minimizer`
- `arXiv 2602.02224 pentagon regular polygon tight frame theorem`
- `"regular pentagon" "Toy Models of Superposition" proof global`
- `2026 "one-active-feature" pentagon ReLU autoencoder`

Evidence: [Chen et al.](https://arxiv.org/abs/2310.06301) proves regular polygons are critical; [Ivanov et al.](https://arxiv.org/abs/2602.02224) derives tight frames under capacity saturation; [Cowsik--Dolev--Infanger](https://openreview.net/forum?id=rapXZIfwbX) treats a large-size limit. No global \(n=2,m=5\) theorem was found.

### Problem 5.1

- `2024 2025 2026 exact two feature sparse autoencoder phase diagram l1 nonnegative dictionary learning absorption global optimum`
- `site:arxiv.org two-feature sparse autoencoder absorption exact phase diagram positive lambda dictionary learning`
- `site:openreview.net two feature hierarchical sparse autoencoder analytic phase diagram absorption local global optimum`
- `site:alignmentforum.org two feature absorption sparse autoencoder analytic model phase diagram`

Evidence: [Chanin et al.](https://arxiv.org/abs/2409.14507) and [Dorrell](https://arxiv.org/abs/2606.02385) are the closest local/two-feature analyses found. The nested \(b=0\) face is solved by Finding 2; the complete diagram was not found.

### Problem 5.2

- `2024 2025 2026 one-sparse input ReLU autoencoder regular pentagon global minimizer theorem`
- `site:arxiv.org one-active-feature toy model superposition regular pentagon loss global optimum`
- `site:openreview.net toy superposition one sparse feature pentagon minimizer 2025 2026`
- `site:alignmentforum.org one active feature pentagon toy model superposition`

Evidence: searches returned [Chen et al.](https://arxiv.org/abs/2310.06301), [Toy Models of Superposition](https://arxiv.org/abs/2209.10652), and Alignment Forum discussions, but no global-minimizer proof.

### Problem 5.3

- `2024 2025 2026 sparse autoencoder empirical phase diagram correlated nested support recovery merge split synthetic dictionary n=64 m=256`
- `site:arxiv.org sparse autoencoder phase diagram feature absorption splitting synthetic ground truth correlations 2025 2026`
- `site:openreview.net sparse autoencoder benchmark phase diagram correlated features absorption recovery synthetic`
- `site:alignmentforum.org SAE absorption phase diagram correlated nested features experiment`

Evidence: [Matryoshka SAEs](https://proceedings.mlr.press/v267/bussmann25a.html) already runs a child-implies-parent synthetic hierarchy; [Sanity Checks for SAEs](https://openreview.net/forum?id=bEYHoD7fCj) uses known ground-truth recovery; [SAEBench](https://openreview.net/pdf/6eb2daa918eb7793e8ccc27253fd57a86a6fc6c5.pdf) includes absorption/disentanglement metrics. None exactly duplicates the proposed grid, but the task requires a reproducible protocol and a narrower novelty claim.

## Machine-readable verdict

```json
{
  "file": "superposition-geometry.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Proposition 2.3",
      "verdict": "correct",
      "note": "The exponential almost-orthogonal packing bound is correct; Johnson--Lindenstrauss is an indirect rather than ideal citation."
    },
    {
      "label": "Theorem 2.4",
      "verdict": "correct",
      "note": "The Welch bound and equiangular-tight-frame equality description are correct."
    },
    {
      "label": "Theorem 2.5",
      "verdict": "correct",
      "note": "The sharp RIP threshold and Gaussian measurement order are correct with standard fixed-distortion high-probability constants."
    },
    {
      "label": "Proposition 3.1",
      "verdict": "correct",
      "note": "The triangle-inequality lower bound, equality characterization, uniqueness, and cost comparison are valid under the stated special model."
    },
    {
      "label": "Proposition 3.2",
      "verdict": "correct",
      "note": "The cone parametrization, Cramer's-rule coefficient sum, derivative signs, and strict boundary minimizer are correct."
    }
  ],
  "items": [
    {
      "label": "Problem 4.3",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2512.05534",
        "https://arxiv.org/abs/2606.02385"
      ],
      "note": "The listed scalar summaries cannot determine which labeled pairs merge; a repaired full-law/full-Gram characterization remains open."
    },
    {
      "label": "Conjecture 4.4",
      "precision": "well-posed",
      "openness": "resolved",
      "citations": [],
      "note": "False: m=2, p=1, an orthogonal true dictionary, and the two inward-slanted atoms give a constant population-cost gap while satisfying both hypotheses for large n."
    },
    {
      "label": "Conjecture 4.5",
      "precision": "well-posed",
      "openness": "resolved",
      "citations": [],
      "note": "True by a pointwise radial lasso lower bound, with the stronger constants lambda_0=1 and C=0."
    },
    {
      "label": "Problem 4.6",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2606.06333"
      ],
      "note": "Ambient dimension is omitted from the requested parameter dependence; a June 2026 paper directly proves objective-driven splitting for multidimensional features."
    },
    {
      "label": "Problem 4.7",
      "precision": "minor-issues",
      "openness": "possibly-resolved",
      "citations": [
        "https://proceedings.mlr.press/v23/spielman12.html",
        "https://arxiv.org/abs/1804.08603"
      ],
      "note": "Polynomial uniqueness and identifiability results cover important allowed regimes, including logarithmic sparsity; the intended quantifier over n and overcompleteness must be clarified."
    },
    {
      "label": "Problem 4.8",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.mlr.press/v267/o-neill25a.html",
        "https://openreview.net/forum?id=33wY6AI13k"
      ],
      "note": "The exact global-minimizer comparison was not found, but dictionary-level effects of amortization were directly studied at ICLR 2026; the nonattainment fallback needs projected-limit definitions."
    },
    {
      "label": "Conjecture 4.9",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2310.06301",
        "https://arxiv.org/abs/2602.02224",
        "https://openreview.net/forum?id=rapXZIfwbX"
      ],
      "note": "Critical-point, tight-frame, and large-size results do not establish finite global pentagon optimality."
    },
    {
      "label": "Problem 5.1",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2409.14507",
        "https://arxiv.org/abs/2606.02385"
      ],
      "note": "The full five-parameter global diagram remains open, but its b=0 face is exactly solved by the radial argument proving Conjecture 4.5."
    },
    {
      "label": "Problem 5.2",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2310.06301",
        "https://arxiv.org/abs/2602.02224"
      ],
      "note": "No global one-active-feature pentagon theorem was found; known work gives criticality or conditional tight-frame structure."
    },
    {
      "label": "Problem 5.3",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.mlr.press/v267/bussmann25a.html",
        "https://openreview.net/forum?id=bEYHoD7fCj"
      ],
      "note": "The empirical protocol leaves essential distributions, tolerances, grids, optimization, seeds, and uncertainty unspecified and overlaps existing hierarchical synthetic benchmarks."
    }
  ],
  "attribution_issues": [
    "Lines 132 and 275 incorrectly attribute an arbitrary learned ReLU encoder to one ISTA step; this requires decoder-tied weights and a fixed threshold bias.",
    "Line 252 omits Dalili--Mahdavi 2026, which directly proves multidimensional-feature splitting under an l1-regularized SAE objective.",
    "Line 262 omits Spielman--Wang--Wright and Awasthi--Vijayaraghavan polynomial uniqueness/identifiability results relevant to growing sparsity.",
    "Line 275 says dictionary-level amortization remains unexamined despite the ICLR 2026 paper The Price of Amortized Inference in Sparse Autoencoders.",
    "Line 323's no-global-minimizer-theorem claim requires reconciliation with the cited Tang et al. paper's explicit global-solution-set claim.",
    "The O'Neill--Gumran--Klindt bibliography should record its ICML 2025 publication rather than only the 2024 arXiv posting."
  ],
  "confidence": "high"
}
```
