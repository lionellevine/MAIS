# Cooperation thresholds over families of bounded agents

*Open problem MAIS-O17 · posed in [MAIS-A1](../agendas/A1/) as [Question 4.9](../agendas/A1/MAIS-A1.tex#L410) · Status: open.*

*Tags: cooperative AI · open-source game theory · program equilibrium · Löbian cooperation · bounded rationality · logic · complexity theory. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Two copies of Critch's $\mathrm{FairBot}_k$ cooperate in the Prisoner's Dilemma once the proof budget $k$ passes a threshold. That is one point of a landscape: over *all* pairs of transparent agents of bounded description length, how fast does the cooperation threshold grow?

The setting is the program game version of the Prisoner's Dilemma: each player is an algorithm handed the other's source code, playing $\mathsf{C}$ (cooperate) or $\mathsf{D}$ (defect), with provability read in a fixed efficient proof system $S$ and all proof lengths counted in symbols. Critch's robust cooperation criterion applies to agents that are *fair* relative to a proof-budget function $G$: the agent provably cooperates whenever its opponent's cooperation has a proof within the budget that $G$ allots. In the statement, $G$ is such a budget function, implemented as a term of the agenda's search-free budget algebra $\mathcal{B}$; a *uniform $G$-fairness implication* is the $S$-proof, uniform in $k$, certifying this conditional cooperation for a given family; $\mathcal{E}_S$ and $d_S$ are the system's expansion and diagonalization costs ([MAIS-O12](MAIS-O12.md)); and $f \succ g$ means $f$ eventually dominates every constant multiple of $g$.

**Question ([MAIS-A1, Question 4.9](../agendas/A1/MAIS-A1.tex#L410)).** Fix a canonical $\mathcal{B}$-term implementation of $G$. A *uniform agent family* is one generator program taking $k$ as input. For a pair of such families $(A, B)$, let $r(A,B)$ be the least $K$ such that $A_k(B_k) = B_k(A_k) = \mathsf{C}$ for all $k \ge K$. Let $r_G(\ell, L)$ be the maximum of $r(A,B)$ over pairs whose two generators have at most $\ell$ symbols and whose uniform $G$-fairness implications have proofs of at most $L$ symbols, with maximum of the empty set equal to $0$.

Once the repaired cooperation theorem applies, $r_G(\ell, L)$ is finite because only finitely many generators and certificate proofs meet these bounds. Give an effective upper bound, and decide whether it is polynomial in $\ell + L$ under polynomial bounds on $\mathcal{E}_S$ and $d_S$. Compare the published condition $G(\ell) \succ \mathcal{E}(O(\ell))$ with the stronger proof-internal inequality in the earlier arXiv argument; in either form, use internal certificates rather than external growth alone.

In words: $r_G(\ell, L)$ is the worst cooperation threshold over all mutually fair agent pairs describable in $\ell$ symbols and certifiable in $L$; the question is whether transparency scales — whether the budget needed for cooperation grows only polynomially in the complexity of the agents. For the cooperation theorem, the certificate conventions, and Critch's criterion, see [MAIS-A1](../agendas/A1/); the refutation and repair of the source cooperation theorem are proved in [MAIS-P2](../papers/P2/).

*Related: [MAIS-O16](MAIS-O16.md) (the single FairBot pair this generalizes) · [MAIS-O15](MAIS-O15.md) (explicit thresholds in the underlying theorem) · [MAIS-O20](MAIS-O20.md) (the same game for Payor's handshake).*
