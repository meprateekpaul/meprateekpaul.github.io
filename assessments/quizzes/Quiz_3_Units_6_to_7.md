# Quiz 3: Units 6–7 — Multiple Sequence Alignment & Molecular Phylogenetics

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Units Covered:** Unit 6 (Multiple Sequence Alignment), Unit 7 (Phylogenetic Analysis)  
**Time Allowed:** 15 Minutes  
**Maximum Marks:** 10 Marks  
**Nature of Examination:** Closed Book, Individual Assessment  

---

## Part I: Student Test Paper

### Instructions to Candidates
1. Answer all questions directly on this paper.
2. State assumptions and definitions clearly where requested.
3. Manage your time effectively (approx. 1.5 minutes per mark).

---

### Question 1: Multiple Choice Concept Checks (4 Marks)

**(a)** What is the primary role of the "guide tree" in progressive multiple sequence alignment algorithms like ClustalW? `[1 Mark]`  
[  ] A) To establish the definitive evolutionary species phylogeny  
[  ] B) To determine the mathematical order in which sequences and profiles are progressively merged  
[  ] C) To calculate the molecular weight of the protein  
[  ] D) To predict the 3D crystal structure coordinates  

**(b)** What is the major inherent algorithmic flaw of progressive alignment heuristics? `[1 Mark]`  
[  ] A) It runs in exponential $O(2^N)$ time  
[  ] B) "Once a gap, always a gap" — errors introduced in early pairwise alignments cannot be corrected when distant sequences are added later  
[  ] C) It cannot align sequences longer than 50 residues  
[  ] D) It requires all sequences to share 100% identity  

**(c)** In molecular phylogenetics, homologous genes in different species that diverged as a direct consequence of a **speciation event** are termed: `[1 Mark]`  
[  ] A) Paralogues  
[  ] B) Orthologues  
[  ] C) Xenologues  
[  ] D) Analogues  

**(d)** Which tree-building method assumes a strict molecular clock (constant evolutionary rate across all branches), producing an ultrametric tree? `[1 Mark]`  
[  ] A) Neighbor-Joining (NJ)  
[  ] B) Maximum Likelihood (ML)  
[  ] C) UPGMA  
[  ] D) Maximum Parsimony (MP)  

---

### Question 2: Parsimony-Informative Site Identification (3 Marks)

Examine the following 4-taxon nucleotide alignment of three columns:

```text
Site:       1   2   3
Taxon 1:    A   C   G
Taxon 2:    A   C   T
Taxon 3:    A   G   G
Taxon 4:    T   G   C
```

For each site, state whether it is **Invariant**, **Uninformative (variable / autapomorphic)**, or **Parsimony-Informative**, providing a 1-line justification for your classification:

* **Site 1:** `____________________________________________________________________________________________________`  
* **Site 2:** `____________________________________________________________________________________________________`  
* **Site 3:** `____________________________________________________________________________________________________`  

---

### Question 3: Bootstrap Analysis Interpretation (3 Marks)

A researcher constructs a phylogenetic tree of five mammalian species. The resulting consensus tree displays the following internal topology:

```text
+-- Opossum (Outgroup)
|
`--+ (Node 1, Bootstrap = 100%)
   |-- Mouse
   `--+ (Node 2, Bootstrap = 94%)
      |-- Chimpanzee
      `-- Human
```

1. What is the operational procedure used to generate bootstrap replicates from an alignment? `[1 Mark]`  
2. What does the bootstrap value of **94%** at Node 2 indicate regarding the evolutionary relationship between Human and Chimpanzee? `[2 Marks]`  

---
---

## Part II: Instructor Answer Key & Marking Scheme

### Question 1: Multiple Choice Answers (4 Marks)
* **(a)** **B) To determine the mathematical order in which sequences and profiles are progressively merged** `[1 Mark]`  
  *Rationale:* The guide tree dictates clustering order (leaves to root). It is not an authentic phylogenetic tree.
* **(b)** **B) "Once a gap, always a gap" — errors introduced in early alignments cannot be corrected later** `[1 Mark]`  
  *Rationale:* Progressive alignment is a greedy heuristic that freezes gaps once placed.
* **(c)** **B) Orthologues** `[1 Mark]`  
  *Rationale:* Orthologues arise via speciation; paralogues arise via gene duplication within a genome.
* **(d)** **C) UPGMA** `[1 Mark]`  
  *Rationale:* UPGMA assumes equal evolutionary rates (ultrametricity). Neighbor-Joining allows unequal rates.

---

### Question 2: Parsimony-Informative Site Identification (3 Marks)

* **Criterion:** A site is parsimony-informative if and only if it has at least two different character states, each occurring in at least two separate taxa.
* **Model Answer & Marking:**
  * **Site 1 (`A, A, A, T`):** **Uninformative (Variable / Autapomorphic)** `[1 Mark]`  
    *Justification:* Nucleotide `T` appears in only one taxon (Taxon 4); a single mutation on Taxon 4 explains this site on all possible trees.
  * **Site 2 (`C, C, G, G`):** **Parsimony-Informative** `[1 Mark]`  
    *Justification:* Contains two character states (`C` and `G`), each appearing exactly twice (Taxa 1 & 2 have `C`; Taxa 3 & 4 have `G`), supporting the grouping $(T_1, T_2)$ vs $(T_3, T_4)$.
  * **Site 3 (`G, T, G, C`):** **Uninformative** `[1 Mark]`  
    *Justification:* Contains three character states (`G, T, C`), but only `G` appears twice; `T` and `C` occur only once each. No partition of two states appearing $\ge 2$ times exists.

---

### Question 3: Bootstrap Analysis Interpretation (3 Marks)

* **1. Bootstrap Generation Procedure (1 Mark):**  
  Columns from the original multiple sequence alignment are randomly resampled **with replacement** to generate hundreds or thousands of pseudo-replicate alignments of equal length, from which replicate trees are reconstructed.
* **2. Interpretation of 94% at Node 2 (2 Marks):**  
  * Across 94% of the resampled pseudo-replicate trees, Human and Chimpanzee clustered together as an exclusive monophyletic clade to the exclusion of other taxa.  
  * In phylogenetic standards, a bootstrap score $\ge 90\text{--}95\%$ represents **statistically strong, robust evidence** that Human and Chimpanzee are sister taxa relative to Mouse and Opossum.
