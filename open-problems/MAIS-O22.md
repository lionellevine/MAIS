# A bounded analogue of Solovay's completeness theorem

*Open problem MAIS-O22 · posed in [MAIS-A1](../agendas/A1/) as [Question 8.2](../agendas/A1/MAIS-A1.tex#L558) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic. Difficulty: ★★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Proof-based agents cooperate by searching for proofs about one another's behavior; a bounded agent can search only within a proof-length budget, so which provability laws survive bounding determines which Löbian cooperation arguments it can run ([MAIS-A1](../agendas/A1/)). Solovay's theorem [S76] pins down the unbounded laws: Gödel–Löb logic $\mathsf{GL}$ proves a modal formula if and only if every arithmetical realization of it is a theorem of Peano arithmetic. The bounded soundness conjecture ([MAIS-O19](MAIS-O19.md)) is one half of a bounded analogue: every $\mathsf{GL}$-law should remain a law when each box is read as "provable within $k^{c_j}$ symbols." The completeness half should say that non-laws stay non-laws under every choice of budgets — but the quantifiers can be placed in several inequivalent ways, and choosing among them is part of the problem.

Fix a proof system $S$ that is **efficient** in Critch's sense [[C19]](../references/C19.md) — an extension of Peano arithmetic with binary numerals and an abbreviation rule, so that symbol counts are not inflated by long numerals or repeated subexpressions; the agenda's default $\mathsf{PA}_{\mathrm{bin}}$ qualifies, and [MAIS-A1](../agendas/A1/) fixes the exact conventions. Enumerate the box occurrences of a modal formula $\varphi$ as $1, \dots, s$; a **budget schedule** is a tuple $c = (c_1, \dots, c_s)$ of positive integers; a **realization** $\rho$ assigns each atom an arithmetical formula with at most one free variable, identified with the shared parameter $k$; and $\varphi^{\rho,c}(k)$ is obtained by structural recursion, the $j$-th box becoming "provable in $S$ within $k^{c_j}$ symbols" applied to the subformula's instance at the numeral $\overline{k}$.

**Question ([MAIS-A1, Question 8.2](../agendas/A1/MAIS-A1.tex#L558)).** Suppose $\mathsf{GL} \nvdash \varphi$. Is it true that for every budget schedule $c$ there is a realization $\rho$ such that $S \nvdash \forall k > \hat{k}\ \varphi^{\rho,c}(k)$ for every $\hat{k}$?

The agenda flags rather than endorses this formulation. It hard-wires three debatable choices: budgets of the shape $k^{c_j}$ (rather than expansion-composed budgets, or budgets depending on the realization's length); a single shared parameter $k$ (Critch's robust-cooperation theorem [[C19]](../references/C19.md), in which two proof-searching agents with possibly different proof-length budgets cooperate, already needs two parameters, one per agent); and the weaker quantifier order "for every schedule, some realization fails," where a Solovay-style construction would aim for one realization defeating all schedules — if his self-referential construction survives length accounting. The nearest precedents are the witness-comparison logics of Guaspari and Solovay [GS79] and the speedup modalities of de Jongh and Montagna [DM89], which admit Solovay-style completeness but compare proofs against each other, never against a fixed symbol budget. For those literatures and the formulation choices, see [MAIS-A1](../agendas/A1/).

## References

- [[S76]](../references/S76.md) R. M. Solovay, *Provability interpretations of modal logic*, Israel Journal of Mathematics 25 (1976), 287–304.
- [GS79] D. Guaspari and R. M. Solovay, *Rosser sentences*, Annals of Mathematical Logic 16 (1979), no. 1, 81–99.
- [DM89] D. H. J. de Jongh and F. Montagna, *Much shorter proofs*, Zeitschrift für mathematische Logik und Grundlagen der Mathematik 35 (1989), 247–260.
- [[C19]](../references/C19.md) A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)

*Related: [MAIS-O19](MAIS-O19.md) (the soundness half) · [MAIS-O18](MAIS-O18.md) (the bounded Löb axiom both halves lean on) · [MAIS-O14](MAIS-O14.md) (budget-scale boundaries a completeness proof must respect).*
