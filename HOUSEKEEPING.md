# Housekeeping

Conventions that keep this repository consistent. Readers don't need this page; it's for anyone editing the repository itself.

## Identifiers and numbering

- Every document carries a unique permanent identifier: **MAIS-On** for open problems, **MAIS-An** for agendas, **MAIS-Pn** for papers. Numbers are assigned on arrival and never reused.
- The identifier names the mathematical content, not a file: a problem keeps its O-number when it is quoted in a paper, expanded into an agenda, or resolved.
- [open-problems/README.md](open-problems/README.md) is the full registry. A new problem lands as its page, its registry row, and its jump-list entries in the same commit. Before assigning a number, compare against the existing statements: a strict first case or a different deliverable may earn its own identifier; a restatement does not.
- The seed agendas A1–A8 expand the survey's headline problems O1–O8. The matching numbers record those particular relationships, not a general convention — a future agenda need not match its problem's number.

## Files and folders

- Folder names carry no MAIS- prefix (`agendas/A1/`, `papers/P2/`); filenames keep it (`MAIS-A1.tex`).
- Each agenda and paper folder is its landing page: a `README.md` with title, byline, abstract, and links, like an arXiv abstract page. Links elsewhere in the repository point to landing pages, not directly to PDFs — except links explicitly labeled "PDF".
- Each agenda and paper records its origin in a `PROVENANCE.md` beside its source.
- Every document opens with a status line: kind + number · author · date · status.

## Building

- Rebuild any document with LaTeX source by running `latexmk -pdf -interaction=nonstopmode -halt-on-error <FILE>.tex` from its folder. Only each `.tex` and its matching `.pdf` are committed; LaTeX auxiliary files are ignored.
- MAIS-P1 is a fixed PDF: a solo paper nearing completion, so its source is not a collaboration surface and is not in the repository.
