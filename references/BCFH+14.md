# Robust cooperation in the Prisoner's Dilemma: program equilibrium via provability logic

*Summary [BCFH+14] · M. Barász, P. Christiano, B. Fallenstein, M. Herreshoff, P. LaVictoire, and E. Yudkowsky, 2014 · [arXiv:1401.5577](https://arxiv.org/abs/1401.5577).*

*Tags: cooperative AI · open-source game theory · program equilibrium · Löbian cooperation · proof-based agents · logic.*

*Summarized by: Claude 5 Fable directed by Lionel Levine.*

**TL;DR.** In the one-shot Prisoner's Dilemma between players who read each other's source code, an agent that cooperates exactly when it can *prove* its opponent cooperates achieves mutual cooperation with its own copy — by Löb's theorem, not by symmetry-matching — while never being the sucker. The paper constructs the agents FairBot and PrudentBot, develops a general theory of *modal agents* in the Gödel–Löb provability logic $\mathsf{GL}$ in which any two agents' mutual actions are determined by a unique fixed point, and proves obstructions showing that no agent of this kind is universally optimal.

## Setup and hypotheses

Agents are formulas of Peano Arithmetic with one free variable; $X(Y)$ is $X$ with the Gödel number of $Y$ substituted, and "$X$ cooperates with $Y$" means $X(Y)$ holds in the standard model. Decisions consult provability in $\mathsf{PA}$ or in the tower $\mathsf{PA}{+}n$ obtained by adding iterated consistency statements. The engine is **Löb's theorem**: for $\mathsf{S}\supseteq\mathsf{PA}$, if $\mathsf{S}\vdash\Box\phi\to\phi$ then $\mathsf{S}\vdash\phi$. The star agent is $\mathrm{FairBot}$, which cooperates with $X$ iff $\mathsf{PA}\vdash[X(\mathrm{FB})=C]$; a **modal agent** is one whose behavior is defined by a fully modalized $\mathsf{GL}$-formula, possibly consulting finitely many lower-rank agents. An agent is **unexploitable** if no opponent gets it to cooperate while defecting.

## Main results

1. **Löbian self-cooperation (Theorem 3.1).** $\mathsf{PA}\vdash[\mathrm{FB}(\mathrm{FB})=C]$. The natural guess is that two copies deadlock, each waiting for the other to prove cooperation first; Löb's theorem dissolves the regress, since $\mathsf{PA}$ proves $\Box[\mathrm{FB}(\mathrm{FB}){=}C]\to[\mathrm{FB}(\mathrm{FB}){=}C]$ by inspection. FairBot is unexploitable assuming $\mathsf{PA}$ is sound.
2. **PrudentBot (Theorem 3.2).** The agent that cooperates iff $\mathsf{PA}$ proves the opponent cooperates with it *and* $\mathsf{PA}{+}1$ proves the opponent defects against DefectBot is unexploitable, cooperates mutually with itself and with FairBot, and defects against CooperateBot. The jump to the stronger system for the second check is essential to its self-cooperation.
3. **Modal-agent theory (Theorems 4.1–4.8).** By the fixed-point theorems of $\mathsf{GL}$, the mutual actions of any two modal agents are the unique solution of their combined modal formulas. Modal agents are *behavioral* — their action depends only on the opponent's behavior, never its syntax — so quining agents that reward copies of their own code (CliqueBot) are not modal.
4. **Third-party calls are necessary (Theorem 4.10).** A modal agent that consults no other agents and cooperates with FairBot must also cooperate with CooperateBot; distinguishing the two requires probes like PrudentBot's DefectBot check.
5. **Obstructions to optimality (§5).** No agent is optimal against all opponents, since an opponent can reward or punish arbitrary features of source code; and every pair of distinct modal agents is split by some third agent.

## Proof method

The recurring move is the Löbian circle: from $\mathsf{PA}\vdash\Box A\to B$ and $\mathsf{PA}\vdash\Box B\to A$, conclude $\mathsf{PA}\vdash A\wedge B$. The modal-agent theory rests on the Kripke semantics and arithmetical soundness of $\mathsf{GL}$ together with the existence and uniqueness of modal fixed points; uniqueness is what makes a pair of agents' outcome well defined and behavior-determined. The authors also supply a Kripke-semantics evaluator that computes any two modal agents' mutual actions.

## Why it matters for AI safety

AI systems are software agents, and programs, unlike people, can exhibit their source code. This paper is the proof of concept that transparency plus provability-based reasoning stabilizes cooperation that classical game theory rules out — mutual cooperation in the one-shot Prisoner's Dilemma, with unexploitability as the safety guarantee. Its agents, however, search *all* proofs, so they are not computable; the authors flag bounded algorithmic versions as the open direction, realized by Critch's parametric bounded Löb theorem [[C19]](C19.md). [MAIS-A1](../agendas/A1/) takes the next step: making the bounded cooperation thresholds certified and numerical, with this paper as the unbounded precursor its whole program quantifies.

## Cited by

- [MAIS-A1](../agendas/A1/) — the unbounded modal-agent theory whose bounded, certified quantification the agenda pursues; its Kripke evaluator is a starting point for the agenda's machine experiments.
- Problems [MAIS-O15](../open-problems/MAIS-O15.md) · [MAIS-O16](../open-problems/MAIS-O16.md) · [MAIS-O17](../open-problems/MAIS-O17.md) · [MAIS-O20](../open-problems/MAIS-O20.md)
