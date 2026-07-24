> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A5](../../../A5/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Audit of `open problems/representation-theory-learned-circuits.tex`

## Summary

The two numbered proofs and the elementary representation-theoretic setup are correct, and all eleven formal problems remain genuinely open in their stated fixed-width/fixed-scale gradient-flow regimes after a 2024--2026 cross-venue search. The file nevertheless has **significant issues**. Most importantly, it repeatedly promotes He et al.'s asymptotic theorem for a Taylor-surrogate projected flow to an asymptotic theorem for projected cross-entropy; the paper proves only finite-horizon closeness of the two flows. It also imports Morwani et al.'s `L_{2,3}` maximum-margin characterization into an ensemble regularized by Euclidean squared norm, which Wei et al.'s norm-parametric theorem does not permit. Independently, the analytic-convergence discussion misses an open positive-probability basin converging to the zero network. These errors do not resolve the headline questions, but they materially overstate the known footholds and invalidate the stated motivation for Conjecture 5.6. Problem 6.3 is also not reproducible enough to be a precise formal item.

## Findings by severity

### Major

1. **Lines 227, 254, 261, 295, 323, and 336 overstate the scope of He et al. (2026).** The paper does introduce exact cross-entropy and projected gradient flow, but then Taylor-expands the loss to an approximate risk `R_ap`. Its asymptotic single-irrep theorem (Theorem 4.3) is explicitly for projected flow under `R_ap`. Proposition 4.2 compares exact and approximate trajectories only on a fixed finite time interval, with an error bound that grows with time; it does not transfer the `t -> infinity` theorem to exact cross-entropy. Thus statements such as “each neuron converges almost surely” and “a dense selection law ... is proved for the projected flow” need the qualification “for the approximate small-logit risk,” and the claimed “solved idealization” in line 336 is not the exact projected version of Definition 3.2. See the primary paper, especially Sections 4.2 and Theorem 4.3: [He et al., arXiv:2606.02993](https://arxiv.org/abs/2606.02993).

2. **Lines 227, 270, and 317 mix incompatible regularizer norms.** Definition 3.2 uses `lambda ||theta||_2^2`. Morwani et al.'s Theorems 7 and 9 characterize maximum margin under `L_{2,3}`, and their experiments train with `L_{2,3}` regularization. Their quoted version of Wei et al.'s theorem says that, for *any chosen norm*, weak regularization approaches maximum margin for that same norm; it does not turn Euclidean regularization into `L_{2,3}` margin. Consequently, “all representations” is not a maximum-margin prediction for the ensemble actually defined here, and Conjecture 5.6 is not supported by Theorem 9 as claimed. The conjecture itself remains a meaningful open statement. See Sections 3, 5, and 7 of [Morwani et al., ICLR 2024](https://openreview.net/forum?id=i9wDX850jR).

3. **Line 227 proposes ruling out an event that necessarily has positive probability.** For quadratic activation every logit is cubic in the parameters, so near the origin

   `L_lambda(theta) = log |G| + lambda ||theta||_2^2 + O(||theta||_2^3)`.

   Hence, for every `lambda > 0`, `theta = 0` is a strict hyperbolic local minimum with Hessian `2 lambda I` and has an open attraction basin. A full-support Gaussian initialization hits that basin with positive probability, and those trajectories converge to identically zero centered logits. Analytic convergence of `theta(t)` therefore does not by itself settle convergence of the normalized correlations `beta_rho`, which are discontinuous at zero. Part 5.1(a) may still be approachable by analyzing the leading asymptotic logit direction in this basin, but “ruling [zero limits] out is all that remains” is false.

### Moderate

4. **Line 323 overstates a second He et al. paper's lottery-ticket theorem.** The full-random-initialization ReLU results are empirical. The rigorous quadratic analysis uses sufficiently small initialization, an early-stage nearly uniform-softmax/decoupled approximation, and initially single-frequency neurons (Assumption 5.1); Corollary 6.1 treats an idealized multi-frequency initialization with controlled equal magnitudes under the decoupled ODE. It is not a theorem for the full fixed-scale Gaussian trajectory of Definition 3.2. The file does later say the fixed-scale regime is open, but calling the intervening claim a proved random-start mechanism obscures exactly that gap. See Sections 5--6 of [He et al., arXiv:2602.16849](https://arxiv.org/abs/2602.16849).

5. **Problem 6.3 is not a reproducible formal experiment.** It leaves the `lambda` grid, `epsilon` and `delta`, numerical flow/optimizer, ReLU subgradient convention, convergence/stopping rule, and statistical reporting rule unspecified. Exact Clarke flow and AdamW are inequivalent readings, as are different thresholds near atoms of the spectral weights. Moreover, `q_[rho]` is a conjectural population limit, so the observable should be described as a finite-`m` multiplicity estimate. These omissions can materially change every requested histogram.

### Minor

6. **Lines 270 and 317 say “every/all neurons” where Morwani et al. allow zero neurons.** Theorem 7's displayed scale permits `lambda = 0`, and a zero vector is vacuously spanned by any representation in Theorem 9. Under Definition 4.2 here a dead neuron is pure for no class. “Every nonzero (active) neuron is supported on one representation” is the defensible translation.

7. **Line 254 reads independence into Conjecture 5.3.** Convergence of empirical proportions is a law of large numbers, but it does not imply that neurons land independently; correlated or exchangeable arrays can have the displayed limit. The formal conjecture is fine, while its explanatory gloss is stronger than its formula.

8. **Line 332 needs a separability qualification.** Unregularized cross-entropy has no finite minimizer along a strictly separating ray, but the blanket claim is not automatic for every width and activation in the file. The standard statement should be restricted to parameter regimes in which the architecture achieves positive margin.

## Proof and background-claim ledger

- **Lines 84--98 (finite-group representation theory): correct.** Character orthogonality, Artin--Wedderburn decomposition, the central idempotent, block dimension `d_rho^2`, conjugate pairing, and the automorphism action are all stated correctly.
- **Line 128 (smooth global flow): correct.** Coercivity handles `lambda > 0`; for `lambda = 0`, the energy identity and the resulting finite-time displacement bound prevent finite-time escape.
- **Line 128 (Clarke trajectories and measurable selection): correct with a presentation gap.** Existence and global continuation are standard for this locally Lipschitz definable loss, and a measurable selection can be obtained from the compact solution multifunction. The text should cite the differential-inclusion and measurable-selection results and should select in a global path space (or explain the compatible diagonal construction), rather than asserting compactness/closed graph on each finite interval and immediately concluding one global assignment. No counterexample was found.
- **Lemma 3.3 (`lem:gcr`): correct.** For a unitary matrix, `Re tr U <= d`, with equality exactly at `U = I`; positivity of the coefficients then makes the joint-kernel condition necessary and sufficient for uniqueness.
- **Lines 147--188 (spectral observable): correct.** The norm of each `psi_rho` is `|G|^{3/2}`, the functions are orthogonal, centering removes softmax gauge, and Bessel gives the stated key-set bound. Chughtai et al. did center logits over the output coordinate before their cosine-similarity calculation, so the claimed match to their measurement is fair: [Chughtai et al., arXiv:2302.03025](https://arxiv.org/abs/2302.03025).
- **Proposition 4.4 (`prop:symmetry`): correct.** The automorphism reindexing is orthogonal, preserves the loss and isotropic initialization, and sends the spectral class indices as claimed. The final marginal-probability identity follows from transitivity and linearity of expectation.
- **Remark 4.5 (`rem:correctness`): essentially correct.** The `S_3` character calculation is right; one ReLU neuron can isolate an input pair and width `|G|^2` can realize an arbitrary lookup table. The asserted nonempty-key-set lower bound is only sketched, but it follows from a uniform angle bound between each centered correct-class logit vector and the centered correct indicator, followed by the character expansion of the identity class function.
- **Lines 227, 270, 317, and 323:** not correct as literature/proof claims for the reasons in Findings 1--4.
- **Lines 310 and 334 (competing empirical mechanisms): supported.** Later work strengthens rather than removes the interpretive dispute: Stander et al. exhibit coset circuits, and Wu et al. give a broader approximately equivariant account without proving the selection laws posed here: [Stander et al.](https://arxiv.org/abs/2312.06581), [Wu et al.](https://arxiv.org/abs/2410.07476).

## Item-by-item precision and openness audit

### Problem 5.1 — The selection law (`prob:law`)

- **Precision:** well-posed. The exceptional-threshold convention and universal quantification over measurable ReLU selections are explicit.
- **Openness:** open with related work. No source found computes the fixed-`lambda`, fixed-width law or proves point-mass/non-point-mass behavior. He et al. prove asymptotics for the surrogate projected risk, Kunin et al. study vanishing initialization, and Marchetti et al. study a sequential-composition/vanishing-initialization regime; none matches the ensemble. The zero basin described above means even the graded smooth subproblem requires a different argument.
- **Evidence:** [He et al. 2026](https://arxiv.org/abs/2606.02993), [Kunin et al. 2025](https://arxiv.org/abs/2506.06489), [Marchetti et al. 2026](https://arxiv.org/abs/2602.03655).
- **Literal queries run:**
  - `2024 2025 2026 selection law irreducible representations group composition neural network random initialization weight decay gradient flow`
  - `site:arxiv.org group multiplication neural network representation selection probability gradient flow weight decay`
  - `site:openreview.net group composition learned irreducible representations random initialization selection 2026`
  - `site:alignmentforum.org grokking group representation circuit random seed selection`

### Problem 5.2 — Sparse or dense (`prob:sparse`)

- **Precision:** minor issues. It should state `C_0, tau_0 > 0` and that `p` tends through primes. Otherwise the nested limsup and observable are clear.
- **Openness:** open with related work. Ding et al. empirically study survival of circular features, while 2026 work gives wide/surrogate quadratic theory and new wide-ReLU mechanisms. None gives the requested `p`-scaling for this ReLU, weight-decayed, linear-width ensemble.
- **Evidence:** [Ding et al. 2024](https://openreview.net/forum?id=2WfiYQlZDa), [He et al. 2026](https://arxiv.org/abs/2602.16849), [Swaroop 2026](https://arxiv.org/abs/2603.23784), [cyclic-geometry TMLR submission](https://openreview.net/forum?id=ve7Iq6JQ6G).
- **Literal queries run:**
  - `2024 2025 2026 modular addition sparse dense frequencies ReLU width scaling number learned frequencies weight decay`
  - `"spectral count" modular addition learned frequencies sparse dense`
  - `site:arxiv.org modular addition surviving frequencies random seeds weight decay ReLU 2025 2026`
  - `site:openreview.net modular addition sparse Fourier features weight decay representation competition`

### Conjecture 5.3 — Law of large numbers for multiplicities (`conj:lln`)

- **Precision:** well-posed. The order of limits, positivity, `tau`-independence, and inclusion of fixed-`m` inner-limit existence are explicit. Only the following prose incorrectly adds independence.
- **Openness:** open with related work. The latest general-group theorem establishes single-irrep alignment only for the approximate projected risk and supplies a population law only in the Abelian case. No non-Abelian multiplicity LLN for the stated unconstrained flow was found.
- **Evidence:** [He et al. 2026](https://arxiv.org/abs/2606.02993), [Marchetti et al. 2026](https://arxiv.org/abs/2602.03655).
- **Literal queries run:**
  - `nonabelian group composition neural network projected gradient flow landing probability irreducible representation d squared 2026`
  - `"uniform diversification" irreducible representations neural network group composition`
  - `"selection probabilities" irreducible representation neural network group composition`
  - `site:arxiv.org 2026 nonabelian representation competition neuron random initialization group composition`

### Question 5.4 — Selection probabilities (`q:dsquared`)

- **Precision:** well-posed conditional on Conjecture 5.3.
- **Openness:** open with related work. Uniform selection is derived only for Abelian irreps in the approximate projected model; the 2026 general-group paper expressly does not provide the non-Abelian landing law. Neither a `d^2` nor `d^3` law for this ensemble was found.
- **Evidence:** [He et al. 2026](https://arxiv.org/abs/2606.02993), [Morwani et al. 2024](https://openreview.net/forum?id=i9wDX850jR).
- **Literal queries run:**
  - `nonabelian group composition neural network projected gradient flow landing probability irreducible representation d squared 2026`
  - `"selection probabilities" irreducible representation neural network group composition`
  - `site:arxiv.org 2026 nonabelian representation competition neuron random initialization group composition`

### Problem 5.5 — `S_3` with fixed architecture (`prob:s3`)

- **Precision:** well-posed. The silent-neuron clause correctly handles an open positive-probability inactive set; equality at a ReLU kink has Gaussian probability zero.
- **Openness:** open with related work. Morwani et al. give a static `L_{2,3}` margin characterization and experiments, and He et al. give a non-Abelian surrogate projected-flow alignment theorem. Neither proves ReLU purity with Euclidean decay nor the four-atom limiting selection law.
- **Evidence:** [Morwani et al. 2024](https://openreview.net/forum?id=i9wDX850jR), [He et al. 2026](https://arxiv.org/abs/2606.02993), [Chughtai et al.](https://arxiv.org/abs/2302.03025).
- **Literal queries run:**
  - `2024 2025 2026 S3 group multiplication neural network irreducible representation selection random initialization quadratic activation`
  - `site:arxiv.org S_3 group composition neural network representation selection gradient flow`
  - `site:openreview.net S3 group multiplication neural network standard representation sign representation`
  - `"S_3" "group composition" neural network irreducible 2026`

### Conjecture 5.6 — `S_3` double limit (`conj:s3`)

- **Precision:** well-posed under the global exceptional-`epsilon` convention, although spelling out whether `epsilon` is held fixed as `lambda -> 0` would improve it.
- **Openness:** open with related work. Morwani et al. show both nontrivial irreps occur in an `L_{2,3}` maximum-margin solution, but that does not predict the Euclidean-regularized ensemble. No dynamics theorem bridging this norm and double limit was found.
- **Evidence:** [Morwani et al. 2024](https://openreview.net/forum?id=i9wDX850jR), [Wei et al. 2019](https://arxiv.org/abs/1810.05369), [He et al. 2026](https://arxiv.org/abs/2606.02993).
- **Literal queries run:**
  - `2024 2025 2026 S3 group multiplication neural network irreducible representation selection random initialization quadratic activation`
  - `site:openreview.net S3 group multiplication neural network standard representation sign representation`
  - `"S_3" "group composition" neural network irreducible 2026`

### Problem 5.7 — Non-identifiability at width 128 (`prob:nonident`)

- **Precision:** well-posed. It asks for positive asymptotic mass rather than an informal difference of mechanisms.
- **Openness:** open with related work. Chughtai et al. report seed variation (including a 50-run aggregate), Stander et al. find coset mechanisms in the same broad architecture family, and Wu et al. analyze many `S_5` networks. None proves positive basin measure for two key sets under the continuous ensemble here.
- **Evidence:** [Chughtai et al.](https://arxiv.org/abs/2302.03025), [Stander et al. 2024](https://arxiv.org/abs/2312.06581), [Wu et al. 2025](https://arxiv.org/abs/2410.07476).
- **Literal queries run:**
  - `2024 2025 2026 S5 group composition neural network learned irreducible representations width 128 random seed nonidentifiability`
  - `site:openreview.net "S5" group multiplication neural network representation circuits`
  - `site:arxiv.org "S_5" neural network group composition representation theory`
  - `"width 128" "group composition" neural network representations`

### Question 5.8 — Exchangeability beyond symmetry (`q:exchangeable`)

- **Precision:** well-posed. Full permutation invariance is equivalent to conditional uniformity on each cardinality orbit whose cardinality event has positive probability.
- **Openness:** open with related work. Existing work observes or proves marginally uniform diversification in different regimes, but no paper found tests higher-order multiplicative structure of the selected subset or the conditional `k`-set law.
- **Evidence:** [Ding et al. 2024](https://openreview.net/forum?id=2WfiYQlZDa), [He et al. 2026](https://arxiv.org/abs/2606.02993).
- **Literal queries run:**
  - `2024 2025 2026 modular addition frequency selection exchangeability conditional uniform random subset frequencies neural network`
  - `"conditional" "surviving frequencies" modular addition neural network random seeds`
  - `"frequency classes" modular addition random initialization symmetry neural network`
  - `site:openreview.net modular addition frequency selection random seeds doubling frequencies`

### Problem 6.1 — The smallest case with competition (`start:c5`)

- **Precision:** well-posed. The architecture, loss, initialization, dimension, normalization, and requested probability are fixed.
- **Openness:** open with related work. He et al. and Kunin et al. analyze small-initialization, decoupled/projected, or wide regimes; no complete 30-dimensional phase portrait at width two and unit scale was found.
- **Evidence:** [He et al. 2026a](https://arxiv.org/abs/2602.16849), [He et al. 2026b](https://arxiv.org/abs/2606.02993), [Kunin et al. 2025](https://arxiv.org/abs/2506.06489).
- **Literal queries run:**
  - `2024 2025 2026 C5 modular addition width 2 quadratic neural network phase portrait gradient flow two neurons`
  - `"width 2" modular addition quadratic activation gradient flow frequencies`
  - `"C_5" "modular addition" "gradient flow" neural network`
  - `site:arxiv.org two neuron modular addition phase portrait frequency competition`

### Problem 6.2 — One rectifier neuron (`start:relu`)

- **Precision:** well-posed up to a null-set convention: on the complement of the strict-activity event, kink equalities can admit nonstationary Clarke choices, but those equalities have probability zero under the Gaussian initialization.
- **Openness:** open with related work. The closest modular-addition result quantifies ReLU harmonic leakage from a specially initialized single-frequency state; wide ReLU experiments find square-wave features. Generic single-ReLU convergence theory concerns different supervised tasks and does not establish Fourier purity here.
- **Evidence:** [He et al. 2026](https://arxiv.org/abs/2602.16849), [Swaroop 2026](https://arxiv.org/abs/2603.23784), [Lee et al.](https://arxiv.org/abs/2202.05510).
- **Literal queries run:**
  - `2024 2025 2026 one ReLU neuron modular addition random initialization alignment frequency gradient flow`
  - `"single neuron" ReLU modular addition Fourier alignment gradient flow`
  - `"one neuron" modular addition ReLU neural network representation frequency`
  - `site:arxiv.org ReLU modular addition random initialization Fourier neuron 2026`

### Problem 6.3 — Measure the law (`start:measure`)

- **Precision:** ill-posed as a reproducible numbered project, for the missing protocol choices listed in Finding 5. A repair is straightforward: publish an exact configuration table, fixed thresholds, integrator/optimizer and ReLU convention, stopping rule, raw seeds/checkpoints, and confidence intervals.
- **Openness:** open with related work. Recent studies add wide quadratic/ReLU mechanism data and many `S_5` models, but the requested cross-group, 1,000-seed empirical selection laws with the file's observables were not found.
- **Evidence:** [Wu et al. 2025](https://arxiv.org/abs/2410.07476), [He et al. 2026](https://arxiv.org/abs/2602.16849), [Swaroop 2026](https://arxiv.org/abs/2603.23784).
- **Literal queries run:**
  - `2024 2025 2026 empirical selection law modular addition 1000 seeds irreducible representations key sets S3 S4`
  - `modular addition hundreds seeds frequency histogram surviving frequencies 2025 2026`
  - `site:arxiv.org group composition empirical selection law random seeds frequencies key representations 2026`
  - `site:openreview.net group operation 1000 seeds representations frequency multiplicity`

## Machine-readable audit

```json
{
  "file": "open problems/representation-theory-learned-circuits.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Lemma 3.3 (lem:gcr)",
      "verdict": "correct",
      "note": "The unitary trace bound and joint-kernel uniqueness argument are complete and correct."
    },
    {
      "label": "Proposition 4.4 (prop:symmetry)",
      "verdict": "correct",
      "note": "Automorphism reindexing preserves the loss and Gaussian law and acts equivariantly on all stated observables."
    },
    {
      "label": "Global-flow and Clarke-selection claim (line 128)",
      "verdict": "correct-with-gaps",
      "note": "The mathematical claim is standard and appears correct, but the text omits citations and the compatibility argument needed to pass from compact finite-interval solution sets to one global measurable path selection."
    },
    {
      "label": "Remark 4.5 (rem:correctness)",
      "verdict": "correct-with-gaps",
      "note": "The S3 construction and lookup-table realization are correct; the uniform lower bound excluding an empty key set is valid but only sketched."
    }
  ],
  "items": [
    {
      "label": "Problem 5.1 (prob:law)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2606.02993",
        "https://arxiv.org/abs/2506.06489",
        "https://arxiv.org/abs/2602.03655"
      ],
      "note": "No fixed-weight-decay selection law was found. The claimed projected-flow foothold is only asymptotic for a Taylor-surrogate risk, and the zero network has a positive-probability attraction basin."
    },
    {
      "label": "Problem 5.2 (prob:sparse)",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/forum?id=2WfiYQlZDa",
        "https://arxiv.org/abs/2602.16849",
        "https://arxiv.org/abs/2603.23784"
      ],
      "note": "The signs of C_0 and tau_0 and the prime subsequence should be explicit. Existing results do not determine the requested ReLU spectral-count scaling."
    },
    {
      "label": "Conjecture 5.3 (conj:lln)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2606.02993",
        "https://arxiv.org/abs/2602.03655"
      ],
      "note": "No non-Abelian multiplicity LLN for the stated unconstrained flow was found. The prose's independence gloss is not implied by the formal LLN."
    },
    {
      "label": "Question 5.4 (q:dsquared)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2606.02993",
        "https://openreview.net/forum?id=i9wDX850jR"
      ],
      "note": "The Abelian surrogate projected model has uniform landing, but no non-Abelian d-squared or competing landing law for this ensemble was found."
    },
    {
      "label": "Problem 5.5 (prob:s3)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/forum?id=i9wDX850jR",
        "https://arxiv.org/abs/2606.02993",
        "https://arxiv.org/abs/2302.03025"
      ],
      "note": "Static L2,3-margin and surrogate projected-flow results are adjacent, but neither proves purity or the four-subset law for the defined weight-decayed ensemble."
    },
    {
      "label": "Conjecture 5.6 (conj:s3)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/forum?id=i9wDX850jR",
        "https://arxiv.org/abs/1810.05369"
      ],
      "note": "The statement remains open, but Morwani's L2,3 maximum-margin theorem does not predict the Euclidean-regularized ensemble used in the conjecture."
    },
    {
      "label": "Problem 5.7 (prob:nonident)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2302.03025",
        "https://arxiv.org/abs/2312.06581",
        "https://arxiv.org/abs/2410.07476"
      ],
      "note": "Many-seed empirical and mechanistic studies exist, but none proves that continuous Gaussian-initialized flow charges two distinct key sets."
    },
    {
      "label": "Question 5.8 (q:exchangeable)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/forum?id=2WfiYQlZDa",
        "https://arxiv.org/abs/2606.02993"
      ],
      "note": "No experiment or theorem found tests full conditional k-set uniformity versus only multiplicative symmetry."
    },
    {
      "label": "Problem 6.1 (start:c5)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2602.16849",
        "https://arxiv.org/abs/2606.02993",
        "https://arxiv.org/abs/2506.06489"
      ],
      "note": "No complete phase portrait or same-frequency probability for width two, C5, and unit-scale initialization was found."
    },
    {
      "label": "Problem 6.2 (start:relu)",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2602.16849",
        "https://arxiv.org/abs/2603.23784",
        "https://arxiv.org/abs/2202.05510"
      ],
      "note": "The exact random-start one-neuron modular-addition claim was not found; current ReLU modular theory starts from a special frequency and wide experiments are not a proof."
    },
    {
      "label": "Problem 6.3 (start:measure)",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2410.07476",
        "https://arxiv.org/abs/2602.16849",
        "https://arxiv.org/abs/2603.23784"
      ],
      "note": "The requested dataset was not found, and the item lacks exact thresholds, lambda grid, training dynamics, ReLU convention, stopping rule, and statistical protocol."
    }
  ],
  "attribution_issues": [
    "He et al. arXiv:2606.02993 prove asymptotic alignment and diversification for projected flow under the Taylor-surrogate risk R_ap; exact cross-entropy is compared only on finite horizons, contrary to lines 227, 254, 261, 295, 323, and 336.",
    "Morwani et al.'s Theorems 7 and 9 concern L_{2,3} maximum margin and L_{2,3}-regularized training, whereas Definition 3.2 uses Euclidean squared regularization; Wei et al.'s theorem preserves the chosen norm rather than changing it.",
    "The lottery-ticket theorem in arXiv:2602.16849 assumes small/specialized or controlled multi-frequency initialization and an early-stage decoupled approximation; full random-start ReLU evidence is empirical.",
    "Morwani et al.'s purity characterization permits zero neurons, so the file should say every nonzero or active neuron rather than every neuron."
  ],
  "confidence": "high"
}
```
