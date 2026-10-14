<!-- solve-problem:ec4c2be5-5f22-47b9-8b99-e43b0c8e702d -->
# Graph isomorphism complexity

A [Tangle Solve problem](https://solve.tangle.tools/problems/ec4c2be5-5f22-47b9-8b99-e43b0c8e702d).

## What is the problem?

The graph isomorphism problem (GI): given two finite undirected graphs G₁ and G₂ on n vertices, decide whether there exists a bijection φ: V(G₁) → V(G₂) preserving adjacency. Formally, GI = {(G₁, G₂) : ∃ permutation π ∈ Sₙ with (u,v) ∈ E(G₁) ⟺ (π(u), π(v)) ∈ E(G₂)}.

The open question: **is GI solvable in polynomial time, i.e., is GI ∈ P?**

Precise framing of what's needed: a deterministic algorithm that decides isomorphism of two n-vertex graphs (adjacency-list or adjacency-matrix input, equivalent up to log factors) in time n^c for an absolute constant c. Equivalent formulations worth knowing: GI is the problem of deciding whether two permutation-group orbits (of Sₙ acting on {0,1}-matrices by simultaneous row/column permutation) intersect; and GI is polynomial-time reducible both ways to canonical labeling (produce a canonical representative of the isomorphism class). A poly-time algorithm for GI (even randomized, by standard derandomization-upwards arguments GI ∈ BPP ⊆ Σ₂^p, so mild assumptions apply — verify details) would settle the question. Ambiguity note: the census asks only about membership in P for general graphs; variants (bounded degree, planar, trees) are known in P and are not the target.

## Why does it matter?

GI is the canonical NP-intermediate candidate: it is in NP but not known in P, and believed not NP-complete (see below), so resolving it either way would be the first natural problem placed definitively on one side. A poly-time algorithm would likely require new machinery in the interplay between combinatorics and permutation groups, with spinoffs for canonical labeling — the computational core of molecule identification in chemistry, circuit equivalence checking, and SAT symmetry breaking. Conversely, an NP-completeness proof would collapse the polynomial hierarchy to its second level, a consequence widely considered false, making GI a structural lightning rod for complexity theory.

## What's already known?

- **Best upper bound:** Babai's quasipolynomial algorithm, exp((log n)^{O(1)}) = n^{polylog n}, announced at STOC 2016; a simplified correctness proof by Helfgelt (arXiv:1710.04574) fixed a gap in the original analysis. The core is the "Local certificates" lemma for vertex-transitive graph structures plus a recursive "divide-and-conquer on Johnson schemes" handling highly regular CRQ structures via the Unaffected Stabilizers lemma.
- **Complexity structure:** GI ∈ NP ∩ co-AM (Goldreich–Merssen–Wigderson... verify exact attribution: interactive proof of non-isomorphism due to Goldreich, Micali, Wigderson). Hence if GI is NP-complete, PH collapses to Σ₂^p (Boppana–Håstad–Zachos). GI is complete for the class SPP under parsimonious reductions (Arvind–Kurur), and is low for PP (Köbler–Schöning–Torán et al.).
- **Known poly-time cases:** bounded-degree (Luks), bounded-genus, bounded-treewidth, interval graphs, planar (Hopcroft–Wong; linear time by Hopcroft–Tarjan lineage), trees. Luks's n^{O(k)} algorithm for degree-k graphs and its group-theoretic bottleneck (composition factors of bounded degree yield only cycles/binary groups — Luks's barrier) is the main historical obstacle.
- **Practice:** nauty/Traces (McKay–Piperno) canonically label graphs with thousands to millions of vertices heuristically-fast; refinement plus individualization–refinement search. Practical hardness lives in strongly regular graph-like (CFI-like) families.
- **Lower bounds:** essentially nothing unconditional; standard reductions from ring/other equivalence problems into GI. Erdős–Rényi random graphs are trivially canonizable whp.

Why quasipolynomial falls short: Babai's recursion over Johnson schemes loses polylog factors inherently; no one has shown how to compress the recursion tree to constant depth or replace design/scheme recursion with a poly-time invariant.

## What would count as solving it?

**Primary (positive):** a proof that GI ∈ P — an explicit deterministic algorithm with proven worst-case running time n^c, published with full correctness proof. Alternatively (and equally accepted): a poly-time canonical labeling algorithm.

**Secondary variants worth listing:**
- GI ∈ BPP or GI ∈ quasi-NC would be major partial results.
- A tight connection resolving the "Luks barrier": e.g., poly-time isomorphism for all strongly regular graphs would be significant progress.
- **Negative side:** a proof that GI is NP-complete (implies PH = Σ₂^p), or a super-quasipolynomial lower bound in any credible model — either would also "settle" the census question negatively, though neither is expected.

A referee accepts: full algorithm + correctness proof + running-time analysis, or an unconditional lower bound / structural collapse theorem.

## How to start

1. **Read Babai's paper first** (arXiv:1512.03547, esp. the outline sections and the "Local certificates" and "Design lemma" sections). Understand precisely where polylog factors are lost: (a) the multiplicative-structure/agreement theorem depth, (b) the recursion over block systems.
2. **Read Luks 1982 (JCSS, degree-bounded GI)** to internalize the group-theoretic bottleneck: why composition factors that are non-cyclic, non-alternating blow up the recursion.
3. **Natural attack:** find a poly-time canonical form or invariant that distinguishes the hard instances — primitive coherent configurations / strongly regular graphs. Even resolving GI in P for strongly regular graphs is open and a plausible stepping stone.
4. **Main obstacle:** quasipolynomiality comes from recursively splitting symmetry in "geometric" (Johnson-like) structures; no known poly-time invariant pins down these structures, and CFI-style / UNG-like families defeat all known poly-time-computable invariants (contrast Weisfeiler–Leman, whose dimension hierarchy provably needs dimension Ω(n) on some instances — Cai–Fürer–Immerman).

## Key references

- L. Babai, "Graph isomorphism in quasipolynomial time", STOC 2016; arXiv:1512.03547. The quasipolynomial-time GI algorithm via group-theoretic recursion, local certificates, and Johnson scheme handling.
- L. Babai, "Graph isomorphism in quasipolynomial time [simplified version]", arXiv:1710.04574, with a fix by H. Helfgelt. Streamlined, fully detailed proof of the above; the version to actually read.
- J. Köbler, U. Schöning, J. Torán, *The Graph Isomorphism Problem: Its Structural Complexity*, Birkhäuser, 1993. Monograph on GI's lowness, completeness for SPP-era classes, and why GI is unlikely NP-complete.
- E. M. Luks, "Isomorphism of graphs of bounded valence can be tested in polynomial time", JCSS 25(1), 1982. Poly-time GI for bounded degree; introduced the group-theoretic methods all later work builds on.
- B. McKay and A. Piperno, "Practical graph isomorphism, II", J. Symbolic Computation 60, 2014. The nauty/Traces canonical labeling tools and the empirical hard-instance families.
- C. Hoffmann, *Group-Theoretic Algorithms and Graph Isomorphism*, LNCS 136, 1982. Early reduction of GI to permutation-group chain problems. (verify availability)

## Warnings

- **Do not attack via Weisfeiler–Leman refinement alone:** Cai–Fürer–Immerman (1992) prove k-dimensional WL fails for all fixed k. Any invariant-based approach must exceed fixed-dimension WL.
- **The Babai paper had a known gap** fixed in arXiv:1710.04574; use that version.
- Random graphs and all practical instances are easy — the problem is entirely about adversarial highly-regular structures (strongly regular graphs, CFI-style families).
- "GI not NP-complete" is a belief, not a theorem: what's proven is the conditional (PH collapse via Boppana–Håstad–Zachos). Don't cite it as unconditional.
- Distinguish GI from graph *automorphism* counting (#GI-like) and subgraph isomorphism (NP-complete); only exact isomorphism of full graphs is the target.
- Babai's result is sometimes miscited as "almost polynomial"; it is quasipolynomial — a genuinely different regime, and the gap to P is the whole problem.

---
*`ALGO-000014` · unverified*

## Acceptance guidance

**Primary (positive):** a proof that GI ∈ P — an explicit deterministic algorithm with proven worst-case running time n^c, published with full correctness proof. Alternatively (and equally accepted): a poly-time canonical labeling algorithm.

**Secondary variants worth listing:**
- GI ∈ BPP or GI ∈ quasi-NC would be major partial results.
- A tight connection resolving the "Luks barrier": e.g., poly-time isomorphism for all strongly regular graphs would be significant progress.
- **Negative side:** a proof that GI is NP-complete (implies PH = Σ₂^p), or a super-quasipolynomial lower bound in any credible model — either would also "settle" the census question negatively, though neither is expected.

A referee accepts: full algorithm + correctness proof + running-time analysis, or an unconditional lower bound / structural collapse theorem.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/ec4c2be5-5f22-47b9-8b99-e43b0c8e702d?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000014.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000014)
