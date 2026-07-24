# Contributing

Each document in this repository has its own author list and its own status, noted at the top of the file. Contributions of every size are welcome!

## The short version

Open an **issue** — a public comment thread attached to this repository. A correction, a counterexample, a half-formed idea, a paragraph of Markdown or LaTeX: post it, and it can be read and answered by anyone here. If you would rather stay off GitHub, email works ([lionel.levine@cornell.edu](mailto:lionel.levine@cornell.edu)), but I process email slowly and in batches, so the public thread is the faster door. Either way, contributions that get used get credited.

## GitHub for mathematicians

GitHub organizes collaboration around two objects with opaque names. An **issue** is a public comment thread attached to the repository — the place to ask a question, report an error, float an idea, or announce that you are working on something.  A **pull request** is a proposed edit: a marked-up copy of one or more files, submitted for the authors to review and merge — the manuscript with margin notes. Both require only a free account, created in a minute at [github.com/signup](https://github.com/signup). To follow what happens here, press **Watch** at the top of the [repository page](https://github.com/lionellevine/MAIS) for notifications of new threads, or subscribe to the [feed of changes](https://github.com/lionellevine/MAIS/commits/main.atom).

## Rough ideas are welcome!

The [Polymath projects](https://polymathprojects.org/) ran on a rule worth keeping: share rough ideas instead of waiting to polish them. The same rule applies here. Contributions that become part of a document should eventually meet the house style in [STYLE.md](STYLE.md) — a style guide written with language models in mind: if you use LLMs in your writing process, provide them with STYLE.md so that they write in the house style.

## Corrections and small improvements

Typos, broken references, clearer phrasings, missing citations: edit the file directly on GitHub — the pencil icon on any file page opens an editor, and **Propose changes** turns your edit into a pull request, with the machinery of forks and branches handled invisibly. Merged corrections are acknowledged in the relevant document.

## Substantial contributions

Progress on an open problem, a new result, a counterexample, a new section or worked example: **say so before investing serious work**, in an issue or by email. This protects you from duplicating effort or working at cross purposes with the authors, it lets others see that the problem is being actively worked on, and it puts the coauthorship question on the table from the start.

## Coauthorship

A substantial contribution to a document earns an invitation to join that document's author list. This applies at every rung of the ladder: helping an open problem grow into an agenda, or an agenda spin off a paper, is the kind of contribution that makes a coauthor.

What counts as substantial is judged per document by its current authors, in conversation with the contributor, and settled before the contribution is merged. When in doubt, ask, in an issue or by email; erring on the side of asking costs nothing.

If your problem is incorporated into an agenda, you are invited to join the agenda's author list.

## Proposing a new problem

If you have an open problem that fits the collection — a precisely stated math problem motivated by AI safety — describe it in an issue or by email. If it fits, we'll add it to [`open/`](open/) with you as an author.

## Writing math in Markdown

Two formats live in this repo: open problems are Markdown, so they render right on GitHub; agendas and papers are LaTeX, each committed with its compiled PDF (see the folder READMEs for how to rebuild one).

For the Markdown: GitHub renders LaTeX in `.md` files — `$...$` inline, `$$...$$` for displays, and most of `amsmath` works. Writing

```
The board is the torus $\Lambda = (\mathbb{Z}/N\mathbb{Z})^2$, and we ask for
$$\Pr[\text{the board resembles a smiley face}] \ge 1 - 10^{-100}.$$
```

renders as: The board is the torus $\Lambda = (\mathbb{Z}/N\mathbb{Z})^2$, and we ask for

$$\Pr[\text{the board resembles a smiley face}] \ge 1 - 10^{-100}.$$

Three gotchas. For a multi-line display (`aligned`, `cases`, a matrix) — or any display that misrenders — a fenced ` ```math ` block is more robust:

````
```math
d(x,y) = \begin{cases} 0 & \text{if } x = y, \\ 1 & \text{otherwise.} \end{cases}
```
````

```math
d(x,y) = \begin{cases} 0 & \text{if } x = y, \\ 1 & \text{otherwise.} \end{cases}
```

Inside a table, a bare `|` reads as a column divider, so write `\vert` (e.g. `$\vert x \vert$` for $\vert x \vert$). And a literal dollar sign is `\$`.

## License

Everything here is under [CC BY 4.0](LICENSE). By contributing, you agree that your contribution is released under the same license.
