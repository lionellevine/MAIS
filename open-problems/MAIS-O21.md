# Is the Löb overhead invariant under polynomial simulation?

*Open problem MAIS-O21 · posed in [MAIS-A1](../agendas/A1/) as [Problem 8.1](../agendas/A1/MAIS-A1.tex#L544) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic · complexity theory. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The Löb overhead $F_S(k,n)$ — the least proof length of the hardest-to-prove sentence $P$ of length at most $n$ whose reflection instance $\Box P \to P$ has a proof of at most $k$ symbols — depends on the proof calculus, the numeral system, the abbreviation discipline, and the Gödel coding. The dependence is not cosmetic: whether numerals can be compressed changes which proof budgets are even admissible in the bounded Löb theorem. Proof complexity's classical remedy is to work up to polynomial simulation. Does the remedy apply here?

The obstacle is that $F_S$ mentions provability *inside* the arithmetic: the bounded-provability formula $\Box_k \varphi$ of system $S$ speaks of $S$-proofs and $S$-budgets, and a translation into $S'$ must not only carry proofs across at polynomial cost but also provably align the two systems' internal notions of "has a proof of at most $k$ symbols." The statement makes both requirements explicit.

**Problem ([MAIS-A1, Problem 8.1](../agendas/A1/MAIS-A1.tex#L544)).** Suppose $S$ and $S'$ prove the same theory. Specify polynomial-size translations of formulas and proofs in both directions, together with polynomial-size $S$- and $S'$-proofs that each translated bounded-provability predicate agrees with the source predicate at the translated budget. Under these hypotheses, prove that $F_S$ and $F_{S'}$ are polynomially related:

$$F_S(k,n) \le p\bigl(F_{S'}(q(k), q(n)),\  k,\  n\bigr)$$

for some polynomials $p, q$, and symmetrically. Or exhibit polynomially simulating systems for which no such alignment of the bounded boxes exists.

Until this is settled, "determine the least Löb overhead" must be read per system, with $\mathsf{PA}_{\mathrm{bin}}$ as the declared default, and the sub-polynomial structure of $F$ — the logarithmic window, the constants in the FairBot threshold — is convention-laden by nature. For the definition of $F_S$ and the evidence that the dependence is real, see [MAIS-A1](../agendas/A1/).

*Related: [MAIS-O1](MAIS-O1.md) (the overhead function itself) · [MAIS-O10](MAIS-O10.md) (polynomial overhead, which robustness would make system-independent) · [MAIS-O14](MAIS-O14.md) (sub-polynomial structure that cannot be robust).*
