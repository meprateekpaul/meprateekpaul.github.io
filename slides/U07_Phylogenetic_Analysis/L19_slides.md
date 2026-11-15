---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 19 Slides: Distance and Character Methods"
footer: "B.Tech. Bioinformatics (SHUATS-inspired) · Prateek Paul"
style: |
  section {
    font-family: 'Inter', sans-serif;
    font-size: 18px;
    padding: 30px;
    background: #0f172a;
    color: #f8fafc;
  }
  h1, h2, h3 {
    color: #38bdf8;
  }
  pre {
    background: #020617;
    color: #a5f3fc;
    border: 1px solid #1e293b;
    border-radius: 8px;
    padding: 12px;
    font-size: 13px;
  }
  footer, header {
    font-size: 11px;
    color: #64748b;
  }
---

<!-- _class: lead -->
# Lecture 19 — Distance and Character Methods
### Concepts of Bioinformatics (CBBI-501)
**Unit 07:** Phylogenetic Analysis  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Two Philosophical Schools of Tree Reconstruction

```text
Topic: Distance-Matrix vs Character-Based Methods

[Visual: Two Paradigms:
  Multiple Alignment -> [Pairwise Distances] -> Distance Matrix -> UPGMA / NJ
  Multiple Alignment -> [Inspect Columns Directly] -> Parsimony / Maximum Likelihood]
```

**Speaker Talking Points:**  
* Tree reconstruction methods divide into two primary mathematical families:
  1. **Distance-Matrix Methods:** Condense the alignment into pairwise distances (loss of data).
  2. **Character-Based Methods:** Evaluate every alignment column directly (retains all data).
* We balance computational speed against biological model sophistication.

---

## Slide 2: Correcting Evolutionary Distances: The Saturation Problem

```text
Topic: Multiple Hits Obscure Real Time

[Visual: Divergence Curve:
  Observed Difference (p) plateaus at 75% for DNA due to multiple substitutions!
  Jukes-Cantor corrected distance d curves upward toward infinity!]

Formula (Jukes-Cantor, 1969):
  d = - (3/4) * ln( 1 - (4/3) * p )
```

**Speaker Talking Points:**  
* Observed sequence difference $p$ underestimates true evolutionary distance.
* If a site mutates $A \to G \to C \to T$, we observe only 1 mutation, but 3 occurred!
* Substitution models correct for hidden multiple hits and homoplasy.

---

## Slide 3: The UPGMA Algorithm

```text
Topic: Unweighted Pair Group Method with Arithmetic Mean (Sokal & Michener, 1958)

  UPGMA In a Nutshell:
  1. Find the smallest distance d(A, B) in distance matrix.
  2. Cluster A and B into a composite node (AB).
  3. Set node height h(AB) = d(A, B) / 2.
  4. Recalculate average distance from (AB) to all remaining taxa.
  5. Repeat until all taxa are merged into the root.
```

**Speaker Talking Points:**  
* UPGMA is the simplest, most intuitive distance-based clustering algorithm.
* It produces an **Ultrametric Tree** where all tips are equidistant from the root.

---

## Slide 4: The Fatal Flaw of UPGMA: The Molecular Clock Assumption

```text
Topic: When Rates Differ, UPGMA Produces Wrong Topologies!

[Visual: Unequal evolutionary rates:
  Lineage A evolves 5x faster than B and C.
  UPGMA incorrectly clusters B and C together first, corrupting the tree!]
```

**Speaker Talking Points:**  
* UPGMA assumes a constant, uniform rate of evolution across all lineages (strict molecular clock).
* In biology, rodents evolve faster than primates; viruses mutate faster than hosts.
* When rate constancy is violated, UPGMA is guaranteed to output the WRONG tree!

---

## Slide 5: The Neighbor-Joining (NJ) Algorithm

```text
Topic: Saitou & Nei's Nobel-Caliber Solution (1987)

[Visual: Star Decomposition:
  Step 1: Start with all taxa radiating from a single central star node.
  Step 2: Calculate transformed Q-matrix (subtracts total divergence of each taxon).
  Step 3: Pair the two taxa that minimize Q(i, j) into a new internal branch.
  Step 4: Repeat until fully resolved into an unrooted bifurcating tree!]
```

**Speaker Talking Points:**  
* Neighbor-Joining does NOT assume a molecular clock.
* Lineages can have completely different branch lengths (accommodates fast and slow evolvers).
* Extremely fast: $\mathcal{O}(N^3)$, runs in seconds for hundreds of taxa.

---

## Slide 6: Character-Based: Maximum Parsimony (MP)

```text
Topic: Occam's Razor in Phylogenetics

  Principle:
  "The tree topology requiring the MINIMUM total number of evolutionary mutational
   steps to explain the observed alignment is the best tree."

[Visual: Evaluating two alternative tree topologies across an informative column:
  Topology 1 requires 1 mutation: A -> G. (Parsimony score = 1) [WINNER!]
  Topology 2 requires 2 independent mutations: A -> G and A -> G. (Score = 2)]
```

**Speaker Talking Points:**  
* Maximum Parsimony evaluates informative columns without relying on pairwise distances.
* Weakness: Long-Branch Attraction (LBA) can mislead parsimony on divergent sequences.

---

## Slide 7: Probabilistic Methods: Maximum Likelihood (ML)

```text
Topic: Ronald Fisher's Statistical Framework Applied to Phylogeny

Formula:
  Likelihood L = P( Multiple Alignment | Tree Topology, Substitution Model )
```

**Speaker Talking Points:**  
* Maximum Likelihood finds the tree topology and branch lengths that maximize the
  probability of observing the actual sequence data.
* Explicitly incorporates substitution models (JC69, K2P, GTR, WAG) and rate variation (+Gamma).
* Statistically robust, but computationally intensive: requires searching tree space.

---

## Slide 8: Summary & Comparison of Methods

```text
Topic: Which Method to Choose?

+---------------+--------------------+--------------------+-------------------+
| Method        | Underlying Model   | Computational Speed| Key Limitation    |
+---------------+--------------------+--------------------+-------------------+
| **UPGMA**     | Strict Mol. Clock  | Extremely Fast     | Assumes clock     |
| **NJ**        | Variable rates     | Fast: O(N^3)       | Condenses data    |
| **Parsimony** | Occam's Razor      | Moderate           | Long-Branch Attract|
| **ML**        | Full Probabilistic | Slow (Hours/Days)  | High compute cost |
+---------------+--------------------+--------------------+-------------------+
```

**Speaker Talking Points:**  
* In practice: use Neighbor-Joining for preliminary exploration; use Maximum Likelihood
  or Bayesian methods (MrBayes) for final publication.

