> **Historical audit record.** This report concerns a pre-repair draft of the agenda now numbered [MAIS-A1](../../../agendas/MAIS-A1/). Its findings were addressed in the July 2026 repair round. Item and line numbers may differ from the current edition; see the [audit index](../README.md) and [repair log](../REPAIR-LOG.md). A narrow passage applying one finding to an external publication has been omitted pending verification with that publication's author.

# Audit report: `open problems/quantitative-bounded-lob.tex`

The file has significant issues. Most of its elementary finite-search arguments and its qualitative background on Löb, Solovay, Parikh, and finite consistency are sound, but the central Parametric Bounded Löb theorem is false under the file's stated convention that an arbitrary computable budget is represented only by a computation-graph predicate and that domination is merely external. A proof-search-dependent presentation of an extensionally fast-growing budget gives a direct counterexample; it also resolves Problem 4.5 negatively, refutes Proposition 4.8(2), and makes Question 4.4 representation-dependent. Independently, the proposed concrete system `PA_bin` is not specified enough to determine exact symbol counts, the fixed-length-family formulation in Question 4.7 is ambiguous and partly trivial, the bounded-outer-box claim in Problem 5.1 is false, and the Payor item is misattributed. Searches found closely related 2026 Lean work but no resolution of the remaining well-defined cores of the thirteen items.

## Findings by severity

### Critical

1. **Theorem 2.4 (lines 157–165) is false as stated.** Fix the file's computable expansion function `E`, and put

   - `M(k) = max_{t <= k} E(t)`, and
   - `D(k) = (k+1)(M(k)+1)`.

   Then `D` is computable and `D \succ E O(log k)`: for every `h(k)=O(log k)`, eventually `h(k) <= k`, so `D(k) >= (k+1)E(h(k))`. Now present a computable function `f` by the following total program: compute `D(k)`; exhaustively search all strings of length at most `D(k)` for an `S`-proof of contradiction; output `0` if one is found, and output `D(k)` otherwise. Since `S` is consistent, on every standard input `f(k)=D(k)`. Thus `f` has exactly the required external growth, even with an explicit computable domination modulus.

   Under the computation-graph convention adopted at lines 84 and 103, however, `S` proves uniformly `not Box_{f(k)} false`. It reasons by the two branches certified by a computation of `f`: if the bounded search found a contradiction proof, the output is zero and there is no zero-symbol proof; if it did not, the output is `D(k)` and the exhaustive-search certificate itself says that there is no contradiction proof of that length. Hence the premise of Theorem 2.4 holds with `p(k)=false`, while its tail conclusion would make consistent `S` prove a contradiction.

   *A passage applying this objection to the cited published theorem is omitted pending verification with the paper's author.*

   A viable repair must make the relevant implementations part of the data and assume `S`-verifiable totality and eventual inequalities (or supply proofs of the three crossover inequalities with their moduli). External monotonicity, external domination, and even a computable external modulus do not suffice.

2. **Problem 4.5 (lines 300–311) is negatively resolved by the same counterexample.** The function above has a computable modulus: after `ceil(C log(k+2)) <= k` and `k+1>M`, its value exceeds `M E(ceil(C log(k+2)))`. The premise proof exists for `p=false`, but no finite `K` and no proof-length bound `Lambda` can produce the demanded tail theorem. Consequently, the problem cannot be described as open in its present quantification over arbitrary computable `f`; line 430's blanket openness claim is false.

3. **Proposition 4.8(2) (lines 333–346) is false.** Choose the same proof-search-dependent `f`, increasing `D` if necessary so `D(k)>=k`. The theory proves uniformly `Box_{f(k)} Con_k -> Con_k`: in the “proof found” branch `f(k)=0`, making the antecedent false; in the “no proof found” branch `f(k)=D(k)`, the search certificate proves `Con_D(k)` and hence `Con_k`. Yet the standard function still externally dominates `E O(log k)`. The proof at line 345 invokes the false Theorem 2.4 and therefore cannot establish the claimed nonuniformity.

4. **Definition 4.1 and Question 4.4 (lines 266–298) are not extensional in `f`.** A standard computable function does not determine a unique arithmetical graph formula. For example, let `d(k)=floor(log_2 k)` and implement `g(k)` as zero if a contradiction proof of length at most `d(k)` is found and as `d(k)` otherwise. By consistency, `g=d` on all standard inputs, while `S` proves `not Box_{g(k)} false`, so PBL fails for that presentation. The ordinary primitive-recursive presentation of `floor(log_2 k)` may behave differently. Therefore the displayed set `{f computable : PBL holds for (S,f)}` is undefined until a canonical index/graph, or an internal equivalence requirement, is fixed.

### High

5. **`PA_bin` is not a concrete proof system (lines 72–103), so the exact quantitative problems do not yet denote unique functions.** “Enderton's Hilbert calculus, with binary numerals and abbreviation lines” does not specify a formal abbreviation grammar, identifier encoding and cost, scope/shadowing, expansion semantics, proof-file grammar, proof checker, or Gödel numbering. The finite-alphabet requirement at line 72 is in tension with unpriced “fresh symbols” at line 86. These choices can change `E_S`, `d_S`, and subpolynomial proof lengths, not merely constants. As a result, Problems 3.4 and 3.7 and Conjecture 3.5 are not yet exact questions about a definite `PA_bin`.

6. **The `log log k` compression claim (line 290) is unsupported under the stated finite-alphabet symbol measure.** The suggested repeated-abbreviation construction needs about `m` distinct live names for `k=2^(2^m)`. Encoding those fresh names over a finite alphabet costs at least order `m log m` symbols in total, not order `m`, unless a stack-based/shadowing convention is added. This is another place where the omitted abbreviation syntax materially affects Question 4.4.

7. **Question 4.7 (lines 324–327) is ambiguous and its finiteness subquestion is not a genuine open problem under the natural uniform-code reading.** “Families whose codes each have at most `ell` symbols” could mean instantiated agents, uniform generator programs, or templates; these are inequivalent. Under the literal instantiated-code reading, formulas containing a growing parameter cannot remain bounded by fixed `ell`. Under the uniform-program reading there are only finitely many code strings of length at most `ell`, so once an applicable robust-cooperation theorem gives every `G`-fair pair a finite threshold, the maximum is automatically finite (with an empty-set convention still missing). A meaningful effective or polynomial bound also needs to charge for a proof/certificate of `G`-fairness: Problem 4.5 itself shows that thresholds depend on the premise-proof length, which is not bounded by source-code length alone. The phrase “Critch's condition” should distinguish the old arXiv proof-internal inequality `G(ell)>6f(2^ell)` from the published Theorem 5.1 condition `G(ell) \succ e O(ell)`, and any use must incorporate the repair to the central theorem.

8. **The claim about provably bounded `b` in Problem 5.1 (line 361) is false.** Let `p(k)=false`, `a(k)=c(k)=0`, let `Q` be `Box_0 false -> false`, and let `B` be the length of a fixed `S`-proof of `Q`. Put `b(k)=B`. The theory proves `Box_B Q` (by verifying that proof) and proves `not Box_0 false`. It therefore cannot consistently prove `Box_B Q -> Box_0 false`. Thus a provably bounded outer budget does not make every triple admissible; the asserted “eventually differs” argument fails for constant `p` and `a`.

### Medium

9. **The Payor source is misattributed (lines 376, 396, 581–585).** The cited post, “Modal fixpoint cooperation without Löb's theorem,” is authored by Andrew Critch. It explicitly credits the central lemma to James Payor and says the theorem was inspired by Scott Garrabrant. The derivation reproduced at line 376 is logically correct, but the bibliography should credit Critch for the post/construction and Payor for the lemma. Source: [Critch's post](https://www.lesswrong.com/posts/2WpPRrqrFQa6n2x3W/modal-fixpoint-cooperation-without-loeb-s-theorem). A related 2026 Kripke-frame post is informative but does not solve the bounded arithmetic question: [“Payorian cooperation is easy with Kripke frames”](https://www.lesswrong.com/posts/LaCP6WyNzX8kiZn3w/payorian-cooperation-is-easy-with-kripke-frames).

10. **The mechanization survey at line 426 is outdated and overbroad.** Duclaux, Formenti, Cobben, Schölkopf, and Jin's 2026 Lean 4 work introduces `ProofWitness`, `witnessChars`, and a proof-search abstraction for proof-based open-source games. It does not resolve the file's concrete questions: bounded semantics and a PBL-like principle are axiomatized, the proof oracle is noncomputable, and there is no concrete PA checker or extracted threshold. Still, “none of these count symbols” now needs qualification. Primary source: [“Proving Your Way to Cooperation: Formalizing Proof-Based Open Source Game Theory in Lean”](https://openreview.net/pdf?id=Wc5TAIUC8k); [AI4Math 2026 workshop](https://ai4math2026.github.io/).

11. **The Ehrenfeucht–Mycielski sentence at line 424 omits the theorem's hypothesis.** The theorem assumes that `T + not alpha` is undecidable; it is not literally a theorem about every theory and every unprovable added axiom. In the intended setting of a consistent recursively axiomatized extension of PA, the omitted condition follows for unprovable `alpha`, so the local application can be repaired by stating that context rather than by claiming the unrestricted formulation. Primary metadata: [Ehrenfeucht and Mycielski, “Abbreviating proofs by adding new axioms”](https://doi.org/10.1090/S0002-9904-1971-12696-4).

12. **The blanket state-of-the-art assertions at lines 35, 169, 405, 426, and 430 need narrowing.** The searches below did not find published solutions of the remaining exact proof-length questions, but absence claims such as “first ... in print,” “no bounded version has appeared anywhere,” and “every numbered item ... is open” are stronger than the evidence supports. In particular, Problem 4.5 is false rather than open, Question 4.7 has a finite-set observation, and the 2026 Lean work is directly related. These should be written as scoped search reports with a date and databases/queries.

## Audit of proofs and background results

| Result or claim | Location | Verdict | Audit note |
|---|---:|---|---|
| Existence and computability of the pointwise least expansion function | 111–120 | correct-with-gaps | The finite-search argument works once a fully specified proof syntax and graph convention are fixed. The current `PA_bin` does not supply those data. |
| Löb's theorem and the standard diagonal derivation | 125–132 | correct | Standard result; the stated derivability conditions suffice. |
| Critch/FairBot eventual self-cooperation | 150–155 | correct-with-gaps | The special external behavioral conclusion for the regular budget `f(k)=k` is plausibly recoverable by metalevel, instance-by-instance proof construction. The draft's stated derivation as an “instance” of Theorem 2.4 is invalid, and a uniform arithmetical conclusion requires internally verified inequalities. |
| Parametric Bounded Löb | 157–165 | flawed | Refuted, under the draft's conventions, by the proof-search-dependent budget above. |
| Proposition 3.2: totality, computability, monotonicity, and minimality of `F_S` | 187–194 | correct-with-gaps | Correct for an actually fixed finite syntax, checker, Gödel coding, and provability predicate. Those are not fully fixed for `PA_bin`. |
| Lemma 3.3: cheap direction | 198–205 | correct | Appending a propositional axiom instance and modus ponens gives the claimed additive formula-size toll. |
| The proof-cost ledger | 214–226 | correct-with-gaps | Properly labelled heuristic. Polynomial claims require an actual calculus and length-tracked diagonalization/internalization proofs; they are not established here. |
| Proposition 4.2: failure for provably bounded budgets and, in plain systems, provably sublogarithmic budgets | 273–286 | correct | The two vacuity arguments follow from finite checking and the explicitly assumed provable lower bound on conclusion length. They do not extend to arbitrary abbreviation systems without further syntax. |
| Remark 4.3 compression estimate | 288–290 | flawed | The qualitative warning is sound, but the claimed `log log k` cost is not justified with finite-alphabet fresh-name costs. |
| Proposition 4.8: bounded reflection is omega-incomplete | 333–346 | flawed | Part (1) is correct instance by instance; part (2) is false for the proof-search-dependent fast budget and depends on the false Theorem 2.4. |
| Internal-bounded-Löb bounded-`b` rationale | 355–362 | flawed | The constant `p,a,b,c` counterexample above disproves “every such triple is admissible.” |
| Payor lemma derivation | 376 | correct | The four modal/provability steps are valid; only source authorship is wrong. |
| Löb/Solovay/GL background | 353, 420 | correct | The qualitative statements match the standard theorems; no quantitative bound follows from them. |
| Friedman–Pudlák finite-consistency discussion | 422 | correct-with-gaps | The broad lower/upper-bound picture matches the cited literature, but every exact rate depends on the proof-system and length conventions, which should be carried into the prose. [Pudlák's survey](https://arxiv.org/abs/1601.01487). |
| Gödel/Buss and Ehrenfeucht–Mycielski speedup discussion | 424 | correct-with-gaps | The Gödel/Buss distinction between line and symbol measures is appropriate. The Ehrenfeucht–Mycielski condition is omitted, though automatic in the intended PA-extension setting. |
| Parikh proof-versus-provability speedup | 424 | correct | Parikh's Theorem 1.3 and Buss's commentary support the claimed separation and the explanation why it does not settle the Löb-rule question. [Original article](https://www.cambridge.org/core/journals/journal-of-symbolic-logic/article/existence-and-feasibility-in-arithmetic/1D2B8E92AC91241C8D0758C4D272894F); [Buss commentary](https://mathweb.ucsd.edu/~sbuss/ResearchWeb/parikh/paper.pdf). |
| Comparative proof-length modalities | 428 | correct-with-gaps | The cited Guaspari–Solovay, Švejdar, and de Jongh/Carbone–Montagna lines are relevant precedent, not fixed-budget solutions. The draft should avoid implying that this search exhausts all later variants. [Carbone–Montagna metadata](https://dblp.uni-trier.de/rec/journals/mlq/CarboneM90.html); [Švejdar bibliography](https://www1.cuni.cz/~svejdar/papers/moda83.html). |

## Item-by-item precision and openness audit

### Problem 3.4 — Determine the overhead

**Precision: ill-posed. Openness: open-no-progress-found.** For any fully specified proof system the function in Definition 3.1 is a legitimate computable function, but the declared default `PA_bin` is not fully specified, so “up to constant factors” does not currently select one function. The proof-complexity and logic searches found Parikh/Pudlák speedup relatives but no result determining this Löb overhead.

### Conjecture 3.5 — Polynomial overhead

**Precision: ill-posed. Openness: open-no-progress-found.** The conjecture becomes precise after fixing the missing syntax, checker, abbreviation, and coding data. No searched source proves a polynomial length bound for the concrete Löb transformation, and the draft's ledger is explicitly heuristic.

### Question 3.6 — Lower bounds

**Precision: ill-posed. Openness: open-no-progress-found.** The permissive phrase “or any efficient system of your choice” does not cure the underdefinition of “efficient,” especially its abbreviation mechanism. Parikh gives large speedup from a short proof of `Box A` to a long proof of `A`, but, as the file correctly observes, not a short proof of `Box A -> A`; no genuine Löb-rule speedup was found.

### Problem 3.7 — System constants

**Precision: ill-posed. Openness: open-no-progress-found.** Exact `E_PA_bin` and `d_PA_bin`, least degrees, and constant-factor asymptotics depend directly on the missing file grammar, abbreviation costs, proof predicate, fixed-point implementation, and chosen `C_0`. Literature on length-tracked derivability conditions supplies techniques, not these requested optima.

### Question 4.4 — The Löb window

**Precision: ill-posed. Openness: open-with-related-work.** PBL depends on the graph/index representing a computable budget, so it is not a property of the extensional function `floor(log_2 k)` under the file's conventions. The proof-dependent implementation above makes the logarithmic function fail PBL, while the canonical primitive-recursive implementation remains a meaningful open variant. Critch's theorem and the failure proposition bracket related regimes but do not settle that repaired question.

### Problem 4.5 — Effective Parametric Bounded Löb

**Precision: ill-posed. Openness: resolved.** It is resolved negatively as written by the explicit fast-growing `f` above, even when the input includes a computable external domination modulus. A repaired problem must take formalized graph definitions and `S`-proofs of all relevant bounds as input. The 2026 Lean work axiomatizes rather than extracts such thresholds.

### Problem 4.6 — The FairBot threshold

**Precision: ill-posed. Openness: open-with-related-work.** The programming language, encoding, arithmetization, exact `PA_bin`, and source of the self-reference are described only as choices to be declared later. Moreover, after those choices, `hat k*` is one fixed integer, so “up to a constant factor” is vacuous without an asymptotic family. Critch, CDR, and the Lean formalization are relevant but do not compute the threshold in a concrete checker.

### Question 4.7 — Polynomial FairBot thresholds

**Precision: ill-posed. Openness: open-with-related-work.** The code of a parameterized family is undefined, the fixed-length finiteness half follows trivially under the natural finite-code interpretation once individual convergence is available, and proof/certificate length is omitted from the proposed polynomial input. The genuinely asymptotic, repaired threshold question remains open in the sources found.

### Problem 5.1 — Internal bounded Löb

**Precision: ill-posed. Openness: open-no-progress-found.** “Require `b(k)>=log_2 k`, say” is not a formal domain restriction, graph representations and internal growth proofs are not fixed, and the supporting bounded-`b` assertion is false. No searched paper establishes the repaired polynomial-budget schema.

### Conjecture 5.2 — Bounded GL, soundness form

**Precision: minor-issues. Openness: open-no-progress-found.** Its core quantifiers and budget translation are stated clearly, conditional on a genuinely fixed `S`; it inherits graph/encoding ambiguity and needs schedules compatible with internally provable budget comparisons. HOL Light proves ordinary GL, not this resource-bounded soundness schema.

### Problem 5.3 — Parametric bounded Payor

**Precision: minor-issues. Openness: open-with-related-work.** The central implication is readable, but external `g \succ log k` and `g-f \succ log k` again do not guarantee the internal inequalities needed by a uniform proof; the program encoding and comparison of two fixed thresholds are also underspecified. Informal Payor/Critch and 2026 Kripke-frame work are related, not fixed-budget arithmetic solutions.

### Problem 8.1 — Robustness

**Precision: minor-issues. Openness: open-no-progress-found.** A precise version must specify formula translations as well as proof translations, their size bounds, and how each system represents the other's bounded provability predicate. Standard polynomial simulation alone does not align the two hypothesis classes. No direct result for this `F_S` was found.

### Question 8.2 — Toward bounded Solovay

**Precision: minor-issues. Openness: open-with-related-work.** The displayed quantifier pattern is intelligible once `S`, realizations, and the translation are fixed, and the file candidly flags its design choices. Comparative-proof modalities and ordinary Solovay completeness are strong precedents, but the searches found no completeness theorem for fixed symbol budgets or for this schedule semantics.

## Literal search-query record

The following are the literal query strings used for the per-item checks; title/author follow-ups are included where they were used.

### Problem 3.4

- `"quantitative Löb theorem" proof length overhead`
- `"Löb's rule" proof speed-up`
- `site:arxiv.org proof length Löb theorem bounded overhead`
- `"Box A -> A" proof length Löb`

### Conjecture 3.5

- `"polynomial overhead" "Löb's theorem" proof length`
- `"short proof" "Box A" "Löb" proof length`
- `site:arxiv.org quantitative Löb proof complexity polynomial`
- `"proof-length" "Löb's theorem" polynomial`

### Question 3.6

- `"Löb's rule" speedup proof length`
- `"Parikh's rule" proof length speedup`
- `provability "much shorter proof" "Löb" rule`
- `site:projecteuclid.org Parikh "Existence and feasibility in arithmetic" proof length`
- `Rohit Parikh "Existence and feasibility in arithmetic" PDF theorem proof shorter provability`
- `Parikh 1971 "Prov T" "much shorter proof"`
- `Parikh 1971 "proof of A" "proof of Prov"`
- `Samuel Buss Parikh 1971 theorem 1.3 provability short proof`

### Problem 3.7

- `"proof expansion function" Gödel encoding proof length`
- `"bounded necessitation" proof length`
- `"formalized Sigma_1 completeness" polynomial proof length Pudlak`
- `"diagonal lemma" proof length complexity`

### Question 4.4

- `"parametric bounded Löb" logarithmic budget`
- `"bounded Löb" "log k"`
- `site:alignmentforum.org bounded Lob logarithmic`
- `site:lesswrong.com parametric bounded Lob open problem`

### Problem 4.5

- `"Parametric Bounded Löb" explicit threshold`
- `"resource-bounded Löb" explicit bounds threshold`
- `"bounded Löb theorem" formalization Lean`
- `"Proving Your Way to Cooperation" Lean bounded Lob`
- `"Proving Your Way to Cooperation" Duclaux Formenti Cobben Schölkopf Jin`
- `"Formalizing Proof-Based Open Source Game Theory in Lean" authors`
- `Wc5TAIUC8k ICML 2026 AI4Math`
- `site:github.com "Proving Your Way to Cooperation" Lean`

### Problem 4.6

- `"FairBot threshold" proof length`
- `"bounded FairBot" threshold`
- `site:alignmentforum.org FairBot proof length threshold`
- `"FairBot_k(FairBot_k)" implementation`

### Question 4.7

- `"G-fair agents" cooperation threshold`
- `"robust cooperation of bounded agents" threshold polynomial code length`
- `"FairBot" "code length" polynomial`
- `site:arxiv.org "open source game theory" proof based Lean`

### Problem 5.1

- `"bounded Löb axiom" proof length`
- `"resource-bounded" "Gödel-Löb" logic axiom`
- `"Löb axiom" bounded provability budget`
- `site:alignmentforum.org "bounded Löb" axiom`

### Conjecture 5.2

- `"bounded Gödel-Löb logic" Critch conjecture`
- `"resource bounded provability logic" proof length`
- `"bounded analogues" "Gödel-Löb"`
- `"provability logic" "proof length" modal completeness`

### Problem 5.3

- `"Payor lemma" bounded`
- `"Modal fixpoint cooperation without Löb's theorem"`
- `site:lesswrong.com "Payor's lemma" proof-based agents`
- `"bounded PayorBot" cooperation`

### Problem 8.1

- `"Löb overhead" polynomial simulation proof systems`
- `"provability predicates" polynomially equivalent proof systems`
- `"proof system simulation" "bounded provability" predicate`
- `"speed-up" proof systems Gödel provability`

### Question 8.2

- `"bounded Solovay" proof length provability logic`
- `"provability logic" comparative proof length completeness`
- `"much shorter proofs" bimodal arithmetical completeness`
- `"Rosser sentences" proof comparison modal logic`

### Cross-checks for the central theorem and historical attribution

- `"Parametric Bounded Löb" error proof gap`
- `"Critch" "bounded Löb" counterexample`
- `"resource-bounded generalization of Löb" correction erratum`
- `"A parametric resource-bounded" Lob theorem citations`
- `Ehrenfeucht Mycielski 1971 "Abbreviating proofs by adding new axioms" theorem condition undecidable`
- `"Abbreviating proofs by adding new axioms" "T+¬α" undecidable`
- `Ehrenfeucht Mycielski unprovable axiom unbounded speedup theorem`
- `site:projecteuclid.org "Abbreviating proofs by adding new axioms"`

```json
{
  "file": "open problems/quantitative-bounded-lob.tex",
  "summary_verdict": "significant-issues",
  "proved_results": [
    {
      "label": "Expansion-function existence and computability (lines 111-120)",
      "verdict": "correct-with-gaps",
      "note": "The finite-search argument is sound after a complete proof syntax and graph convention are fixed; PA_bin does not yet provide them."
    },
    {
      "label": "Theorem 2.2 (Lob)",
      "verdict": "correct",
      "note": "The standard theorem and displayed derivation are correct."
    },
    {
      "label": "Theorem 2.3 (FairBot)",
      "verdict": "correct-with-gaps",
      "note": "The regular-budget behavioral result is plausibly recoverable instance by instance, but the draft's derivation through Theorem 2.4 is invalid and uniform inequalities need internal verification."
    },
    {
      "label": "Theorem 2.4 (Parametric Bounded Lob)",
      "verdict": "flawed",
      "note": "Under the draft's conventions, a proof-search-dependent computation graph represents an extensionally fast-growing f while S uniformly proves not Box_f false."
    },
    {
      "label": "Proposition 3.2 (F is computable and minimal)",
      "verdict": "correct-with-gaps",
      "note": "Correct for a completely fixed finite proof syntax, checker, coding, and predicate, which the declared PA_bin does not fully specify."
    },
    {
      "label": "Lemma 3.3 (cheap direction)",
      "verdict": "correct",
      "note": "Appending the propositional axiom instance and modus ponens gives the stated additive formula-size cost."
    },
    {
      "label": "Proposition 4.2 (failure below the window)",
      "verdict": "correct",
      "note": "Both finite-check/vacuity proofs work under their explicitly stated provability and plain-system hypotheses."
    },
    {
      "label": "Remark 4.3 (log-log abbreviation compression)",
      "verdict": "flawed",
      "note": "Fresh identifier costs under a finite alphabet are omitted, so the claimed asymptotic size does not follow."
    },
    {
      "label": "Proposition 4.8 (bounded reflection is omega-incomplete)",
      "verdict": "flawed",
      "note": "Part 1 is sound, but part 2 is false for the proof-search-dependent fast budget and invokes the false Theorem 2.4."
    },
    {
      "label": "Bounded-b claim in Problem 5.1",
      "verdict": "flawed",
      "note": "Constant p=false, a=c=0, and b equal to the length of a proof of Box_0 false -> false give a counterexample."
    },
    {
      "label": "Payor lemma derivation",
      "verdict": "correct",
      "note": "The derivation is valid, although the cited post is authored by Andrew Critch and credits the lemma to James Payor."
    },
    {
      "label": "Lob-Solovay-GL qualitative background",
      "verdict": "correct",
      "note": "The classical qualitative statements are accurate."
    },
    {
      "label": "Quantitative proof-complexity background (Friedman, Pudlak, Parikh, Ehrenfeucht-Mycielski)",
      "verdict": "correct-with-gaps",
      "note": "The main comparisons are sound; the Ehrenfeucht-Mycielski undecidability hypothesis and system-dependence of exact rates should be stated."
    }
  ],
  "items": [
    {
      "label": "Problem 3.4",
      "precision": "ill-posed",
      "openness": "open-no-progress-found",
      "citations": [
        "https://mathweb.ucsd.edu/~sbuss/ResearchWeb/parikh/paper.pdf",
        "https://arxiv.org/abs/1601.01487"
      ],
      "note": "F_S is definite for a fully specified system, but PA_bin omits the abbreviation grammar, identifier costs, checker, and coding needed to select one exact function."
    },
    {
      "label": "Conjecture 3.5",
      "precision": "ill-posed",
      "openness": "open-no-progress-found",
      "citations": [
        "https://arxiv.org/abs/1601.01487"
      ],
      "note": "No polynomial Lob-overhead theorem was found; the claim becomes precise only after the concrete system is completed."
    },
    {
      "label": "Question 3.6",
      "precision": "ill-posed",
      "openness": "open-no-progress-found",
      "citations": [
        "https://www.cambridge.org/core/journals/journal-of-symbolic-logic/article/existence-and-feasibility-in-arithmetic/1D2B8E92AC91241C8D0758C4D272894F",
        "https://mathweb.ucsd.edu/~sbuss/ResearchWeb/parikh/paper.pdf"
      ],
      "note": "Parikh's speedup does not supply a short proof of Box A -> A, and no genuine Lob-rule speedup was found; efficient systems remain underdefined."
    },
    {
      "label": "Problem 3.7",
      "precision": "ill-posed",
      "openness": "open-no-progress-found",
      "citations": [
        "https://arxiv.org/abs/1601.01487"
      ],
      "note": "Exact E and d asymptotics depend on proof-file, abbreviation, coding, and fixed-point conventions not supplied for PA_bin."
    },
    {
      "label": "Question 4.4",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://acritch.com/papers/parametric-bounded-lob.pdf",
        "https://arxiv.org/abs/1602.04184"
      ],
      "note": "PBL is representation-dependent: a proof-search-dependent graph extensionally equal to floor(log_2 k) makes PBL fail, while the canonical primitive-recursive presentation remains open."
    },
    {
      "label": "Problem 4.5",
      "precision": "ill-posed",
      "openness": "resolved",
      "citations": [
        "https://acritch.com/papers/parametric-bounded-lob.pdf",
        "https://openreview.net/pdf?id=Wc5TAIUC8k"
      ],
      "note": "Resolved negatively as stated: an externally dominating f with an explicit modulus can have a graph for which the premise holds with p=false and no tail conclusion exists."
    },
    {
      "label": "Problem 4.6",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://acritch.com/papers/parametric-bounded-lob.pdf",
        "https://arxiv.org/abs/2208.07006",
        "https://openreview.net/pdf?id=Wc5TAIUC8k"
      ],
      "note": "No concrete threshold was found; the calculus and program encoding are not fixed, and constant-factor optimization of one fixed integer is not an asymptotic problem."
    },
    {
      "label": "Question 4.7",
      "precision": "ill-posed",
      "openness": "open-with-related-work",
      "citations": [
        "https://acritch.com/papers/parametric-bounded-lob.pdf",
        "https://arxiv.org/abs/2208.07006",
        "https://openreview.net/pdf?id=Wc5TAIUC8k"
      ],
      "note": "Family-code length is undefined; finiteness is automatic for finitely many uniform codes once individual convergence holds, while a polynomial bound must also control fairness-certificate length."
    },
    {
      "label": "Problem 5.1",
      "precision": "ill-posed",
      "openness": "open-no-progress-found",
      "citations": [
        "https://acritch.com/papers/parametric-bounded-lob.pdf"
      ],
      "note": "The bounded-b rationale is false, the suggested lower restriction on b is informal, and internal budget comparisons and representations are not specified."
    },
    {
      "label": "Conjecture 5.2",
      "precision": "minor-issues",
      "openness": "open-no-progress-found",
      "citations": [
        "https://arxiv.org/abs/2102.05945",
        "https://acritch.com/papers/parametric-bounded-lob.pdf"
      ],
      "note": "The core schema is clear, but it inherits system/graph ambiguity and needs internally provable schedule comparisons; ordinary GL mechanization does not resolve it."
    },
    {
      "label": "Problem 5.3",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://www.lesswrong.com/posts/2WpPRrqrFQa6n2x3W/modal-fixpoint-cooperation-without-loeb-s-theorem",
        "https://www.lesswrong.com/posts/LaCP6WyNzX8kiZn3w/payorian-cooperation-is-easy-with-kripke-frames"
      ],
      "note": "No bounded arithmetic theorem was found; the central implication needs internal rather than merely external budget gaps, and the agent-threshold comparison needs a fixed asymptotic family."
    },
    {
      "label": "Problem 8.1",
      "precision": "minor-issues",
      "openness": "open-no-progress-found",
      "citations": [
        "https://arxiv.org/abs/1601.01487"
      ],
      "note": "A precise version must specify formula and proof translations, size bounds, and translations between the two bounded provability predicates."
    },
    {
      "label": "Question 8.2",
      "precision": "minor-issues",
      "openness": "open-with-related-work",
      "citations": [
        "https://dblp.uni-trier.de/rec/journals/mlq/CarboneM90.html",
        "https://www1.cuni.cz/~svejdar/papers/moda83.html"
      ],
      "note": "Ordinary and comparative-proof completeness results are related, but no fixed-symbol-budget Solovay theorem or result for the proposed schedule semantics was found."
    }
  ],
  "attribution_issues": [
    "The bibliography attributes 'Modal fixpoint cooperation without Lob's theorem' to J. Payor, but the linked post is by Andrew Critch; the post credits the lemma to James Payor and inspiration to Scott Garrabrant.",
    "The Ehrenfeucht-Mycielski summary omits the hypothesis that T plus not-alpha is undecidable; this is automatic only after stating the intended essentially undecidable arithmetic setting.",
    "The July 2026 related-work discussion omits Duclaux et al.'s Lean formalization, which tracks witnessChars abstractly but does not instantiate concrete PA symbol counts."
  ],
  "confidence": "high"
}
```
