# A bounded Payor lemma and its cooperation threshold

*Open problem MAIS-O20 · posed in [MAIS-A1](../agendas/A1/MAIS-A1.pdf) as [Problem 5.4](../agendas/A1/MAIS-A1.tex#L485) · Status: open.*

*Safety: cooperative AI, agent foundations — Löbian cooperation · open-source game theory · program equilibrium · proof-based agents · bounded rationality. Mathematics: logic. Difficulty: ★★ project.*

Löb's theorem has a rival. Payor's lemma says: if $S \vdash \Box(\Box\varphi \to \varphi) \to \varphi$, then $S \vdash \varphi$ — and its four-line proof uses neither the diagonal lemma nor inner necessitation. In the bounded setting those absences are savings: the diagonalization cost $d_S$ and the inner-necessitation half of the expansion cost $\mathcal{E}_S$ drop out of the bookkeeping. Does the cheaper route give a smaller cooperation threshold?

Fix an efficient proof system $S$ under the agenda's conventions (default $\mathsf{PA}_{\mathrm{bin}}$). For $p \in \mathrm{Lang}_1(S)$ (at most one free variable) and represented budgets $f, g$, the formula $\Box_{f(k)}\,p(k)$ asserts that the instance $p(\overline{k})$ (with $\overline{k}$ the binary numeral of $k$) has an $S$-proof of at most $f(k)$ symbols; $\lambda(k) := |\overline{k}|+1$ is the numeral-length budget; and $u \leq_S^{*} v$ means $S$ proves $u(k) \le v(k)$ beyond some standard threshold. Payor's handshake has a bounded agent, the analogue of $\mathrm{FairBot}_k$: in the program-game Prisoner's Dilemma, $\mathrm{PB}_k(\mathrm{Opp})$ searches all $S$-proofs of at most $k$ symbols for a proof of $\Box_k c \to c$, where $c$ is the sentence "$\mathrm{PB}_k(\mathrm{Opp}) = \mathsf{C}$ and $\mathrm{Opp}(\mathrm{PB}_k) = \mathsf{C}$" (both self-references by Kleene's recursion theorem); if found, it plays $\mathsf{C}$ (cooperate), otherwise $\mathsf{D}$ (defect). Where $\mathrm{FairBot}_k$ demands a proof of the opponent's cooperation, $\mathrm{PB}_k$ demands a proof that provable mutual cooperation implies mutual cooperation. Write $\hat{k}^{*}$ for the FairBot cooperation threshold ([MAIS-O16](MAIS-O16.md)).

**Problem ([MAIS-A1, Problem 5.4](../agendas/A1/MAIS-A1.tex#L485)).** Let $S$ satisfy the conventions above. Determine internal comparison conditions on represented budgets $f, g$ under which, for every $p \in \mathrm{Lang}_1(S)$,

$$S \vdash \forall k\,\Bigl(\Box_{g(k)}\bigl(\Box_{f(k)}\,p(k) \to p(k)\bigr) \to p(k)\Bigr) \quad\Longrightarrow\quad \exists\,\hat{k}:\ S \vdash \forall k > \hat{k}\;p(k),$$

with explicit $\hat{k}$. In particular, test whether the certificates $b\lambda \leq_S^{*} g$ and $f + b\lambda \leq_S^{*} g$ for every standard $b$ suffice. Then prove that two copies of $\mathrm{PB}_k$ cooperate above an explicit threshold $\hat{k}^{*}_{\mathrm{P}}$, and compare it with $\hat{k}^{*}$ in a common system and encoding.

The proof should use only bounded necessitation, quantifier distribution, and implication distribution; the four-line unbounded proof is the map. A short, self-contained note tabulating the comparison against the bounded Löb route — which hypothesis shapes, which budget windows, which thresholds — would be a complete first paper. For the unbounded lemma and the conventions, see [MAIS-A1](../agendas/A1/MAIS-A1.pdf).

*Related: [MAIS-O16](MAIS-O16.md) (the FairBot threshold to beat) · [MAIS-O15](MAIS-O15.md) (explicit thresholds on the Löb route) · [MAIS-O12](MAIS-O12.md) (the system constants Payor's proof avoids).*
