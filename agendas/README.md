# Research agendas

Research directions: a motivating question, some real mathematics, and a cluster of related open problems. Agendas incorporate [open problems](../open/) and spin off [papers](../papers/).

Agendas are numbered MAIS-A1, MAIS-A2, … in order of arrival; numbers are permanent. Each agenda below expands one starred Open Problem of the survey [*Math for AI Safety: An Invitation for Mathematicians*](../papers/MAIS-P1/MAIS-P1.pdf) and begins by reproducing its statement. The survey statement is authoritative: when an open problem changes there, the change must be propagated to the corresponding agenda.

| # | Agenda | Source | PDF | Status |
|---|--------|--------|-----|--------|
| MAIS-A1 | Quantitative bounded Löb | [TeX](MAIS-A1.tex) | [PDF](MAIS-A1.pdf) | Draft · July 12, 2026 |
| MAIS-A2 | Behavioral tomography of world-models | [TeX](MAIS-A2.tex) | [PDF](MAIS-A2.pdf) | Draft · July 12, 2026 |
| MAIS-A3 | The geometry and identifiability of superposition | [TeX](MAIS-A3.tex) | [PDF](MAIS-A3.pdf) | Draft · July 12, 2026 |
| MAIS-A4 | Training for interpretability | [TeX](MAIS-A4.tex) | [PDF](MAIS-A4.pdf) | Draft · July 12, 2026 |
| MAIS-A5 | Which irreducible representations does training select? | [TeX](MAIS-A5.tex) | [PDF](MAIS-A5.pdf) | Draft · July 12, 2026 |
| MAIS-A6 | Does geometric simplicity force a legible mechanism? | [TeX](MAIS-A6.tex) | [PDF](MAIS-A6.pdf) | Draft · July 12, 2026 |
| MAIS-A7 | Effective loss and learning dynamics | [TeX](MAIS-A7.tex) | [PDF](MAIS-A7.pdf) | Draft · July 13, 2026 |
| MAIS-A8 | A predictive theory of out-of-distribution generalization | [TeX](MAIS-A8.tex) | [PDF](MAIS-A8.pdf) | Draft · July 16, 2026 |

## Provenance

These agendas are an experiment in AI-written mathematics, published with their provenance on the table. Each was written by **Claude Fable 5** (Anthropic) under Lionel Levine's direction: he chose the problems, set the standard — self-contained, every statement precise, every problem stated as open genuinely believed open — and reviewed the results. The drafts then went through an adversarial review, one independent reviewing agent per file, with every reported issue either fixed or rejected with a recorded dissent; each file was then independently audited by **GPT 5.6 Sol** (OpenAI), which checked the proofs of the small results proved along the way, the precision of each problem statement, and — with literature search — whether each problem stated as open is in fact open. The audit's findings were resolved in a documented repair round, and results the audit itself contributed are credited in-file.

No human has verified every line of these files, and the byline is meant to say so plainly. If you find an error, or believe a problem stated here as open has been resolved, please open an issue; corrections are credited.

## Rebuilding

To rebuild an agenda, run `latexmk -pdf -interaction=nonstopmode -halt-on-error MAIS-A1.tex` from this directory. Only each `.tex` source and its matching `.pdf` are committed; LaTeX auxiliary files are ignored.
