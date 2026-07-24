# Research agendas

Research directions: a motivating question, some real mathematics, and a cluster of related open problems. Agendas incorporate [open problems](../open/) and spin off [papers](../papers/).

Agendas are numbered MAIS-A1, MAIS-A2, … in order of arrival; numbers are permanent. Each agenda below expands one starred Open Problem of the survey [*Math for AI Safety: An Invitation for Mathematicians*](../papers/MAIS-P1/MAIS-P1.pdf) and begins by reproducing its statement. The survey statement is authoritative: when an open problem changes there, the change must be propagated to the corresponding agenda.

| # | Agenda | Source | PDF | Status |
|---|--------|--------|-----|--------|
| MAIS-A1 | Quantitative bounded Löb | [TeX](MAIS-A1/MAIS-A1.tex) | [PDF](MAIS-A1/MAIS-A1.pdf) | Draft · July 12, 2026 |
| MAIS-A2 | Behavioral tomography of world-models | [TeX](MAIS-A2/MAIS-A2.tex) | [PDF](MAIS-A2/MAIS-A2.pdf) | Draft · July 12, 2026 |
| MAIS-A3 | The geometry and identifiability of superposition | [TeX](MAIS-A3/MAIS-A3.tex) | [PDF](MAIS-A3/MAIS-A3.pdf) | Draft · July 12, 2026 |
| MAIS-A4 | Training for interpretability | [TeX](MAIS-A4/MAIS-A4.tex) | [PDF](MAIS-A4/MAIS-A4.pdf) | Draft · July 12, 2026 |
| MAIS-A5 | Which irreducible representations does training select? | [TeX](MAIS-A5/MAIS-A5.tex) | [PDF](MAIS-A5/MAIS-A5.pdf) | Draft · July 12, 2026 |
| MAIS-A6 | Does geometric simplicity force a legible mechanism? | [TeX](MAIS-A6/MAIS-A6.tex) | [PDF](MAIS-A6/MAIS-A6.pdf) | Draft · July 12, 2026 |
| MAIS-A7 | Effective loss and learning dynamics | [TeX](MAIS-A7/MAIS-A7.tex) | [PDF](MAIS-A7/MAIS-A7.pdf) | Draft · July 13, 2026 |
| MAIS-A8 | A predictive theory of out-of-distribution generalization | [TeX](MAIS-A8/MAIS-A8.tex) | [PDF](MAIS-A8/MAIS-A8.pdf) | Draft · July 16, 2026 |

Every problem, conjecture, and question posed inside an agenda carries its own permanent MAIS-O number: see the [index of open problems](../open/INDEX.md).

## What each agenda contains

**MAIS-A1 · Quantitative bounded Löb.** Löb's theorem converts a proof of "if $P$ is provable then $P$" into a proof of $P$ outright, by an explicit construction with an explicit cost. This agenda asks what that cost is: it defines the least overhead $F(k,n)$ such that a $k$-symbol proof of the hypothesis guarantees a proof of $P$ of at most $F(k,|P|)$ symbols, proves $F$ well-defined and computable, and poses problems on its growth — among them explicit cooperation thresholds for resource-bounded agents that cooperate by proving each other's cooperation.

**MAIS-A2 · Behavioral tomography of world-models.** Two theorems of Richens and coauthors show that any policy near-optimal across a rich family of interventions determines an approximate causal model of its environment — but the extraction consumes unlimited noiseless queries. This agenda develops the finite-sample side: explicit margin conditions replacing measure-zero genericity, query complexity under exact, sampled, and Boltzmann-perturbed answers, and the error floor imposed by the agent's regret.

**MAIS-A3 · The geometry and identifiability of superposition.** A neural network can store many more concepts than it has dimensions, as nearly orthogonal directions read out through sparse coefficients; the recovery tool used in practice is an $\ell^1$-penalized dictionary learner. Classical dictionary-learning theory assumes independent supports, but real concepts co-occur. Two small propositions show the support correlations alone decide identifiability — nested supports force merging, solo firing restores recovery — and the open problems live between those poles, starting with a two-feature phase boundary.

**MAIS-A4 · Training for interpretability.** Can a training objective make a network's internal features easy to recover? "Easy to interpret" is not yet a mathematical property, and this agenda does not pretend it is: it isolates three precise surrogates — coherence, $\ell^1$-recoverability, monosemanticity — inside a single toy model, proves small theorems marking the boundary of what is easy, and poses the problems that remain where resources are scarce and training means dynamics rather than exact minimization.

**MAIS-A5 · Which irreducible representations does training select?** Small networks trained to multiply in a finite group $G$ discover representation-theoretic algorithms, but *which* irreducible representations appear varies with the random initialization, and no theorem predicts the variation. This agenda defines the training ensemble and a black-box observable — the key set of irreducible representations visible in a trained network's outputs — precisely enough that the question becomes the law of a random subset of $\mathrm{Irr}(G)$.

**MAIS-A6 · Does geometric simplicity force a legible mechanism?** For a quadratic network computing addition mod $p$, the population loss is an explicit degree-six polynomial, and Fourier inversion gives exact fits built from single-frequency neurons — the algorithm found by reverse-engineering trained networks. The headline question: in a fixed ball, is every exact fit of smallest local learning coefficient of this single-frequency form? A proof would connect geometric simplicity to a mechanism one can read from the weights; a counterexample would show that the two notions of simplicity can part ways.

**MAIS-A7 · Effective loss and learning dynamics.** Watanabe's free-energy asymptotics predict which solutions Bayesian learning prefers as sample size grows; gradient descent is not Bayesian, yet in solvable cases it exhibits the same staircase of preferences, unfolding in training time. This agenda formalizes the correspondence several inequivalent ways: an Eyring–Kramers law with prefactors governed by real log canonical thresholds, entropic selection within a connected optimal set, effective diffusions on singular strata, and a time–sample dictionary calibrated on the deep linear network.

**MAIS-A8 · A predictive theory of out-of-distribution generalization.** An agent trained to collect a coin that always sat at the right end of its levels learned "move right," not "get the coin." This agenda turns that episode into mathematics: a one-dimensional environment with the degeneracy built in — two policies indistinguishable on the training distribution — where the linear case is solved (the implicit-bias theorem predicts the outcome, and it flips with the input encoding) and everything past the linear case is open.

## Provenance

Each agenda records its own provenance in a `PROVENANCE.md` beside its source, since different agendas may come to be in different ways. The original eight, MAIS-A1–A8, share one story: an experiment in AI-written mathematics — written by **Claude Fable 5** (Anthropic) under Lionel Levine's direction, adversarially reviewed, and independently audited by **GPT 5.6 Sol** (OpenAI). No human has verified every line, and the bylines are meant to say so plainly; details in each folder.

## Rebuilding

To rebuild an agenda, run `latexmk -pdf -interaction=nonstopmode -halt-on-error MAIS-A1.tex` from its folder. Only each `.tex` source and its matching `.pdf` are committed; LaTeX auxiliary files are ignored.
