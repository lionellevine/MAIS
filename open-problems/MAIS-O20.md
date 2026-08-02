# A bounded Payor lemma and its cooperation threshold

*Open problem MAIS-O20 · posed in [MAIS-A1](../agendas/A1/) as [Problem 5.4](../agendas/A1/MAIS-A1.tex#L486) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · open-source game theory · program equilibrium · proof-based agents · bounded rationality · logic. Difficulty: ★★.*

*Authored by: Claude Fable 5 directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Löb's theorem has a rival. Payor's lemma — proved by James Payor and written up by Critch [[C23]](https://www.lesswrong.com/posts/2WpPRrqrFQa6n2x3W/) — says: if $S \vdash \Box(\Box\varphi \to \varphi) \to \varphi$, then $S \vdash \varphi$ — and its four-line proof uses neither the diagonal lemma nor inner necessitation. In the bounded setting those absences are savings: the diagonalization cost $d_S$ (constructing a self-referential sentence and proving its defining equivalence) and the inner-necessitation half of the expansion cost $\mathcal{E}_S$ (converting an $m$-symbol proof of $\varphi$ into an $S$-proof that $\varphi$ has an $m$-symbol proof) drop out of the bookkeeping. Does the cheaper route give a smaller cooperation threshold?

Fix an **efficient** proof system $S$ in the sense of Critch [[C19]](../references/C19.md) — roughly, Peano Arithmetic with binary numerals and an abbreviation rule, so that proof length in symbols is an honest cost measure; the default $\mathsf{PA}_{\mathrm{bin}}$ is fixed in [MAIS-A1](../agendas/A1/) down to checker and coding. For $p \in \mathrm{Lang}_1(S)$ (at most one free variable) and represented budgets $f, g$ (computable functions whose graph formulas $S$ proves total and single-valued), the formula $\Box_{f(k)}\ p(k)$ asserts that the instance $p(\overline{k})$ (with $\overline{k}$ the binary numeral of $k$) has an $S$-proof of at most $f(k)$ symbols; $\lambda(k) := |\overline{k}|+1$ is the numeral-length budget; and $u \leq_S^{\ast } v$ means $S$ proves $u(k) \le v(k)$ beyond some standard threshold.

Payor's handshake has a bounded agent, the analogue of the $\mathrm{FairBot}_k$ of Barász, Christiano, Fallenstein, Herreshoff, LaVictoire, and Yudkowsky [[BCFH+14]](../references/BCFH+14.md). The arena is the program-game Prisoner's Dilemma, where each player is an algorithm handed the other's source code — the standard model of AI agents transparent to one another. There $\mathrm{FairBot}_k$ plays $\mathsf{C}$ (cooperate) if and only if it finds an $S$-proof of at most $k$ symbols that its opponent cooperates against it; $\mathrm{PB}_k(\mathrm{Opp})$ instead searches all $S$-proofs of at most $k$ symbols for a proof of $\Box_k c \to c$, where $c$ is the sentence "$\mathrm{PB}_k(\mathrm{Opp}) = \mathsf{C}$ and $\mathrm{Opp}(\mathrm{PB}_k) = \mathsf{C}$" (both self-references by Kleene's recursion theorem), playing $\mathsf{C}$ if it finds one and $\mathsf{D}$ (defect) otherwise. Where $\mathrm{FairBot}_k$ demands a proof of the opponent's cooperation, $\mathrm{PB}_k$ demands a proof that provable mutual cooperation implies mutual cooperation. Write $\hat{k}^{\ast }$ for the FairBot cooperation threshold: the least $K$ such that two copies of $\mathrm{FairBot}_k$ cooperate for all $k \ge K$ — possibly infinite; even its finiteness is open ([MAIS-O16](MAIS-O16.md)).

**Problem ([MAIS-A1, Problem 5.4](../agendas/A1/MAIS-A1.tex#L486)).** Let $S$ satisfy the conventions above. Determine internal comparison conditions on represented budgets $f, g$ under which, for every $p \in \mathrm{Lang}_1(S)$,

$$S \vdash \forall k\ \Bigl(\Box_{g(k)}\bigl(\Box_{f(k)}\ p(k) \to p(k)\bigr) \to p(k)\Bigr) \quad\Longrightarrow\quad \exists\ \hat{k}:\ S \vdash \forall k > \hat{k}\ p(k),$$

with explicit $\hat{k}$. In particular, test whether the certificates $b\lambda \leq_S^{\ast } g$ and $f + b\lambda \leq_S^{\ast } g$ for every standard $b$ suffice. Then prove that two copies of $\mathrm{PB}_k$ cooperate above an explicit threshold $\hat{k}^{\ast }_{\mathrm{P}}$, and compare it with $\hat{k}^{\ast }$ in a common system and encoding.

The proof should use only bounded necessitation, quantifier distribution, and implication distribution — the bounded counterparts of the modal rules in the four-line unbounded proof, stated with exact constants in [MAIS-A1](../agendas/A1/); the unbounded proof is the map. A short, self-contained note tabulating the comparison against the bounded Löb route — which hypothesis shapes, which budget windows, which thresholds — would be a complete first paper.

## References

- [C23] A. Critch, *Modal fixpoint cooperation without Löb's theorem*, LessWrong, February 2023 (the central lemma is credited there to James Payor). [lesswrong.com/posts/2WpPRrqrFQa6n2x3W](https://www.lesswrong.com/posts/2WpPRrqrFQa6n2x3W/)
- [[C19]](../references/C19.md) A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)
- [[BCFH+14]](../references/BCFH+14.md) M. Barász, P. Christiano, B. Fallenstein, M. Herreshoff, P. LaVictoire, and E. Yudkowsky, *Robust cooperation in the Prisoner's Dilemma: program equilibrium via provability logic*, 2014. [arXiv:1401.5577](https://arxiv.org/abs/1401.5577)

*Related: [MAIS-O16](MAIS-O16.md) (the FairBot threshold to beat) · [MAIS-O15](MAIS-O15.md) (explicit thresholds on the Löb route) · [MAIS-O12](MAIS-O12.md) (the system constants Payor's proof avoids).*
