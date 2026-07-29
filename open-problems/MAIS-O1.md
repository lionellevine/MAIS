# Quantitative bounded Löb

*Open problem MAIS-O1 · headline problem 1 of the survey [MAIS-P1](../papers/P1/) · canonically formalized in [MAIS-A1](../agendas/A1/) as [Problem 3.4](../agendas/A1/MAIS-A1.tex#L276) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic · complexity theory. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Löb's theorem converts a proof of "if $P$ is provable then $P$" into a proof of $P$. The conversion is an explicit construction, so it has a cost, measured in symbols of proof. That cost is what a transparent software agent pays to conclude cooperation from its opponent's conditional promise of cooperation, so quantifying it would turn the Löbian argument from a possibility theorem into a budget.

Fix a proof system $S$ that is *efficient* in Critch's sense [[C19]](../references/C19.md): a consistent, recursively axiomatized extension of Peano arithmetic with binary numerals (the numeral for $k$ has length $O(\log k)$) and an abbreviation rule, so that a long expression used many times is paid for once. Write $S\vdash_{\le k}\varphi$ for "$\varphi$ has an $S$-proof of at most $k$ symbols," $\ell_S(\varphi)$ for the least length in symbols of an $S$-proof of $\varphi$, $|\varphi|$ for the length of the formula $\varphi$, and $\Box P$ for the arithmetized statement "$P$ is provable in $S$." The concrete default $\mathsf{PA}_{\mathrm{bin}}$ is Peano arithmetic in Enderton's Hilbert calculus with binary numerals and a priced abbreviation mechanism; the exact calculus, abbreviation grammar, and Gödel coding are fixed in [MAIS-A1](../agendas/A1/), and the overhead defined below depends on those choices. The agenda's Definition 3.1 sets

$$F_S(k,n) := \max\bigl\lbrace \ \ell_S(P) :\ P \text{ a sentence of } \mathrm{Lang}(S),\ |P|\le n,\ \ell_S(\Box P\to P)\le k\ \bigr\rbrace , \qquad \max\emptyset := 0.$$

In words: among all sentences of length at most $n$ whose reflection instance $\Box P \to P$ has a proof of at most $k$ symbols, $F_S(k,n)$ is the length of the hardest one to prove outright. Löb's theorem makes every such $P$ provable, so $F_S$ is a well-defined, total computable function, and it is the pointwise least monotone overhead for which $S\vdash_{\le k}(\Box P\to P)$ implies $S\vdash_{\le F_S(k,|P|)}P$ (agenda, Proposition 3.2). Computability puts no ceiling on growth.

**Problem ([MAIS-A1, Problem 3.4](../agendas/A1/MAIS-A1.tex#L276)).** Determine the asymptotic growth of $F_{\mathsf{PA}_{\mathrm{bin}}}(k,n)$, up to constant factors in $k$ and $n$. (The growth is joint: for fixed $k$ only finitely many sentences $P$ satisfy $\ell_S(\Box P \to P) \le k$, and for fixed $n$ only finitely many satisfy $|P| \le n$, so $F_{\mathsf{PA}_{\mathrm{bin}}}$ is eventually constant in each argument separately; the agenda's Conjecture 3.5, [MAIS-O10](MAIS-O10.md), states the expected joint answer.) The same question may be asked for every efficient proof system.

Auditing the standard proof of Löb's theorem gives a heuristic upper bound whose dominant term is one internalization of the assembled proof, priced by the system's expansion function $\mathcal{E}_S$, the cost of noticing a proof: whenever $\varphi$ has an $S$-proof of at most $m$ symbols, $\mathcal{E}_S(m)$ symbols suffice to prove the sentence "$\varphi$ has an $S$-proof of at most $m$ symbols." The nearest proved relatives are the Friedman–Pudlák bounds for the corner $P=\bot$ (surveyed by Pudlák [[P17]](https://arxiv.org/abs/1601.01487)), where the answer lies between two polynomials. For the audit, the proof-system conventions, and what is known, see [MAIS-A1](../agendas/A1/). Auditing the problem's source theorem, Critch's parametric resource-bounded generalization of Löb's theorem [[C19]](../references/C19.md), produced a refutation of its unrestricted form (counterexamples that depend on the choice of proof search) and a repair, published as [MAIS-P2](../papers/P2/).

## References

- [[C19]](../references/C19.md) A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)
- [P17] P. Pudlák, *Incompleteness in the finite domain*, Bulletin of Symbolic Logic 23 (2017), no. 4, 405–441. [arXiv:1601.01487](https://arxiv.org/abs/1601.01487)

*Related: [MAIS-O10](MAIS-O10.md) (the conjectured polynomial answer) · [MAIS-O11](MAIS-O11.md) (the lower-bound half: any genuine speedup from Löb's rule) · [MAIS-O12](MAIS-O12.md) (the two system constants in the upper bound) · [MAIS-O16](MAIS-O16.md) (the cooperation threshold this overhead prices).*
