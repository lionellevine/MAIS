# Research agendas

Research directions: a motivating question, some real mathematics, and a cluster of related open problems. Agendas incorporate [research problems](../problems/) and spin off [draft papers](../papers/).

Agendas are numbered A1, A2, … in order of arrival; numbers are permanent. Each agenda below expands one open problem from Lionel Levine's *Math for AI Safety: An Invitation for Mathematicians* and begins by reproducing its statement verbatim.

| Agenda | Survey open problem | Source | PDF | Status |
|---|---|---|---|---|
| A1 | 1 — Quantitative bounded Löb | [TeX](op01-quantitative-bounded-lob.tex) | [PDF](op01-quantitative-bounded-lob.pdf) | Draft · July 12, 2026 |
| A2 | 2 — Behavioral tomography of world-models | [TeX](op02-behavioral-tomography.tex) | [PDF](op02-behavioral-tomography.pdf) | Draft · July 12, 2026 |
| A3 | 3 — The geometry and identifiability of superposition | [TeX](op03-superposition-geometry.tex) | [PDF](op03-superposition-geometry.pdf) | Draft · July 12, 2026 |
| A4 | 4 — Training for interpretability | [TeX](op04-training-for-interpretability.tex) | [PDF](op04-training-for-interpretability.pdf) | Draft · July 12, 2026 |
| A5 | 5 — Representation theory of learned circuits | [TeX](op05-representation-theory-learned-circuits.tex) | [PDF](op05-representation-theory-learned-circuits.pdf) | Draft · July 12, 2026 |
| A6 | 6 — Does geometric simplicity force a legible mechanism? | [TeX](op06-geometric-simplicity-legible-mechanism.tex) | [PDF](op06-geometric-simplicity-legible-mechanism.pdf) | Draft · July 12, 2026 |
| A7 | 7 — Opposing staircases | [TeX](op07-opposing-staircases.tex) | [PDF](op07-opposing-staircases.pdf) | Draft · July 13, 2026 |
| A8 | 8 — A predictive theory of out-of-distribution generalization | [TeX](op08-ood-generalization.tex) | [PDF](op08-ood-generalization.pdf) | Draft · July 16, 2026 |

The survey statement is authoritative. When an open problem changes there, its number, title, and full statement must be propagated to the corresponding agenda.

To rebuild an agenda, run `latexmk -pdf -interaction=nonstopmode -halt-on-error FILE.tex` from this directory. Only each `.tex` source and its matching `.pdf` are committed; LaTeX auxiliary files are ignored.
