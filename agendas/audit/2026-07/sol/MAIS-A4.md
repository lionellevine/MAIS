> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A4](../../../A4/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Audit report: `training-for-interpretability.tex`

## Summary verdict

The file's eight displayed proofs are mathematically sound (apart from one harmless sentence in Theorem 4.3's proof), and its core definitions are mostly careful. It nevertheless has **significant issues** for publication as an open-problems supplement. Most importantly, Conjecture 5.3 is already a consequence of the subadditivity established immediately before it: a short padding argument proves convergence along every aspect-ratio sequence. Question 5.10 is not well-posed because the ReLU objective need not have a classical gradient, its three “phases” are not defined as subsets of parameter space, and several limits used to define the requested probabilities may not exist. The literature/attribution account also needs correction: the paper attributes experiments on the exact privileged-basis objective to Jermyn et al., although their model and tasks are different; it describes *The Persian Rug* as an exact solution although that paper optimizes within an empirically motivated statistical-symmetry ansatz and proves only near-optimal scaling; and it omits several directly relevant 2025–2026 theoretical papers. Finally, the claim that merely imposing coherence below \(1/\sqrt n\) leaves only linearly many vectors does not follow from the Welch bound and needs a uniform gap below the threshold. These defects do not undermine the elementary theorems, but they do undermine the file's claim that every item in Section 5 is open after a July 2026 literature check.

## Findings, ordered by severity

### 1. Conjecture 5.3 is resolved by a direct padding argument

**Location:** lines 323–339, especially the last sentence of Remark 5.2 and Conjecture 5.3.

The remark proves subadditivity, defines \(p(q,S,c)\) for rational \(q\in(0,1)\) by Fekete's lemma, and proves that it extends continuously to all \(q\in(0,1)\). Those facts already imply the conjectured convergence.

Write \(P_{m,n}=P_{m,n,S}(c)\), fix a sequence \(m_j\to\infty\) with \(\beta_j=n_j/m_j\to\beta\in(0,1)\), and use the continuous extension of \(p\).

*Lower bound.* For every \(j\), \(\beta_j\) is rational, and the Fekete limit for the ray through \((m_j,n_j)\) satisfies

\[
p(\beta_j,S,c)=\inf_{k\ge1}\frac{P_{k m_j,k n_j}}{k m_j}
\le \frac{P_{m_j,n_j}}{m_j}.
\]

Continuity of \(p\) gives

\[
\liminf_j \frac{P_{m_j,n_j}}{m_j}\ge p(\beta,S,c).
\]

*Upper bound.* Fix rational \(q=N/M<\beta\) and \(\varepsilon>0\). Replacing \((M,N)\) by a sufficiently large multiple, Fekete's lemma supplies a block with

\[
\frac{P_{M,N}}M\le p(q,S,c)+\varepsilon.
\]

Let \(k_j=\lfloor m_j/M\rfloor\) and \(r_j=m_j-k_jM<M\). For all large \(j\), \(k_jN\le n_j\), because \(q<\beta_j\). Put \(k_j\) copies of the block in orthogonal hidden-coordinate subspaces, leave the remaining hidden coordinates unused, and make the remaining \(r_j\) feature columns zero with optimal constant outputs. Cross-block coherence is zero and the extra loss is \(r_jv(S)\), hence

\[
\frac{P_{m_j,n_j}}{m_j}
\le \frac{k_jP_{M,N}+r_jv(S)}{m_j}
\longrightarrow \frac{P_{M,N}}M
\le p(q,S,c)+\varepsilon.
\]

Let \(\varepsilon\downarrow0\) and then \(q\uparrow\beta\), using continuity. This gives the matching limsup. Thus Conjecture 5.3 is **resolved**, and the sentence “What block sums do not give is convergence along general sequences” is false.

### 2. Question 5.10 does not define the probabilities it asks for

**Location:** lines 432–441.

There are three independent precision failures.

1. The vector field \(-\nabla(L+\lambda R)\) is not globally defined. For example, at \(W=0,b=0\), varying one bias \(b_i\) gives a left derivative \(0\) and a right derivative \(-2\mathbb E x_i=-(1-S)\) for its loss summand. ReLU therefore makes \(L\) nondifferentiable at an allowed parameter point. Saying that “well-posedness … [is] part of the question” does not define whether the intended dynamics is classical gradient flow, a Clarke subgradient differential inclusion, a chosen ReLU derivative, or another selection; these give inequivalent laws.
2. “Drop the second feature,” “dedicate the dimension to it,” and “store the pair antipodally” are informal labels, not measurable, mutually exclusive subsets of parameter space. For example, “antipodal” could mean exactly \(w_2=-w_1\), merely \(w_1w_2<0\), or behavioral two-feature storage with arbitrary magnitudes and biases. “Drop” could mean \(w_2=0\), a dead output due to bias, or negligible contribution. The requested phase probabilities consequently have no defined events.
3. Parts (1) and (3) use \(\theta_\infty\) even if the flow does not converge. Part (2) says “wherever defined,” but does not specify conditioning, a cemetery state, or a probability assigned to nonconvergent trajectories. Part (3) also changes to parameters \((m,k,S,\sigma)\) while the opening tuple fixes \((m,n,S,\lambda,\sigma)\).

This item is **ill-posed** as written. A solution requires a generalized-flow convention, formal phase sets, and treatment of nonconvergence before any openness question has a truth value.

### 3. The claimed July 2026 openness check misses directly overlapping 2025–2026 theory

**Location:** lines 304, 364–384, 398, 402–425, 464–470.

The following primary sources do not solve all of the exact questions, but they are too close to omit from a claim that the theoretical landscape has been checked through July 2026:

- Ivanov et al., [*Spectral Superposition: A Theory of Feature Geometry*](https://arxiv.org/abs/2602.02224) (February 2026), analyze the canonical toy model, prove spectral localization conditional on capacity saturation, derive tight-frame/association-scheme classifications covering polygons and antiprisms, and derive induced Gram/projector/eigenvalue gradient-flow equations. This bears directly on Problems 5.1 and 5.7 and Question 5.10. It does **not** prove that the capacity-saturation hypothesis holds at every global minimizer, identify the regular pentagon as the unique global optimum, compute the coherence frontier, or give the phase probabilities in Question 5.10.
- Dorrell, [*How Optimality Structures Sparse Dictionaries*](https://arxiv.org/abs/2606.02385) (June 2026), extends local optimality analysis to nonnegative jointly optimized SAE dictionaries and explicitly treats dense antipodal features, splitting, absorption, and residual structure. It does not visibly settle the exact population estimator \(J_{W,S,\alpha}\) for \(W^*=(\pm e_1,\pm e_2)\), but it is directly relevant to Problem 5.5 and Question 5.6.
- Mencattini, Montagna, and Locatello, [*The Rate-Distortion-Polysemanticity Tradeoff in SAEs*](https://arxiv.org/abs/2605.14694) (May 2026), prove under toy-model assumptions that imposing monosemanticity raises achievable rate/distortion and relate optimal polysemanticity to co-occurrence. This is a candidate partial resolution of the qualitative content of Problem 5.8, although its SAE setup and polysemanticity measure must be compared carefully with the exact \(L',M\) used here.
- Chen et al., [*Taming Polysemanticity in LLMs: Provable Feature Recovery via Sparse Autoencoders*](https://arxiv.org/abs/2506.14002), accepted at ICLR 2026, give a statistical identifiability framework and a bias-adaptation SAE algorithm with a feature-recovery theorem. It does not analyze the fixed estimator \(J\) or an upstream minimizer of \(L+\lambda R\), but directly qualifies claims that feature-recovery guarantees for modified SAE training are absent.
- Zhu et al., [*Diagnosing and Fixing Latent Recovery in Sparse Autoencoders*](https://openreview.net/forum?id=Hl3rEn7S4P) (ICLR 2026 workshop oral), prove upper and lower latent-recovery bounds involving coherence and sparsity and propose a self-consistency regularizer. Again, this does not settle REC as defined here, but it is directly related to Problems 5.5–5.6.
- Klindt et al., [*A unifying framework from neural superposition to sparse interpretable codes*](https://www.nature.com/articles/s42256-026-01259-z), synthesizes identifiability and compressed-sensing guarantees into a superposition-to-sparse-code pipeline. Its publication date, 14 July 2026, is two days after this draft, so it should be treated as contemporaneous follow-up rather than a pre-draft omission.

These sources change several openness verdicts to `open-with-related-work`, and Ivanov et al. and Mencattini et al. warrant a human check under `possibly-resolved` for the especially overlapping items.

### 4. Jermyn et al. are cited for observations in a different architecture

**Location:** lines 258 and 412.

The file says Definition 4.7 is “the setting of Jermyn, Schiefer, and Hubinger” and that “this architecture has both monosemantic and polysemantic local minima.” The source does not study the displayed objective \(g_\theta(x)=\operatorname{ReLU}(V\operatorname{ReLU}(Wx+\beta)+c)\) on \(x\sim\mathcal D_{m,S}\). Jermyn et al., [*Engineering Monosemanticity in Toy Models*](https://arxiv.org/abs/2211.09169), first randomly project sparse feature vectors \(f\) to inputs \(Pf\), then use

\[
h=N(L_1Pf+b),\qquad y=L_2h,
\]

with a linear, unbiased output layer, and study feature decoding, random reprojection, and an absolute-value task. Their empirical basin and negative-bias observations motivate Problem 5.8, but do not establish the existence of either kind of local minimum for this file's \(L'_{m,k,S}\). This is an attribution error, not merely a missing caveat.

### 5. *The Persian Rug* is described as an exact unrestricted solution, which it is not

**Location:** lines 254 and 470.

The file says Cowsik, Dolev, and Infanger “obtain a complete solution” and “solve a large-\(m\) toy model exactly … obtaining the optimal loss scaling.” Their paper, [*The Persian Rug*](https://arxiv.org/abs/2410.12101), instead:

- empirically observes statistical permutation symmetry in trained large models;
- optimizes the macroscopic parameters within that statistically symmetric ansatz;
- constructs weights attaining the symmetric variance bound and empirically matching trained loss; and
- gives high-sparsity upper and lower scaling bounds, described as near-optimal and in places matching only up to logarithmic or constant factors.

The paper itself says “optimal permutation symmetric algorithm” and “near-optimal among recently proposed architectures,” not an exact proof of the unrestricted global optimum. The supplement should use that narrower attribution. Likewise, line 254's statement that Elhage et al. “solve tiny cases” should be read as evaluation of candidate phases, not a proof of global optimality; line 398 itself says such a global-optimum theorem would be the first.

### 6. The \(1/\sqrt n\) coherence claim is not a consequence of the Welch bound

**Location:** line 100 (and the paraphrase at line 244).

From Lemma 4.2, \(m\) unit vectors with coherence at most \(c<1/\sqrt n\) satisfy

\[
m\le \frac{n(1-c^2)}{1-nc^2}.
\]

This is \(O(n)\) only if there is a **uniform relative gap**, for example \(c^2\le(1-\eta)/n\) for fixed \(\eta>0\). The condition \(c<1/\sqrt n\) by itself permits the denominator \(1-nc^2\) to approach zero with \(n\); the Welch bound alone therefore does not “collapse … supply to a linear one.” Indeed Welch-equality systems have \(c^2=(m-n)/(n(m-1))<1/n\) for every finite \(m\), and real equiangular tight frames include examples as large as \(m=n(n+1)/2\) in the dimensions where maximal examples exist. The safe claim is the bound actually proved, or the fixed-gap \(O_\eta(n)\) consequence. The exponential lower bound at fixed \(\varepsilon\), and the Benedetto–Fickus frame-potential statement, are otherwise correct.

### 7. The “standard epi-convergence” assertion omits essential hypotheses

**Location:** line 360, read with the attainment caveat at lines 147–149.

The statement that minimizers approach \(\operatorname{argmin}L\) as \(\lambda\downarrow0\) and the orthogonal phase as \(\lambda\to\infty\) does not follow from “standard epi-convergence” on the noncompact \((W,b)\)-space without equicoercivity, attainment, and a precise topology. As \(\lambda\to\infty\), epi-convergence would first constrain to minimizers of \(R\), but \(R=0\) means pairwise orthogonal **nonzero** columns plus arbitrarily many zero columns; it does not by itself prove convergence of minimizers or exclude escaping norms/biases. As \(\lambda\downarrow0\), cluster points require precompactness and need not exist. The formal Problem 5.4 wisely requires nonempty minimizer sets in part (1), but this explanatory “routine regimes” claim should not be presented as established.

### 8. Smaller precision defects in Problems 5.5, 5.8, and 5.9

**Problem 5.5, lines 366–374 — `minor-issues`.** Part (2) does not require \(\operatorname{argmin}(L+\lambda R)\ne\varnothing\). Therefore “every” regularized minimizer recovers \(W_\lambda\) is formally true when that argmin is empty, creating an unintended vacuous witness. Remark 3.2 acknowledges attainment but its alternative reading in terms of “\(\delta\)-minimizers uniformly in small \(\delta\)” is not actually quantified. Require both argmins nonempty or state the uniform approximate-minimizer version.

**Problem 5.8, lines 404–414 — `minor-issues`.** The set defining \(\delta^*\) can be empty, but no convention says whether \(\inf\varnothing=+\infty\) or whether \(\delta^*\) is intended to lie in \([0,1]\). The Jermyn attribution in part (2) is also to a different objective, as above; the requested existence statement itself is otherwise precise.

**Problem 5.9, lines 420–426 — `minor-issues`.** The exact definition of \(Q_{m,n,S}\) and its conjectured formula are well-posed. The final “more generally” request is not: the comparison does not fix or quantify the wiring budget \(k_0\) and coherence cap \(c\), nor define the two recovery-constrained frontier functions whose least losses are to be compared. Two readers can interpret it as a pointwise comparison at selected budgets or as optimization over budgets, which are inequivalent.

### 9. Proof audit: all eight displayed results survive line-by-line checking

- **Proposition 3.1 (Scalarization): correct.** Both inequalities follow directly from the two minimizing properties; no convexity is needed.
- **Lemma 4.1 (Dropped-feature floor): correct.** The mixture has mean \((1-S)/2\), second moment \((1-S)/3\), and variance \(v(S)=(1-S)(1+3S)/12\); the ReLU constraint is inactive at the optimal constant.
- **Lemma 4.2 (Packing): correct.** The Welch calculation and rearrangement are correct. The induction for pairwise nonpositive inner products correctly loses at most two vectors on projection and yields \(2n\).
- **Theorem 4.3 (Price of orthogonality): correct.** The antipodal per-coordinate error is \((1-S)^2\mathbb E\min(U,U')^2=(1-S)^2/6\), because \(\mathbb E\min(U,U')^2=1/6\); summing and subtracting gives the threshold \(S>3/7\). Minor textual slip: for \(n=1\), the antipodal system has \(\mu_+=-1\), not \(0\), but it is still feasible for \(\mu_+\le0\), so no conclusion changes.
- **Theorem 4.5 (General coherence caps): correct.** It combines the real-valued upper bound on the number of nonzero columns with the per-zero-column floor; nonintegrality of \(m_*(c)\) only weakens the inequality and causes no gap.
- **Proposition 4.8 (Blindness): correct.** The identity, nonnegative shear, and \(Q,-Q\) constructions all reconstruct \(x\ge0\) exactly and have the claimed alignment indices.
- **Proposition 4.9 (Free lunch): correct.** Nonnegativity plus the zero-valued witness forces both summands to vanish; \(R'=0\) is exactly row-1-sparsity.
- **Proposition 4.10 (Perfectly monosemantic bottleneck): correct.** At most \(k\) input coordinates can influence the hidden layer, and each remaining independent coordinate incurs at least its variance \(v(S)\); the identity/constant construction attains the bound.

I also checked the unnumbered numerical/background computations used later: the mass decomposition in Example 6.3 sums correctly, \(R=2w_1^2w_2^2\) in Example 6.1, the symmetry action in Section 5 is valid, the compact-domain minimum defining \(J\) is attained (codes can be uniformly bounded by comparison with \(a=0\)), and the block-sum subadditivity and rational convexity claims in Remark 5.2 are correct. The defect in that remark is only its final claim that general-sequence convergence does not follow.

## Per-item precision and openness ledger

1. **Problem 5.1 (Coherence-constrained frontier):** precision `well-posed`; openness `open-with-related-work`. Elhage et al. provide candidate phase calculations; Chen et al. analyze \(k\)-gon critical points; Cowsik et al. give a large-system symmetric ansatz; Ivanov et al. classify capacity-saturated tight-frame geometries. None computes the exact constrained \(P_{3,2,S}\) or \(P_{5,2,S}\), proves the proposed finite analytic stratification, or determines \(c^*\).
2. **Conjecture 5.3 (Thermodynamic frontier):** precision `well-posed`; openness `resolved`. The direct proof is Finding 1. The literature search found Cowsik et al. in a related large-system regime but is not needed for the resolution.
3. **Problem 5.4 (Penalizing the sum to control the max):** precision `well-posed`; openness `open-with-related-work`. Frame-potential and incoherent-dictionary regularization literature studies \(R\)-like objectives, and Ivanov/Cowsik study tight-frame geometry, but no source found the exact upstream \(L+\lambda R\) minimizer/coherence map. The explanatory epi-convergence claim is unsupported, not part of the formal quantifiers.
4. **Problem 5.5 (Recovery transfer):** precision `minor-issues`; openness `open-with-related-work`. Cui et al., Dorrell, Chen et al., Zhu et al., and classical nonnegative sparse recovery all substantially overlap, but none located source proves the exact every-global-minimizer predicate for this \(J\) and the four antipodal atoms, still less transfer from an upstream \(L+\lambda R\) argmin.
5. **Question 5.6 (Does coherence rank recoverability?):** precision `well-posed`; openness `open-with-related-work`. Itoh, Duarte, and Parente's [positive subset coherence conditions](https://arxiv.org/abs/1512.02743) already show that unsigned mutual coherence is not the only geometry controlling nonnegative \(\ell^1\) recovery, while Dorrell treats dense antipodal SAE features. No exact pair \(W,W'\) satisfying this file's universal-global-minimizer REC predicate was found.
6. **Problem 5.7 (Single-orbit training):** precision `well-posed`; openness `possibly-resolved`. Ivanov et al.'s February 2026 classification is close enough to demand a human comparison, but it assumes capacity saturation and proves tight-frame/association-scheme structure, not that the regular pentagon is the unique unrestricted global optimum or that an \(R\)-penalty creates a single orbit.
7. **Problem 5.8 (Monosemanticity frontier):** precision `minor-issues`; openness `possibly-resolved`. Mencattini et al. theoretically characterize a rate–distortion–polysemanticity tradeoff in a 2026 SAE toy model; its architecture and metric differ, so it is not yet an exact resolution of \(P'_{m,k,S}\), but it may cover a nearby frontier. Jermyn et al. are empirical and use a different objective.
8. **Problem 5.9 (Wiring frontier):** precision `minor-issues`; openness `open-with-related-work`. Gao et al. [measure the empirical capability–interpretability frontier](https://arxiv.org/abs/2511.13653), while 2026 work such as [*Sparse but not Simpler*](https://arxiv.org/abs/2603.15919) tests the limits of structural sparsity. No exact column-sparse toy-model value or recovery-constrained comparison was found.
9. **Question 5.10 (What does gradient flow select?):** precision `ill-posed`; openness `open-with-related-work` after a repair. Chen et al., [*Dynamical versus Bayesian Phase Transitions in a Toy Model of Superposition*](https://arxiv.org/abs/2310.06301), empirically link SGD plateaus to \(k\)-gon critical points; Ivanov et al. derive spectral gradient-flow equations; and Lecomte et al., [*Incidental polysemanticity*](https://www.alignmentforum.org/posts/sEyWufriufTnBKnTG/incidental-polysemanticity), analyze winner-take-all dynamics in a similar tied ReLU autoencoder. None gives the requested law for the exact, presently undefined events.

## Search-query log

Queries are reproduced literally. Search results were checked against primary arXiv, OpenReview, proceedings, journal, lab, or Alignment Forum pages rather than relying on result snippets.

### Problem 5.1

- `"Toy Models of Superposition" coherence constrained frontier`
- `2024 2025 2026 toy model superposition exact global optimum regular polygon`
- `ReLU tied autoencoder coherence constraint phase diagram superposition`
- `"Persian rug" solving toy models superposition coherence regularizer`

### Conjecture 5.3

- `"thermodynamic frontier" superposition autoencoder`
- `large m limit toy models superposition loss compression ratio rigorous 2024 2025`
- `asymptotic optimal loss sparse ReLU autoencoder permutation symmetric`
- `subadditive limit feature dimension ratio superposition`

### Problem 5.4

- `"interference regularizer" coherence toy models superposition`
- `frame potential regularization coherence neural dictionary training`
- `2024 2025 incoherence regularizer sparse autoencoder training interpretability`
- `mutual coherence regularizer dictionary learning global minimizer`

### Problem 5.5

- `"antipodal" sparse autoencoder dictionary recovery nonnegative codes`
- `2025 2026 sparse autoencoder theoretical recovery superposition dictionary global optimum`
- `nonnegative sparse coding dictionary identifiability antipodal atoms`
- `L1 autoencoder global minimizer true dictionary population objective`

### Question 5.6

- `coherence does not predict dictionary recovery counterexample`
- `mutual coherence insufficient sparse recovery average case support distribution`
- `antipodal high coherence nonnegative sparse coding recoverability`
- `2024 2025 sparse autoencoder coherence feature recovery metric Goodhart`

### Problem 5.7

- `"regular pentagon" "toy models of superposition" global optimum`
- `2026 spectral superposition polygons association schemes global optimum`
- `"single orbit" identifiability neural network minima symmetry superposition`
- `toy model superposition polytope phase rigorous optimum`

### Problem 5.8

- `"Engineering Monosemanticity in Toy Models" local minima proof`
- `2024 2025 2026 monosemantic polysemantic local minima ReLU autoencoder theory`
- `monosemanticity frontier bottleneck sparse features hidden bias`
- `privileged basis neural network monosemanticity regularizer theorem`

### Problem 5.9

- `"column-1-sparse" "toy model" superposition`
- `2024 2025 2026 weight sparse transformers interpretable circuits theorem`
- `sparse wiring autoencoder task loss exact antipodal`
- `L0 weight regularization monosemanticity superposition theory`

### Question 5.10

- `"Toy Models of Superposition" gradient flow dynamics phase probability`
- `gradient flow superposition toy model phase transitions 2024 2025 2026`
- `implicit bias ReLU autoencoder monosemantic polysemantic initialization`
- `dynamical versus Bayesian phase transitions toy model superposition gradient descent`
- `"A Mechanism for the Emergence of Superposition in Toy Models"`
- `site:alignmentforum.org toy model superposition training dynamics gradient`

### Cross-item and attribution checks

- `"Superposition Phase Transitions in ReLU Networks"`
- `"balanced Parseval tight-frame model" superposition`
- `site:arxiv.org superposition phase transitions ReLU networks 2026 tight frame`
- `site:openreview.net superposition feature geometry toy model 2026`
- `real equiangular tight frames infinite family N superlinear dimension Steiner ETF projective plane`
- `Welch bound coherence below 1/sqrt n number vectors linear`
- `Aharon Elad Bruckstein uniqueness overcomplete dictionaries (k+1) binomial m k samples`
- `Hillar Sommer dictionary learning (k+1) choose m k samples theorem`
- `Gribonval Jenatton Bach local minimum polynomial samples true dictionary`

## Machine-readable verdict

```json
{
  "file": "training-for-interpretability.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Proposition 3.1",
      "verdict": "correct",
      "note": "The scalarization inequalities follow directly from the two minimizing properties; no convexity is required."
    },
    {
      "label": "Lemma 4.1",
      "verdict": "correct",
      "note": "The mixture mean, second moment, and variance are computed correctly, and the optimal nonnegative constant is feasible."
    },
    {
      "label": "Lemma 4.2",
      "verdict": "correct",
      "note": "The Welch-bound calculation and the induction proving the 2n signed-packing bound are valid."
    },
    {
      "label": "Theorem 4.3",
      "verdict": "correct",
      "note": "The antipodal error and 3/7 threshold are correct. The proof's statement mu_+=0 has a harmless n=1 exception (it is -1), but feasibility and the theorem are unaffected."
    },
    {
      "label": "Theorem 4.5",
      "verdict": "correct",
      "note": "The packing bound and dropped-feature floor combine exactly as claimed."
    },
    {
      "label": "Proposition 4.8",
      "verdict": "correct",
      "note": "The identity, shear, and Hadamard constructions reconstruct all nonnegative inputs and have the stated alignment."
    },
    {
      "label": "Proposition 4.9",
      "verdict": "correct",
      "note": "A zero-valued witness exists, and nonnegativity forces every global minimizer to have zero loss and row-1-sparse W."
    },
    {
      "label": "Proposition 4.10",
      "verdict": "correct",
      "note": "At most k input features can influence the hidden layer, so every unread independent coordinate costs at least v(S); the construction attains the bound."
    }
  ],
  "items": [
    {
      "label": "Problem 5.1",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "Elhage et al. (2022), arXiv:2209.10652",
        "Cowsik et al. (2024), arXiv:2410.12101",
        "Chen et al. (2023), arXiv:2310.06301",
        "Ivanov et al. (2026), arXiv:2602.02224"
      ],
      "note": "Recent work classifies related symmetric or capacity-saturated geometries but does not compute the exact coherence-constrained frontiers, analytic stratification, or c*."
    },
    {
      "label": "Conjecture 5.3",
      "precision": "well-posed",
      "openness": "resolved",
      "citations": [
        "Cowsik et al. (2024), arXiv:2410.12101 (related large-system regime)"
      ],
      "note": "The source's Fekete limit plus zero-column and unused-dimension padding gives a matching liminf and limsup along every sequence n/m tending to beta; a complete proof is in this audit."
    },
    {
      "label": "Problem 5.4",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "Benedetto and Fickus (2003), Finite normalized tight frames",
        "Cowsik et al. (2024), arXiv:2410.12101",
        "Ivanov et al. (2026), arXiv:2602.02224"
      ],
      "note": "No source found determines the global-minimizer coherence map for L+lambda R. The surrounding epi-convergence assertion is not justified without compactness and attainment hypotheses."
    },
    {
      "label": "Problem 5.5",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "Cui et al. (2026), arXiv:2506.15963",
        "Dorrell (2026), arXiv:2606.02385",
        "Chen et al. (2026), arXiv:2506.14002",
        "Zhu et al. (2026), OpenReview:Hl3rEn7S4P"
      ],
      "note": "Part (2) can be vacuous if the regularized argmin is empty. The cited theory substantially overlaps but does not establish the exact every-global-minimizer REC predicate or upstream transfer."
    },
    {
      "label": "Question 5.6",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "Itoh, Duarte, and Parente (2016), arXiv:1512.02743",
        "Dorrell (2026), arXiv:2606.02385",
        "Mencattini et al. (2026), arXiv:2605.14694"
      ],
      "note": "Positive-subset coherence and antipodal-feature theory show why unsigned coherence is incomplete, but no exact W,W' witness for the file's universal REC predicate was found."
    },
    {
      "label": "Problem 5.7",
      "precision": "well-posed",
      "openness": "possibly-resolved",
      "citations": [
        "Ivanov et al. (2026), arXiv:2602.02224",
        "Chen et al. (2023), arXiv:2310.06301"
      ],
      "note": "Ivanov et al. classify capacity-saturated polygonal geometries, but do not plainly prove capacity saturation, unrestricted global optimality of the pentagon, or the single-orbit assertion. Human comparison is warranted."
    },
    {
      "label": "Problem 5.8",
      "precision": "minor-issues",
      "openness": "possibly-resolved",
      "citations": [
        "Jermyn et al. (2022), arXiv:2211.09169",
        "Mencattini et al. (2026), arXiv:2605.14694",
        "Chen et al. (2026), arXiv:2506.14002"
      ],
      "note": "The empty-set convention for delta* is missing, and Jermyn et al. use a different architecture. Mencattini et al. prove a closely related monosemanticity frontier under different toy assumptions, so exact coverage needs a human check."
    },
    {
      "label": "Problem 5.9",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "Gao et al. (2025), arXiv:2511.13653",
        "Zhang (2026), arXiv:2603.15919"
      ],
      "note": "The exact Q problem is precise, but the final recovery comparison does not quantify k0 and c or define its frontiers. No exact toy-model solution was found."
    },
    {
      "label": "Question 5.10",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "Chen et al. (2023), arXiv:2310.06301",
        "Ivanov et al. (2026), arXiv:2602.02224",
        "Lecomte et al. (2023), Incidental polysemanticity, AI Alignment Forum"
      ],
      "note": "The ReLU gradient field is not globally defined, phase events are informal and nonexhaustive, and theta_infinity is used without a nonconvergence convention. Related dynamics work does not repair these definitions."
    }
  ],
  "attribution_issues": [
    "Lines 258 and 412 attribute local-minimum observations for the exact L' architecture to Jermyn et al., but that paper uses randomly projected inputs, a linear output without output ReLU or bias, and different tasks.",
    "Lines 254 and 470 overstate The Persian Rug as an exact unrestricted solution; it proves optimality within a statistical-symmetry ansatz, matches trained models empirically, and gives near-optimal asymptotic scaling.",
    "The claim that Elhage et al. solve tiny cases should be limited to closed-form candidate-phase calculations, since the file itself says no polytope phase has been certified as the true global optimum.",
    "The July 2026 related-work account omits directly overlapping work by Ivanov et al. (2602.02224), Dorrell (2606.02385), Mencattini et al. (2605.14694), Chen et al. (2506.14002), and Zhu et al. (OpenReview Hl3rEn7S4P)."
  ],
  "confidence": "high"
}
```
