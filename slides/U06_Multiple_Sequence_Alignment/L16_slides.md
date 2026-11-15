---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 16 Slides: Principles of Multiple Alignment"
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
# Lecture 16 — Principles of Multiple Alignment
### Concepts of Bioinformatics (CBBI-501)
**Unit 06:** Multiple Sequence Alignment  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: From Pairwise to Multiple Alignment

```text
Topic: The Power of N Sequences

[Visual: Pairwise alignment (sparse, ambiguous matches)
         vs 10-sequence MSA showing an invariant vertical column:
  HBA_HUMAN   ... K V G A H A G E Y G A E A ...
  HBB_HUMAN   ... K V N - V D E V G G E A L ...
  HBD_HUMAN   ... K V N - V D A V G G E A L ...
  HBG1_HUMAN  ... K V N - V E D A G G E T L ...
  MB_HUMAN    ... K V E - A D I P G H G Q E ...
                          ^ (Invariant catalytic core!)]
```

**Speaker Talking Points:**  
* Pairwise alignment compares two sequences; Multiple Sequence Alignment (MSA)
  aligns $N$ sequences ($N \ge 3$) simultaneously.
* An MSA is an evolutionary consensus tape: individual noise cancels out,
  revealing invariant active-site residues, secondary structures, and ancestral motifs.

---

## Slide 2: What an MSA Reveals That Pairwise Cannot

```text
Topic: Biological Insights from Multi-Sequence Profiles

+-------------------------+---------------------------------------------------+
| Feature Revealed by MSA | Biological Meaning & Application                  |
+-------------------------+---------------------------------------------------+
| Invariant Columns       | Essential catalytic or structural residues        |
| Conservative Positions  | Hydrophobic core vs surface-exposed tolerance     |
| Indel Boundaries        | Flexible loop regions tolerating insertions       |
| Consensus Motifs        | PROSITE patterns, signature fingerprints          |
| Phylogenetic Signal     | Informative characters for tree reconstruction    |
+-------------------------+---------------------------------------------------+
```

**Speaker Talking Points:**  
* Two sequences sharing 30% identity look mostly ambiguous.
* Adding 20 diverse homologs reveals which 30% of positions are strictly conserved!

---

## Slide 3: Structural vs Evolutionary Alignment

```text
Topic: The Two Defining Paradigms of Alignment

1. Structural Alignment (The Gold Standard):
   * Aligns residues whose C_alpha coordinates superimpose in 3D physical space.
   * Based on Cartesian geometry (RMSD, DALI, CE), NOT sequence identity.
   * Structures diverge 3-10x slower than primary sequence.

2. Evolutionary Sequence Alignment:
   * Aligns residues inferred to share common ancestry based on sequence scores.
   * In the "Twilight Zone" (<25% identity), sequence alignment frequently places
     gaps inside rigid alpha-helices, violating physical structural reality!
```

**Speaker Talking Points:**  
* When 3D experimental structures exist, structural alignment is always authoritative.

---

## Slide 4: The Mathematical Objective: Sum-of-Pairs (SP)

```text
Topic: Scoring a Multi-Sequence Alignment

[Visual: A single alignment column containing 4 residues:
  Seq 1: H
  Seq 2: H       Compute all (4 choose 2) = 6 pairwise combinations!
  Seq 3: Y       SP_column = s(H,H) + s(H,Y) + s(H,H) + s(H,Y) + s(H,H) + s(Y,H)
  Seq 4: H]

Formula:
  SP_Score = Sum_columns [ Sum_{i < j} s(m_{i, k}, m_{j, k}) ]
```

**Speaker Talking Points:**  
* The Sum-of-Pairs score evaluates every column as the sum of all pairwise substitution scores.
* Maximizing the global SP score is the standard mathematical definition of optimal MSA.

---

## Slide 5: The Curse of Dimensionality

```text
Topic: Dynamic Programming in N Dimensions

  Pairwise Alignment (N = 2):
  * 2D Matrix of size (L x L).
  * 3 incoming routes per cell (Diag, Up, Left): O(L^2).

  N-Sequence Alignment:
  * N-Dimensional hypercube lattice of size (L^N).
  * Number of incoming routes per cell: (2^N - 1).
  * Complexity: O(2^N * L^N).
```

**Speaker Talking Points:**  
* For 5 sequences of length 300: 300^5 = 2.43 x 10^12 cells (compute-heavy).
* For 10 sequences of length 300: 300^10 = 5.9 x 10^24 cells (COMPUTATIONALLY IMPOSSIBLE!).

---

## Slide 6: The NP-Completeness of Exact MSA

```text
Topic: Wang & Jiang's Mathematical Proof (1994)

  Theorem (Wang & Jiang, 1994):
  "The problem of computing the optimal Multiple Sequence Alignment
   under the Sum-of-Pairs scoring function with affine gap penalties
   is NP-COMPLETE."
```

**Speaker Talking Points:**  
* NP-complete means there is no known polynomial-time algorithm to solve it.
* Exact dynamic programming for large $N$ will never run on any supercomputer.
* This mathematical reality forces bioinformatics to use **Heuristic Approximations**.

---

## Slide 7: The Heuristic Spectrum: Progressive vs Iterative

```text
Topic: How Modern Tools Solve the Problem

1. Progressive Alignment (Feng-Doolittle):
   * Build pairwise distances -> Guide Tree -> Progressively merge sequences.
   * Extremely fast, but suffers from early error trapping ("Once a gap, always a gap").
   * Examples: ClustalW, Clustal Omega.

2. Iterative Refinement:
   * Re-aligns sub-clusters repeatedly to fix early mistakes and optimize SP score.
   * Examples: MUSCLE, MAFFT.

3. Consistency-Based:
   * Merges global and local pairwise information before guide tree assembly.
   * Example: T-Coffee.
```

**Speaker Talking Points:**  
* We trade mathematical perfection for practical, high-accuracy biological solutions.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 16

* MSA transforms individual sequences into evolutionary and functional profiles.
* Structural alignment superimposes 3D coordinates; sequence alignment infers homology.
* Sum-of-Pairs (SP) scores every column across all pairwise combinations.
* Exact MSA is NP-complete, requiring heuristic approximations.
* Next Lecture: Progressive Alignment, Guide Trees, and Modern Tools (Clustal, MUSCLE, MAFFT).
```

