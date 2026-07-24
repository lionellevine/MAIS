> **Historical scoped-verification record.** This report rechecks content-destructive verdicts about a pre-repair draft of [MAIS-A3](../../../agendas/MAIS-A3/); it is not a second audit of the current edition. Item and line numbers may differ. See the [audit index](../README.md) and [repair log](../REPAIR-LOG.md).

# Verification of selected verdicts in `superposition-geometry-codex-report.md`

- **File audited:** `open problem supplement/superposition-geometry.tex`
- **Audit report verified:** `audit/superposition-geometry-codex-report.md` (GPT 5.6 Sol)
- **Date:** 2026-07-16
- **Verifier:** Claude Fable 5, scoped verification pass
- **Scope note:** This pass covers only content-destructive verdicts; ill-posed and related-work verdicts were deliberately not pre-verified.

Items verified: (1) Conjecture 4.4 graded RESOLVED-false; (2) Conjecture 4.5 graded RESOLVED-true; (3) Problem 4.7 graded POSSIBLY-RESOLVED. Items 1–2 were re-derived by hand in full; item 3 was checked against the two cited primary sources (Spielman–Wang–Wright, arXiv:1206.5882; Awasthi–Vijayaraghavan, arXiv:1804.08603), fetched 2026-07-16.

---

## Item 1. Conjecture 4.4 (`conj:independent`) graded RESOLVED-false — **CONFIRMED**

**Hypothesis check.** The conjecture (tex lines 222–230) quantifies over all $m\ge2$, all $n$, product Bernoulli supports with any $p>0$, $\nu=\mathrm{Unif}[1,2]$, $\sigma=0$, and requires only the two displayed inequalities. The counterexample takes $m=2$, $p=1$, $\Phi=(e_1,e_2)\subset\R^n$. Then $\mu=0$, so the first inequality holds for any $c>0$; and $pm+\log m=2+\log 2$ is constant while the second inequality's right side $c\sqrt{n/\log m}$ grows with the free parameter $n$, so it holds once $n\ge \log 2\,\bigl((2+\log2)/c\bigr)^2$. Every stated hypothesis is satisfied; nothing is violated. (The file's own prose at line 232 claims the second inequality excludes $p=1$; it does not, because $n$ is untethered to $m$.)

**Re-derivation of the computation.** Data: $y=ae_1+be_2$, $a,b\sim\mathrm{Unif}[1,2]$ i.i.d.

1. *True dictionary.* At $\Phi=(e_1,e_2)$ the nonnegative lasso separates coordinatewise: $\min_{z_1\ge0}\tfrac12(a-z_1)^2+\lambda z_1$ has optimum $z_1=a-\lambda$ (valid since $a\ge1>\lambda$), value $\lambda a-\lambda^2/2$. Summing and taking expectations: $F_\lambda(\Phi)=\lambda\,\E[a+b]-\lambda^2=3\lambda-\lambda^2$. Matches the report.
2. *Slanted dictionary.* For $u_1=(2e_1+e_2)/\sqrt5$, $u_2=(e_1+2e_2)/\sqrt5$: solving $2z_1+z_2=\sqrt5\,a$, $z_1+2z_2=\sqrt5\,b$ gives $z=\tfrac{\sqrt5}{3}(2a-b,\,2b-a)$, which is $\ge0$ on $[1,2]^2$ (since $2a-b\ge0$, $2b-a\ge0$) with exact reconstruction and $\|z\|_1=\tfrac{\sqrt5}{3}(a+b)$. Hence $\ell_\lambda\le\lambda\|z\|_1$ and $F_\lambda(\Psi)\le\sqrt5\,\lambda\approx2.236\,\lambda$. Matches the report.
3. *Exclusion of recovering dictionaries.* Suppose $\Psi=(u_1,u_2)$ $(C\lambda)$-recovers $\Phi$, i.e. $\langle u_1,e_1\rangle,\langle u_2,e_2\rangle\ge1-C\lambda$ (up to relabeling); then $\|u_j-e_j\|\le\sqrt{2C\lambda}$. Test against $h=(e_1+e_2)/\sqrt2$: $\langle u_j,h\rangle\le 1/\sqrt2+\sqrt{2C\lambda}$, so for any $z\ge0$ with $t=\|z\|_1$, $\|y-\Psi z\|\ge\langle y-\Psi z,h\rangle\ge \tfrac{a+b}{\sqrt2}-t\bigl(\tfrac1{\sqrt2}+\sqrt{2C\lambda}\bigr)$. Minimizing $\tfrac12(r-\beta t)_+^2+\lambda t$ in $t$ gives $\ell_\lambda(y,\Psi)\ge\lambda(a+b)/(1+2\sqrt{C\lambda})-\lambda^2\ge\lambda(a+b)(1-2\sqrt{C\lambda})-\lambda^2$, hence $F_\lambda(\Psi)/\lambda\ge 3-6\sqrt{C\lambda}-\lambda$. This matches the report's $3-O(\sqrt\lambda)$.
4. *Conclusion.* Since the global minimum value is at most $\sqrt5\lambda$, once $6\sqrt{C\lambda}+\lambda<3-\sqrt5\approx0.764$ no global minimizer of $F_\lambda$ can $(C\lambda)$-recover $\Phi$. As the conjecture demands recovery for every $\lambda\in(0,c)$, it is refuted for every proposed pair $(c,C)$. The requirement $Cc<1$ does not rescue it.

**Verdict: CONFIRMED.** The counterexample is complete, correct, and violates no stated hypothesis; RESOLVED-false is the right grade.

**Minimal repair:** replace the second displayed hypothesis with a bound that does not weaken as the ambient $n$ grows — e.g. state the conjecture in an explicitly overcomplete regime $m>n$ (so $p=1$ forces $pm=m>n\ge$ RHS$^2$-scale, a contradiction) or add a direct $n$-free cap on the expected support size $pm$ — and correct the prose at line 232 accordingly.

---

## Item 2. Conjecture 4.5 (`conj:nested`) graded RESOLVED-true with $\lambda_0=1$, $C=0$ — **CONFIRMED**

**Re-derivation.** Model (tex lines 146–156, 234–240): $y=v_1$ w.p. $1-\rho$, $y=v_1+v_2$ w.p. $\rho$; $\theta\in(0,\pi/2]$, $\rho\in(0,1)$; estimator $F_\lambda$ over $U_{n,2}$ (unit-norm atoms, nonnegative codes).

1. *Pointwise radial lower bound.* For unit-column $\Psi$ and $z\ge0$ with $t=\|z\|_1$: $\|\Psi z\|\le\sum_j z_j\|u_j\|=t$, so $\|y-\Psi z\|\ge(r-t)_+$ with $r=\|y\|$. Hence $\ell_\lambda(y,\Psi)\ge\min_{t\ge0}\tfrac12(r-t)_+^2+\lambda t$, which equals $\lambda r-\lambda^2/2$ for $\lambda<r$ (optimal $t=r-\lambda$) and $r^2/2$ for $\lambda\ge r$. Matches the report's display.
2. *Equality condition.* Equality at $\lambda<r$ forces equality in the triangle inequality (all active atoms equal $y/\|y\|$) and $\Psi z$ positively parallel to $y$: i.e., some atom sits exactly on the ray of $y$. If no atom is on the ray, a minimizing code exists (coercivity) and pays strictly more.
3. *Achievability and uniqueness.* The two data rays are $v_1$ ($r=1$) and $v_1+v_2$ ($r=2\cos(\theta/2)\ge\sqrt2$ for $\theta\le\pi/2$). For $\lambda\in(0,1)$, $\lambda<r$ on both events. The dictionary $\{v_1,w\}$, $w=(v_1+v_2)/\|v_1+v_2\|$, attains the bound on both: $z=(1-\lambda,0)$ gives $\lambda-\lambda^2/2$; $z=(0,\,2\cos(\theta/2)-\lambda)$ gives $2\cos(\theta/2)\lambda-\lambda^2/2$. Both events have positive probability ($\rho\in(0,1)$) and distinct rays ($\theta>0$), so any minimizer must place one atom on each ray; with $M=2$ that forces $\Psi=\{v_1,w\}$ up to permutation, and it is the unique global minimizer.
4. *Conclusion vs. quantifiers.* For $\Psi=\{v_1,w\}$: $\langle v_1,v_2\rangle=\cos\theta$ and $\langle w,v_2\rangle=(1+\cos\theta)/(2\cos(\theta/2))=\cos(\theta/2)$, so $\max_j\langle u_j,v_2\rangle=\cos(\theta/2)$ exactly (for $\theta\in(0,\pi/2]$, $\cos(\theta/2)>\cos\theta$). The conjecture asks for $\exists\,\lambda_0,C$ depending on $(\theta,\rho)$ with $\max_j\langle u_j,v_2\rangle\le\cos(\theta/2)+C\lambda$ for all $\lambda\in(0,\lambda_0)$; this holds with the uniform constants $\lambda_0=1$, $C=0$, strictly stronger than required. The "in particular" clause (no $\varepsilon$-recovery for $\varepsilon<1-\cos(\theta/2)-C\lambda$) follows immediately.

**Verdict: CONFIRMED.** The radial argument is a complete proof; RESOLVED-true with $\lambda_0=1$, $C=0$ is correct. (The report's side claim that this also settles the $b=0$ face of Problem 5.1 follows from the same uniqueness statement, though that verdict was outside this pass's scope.)

**Minimal repair:** restate Conjecture 4.5 as a proposition with the four-line radial-thresholding proof above, and sweep the prose that presents it as open (tex lines ~242, 303, 315, 325, 339).

---

## Item 3. Problem 4.7 (`prob:samples`) graded POSSIBLY-RESOLVED — **PARTIAL**

The auditor's citations are apt and its criticism of the file's blanket "open even for $k=\lceil\log m\rceil$" is substantially right, but "possibly-resolved" overstates what the cited results cover. Checked against the primary sources:

**What the file's problem actually asks** (tex lines 258–260): do there exist $N=\mathrm{poly}(m)$ *designed* $k$-sparse codes such that for **almost every** (Lebesgue) $A$ satisfying only the **spark** condition, the dataset is *uniquely coded* — exact uniqueness $B=APD$ against **every** $B\in\R^{n\times m}$ and every **column-$k$-sparse** competing code matrix — with $n\ge2k$ allowed (including the minimal $n=2k$, and including square $m=n$).

**Spielman–Wang–Wright (COLT 2012, arXiv:1206.5882), Theorem 3 (Uniqueness), read directly:** square $m=n$, arbitrary nonsingular $A$, Bernoulli($\theta$)–subgaussian codes with $1/n\le\theta\le1/C$, $p>Cn\log n$ samples; w.h.p. any alternative factorization $Y=A'X'$ **with $\max_i\|e_i^{\top}X'\|_0\le\max_i\|e_i^{\top}X\|_0$** satisfies $A'=A\Pi\Lambda$. The sparsity range comfortably includes $\theta\approx(\log n)/n$, the good event depends only on $X$ (so one realization works for all nonsingular $A$ simultaneously, matching the file's $\exists x\,\forall A$ quantifier), and the report's conditioning argument for exact $k$-sparsity goes through. **However, the competitor class is row-sparsity-bounded, not column-$k$-sparse.** These classes are incomparable: a column-$k$-sparse competitor may have rows far denser than the true $X$'s $\approx\theta p$ maximum row weight (total budget $kp\gg\theta p$ concentrated in few rows), so SWW's theorem does not exclude it. Even the square subcase of the file's "uniquely coded" property is therefore not literally settled by SWW without an additional argument — contrary to the report's assertion that conditioning "gives existential polynomial-size, $k$-sparse datasets in the allowed square regime."

**Awasthi–Vijayaraghavan (FOCS 2018, arXiv:1804.08603), Informal Theorem 1.4 (Polynomial Identifiability), read directly:** requires $A$ to be $(k,\delta=1/\mathrm{polylog}(m))$-**RIP** with $k\le n/\mathrm{polylog}(m)$; supports arbitrary $k$-sparse subject to a **triples condition** (every triple of columns co-occurs in a $1/\mathrm{poly}(n)$ fraction of samples); Rademacher/spike-and-slab values; conclusion is recovery of $\hat A$ with $\|\hat A_i-b_iA_i\|\le1/\mathrm{poly}(m)$, w.h.p. Three mismatches with the file's problem: (a) RIP with $\delta=1/\mathrm{polylog}$ fails on a positive-measure set of matrices, so it does not cover "almost every $A$ satisfying spark"; (b) the guarantee is approximate recovery within their generative model, not exact factorization uniqueness against arbitrary column-$k$-sparse competitors; (c) $k\le n/\mathrm{polylog}(m)$ excludes the minimal-dimension regime $n=2k$ the file explicitly allows. (The designed-codes and triples-condition aspects, by contrast, are compatible with the file's existential quantifier.)

**Verdict: PARTIAL.** Both sources cover neighboring subregimes or variant uniqueness notions — SWW a row-sparse-competitor uniqueness in the square case at logarithmic (indeed up to linear) sparsity, A–V approximate identifiability for RIP dictionaries at near-linear sparsity — and per the coverage rule (subregime = partial) the correct grade is *open-with-related-work*, not *possibly-resolved*. What survives of the finding: the file's unqualified sentence "open even for $k=\lceil\log m\rceil$" is misleading as written and must be sharpened to its exact uniquely-coded notion (a.e.-spark $A$, exact uniqueness, column-$k$-sparse competitors, all $n\ge2k$), with SWW and A–V cited as the near-misses that make the qualification necessary. What does not survive: the suggestion that the square subcase is already settled.

---

## Summary

| Item | Auditor's grade | This verification |
|---|---|---|
| Conjecture 4.4 | resolved (false) | **CONFIRMED** — counterexample re-derived in full; no stated hypothesis violated |
| Conjecture 4.5 | resolved (true, $\lambda_0=1$, $C=0$) | **CONFIRMED** — radial bound re-derived; constants and quantifiers check |
| Problem 4.7 | possibly-resolved | **PARTIAL** — sources cover variant/subregime results only (SWW: row-sparse competitor class, square case; A–V: RIP not a.e.-spark, approximate not exact, $n\gg k\,\mathrm{polylog}$); correct grade is open-with-related-work, though the file's "open even for $\log m$" prose does need qualification |

**Recommendation:** apply findings 1 and 2 as written (rewrite Conjecture 4.4's hypotheses with an $n$-free density bound; promote Conjecture 4.5 to a proved proposition and update dependent prose), and downgrade the Problem 4.7 verdict to open-with-related-work while adding the SWW and Awasthi–Vijayaraghavan citations and sharpening the openness sentence to the file's exact uniqueness notion.
