# Admissible budgets for a bounded Löb axiom

*Open problem MAIS-O18 · posed in [MAIS-A1](../agendas/A1/) as [Problem 5.1](../agendas/A1/MAIS-A1.tex#L447) · Status: open.*

*Tags: cooperative AI · agent foundations · Löbian cooperation · proof-based agents · bounded rationality · logic. Difficulty: ★★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

Löb's theorem has two strengths. The *rule* — from $\vdash \Box P \to P$ infer $\vdash P$ — is what the parametric bounded theorem quantifies. The *axiom* is its internalization, $\Box(\Box P \to P) \to \Box P$, one box deeper; it is what a bounded provability logic would need as its Löb axiom. Which proof budgets make the bounded axiom hold?

Fix an efficient proof system $S$ (default $\mathsf{PA}_{\mathrm{bin}}$). For $p \in \mathrm{Lang}_1(S)$ (at most one free variable) and a represented budget $a$, the formula $\Box_{a(k)}\ p(k)$ asserts that the instance $p(\overline{k})$ (with $\overline{k}$ the binary numeral of $k$) has an $S$-proof of at most $a(k)$ symbols. $\mathcal{B}$-terms are the agenda's search-free budget terms with canonical graphs; $\lambda(k) := |\overline{k}|+1$ is the numeral-length budget; and $u \leq_S^{\ast } v$ means $S$ proves $u(k) \le v(k)$ for all $k$ beyond some standard threshold. The lower bound on $b$ in the statement removes a cheap obstruction: with $p = \bot$ and $a = c = 0$, taking $b$ the length of a fixed proof of $\Box_0 \bot \to \bot$ makes the antecedent provable and the consequent refutable.

**Problem ([MAIS-A1, Problem 5.1](../agendas/A1/MAIS-A1.tex#L447)).** Fix an efficient $S$. Determine for which triples of $\mathcal{B}$-terms $(a, b, c)$, and more generally which triples of internally certified represented budgets, it holds that for every $p \in \mathrm{Lang}_1(S)$ there is $\hat{k}$ with

$$S \vdash \forall k > \hat{k}\ \Bigl(\Box_{b(k)}\bigl(\Box_{a(k)}\ p(k) \to p(k)\bigr) \ \to\  \Box_{c(k)}\ p(k)\Bigr).$$

Restrict first to $\mathcal{B}$-terms satisfying $\lambda \leq_S^{\ast } b$, so the outer box is not a fixed finite search. Prove that some triple of polynomials works for $\mathsf{PA}_{\mathrm{bin}}$, and for given $(a, b)$ characterize the admissible $c$. (The admissible $c$ need not have a least element pointwise; for polynomial $c$, determine the least admissible degree.)

In words: whenever the reflection instance at budget $a$ has a proof within budget $b$, the sentence itself must have a proof within budget $c$, and $S$ proves this uniformly for all large $k$. This is the statement the parametric bounded Löb theorem would become if its implication moved inside the box, and the heuristic reduction of bounded Gödel–Löb soundness makes it the case that carries the real content. For the conventions and that reduction, see [MAIS-A1](../agendas/A1/).

*Related: [MAIS-O19](MAIS-O19.md) (bounded GL soundness, whose Löb-axiom case this is) · [MAIS-O15](MAIS-O15.md) (the rule-form counterpart with explicit thresholds) · [MAIS-O13](MAIS-O13.md) (the budget comparisons the certificates need).*
