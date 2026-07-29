# Does Löb's rule shorten proofs?

*Open problem MAIS-O11 · posed in [MAIS-A1](../agendas/A1/) as [Question 3.6](../agendas/A1/MAIS-A1.tex#L306) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic · complexity theory. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Löb's rule says: to prove $P$, prove $\Box P \to P$ instead. Does the detour ever save a single symbol? Not one example is known. The stakes are in Löbian cooperation, where bounded agents read each other's source code and cooperate exactly when they find a proof of the other's cooperation within a fixed symbol budget ([MAIS-A1](../agendas/A1/)); without lower bounds on how long such proofs must be, those budgets rest on heuristics alone.

Work in an efficient proof system $S$, in Critch's sense [[C19]](https://arxiv.org/abs/1602.04184): a consistent, recursively axiomatized extension of Peano arithmetic with binary numerals and with abbreviations, so that a long expression used many times is paid for once. Write $\ell_S(\varphi)$ for the least symbol length of an $S$-proof of $\varphi$, and $\Box P$ for arithmetized provability. The default $\mathsf{PA}_{\mathrm{bin}}$ is Peano arithmetic in a Hilbert calculus that the agenda fixes down to the abbreviation grammar and the Gödel coding, since proof lengths depend non-cosmetically on such conventions ([MAIS-A1](../agendas/A1/), §2). One direction is cheap: appending to a shortest proof of $P$ one propositional axiom instance and one modus ponens gives a constant $C_1 = C_1(S)$ with $\ell_S(\Box P \to P) \le \ell_S(P) + C_1(|P|+1)$ for every provable $P$ (agenda, Lemma 3.3). So the reflection instance is never much harder than the sentence; the question is whether it can be genuinely easier. Parikh's speedup [P71] — theorems $A$ for which $\Box A$ has a short proof while every proof of $A$ is far longer — does not settle it, because a short proof of $\Box A \to A$ would combine with the short proof of $\Box A$ to give a short proof of $A$. The overhead $F_{\mathsf{PA}_{\mathrm{bin}}}(k,n)$ below is the maximum of $\ell_S(P)$ over sentences $P$ with $|P|\le n$ and $\ell_S(\Box P\to P)\le k$ (see [MAIS-O1](MAIS-O1.md)).

**Question ([MAIS-A1, Question 3.6](../agendas/A1/MAIS-A1.tex#L306)).**

1. Exhibit $\delta > 0$ and a sequence of sentences $P_i$ with $\ell_S(\Box P_i \to P_i) \to \infty$ and

   $$\ell_S(P_i) \ \ge\  (1+\delta)\ \ell_S(\Box P_i \to P_i) + C_1(|P_i|+1),$$

   beating the trivial toll of the lemma above; that is, exhibit any genuine speedup from Löb's rule. (Here $S = \mathsf{PA}_{\mathrm{bin}}$, or any efficient system of your choice.)
2. Decide Conjecture 3.5 ([MAIS-O10](MAIS-O10.md)): is $F_{\mathsf{PA}_{\mathrm{bin}}}(k,n)$ bounded by a fixed polynomial in $k+n$, or does it grow faster than every polynomial along some sequence $(k_i, n_i)$?

Part 1 asks for a sequence of sentences whose direct proofs are longer, by a fixed factor plus the trivial toll, than the proofs of their reflection instances: the first witness that the detour pays at all. In part 2, Conjecture 3.5 asserts the first alternative, the polynomial bound. The nearest proved lower bounds are Friedman's and Pudlák's [[P17]](https://arxiv.org/abs/1601.01487), for the one instance $P=\bot$ where the hypothesis is unprovable; for the speedup literature and why it falls short here, see [MAIS-A1](../agendas/A1/).

## References

- [C19] A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)
- [P71] R. Parikh, *Existence and feasibility in arithmetic*, Journal of Symbolic Logic 36 (1971), no. 3, 494–508.
- [P17] P. Pudlák, *Incompleteness in the finite domain*, Bulletin of Symbolic Logic 23 (2017), no. 4, 405–441. [arXiv:1601.01487](https://arxiv.org/abs/1601.01487)

*Related: [MAIS-O1](MAIS-O1.md) (the overhead function) · [MAIS-O10](MAIS-O10.md) (the conjecture part 2 decides) · [MAIS-O21](MAIS-O21.md) (whether any answer transfers between proof systems).*
