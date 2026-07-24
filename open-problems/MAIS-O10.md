# Polynomial overhead for Löb's theorem

*Open problem MAIS-O10 · posed in [MAIS-A1](../agendas/A1/) as [Conjecture 3.5](../agendas/A1/MAIS-A1.tex#L294) · Status: open.*

*Safety: cooperative AI, agent foundations — Löbian cooperation · proof-based agents · bounded rationality. Mathematics: logic · complexity theory. Difficulty: ★★ project.*

How much can proving $\Box P \to P$ save over proving $P$ directly? If the answer is "only polynomially much," then every proof budget in the Löbian cooperation story — the thresholds at which source-reading agents establish each other's cooperation — becomes polynomially effective. This page states the expected answer; deciding it is the problem.

Work in an efficient proof system, by default $\mathsf{PA}_{\mathrm{bin}}$: Peano arithmetic with binary numerals and an abbreviation rule, all proof lengths counted in symbols. Write $\ell_S(\varphi)$ for the least symbol length of an $S$-proof of $\varphi$ and $\Box P$ for arithmetized provability. The **Löb overhead** is $F_S(k,n)$, the maximum of $\ell_S(P)$ over sentences $P$ with $|P|\le n$ and $\ell_S(\Box P\to P)\le k$: the hardest-to-prove sentence among those whose reflection instance has a $k$-symbol proof (see [MAIS-O1](MAIS-O1.md)). Auditing the standard proof of Löb's theorem step by step — diagonalize, internalize the fixed point, chain with the hypothesis, notice the resulting proof — the agenda's ledger gives the heuristic bound $F_S(k,n) \lesssim \mathcal{E}_S(k + d_S(O(n)) + \mathrm{poly}(n)) + k + d_S(O(n)) + \mathrm{poly}(n)$, where $\mathcal{E}_S(m)$ is the cost of proving "$\varphi$ has an $m$-symbol proof" when you hold such a proof, and $d_S(n)$ is the cost of proving the diagonal fixed-point equivalence for formulas of length $n$.

**Conjecture ([MAIS-A1, Conjecture 3.5](../agendas/A1/MAIS-A1.tex#L294)).** There are constants $C, c$ (depending on the system) with

$$F_{\mathsf{PA}_{\mathrm{bin}}}(k,n) \ \le\  C\ (k+n)^{c} \quad \text{for all } k, n.$$

In the strong form: $F_{\mathsf{PA}_{\mathrm{bin}}}(k,n) \le C\ (k + n^{c})$, i.e. the premise length enters linearly. The strong form would follow from the ledger together with a linear expansion function ($\mathcal{E}_{\mathsf{PA}_{\mathrm{bin}}}(m) = O(m)$) and polynomial $d_S$.

A concrete route in: carry out the ledger for $\mathsf{PA}_{\mathrm{bin}}$ with explicit constants, using the length-tracked derivability conditions in Pudlák's Handbook chapter, and read off explicit $C, c$. No published proof carries this out for any concrete system. For the ledger and the surrounding formalism, see [MAIS-A1](../agendas/A1/).

*Related: [MAIS-O1](MAIS-O1.md) (the overhead function this conjecture answers) · [MAIS-O12](MAIS-O12.md) (the constants $\mathcal{E}_S$ and $d_S$ the strong form needs) · [MAIS-O11](MAIS-O11.md) (the lower-bound counterpart).*
