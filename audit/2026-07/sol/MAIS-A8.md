> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A8](../../../agendas/MAIS-A8/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Audit report: open problems/ood-generalization.tex

## Summary verdict

The elementary coin-line and linear-classifier results are mathematically sound: I found no proof error in Theorem 2.1, Lemma 3.2, Propositions 3.3 and 4.2–4.4, Theorem 4.1, or Example 4.5. The file nevertheless has significant publication-blocking issues. Most importantly, the finite-width ReLU “gradient flow” is not uniquely defined by invoking a Clarke differential inclusion, so seven of the central probabilities and stopping-time problems are not mathematical objects as written; the cited Lyu–Li paper does not establish the claimed well-posedness. Three statements advertised as open are in fact settled by short arguments in the file's own model: Conjecture 5.3 (kernel regime), conditional Conjecture 5.4 (mean-field regime), and both parts of Problem 6.1 (linear policy gradient). The monomial subproblem in Problem 5.8 is also immediately solvable. In addition, the explanation of “structural” KKT degeneracy at line 244 is false, logistic loss has no finite zero-loss parameter set as claimed at lines 71 and 314, Arora et al. 2019 does not prove the logistic-flow assertion attributed to it, and several directly relevant 2024–2026 results are missing. The correct overall verdict is therefore significant-issues, despite the correctness of the displayed elementary proofs.

## Findings, ordered by severity

### 1. The finite-width ReLU dynamics, and hence many numbered items, are not well-posed

**Locations:** lines 57–62, 150–154, 238–253, 279–289, 305–314, 321–345, and 363–365.

The sentence at line 62 says that ReLU gradient flow is “understood in the sense of the Clarke subdifferential” and cites Lyu and Li for well-posedness. A Clarke subgradient differential inclusion generally admits more than one absolutely continuous solution. It does not select a trajectory. Lyu and Li formulate results for trajectories satisfying a differential inclusion; they do not supply the uniqueness theorem needed here. The issue is not merely formal. Boursier, Pillaud-Vivien, and Flammarion explicitly note for shallow ReLU flow that the Cauchy–Lipschitz theorem does not apply and “uniqueness is not ensured”; they fix the derivative convention 1 on the strictly positive half-line and 0 otherwise, and still state their results for all flows satisfying the resulting equation. See [Lyu–Li, Gradient Descent Maximizes the Margin of Homogeneous Neural Networks](https://arxiv.org/abs/1906.05890) and [Boursier–Pillaud-Vivien–Flammarion, NeurIPS 2022, pp. 2–3](https://proceedings.neurips.cc/paper_files/paper/2022/file/7eeb9af3eb1f48e29c05e8dd3342b286-Paper-Conference.pdf).

The probability q averages only over initialization. It does not average over, or specify, a measurable selection of differential-inclusion solutions. Thus two allowed solutions from the same initialization can in principle give different probe signs. The assertion that “nothing below changes” under a fixed smooth approximation does not repair this: no approximation is named, and different smoothings define different finite-width dynamics, tangent kernels, and selection maps. One must either specify a particular activation, specify a single-valued derivative convention together with an existence/uniqueness result, or quantify over all solutions.

Consequences for numbered statements:

- Problem 5.1, Conjecture 5.2, Question 5.5, Problem 5.6, Question 5.9, Problem 6.3, and Problem 7.4 are ill-posed because their q, q-RL, or stopping-time predictor is not uniquely defined.
- Problem 5.7 is well-defined for its linear part, but its final “same question for the two-layer architecture” inherits the missing convention and is not itself a complete statement.
- The kernel flow in Conjecture 5.3 is a separate, finite-dimensional function-space ODE and is well-defined.
- The mean-field flow in Conjecture 5.4 is identified by reference to the Chizat–Bach construction, although its claimed equivalence between predictor convergence and weak convergence of representing measures is false; see Finding 3.
- Line 325 is also false as written: J is a polynomial in sigmoid values, but as a function of two-layer ReLU parameters it is only piecewise smooth / locally Lipschitz, not smooth.

### 2. Conjecture 5.3 (kernel regime) is resolved by a direct monotonicity argument

**Locations:** lines 257–269 and the openness claims at lines 238, 349, and 379.

Write the L training inputs as x_i, their positive weights as omega_i, and the kernel-flow solution as

f_t(x) = f_0(x) + sum_i beta_i(t) K(x_i,x),

where

beta_i'(t) = omega_i / (1 + exp(f_t(x_i))) > 0.

If all beta_i were bounded, every training value f_t(x_i) would be bounded because there are finitely many points. Each beta_i' would then eventually be bounded below by a positive constant, a contradiction. Hence at least one beta_i tends to infinity. Every coefficient is nonnegative. For the two-layer ReLU NTK, K(x_i,x-star) is strictly positive because each training input and the probe have positive inner product (indeed at least 1); the usual two-layer NTK formula is a sum of nonnegative arc-cosine terms and is positive at an acute angle. It follows immediately that

f_t(x-star) = f_0(x-star) + sum_i beta_i(t) K(x_i,x-star) tends to positive infinity.

This proves the exact conclusion of Conjecture 5.3 almost surely (the finite collection of initial GP values is finite almost surely). No RKHS max-margin theorem, strict positive definiteness, or limit interchange is required for the infinite-width statement itself. [Carvalho et al. 2024](https://arxiv.org/abs/2404.12928) gives a modern general strict-positivity result for NTKs, but even that stronger fact is unnecessary here. Problem 7.3 still has genuinely open finite-width/interchange and positive-diversity components.

### 3. Conditional Conjecture 5.4 (mean-field regime) is also resolved

**Locations:** lines 271–275.

Let x_0 = (1,0,L), one of the training inputs. For every two-layer representation,

f(x_0) <= norm-var(f) times norm-2(x_0),

by the triangle inequality, positive homogeneity of ReLU, and Cauchy–Schwarz. Therefore a variation-norm-one predictor cannot have training margin exceeding norm-2(x_0). The single unit

f_0(x) = ReLU(x_0 dot x / norm-2(x_0))

has variation norm one and takes the value norm-2(x_0) on every training input (1,p,L), because x_0 dot (1,p,L) = 1 + L squared. It is thus max-margin.

Moreover equality in the point-evaluation bound forces every nonzero representing atom to have a nonnegative output coefficient and its hidden direction parallel to x_0. Thus the optimizing predictor is the same ray, up to the normalization already fixed. At the probe (1,p-star,0) it has value 1 / norm-2(x_0), which is strictly positive. Combined with the max-margin characterization in [Chizat–Bach 2020](https://proceedings.mlr.press/v125/chizat20a.html), this establishes the conjecture under its stated convergence premise.

There is a precision defect in the premise: pointwise convergence of predictors is not “equivalent” to weak convergence of normalized representing measures. Many measures can represent the same predictor, and pointwise convergence alone does not give tightness or identify a weak measure limit. The two alternatives must be separated.

### 4. Problem 6.1 (linear policy gradient) is resolved for every finite initialization

**Locations:** lines 327–331 and the blanket openness claim near line 379.

Let z_p = w_0 + p w_1 + L w_2 for nonterminal training positions p = 0,...,L-1, and let g_p = partial J_0 / partial z_p. Increasing the probability of stepping right at any p cannot lower the probability of reaching L within the remaining horizon: any path from p-1 to L must first pass p+1 and therefore reaches p+1 with fewer steps left. The policy-gradient advantage of right over left is consequently nonnegative, so g_p >= 0. It is strictly positive for p=L-1 at every finite w, since starting at L-1 has positive probability and a right step hits the coin immediately while a left step has a strictly smaller finite-horizon success probability.

Set B = w_0 + L w_2. The feature vectors are (1,p,L), so the gradient flow satisfies

B' = (1 + L squared) sum_p g_p > 0,

w_1' = sum_p p g_p >= 0,

and w_2 - L w_0 is invariant. Also

w_1' <= ((L-1)/(1+L squared)) B'.

If B were bounded, then w_1 would be bounded, the invariant would make all components of w bounded, and monotonicity would make w converge to a finite limit. Continuity would then leave g_(L-1) strictly positive at that limit, contradicting bounded B. Hence B tends to positive infinity. The invariant gives w_0 tending to positive infinity, while w_1 is nondecreasing and therefore bounded below by its initial value. Thus every training logit B+p w_1 tends to positive infinity, J_0 tends to 1, and the probe logit w_0+p-star w_1 also tends to positive infinity.

Both requested conclusions hold for every finite initialization, stronger than “almost every.” The nearby literature cited in the file does not appear to state this coin-line calculation, so this is best described as an elementary resolution exposed by the audit, not a priority claim for another paper.

### 5. The line-244 explanation of parameter-space max-margin degeneracy is false

**Location:** line 244.

On the training inputs x_p=(1,p,L), the vector n=(L,0,-1) is invisible: n dot x_p=0. Shifting a hidden weight u to u+delta n therefore leaves all training preactivations unchanged. But the parameter-space margin program penalizes the Euclidean parameter norm. At a norm-minimizing representative u dot n=0, and

norm-2(u+delta n) squared = norm-2(u) squared + delta squared norm-2(n) squared

for nonzero delta. Thus the shifted parameter is not margin-optimal. Loss degeneracy is not norm-margin degeneracy. An arbitrary initial component in the invisible direction can remain bounded under gradient dynamics, but it is washed out after normalization when the norm diverges; that is a different issue. There may still be multiple nonconvex KKT points, but the stated “indeed” argument does not establish them and should not be used as the motivation for Problems 5.1–5.2.

### 6. “Zero logistic loss” and the singular-learning-theory interpretation are wrong

**Locations:** lines 71 and 313–314.

For logistic loss ell(z)=log(1+exp(-z)), ell(z)>0 at every finite z. A separable classifier has infimum zero only along parameters whose norm diverges; Theorem 4.1 itself states that divergence. Therefore there is no positive-dimensional finite “zero-loss parameter” set of the kind asserted at lines 71 and 314. Zhang et al.'s interpolation theorem establishes exact interpolation / zero training error for arbitrary real labels, not a finite zero of the logistic objective used in this note.

This matters for the appeal to singular learning theory. Standard local-volume reasoning around a finite singular zero set cannot simply be transferred to an infimum at infinity. The paragraph may be reformulated in terms of zero classification error or asymptotically vanishing loss, but the current claimed geometric object does not exist.

There is a second scope gap: Theorem 2.1 accurately quotes Zhang et al.'s biased form with offsets b_j, whereas equation (2.1) is written without explicit biases. The coin encodings include a constant coordinate and hence can absorb a bias, but the general background inference for arbitrary x in R^d needs that augmentation stated.

### 7. Arora et al. 2019 does not support the logistic-flow convergence attributed to it

**Location:** line 262.

[Arora et al., On Exact Computation with an Infinitely Wide Neural Net](https://arxiv.org/abs/1904.11955) proves a nonasymptotic equivalence to NTK kernel regression in its training theorem; it is a squared-loss/kernel-regression result. It does not prove that this exact ReLU network under logistic-loss gradient flow converges, for each fixed t, to the displayed logistic kernel ODE. The assertion may be obtainable from other lazy-training results after checking their hypotheses, but the cited paper is not evidence for the statement as written. The unspecified “fixed smooth approximation” also changes the kernel and cannot be used to justify an assertion explicitly made for the ReLU NTK.

### 8. Problem 5.8's monomial family is already solved

**Locations:** lines 301–303.

Let psi_k(p,c) contain all monomials p^i c^j with i+j<=k. For the all-positive epsilon=0 training data, the unique maximum-margin vector has the KKT form

w-hat = sum_p alpha_p psi_k(p,L), with alpha_p >= 0 and at least one alpha_p > 0.

At the probe,

psi_k(p,L) dot psi_k(p-star,0) = sum from i=0 to k of (p p-star)^i > 0,

because exactly the j=0 monomials survive. Therefore w-hat dot psi_k(p-star,0)>0 for every nonnegative integer k and every L>=4. The entire monomial family selects the proxy. The more ambitious request for a useful structural criterion on arbitrary feature maps remains open-ended, but the concrete family advertised as the first task is not open.

### 9. The Bayesian-sampler test omits the closest direct comparison and does not actually train with SGD

**Locations:** lines 305–314.

Question 5.9 motivates itself with a claim about stochastic gradient descent but defines q-ntk using full-batch gradient flow, with randomness only in initialization. Those are distinct sampling procedures. A disagreement with the NNGP sign-conditioned posterior would test the distribution induced by random initialization plus deterministic flow, not by itself the stated SGD-as-Bayesian-sampler hypothesis.

The nearest prior work is [Bernstein and Yue, On the Implicit Biases of Architecture & Gradient Descent, ICLR 2022](https://openreview.net/forum?id=eOdSD0B5TE), which directly compares the NNGP posterior to finite-width gradient descent and finds that gradient descent adds a large-margin selection bias. That paper does not compute this coin-line Q(L), so the numerical marginal remains useful, but the conceptual discrimination is not new and the paper should be discussed. [Yu, Tian, and Chen 2025](https://arxiv.org/abs/2504.11130) additionally proves that for finite-width networks trained with cross-entropy, the empirical NTK cannot stay uniformly close to the infinite-width NTK for all time; this bears directly on the order of limits used here.

The Gaussian calculation itself is sound: nonsingularity of the joint training-plus-probe Gram matrix, rather than merely the training Gram matrix, is what gives positive conditional variance and hence Q(L)<1.

### 10. The July 2026 openness survey misses directly relevant 2024–2026 work

**Locations:** lines 367–379 and, through the blanket claim, all numbered network and RL items.

The following do not solve the exact finite-width coin-line statements, but they substantially overlap them and should prevent “no progress” or novelty claims without qualification:

- [Brown and Young, Understanding Goal Generalisation in Sequential Reinforcement Learning, May 2026](https://arxiv.org/abs/2605.23565) studies more than 100 sequential training pipelines across more than 250 OOD environments and introduces latent policy gradients to predict OOD goal behavior. It is unusually direct overlap for Problems 6.3 and 7.4 and for the paper's overall framing.
- [Yu, Tian, and Chen, ICLR 2025](https://arxiv.org/abs/2504.11130) proves divergence of the empirical NTK from its initialization-time NTK under long-time cross-entropy training, directly constraining Problem 7.3 and Question 5.9.
- [Carvalho et al. 2024](https://arxiv.org/abs/2404.12928) proves strict positive definiteness of feedforward NTKs for nonpolynomial activations, relevant to Conjecture 5.3 and Problem 7.3.
- [Kumar and Haupt 2024](https://arxiv.org/abs/2402.09226) and [Min, Mallada, and Vidal 2024](https://arxiv.org/abs/2307.12851) analyze directional convergence / early alignment for small-initialization two-layer ReLU flows, directly relevant to Problems 5.1–5.2.
- [Yang et al., AISTATS 2024](https://proceedings.mlr.press/v238/yang24c.html), [Qiu, Kuang, and Goel, ICML 2024](https://proceedings.mlr.press/v235/qiu24e.html), and [Zhang et al., ICML 2024](https://arxiv.org/abs/2406.03345) give theoretical feature-learning accounts of early spurious-feature reliance and OOD failure, relevant to Problems 5.6–5.7.
- [Xu et al., How Neural Networks Extrapolate](https://arxiv.org/abs/2009.11848) gives architecture/feature conditions for ReLU extrapolation and should be discussed around Problem 5.8.
- [Kumar, Viqueira, and Greenwald, Zero Collapse, May 2026](https://arxiv.org/abs/2605.30896) gives a neighboring vanishing-reward-signal failure mode for policy gradients, relevant to Question 6.2.

The source already cites June 2026 work, so these May 2026 omissions cannot be explained by a pre-2026 cutoff. None of these papers appears to supply the exact coin-line selection probability, but they materially change the “to my knowledge, a first” and neighboring-literature presentation.

### 11. Remaining statement-level precision issues

**Problem 5.7 (lines 291–297), minor issues.** The linear crossover time is well-defined once a particular sufficiently small step size is fixed. The last sentence, “Then pose the same question for the two-layer architecture,” is not a mathematical statement: it does not replace the discrete k by a flow time, state a ReLU solution convention, or specify what happens if the probe sign changes repeatedly.

**Question 6.2 (lines 335–337), minor issues.** The file globally restricts epsilon to rational values, whereas “for every epsilon in (0,bar-epsilon]” naturally quantifies over all reals. Both readings define sensible but different statements. The rationality restriction is unnecessary for policy gradient and should be discharged or the quantifier should explicitly say rational epsilon.

**Problem 6.3 (lines 339–345), ill-posed independently of ReLU nonuniqueness.** On an initialization for which tau_delta=infinity, theta(tau_delta) is undefined. Saying that proving finiteness is part of the problem does not define the displayed random event before that proof. One can define a joint event with tau_delta<infinity, condition on finiteness, or assign an explicit cemetery value.

**Problem 7.1 (lines 351–353), minor issues.** Two inequivalent readings of “boundary action” and “exact test return” are available. The file's earlier convention takes the eventual sign and produces a deterministic argmax policy. But the boundary logit is bounded, so the limiting logistic policy remains stochastic with probability sigma(d-infinity), and its return differs from the deterministic-sign policy's return. A possible d-infinity=0 tie is also unhandled.

**Problem 7.3 (lines 359–361), minor issues.** “Handle the interchange of limits” does not specify the quantity or topology: uniform convergence of the empirical NTK, convergence of the probe value, or convergence only of its sign are inequivalent. This matters because [Yu et al. 2025](https://arxiv.org/abs/2504.11130) rules out uniform-in-time NTK approximation on training samples under cross-entropy at every finite width, while a weaker sign conclusion at this one probe could still hold.

### 12. Proof audit: all displayed elementary results are correct

**Theorem 2.1 (lines 67–69): correct.** The quoted Zhang et al. construction has n output weights, n offsets, and one shared d-dimensional direction, totaling 2n+d. The nearby architecture/scope and zero-logistic-loss inferences are separate errors noted above.

**Lemma 3.2 (lines 107–118): correct.** Under mu_0 both relevant policies move right on every nonterminal visited state. Under the test law the right-only policy succeeds exactly on c>=p_0. Counting the upper triangular pairs gives (L+2)/(2(L+1)). At p=c the episode is already terminal; the phrase “either action” is harmless only under this terminal-state convention.

**Proposition 3.3 (lines 158–164): correct.** With c=L fixed, neither the return nor cloning loss depends on a tabular coordinate with c not equal to L, so the probe coordinate has identically zero derivative.

**Theorem 4.1 (lines 172–179): correct.** This is the standard small-step separable-logistic implicit-bias statement of Soudry et al. Replacing rational weights by integer repetitions and an overall time/step rescaling is valid.

**Proposition 4.2 (lines 185–195): correct.** The vector (1,0,L)/(1+L squared) is feasible and is certified by the p=0 constraint; strict convexity gives uniqueness. Its dot product with every state encoding is strictly positive.

**Proposition 4.3 (lines 201–211): correct.** The candidate (0,-1,1) has margin |c-p|. The displayed positive coefficients have equal total mass and matching first moments for L>=4, yielding a valid KKT certificate. The probe margin is negative.

**Proposition 4.4 (lines 213–219): correct.** The sole support vector (1,1) certifies (1/2,1/2), and at p-star>=2 the probe score 1-p-star is negative.

**Example 4.5 (lines 221–223): correct.** Symmetry/KKT gives w_p=1/(L+1) and v_L=L/(L+1), with all unseen coordinates zero, and hence a positive probe score.

## Item-by-item precision and openness assessment

1. **Problem 5.1, The selection map:** ill-posed because finite-width ReLU flow is not uniquely selected. Related small-initialization/alignment work exists, but I found no exact coin-line finite-width solution.
2. **Conjecture 5.2, The proxy wins at epsilon=0:** ill-posed for the same reason. Substantial related implicit-bias/alignment work exists; no exact published resolution found.
3. **Conjecture 5.3, Kernel regime:** well-posed and resolved by the positive-coefficient kernel-flow argument in Finding 2.
4. **Conjecture 5.4, Mean-field regime:** minor issues because predictor convergence is not equivalent to weak measure convergence; conditional conclusion resolved by Finding 3.
5. **Question 5.5, Is there any coin-lover?:** ill-posed because the probability is not defined without a flow selection; related finite-width initialization-bias work does not answer the exact existential question.
6. **Problem 5.6, Diversity at the level of networks:** ill-posed in its finite-width part; the kernel SVM part is meaningful. Several 2024 spurious-feature/OOD analyses are related, but no exact epsilon-positive coin kernel computation was found.
7. **Problem 5.7, The crossover time:** minor issues because the network add-on is only an instruction, not a statement. The linear question appears open; recent theory on temporal spurious-feature dynamics is closely related.
8. **Problem 5.8, Which representations misgeneralize?:** minor issues because k's domain is implicit and “a structural condition” is not a sharply delimited deliverable. The monomial task is resolved in Finding 8; the broad arbitrary-feature criterion remains open.
9. **Question 5.9, The Bayesian-sampler test:** ill-posed because the finite-width ReLU trajectory is not defined; it also substitutes full-batch flow for the SGD named in the hypothesis. Bernstein–Yue and Yu–Tian–Chen are direct related work; the exact coin orthant probability comparison remains open.
10. **Problem 6.1, Linear policy gradient, no diversity:** well-posed and resolved by Finding 4.
11. **Question 6.2, Exploration starvation:** minor rational/all-real epsilon ambiguity. The exact statement appears open, with related work on exploration-controlled extrapolation, latent policy gradients, and vanishing-signal traps.
12. **Problem 6.3, The misgeneralization curve:** ill-posed because both the ReLU flow and theta(tau_delta) on tau_delta=infinity are undefined. Brown–Young is substantial direct empirical/methodological overlap, not an exact solution.
13. **Problem 7.1, The boundary residual:** minor ambiguity between deterministic sign policy and limiting stochastic logistic policy. I found no paper computing this exact two-dimensional recursion; residual and low-dimensional logistic analyses are related.
14. **Problem 7.2, The crossover asymptotics:** well-posed (with the fixed-step convention inherited from Problem 5.7). I found related transient/spurious-feature analyses but no exact asymptotic for this dataset.
15. **Problem 7.3, Kernel-regime selection, end to end:** minor issues because the topology/quantity for limit interchange is unspecified. The infinite-width epsilon=0 claim is resolved; the finite-width interchange and epsilon-positive SVM parts remain open, with a strong obstruction from Yu et al.
16. **Problem 7.4, The atlas:** ill-posed until finite-width ReLU trajectories are specified. Brown–Young is atlas-like related work at a much larger empirical scale, but no exact coin-line atlas was found.

## Per-item literature search-query log

The following are the literal queries used. Searches were run across general web/arXiv indexing and venue pages; source pages were then opened for the works cited above.

### Problem 5.1

- "coin line" two-layer ReLU gradient flow misgeneralization
- two-layer ReLU all positive labels off-training extrapolation initialization selection
- 2024 2025 2026 finite width ReLU implicit bias initialization KKT direction selection
- goal misgeneralization behavior cloning gradient descent theory two-layer network

### Conjecture 5.2

- wide unnormalized two-layer ReLU logistic loss all positive labels proxy feature implicit bias
- infinite width fixed initialization scale feature selection ReLU logistic 2025
- two homogeneous network small initialization directional convergence KKT 2024
- fixed width two layer ReLU logistic loss implicit bias initialization 2026

### Conjecture 5.3

- logistic gradient flow reproducing kernel Hilbert space separable data maximum margin theorem
- implicit bias kernel gradient descent logistic loss RKHS max margin
- 2024 2025 RKHS gradient flow logistic loss converges maximum margin direction
- ReLU neural tangent kernel strictly positive definite nonparallel inputs theorem

### Conjecture 5.4

- variation norm max margin two layer ReLU all positive labels single neuron optimizer
- Chizat Bach mean field max margin variation norm uniqueness
- 2024 2025 mean field implicit bias logistic loss variation norm
- Barron variation norm point evaluation inequality ReLU

### Question 5.5

- finite width ReLU initialization scale off distribution sign probability goal misgeneralization
- coin lover network goal misgeneralization initialization
- neural network extrapolation all positive labels initialization two layer ReLU
- standard two layer ReLU goal misgeneralization width initialization

### Problem 5.6

- kernel SVM spurious feature rare counterexamples extrapolation ReLU NTK
- 2024 neural tangent kernel spurious correlations OOD
- two-layer networks diversity rare counterexamples goal misgeneralization
- kernel max margin coin position proxy goal

### Problem 5.7

- logistic regression rare examples crossover time epsilon implicit bias max margin
- gradient descent separable logistic imbalanced data transient time rare class
- 2024 2025 gradient descent spurious feature rare minority feature learning time
- Sagawa overparameterization spurious correlation fraction minority dynamics

### Problem 5.8

- maximum margin polynomial features extrapolation monomial encoding all positive labels
- feature map criterion max margin OOD spurious coordinate
- kernel extrapolation geometry feature encoding implicit bias 2024
- Nagarajan Andreassen Neyshabur OOD max margin geometric skew

### Question 5.9

- SGD Bayesian sampler NNGP posterior orthant probability margin Bernstein Yue
- 2024 2025 SGD Bayesian sampler function distribution GP posterior classification
- NNGP posterior versus gradient descent margin implicit bias Bernstein Yue
- finite width NTK logistic long time interchange limits 2025

### Problem 6.1

- policy gradient linear function approximation deterministic chain global convergence softmax MDP
- 2024 2025 implicit bias policy gradient linear MDP extrapolation
- policy gradient goal misgeneralization linear policy coin line
- softmax policy gradient linear function approximation MDP convergence conditions

### Question 6.2

- exploration starvation policy gradient rare states vanishing signal proxy goal
- policy gradient rare rewarding trajectories vanishing gradient exploration 2024 2025
- goal misgeneralization exploration training diversity theory
- latent policy gradients goal generalisation 2026

### Problem 6.3

- goal misgeneralization diversity curve two layer policy gradient CoinRun
- CoinRun randomize coin percentage theory training curve
- 2024 2025 goal misgeneralization training diversity curve
- "Understanding Goal Generalisation" sequential reinforcement learning 2026 diversity

### Problem 7.1

- Soudry bounded residual single support vector initialization step size exact limit logistic regression
- logistic regression max margin residual initialization dependence boundary point
- Ji Telgarsky residual bounded convergence support vectors not span
- 2024 implicit bias residual orthogonal max margin initialization

### Problem 7.2

- logistic regression rare examples crossover time epsilon implicit bias max margin
- gradient descent separable logistic imbalanced data transient time rare class
- 2024 2025 gradient descent spurious feature rare minority feature learning time
- grokking transition lazy rich training dynamics rare feature crossover

### Problem 7.3

- 2025 empirical NTK divergence classification cross entropy long time infinite width
- "Divergence of Empirical NTK" classification problems
- long time neural tangent kernel logistic loss finite width infinite width limits do not commute
- 2024 2025 lazy training cross entropy NTK drift classification

### Problem 7.4

- coin line goal misgeneralization selection map simulation two layer ReLU
- two layer ReLU coin collecting toy selection map
- goal misgeneralization atlas width initialization scale diversity
- Gaussian process posterior CoinRun proxy

## Machine-readable verdict

```json
{
  "file": "open problems/ood-generalization.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Theorem 2.1",
      "verdict": "correct",
      "note": "The Zhang et al. interpolation theorem is accurately stated. The nearby inference to a finite zero-logistic-loss set and the bias-free architecture scope are separate background errors."
    },
    {
      "label": "Lemma 3.2",
      "verdict": "correct",
      "note": "The right-only policy succeeds exactly when c is at least p0, giving (L+2)/(2(L+1)); the coin-tracking policy always succeeds."
    },
    {
      "label": "Proposition 3.3",
      "verdict": "correct",
      "note": "At epsilon zero, neither objective depends on tabular coordinates with c not equal to L, so the probe coordinate is frozen."
    },
    {
      "label": "Theorem 4.1",
      "verdict": "correct",
      "note": "This is the standard small-step separable logistic implicit-bias theorem; rational positive weights can be represented by repeated examples and an overall step rescaling."
    },
    {
      "label": "Proposition 4.2",
      "verdict": "correct",
      "note": "The displayed vector is feasible, has a valid one-point KKT certificate, is unique by strict convexity, and has positive score at every state."
    },
    {
      "label": "Proposition 4.3",
      "verdict": "correct",
      "note": "The feasibility and KKT moment-matching certificate are valid for L at least 4, and the probe score is negative."
    },
    {
      "label": "Proposition 4.4",
      "verdict": "correct",
      "note": "The support vector (1,1) certifies (1/2,1/2), and the probe score is negative for the stated L."
    },
    {
      "label": "Example 4.5",
      "verdict": "correct",
      "note": "The symmetric one-hot optimum and its positive probe score are computed correctly."
    }
  ],
  "items": [
    {
      "label": "Problem 5.1",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/1906.05890",
        "https://arxiv.org/abs/2307.12851",
        "https://arxiv.org/abs/2402.09226"
      ],
      "note": "A Clarke differential inclusion does not select a unique finite-width ReLU trajectory, while q averages only over initialization. Related alignment and small-initialization results do not solve the exact coin-line selection map."
    },
    {
      "label": "Conjecture 5.2",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2402.09226",
        "https://arxiv.org/abs/2410.19139",
        "https://arxiv.org/abs/2510.21078"
      ],
      "note": "The probability is undefined without a ReLU flow-selection convention. Recent initialization and directional-bias results overlap but do not establish this exact double-limit claim."
    },
    {
      "label": "Conjecture 5.3",
      "precision": "well-posed",
      "openness": "resolved",
      "citations": [
        "https://arxiv.org/abs/2404.12928",
        "https://proceedings.mlr.press/v125/chizat20a.html"
      ],
      "note": "Writing the kernel trajectory with nonnegative increasing coefficients shows at least one coefficient diverges; strict positivity of every training-probe kernel value then forces the probe value to positive infinity."
    },
    {
      "label": "Conjecture 5.4",
      "precision": "minor-issues",
      "openness": "resolved",
      "citations": [
        "https://proceedings.mlr.press/v125/chizat20a.html"
      ],
      "note": "Pointwise predictor convergence is not equivalent to weak convergence of representing measures. Under the stated max-margin convergence premise, the point-evaluation bound is tight only for the single direction (1,0,L), which is positive at the probe."
    },
    {
      "label": "Question 5.5",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2307.12851",
        "https://arxiv.org/abs/2402.09226",
        "https://arxiv.org/abs/2410.19139"
      ],
      "note": "The existential probability is undefined until a unique ReLU trajectory is specified. No exact published coin-lover result was found."
    },
    {
      "label": "Problem 5.6",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2406.03345",
        "https://proceedings.mlr.press/v238/yang24c.html",
        "https://proceedings.mlr.press/v235/qiu24e.html"
      ],
      "note": "The finite-width limit uses the undefined ReLU flow; the kernel SVM half is meaningful. Recent spurious-feature and feature-contamination analyses substantially overlap but do not compute this dataset."
    },
    {
      "label": "Problem 5.7",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.mlr.press/v238/yang24c.html",
        "https://proceedings.mlr.press/v235/qiu24e.html",
        "https://arxiv.org/abs/2406.03345"
      ],
      "note": "The linear crossover is well-defined for a fixed small step, but the final two-layer instruction does not define a time variable or flow convention. No exact epsilon asymptotic was found."
    },
    {
      "label": "Problem 5.8",
      "precision": "minor-issues",
      "openness": "possibly-resolved",
      "citations": [
        "https://arxiv.org/abs/2009.11848",
        "https://arxiv.org/abs/2010.15775"
      ],
      "note": "The monomial subproblem is fully resolved: all training-probe feature inner products are positive, so every max-margin KKT combination selects the proxy. The requested general structural criterion remains broad and open."
    },
    {
      "label": "Question 5.9",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://openreview.net/forum?id=eOdSD0B5TE",
        "https://arxiv.org/abs/2110.04274",
        "https://arxiv.org/abs/2504.11130"
      ],
      "note": "The finite-width ReLU trajectory is not uniquely defined, and full-batch flow is not the SGD sampler named in the motivation. Bernstein and Yue directly compare NNGP posterior bias with gradient-descent margin bias; the exact coin marginal remains uncomputed."
    },
    {
      "label": "Problem 6.1",
      "precision": "well-posed",
      "openness": "resolved",
      "citations": [
        "https://arxiv.org/abs/2605.24939",
        "https://arxiv.org/abs/2402.07875"
      ],
      "note": "A direct monotonicity argument gives nonnegative per-state logit gradients, a strictly increasing aggregate B, an invariant w2-Lw0, and divergence of both training and probe logits to positive infinity for every finite initialization."
    },
    {
      "label": "Question 6.2",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2402.07875",
        "https://arxiv.org/abs/2605.23565",
        "https://arxiv.org/abs/2605.30896"
      ],
      "note": "The global rational-epsilon restriction conflicts with the natural all-real interval quantifier. Related work treats exploration-controlled extrapolation and vanishing policy-gradient signals, not this exact lower bound."
    },
    {
      "label": "Problem 6.3",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2605.23565",
        "https://arxiv.org/abs/2105.14111"
      ],
      "note": "The ReLU trajectory is not selected and theta(tau_delta) is undefined on tau_delta equal to infinity. Brown and Young provide substantial predictive goal-generalization overlap but not this coin-line curve."
    },
    {
      "label": "Problem 7.1",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/1803.07300",
        "https://arxiv.org/abs/2602.12471"
      ],
      "note": "The deterministic sign action and the limiting stochastic logistic policy give different returns, and the zero-residual tie is unspecified. No exact solution of this recursion was found."
    },
    {
      "label": "Problem 7.2",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.mlr.press/v238/yang24c.html",
        "https://proceedings.mlr.press/v235/qiu24e.html",
        "https://arxiv.org/abs/2005.04345"
      ],
      "note": "The fixed-step linear asymptotic is precise. Transient spurious-feature and minority-dynamics work is related, but no exact exponent for this coin dataset was found."
    },
    {
      "label": "Problem 7.3",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2504.11130",
        "https://arxiv.org/abs/2404.12928",
        "https://proceedings.mlr.press/v125/chizat20a.html"
      ],
      "note": "The infinite-width epsilon-zero sign claim is resolved directly, but the finite-width limit interchange and epsilon-positive kernel SVM remain. The required topology or observable for interchange is unspecified, and uniform-in-time NTK approximation is obstructed by Yu et al."
    },
    {
      "label": "Problem 7.4",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2605.23565",
        "https://arxiv.org/abs/2105.14111"
      ],
      "note": "The requested finite-width maps depend on an unspecified ReLU flow selection. Brown and Young provide atlas-like OOD goal-generalization experiments, but no exact coin-line atlas was found."
    }
  ],
  "attribution_issues": [
    "Line 62 attributes well-posedness of nonsmooth ReLU gradient flow to Lyu and Li 2020, but that work does not establish the uniqueness needed to define q.",
    "Line 262 attributes fixed-time ReLU NTK convergence for the displayed logistic gradient flow to Arora et al. 2019, whose training-equivalence theorem is for squared-loss kernel regression.",
    "Lines 238, 349, and 379 present Conjectures 5.3 and 5.4 and Problem 6.1 as open although each has a short direct resolution in this model; Problem 5.8's monomial component is also immediate.",
    "Question 5.9 omits Bernstein and Yue 2022, a direct NNGP-posterior versus finite-width-gradient-descent comparison showing an additional margin bias.",
    "The July 2026 related-work and novelty discussion omits Brown and Young 2026, Yu et al. 2025, Carvalho et al. 2024, and several 2024 theoretical spurious-feature and ReLU-alignment papers that materially overlap the numbered items.",
    "Theorem 2.1 uses biased ReLU units while equation (2.1) is bias-free; the coin encodings repair this through a constant coordinate, but the general extrapolation from the cited theorem does not state that augmentation."
  ],
  "confidence": "high"
}
```
