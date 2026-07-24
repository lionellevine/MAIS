# How I write mathematics

*Style guide · Lionel Levine · July 2026 · Status: living document.*

The documents in this repo aim to follow these guidelines, and contributions (see `CONTRIBUTING.md`) should too. The guide is written to be handed to a language model: if you use LLMs in your writing process, provide them with this file so that they write in the house style. They are distilled from my own papers and edits, and from Halmos, Knuth, Tao, Thurston, and Zagier; each guideline (and each example) was individually approved, and several were edited, by me. When guidelines collide, the reader wins. ✗ marks what not to write, ✓ what to write instead; ✓ examples are from my own writing unless noted.

## What to write

1. **Have something to say.** One piece, one subject; a section with no point gets cut, not polished.
2. **Write for one reader**: a friendly colleague, curious but slightly skeptical, smart but not in this field. Keep them in view in every sentence.
   - For `open/` in this repo, the one reader is an ILIAD attendee: mathematically fluent and alignment-literate. Skip the safety catechism; spell out the mathematics.
3. **Open with a question or an image**: sections open with a conceptual question or evocative image, one paragraph of context, then the precise setup. Avoid "In this paper we prove X" — let the result emerge from the motivation.
4. **Examples are the heart.** Build each section around a crucial example or counterexample; big general theories are afterthoughts based on small but profound insights.
5. **Show the phenomenon before the theorem**: raw data, a table, a picture. Zoom out until the regularity is unmistakable, and let the reader conjecture before you state.
   - ✗ "We now define the crossout strategy and prove it is optimal." ✓ [Ethiopian Dinner] The dinner $D=\{(1,2),(2,3),(3,1)\}$ comes first: greedy Alice ends with 4, patient Alice "can finish up with $(3,1)$ for dessert and a total score of 5" — the reader feels the puzzle before any strategy is named.
6. **Contrast and mystery**: state two things that ought to agree, reveal they differ, explain why. ("Perhaps it is this determinism that prevents the sandpile from approximating the circular symmetry…? Not so.")
7. **Toy case first**, even if the toy case is already known.
   - ✓ [MAIS intro] Before the abstract five-stage pipeline, one concrete instance: "consider the problem of building a tool for proving inequalities in a proof assistant" — every stage and every failure mode is illustrated on it.
8. **Prefer the direct formulation to the fancy one.**
   - ✗ "The learning coefficient $\lambda$ appears as the leading pole of the zeta function $\zeta(s)=\int|L(\theta)-L_0|^s\,d\theta$." ✓ "The learning coefficient measures volume growth: the volume of the set of parameters within $\varepsilon$ of the minimal loss scales like $\varepsilon^\lambda$."

## Structure

9. **Spiral when the material allows**: after each new concept, review the earlier ones from its vantage point; plant a key word early and re-mention it with more detail each time. But don't over-reach — never force connections between concepts that are genuinely distinct.
   - ✓ [MAIS intro] "Bounded compute" is planted in the first paragraph (a mathematician is "a professional allocator of bounded compute"), returns as logical induction, returns again as resource-bounded Löb — each pass more precise.
10. **Keep the big picture on the page**: milestones early, technicalities pushed back; the reader should always know the near-term and long-term objective and why the current step is plausible.
11. **One point per paragraph**, usually 2–4 sentences. Transitions between sections explicit but brief.
12. **Proofs are modular and explicitly strategized**: announce the plan ("Our strategy will be to define a chain $\xi$…"), track progress ("It remains to show…"), use "To see this" for quick sub-arguments, and break long proofs into named lemmas stated to be easy to *use*.

## Math and prose

13. **Oscillate registers**: formal when stating theorems, conversational when motivating them. This oscillation between rigor and intuition is the signature rhythm.
14. **Never leave a formal statement without a prose gloss**: restate informally, give the intuition, note the surprise, or announce the strategy. State definitions twice, formally and informally. Pay special attention to precision in the gloss — as a test, could the reader reconstruct the formal statement from the gloss alone?
    - ✗ "In other words, the epicenter is roughly uniform." (sounds fine; reconstructs to the wrong statement) ✓ "In other words, the epicenter $i_\tau$ has the same distribution as the input." (survives the round trip)
15. **Tell the reader where every statement stands**: proved, assumed, about to be proved, or open.
16. **Label heuristic reasoning as such**, so it can't be mistaken for proof.
17. **Words over symbols in prose**: no ∀ ∃ ⇒ in sentences; never start a sentence with a symbol; the paragraph should still read when the formulas are skipped.
18. **Display an equation the way you'd place a figure.** The eye jumps to a display first, then scans the surrounding text to make sense of it — the purpose of display is eye-friendly page layout, not just readability of the equation. So display only the crucially important, even if it's simple, and inline the rest.
    - ✓ [Ethiopian Dinner] What gets displayed is the crucially important, even though it's words — the mantra: "Eat your opponent's least favourite morsel on your own last move." Routine expressions like $a_i+b_i$ stay inline.

## Sentences

19. **Vary sentence length**; save short declaratives for punchlines.
20. **Qualifications ride in parentheses or a footnote**, not in stacked subordinate clauses; a sentence that needs several gets split.
    - ✗ "The burning test, which was introduced by Dhar, and which applies when the graph is Eulerian, identifies…" ✓ "Dhar's burning test [Dhar90] identifies the recurrent states of the open chain on an Eulerian graph."
21. **Footnotes may carry real intellectual content** — a Goodhart's Law connection, a mathematical justification — keeping the main text clean while rewarding close readers.
22. **Evocative names for central objects, bland names for peripheral ones.** A good name is a handle that transmits insight.
    - ✗ "the KC-strategy," "Algorithm A" ✓ "the crossout strategy" (its mantra is the name); "burst size," "straw that breaks the camel's back" — while peripheral cases stay bland: Type I, Type II.
23. **Dashes sparingly**; no em-dash asides where a comma or a new sentence will do.
24. **Unobtrusive style**, like good background music: write to communicate, not to impress.
25. **No private jargon.** A term coined in a chat or an earlier draft means nothing to the reader — always write with the reader in mind.
26. **Avoid LLMisms and verbal tics**: the "it's not X, it's Y" construction; "exactly" deployed just to sound exact; "substrate," "instrument," "doing real work," "load-bearing," "clean," "gap." All of these have their place — use them mindfully, not by reflex.

## Notation

27. **Notation is a system, designed before writing**: one concept, one notation; never one notation for two things; minimal subscripts; no irrelevant labels; name-and-conquer recurring subexpressions.
28. **Key terms bold at first appearance**; theorem environments get monikers (`\moniker{Aggregate density}`, `\moniker{Cutoff}`) so results are memorable by name.

## Honesty and persuasion

29. **True persuasion**: hold your view with conviction; understand deeply how the reader's view differs; empathize with why theirs feels natural to them; then gently — playfully but seriously — offer yours as an alternative. The failure mode that looks like persuasion but isn't: optimizing the reader's opinion of the author.
    - ✓ [MAIS intro] The artisanal and industrial stances are honored before the civic one is offered: "This survey is an invitation to try the third stance. The stances are not exclusive…" — the reader's current view respected, the alternative offered gently.
30. **Describe results accurately**: no overstatement, no understatement. Note what's unknown when the gap matters to the main narrative; don't chronicle every unknown.
31. **Justify every inclusion by truth and clarity**, never by projected effect on the reader: no hype, no name-dropping, no "seminal." Never advertise a problem's appeal — demonstrate it.
32. **State negative results constructively**: name the next step they make urgent, not the doom they imply.
    - ✗ "stated values cannot be externally verified from behavior, and the trust assumption is irreducible." ✓ "…so research into clear-box character verification or 'proof-of-character-training' becomes a high priority."
33. **Communicate ways of thinking, not just theorems.** One person's clear mental image is another's intimidation, so offer more than one way to see the central object.

## Revision

34. **Prevent relics — don't insert them in the first place.** Every sentence is addressed to the reader of *this* draft, not to a collaborator or an earlier version. Then sweep once anyway for overcorrections and leftover hedges.
    - ✗ "We give three applications" atop a section that now contains two — a promise from an earlier draft. ✓ Promises, counts, and cross-references get written to the current draft, or written last.
35. **Never open a paragraph with an unanchored back-reference.** Re-establish the object in place, then proceed.
    - ✗ "The Opus 4.5 episode from the introduction is the verification gap in concrete form." (what episode? what gap?) ✓ "When a lab deploys a new model, what would enable auditors and researchers to verify the constitution it was trained on? As a case study…"
36. **The avoid-list**: no throat-clearing openings ("It is well known that…"); no gratuitous formalism (a definition stated only to be used a page later); no apologetic hedging ("We humbly conjecture…" — just conjecture); no restating the same result three ways; no bullet-point prose outside genuine lists.
37. **End on a payoff** — a picture, an application, a line that lands the point — not a summary. Then stop, with no further ado.
    - ✓ [Ethiopian Dinner abstract] "We conclude that it's never too early to start thinking about dessert." ✓ [MAIS conclusion] "…strip it down to the simplest interesting case, and start proving things!"
