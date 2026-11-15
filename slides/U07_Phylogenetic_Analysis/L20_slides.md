---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 20 Slides: Evaluating Trees and Bootstrap"
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
# Lecture 20 — Evaluating Trees and Bootstrap
### Concepts of Bioinformatics (CBBI-501)
**Unit 07:** Phylogenetic Analysis  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Tree Evaluation Dilemma

```text
Topic: When Algorithms Always Output an Answer

[Visual: A tree-building algorithm fed random junk characters -> Outputs a bifurcating tree!
         Question: How do we know which internal branches represent genuine evolutionary history
         and which are artifacts of noisy data?]
```

**Speaker Talking Points:**  
* Any phylogenetic algorithm will produce *a* tree from any input matrix, even if the
  underlying data is complete nonsense.
* Building a tree is only half the task; the critical scientific requirement is
  **evaluating statistical confidence** in each internal clade.

---

## Slide 2: The Non-Parametric Bootstrap (Felsenstein, 1985)

```text
Topic: Resampling the Multiple Sequence Alignment

[Visual: Original Alignment (Columns 1 to C)
         -> Resample Columns WITH REPLACEMENT
         -> Pseudo-Replicate Alignment 1 (Some columns repeated, ~37% omitted)
         -> Reconstruct Tree 1]
```

**Speaker Talking Points:**  
* In 1985, Joseph Felsenstein adapted Bradley Efron's bootstrap technique to phylogenetics.
* If a clade is genuinely supported by authentic evolutionary signal, it will be supported
  by many independent columns and survive random column resampling.

---

## Slide 3: Resampling with Replacement Mechanics

```text
Topic: The Mathematics of Column Drawing

  Original Alignment:  [ Col 1 | Col 2 | Col 3 | Col 4 | Col 5 | Col 6 ]

  Bootstrap Replicate 1:
  Drawn: Col 2, Col 2, Col 3, Col 5, Col 5, Col 6
  (Col 1 and Col 4 were OMITTED; Col 2 and Col 5 were DUPLICATED!)

  Mathematical Fact:
  As length C -> infinity, the probability that any specific column is OMITTED is:
    (1 - 1/C)^C ≈ 1/e ≈ 36.8%
  Each replicate contains approximately 63.2% of the original unique columns!
```

**Speaker Talking Points:**  
* The pseudo-replicate has the exact same dimensions ($N \times C$) as the original alignment.

---

## Slide 4: Building the Replicate Tree Forest

```text
Topic: Repeating the Process B Times

  Workflow:
  1. Generate B = 1,000 pseudo-replicate alignments.
  2. Reconstruct 1,000 independent phylogenetic trees using the SAME tree-building method.
  3. Compare all 1,000 trees against the original topology.
  4. For every internal node, count: "In how many of the 1,000 trees does this clade appear?"
```

**Speaker Talking Points:**  
* If a clade appears in 950 out of 1,000 replicate trees, its bootstrap value is **95%**.
* Standard publication standards require at least $B = 1,000$ replicates.

---

## Slide 5: Consensus Trees: Strict vs Majority-Rule

```text
Topic: Synthesizing the Forest into a Single Tree

1. Strict Consensus:
   * Retains an internal branch ONLY if it appears in 100% of all bootstrap trees.
   * Highly conservative; often collapses trees into unresolved star polytomies.

2. Majority-Rule (50%) Consensus:
   * Retains internal branches that appear in MORE THAN 50% of bootstrap trees.
   * Annotates internal nodes with their percentage support (50% to 100%).
```

**Speaker Talking Points:**  
* In scientific publications, the majority-rule consensus tree is the standard visual output.

---

## Slide 6: Interpreting Bootstrap Support Percentages

```text
Topic: What the Numbers Actually Mean

+-------------------------+---------------------------------------------------+
| Bootstrap Value         | Scientific Interpretation                         |
+-------------------------+---------------------------------------------------+
| **>= 90% (or >= 95%)**  | Strongly supported clade; high confidence         |
| **70% to 89%**          | Moderately supported; biological hypothesis viable|
| **< 70%**               | WEAK / UNRESOLVED; should be collapsed to polytomy|
+-------------------------+---------------------------------------------------+
```

**Speaker Talking Points:**  
* WHAT IT MEANS: Measures the sensitivity of a clade to random character sampling.
* WHAT IT DOES NOT MEAN: A 95% bootstrap is NOT the probability that the clade is true!
  Systematic biases (e.g. Long-Branch Attraction) can yield 100% bootstrap support for the WRONG tree!

---

## Slide 7: Standard Tree File Formats: Newick & NEXUS

```text
Topic: Storing Graph Topologies in Text

Newick Format (Parentheses Notation):
  ((HBB_HUMAN:0.005,HBB_CHIMP:0.005)99:0.035,HBD_HUMAN:0.040)100:0.610;

  * Semicolon `;` terminates the tree string.
  * Colons `:` precede branch lengths.
  * Numbers after closing parentheses represent Bootstrap Support Percentages (e.g. `99`).

NEXUS Format:
  * Modular block structure (`#NEXUS`, `BEGIN TAXA;`, `BEGIN CHARACTERS;`, `BEGIN TREES;`).
```

**Speaker Talking Points:**  
* Newick format is universal: supported by MEGA, FigTree, iTOL, and Python Biopython.

---

## Slide 8: The Phylogenetic Software Landscape

```text
Topic: Tools for the Bioinformatician

1. MEGA (Molecular Evolutionary Genetics Analysis):
   * Comprehensive, user-friendly desktop GUI. Ideal for undergraduate education.
2. PHYLIP (Phylogeny Inference Package — Felsenstein):
   * Classic command-line suite: `dnadist`, `protpars`, `neighbor`, `consense`.
3. High-Performance Maximum Likelihood:
   * **PhyML**, **RAxML**, **IQ-TREE** (fast, scalable to thousands of taxa).
4. Bayesian Inference:
   * **MrBayes** (computes posterior probabilities via MCMC).
5. Visualization:
   * **iTOL (Interactive Tree of Life)** and **FigTree**.
```

**Speaker Talking Points:**  
* Capstone of Units 5–7: From pairwise alignment, to MSA, to robust phylogenetic trees!

