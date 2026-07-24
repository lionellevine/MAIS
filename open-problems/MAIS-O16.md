# The FairBot cooperation threshold

*Open problem MAIS-O16 · posed in [MAIS-A1](../agendas/A1/MAIS-A1.pdf) as [Problem 4.8](../agendas/A1/MAIS-A1.tex#L405) · Status: open.*

*Safety: cooperative AI — open-source game theory · program equilibrium · Löbian cooperation. Mathematics: logic · computational. Difficulty: ★★ project.*

AI systems are software agents, and programs, unlike people, can exhibit their source code cheaply. Whether transparent agents can cooperate where opaque ones defect is a basic question of cooperative AI — and in the simplest case it has been reduced to a single unknown number.

In a **program game**, each player is an algorithm handed the other's source code before choosing its action; the game here is the Prisoner's Dilemma, where between opaque players mutual defection is the unique equilibrium. Critch's bounded agent is

$$\mathrm{FairBot}_k(\mathrm{Opp}):\ \text{search all proofs of at most } k \text{ symbols for a proof that } \mathrm{Opp}(\mathrm{FairBot}_k)=\mathsf{C};\ \text{if found, play } \mathsf{C}; \text{ otherwise play } \mathsf{D},$$

where the self-reference is implemented by Kleene's recursion theorem. The natural guess is that two copies deadlock, each waiting for the other to prove cooperation first. They do not: Critch's theorem gives a finite threshold $\hat{k}$ above which $\mathrm{FairBot}_k(\mathrm{FairBot}_k)=\mathsf{C}$ — provided the proof system can certify the growth of its own proof-search overhead, a hypothesis never verified for any concrete system. Fixing a standard system and encoding, define

$$\hat{k}^{*} := \min\{\, K : \mathrm{FairBot}_k(\mathrm{FairBot}_k) = \mathsf{C} \text{ for all } k \ge K \,\} \in \mathbb{N} \cup \{\infty\}.$$

**Problem ([MAIS-A1, Problem 4.8](../agendas/A1/MAIS-A1.tex#L405)).** Prove the standing expansion certificate for one standard system and encoding, deduce $\hat{k}^{*}<\infty$, and give a certified numerical interval containing the exact threshold. Compute the threshold if feasible.

Proof *search* need not be the bottleneck: an agent can front-load the known proof, so that verifying Löbian cooperation takes well under a second of computer time. Measuring $\hat{k}^{*}$ in a real proof assistant is a feasible experiment, not a thought experiment. For the proof-system conventions and the certified-budget formalism, see [MAIS-A1](../agendas/A1/MAIS-A1.pdf).

*Related: [MAIS-O1](MAIS-O1.md) (the Löb overhead this threshold depends on) · [MAIS-O17](MAIS-O17.md) (thresholds over families of agents) · [MAIS-O20](MAIS-O20.md) (a bounded Payor lemma).*
