# A bounded analogue of Solovay's completeness theorem

*Open problem MAIS-O22 · posed in [MAIS-A1](../agendas/A1/MAIS-A1.pdf) as [Question 8.2](../agendas/A1/MAIS-A1.tex#L557) · Status: open.*

*Safety: cooperative AI, agent foundations — Löbian cooperation · proof-based agents · bounded rationality. Mathematics: logic. Difficulty: ★★★ hard.*

Solovay's theorem says Gödel–Löb logic $\mathsf{GL}$ proves a modal formula if and only if every arithmetical realization of it is a theorem of Peano arithmetic. The bounded soundness conjecture ([MAIS-O19](MAIS-O19.md)) is one half of a bounded analogue: every $\mathsf{GL}$-law should remain a law when each box is read as "provable within $k^{c_j}$ symbols." The completeness half should say that non-laws stay non-laws under every choice of budgets — but the quantifiers can be placed in several inequivalent ways, and choosing among them is part of the problem.

Fix an efficient proof system $S$ under the agenda's conventions (default $\mathsf{PA}_{\mathrm{bin}}$). Enumerate the box occurrences of a modal formula $\varphi$ as $1, \dots, s$; a **budget schedule** is a tuple $c = (c_1, \dots, c_s)$ of positive integers; a **realization** $\rho$ assigns each atom a formula in $\mathrm{Lang}_1(S)$ (at most one free variable); and $\varphi^{\rho,c}(k)$ is the arithmetical formula obtained by structural recursion, the $j$-th box becoming "provable in $S$ within $k^{c_j}$ symbols" applied to the instance at the numeral $\overline{k}$.

**Question ([MAIS-A1, Question 8.2](../agendas/A1/MAIS-A1.tex#L557)).** Suppose $\mathsf{GL} \nvdash \varphi$. Is it true that for every budget schedule $c$ there is a realization $\rho$ such that $S \nvdash \forall k > \hat{k}\;\varphi^{\rho,c}(k)$ for every $\hat{k}$?

The agenda flags rather than endorses this formulation. It hard-wires three debatable choices: budgets of the shape $k^{c_j}$ (rather than expansion-composed budgets, or budgets depending on the realization's length); a single shared parameter $k$ (Critch's robust-cooperation theorem already needs two, one per agent); and the weaker quantifier order "for every schedule, some realization fails," where a Solovay-style construction would aim for one realization defeating all schedules — if his self-referential construction survives length accounting. The nearest precedents are the witness-comparison logics of Guaspari–Solovay and the speedup modalities of de Jongh–Montagna, which admit Solovay-style completeness but compare proofs against each other, never against a fixed symbol budget. For those literatures and the formulation choices, see [MAIS-A1](../agendas/A1/MAIS-A1.pdf).

*Related: [MAIS-O19](MAIS-O19.md) (the soundness half) · [MAIS-O18](MAIS-O18.md) (the bounded Löb axiom both halves lean on) · [MAIS-O14](MAIS-O14.md) (budget-scale boundaries a completeness proof must respect).*
