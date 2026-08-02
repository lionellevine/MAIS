# Cooperative and uncooperative institution designs: surprises and problems in open-source game theory

*Summary [CDR22] · A. Critch, M. Dennis, and S. Russell, 2022 · [arXiv:2208.07006](https://arxiv.org/abs/2208.07006).*

*Tags: cooperative AI · open-source game theory · program equilibrium · proof-based agents · bounded rationality · institution design · logic.*

*Summarized by: GPT 5.6 Sol directed by Lionel Levine.*

**TL;DR.** Programs that can inspect one another need not behave like opaque players. In a one-shot Prisoner's Dilemma, a bounded agent that cooperates only after proving its opponent will cooperate can be unexploitable and still cooperate with a copy of itself; reversing the default action can instead make two apparently cooperative agents defect. The paper derives several such large-budget outcomes from Critch's parametric bounded Löb theorem, extends one result to randomized agents, and poses ten open problems. Its analogies with human institutions are proposals for modelling, not consequences of the program theorems.

## Setting

An **open-source game** gives each player the other player's source code before either acts. The players here are **formal verifier agents**: they enumerate candidate proofs, up to a character budget $k$, about what their opponent will do. The proof checker is assumed sound and able to reason about arbitrary computable programs.

Four agent families drive the examples:

- $\mathrm{CUPOD}(k)$, “cooperate unless proof of defection,” defects only if it finds a proof that its opponent defects.
- $\mathrm{DUPOC}(k)$, “defect unless proof of cooperation,” cooperates only if it finds a proof that its opponent cooperates.
- $\mathrm{CIMCIC}(k)$ cooperates if it proves that its own cooperation would imply the opponent's cooperation.
- $\mathrm{DIMCID}(k)$ defects if it proves that its own cooperation would imply the opponent's defection.

The large-$k$ arguments invoke a parametric bounded Löb principle: roughly, if the proof system verifies that a short proof of $p(k)$ would make $p(k)$ true, then $p(k)$ holds for all sufficiently large $k$.

## Main results

1. **The default action does not predict self-play.** For all sufficiently large $k$, two CUPODs defect against each other, while two DUPOCs cooperate (Theorems 3.4 and 3.7). In both cases a bounded Löbian argument resolves the apparent regress in which each agent reasons about the other's reasoning.
2. **One-sided safety properties.** Assuming the proof checker is sound, CUPOD never exploits an opponent: it never defects while the opponent cooperates. Dually, DUPOC is never exploited: it never cooperates while the opponent defects (Propositions 3.1 and 3.2).
3. **Randomized self-cooperation.** A probabilistic DUPOC that cooperates with probability $q$ after proving that its opponent cooperates with probability at least $q$ achieves mutual cooperation with probability at least $2q-1$ for large $k$, or at least $q^2$ when the two random sources are independent (Theorem 4.1).
4. **Conditional strategies can reinforce either outcome.** For large $k$, CIMCIC cooperates with itself and with DUPOC (Theorem 5.2). DIMCID defects against itself and against CUPOD (Theorem 5.5).
5. **Proof enumeration need not determine runtime.** The theorems do not depend on checking candidate strings in lexicographic order. A verifier can try a known cooperation proof first, avoiding exhaustive search when that proof succeeds. The paper proposes this optimization but does not implement or benchmark it.

The paper leaves ten open problems, including the outcomes of DUPOC–CUPOD, CUPOD–CIMCIC, and DUPOC–DIMCID; a bounded theory of general modal agents; bounded PrudentBot; population dynamics; and an implementation in HOL/ML or Coq.

## Method and qualification

Each large-budget result chooses an outcome statement $p(k)$, shows that a sufficiently short proof of $p(k)$ would trigger the agents to realize that outcome, and applies the parametric bounded Löb theorem. This is a proof about the source code rather than a simulation of the agents.

As written, these results inherit a missing hypothesis from the bounded Löb theorem they cite [[C19]](C19.md). [MAIS-P2](../papers/P2/) shows that external growth of a represented budget does not ensure that the proof system can prove the budget comparisons used inside the Löbian argument. The displayed agents use simple budgets such as $k$, so their intended conclusions are natural targets for repair, but a complete theorem must fix a concrete proof calculus and representation and prove the required comparisons internally. A formalization that assumes the bounded Löb step as an axiom does not perform this check.

## Why it matters for AI safety

Future AI systems may be able to expose verifiable code, policies, or proof-carrying commitments to one another. The paper shows that such transparency can support one-shot cooperation without making an agent exploitable, but can also stabilize mutual defection through the same self-referential mechanism. The safety question is therefore not simply whether agents are transparent. It is which decision rules transparency makes mutually reinforcing, and whether humans can verify the assumptions behind those rules. The paper's extension from programs to human institutions is a motivating analogy; no theorem establishes that real institutions satisfy the required formal-verification model.

## Cited by

- [MAIS-A1](../agendas/A1/) — uses its proof-order observation as motivation for a concrete bounded-agent implementation and asks that the required resource comparisons be certified.
- Problems [MAIS-O16](../open-problems/MAIS-O16.md) · [MAIS-D1](../open-problems/MAIS-D1.md)
