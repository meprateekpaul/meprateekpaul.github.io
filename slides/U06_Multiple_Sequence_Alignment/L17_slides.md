---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 17 Slides: Progressive Alignment and Tools"
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
# Lecture 17 — Progressive Alignment and Tools
### Concepts of Bioinformatics (CBBI-501)
**Unit 06:** Multiple Sequence Alignment  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Progressive Alignment Paradigm

```text
Topic: Feng & Doolittle's Heuristic Revolution (1987)

[Visual: 3-Stage Pipeline Diagram:
  Stage 1: All-against-all Pairwise Alignments -> Distance Matrix
  Stage 2: Guide Tree Construction (UPGMA / Neighbor-Joining)
  Stage 3: Progressive Profile Merging from Leaves to Root]
```

**Speaker Talking Points:**  
* Since exact multi-dimensional dynamic programming is NP-complete, we need a fast heuristic.
* Da-Fei Feng and Russell Doolittle proposed **Progressive Alignment**:
  Align the most similar sequences first, freeze them into consensus profiles,
  and progressively merge more distant sequences following a branching tree.

---

## Slide 2: Step 1 & 2: Pairwise Distances and the Guide Tree

```text
Topic: Determining the Order of Alignment

  Step 1: Compute All Pairwise Distances
  * For N sequences, run (N choose 2) standard Needleman-Wunsch alignments.
  * Convert similarity scores into an evolutionary distance matrix D.

  Step 2: Construct the Guide Tree
  * Apply a clustering algorithm (UPGMA or Neighbor-Joining).
  * Group the most closely related sequences together into the lowest branches.
```

**Speaker Talking Points:**  
* CRITICAL DISTINCTION: A **Guide Tree** is NOT an authentic phylogenetic tree!
* Its sole computational function is to dictate the sequential order of profile merging.

---

## Slide 3: Step 3: Progressive Profile Merging

```text
Topic: Merging Alignments at Tree Vertices

[Visual: Tree traversal from leaves to root:
  Leaf 1: HBB_HUMAN \
                     >-- Align pair -> Create Profile A
  Leaf 2: HBB_CHIMP /                                    \
                                                          >-- Merge Profile A & B
  Leaf 3: HBD_HUMAN \                                    /    into final Master MSA
                     >-- Align pair -> Create Profile B /
  Leaf 4: HBG_HUMAN /]
```

**Speaker Talking Points:**  
* Sequence-to-Sequence: Align two raw sequences.
* Sequence-to-Profile: Align a new sequence against an existing multi-sequence profile.
* Profile-to-Profile: Merge two independent multi-sequence profiles together.

---

## Slide 4: The Fatal Flaw: "Once a Gap, Always a Gap"

```text
Topic: Error Propagation in Progressive Alignment

[Visual: Propagation of an early mistake:
  Step 1: Low-level noise introduces an erroneous gap in HBB_CHIMP.
  Step 2: Profile A is FROZEN: gap cannot be moved or closed!
  Step 3: All subsequent additions (HBD, HBG, MB) are forced to align around
          the erroneous gap, corrupting the entire master alignment!]
```

**Speaker Talking Points:**  
* Progressive alignment is **greedy**: decisions made at early steps are permanent.
* If a gap is placed in an incorrect position early on, that error propagates
  all the way to the root without any opportunity for correction.

---

## Slide 5: The Classic Benchmark: ClustalW

```text
Topic: Thompson, Higgins & Gibson (1994)

  Innovations in ClustalW:
  1. Sequence Weighting: Down-weights redundant sequences (e.g. 50 human globins)
     so they do not bias profile consensus scores.
  2. Position-Specific Gap Penalties:
     * Discourages gaps inside hydrophobic core regions.
     * Encourages gaps in flexible hydrophilic loop regions.
     * Prevents gaps from opening closer than 8 residues apart.
```

**Speaker Talking Points:**  
* ClustalW is the historical standard named in your university syllabus.
* Today, ClustalW is superseded because its $O(N^2)$ pairwise step cannot scale.

---

## Slide 6: Modern Algorithmic Champions: MUSCLE and MAFFT

```text
Topic: Overcoming the Progressive Flaw

1. MUSCLE (Robert Edgar, 2004) — Iterative Refinement:
   * Builds an initial progressive alignment.
   * Then cuts the guide tree edges, splits the alignment into two halves,
     and re-aligns them. If the SP score improves, keeps the new alignment!
   * Completely eliminates the "once a gap, always a gap" trap!

2. MAFFT (Kazutaka Katoh, 2002) — Fast Fourier Transform:
   * Uses Fast Fourier Transform (FFT) on amino acid physicochemical properties.
   * Identifies homologous blocks at lightning speed; scales to 50,000 sequences.
```

**Speaker Talking Points:**  
* MUSCLE and MAFFT are the current gold standards for accuracy and speed.

---

## Slide 7: High-Accuracy and Ultra-Scale Tools: T-Coffee & Clustal Omega

```text
Topic: The Specialists

+------------------+-------------------------+--------------------------------+
| Tool             | Core Innovation         | Best Use Case                  |
+------------------+-------------------------+--------------------------------+
| **T-Coffee**     | Consistency-based library| Highest accuracy on difficult  |
|                  | (merges global + local) | alignments (<100 sequences)    |
| **Clustal Omega**| mBed fast distance calc | Ultra-scale massive alignments |
|                  | and HMM-profile trees   | (>10,000 to 100,000 sequences) |
+------------------+-------------------------+--------------------------------+
```

**Speaker Talking Points:**  
* T-Coffee sacrifices speed for maximum accuracy.
* Clustal Omega scales to hundreds of thousands of sequences using HMM profiles.

---

## Slide 8: Summary & Practical Recommendations

```text
Topic: Choosing Your MSA Tool in the Lab

* For routine day-to-day alignments (<500 sequences): **MUSCLE** or **MAFFT**.
* For massive genomic/viral datasets (>5,000 sequences): **Clustal Omega** or **MAFFT-FFT**.
* For hard, distantly related proteins (<25% identity): **T-Coffee** or structural alignment.
* Next Unit: Phylogenetic Analysis — Nodes, branches, orthologues vs paralogues,
  and constructing trees!
```

