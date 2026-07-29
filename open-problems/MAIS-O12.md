# Expansion and diagonalization costs in Peano arithmetic

*Open problem MAIS-O12 · posed in [MAIS-A1](../agendas/A1/) as [Problem 3.7](../agendas/A1/MAIS-A1.tex#L323) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic · complexity theory. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

If you hold an $m$-symbol proof of $\varphi$ in your hand, how many symbols does it take to prove the sentence "$\varphi$ has an $m$-symbol proof"? Every quantitative Löbian argument — the overhead of Löb's theorem, the FairBot cooperation threshold — reduces to two such system constants, and neither has been determined for any concrete system.

Work in $\mathsf{PA}_{\mathrm{bin}}$: Peano arithmetic in Enderton's Hilbert calculus with binary numerals and an abbreviation rule (a proof line may define a fresh symbol as shorthand, every character charged), proof lengths counted in symbols; $S\vdash_{\le k}\varphi$ means $\varphi$ has an $S$-proof of at most $k$ symbols, and $\Box_m\varphi$ is the arithmetized statement "$\varphi$ has an $S$-proof of at most $m$ symbols." An **expansion function** for $S$ is a computable $\mathcal{E}$ satisfying *bounded necessitation* — $S \vdash_{\le m} \varphi$ implies $S \vdash_{\le \mathcal{E}(m)} \Box_m \varphi$ — and *bounded inner necessitation* — $S \vdash \Box_m \varphi \to \Box_{\mathcal{E}(m)} \Box_m \varphi$ for all $\varphi$ and $m$; the pointwise least one, $\mathcal{E}_S$, exists and is computable (agenda, Definition 2.1 and following). The second constant prices self-reference: $d_S(n)$ is the least $d$ such that every formula $\Phi$ with one free variable and $|\Phi| \le n$ has a fixed point $\Psi$ with $|\Psi| \le C_0(n+1)$ and $S \vdash_{\le d} \Psi \leftrightarrow \Phi(\ulcorner \Psi \urcorner)$, where $\ulcorner \Psi \urcorner$ is the numeral of the Gödel code of $\Psi$ and $C_0$ is a fixed constant bounding the size of the standard diagonal construction (the value of $d_S$ depends on the choice of $C_0$; any fixed choice serves).

**Problem ([MAIS-A1, Problem 3.7](../agendas/A1/MAIS-A1.tex#L323)).** For $S = \mathsf{PA}_{\mathrm{bin}}$: determine $\mathcal{E}_S$ and $d_S$ up to constant factors. In particular, decide whether $\mathcal{E}_S(m) = O(m)$, as Critch's engineering estimate suggests, or whether internalization has an inherent superlinear cost; and determine the least degree of $d_S$ for the standard diagonal construction and for any construction.

Critch's engineering estimate [[C19]](../references/C19.md) is his remark that a linear expansion function "seems reasonable to expect" of a proof system engineered for easy checking; no such bound has been proved for any concrete system. In the last clause, the degree of $d_S$ is its exponent of polynomial growth (standard length-of-proofs techniques should give polynomial upper bounds), and the two readings differ in what $\Psi$ may be: the fixed point the standard construction produces, or any fixed point within the length bound.

The techniques should be in reach: Pudlák's Handbook chapter [P98] proves the derivability conditions with length tracking, and the same calculation would produce the certified bound on $\mathcal{E}$ that the bounded FairBot theorem assumes. That theorem, after Critch [[C19]](../references/C19.md), says that two copies of $\mathrm{FairBot}_k$ — the agent that cooperates in a one-shot Prisoner's Dilemma exactly when it finds an $S$-proof of at most $k$ symbols that its opponent cooperates — do cooperate for all $k$ above a finite threshold, provided $S$ itself certifies a suitable bound on $\mathcal{E}$. For the definitions in full and the ledger these constants dominate, see [MAIS-A1](../agendas/A1/).

## References

- [[C19]](../references/C19.md) A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)
- [[P98]](../references/P98.md) P. Pudlák, *The lengths of proofs*, in: Handbook of Proof Theory (S. R. Buss, ed.), Elsevier, 1998, pp. 547–637.

*Related: [MAIS-O10](MAIS-O10.md) (polynomial overhead follows from linear $\mathcal{E}_S$ and polynomial $d_S$) · [MAIS-O16](MAIS-O16.md) (the cooperation threshold whose finiteness needs the certified $\mathcal{E}$ bound) · [MAIS-O20](MAIS-O20.md) (a route that avoids $d_S$ entirely).*
