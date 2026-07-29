# Soundness of Gödel–Löb logic under polynomial budgets

*Open problem MAIS-O19 · posed in [MAIS-A1](../agendas/A1/) as [Conjecture 5.3](../agendas/A1/MAIS-A1.tex#L463) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Solovay [S76] proved that Gödel–Löb logic $\mathsf{GL}$ — propositional modal logic with the distribution axiom $\Box(A \to B) \to (\Box A \to \Box B)$, the Löb axiom $\Box(\Box A \to A) \to \Box A$, and the necessitation rule — captures exactly the propositional laws of provability in Peano arithmetic. For proof-based agents — programs that cooperate when they find a proof, within a budget, that their counterpart cooperates — the provability that matters is the budgeted kind. Do Solovay's laws survive when every "provable" becomes "provable within $k^c$ symbols"? Critch conjectured they do, in the paper that proved his parametric resource-bounded Löb theorem [[C19]](https://arxiv.org/abs/1602.04184); making the conjecture precise already takes some care.

Fix a proof system $S$ that is **efficient** in Critch's sense [[C19]](https://arxiv.org/abs/1602.04184): a consistent, recursively axiomatized extension of Peano arithmetic with binary numerals and priced abbreviations, proof length counted in symbols; the default $\mathsf{PA}_{\mathrm{bin}}$ is fixed, down to its Gödel coding, in [MAIS-A1](../agendas/A1/). Write $\Box_m \psi$ for the arithmetized statement "$\psi$ has an $S$-proof of at most $m$ symbols." Three quantities attached to $S$ enter the hypothesis below: the **expansion function** $\mathcal{E}$, the price of noticing a proof (every $\varphi$ provable in at most $m$ symbols has a proof of $\Box_m \varphi$ within $\mathcal{E}(m)$ symbols, and $S$ proves $\Box_m \varphi \to \Box_{\mathcal{E}(m)} \Box_m \varphi$ — bounded inner necessitation); the **diagonalization cost** $d_S(n)$, the price of proving diagonal-lemma fixed-point equivalences for formulas of length at most $n$; and a *certified* bound $E^\sharp$ on $\mathcal{E}$, a term of the agenda's search-free **budget algebra** $\mathcal{B}$ (which contains all polynomials in $k$) that $S$ proves dominates $\mathcal{E}$.

Enumerate the box occurrences of a modal formula $\varphi$ as $1, \dots, s$. A **budget schedule** is a tuple $c = (c_1, \dots, c_s)$ of positive integers. Given a **realization** $\rho$ assigning each atom a formula in $\mathrm{Lang}_1(S)$ (at most one free variable), define $\varphi^{\rho,c}(k)$ by structural recursion: atoms go to their realizations, connectives commute, and the $j$-th box receives the budget $k^{c_j}$, so that $\Box \psi$ becomes "$\psi(\overline{k})$ has an $S$-proof of at most $k^{c_j}$ symbols" (with $\overline{k}$ the binary numeral of $k$).

**Conjecture ([MAIS-A1, Conjecture 5.3](../agendas/A1/MAIS-A1.tex#L463)).** Let $S$ satisfy the conventions above, with a polynomial $\mathcal{B}$-term bound $E^\sharp$ on $\mathcal{E}$ and a polynomial bound on $d_S$. For every modal formula $\varphi$ with $\mathsf{GL} \vdash \varphi$ there is a budget schedule $c$ (depending on $S$ and $\varphi$ only) such that for every realization $\rho$ there is $\hat{k}$ with

$$S \vdash \forall k > \hat{k}\ \  \varphi^{\rho,c}(k).$$

In words: every law of provability logic remains a law when every "provable" is replaced by "provable within $k^{c_j}$ symbols," for exponents chosen once per law, uniformly in the subject matter and for all sufficiently large $k$. The expected proof inducts on a $\mathsf{GL}$-derivation — the distribution axiom is Critch's implication-distribution lemma (gluing a proof of an implication to a proof of its antecedent costs only a constant), the axiom $\Box A \to \Box\Box A$ is bounded inner necessitation, modus ponens composes schedules after a polarity-respecting harmonization of budgets — and the Löb axiom case, [MAIS-O18](MAIS-O18.md), is the real content. For the conventions and the harmonization sketch, see [MAIS-A1](../agendas/A1/).

## References

- [C19] A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)
- [S76] R. M. Solovay, *Provability interpretations of modal logic*, Israel Journal of Mathematics 25 (1976), 287–304.

*Related: [MAIS-O18](MAIS-O18.md) (the Löb axiom case) · [MAIS-O22](MAIS-O22.md) (the completeness converse) · [MAIS-O12](MAIS-O12.md) (the polynomial bounds on $\mathcal{E}$ and $d_S$ the hypothesis needs).*
