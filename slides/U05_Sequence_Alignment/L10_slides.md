---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 10 Slides: Biological Basis and Dot Plots"
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
# Lecture 10 — Biological Basis and Dot Plots
### Concepts of Bioinformatics (CBBI-501)
**Unit 05:** Sequence Alignment and Database Searching  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Why Align Biological Sequences?

```text
Topic: The Rosetta Stone of Molecular Biology

[Visual: Two aligned protein strings showing conserved residues (*) and mutations (: .)
  HBB_HUMAN   VHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFESFGDLSTPDAVMGNPK
              |||||:||:|| |||||||||| ||||||||||||||||||||||||||:|||||||||
  HBB_CHIMP   VHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFESFGDLSSPDAVMGNPK]
```

**Speaker Talking Points:**  
* Sequence alignment is the single most fundamental algorithm in bioinformatics.
* Primary sequences are evolutionary tapes: mutations accumulate over millions of years.
* Alignment places homologous residues into equivalent vertical columns to reveal
  functional constraints, catalytic active sites, and phylogenetic history.

---

## Slide 2: Homology vs Similarity vs Identity

```text
Topic: Clarifying the Most Abused Vocabulary in Biology

+--------------------+-------------------------+------------------------------+
| Term               | Nature of Definition    | Quantifiability              |
+--------------------+-------------------------+------------------------------+
| **Identity**       | Mathematical Fact       | Exact percentage (e.g. 78%)  |
| **Similarity**     | Physicochemical Score   | Metric from scoring matrix   |
| **Homology**       | Evolutionary Hypothesis | **BINARY**: Yes or No!       |
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* Two sequences are either homologous (descended from a common ancestor) or they are not.
* It is biologically nonsensical to state: "these genes are 70% homologous"!
* Correct phrasing: "These sequences share 70% identity and are inferred to be homologous."

---

## Slide 3: The Tree of Homology: Orthologues, Paralogues, Xenologues

```text
Topic: How Homologous Genes Arise

                     Ancestral Globin Gene
                               |
               [Gene Duplication Event: ~500 Mya]
                               |
            +------------------+------------------+
            |                                     |
       Alpha-Globin                          Beta-Globin
            |                                     |
    [Speciation Event]                    [Speciation Event]
     (Human vs Mouse)                      (Human vs Mouse)
      /           \                         /           \
Human Alpha    Mouse Alpha           Human Beta      Mouse Beta
```

**Speaker Talking Points:**  
* **Orthologues:** Genes separated by a **speciation event** (Human Beta vs Mouse Beta).
  Usually retain identical biological function.
* **Paralogues:** Genes separated by a **gene duplication event** (Human Alpha vs Human Beta).
  Often evolve new functions (neo-functionalization) or split tasks (sub-functionalization).
* **Xenologues:** Genes acquired through **horizontal gene transfer (HGT)**.

---

## Slide 4: Mutational Mechanisms: Substitutions and Indels

```text
Topic: How Sequences Diverge

1. Substitutions (Point Mutations):
   * Transitions: Purine <-> Purine (A <-> G) or Pyrimidine <-> Pyrimidine (C <-> T).
   * Transversions: Purine <-> Pyrimidine (e.g., A <-> T in HbS Glu6Val!).
   * Evolutionary constraint: Transitions are biochemically ~2x more frequent than transversions.

2. Indels (Insertions and Deletions):
   * Caused by DNA replication slippage or unequal recombination.
   * In coding exons, indels that are not multiples of 3 cause catastrophic frameshifts.
   * In sequence alignments, indels are represented as gap characters (`-`).
```

**Speaker Talking Points:**  
* Alignments must penalize indels because creating an insertion/deletion disrupts
  the reading frame and macromolecular backbone geometry.

---

## Slide 5: The First Visual Alignment: The Dot Plot

```text
Topic: 2D Matrix Visualization (Gibbs & McIntyre, 1970)

  Sequence 2 ->  V   H   L   T   P   E
  Sequence 1 v
      V          *
      H              *
      L                  *
      T                      *
      P                          *
      E                              *
```

**Speaker Talking Points:**  
* A 2D grid where Sequence 1 labels the rows and Sequence 2 labels the columns.
* In the simplest dot plot, place a dot at position $(i, j)$ if residue $S_1[i] == S_2[j]$.
* Perfect identity produces an unbroken diagonal line from top-left to bottom-right.

---

## Slide 6: Filtering Noise: Window Size (w) and Stringency (s)

```text
Topic: Eliminating Spurious Random Matches

[Visual: Unfiltered Dot Plot (solid field of random dots)
         vs Filtered Window Dot Plot (crisp, clean diagonal lines)]

Algorithm:
  A dot is plotted at the center of window `w` ONLY if at least `s` residues match!
  Example: Window = 5, Stringency = 4 (at least 4 out of 5 residues must match).
```

**Speaker Talking Points:**  
* In large sequences, individual amino acids match by random chance (1 in 20).
* A sliding window calculates local similarity, suppressing random background noise
  while preserving significant evolutionary signals.

---

## Slide 7: Interpreting Biological Patterns in Dot Plots

```text
Topic: Diagnostic Geometric Signatures

+-------------------------+---------------------------------------------------+
| Visual Pattern          | Biological / Evolutionary Phenomenon              |
+-------------------------+---------------------------------------------------+
| Unbroken main diagonal  | Complete, continuous sequence identity            |
| Parallel shifted line   | Direct tandem repeat or internal gene duplication |
| Horizontal gap/shift    | Insertion in Sequence 2 (or deletion in Seq 1)    |
| Vertical gap/shift      | Insertion in Sequence 1 (or deletion in Seq 2)    |
| Anti-diagonal (X-shape) | Genomic inversion (reverse-complement match)      |
+-------------------------+---------------------------------------------------+
```

**Speaker Talking Points:**  
* Dot plots are unbeatable for rapid visual discovery of large-scale genomic rearrangements.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 10

* Alignment reflects evolutionary descent with modification.
* Homology is binary; similarity and identity are quantifiable measurements.
* Orthologues diverge by speciation; paralogues diverge by duplication.
* Dot plots provide the first 2D visual map of sequence relationships.
* Next Lecture: Optimal Global Alignment — The Needleman-Wunsch algorithm worked
  by hand step by step!
```

