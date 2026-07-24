# Steering Conway's Life from a small seed

*Open problem MAIS-O1 · Lionel Levine · July 2026 · Status: open, as far as a literature check shows.*

Can a small controller reliably steer a vast system to a desired global state, despite noise it cannot remove and rival processes it did not design? This is an abstraction of a core difficulty of AI alignment: goal-directed control of a complex world from limited leverage, with the difficulty concentrated where it is in practice — robustness and competition. Conway's Game of Life offers the simplest medium I know in which to pose the question precisely, and there it becomes a concrete problem in probability and theoretical computer science.

The problem originated on LessWrong. Alex Flint's [*Agency in Conway's Game of Life*](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life) (2021) posed the **control question**: on a $10^{30}\times 10^{30}$ Life board, initialized at random except for a $10^{20}\times 10^{20}$ corner that you control, can you choose the corner so that after $10^{60}$ steps the whole board resembles a giant smiley face? Flint proposed the **AI hypothesis**: any pattern that solves the control question does so, essentially, by being an AI.

In [a comment](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=iDt4ddqhysLZcrzLo) I argued the opposite: no intelligence is needed, only an **infectious Turing machine** — a device that gradually converts its random environment into squares of its own tape, kept error-free by simple repair bots. I was not the only doubter: several commenters sketched unintelligent strategies, and [itaibn0](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=bqjCwbb7xEXW7FZuL) distinguished the *outer* intelligence needed to design a seed from the *inner* intelligence the seed itself exhibits; only the latter is at stake in the AI hypothesis. The finite numbers matter: they make the question one of overwhelming reliability in a single enormous experiment.

## The question

On a $10^{30}\times 10^{30}$ board of Conway's Game of Life, initialize every cell i.i.d. random **except** a $10^{20}\times 10^{20}$ upper-left corner that we control. Can we choose the corner's initial state (the *seed*) so that, with probability at least $1-10^{-100}$ over the random remainder, the board resembles a giant smiley face after $10^{60}$ generations?

The numerical reliability threshold is illustrative; Flint suggests $99\%$, while $1-10^{-100}$ is a deliberately stringent version. What matters is a fixed high reliability, not infallibility or an asymptotic limit. Probability $1$ is too much to ask because every particular remainder has positive probability, and some remainders are fatal. [Richard Kennaway observed](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=sud4pRgL3yEExz6Fo) that if the far corner happens to hold a $180^\circ$-rotated copy of the seed, with the rest of the board arranged symmetrically, then the evolution stays symmetric forever and no asymmetric smiley can appear; a rival machine with an incompatible target is just as possible. The asymptotic limit is a subtler trap: at sufficiently fantastic board sizes, the random remainder breeds machines that compete with ours ("Emergent adversaries" below).

## A precise finite statement

- Board side $N_0=10^{30}$, seed side $M_0=10^{20}$, and observation time $T_0=10^{60}=N_0^2$.
- Board $\Lambda=(\mathbb Z/N_0\mathbb Z)^2$ (torus; or an $N_0\times N_0$ grid with dead boundary — note which, since a dead boundary hands the controller free "walls").
- Seed region $S$: an $M_0\times M_0$ upper-left corner; the controller picks $\sigma\in\{0,1\}^S$ without seeing the remainder.
- Remainder $\xi\in\{0,1\}^{\Lambda\setminus S}$: i.i.d. $\mathrm{Bernoulli}(\tfrac12)$.
- Dynamics: synchronous Life, $\omega_t=\mathrm{Life}^t(\omega)$.
- Target $\mathcal T$: a **macroscopic** predicate rather than exact cell equality. For example, partition the board into a large but fixed grid of macropixels, label them by a low-complexity smiley-face bitmap, and require all but a small fraction to lie on the correct side of two separated density thresholds.

**Question (overwhelmingly reliable control).** Does there exist a seed $\sigma$ such that

$$
\Pr_\xi\!\left[\mathrm{Life}^{T_0}(\sigma\cup\xi)\models\mathcal T\right]
\ge 1-10^{-100}\,?
$$

The exponent $2$ in $T_0=N_0^2$ is not a known threshold. Locality gives an order-$N_0$ lower bound for affecting the far side of the board, and the observed relaxation of random Life does not supply a diffusive $N_0^2$ scale. A massively parallel expanding front might finish in nearly linear time, while a constructor that writes cells one at a time might need order $N_0^2$; best to regard $N_0^2$ as Flint's generous fixed horizon. Flint asks what the board looks like **at** time $T_0$, so a fast solution must hold its work, or delay the unveiling, until then. The easier variant asks only for some $t\le T_0$ at which the target appears; a stronger one asks that it then persist for a long interval.

Other knobs that change the problem are the coarse-graining and permitted Hamming error in the target, the random density $p$, and torus versus dead boundary. A deeper knob is the rule itself: [Paul Christiano pointed out](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=CTDf7a3eQmvo6g5Nf) that in a reversible automaton — Margolus's Critters, say — the task is impossible on average, and one can only hope to succeed against a sparse background; success in Life leans on the rule's willingness to destroy information. The reversible variant is a different problem worth posing.

## Is it open?

**Solved: the empty-background version.** Life is Turing-complete and supports **universal construction** (Berlekamp–Conway–Guy, *Winning Ways*, 1982; self-replicating machines were realized by Wade's Gemini in 2010, Greene's tape-copying replicator in 2013, and Goucher's 0E0P metacell in 2018). On an all-dead background, a seed can compute anything and construct any pattern — tile the board, draw the smiley. This is engineering, not open. (The worst-case background, by contrast, is provably impossible — Kennaway's symmetry above — which is why the problem lives on the random background in between.)

**Open: the random-background, overwhelmingly reliable version.** The hard ingredients are each at or beyond the research frontier:

- *Life on random initial conditions is rigorously intractable today.* Even the limiting density is only heuristic: mean-field predicts $\rho^{\ast}\approx 0.37\approx 1/e$, but 2-D simulation settles into "ash" at density about $0.03$; the gap (spatial correlations) is not rigorously understood. Numerical work finds a transient correlation length growing like $t^{1/z'}$ with $z'\approx1.5$ (and a related relaxation exponent $z\approx1.66$), saturating at about $50$ cells rather than diffusing across the board. No theorem gives a limiting measure, density convergence, or ergodicity for Life started from $\mathrm{Bernoulli}(p)$. (See arXiv:1407.1006 and arXiv:1809.03266.)
- *Fault-tolerant computation in a noisy cellular automaton exists — but only by designing the rule.* Gács ("Reliable Cellular Automata with Self-Organization," *J. Stat. Phys.* 103, 2001, 45–267) builds a 1-D CA that reliably computes under positive-rate i.i.d. noise, via an infinite hierarchy of self-simulating, self-repairing blocks (refuting the positive-rates conjecture); Toom's 2-D "eroder" is a simpler two-dimensional fault-tolerance mechanism. Neither transfers: here the rule is *fixed* (Life) and the randomness is in the *initial condition* (static), not per-step. Achieving Gács-style robustness *inside Life*, with no freedom to redesign the rule, is plausibly the crux.
- *Cellular-automaton control and reachability are studied in the wrong regime.* Configuration reachability is undecidable in the infinite 1-D setting and NP- or PSPACE-hard in finite settings; "regional" and "boundary" controllability results exist (SAT formulations; linear and additive rules) but are deterministic, worst-case, and small-scale — not "fixed rule, enormous random background, overwhelming reliability." (arXiv:1901.08246; arXiv:2504.03691; arXiv:1606.05122.) The closest formal notion, [pointed out by Vanessa Kosoy](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=DHjNQ3yQfM5fu6q8g), is Schaeffer's *physical universality*: a cellular automaton in which the exterior of any finite region can implement any prescribed transformation of it. But Schaeffer designed his rule for the purpose; whether Life is physically universal is open.

**In progress: clearing ash, empirically.** Flint's post prompted engineering work by the Life community on the first milestone below. Naive approaches fail instructively: [Oscar Cunningham found](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=xm6cgwkaP3CQ4fgxE) that gliders fired into settled ash create more ash than they destroy, growing a stalagmite of ash back toward the source. Newer construction technology fares better — see the [Clearing Ash](https://conwaylife.com/forums/viewtopic.php?t=5364) forum thread and the [space-cleaning experiments of October 2021](https://conwaylife.com/forums/viewtopic.php?p=136948#p136948) — and [Dave Greene's assessment](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=MafPgirkzwcknxTBw) is that a workable space-cleaning mechanism looks plausible, perhaps enabling "a 99+% success rate for a Very Very Slow Huge-Smiley-Face Constructor." None of this is rigorous, and $99\%$ is a long way from $1-10^{-100}$, but it is the state of the art.

So the problem as posed appears genuinely open: the empty-background version is solved, the random version has attracted empirical probes but no rigorous results, and even its prerequisite — a rigorous theory of Life on random initial conditions — does not exist. (One cannot prove nobody has posed it; a targeted search found nothing matching.)

## Why it's hard

- **Competing growth.** Light-speed limits force the seed's organized region to spend at least order $N_0$ generations growing across the board, while the random soup, evolving on its own, bombards the advancing front with gliders and debris. You want the controlled phase to percolate and dominate with overwhelming probability — a first-passage-percolation, two-type-competition flavor, and a natural entry point for a probabilist.
- **Robustness inside a fixed, fragile rule.** Life patterns die to single bit-flips; surviving in — let alone computing in — a chaotic random environment likely requires an in-Life analogue of Gács's hierarchical self-repair. Whether Life's rule admits one is open.
- **Emergent adversaries at still larger scales.** On a board of side $N$, a particular local window specifying $k$ independent bits has about $N^2$ possible placements, hence expected count about $N^2 2^{-k}$ ([a back-of-envelope](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=CGtHTuX3dHNxgYi7c) run in the post's comments). On Flint's board $N_0^2=10^{60}\approx 2^{199}$, so windows of roughly two hundred specified bits are typical; that is nowhere near a protected universal constructor, much less an accidental copy of our $10^{40}$-bit seed. But if $N$ is allowed to tend to infinity while the machine size stays fixed, every fixed finite construction that can survive the surrounding soup eventually appears many times. Some may be rival constructors — Boltzmann brains with incompatible goals — and a dumb infectious Turing machine is not automatically equipped to beat them.

## Milestones, in increasing difficulty

1. **Clear and hold:** at Flint's parameters, seed a machine that erases the soup from a macroscopic window and holds it dead for a long interval with the stated reliability. (Even this is nontrivial — eaters against incoming glider streams.)
2. **Simple target:** fill a macroscopic region with a chosen simple phase (all dead; all blinkers) with the stated reliability.
3. **Arbitrary macroscopic bitmap:** draw the smiley at time $T_0$ with the stated reliability.
4. **Scaling law:** characterize the regimes of board size, controller size, random density, and reliability in which each of the above remains possible.

## Conjecture

At Flint's fixed parameters, yes: an infectious Turing machine can overwrite the board and write the target with failure probability at most $10^{-100}$. The open crux is making the construction robust to random soup. If the conjecture holds, the control question is solved by something lifelike but hardly intelligent, which puts pressure on the AI hypothesis. The opposite intuition also has defenders: [JBlack expects](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=2wsXasPuzh7wwYijW) that no seed at all is robust against a random environment.

Here is a more ambitious asymptotic afterthought. Fix a coarse-grained smiley target $\mathcal T_N$ and a choice of boundary condition, and let $\xi$ be i.i.d. $\mathrm{Bernoulli}(\tfrac12)$ off the seed. I conjecture that for every $0<\varepsilon<1$, $0<\delta<2\varepsilon$, and $\eta>0$, for all sufficiently large $N$ there is a seed $\sigma_N$ (depending also on $\varepsilon,\delta,\eta$) in an $\lfloor N^\varepsilon\rfloor\times\lfloor N^\varepsilon\rfloor$ corner such that

$$
\Pr\!\left[
\mathrm{Life}^{\lceil N^{1+\eta}\rceil}
(\sigma_N\cup\xi)
\models\mathcal T_N
\right]
\ge 1-\exp\!\left(-N^{2\varepsilon-\delta}\right).
$$

The time budget, $N^{1+\eta}$ for every fixed $\eta>0$, is nearly linear — a sharper guess than the generous $N_0^2$ above, with room only for a small polynomial overhead from propagation and repair. The failure exponent is just below the number $N^{2\varepsilon}$ of controlled bits, allowing the machine and its redundancy to grow with the world. This scaling suppresses an accidental copy of a comparably large, fully specified seed: even after a union bound over $N^2$ possible locations, its probability is $\exp(-\Theta(N^{2\varepsilon}))$.

What the scaling does **not** dispose of is smaller self-protecting rivals. If a fixed robust constructor can arise in random soup, then at sufficiently large $N$ it appears at positive density, and the corner seed must defeat a whole population of them. That is why this asymptotic statement is substantially stronger than Flint's finite question, and may require a new idea beyond the infectious Turing machine.

## Key references

- Alex Flint, ["Agency in Conway's Game of Life,"](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life) LessWrong (2021) — the control question and the AI hypothesis; see also [the comment](https://www.lesswrong.com/posts/3SG4WbNPoP8fsuZgs/agency-in-conway-s-game-of-life?commentId=iDt4ddqhysLZcrzLo) proposing the infectious Turing machine.
- Berlekamp, Conway, Guy, *Winning Ways for Your Mathematical Plays* (1982) — Life universality and construction.
- Gács, "Reliable Cellular Automata with Self-Organization," *J. Stat. Phys.* 103 (2001) 45–267.
- Toom, "Stable and Attractive Trajectories in Multicomponent Systems" (1980) — the eroder / NEC rule.
- Luke Schaeffer, "A Physically Universal Cellular Automaton," ITCS 2015 (see [Scott Aaronson's exposition](https://www.scottaaronson.com/blog/?p=1896)) — external control of arbitrary finite regions, in a rule built for it.
- Life community work on clearing random ash: the [Clearing Ash](https://conwaylife.com/forums/viewtopic.php?t=5364) forum thread; [space-cleaning experiments, Oct 2021](https://conwaylife.com/forums/viewtopic.php?p=136948#p136948).
- Cellular-automaton reachability and control: arXiv:1901.08246; arXiv:2504.03691; arXiv:1606.05122.
- Life on random initial conditions (heuristic): arXiv:1407.1006; Cornu and Hilhorst, "Density decay and growth of correlations in the Game of Life," arXiv:1809.03266.
- Self-replication in Life: Wade's Gemini (2010); Greene's replicator (2013); Goucher's 0E0P metacell (2018).
