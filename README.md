<!-- solve-problem:62c3cedb-32bf-4c60-95c1-7d158f32d7e7 -->
# Strong bounded-depth Frege bounds for random 3-CNF

A [Tangle Solve problem](https://solve.tangle.tools/problems/62c3cedb-32bf-4c60-95c1-7d158f32d7e7).

## What is the problem?

Prove superpolynomial — ideally exponential in n — lower bounds on the size of bounded-depth Frege refutations of random unsatisfiable 3-CNF formulas.

**Setting.** Sample a random 3-CNF F with n variables and m = Δn clauses, each clause a uniformly random triple of distinct literals. For Δ above the satisfiability threshold (Δ ≈ 4.267) F is unsatisfiable whp. A depth-d Frege proof system is a propositional proof system with a fixed finite sound/complete rule set, where every formula in the proof has depth ≤ d (constants, literals, ¬, ∧, ∨; leaves are literals, ∧/∨ gates of unbounded fan-in). Size = total symbols. **Goal:** show that whp over F, any depth-d Frege refutation of F has size ≥ T(n), for each fixed d, with T superpolynomial, ideally exp(n^c).

Note: the regime below the threshold (contradictory formulas obtained by requiring a random satisfiable formula plus its negation, or F plus random clauses forcing unsatisfiability) is handled differently; here the target is genuinely unsatisfiable random formulas at large constant density Δ. A subtlety: at large Δ, the formula is trivially refutable by resolution in polynomial size? No — random 3-CNFs at large constant Δ are hard for resolution: Chvátal–Szemerédi give exponential resolution lower bounds. The question is whether analogous exponential bounds hold for depth-2 Frege (= resolution with conjunctions? note depth conventions: depth-2 Frege already extends resolution).

## Why does it matter?

This is the natural proof-complexity counterpart of the empirically observed hardness of random SAT instances, and a key test of whether proof complexity can explain SAT-solver performance. Currently, exponential lower bounds for AC⁰-Frege (bounded-depth Frege) exist only for crafted formulas (parity variants, Tseitin, Pigeonhole-style); random 3-CNFs are the paradigmatic "natural" hard instances. Resolving it would also advance the frontier between resolution and full Frege lower bounds — a major open problem — and connect proof complexity to the statistical-physics picture of the random-SAT phase transition and algorithmic barriers.

## What's already known?

- **Resolution:** Chvátal–Szemerédi (1988): whp, random 3-CNF at constant density requires exponential-size resolution refutations. Hence depth-1 (tree-like/resolution) lower bounds are classical.
- **Depth-d Frege for random 3-CNF:** Gryaznov–Talebanfard (2024) prove n^{1+ε_d} lower bounds for each fixed depth d, via a deterministic-restrictions argument; ε_d → 0 as d grows. This is superlinear but not superpolynomial.
- **Crafted formulas:** exponential AC⁰-Frege lower bounds for modified parity principles, Tseitin contradictions on expanders (with auxiliary variables), and the Ajtai–Ben-Sasson–Håstad–Maass–Pitassi themes; the dominant technique is Håstad's switching lemma applied via random restrictions, showing shallow formulas simplify under restriction.
- **Why existing approaches fall short:** random 3-CNFs do not encode a compact algebraic/combinatorial principle; the usual "hit with a random restriction and use a switching-lemma round" strategy gives only mildly superlinear size bounds because the density of the formula survives restrictions poorly, and iterating restrictions across d rounds loses too much (hence ε_d shrinking).

(Verify all claims against the cited 2024 paper.)

## What would count as solving it?

Success = a theorem: "For every fixed d ≥ 2 there exist Δ₀ and c > 0 such that whp over random 3-CNF F with n variables and Δn ≥ Δ₀n clauses, every depth-d Frege refutation of F has size ≥ exp(n^c)." Intermediate acceptable milestones:
1. Any fixed superpolynomial bound n^{ω_d(1)} for fixed d ≥ 2 (strictly improving GT2024).
2. Exponential bounds for depth 2 or 3 specifically.
3. Improved quantitative tradeoff: superpolynomial for d up to c log n / log log n.
A referee would want the bound to hold for genuinely unsatisfiable dense random formulas (or the standard surrogate: F ∧ (clauses forcing an assignment) — but that variant is weaker; state which).

## How to start

1. Read Gryaznov–Talebanfard, arXiv:2403.02275, carefully — identify exactly where the ε_d loss arises (the deterministic-restriction switching argument) and whether a sharper multi-round analysis or restriction distribution can amplify it.
2. Study the classical pipeline: Håstad's switching lemma and Krajíček's "Bounded Arithmetic, Propositional Logic, and Complexity Theory" Ch. on AC⁰-Frege lower bounds; compare how parity/Tseitin get exponential bounds via "many" independent critical restrictions vs. the single-survivor structure of random CNFs.
3. Consider structural properties of dense random 3-CNFs: expansion of the clause-variable incidence graph, clustering of satisfying assignments of random 2-CNF projections, or the statistical-mechanics condensation picture as a switching-lemma-friendly invariant.
4. Main obstacle: no known "semantic certificate" of hardness for random CNFs that survives d rounds of restriction alternation; the resolution lower bound via width (Ben-Sasson–Wigderson) has no depth-d analogue.

## Key references

- V. Gryaznov, N. Talebanfard, *Bounded-Depth Frege Lower Bounds for Random 3-CNFs via Deterministic Restrictions*, arXiv:2403.02275 (2024). Establishes n^{1+ε_d} depth-d Frege lower bounds for random 3-CNFs; the current state of the art and the direct starting point. https://arxiv.org/abs/2403.02275
- V. Chvátal, E. Szemerédi, *Many hard examples for resolution*, J. ACM 35(4), 1988. Exponential resolution lower bounds for random 3-CNFs at constant density — the depth-1 baseline technique.
- E. Ben-Sasson, A. Wigderson, *Short proofs are narrow — resolution made simple*, J. ACM 48(2), 2001. Width–size tradeoff for resolution, the engine behind resolution lower bounds; useful for understanding why it doesn't lift.
- J. Håstad, *Computational Limitations of Small-Depth Circuits*, MIT Press, 1987. The switching lemma, the core tool for all shallow-circuit/proof lower bounds.
- (verify) J. Krajíček, *Bounded Arithmetic, Propositional Logic, and Complexity Theory*, Cambridge, 1995 — Ch. on AC⁰-Frege: general framework for depth-d Frege lower bounds via restrictions.

## Warnings

- Depth conventions vary (is resolution depth 1 or 2?); state your convention and compare bounds accordingly.
- Beware the "cheap" variant: adding explicit contradiction clauses to a random satisfiable formula makes the problem much easier to refute — lower bounds for that surrogate don't settle the random-unsat formula question; conversely, upper-bound constructions often exploit such surrogates.
- Very large density (Δ ≥ C log n or polynomial) makes formulas easy; the interesting regime is constant Δ.
- Random 3-CNFs lack the algebraic structure (parity, Tseitin labels) powering prior exponential AC⁰-Frege bounds — expect to need a genuinely new invariant, not a direct adaptation.
- Verify all citations and the exact statement of the 2024 result before building on it; details above reconstructed from the census record and field knowledge.

---
*`ALGO-000069` · unverified*

## Acceptance guidance

Success = a theorem: "For every fixed d ≥ 2 there exist Δ₀ and c > 0 such that whp over random 3-CNF F with n variables and Δn ≥ Δ₀n clauses, every depth-d Frege refutation of F has size ≥ exp(n^c)." Intermediate acceptable milestones:
1. Any fixed superpolynomial bound n^{ω_d(1)} for fixed d ≥ 2 (strictly improving GT2024).
2. Exponential bounds for depth 2 or 3 specifically.
3. Improved quantitative tradeoff: superpolynomial for d up to c log n / log log n.
A referee would want the bound to hold for genuinely unsatisfiable dense random formulas (or the standard surrogate: F ∧ (clauses forcing an assignment) — but that variant is weaker; state which).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/62c3cedb-32bf-4c60-95c1-7d158f32d7e7?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000069.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000069)
