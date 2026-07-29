# Is the Löb overhead invariant under polynomial simulation?

*Open problem MAIS-O21 · posed in [MAIS-A1](../agendas/A1/) as [Problem 8.1](../agendas/A1/MAIS-A1.tex#L545) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic · complexity theory. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

The Löb overhead $F_S(k,n)$ — the least proof length of the hardest-to-prove sentence $P$ of length at most $n$ whose reflection instance $\Box P \to P$ has a proof of at most $k$ symbols, the box being the ordinary unbounded provability predicate "$P$ is provable in $S$" — depends on the proof calculus, the numeral system, the abbreviation discipline, and the Gödel coding.

The dependence is not cosmetic, and it matters: the overhead prices the Löbian argument by which proof-based agents cooperate ([MAIS-O1](MAIS-O1.md)), so if $F_S$ is an artifact of coding conventions, the cooperation thresholds built on it are too. The evidence is a theorem of Critch [[C19]](../references/C19.md), who generalized Löb's theorem to proofs of bounded length: whether the bounded theorem admits a given proof budget turns on whether numerals can be compressed by an abbreviation rule — a matter of pure convention (the failure and repair arguments are in [MAIS-A1](../agendas/A1/)). Proof complexity's classical remedy for convention-dependence is to work up to polynomial simulation (see Pudlák [P98]). Does the remedy apply here?

The obstacle is that $F_S$ mentions provability *inside* the arithmetic, with budgets attached: the bounded-provability formula $\Box_k \varphi$ of system $S$ asserts that $\varphi$ has an $S$-proof of at most $k$ symbols, so it speaks of $S$-proofs and $S$-budgets. A translation into $S'$ must not only carry proofs across at polynomial cost but also provably align the two systems' internal notions of "has a proof of at most $k$ symbols." The statement makes both requirements explicit.

**Problem ([MAIS-A1, Problem 8.1](../agendas/A1/MAIS-A1.tex#L545)).** Suppose $S$ and $S'$ prove the same theory. Specify polynomial-size translations of formulas and proofs in both directions, together with polynomial-size $S$- and $S'$-proofs that each translated bounded-provability predicate agrees with the source predicate at the translated budget. Under these hypotheses, prove that $F_S$ and $F_{S'}$ are polynomially related:

$$F_S(k,n) \le p\bigl(F_{S'}(q(k), q(n)),\  k,\  n\bigr)$$

for some polynomials $p, q$, and symmetrically. Or exhibit polynomially simulating systems for which no such alignment of the bounded boxes exists.

Until this is settled, "determine the least Löb overhead" must be read per system, with $\mathsf{PA}_{\mathrm{bin}}$ (Peano arithmetic with binary numerals and an abbreviation rule; the exact calculus and coding are fixed in [MAIS-A1](../agendas/A1/)) as the declared default; and the sub-polynomial structure of $F$ is convention-laden by nature. That structure includes the logarithmic window ([MAIS-O14](MAIS-O14.md)) — the budget scale at which the bounded Löb theorem is neither known to hold nor known to fail — and the constants in the FairBot threshold ([MAIS-O16](MAIS-O16.md)), the least budget at which two copies of Critch's proof-searching agent $\mathrm{FairBot}_k$ [[C19]](../references/C19.md) provably cooperate.

## References

- [[P98]](../references/P98.md) P. Pudlák, *The lengths of proofs*, in: Handbook of Proof Theory (S. R. Buss, ed.), Elsevier, 1998, pp. 547–637.
- [[C19]](../references/C19.md) A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)

*Related: [MAIS-O1](MAIS-O1.md) (the overhead function itself) · [MAIS-O10](MAIS-O10.md) (polynomial overhead, which robustness would make system-independent) · [MAIS-O14](MAIS-O14.md) (sub-polynomial structure that cannot be robust).*
