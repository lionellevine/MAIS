> **Historical scoped-verification record.** This report rechecks one content-destructive verdict about a pre-repair draft of [MAIS-A2](../../../A2/); it is not a second audit of the current edition. Item and line numbers may differ. See the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Verification report: behavioral-tomography.tex, Theorem 2.4 verdict

- **File:** `open problem supplement/behavioral-tomography.tex`
- **Audit report verified:** `audit/behavioral-tomography-codex-report.md` (GPT 5.6 Sol), Finding 1 / per-result verdict "Theorem 2.4: flawed"
- **Date:** 2026-07-16
- **Verifier:** Claude Fable 5, scoped verification pass
- **Scope note:** This pass covers only content-destructive verdicts (one flawed proof grade); ill-posed and related-work verdicts were deliberately not pre-verified.

## Verdict: CONFIRMED

The auditor's grade of `flawed` for Theorem 2.4 (lines 106–114) is correct. The counterexample in the audit report is valid against the file's own definitions, satisfies every hypothesis the file's theorem actually states, occupies an open positive-measure parameter set (so it cannot hide in the theorem's Lebesgue-null exception), and refutes both clauses (a) and (b). Independently, the source paper confirms that the file's specialization dropped part of Richens–Everitt's intervention class.

## Re-derivation of the counterexample

Setup (all per the file's Definitions 2.1–2.3): chance variables **C** = {O, H}, graph O → H, observation set **O** = {O}, utility parents **Z** = {O, H}, so Anc(U) = {O, H} and Anc(U) ⊄ **O** — the theorem's graphical hypothesis holds. Write g(o,h) = u(1,o,h) − u(0,o,h) and choose utilities with

g(0,0) < 0 < g(0,1),  g(1,0) > 0,  g(1,1) > 0,

all table entries interior, and let b := P(H=1 | O=1) vary over a nontrivial interval with everything else fixed.

**Step 1 (slice w=1 is sign-frozen).** By the file's own transform (line 162), Δ_M(σ, 1) = Σ_h P_M(O=1, H=h; σ) g(1,h). Both weights g(1,·) are positive, so Δ_M(σ,1) > 0 whenever P(O=1; σ) > 0 and = 0 otherwise, for every mixture σ ∈ Σ(**C**). The optimal action at observation 1 is 1 (free at zero mass), for every σ, regardless of b.

**Step 2 (slice w=0 never sees b).** Δ_M(σ, 0) = Σ_h P_M(O=0, H=h; σ) g(0,h). Under any local intervention of Definition 2.2, O's mechanism becomes a transformed marginal and H's mechanism at the realized value o=0 is a transform of P(H | O=0) only; the entry b enters the joint law only through states with O=1, which lie entirely in the w=1 slice. Mixtures are convex combinations, so linearity preserves this: Δ_M(·, 0) is independent of b.

**Step 3 (common policy assignment).** P(O=1; σ) does not depend on b (O's marginal and its transforms never involve H's table), so for every σ the two models M_b, M_{b'} have identical demanded actions on both slices, and at zero-mass or tie points both leave the action free — choose the same action. Hence B_0(M_b) ∩ B_0(M_{b'}) ≠ ∅: a common assignment of optimal policies exists, yet the models differ in a table entry of H ∈ Anc(U).

**Step 4 (hypotheses of the file's theorem are satisfied).** Domain dependence, as the file defines it in Theorem 2.4 ("no single policy is optimal for (M,σ) for all mixtures simultaneously"): the hard profile fixing (O,H)=(0,0) demands action 0 at w=0 (gap g(0,0)<0), while the hard profile fixing (O,H)=(0,1) demands action 1 there. So each M_b is domain dependent. All defining inequalities are strict, so the family sits in an open, positive-measure set of (θ, u); the theorem's "Lebesgue-almost-every" exclusion cannot absorb it.

**Conclusion.** Clause (a) fails under the file's own gloss at line 114 ("any two models satisfying the hypotheses that admit a common assignment of policies must agree on Anc(U)"). Clause (b) fails at δ = 0, where γ_M(0) = 0 would force exact agreement but |b − b'| is bounded below. The downstream identification at line 185 ("Theorem 2.4(a) is therefore the statement: for almost every (θ,u), the map M ↦ Δ_M is injective") is false for the same reason, as are its echoes at lines 220 and 340.

**Not a hypothesis violation.** The margin conditions (M1)–(M6) — in particular (M3), which the counterexample violates (g(1,·) is single-signed on the w=1 slice) — are introduced in Section 3 and are *not* hypotheses of Theorem 2.4. So the auditor's counterexample does not run afoul of any hypothesis the file states; the REJECTED branch does not apply.

## Source check (attribution of the gap)

The published Richens–Everitt paper (arXiv:2402.10877, "Robust agents learn causal world models," ICLR 2024) states explicitly in its Section 2.3 that it "include[s] shifts that drop inputs to the policy Pa_D → Pa_D' ⊆ Pa_D (e.g. masking) as local interventions," and Theorem 1 quantifies the policy oracle over all mixtures of local interventions in that richer sense. The file's Definition 2.2 transforms chance-variable mechanisms only and keeps **O** fixed, and Theorem 2.4 quantifies over Σ(**C**) of those alone. So the flaw is a genuine mis-specialization: a hypothesis of the source theorem (the masking interventions) was dropped, and the weakened statement is false — this is a mathematical error in the file's stated theorem, not merely an attribution slip, so PARTIAL does not apply either. Masking indeed dismantles the counterexample: once the decision cannot condition on O, the always-positive O=1 slice pools with the O=0 slice and b becomes behaviorally visible.

## Minimal repair (sketch)

Either of the following restores a true statement; the first is faithful to the source.

1. **Enlarge the intervention class.** Add to Definition 2.2 the observation-masking operations **O** → **O**′ ⊆ **O** (the agent's policy in a masked task is a map dom(**O**′) → [0,1]), state Theorem 2.4 with the policy assignment quantified over (mixture, observation-subset) pairs, and extend the behavioral transform to the family Δ_M^{**O**′} for **O**′ ⊆ **O**. Lines 185, 220, and 340 must then refer to injectivity of this larger family, and the query model of §3.3 should say whether the analyst may issue masked queries.
2. **Keep the fixed-observation transform but demote the claim.** State Richens–Everitt accurately (with masking) as background, and present fixed-observation injectivity as *open in general*, noting that on the margin class the (M3) condition removes the known single-signed-slice obstruction — which is consistent with Proposition 3.2 (whose proof genuinely uses (M3) and which the audit, correctly in my reading, grades sound) and with Question 4.1 remaining a well-posed open question.

## Verdict line

**CONFIRMED** — Theorem 2.4 as stated in the file is false; the audit's counterexample is correct, hypothesis-compliant, and open-set robust, and the source paper confirms the omitted masking interventions.
