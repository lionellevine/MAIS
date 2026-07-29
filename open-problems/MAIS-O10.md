# Polynomial overhead for Löb's theorem

*Open problem MAIS-O10 · posed in [MAIS-A1](../agendas/A1/) as [Conjecture 3.5](../agendas/A1/MAIS-A1.tex#L295) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic · complexity theory. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

How much can proving $\Box P \to P$ save over proving $P$ directly? If the answer is "only polynomially much," then every proof budget in the Löbian cooperation story — the thresholds at which source-reading agents establish each other's cooperation — becomes polynomially effective. This page states the expected answer; deciding it is the problem.

Work in an efficient proof system, by default $\mathsf{PA}_{\mathrm{bin}}$: Peano arithmetic in Enderton's Hilbert calculus with binary numerals and a priced abbreviation rule (a proof line may define a fresh name for a fixed string, possibly using earlier abbreviations, every character charged, so an expression used many times is paid for once), all proof lengths counted in symbols of the proof file as written. The overhead below depends on these conventions, and [MAIS-A1](../agendas/A1/) fixes them exactly, down to the Gödel coding. Write $\ell_S(\varphi)$ for the least symbol length of an $S$-proof of $\varphi$ and $\Box P$ for arithmetized provability. The **Löb overhead** is $F_S(k,n)$, the maximum of $\ell_S(P)$ over sentences $P$ with $|P|\le n$ and $\ell_S(\Box P\to P)\le k$: the hardest-to-prove sentence among those whose reflection instance has a $k$-symbol proof (see [MAIS-O1](MAIS-O1.md)).

The expected answer comes from the agenda's **ledger**, an itemized symbol-count of the standard proof of Löb's theorem run on a $k$-symbol proof of $\Box P \to P$ with $|P|\le n$: diagonalize to get a sentence $\Psi$ provably equivalent to $\Box\Psi \to P$; derive $\Box\Psi \to \Box P$ by internalized modus ponens and formalized $\Sigma_1$-completeness; chain with the given proof to get $\Box\Psi \to P$, hence $\Psi$ by the fixed point; then notice the proof of $\Psi$ just assembled (the dominant cost) to get $\Box\Psi$, and conclude $P$. Totaled, the ledger gives the heuristic bound $F_S(k,n) \lesssim \mathcal{E}_S(k + d_S(O(n)) + \mathrm{poly}(n)) + k + d_S(O(n)) + \mathrm{poly}(n)$. Here $\mathcal{E}_S$ prices the act of noticing a proof: writing $\Box_m\varphi$ for the arithmetized statement "$\varphi$ has an $S$-proof of at most $m$ symbols," $\mathcal{E}_S$ is the pointwise least computable function such that every $\varphi$ with an $S$-proof of at most $m$ symbols has a proof of $\Box_m\varphi$ in at most $\mathcal{E}_S(m)$ symbols, and $S$ proves $\Box_m\varphi \to \Box_{\mathcal{E}_S(m)}\Box_m\varphi$ for every $\varphi$ and $m$. The constant $d_S(n)$ prices diagonalization: the least $d$ such that every formula $\Phi$ with one free variable and $|\Phi|\le n$ has a fixed point $\Psi$, of length at most a fixed constant multiple of $n$, whose equivalence $\Psi \leftrightarrow \Phi(\ulcorner\Psi\urcorner)$ has an $S$-proof of at most $d$ symbols, where $\ulcorner\Psi\urcorner$ is the numeral of the Gödel code of $\Psi$.

**Conjecture ([MAIS-A1, Conjecture 3.5](../agendas/A1/MAIS-A1.tex#L295)).** There are constants $C, c$ (depending on the system) with

$$F_{\mathsf{PA}_{\mathrm{bin}}}(k,n) \ \le\  C\ (k+n)^{c} \quad \text{for all } k, n.$$

In the strong form: $F_{\mathsf{PA}_{\mathrm{bin}}}(k,n) \le C\ (k + n^{c})$, i.e. the premise length enters linearly. The strong form would follow from the ledger together with a linear expansion function ($\mathcal{E}_{\mathsf{PA}_{\mathrm{bin}}}(m) = O(m)$) and polynomial $d_S$.

A concrete route in: carry out the ledger for $\mathsf{PA}_{\mathrm{bin}}$ with explicit constants, using the length-tracked derivability conditions in Pudlák's Handbook chapter, and read off explicit $C, c$. No published proof carries this out for any concrete system. For the ledger and the surrounding formalism, see [MAIS-A1](../agendas/A1/).

## References

- P. Pudlák, *The lengths of proofs*, in: Handbook of Proof Theory (S. R. Buss, ed.), Elsevier, 1998, pp. 547–637.
- A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)
- P. Pudlák, *Incompleteness in the finite domain*, Bulletin of Symbolic Logic 23 (2017), no. 4, 405–441. [arXiv:1601.01487](https://arxiv.org/abs/1601.01487)

*Related: [MAIS-O1](MAIS-O1.md) (the overhead function this conjecture answers) · [MAIS-O12](MAIS-O12.md) (the constants $\mathcal{E}_S$ and $d_S$ the strong form needs) · [MAIS-O11](MAIS-O11.md) (the lower-bound counterpart).*
