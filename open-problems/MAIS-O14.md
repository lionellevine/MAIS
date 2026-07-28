# Bounded Löb at logarithmic proof budgets

*Open problem MAIS-O14 · posed in [MAIS-A1](../agendas/A1/) as [Question 4.5](../agendas/A1/MAIS-A1.tex#L374) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

For which proof budgets does the parametric bounded Löb theorem hold? Above a certain growth rate it is a theorem; below, it provably fails; between the two lies an undecided logarithmic window — the scale at which a budget can just afford to write down the numeral of its own parameter.

Fix an efficient proof system, by default $\mathsf{PA}_{\mathrm{bin}}$ (Peano arithmetic with binary numerals and abbreviations). For $p$ a formula with at most one free variable and $f$ a represented budget, $\Box_{f(k)}\ p(k)$ is the formula with free variable $k$ asserting that the instance $p(\overline{k})$ (with $\overline{k}$ the binary numeral of $k$) has an $S$-proof of at most $f(k)$ symbols. Say **PBL holds for $(S,f)$** if for every such $p$: whenever $S \vdash \forall k\ (\Box_{f(k)}\ p(k) \to p(k))$, there exists $\hat{k}$ with $S \vdash \forall k > \hat{k}\ p(k)$ (agenda, Definition 4.2). The repaired parametric theorem gives PBL for every *internally regular* budget — one that $S$ proves eventually exceeds the cost of noticing a proof at numeral-length scale plus any fixed multiple of the numeral length. In the other direction, PBL fails for every provably bounded budget (take $p = \bot$; the hypothesis holds vacuously), and in systems without abbreviations for every provably sub-logarithmic budget. Abbreviations compress numerals, so that failure proof breaks in $\mathsf{PA}_{\mathrm{bin}}$: the window is genuinely open. Write $\lambda(k) := |\overline{k}|+1$ for the numeral-length budget and $\lambda_{a/b}(k) := \lfloor a\lambda(k)/b \rfloor$ for its rational scalings; $\mathcal{B}$-terms are the members of the agenda's search-free budget algebra, each carrying its canonical graph.

**Question ([MAIS-A1, Question 4.5](../agendas/A1/MAIS-A1.tex#L374)).** For $S = \mathsf{PA}_{\mathrm{bin}}$, does PBL hold for the canonical numeral-length budget $f = \lambda$? For the canonical budgets $\lambda_{a/b}$ with fixed $0 < a < b$? More ambitiously, characterize the $\mathcal{B}$-terms $f$ for which PBL holds. The graph is part of each term, so this is a property of a finite syntactic object rather than of an extensional function with many presentations.

A failure proof must survive numeral compression (for $k = 2^{2^m}$, repeated squaring writes $\overline{k}$ in far fewer than $\log k$ symbols); a success proof must run on a budget too small for internal regularity. Either outcome would locate the exact boundary of the Löbian argument. For the failure proposition, the abbreviation wrinkle, and the repaired theorem, see [MAIS-A1](../agendas/A1/); the refutation that forced the repair is [MAIS-P2](../papers/P2/).

*Related: [MAIS-O13](MAIS-O13.md) (provable comparisons between the budget terms in play) · [MAIS-O15](MAIS-O15.md) (explicit thresholds above the window) · [MAIS-O18](MAIS-O18.md) (the same admissibility question one box deeper).*
