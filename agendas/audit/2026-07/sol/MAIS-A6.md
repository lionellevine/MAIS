> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A6](../../../A6/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Audit of `learning-coefficients-real-architectures.tex`

## Summary verdict

This file has significant mathematical and openness issues despite several careful and correct elementary proofs. Most importantly, Problem 5.2 is completely solvable by an exact reduction of uniform-truth attention to the already cited reduced-rank-regression model, and Question 9.1 is affirmative by a finite activation-cell decomposition; both are therefore incorrectly advertised as open. Problem 6.1(a), and the convergence plus leading fluctuations requested in the first half of Problem 6.2, are direct applications of Watanabe's published WBIC theorem rather than missing adaptations. The Aoyagi--Watanabe formula itself is transcribed correctly, but Theorem 3.1 omits the parameter-domain/prior-support condition needed to make it the global coefficient, and the preceding description of a multiplication fiber as a determinantal variety “singular exactly where the factorization drops rank” is false. The Fourier construction, RLCT calculus lemma, Gaussian assumptions, width lower bound, Proposition 4.6, and the submersion argument in Remark 4.8 check out. The file should not be published with the blanket claim at line 58 that every numbered item is open.

## Findings, ordered by severity

### 1. Problem 5.2 is resolved exactly, including the supposedly unknown five-parameter case

**Location:** lines 363--373, especially Problem 5.2 at lines 365--371; repeated claims at lines 437, 447, and 473.

Let
\[
P=I_v-\frac1v\mathbf 1\mathbf 1^{\mathsf T}
\]
be output centering. An output softmax is uniform exactly when its logit row times \(P\) is zero. Constant-token contexts \(x=(a,\ldots,a)\) have
\[
\ell(x)P=E_aUP,
\]
independently of \(Q\), \(T\), and the attention weights. Consequently uniform output for every context implies \(EUP=0\). Conversely, if \(EUP=0\), every attention-weighted convex combination in line 352 has centered logit zero, so every output is uniform. Thus
\[
W_0=\{(E,Q,U):EUP=0\}
\]
exactly; attention proper is not a higher-order correction to the zero-set geometry.

On every bounded neighborhood, categorical KL from the uniform distribution is two-sided comparable to squared centered-logit norm. Constant contexts give the lower bound and convexity of squared norm gives the upper bound, hence
\[
K(E,Q,U)\asymp \|EUP\|_F^2.
\]
Choose an orthonormal \(C\in\mathbb R^{v\times(v-1)}\) spanning \(\mathbf1^\perp\), and put \(\bar U=UC\). Flat \(Q\)-coordinates and the flat all-ones output direction in \(U\) do not change an RLCT. The problem is therefore precisely reduced-rank regression at zero truth with
\[
(M,N,H,r)=(v,v-1,e,0).
\]
Substitution in the file's own Theorem 3.1 gives, for every \(R>0\), the local pair at zero and the minimum over \(W_0\cap\bar B_R\):
\[
(\lambda,m)=
\begin{cases}
\left(\dfrac{2e(2v-1)-1-e^2}{8},1\right),&e\le 2v-1\text{ and }e\text{ odd},\\[6pt]
\left(\dfrac{2e(2v-1)-e^2}{8},2\right),&e\le 2v-1\text{ and }e\text{ even},\\[6pt]
\left(\dfrac{v(v-1)}2,1\right),&e>2v-1.
\end{cases}
\]
In particular, the case \((v,T,e)=(2,2,1)\) highlighted at line 437 is \((\lambda,m)=(1/2,1)\). The primary reduced-rank source is [Aoyagi--Watanabe (2005)](https://www.sciencedirect.com/science/article/abs/pii/S0893608005000559). Current attention/LLC work such as the [ICLR 2025 refined-LLC paper](https://openreview.net/forum?id=SUc1UOWndp) is empirical and does not supersede this calculation; it does show that the literature search must include current ML venues.

### 2. Question 9.1 is affirmative for the finite-input ReLU model actually stated

**Location:** lines 459--465.

The question does not require a general theory for arbitrary ReLU models. Here there are only \(p^2\) inputs and finitely many hidden units. Parameter space therefore has a finite semialgebraic partition by the signs of all hidden preactivations on all inputs. On each full-dimensional activation cell, every ReLU is either its linear argument or zero, so the Gaussian regression model and its population loss agree with an analytic (indeed polynomial) branch on that cell. Apply the standard analytic singular-learning/zeta argument on each compact semianalytic cell (semianalytic boundary conditions are handled in the same resolution). Cells whose closure contains no exact fit are exponentially negligible. The total evidence is a finite sum of positive branch evidences, so the smallest branch RLCT dominates and, among ties, the largest pole order dominates. The weighted sublevel volume is the same finite sum of branch volumes and has exactly the same minimum exponent and maximum logarithmic power. Hence the answer to Question 9.1 is **yes**, with \((\lambda,m)=(\lambda_{\rm vol},m_{\rm vol})\).

This finite-cell proof does not settle continuous-input or unbounded-architecture ReLU theory, for which [Nagayasu--Watanabe](https://arxiv.org/abs/2303.15739) only gives bounds. It does settle the numbered finite-input question.

There is also an attribution error in line 459. The cited [Lion--Rolin 1997 paper](https://aif.centre-mersenne.org/item/AIF_1997__47_3_859_0/) is a preparation/quantifier-elimination paper. The directly relevant integration-and-volume theorem is [Lion--Rolin 1998](https://eudml.org/doc/75301), and it concerns globally subanalytic families/subanalytic integrands. It does not imply that a volume weighted by an **arbitrary** smooth positive prior is definable in a log-exponential structure. Smooth positivity preserves the leading RLCT pair here by resolution/comparison, not by the claimed definability statement.

### 3. Problem 6.1(a) and much of Problem 6.2 are already Watanabe's WBIC theorem

**Location:** lines 397--430, especially lines 417, 422, and 427.

For every fixed \(\gamma>0\), the factor \(\exp(-\gamma\|w-w^*\|^2/2)\) is simply a fixed smooth positive prior on the compact ball. [Watanabe's 2013 WBIC theorem](https://jmlr.org/papers/v14/watanabe13a.html), Theorem 4 in the paper, applies without an adaptation. With \(\beta_0=1\), it gives
\[
\mathbb E^\beta[nL_n(w)]
=nL_n(w^*)+\lambda\log n+U_n\sqrt{\lambda\log n/2}+O_p(1).
\]
The toy model's global minimum is \(\lambda=1/4\), so division by \(\log n\) proves Problem 6.1(a) immediately. Part (b), where the prior itself varies with \(n\), remains a genuine asymptotic competition problem.

For Problem 6.2, restricting to a sufficiently small hard ball makes that ball the compact parameter domain. The same theorem gives convergence to the ball's RLCT, which is the local coefficient by Definition 2.5, and gives the leading \(1/\sqrt{\log n}\) fluctuation term (with the theorem's \(U_n\), asymptotically Gaussian, subject to its possible parity degeneration). What remains open is the requested classification of factorization points attaining the global Aoyagi--Watanabe minimum and any finer fluctuation refinement. Recent relevant work includes [Kurumadani's local RLCT formulas](https://arxiv.org/abs/2408.13030), [geometry of multiplication fibers](https://arxiv.org/abs/2411.19920), and the [2025 local-posterior-sampling benchmark](https://arxiv.org/abs/2507.21449).

### 4. Theorem 3.1 lacks the domain/prior hypothesis that makes its formula global, and line 158 misdescribes the fiber

**Location:** lines 153--180.

The four-case Aoyagi--Watanabe formula and parity are transcribed correctly from the [primary paper](https://www.sciencedirect.com/science/article/abs/pii/S0893608005000559). As written, however, “for reduced-rank regression as above” inherits no specified compact \(W\) or prior support. A global RLCT depends on which parts of the fiber the parameter domain meets. The formula is valid when the positive prior/domain contains a factorization attaining the global minimum. It need not hold on an arbitrary sufficiently small compact neighborhood of another exact factorization. The file itself supplies the counterexample at line 427: for \(M=N=H=2,r=0\), a small neighborhood of \((A,B)=(I_2,0)\) has local coefficient \(2\), whereas the table gives \(3/2\). Thus Theorem 3.1 is `correct-with-gaps`, not an unconditional theorem about any \(W\) allowed by Section 2.

Line 158 is also false as stated. The set \(\{(A,B):BA=C\}\) is a fiber of a matrix-multiplication map, not in general “a determinantal variety,” and it is not singular exactly when one factor drops rank. In the preceding \(C=0\) example, \(A=I_2\) is invertible, so locally the equation \(BA=0\) is equivalent to \(B=0\); the fiber is smooth there even though \(B\) has rank zero. Current papers explicitly study these sets as multiplication fibers with rank stratifications: [Pepin Lehalleur--Rimányi (2024)](https://arxiv.org/abs/2411.19920) and [Shewchuk--Bhattacharya (2024)](https://arxiv.org/abs/2404.14855).

### 5. Problem 4.10 already has finite-\(\beta\) local invariance, and its global \(\beta\to\infty\) clause is ambiguous

**Location:** lines 329--335.

For finite \(\beta>0\), KL between two softmax distributions is locally comparable to squared distance between their centered logits. Under the analytic coordinate change \(V=\beta\widetilde V\), a neighborhood of the scaled Fourier point maps to a neighborhood of the \(\beta=1\) Fourier point, and
\[
K_\beta(u,\beta\widetilde V)\asymp
\beta^2\bigl\|P(f_{u,\widetilde V}-\delta)\bigr\|^2
\asymp K_1(u,\widetilde V).
\]
Therefore the local coefficient and multiplicity at the scaled Fourier point are constant for all finite \(\beta\). Their numerical value remains open, as does the global minimum.

The last sentence is not fully well-posed for that global minimum. The admissible radius satisfies \(R\ge(1+\beta)R_p\), so \(R\) cannot remain fixed as \(\beta\to\infty\). Taking \(R(\beta)=(1+\beta)R_p\), \(R(\beta)=\beta^2R_p\), or an unrestricted-domain limit are inequivalent questions and can include different zero-set strata. This is a precision issue, not merely exposition.

### 6. The 2024--2026 related-work account is incomplete but does not otherwise resolve the modular or generic-teacher items

**Location:** lines 263--264, 282, 327, and 445--451.

The modular-addition items remain open in their exact RLCT form, but there is material current overlap: Tian's preprint cited at line 264 is now a [NeurIPS 2025 paper](https://openreview.net/pdf?id=tD7MLq0dbZ); [Morwani et al. (ICLR 2024)](https://openreview.net/forum?id=i9wDX850jR) proves single-frequency structure under margin maximization; [McCracken et al. (NeurIPS 2025)](https://proceedings.neurips.cc/paper_files/paper/2025/hash/3edb234091dca2023308398dbf824850-Abstract-Conference.html) gives a different abstract-algorithm account; and [He et al. (February 2026)](https://arxiv.org/abs/2602.16849) studies Fourier diversification and grokking dynamics. None computes the singular local coefficients requested here, but the last two are absent from the “what is known” discussion.

For attention, the [ICLR 2025 refined-LLC study](https://openreview.net/forum?id=SUc1UOWndp) estimates componentwise coefficients but does not give exact RLCTs. For linear attention, [Yoshida--Watanabe's tensor-decomposition RLCT bounds](https://arxiv.org/abs/2303.05731) are adjacent rather than a solution. Generic-constancy results for algebraic families support Conjecture 5.3 in spirit, while [semi-regular](https://arxiv.org/abs/2406.02646) and [non-singular-point](https://arxiv.org/abs/2408.13030) formulas do not cover this attention family.

### 7. Two background statements need small qualifications

**Location:** lines 81--103.

“Neural networks are never regular” at line 81 is false literally: a one-parameter linear neuron with fixed nonzero input and Gaussian output is an identifiable regular statistical model. The intended statement about commonly overparameterized networks is defensible, but the universal claim is not.

Theorems 2.1 and 2.2 omit a nontriviality hypothesis such as \(K\not\equiv0\). Their listed assumptions allow a constant model equal to the truth, in which case the free energy has no positive logarithmic coefficient and the zeta function has no largest negative pole. With that routine exclusion, the stated realizable \(\beta=1\) free-energy and expected-generalization formulas are correct.

## Proof and background-claim ledger

| Result or claim | Verdict | Audit note |
|---|---|---|
| Theorem 2.1 (Watanabe), lines 83--89 | `correct-with-gaps` | Correct in the intended nontrivial realizable analytic setting; add \(K\not\equiv0\). |
| Theorem 2.2 (zeta continuation), lines 101--103 | `correct-with-gaps` | Correct under the same nontriviality qualification; otherwise there is no largest pole. |
| Resolution/volume claims, lines 105--121 | `correct` | Normal-crossing ratios, pole order, and leading sublevel-volume form agree with the standard theory. |
| Example 2.3, lines 123--128 | `correct` | All three pairs and the general \(r/(2k)\) computation check. |
| Lemma 2.4, lines 132--139 | `correct` | Sum, product, equal-threshold multiplicity, and comparability rules are correct for separate variables. |
| Definition 2.5 and lower semicontinuity, lines 145--149 | `correct` | The direction of semicontinuity and compact-minimum argument are correct. |
| Theorem 3.1, lines 160--178 | `correct-with-gaps` | Formula correct; global claim needs domain/prior support containing a minimizing factorization. |
| Multiplication-fiber geometry, line 158 | `flawed` | Not generally a determinantal variety; rank drop is not equivalent to a singular point. |
| Gaussian relative-variance check, lines 208--210 | `correct` | For mean error \(d\), \(\mathbb E[f^2]=\|d\|^2+\|d\|^4/4\); boundedness gives the global condition. |
| Lemma 4.2, lines 216--253 | `correct` | Both trigonometric identities, Fourier inversion signs, constant column, and padding check. |
| Minimal-width lower bound, line 257 | `correct` | Subtracting the row/column additive part lowers rank by at most two, so \(H\ge p-2\). |
| Proposition 4.6(i), lines 296--303 | `correct` | The sublevel inclusion is scaled correctly; \(P\asymp|\bar u|^4\) in codimension \(2p-1\), giving \((2p-1)/4\). |
| Proposition 4.6(ii), lines 305--306 | `correct` | The \(3p-2\) independent orbit directions and tubular-volume upper bound on \(\lambda\) are valid. |
| Remark 4.8, lines 317--319 | `correct` | Polarization makes the squares span all \(p^2\) input functions; generic tiny units give a submersion and \((p^3/2,1)\). |
| Softmax realizability/analyticity, line 329 | `correct` | Scaling \(V\) realizes the smoothed truth; finite-\(\beta\) KL is analytic. |
| Attention finite-variance condition, lines 357--359 | `correct` | On a compact parameter ball all categorical probabilities are uniformly positive, yielding quadratic comparability. |
| Attention Taylor degrees, line 373 | `correct but misleading` | Scores begin in degree 3 and attention corrections in degree 5, but exact centering makes them irrelevant at uniform truth. |
| Linear-attention degree count, lines 385--390 | `correct` | Logits have multidegree \((3,1,1)\), total degree 5; squared Gaussian loss has degree 10. |
| Toy local coefficients, lines 411--415 | `correct` | Smooth line points have \(1/2\); at the origin \(K\asymp(w_1^2+w_2^2)^4\), giving \(1/4\). |
| ReLU realization, lines 461--462 | `correct` | The displayed unit is exactly an input-pair indicator; \(p^2\) output-labelled units realize the table. |

## Per-item precision and openness

| Numbered item | Precision | Openness verdict | Reason |
|---|---|---|---|
| Question 4.3 | `well-posed` | `open-with-related-work` | Exact minimal width for this constrained square-unit architecture was not found; tensor-rank and new exact-solution work are relevant. |
| Problem 4.5 | `minor-issues` | `open-with-related-work` | “The multiplicity at the minimizing points” could mean the list of pointwise multiplicities or their maximum/global pole order. Cullen 2026 covers nondegenerate points, not these singular minima. |
| Conjecture 4.7 | `well-posed` | `open-with-related-work` | No equality/counterexample for a padded dead unit was found. |
| Conjecture 4.9 | `well-posed` | `open-with-related-work` | Fourier structure is proved for other selection principles, not for RLCT minimizers. |
| Problem 4.10 | `minor-issues` | `open-with-related-work` | The local pair is finite-\(\beta\) invariant, but not computed; the global \(\beta\to\infty\) question lacks a choice of \(R(\beta)\). |
| Problem 5.2 | `well-posed` | `resolved` | Exact reduction to \(\|EUP\|_F^2\) gives the closed formula above and no \(T\) or \(R\) dependence. |
| Conjecture 5.3 | `well-posed` | `open-with-related-work` | Generic LCT constancy is known in algebraic settings, but no theorem found covers this real-analytic teacher-dependent KL germ and its real multiplicity. |
| Problem 5.4 | `well-posed` | `open-with-related-work` | Current attention LLC work is empirical; no exact generic-teacher value was found. |
| Problem 5.5 | `well-posed` | `open-with-related-work` | Tensor-decomposition RLCT bounds overlap the multilinear structure but do not compute this context-indexed polynomial. |
| Problem 6.1 | `well-posed` | `open-with-related-work` | Part (a) is a direct WBIC corollary; the varying-\(\gamma_n\) regimes and transition remain open. |
| Problem 6.2 | `minor-issues` | `open-with-related-work` | The underlying compact domain/prior is not explicit. Convergence and leading WBIC fluctuations are known; classification of factorization strata remains open. |
| Question 9.1 | `well-posed` | `resolved` | Finite activation-cell decomposition reduces the stated model to a finite sum of analytic branch models. |

## Per-item search-query log

Searches were run on 2026-07-14. The strings below are literal queries; repeated vocabulary was intentional to cross arXiv, published venues, OpenReview/ML venues, and general web/Scholar indexing.

### Question 4.3

- `minimal width quadratic neural network modular addition exact representation tensor rank 2024 2025 2026`
- `site:arxiv.org modular addition quadratic network exact solutions width Fourier neurons learning coefficient`
- `"Composing global solutions to reasoning tasks" modular addition quadratic zero mean exact solutions`
- `site:openreview.net modular addition quadratic network tensor rank exact representation`

Evidence found: [Tian/CoGS, NeurIPS 2025](https://openreview.net/pdf?id=tD7MLq0dbZ), [He et al. 2026](https://arxiv.org/abs/2602.16849), and [McCracken et al., NeurIPS 2025](https://proceedings.neurips.cc/paper_files/paper/2025/hash/3edb234091dca2023308398dbf824850-Abstract-Conference.html); none determines \(H_{\min}(p)\) for the stated architecture.

### Problem 4.5

- `"learning coefficient" modular addition quadratic neural network Fourier solution RLCT`
- `"A basin-selection perspective on grokking via singular learning theory"`
- `site:arxiv.org 2025 2026 RLCT modular arithmetic neural network`
- `site:openreview.net singular learning theory grokking modular addition learning coefficient`

Evidence found: [Cullen et al. 2026](https://arxiv.org/abs/2603.01192) treats explicitly nondegenerate basins; [Tian/CoGS](https://openreview.net/pdf?id=tD7MLq0dbZ) treats exact-solution algebra, not RLCTs at the Fourier/dead-unit strata.

### Conjecture 4.7

- `2024 2025 2026 minimal hidden width exact modular addition quadratic activation squared loss one hot`
- `2026 marginal cost width local learning coefficient dead neuron quadratic network RLCT`
- `site:openreview.net modular addition quadratic activation exact width global solutions 2025`
- `site:proceedings.neurips.cc modular addition quadratic network global solution width`

Evidence found: the same Cullen and Tian papers overlap the architecture, but no equality for the padded local coefficient was found.

### Conjecture 4.9

- `2025 2026 modular addition single-frequency neurons theorem quadratic activation exact solutions Fourier`
- `site:proceedings.neurips.cc 2025 modular addition Fourier neurons quadratic activation`
- `site:openreview.net 2026 modular addition Fourier frequency diversification quadratic network`
- `site:arxiv.org 2024 2025 modular addition non-Fourier exact solutions quadratic network`

Evidence found: [Morwani et al., ICLR 2024](https://openreview.net/forum?id=i9wDX850jR), [Tian, NeurIPS 2025](https://openreview.net/pdf?id=tD7MLq0dbZ), [McCracken et al., NeurIPS 2025](https://proceedings.neurips.cc/paper_files/paper/2025/hash/3edb234091dca2023308398dbf824850-Abstract-Conference.html), and [He et al. 2026](https://arxiv.org/abs/2602.16849). They use margin, solution composition, abstract algorithms, or dynamics rather than RLCT minimization.

### Problem 4.10

- `2024 2025 2026 real log canonical threshold softmax cross entropy neural network exact`
- `site:arxiv.org "RLCT" softmax cross-entropy neural network modular addition`
- `site:openreview.net "learning coefficient" softmax cross entropy`
- `multinomial logistic regression real log canonical threshold singular softmax`

No source computing this Fourier-point germ was found. [Kurumadani's semi-regular method](https://arxiv.org/abs/2406.02646) is related but does not cover it. Finite-\(\beta\) invariance follows directly from softmax KL's positive-definite Hessian on centered logits, as above.

### Problem 5.2

- `2024 2025 2026 transformer attention exact real log canonical threshold RLCT`
- `site:arxiv.org/abs attention "real log canonical threshold"`
- `site:openreview.net transformer "local learning coefficient" attention 2025`
- `site:proceedings.mlr.press attention singular learning theory learning coefficient`

The searches found empirical attention LLC work, notably [Wang et al., ICLR 2025](https://openreview.net/forum?id=SUc1UOWndp), but no published exact computation. The problem is nevertheless resolved by the elementary exact reduction to [Aoyagi--Watanabe](https://www.sciencedirect.com/science/article/abs/pii/S0893608005000559).

### Conjecture 5.3

- `RLCT generic constancy analytic family parameter real log canonical threshold constructible`
- `log canonical threshold generic constancy family semicontinuity analytic parameters`
- `site:arxiv.org 2024 2025 learning coefficient generic teacher neural network`
- `site:scholar.google.com "real log canonical threshold" "generic" family`

Evidence found: generic constancy is standard for algebraic families of ideals (an explicit statement appears in [Blum--Jonsson, Proposition 6.1](https://www.sciencedirect.com/science/article/am/pii/S0001870820300888)); [Kurumadani 2024](https://arxiv.org/abs/2408.13030) gives formulas at many non-singular points. Neither directly proves the real-analytic attention assertion, especially its real multiplicity.

### Problem 5.4

- `real log canonical threshold attention transformer learning coefficient exact 2024 2025 2026`
- `site:arxiv.org transformer "local learning coefficient" attention`
- `site:arxiv.org attention model RLCT singular learning theory`
- `site:openreview.net attention "learning coefficient" singular`

Evidence found: [ICLR 2025 refined attention LLCs](https://openreview.net/forum?id=SUc1UOWndp) and later empirical work, but no exact generic teacher calculation.

### Problem 5.5

- `2024 2025 2026 linear attention tensor factorization real log canonical threshold learning coefficient`
- `site:arxiv.org linear attention singular learning theory RLCT`
- `site:openreview.net linear attention "learning coefficient"`
- `tensor decomposition RLCT multilinear map zero truth attention`

Evidence found: [Yoshida--Watanabe](https://arxiv.org/abs/2303.05731) gives tensor-decomposition RLCT upper bounds, and current linear-attention theory studies dynamics rather than this RLCT. No exact formula matching the stated context polynomial was found.

### Problem 6.1

- `Watanabe 2013 WBIC theorem beta 1/log n expectation empirical loss lambda log n JMLR`
- `local learning coefficient estimator Gaussian localization fixed gamma consistency WBIC`
- `site:arxiv.org 2024 2025 2026 local learning coefficient estimator consistency localization gamma`
- `site:openreview.net local learning coefficient estimator localization WBIC`

Evidence found: [Watanabe 2013](https://jmlr.org/papers/v14/watanabe13a.html) resolves fixed \(\gamma\); [Lau et al.](https://arxiv.org/abs/2308.12108) defines the local estimator, and [Hitchcock--Hoogland 2025](https://arxiv.org/abs/2507.21449) benchmarks sampling. No varying-\(\gamma_n\) theorem for this toy competition was found.

### Problem 6.2

- `local RLCT reduced rank regression arbitrary factorization point A B product fiber`
- `"local learning coefficient" reduced rank regression arbitrary point`
- `site:arxiv.org 2024 2025 2026 reduced rank regression local RLCT fiber strata`
- `WBIC hard restriction local ball consistency local learning coefficient`

Evidence found: WBIC gives convergence and leading fluctuations; [Kurumadani 2024](https://arxiv.org/abs/2408.13030) handles many non-singular points, while [Pepin Lehalleur--Rimányi 2024](https://arxiv.org/abs/2411.19920) and [Shewchuk--Bhattacharya 2024](https://arxiv.org/abs/2404.14855) analyze multiplication fibers. No complete pointwise RLCT classification was found.

### Question 9.1

- `Lion Rolin 1997 preparation theorem logarithmico-exponential volume semialgebraic sublevel asymptotic`
- `semialgebraic function sublevel volume asymptotic rational power logarithm o-minimal integration`
- `ReLU semialgebraic Bayesian free energy exact asymptotic RLCT volume exponent 2024 2025 2026`
- `Nagayasu Watanabe deep ReLU Bayesian free energy upper bound exact expansion`
- `"free energy" subanalytic statistical model singular learning theory ReLU exact expansion`
- `Lion Rolin volume subanalytic sets log analytic volume theorem`

Evidence found: [Lion--Rolin 1997](https://aif.centre-mersenne.org/item/AIF_1997__47_3_859_0/), the actually relevant [Lion--Rolin 1998 volume paper](https://eudml.org/doc/75301), and [Nagayasu--Watanabe's ReLU bounds](https://arxiv.org/abs/2303.15739). The numbered finite-input question is resolved by the finite activation-cell reduction above, even though no searched paper states that specialization.

## Machine-readable verdict

```json
{
  "file": "learning-coefficients-real-architectures.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Theorem 2.1",
      "verdict": "correct-with-gaps",
      "note": "Correct in the intended nontrivial realizable analytic setting, but the assumptions permit K identically zero, when no positive lambda exists."
    },
    {
      "label": "Theorem 2.2",
      "verdict": "correct-with-gaps",
      "note": "The zeta statement is correct after the same nontriviality exclusion; for K identically zero there is no largest negative pole."
    },
    {
      "label": "Example 2.3",
      "verdict": "correct",
      "note": "All thresholds and multiplicities, including r/(2k), check."
    },
    {
      "label": "Lemma 2.4",
      "verdict": "correct",
      "note": "The sum, product, multiplicity, and comparability rules are correct for separate variables."
    },
    {
      "label": "Theorem 3.1",
      "verdict": "correct-with-gaps",
      "note": "The Aoyagi-Watanabe case formula is correct, but the global statement needs a parameter-domain/prior-support hypothesis ensuring that an RLCT-minimizing factorization is included."
    },
    {
      "label": "Lemma 4.2",
      "verdict": "correct",
      "note": "The trigonometric identities, Fourier inversion, output coefficients, and padding are correct."
    },
    {
      "label": "Proposition 4.6",
      "verdict": "correct",
      "note": "Both the dead-unit sublevel-volume bound and the scaling/rotation tube bound are valid."
    },
    {
      "label": "Remark 4.8",
      "verdict": "correct",
      "note": "The polarization spanning argument yields a submersion and local pair (p^3/2,1)."
    }
  ],
  "items": [
    {
      "label": "Question 4.3",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/pdf?id=tD7MLq0dbZ",
        "https://arxiv.org/abs/2602.16849",
        "https://proceedings.neurips.cc/paper_files/paper/2025/hash/3edb234091dca2023308398dbf824850-Abstract-Conference.html"
      ],
      "note": "Exact-solution and mechanism papers overlap the problem, but no minimal width for this constrained architecture was found."
    },
    {
      "label": "Problem 4.5",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2603.01192",
        "https://openreview.net/pdf?id=tD7MLq0dbZ"
      ],
      "note": "The requested multiplicity could mean all pointwise multiplicities or their maximum. Existing formulas avoid the Fourier and more singular minimizing strata."
    },
    {
      "label": "Conjecture 4.7",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2603.01192",
        "https://openreview.net/pdf?id=tD7MLq0dbZ"
      ],
      "note": "No equality or counterexample for the padded dead-unit coefficient was found."
    },
    {
      "label": "Conjecture 4.9",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/forum?id=i9wDX850jR",
        "https://openreview.net/pdf?id=tD7MLq0dbZ",
        "https://arxiv.org/abs/2602.16849"
      ],
      "note": "Single-frequency structure and related mechanisms are known under other selection principles, not RLCT minimization."
    },
    {
      "label": "Problem 4.10",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2406.02646"
      ],
      "note": "The local pair is constant for every finite beta by centered-logit equivalence and output scaling, but its value is open. The global beta-to-infinity clause must specify R(beta)."
    },
    {
      "label": "Problem 5.2",
      "precision": "well-posed",
      "openness": "resolved",
      "citations": [
        "https://www.sciencedirect.com/science/article/abs/pii/S0893608005000559",
        "https://openreview.net/forum?id=SUc1UOWndp"
      ],
      "note": "Uniform output is equivalent to EUP=0 and K is comparable to ||EUP||_F^2. Aoyagi-Watanabe with (M,N,H,r)=(v,v-1,e,0) gives the full formula, independent of T and R."
    },
    {
      "label": "Conjecture 5.3",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://www.sciencedirect.com/science/article/am/pii/S0001870820300888",
        "https://arxiv.org/abs/2408.13030",
        "https://arxiv.org/abs/2406.02646"
      ],
      "note": "Generic constancy exists for algebraic families, but no result found establishes the stated real-analytic attention pair and multiplicity."
    },
    {
      "label": "Problem 5.4",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/forum?id=SUc1UOWndp"
      ],
      "note": "Current attention LLC work is empirical and does not compute the exact generic-teacher RLCT."
    },
    {
      "label": "Problem 5.5",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2303.05731"
      ],
      "note": "Tensor-decomposition RLCT bounds are adjacent, but no exact value for this linear-attention polynomial was found."
    },
    {
      "label": "Problem 6.1",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://jmlr.org/papers/v14/watanabe13a.html",
        "https://arxiv.org/abs/2308.12108",
        "https://arxiv.org/abs/2507.21449"
      ],
      "note": "Part (a) is a direct WBIC theorem corollary; the varying-gamma regimes in part (b) remain open."
    },
    {
      "label": "Problem 6.2",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://jmlr.org/papers/v14/watanabe13a.html",
        "https://arxiv.org/abs/2408.13030",
        "https://arxiv.org/abs/2411.19920",
        "https://arxiv.org/abs/2404.14855"
      ],
      "note": "The compact domain/prior after hard restriction is implicit. WBIC supplies convergence and leading fluctuations; the factorization-point classification remains open."
    },
    {
      "label": "Question 9.1",
      "precision": "well-posed",
      "openness": "resolved",
      "citations": [
        "https://eudml.org/doc/75301",
        "https://aif.centre-mersenne.org/item/AIF_1997__47_3_859_0/",
        "https://arxiv.org/abs/2303.15739"
      ],
      "note": "For the stated finite input set, finitely many activation cells reduce the evidence and sublevel volume to finite sums of analytic branch contributions, proving the requested equality."
    }
  ],
  "attribution_issues": [
    "Lines 365-373, 437, 447, and 473 present the uniform-attention RLCT as unknown, but it is an exact reduced-rank-regression instance of the cited Aoyagi-Watanabe result.",
    "Line 422 presents Problem 6.1(a) as an unwritten adaptation, although it is a direct application of Watanabe 2013, Theorem 4; the convergence and leading fluctuations in Problem 6.2 are likewise already in that theorem after restricting the domain.",
    "Line 459 cites Lion-Rolin 1997 for a volume-under-integration claim whose directly relevant source is Lion-Rolin 1998, and overstates it for arbitrary smooth priors.",
    "Question 9.1 is presented as a missing ReLU theorem, but the finite-input model stated there is covered by a finite activation-cell reduction to analytic branch models.",
    "The modular related-work account omits the 2025 final venue for Tian's paper and relevant 2025-2026 mechanism papers by McCracken et al. and He et al."
  ],
  "confidence": "high"
}
```
