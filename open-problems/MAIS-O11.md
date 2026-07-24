# Does Löb's rule shorten proofs?

*Open problem MAIS-O11 · posed in [MAIS-A1](../agendas/A1/MAIS-A1.pdf) as [Question 3.6](../agendas/A1/MAIS-A1.tex#L305) · Status: open.*

*Safety: cooperative AI, agent foundations — Löbian cooperation · proof-based agents · bounded rationality. Mathematics: logic · complexity theory. Difficulty: ★★★ hard.*

Löb's rule says: to prove $P$, prove $\Box P \to P$ instead. Does the detour ever save a single symbol? Not one example is known — and without lower bounds, the proof budgets in Löbian cooperation rest on heuristics alone.

Work in an efficient proof system $S$ (a consistent, recursively axiomatized extension of Peano arithmetic with binary numerals and abbreviations; the default is $\mathsf{PA}_{\mathrm{bin}}$), with $\ell_S(\varphi)$ the least symbol length of an $S$-proof and $\Box P$ arithmetized provability. One direction is cheap: appending to a shortest proof of $P$ one propositional axiom instance and one modus ponens gives a constant $C_1 = C_1(S)$ with $\ell_S(\Box P \to P) \le \ell_S(P) + C_1(|P|+1)$ for every provable $P$ (agenda, Lemma 3.3). So the reflection instance is never much harder than the sentence; the question is whether it can be genuinely easier. Parikh's speedup — theorems $A$ for which $\Box A$ has a short proof while every proof of $A$ is far longer — does not settle it, because a short proof of $\Box A \to A$ would combine with the short proof of $\Box A$ to give a short proof of $A$. The overhead $F_{\mathsf{PA}_{\mathrm{bin}}}(k,n)$ below is the maximum of $\ell_S(P)$ over sentences $P$ with $|P|\le n$ and $\ell_S(\Box P\to P)\le k$ (see [MAIS-O1](MAIS-O1.md)).

**Question ([MAIS-A1, Question 3.6](../agendas/A1/MAIS-A1.tex#L305)).**

1. Exhibit $\delta > 0$ and a sequence of sentences $P_i$ with $\ell_S(\Box P_i \to P_i) \to \infty$ and

   $$\ell_S(P_i) \ \ge\  (1+\delta)\ \ell_S(\Box P_i \to P_i) + C_1(|P_i|+1),$$

   beating the trivial toll of the lemma above; that is, exhibit any genuine speedup from Löb's rule. (Here $S = \mathsf{PA}_{\mathrm{bin}}$, or any efficient system of your choice.)
2. Decide Conjecture 3.5 ([MAIS-O10](MAIS-O10.md)): is $F_{\mathsf{PA}_{\mathrm{bin}}}(k,n)$ bounded by a fixed polynomial in $k+n$, or does it grow faster than every polynomial along some sequence $(k_i, n_i)$?

Part 1 asks for a sequence of sentences whose direct proofs are longer, by a fixed factor plus the trivial toll, than the proofs of their reflection instances: the first witness that the detour pays at all. The nearest proved lower bounds are Friedman's and Pudlák's, for the one instance $P=\bot$ where the hypothesis is unprovable; for the speedup literature and why it falls short here, see [MAIS-A1](../agendas/A1/MAIS-A1.pdf).

*Related: [MAIS-O1](MAIS-O1.md) (the overhead function) · [MAIS-O10](MAIS-O10.md) (the conjecture part 2 decides) · [MAIS-O21](MAIS-O21.md) (whether any answer transfers between proof systems).*
