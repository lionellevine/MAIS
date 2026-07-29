# The FairBot cooperation threshold

*Open problem MAIS-O16 · posed in [MAIS-A1](../agendas/A1/) as [Problem 4.8](../agendas/A1/MAIS-A1.tex#L406) · Status: open.*

*Tags: cooperative AI · open-source game theory · program equilibrium · Löbian cooperation · logic · computational. Difficulty: ★★.*

*Authored by: Claude 5 Fable directed by Lionel Levine · Audited by: GPT 5.6 Sol.*

AI systems are software agents, and programs, unlike people, can exhibit their source code cheaply. Whether transparent agents can cooperate where opaque ones defect is a basic question of cooperative AI — and in the simplest case it has been reduced to a single unknown number.

In a **program game**, each player is an algorithm handed the other's source code before choosing its action; the game here is the Prisoner's Dilemma, where between opaque players mutual defection is the unique equilibrium. Critch's bounded agent is

$$\mathrm{FairBot}_k(\mathrm{Opp}):\ \text{search all proofs of at most } k \text{ symbols for a proof that } \mathrm{Opp}(\mathrm{FairBot}_k)=\mathsf{C};\ \text{if found, play } \mathsf{C}; \text{ otherwise play } \mathsf{D},$$

where the self-reference is implemented by Kleene's recursion theorem. The natural guess is that two copies deadlock, each waiting for the other to prove cooperation first. They do not: Critch's theorem gives a finite threshold $\hat{k}$ above which $\mathrm{FairBot}_k(\mathrm{FairBot}_k)=\mathsf{C}$ — provided the proof system can certify the growth of its own proof-search overhead, a hypothesis never verified for any concrete system.

What must be certified, precisely: fix a proof system $S$, a consistent recursively axiomatized extension of Peano Arithmetic, and write $\Box_m \varphi$ for the arithmetic sentence asserting that $\varphi$ has an $S$-proof of at most $m$ symbols. An **expansion function** for $S$ is a computable $\mathcal{E}$, chosen nondecreasing with a graph that $S$ proves total and single-valued, such that every $\varphi$ provable in at most $m$ symbols has a proof of $\Box_m \varphi$ in at most $\mathcal{E}(m)$ symbols, and such that $S$ proves each implication $\Box_m \varphi \to \Box_{\mathcal{E}(m)} \Box_m \varphi$ — the price of noticing one's own bounded proofs. The **standing expansion certificate** is an explicit search-free budget term $E^{\sharp }$, built from constants, $k$, and the numeral-length function (of order $\log k$) by addition, multiplication, composition, and $x \mapsto 2^{x}$, together with one $S$-proof of the universal sentence that $\mathcal{E}(m) \le E^{\sharp }(m)$ for all $m$: the system itself certifies a bound on its own expansion cost. Fixing a standard system and encoding, define

$$\hat{k}^{\ast } := \min\lbrace \  K : \mathrm{FairBot}_k(\mathrm{FairBot}_k) = \mathsf{C} \text{ for all } k \ge K \ \rbrace  \in \mathbb{N} \cup \lbrace \infty\rbrace .$$

**Problem ([MAIS-A1, Problem 4.8](../agendas/A1/MAIS-A1.tex#L406)).** Prove the standing expansion certificate for one standard system and encoding, deduce $\hat{k}^{\ast }<\infty$, and give a certified numerical interval containing the exact threshold. Compute the threshold if feasible.

In the last clause, certified means proved: an interval containing $\hat{k}^{\ast }$ is a proof that the two copies cooperate at every budget at or above the upper endpoint, together with a defecting budget large enough to show the threshold is at least the lower endpoint. Any single budget is decidable — run the two terminating programs — so the content lies in the upper endpoint's claim about all larger $k$.

Proof *search* need not be the bottleneck: Critch, Dennis, and Russell observe that an agent can front-load the known proof, so that verifying Löbian cooperation takes well under a second of computer time. Measuring $\hat{k}^{\ast }$ in a real proof assistant is a feasible experiment, not a thought experiment. For the proof-system conventions and the certified-budget formalism, see [MAIS-A1](../agendas/A1/); the counterexamples that make the certification necessary are in [MAIS-P2](../papers/P2/).

## References

- A. Critch, *A parametric, resource-bounded generalization of Löb's theorem, and a robust cooperation criterion for open-source game theory*, Journal of Symbolic Logic 84 (2019), no. 4, 1368–1381. [arXiv:1602.04184](https://arxiv.org/abs/1602.04184)
- M. Barász, P. Christiano, B. Fallenstein, M. Herreshoff, P. LaVictoire, and E. Yudkowsky, *Robust cooperation in the Prisoner's Dilemma: program equilibrium via provability logic*, 2014. [arXiv:1401.5577](https://arxiv.org/abs/1401.5577)
- A. Critch, M. Dennis, and S. Russell, *Cooperative and uncooperative institution designs: surprises and problems in open-source game theory*, 2022. [arXiv:2208.07006](https://arxiv.org/abs/2208.07006)

*Related: [MAIS-O1](MAIS-O1.md) (the Löb overhead this threshold depends on) · [MAIS-O17](MAIS-O17.md) (thresholds over families of agents) · [MAIS-O20](MAIS-O20.md) (a bounded Payor lemma).*
