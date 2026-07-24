> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A2](../../../A2/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Audit report: `behavioral-tomography.tex`

## Summary verdict

**Significant issues.** The note contains a serious false specialization of Richens--Everitt: its Theorem 2.4 removes the source theorem's ability to mask observed inputs, and the stated conclusion then fails on an open, positive-measure set of domain-dependent diagrams. A two-variable counterexample is given below, so both the exact and approximate clauses, as well as the claims at lines 185, 220, and 340 that identify this result with injectivity of the note's behavioral transform, need human correction before publication. The cited Richens--Abel--Bellot--Everitt bound is accurately stated, and Proposition 3.2 is correct. Remark 3.3 has a repairable gap because its transcript count proves a deterministic/high-probability bound, whereas the defined minimax risk is expected loss. Among the fifteen numbered open items I found no resolution in searches through 14 July 2026; all have substantial related work, including a June 2026 paper omitted from the survey, *Inverting the Bellman Equation: From Q-Values to World Models*. Several items nevertheless need precision repairs: the general-agent identified set uses equality of whole policies despite declaring that only first actions are observed; the Boltzmann problem asks for the wrong large-`beta` behavior; and Problems 4.2--4.6, 4.13, 5.2, and 5.3 contain class, quantifier, or degeneracy ambiguities.

## Findings, ordered by severity

### 1. Theorem 2.4 is false for the interventions defined in this file

**Location:** `behavioral-tomography.tex:106-114`, with consequences at `:185`, `:220`, `:340`, and `:357`.

The cited Richens--Everitt result does not quantify only over the local chance-variable interventions in Definition 2.2. Its proof also changes the decision's input set: the paper explicitly permits a shifted diagram with a subset of the original decision parents, and Lemma 4 invokes **input masking** before extracting the model. See the intervention definition and Theorem 1 in the [official ICLR paper](https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf), especially pp. 5--6, and the input-masking step in Lemma 4, pp. 18--19. Definition 2.2 of the note only transforms chance-variable mechanisms and keeps the observation set fixed.

Here is a counterexample to the note's exact clause. Let the chance variables be `O,H`, let the agent observe `O`, let the graph be `O -> H`, and take both `O,H` as utility parents. Write

\[
g(o,h)=u(1,o,h)-u(0,o,h).
\]

Choose utility values satisfying

\[
g(0,0)<0<g(0,1),\qquad g(1,0)>0,\quad g(1,1)>0.
\]

Take all causal probabilities in the interior and vary only
`b=P(H=1 | O=1)` over a nontrivial interval, holding the other entries fixed. At observation `O=1`, action 1 is strictly optimal under every profile having positive mass there, whatever `b` is, because both possible utility gaps are positive. At observation `O=0`, behavior depends on `P(H | O=0)` and on the chosen local transforms, but not on `b`. These facts persist under arbitrary mixtures because the corresponding unnormalised gaps are linear in the mixture. At zero-probability observations choose the same tie action. Thus every value of `b` in the interval admits the same assignment of optimal policies for every mixture in the note's `Sigma(C)`.

The diagram is nevertheless domain dependent: the hard profile fixing `(O,H)=(0,0)` demands action 0 at observation 0, while the hard profile fixing `(O,H)=(0,1)` demands action 1. Both variables are in `Anc(U)`. Moreover, all displayed inequalities are strict, so this failure occupies an open, positive-measure set of utilities and parameters; it cannot be put into the exceptional Lebesgue-null set. This directly contradicts part (a). It also contradicts part (b), since two models separated by a fixed change in `b` already share exact optimal behavior at `delta=0`, while the claimed modulus has `gamma_M(0)=0`.

Masking `O` removes the obstruction: once the decision cannot condition on `O`, the always-positive `O=1` slice is combined with the other slice and its magnitude can affect the optimal action. Condition (M3), introduced later in the note, also rules out this particular obstruction by requiring both utility-gap signs on every observation slice. Consequently Proposition 3.2 and Question 4.1 can still be studied on the stronger margin class, but Richens--Everitt does **not** establish the note's asserted generic injectivity of `M -> Delta_M`.

**Verdict:** `flawed`.

### 2. The general-agent “identified set” does not match the declared observation

**Location:** `behavioral-tomography.tex:294-302`.

The note says that the analyst observes only the first-action function `f_pi`, but line 296 includes an environment `E'` only when

\[
A(E,n,\delta)\cap A(E',n,\delta)\ne\varnothing,
\]

which requires one and the same complete history-dependent policy to be bounded in both environments. First-action data instead make two environments indistinguishable whenever there are possibly different agents `pi` and `pi'` with

\[
\pi\in A(E,n,\delta),\quad \pi'\in A(E',n,\delta),\quad f_\pi=f_{\pi'}.
\]

Policies can agree on every queried first action and differ after the first transition, so the two relations are not equivalent. The displayed `epsilon*` is a valid but generally smaller full-policy-sharing radius, not “the error that no analyst can beat” from first-action observations. The upper bound in line 298 is valid for that narrower object; it does not by itself bound the correctly defined first-action identified set. Problem 4.12 is therefore mathematically interpretable as written, but it addresses a stronger observation model than its surrounding prose and intended lower-bound construction claim.

**Precision verdict for Problem 4.12:** `minor-issues` (substantive target mismatch, but the displayed quantity itself is defined).

### 3. Problem 4.9 asks for the wrong large-temperature asymptotic

**Location:** `behavioral-tomography.tex:193-197`, `:272-276`.

The requested “blow-up” of the constant as `beta -> infinity` is backwards. For the elementary local model

\[
P(Y=1\mid q)=\operatorname{logit}^{-1}\!\bigl(\beta a(q-q_*)\bigr),
\]

the Fisher information at the switch is `beta^2 a^2/4`, so local threshold error scales as `1/(beta sqrt(N))`, improving rather than deteriorating with `beta`. In the limit `beta=infinity`, the channel becomes the noiseless sign oracle used for bisection, which can achieve exponentially small one-dimensional localisation error in the number of adaptive queries. Only `beta -> 0` necessarily destroys information. There may be a non-uniform crossover between a smooth parametric regime and a noiseless-search regime, but it cannot be represented by a universally exploding `c(sk,lambda,beta)` at large `beta`. This is also consistent with the logit identification literature beginning with [Magnac--Thesmar](https://onlinelibrary.wiley.com/doi/10.1111/1468-0262.00306); recent reward/model-identifiability work likewise treats rationality parameters as observation-model parameters rather than regret floors, e.g. [Skalse--Abate, AAAI 2025](https://ojs.aaai.org/index.php/AAAI/article/view/34977).

**Precision verdict:** `minor-issues`; the experiment is defined, but the demanded asymptotic premise must be replaced by a joint `(N,beta)` question.

### 4. Several problem classes and quantifiers are not fixed tightly enough

**Locations:** `behavioral-tomography.tex:222-252`, `:306-313`, `:325-333`.

- **Problem 4.2:** by Definition 2.3 a skeleton already contains a numerical utility `u`, yet the problem asks for polynomials in `(theta,u)` and then quantifies over “almost every `u`.” One reading fixes `u`, making that quantifier inapplicable; another fixes only `(C,O,Z)` and lets `u` vary, contrary to the defined `sk`. A representation/bit-complexity convention is also needed for “computable ... in polynomial time,” including bounds on the number, degrees, and coefficient encodings of the output polynomials.
- **Problems 4.3 and 4.5:** an arbitrary class `N` satisfying injectivity and a Lipschitz modulus need not have a universal query complexity controlled by `(m,K,lambda,L)`. A singleton class satisfies those conditions and needs zero queries; a full-dimensional class has the packing lower bound. The questions remain meaningful for a specified class, but the uniform reading needs a richness/metric-entropy condition.
- **Conjectures 4.4 and 4.6:** `M(sk,lambda,mu)` depends on the polynomial list that Problem 4.2 has not yet selected. “For every successful list,” “for some canonical list,” and “for the list produced by a particular construction” are inequivalent assertions.
- **Problem 4.13:** after fixing `S,A,n`, the condition `T <= poly(|S|,|A|,n)` is vacuous unless it means one uniform algorithm and one polynomial over varying instances. Also, if `(n-1)(1-delta) <= 4`, the target error on line 309 is at least 1, while all transition entries already lie in `[0,1]`; a zero-query estimator satisfies the target for every corruption rate, making `eta*=1` under the natural domain. The “is `eta*>0`?” subquestion is therefore trivial in a large stated regime.
- **Problem 5.2:** “injective at `M`” can mean local one-to-one behaviour or a singleton global fibre. Part (b) presupposes a linear expansion `r_M(delta)=c delta+O(delta^2)` even at non-identifiable or singular points; there the radius can have a positive limit, equal 1 because another graph remains possible, or have a fractional-power modulus. The problem should ask which regime occurs before requesting `c`.
- **Problem 5.3:** the “locus where `r_M(delta)<=L delta`” omits “for all sufficiently small `delta`” (or another range), and the first finite-sample request does not explicitly set the agent-regret level to zero before later saying “then add” positive regret.

These are precision defects, not evidence that the substantive questions are already solved.

### 5. Proof audit: Proposition 3.2 is sound; Remark 3.3 needs a risk conversion

**Location:** `behavioral-tomography.tex:160-183`, `:189-208`.

The decomposition in lines 162--169 is an exact expansion of expected utility. In Proposition 3.2, (M3) supplies a compatible hard endpoint with the opposite sign on every observation slice; linearity supplies a unique affine zero; and the displayed formula recovers each profile value and hence the transform. Adversarial action choice at the single zero does not obstruct locating the boundary from the complete policy assignment. I find the proposition **correct**.

Remark 3.3 correctly constructs a `K(G)`-dimensional grid that remains inside the weaker margin class and correctly invokes binary-channel capacity. Its first sentence, however, counts transcripts of a deterministic decision tree and then speaks as if the defined expected minimax risk were a worst-case deterministic error guarantee. A randomized estimator can have more than `2^N` possible outputs, and expected error `<= epsilon` does not imply success within `epsilon` on every run. Yao's principle plus Markov/Fano applied to a slightly more widely separated packing repairs the argument and preserves the asserted `Omega(K log(1/epsilon))` order, but changes constants. **Verdict: `correct-with-gaps`.** Modern sharp noisy-search results such as [Gretta--Price](https://arxiv.org/abs/2311.00840) support the capacity-scale intuition but do not supply the missing model-reconstruction argument.

### 6. The second extraction theorem is accurately reported, with a small endpoint overstatement

**Location:** `behavioral-tomography.tex:116-131`, `:298`, `:304`, `:340`.

Theorem 2.5 matches Theorem 1 of [Richens--Abel--Bellot--Everitt](https://arxiv.org/abs/2506.01622): the square-root bound, the refined `O(delta/sqrt(n))+O(1/n)` behaviour, and the order `n |A| |S|^2` first-action queries are all present in the source. The binomial-median explanation is a fair high-level account. The theorem is **correct** as an attributed result.

The prose at line 131 slightly overstates the depth-one converse by saying communicating action-independent environments realise every table-entry value in the closed interval `[0,1]`. For example, in a multi-state action-independent chain, a self-loop probability equal to 1 makes that state absorbing and violates communication. Arbitrarily close values suffice for the no-uniform-bound conclusion, so this is an endpoint correction, not a failure of the cited theorem.

### 7. The related-work/attribution survey is incomplete as of its own cutoff

**Location:** `behavioral-tomography.tex:270`, `:304`, `:338-344`.

The strongest omission found is the 19 June 2026 preprint [*Inverting the Bellman Equation: From Q-Values to World Models*](https://arxiv.org/abs/2606.21173). It gives generic transition-kernel identifiability and explicit reconstruction/error results from richer `(Q, policy, reward)` observations. It does **not** resolve any numbered item here, because the note permits only policy bits/first actions, but it is too close to the claimed June/July 2026 frontier to omit and is directly relevant to Problems 4.9 and 4.12.

The description of [Nayebi](https://arxiv.org/abs/2603.02491) as the “nearest published relative” is also unsupported by the cited bibliography: the located item is an arXiv preprint. Its average-case selection theorem is genuinely relevant to Problem 4.8 but uses a diagnostic goal family rather than the note's interventional measure `nu`, so the note is right not to call the interventional problem resolved. Other omitted but materially related finite-sample/restricted-intervention work includes [JMLR 2025 optimal experiment design](https://www.jmlr.org/papers/v26/22-1516.html), [finite-sample interventional causal representation learning](https://arxiv.org/abs/2603.25796), and [Bing et al. 2024](https://proceedings.mlr.press/v236/bing24a.html). None observes the behavioral transform of this note.

The claim at line 344 that noisy binary search was “solved with optimal constants by Ben-Or--Hassidim” is too unqualified for the stated 2026 literature cutoff. Later work gives corrected or sharper constants in important error/noise regimes, including [Dereniowski--Łukasiewicz--Uznański](https://arxiv.org/abs/2107.05753), [Gu--Xu](https://doi.org/10.1145/3564246.3585131), and [Gretta--Price](https://arxiv.org/abs/2311.00840). This does not resolve the note's coupled reconstruction problem, but the attribution should describe the precise noisy-search model/regime rather than credit one 2008 paper with the whole subject.

Finally, lines 280 and 348 identify `W=O` with “interventions on [the agent's] inputs.” In the formal model, `W=O` intervenes on the mechanisms of observed **environmental variables**; if such a variable has descendants, the intervention also changes the world downstream. Clamping or masking the decision's sensory input while leaving the environment unchanged is a different operation--indeed, it is the operation missing from Theorem 2.4. Problem 4.10 remains well-defined as a chance-variable intervention question, but the attribution to the survey's input surface requires qualification.

### 8. Minor definition and numerical slips

**Location:** `behavioral-tomography.tex:116`, `:165`, `:294-315`.

Line 165 says there are `4^n` profiles, but the file has set `m=|C|`; the correct count is `4^m`. Line 116 calls `Psi_n` finite after defining a composite goal as a finite disjunction. It is finite only if disjunctions are treated semantically as subsets of the finite set of sequential goals (so order, repetition, and redundant disjuncts are quotiented out). As raw finite strings, arbitrarily repeated disjuncts make the set infinite. The conventional semantic reading repairs the definition, but it must be stated because Problem 4.13 uses the literal cardinality `|S x Psi_n|` as its corruption denominator.

## Per-result verdicts

| Result or claim | Verdict | Audit note |
|---|---|---|
| Theorem 2.4 (Richens--Everitt specialization), lines 106--112 | `flawed` | Omits observation masking required by the cited result; the open-set `O -> H` counterexample above refutes exact and approximate clauses. |
| Theorem 2.5 (Richens--Abel--Bellot--Everitt), lines 122--129 | `correct` | Bound and refinement match arXiv:2506.01622. |
| Proposition 3.2, lines 173--183 | `correct` | The sign-boundary recovery works, including ties at the single affine zero. |
| Remark 3.3, lines 206--208 | `correct-with-gaps` | Packing order is right; conversion from deterministic transcript counting to randomized expected minimax risk is omitted. |

## Per-item precision and openness verdicts

The openness verdicts below are negative-search conclusions, not claims that no unpublished solution exists. Searches covered arXiv, publisher/conference pages, web queries targeting Google Scholar, OpenReview, the Alignment Forum, and 2024--2026 terminology variants. The closest papers use different observation or intervention models.

| Item | Precision | Openness | Evidence and scope |
|---|---|---|---|
| Question 4.1, “Do margins suffice?” | `well-posed` | `open-with-related-work` | [Richens--Everitt](https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf) gives generic recovery only in its richer shift model. Quantitative genericity/faithfulness work such as [Boeken et al.](https://arxiv.org/abs/2410.16004) does not establish injectivity of this transform under (M1)--(M6). |
| Problem 4.2, effective genericity | `minor-issues` | `open-with-related-work` | Skeleton/utility and complexity ambiguities above. Strong-faithfulness volume results and [Boeken et al.](https://arxiv.org/abs/2410.16004) are adjacent, not an effective inverse theorem for `Delta`. |
| Problem 4.3, exact query complexity | `minor-issues` | `open-with-related-work` | Arbitrary-class degeneracy above. [Richens--Everitt](https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf) is unlimited-query; [JMLR optimal experiment design](https://www.jmlr.org/papers/v26/22-1516.html) observes causal variables, not policy bits. |
| Conjecture 4.4, exact rate | `minor-issues` | `open-with-related-work` | Depends on an unspecified output of Problem 4.2. No located source composes `K` behavioral threshold searches into causal-table recovery with the conjectured uniform constants. |
| Problem 4.5, noisy query complexity | `minor-issues` | `open-with-related-work` | Inherits the arbitrary-class issue. [Gretta--Price](https://arxiv.org/abs/2311.00840) and [Dereniowski et al.](https://arxiv.org/abs/2107.05753) sharpen noisy search, but do not address the coupled unknown-graph inverse map. |
| Conjecture 4.6, noisy capacity rate | `minor-issues` | `open-with-related-work` | Depends on the unspecified effective-genericity class. No found paper proves capacity achievement for this behavioral transform. |
| Problem 4.7, regret floor | `well-posed` | `open-with-related-work` | The approximate Richens--Everitt result is for the richer masking model and is non-uniform; [Bellot--Richens--Everitt](https://proceedings.mlr.press/v267/bellot25a.html) studies predictive limits, not this identified-set modulus. |
| Problem 4.8, average-case regret | `well-posed` | `open-with-related-work` | [Nayebi](https://arxiv.org/abs/2603.02491) proves a related goal-family result. It does not use the declared interventional distribution `nu` and does not compute `varphi(delta,kappa)`. |
| Problem 4.9, Boltzmann agents | `minor-issues` | `open-with-related-work` | Large-`beta` premise is wrong. [Magnac--Thesmar](https://onlinelibrary.wiley.com/doi/10.1111/1468-0262.00306), [Skalse--Abate](https://ojs.aaai.org/index.php/AAAI/article/view/34977), and [Inverting the Bellman Equation](https://arxiv.org/abs/2606.21173) concern related identification with richer data, not minimax active design from these samples. |
| Problem 4.10, restricted intervention sets | `well-posed` | `open-with-related-work` | Classical [z-identifiability](https://arxiv.org/abs/1210.4842), [JMLR 2025 design](https://www.jmlr.org/papers/v26/22-1516.html), and [Bing et al.](https://proceedings.mlr.press/v236/bing24a.html) use observed distributions/representations rather than an optimal-policy bit. |
| Question 4.11, the chain | `well-posed` | `open-with-related-work` | The same restricted-intervention literature is relevant, but no located work factors a binary chain from this one-bit behavioral projection. |
| Problem 4.12, `1/n` rate | `minor-issues` | `open-with-related-work` | The displayed radius mismatches first-action equivalence. [Lu et al.](https://arxiv.org/abs/2606.24842) prove transition-local certification/tightness for their own bound, not a common all-goal first-action map with separation `c/n`; [Inverting the Bellman Equation](https://arxiv.org/abs/2606.21173) assumes Q-values. |
| Problem 4.13, persistent corruption | `minor-issues` | `open-with-related-work` | Uniform-polynomial, semantic-cardinality, and trivial-target regimes above. [Krishnamurthy et al.](https://arxiv.org/abs/2002.11650) study robust contextual/threshold search, not persistent corruptions over the composite-goal certificate space. |
| Problem 5.2, starter identified set | `minor-issues` | `open-with-related-work` | “Injective at” and the assumed linear expansion need regimes. Richens--Everitt's two-variable simulations do not provide the semialgebraic fibre/radius calculation. |
| Problem 5.3, starter finite sample | `minor-issues` | `open-with-related-work` | The locus and regret level need quantifiers. Sharp noisy-search work supplies a one-dimensional component only; no found paper proves matching three-parameter/two-graph behavioral recovery. |

## Search-query log

Queries are reproduced literally. Several broad searches were deliberately reused for adjacent items so that each item was checked under both its local terminology and the authors' terminology.

### Question 4.1

- `"behavioral transform" causal model identifiability optimal policy interventions`
- `site:arxiv.org "robust agents learn causal world models" margin genericity identifiability`
- `site:openreview.net 2024 2025 2026 causal model elicitation agent behavior identifiability`
- `site:alignmentforum.org world model extraction behavior causal interventions agent`

### Problem 4.2

- `effective generic identifiability polynomial margin algebraic statistics inverse map Łojasiewicz inequality causal model`
- `site:arxiv.org 2024 2025 "quantitative identifiability" polynomial map inverse margin`
- `strong faithfulness excluded volume causal Bayesian networks Uhler Raskutti Buhlmann Yu`
- `site:scholar.google.com polynomial generic identifiability effective algebraic statistics finite sample`

### Problem 4.3

- `finite query complexity recover causal model from optimal policy oracle interventions`
- `site:arxiv.org 2024 2025 2026 policy oracle causal discovery query complexity behavior`
- `site:openreview.net 2024 2025 active query inverse reinforcement learning model identification noisy policy`
- `site:arxiv.org 2024 2025 2026 finite sample querying agent causal model behavior world model extraction`

### Conjecture 4.4

- `finite query complexity recover causal model from optimal policy oracle interventions`
- `"Robust agents learn causal world models" two binary variables algorithm simulation`
- `site:arxiv.org "behavioral transform" query complexity causal model`
- `site:scholar.google.com optimal policy oracle causal model recovery query complexity`

### Problem 4.5

- `noisy binary search capacity 1-H(eta) adaptive queries optimal constants`
- `site:openreview.net 2024 2025 active query inverse reinforcement learning model identification noisy policy`
- `finite query complexity recover causal model from optimal policy oracle interventions`
- `corruption robust threshold search continuum contextual search`

### Conjecture 4.6

- `noisy binary search capacity 1-H(eta) adaptive queries optimal constants`
- `site:arxiv.org noisy binary search optimal capacity 2024 2025`
- `site:scholar.google.com noisy binary search capacity adaptive query`
- `site:openreview.net noisy policy query world model identification`

### Problem 4.7

- `"regret" identifiability causal model from policy behavior lower bound`
- `site:arxiv.org 2024 2025 2026 average-case regret world model recovery agent policy`
- `site:openreview.net "average-case regret" world model agent causal`
- `site:alignmentforum.org selection theorem average regret world model`

### Problem 4.8

- `"What Capable Agents Must Know" average-case regret transition kernel`
- `site:arxiv.org/abs/2603.02491 average-case regret diagnostic goal family margin`
- `site:alignmentforum.org "average-case regret" "world model"`
- `site:scholar.google.com "General agents contain world models" average regret`

### Problem 4.9

- `active learning logistic threshold query design minimax rate inverse temperature beta binary response`
- `Boltzmann rational policy identifiability world model inverse reinforcement learning`
- `site:openreview.net 2024 2025 2026 Boltzmann policy identifiability active query inverse decision`
- `dynamic discrete choice identification logit policy transition probabilities Magnac Thesmar`
- `"Inverting the Bellman Equation: From Q-Values to World Models" theorem identifiability policy queries`

### Problem 4.10

- `causal identifiability restricted intervention targets which edges table parameters z-identifiability`
- `minimum intervention targets identify DAG causal graph Eberhardt experiment design 2024 2025`
- `site:arxiv.org 2024 2025 2026 limited interventions causal discovery identifiability`
- `sample complexity interventional causal representation learning restricted interventions`

### Question 4.11

- `single node interventions identify binary Markov chain transition matrices endpoint observation`
- `causal identifiability restricted intervention targets which edges table parameters z-identifiability`
- `two binary variables causal direction identifiability optimal decision behavior interventions semialgebraic`
- `site:scholar.google.com binary causal chain single intervention identifiability`

### Problem 4.12

- `world model recovery goal-conditioned agent O(1/n) lower bound policy 2026`
- `site:arxiv.org 2024 2025 2026 transition kernel identifiability goal-conditioned policy first action`
- `arXiv 2606.24842 "World models in pieces"`
- `site:arxiv.org/abs/2606.21173 "Inverting the Bellman Equation"`
- `arXiv 2603.21399 "agent-bounded indistinguishability"`

### Problem 4.13

- `persistent adversarial corruption query model randomized self reducibility goal space`
- `site:openreview.net adversarial persistent label corruption active queries robust 2024 2025`
- `corruption robust threshold search continuum contextual search`
- `site:arxiv.org persistent corruption active learning query 2024 2025 2026`

### Problem 5.2

- `two binary variables causal direction identifiability optimal decision behavior interventions semialgebraic`
- `two-node causal Bayesian network policy oracle recovery finite noisy queries`
- `site:arxiv.org 2024 2025 2026 two variable causal model intervention identifiability finite sample`
- `"Robust agents learn causal world models" two binary variables algorithm simulation`

### Problem 5.3

- `two-node causal Bayesian network policy oracle recovery finite noisy queries`
- `noisy binary search capacity 1-H(eta) adaptive queries optimal constants`
- `site:arxiv.org 2024 2025 2026 two variable causal model intervention identifiability finite sample`
- `site:openreview.net finite sample world model extraction noisy behavior`

Additional source-verification searches included:

- `"Robust agents learn causal world models" Richens Everitt theorem 1 theorem 2`
- `"General agents contain world models" Richens Abel Bellot Everitt Theorem 1`
- `"General agents contain world models" "sqrt" transition probability n delta`
- `"Agents robust to distribution shifts learn causal world models even under mediation"`
- `site:arxiv.org Ceriscioli Mohan mediation causal world models agents 2025`
- `"The limits of predicting agents from behaviour" Bellot Richens Everitt`
- `arXiv 2603.02491 Nayebi capable agents selection theorems`
- `site:alignmentforum.org "robust agents learn causal world models"`

## Machine-readable verdict

```json
{
  "file": "behavioral-tomography.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Theorem 2.4 (Richens--Everitt specialization)",
      "verdict": "flawed",
      "note": "The source theorem allows masking decision inputs; the note fixes the observation set. On O->H with O observed, utility gaps of both signs at O=0 but both positive at O=1 give an open positive-measure domain-dependent family in which P(H=1|O=1) varies while all optimal-policy assignments coincide. Both exact and approximate clauses fail."
    },
    {
      "label": "Theorem 2.5 (Richens--Abel--Bellot--Everitt)",
      "verdict": "correct",
      "note": "The square-root bound and O(delta/sqrt(n))+O(1/n) refinement match arXiv:2506.01622."
    },
    {
      "label": "Proposition 3.2",
      "verdict": "correct",
      "note": "M3 supplies opposite-sign hard endpoints and the unique affine sign boundary recovers every profile value, including the zero/tie case."
    },
    {
      "label": "Remark 3.3 (information-theoretic floor)",
      "verdict": "correct-with-gaps",
      "note": "The packing and asymptotic order are sound, but deterministic transcript counting is not directly a lower bound for randomized expected minimax risk; a Yao/Markov/Fano conversion with changed constants is needed."
    }
  ],
  "items": [
    {
      "label": "Question 4.1",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf",
        "https://arxiv.org/abs/2410.16004"
      ],
      "note": "No source found proves or refutes injectivity under M1--M6; the cited generic theorem uses a richer shift model."
    },
    {
      "label": "Problem 4.2",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2410.16004",
        "https://arxiv.org/abs/1207.0547"
      ],
      "note": "A skeleton fixes u although u is later varied, and polynomial-time output/encoding is not specified. Related faithfulness-volume work does not give the requested effective inverse."
    },
    {
      "label": "Problem 4.3",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf",
        "https://www.jmlr.org/papers/v26/22-1516.html"
      ],
      "note": "An arbitrary injective Lipschitz class can be a singleton, so complexity is not determined by m,K,lambda,L without a richness condition. No finite-query result for this observation model was found."
    },
    {
      "label": "Conjecture 4.4",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf"
      ],
      "note": "The class depends on a polynomial list not yet selected by Problem 4.2. No matching composed bisection theorem was found."
    },
    {
      "label": "Problem 4.5",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2311.00840",
        "https://arxiv.org/abs/2107.05753"
      ],
      "note": "It inherits Problem 4.3's arbitrary-class ambiguity. Sharp noisy search does not solve the coupled causal inverse problem."
    },
    {
      "label": "Conjecture 4.6",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2311.00840",
        "https://arxiv.org/abs/2107.05753"
      ],
      "note": "The effective-genericity class is unspecified; no capacity-achieving reconstruction result for this transform was found."
    },
    {
      "label": "Problem 4.7",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.mlr.press/v267/bellot25a.html",
        "https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf"
      ],
      "note": "Located work does not compute the identified-set modulus or matching lower construction for the note's fixed-observation transform."
    },
    {
      "label": "Problem 4.8",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2603.02491"
      ],
      "note": "Nayebi proves a goal-family average-case result, not the interventional nu-model or its threshold/rate."
    },
    {
      "label": "Problem 4.9",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://onlinelibrary.wiley.com/doi/10.1111/1468-0262.00306",
        "https://ojs.aaai.org/index.php/AAAI/article/view/34977",
        "https://arxiv.org/abs/2606.21173"
      ],
      "note": "The requested large-beta blow-up is false; local information grows like beta squared and beta=infinity recovers noiseless threshold search. Related identification work uses richer observations."
    },
    {
      "label": "Problem 4.10",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/1210.4842",
        "https://www.jmlr.org/papers/v26/22-1516.html",
        "https://proceedings.mlr.press/v236/bing24a.html"
      ],
      "note": "Restricted-intervention identification is developed for richer observed-distribution models, not policy-bit tomography. W=O is not literally sensory-input clamping."
    },
    {
      "label": "Question 4.11",
      "precision": "well-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/1210.4842",
        "https://www.jmlr.org/papers/v26/22-1516.html"
      ],
      "note": "No source found characterizes factor identifiability of this chain from its one-bit behavioral projection."
    },
    {
      "label": "Problem 4.12",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2606.24842",
        "https://arxiv.org/abs/2606.21173",
        "https://arxiv.org/abs/2506.01622"
      ],
      "note": "The displayed identified set uses a shared full policy rather than equality of observed first-action maps. Lu et al.'s tightness is for a different certificate bound, and Q-value inversion assumes richer data."
    },
    {
      "label": "Problem 4.13",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2002.11650"
      ],
      "note": "Uniform polynomial quantifiers and the semantic quotient making Psi_n finite are missing, and the target is vacuous when (n-1)(1-delta)<=4. Robust search literature does not cover persistent corruption of this goal space."
    },
    {
      "label": "Problem 5.2",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf"
      ],
      "note": "Injective at M is ambiguous and a linear radius expansion need not exist at non-identifiable or singular points. No semialgebraic solution was found."
    },
    {
      "label": "Problem 5.3",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://arxiv.org/abs/2311.00840",
        "https://proceedings.iclr.cc/paper_files/paper/2024/file/44a2b9f7bf9aec3f1fa333ad875b0ee0-Paper-Conference.pdf"
      ],
      "note": "The Lipschitz locus needs a delta range and the first noisy-query task should state delta=0. No matching two-graph finite-sample result was found."
    }
  ],
  "attribution_issues": [
    "Theorem 2.4 is attributed to Richens--Everitt but omits the source theorem's input-masking intervention and is false as stated.",
    "The June 2026 preprint Inverting the Bellman Equation: From Q-Values to World Models is materially related but omitted from the claimed mid-2026 literature frontier.",
    "Nayebi 2026 is called a published relative although the located and cited work is an arXiv preprint.",
    "The claim that Ben-Or--Hassidim solved noisy binary search with optimal constants is overbroad in light of later corrected/sharper results by Dereniowski et al., Gu--Xu, and Gretta--Price.",
    "The identification W=O with intervention on an agent's inputs conflates intervention on observed environmental mechanisms with sensory-input clamping/masking."
  ],
  "confidence": "medium"
}
```
