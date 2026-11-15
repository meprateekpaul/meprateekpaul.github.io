# Lecture 20 — Evaluating Trees and Bootstrap

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 7:** Phylogenetic Analysis  
**Syllabus Topic:** Tree building and tree evaluation, Phylogenetic software  
**Primary Learning Outcome:** LO5 — Evaluate phylogenetic trees, perform bootstrap resampling analysis, interpret support values, and navigate phylogenetic software (MEGA, PHYLIP, iTOL).

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Tree Evaluation Dilemma
================================================================================
Topic: When Algorithms Always Output an Answer

[Visual: A tree-building algorithm fed random junk characters -> Outputs a bifurcating tree!
         Question: How do we know which internal branches represent genuine evolutionary history
         and which are artifacts of noisy data?]

Speaker Bullets:
* Any phylogenetic algorithm will produce *a* tree from any input matrix, even if the
  underlying data is complete nonsense.
* Building a tree is only half the task; the critical scientific requirement is
  **evaluating statistical confidence** in each internal clade.
```

```
================================================================================
SLIDE 2: The Non-Parametric Bootstrap (Felsenstein, 1985)
================================================================================
Topic: Resampling the Multiple Sequence Alignment

[Visual: Original Alignment (Columns 1 to C)
         -> Resample Columns WITH REPLACEMENT
         -> Pseudo-Replicate Alignment 1 (Some columns repeated, ~37% omitted)
         -> Reconstruct Tree 1]

Speaker Bullets:
* In 1985, Joseph Felsenstein adapted Bradley Efron's bootstrap technique to phylogenetics.
* If a clade is genuinely supported by authentic evolutionary signal, it will be supported
  by many independent columns and survive random column resampling.
```

```
================================================================================
SLIDE 3: Resampling with Replacement Mechanics
================================================================================
Topic: The Mathematics of Column Drawing

  Original Alignment:  [ Col 1 | Col 2 | Col 3 | Col 4 | Col 5 | Col 6 ]

  Bootstrap Replicate 1:
  Drawn: Col 2, Col 2, Col 3, Col 5, Col 5, Col 6
  (Col 1 and Col 4 were OMITTED; Col 2 and Col 5 were DUPLICATED!)

  Mathematical Fact:
  As length C -> infinity, the probability that any specific column is OMITTED is:
    (1 - 1/C)^C ≈ 1/e ≈ 36.8%
  Each replicate contains approximately 63.2% of the original unique columns!

Speaker Bullets:
* The pseudo-replicate has the exact same dimensions ($N \times C$) as the original alignment.
```

```
================================================================================
SLIDE 4: Building the Replicate Tree Forest
================================================================================
Topic: Repeating the Process B Times

  Workflow:
  1. Generate B = 1,000 pseudo-replicate alignments.
  2. Reconstruct 1,000 independent phylogenetic trees using the SAME tree-building method.
  3. Compare all 1,000 trees against the original topology.
  4. For every internal node, count: "In how many of the 1,000 trees does this clade appear?"

Speaker Bullets:
* If a clade appears in 950 out of 1,000 replicate trees, its bootstrap value is **95%**.
* Standard publication standards require at least $B = 1,000$ replicates.
```

```
================================================================================
SLIDE 5: Consensus Trees: Strict vs Majority-Rule
================================================================================
Topic: Synthesizing the Forest into a Single Tree

1. Strict Consensus:
   * Retains an internal branch ONLY if it appears in 100% of all bootstrap trees.
   * Highly conservative; often collapses trees into unresolved star polytomies.

2. Majority-Rule (50%) Consensus:
   * Retains internal branches that appear in MORE THAN 50% of bootstrap trees.
   * Annotates internal nodes with their percentage support (50% to 100%).

Speaker Bullets:
* In scientific publications, the majority-rule consensus tree is the standard visual output.
```

```
================================================================================
SLIDE 6: Interpreting Bootstrap Support Percentages
================================================================================
Topic: What the Numbers Actually Mean

+-------------------------+---------------------------------------------------+
| Bootstrap Value         | Scientific Interpretation                         |
+-------------------------+---------------------------------------------------+
| **>= 90% (or >= 95%)**  | Strongly supported clade; high confidence         |
| **70% to 89%**          | Moderately supported; biological hypothesis viable|
| **< 70%**               | WEAK / UNRESOLVED; should be collapsed to polytomy|
+-------------------------+---------------------------------------------------+

Speaker Bullets:
* WHAT IT MEANS: Measures the sensitivity of a clade to random character sampling.
* WHAT IT DOES NOT MEAN: A 95% bootstrap is NOT the probability that the clade is true!
  Systematic biases (e.g. Long-Branch Attraction) can yield 100% bootstrap support for the WRONG tree!
```

```
================================================================================
SLIDE 7: Standard Tree File Formats: Newick & NEXUS
================================================================================
Topic: Storing Graph Topologies in Text

Newick Format (Parentheses Notation):
  ((HBB_HUMAN:0.005,HBB_CHIMP:0.005)99:0.035,HBD_HUMAN:0.040)100:0.610;

  * Semicolon `;` terminates the tree string.
  * Colons `:` precede branch lengths.
  * Numbers after closing parentheses represent Bootstrap Support Percentages (e.g. `99`).

NEXUS Format:
  * Modular block structure (`#NEXUS`, `BEGIN TAXA;`, `BEGIN CHARACTERS;`, `BEGIN TREES;`).

Speaker Bullets:
* Newick format is universal: supported by MEGA, FigTree, iTOL, and Python Biopython.
```

```
================================================================================
SLIDE 8: The Phylogenetic Software Landscape
================================================================================
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

Speaker Bullets:
* Capstone of Units 5–7: From pairwise alignment, to MSA, to robust phylogenetic trees!
```

---

## Detailed Comprehensive Technical Notes

### 1. The Tree Evaluation Problem

When a multiple sequence alignment is supplied to a tree-reconstruction algorithm (such as Neighbor-Joining or Maximum Likelihood), the algorithm optimizes its internal mathematical criterion and returns a single bifurcating tree topology.

However, two major statistical questions remain:
1. Is the branching order supported by the entire length of the sequence, or is it an artifact driven by a single highly variable, noisy alignment column?
2. If we had collected a slightly different sample of homologous sequences or independent genetic markers, would the reconstructed clades remain stable?

To address this without having to spend millions of dollars re-sequencing biological specimens, computational biologists utilize **non-parametric resampling techniques**.

---

### 2. The Non-Parametric Bootstrap Algorithm (Felsenstein, 1985)

Adapted from Bradley Efron's statistical resampling theory by Joseph Felsenstein in 1985, the phylogenetic bootstrap is the gold-standard method for evaluating branch support.

```
  Original Alignment M:
  Taxon 1:  A  T  G  C  A  T
  Taxon 2:  A  T  G  C  G  T
  Taxon 3:  A  C  G  A  G  A
  Taxon 4:  A  C  G  A  A  A
  Columns:  1  2  3  4  5  6
             |
             | Random Resampling WITH REPLACEMENT (Draw 6 columns)
             v
  Bootstrap Pseudo-Replicate M* (Example):
  Drawn:    Col 2, Col 2, Col 3, Col 5, Col 5, Col 6
  Taxon 1:  T  T  G  A  A  T
  Taxon 2:  T  T  G  G  G  T
  Taxon 3:  C  C  G  G  G  A
  Taxon 4:  C  C  G  A  A  A
             |
             v Reconstruct Tree T* using identical algorithm
             |
             v Repeat for B = 1,000 independent pseudo-replicates!
```

#### The Mathematical Foundation of Column Sampling:
Let an alignment contain $C$ columns. In generating a single pseudo-replicate alignment of length $C$, each column is drawn independently with probability $\frac{1}{C}$.
The probability that a specific column $k$ is **NOT** selected in a single draw is:
$$P(\text{not selected}) = 1 - \frac{1}{C}$$

The probability that column $k$ is omitted across all $C$ independent draws is:
$$P(\text{omitted in replicate}) = \left( 1 - \frac{1}{C} \right)^C$$

In the mathematical limit as alignment length $C \to \infty$:
$$\lim_{C \to \infty} \left( 1 - \frac{1}{C} \right)^C = e^{-1} \approx \mathbf{0.3679\text{ (36.8\%)}}$$

Thus, in every bootstrap replicate:
- Approximately **$36.8\%$ of the original unique alignment columns are omitted**.
- Approximately **$63.2\%$ of the original unique columns are included** (some appearing once, twice, three times, or more).

If an internal clade depends entirely on one or two idiosyncratic columns, omitting those columns in $\approx 37\%$ of replicates will cause that clade to collapse, resulting in a low bootstrap score. Conversely, if a clade is backed by pervasive phylogenetic signal distributed across the entire gene, it will withstand column omission and appear in $>95\%$ of replicate trees.

---

### 3. Consensus Tree Construction

After generating $B$ bootstrap replicate trees (typically $B = 1,000$), the collection of trees is synthesized into a single **Consensus Tree**:

1. **Strict Consensus Tree:**  
   Retains only those internal branches (bipartitions) that are present in **$100\%$ of all $B$ trees**. If even one tree out of 1,000 exhibits a conflicting branch, that internal node is collapsed into an unresolved multifurcation (polytomy). Strict consensus trees are often excessively conservative and poorly resolved.
2. **Majority-Rule (50%) Consensus Tree:**  
   Retains all internal branches that appear in **more than $50\%$ of the $B$ bootstrap trees** ($> B/2$). Because two mutually conflicting bifurcations cannot both appear in $>50\%$ of trees, majority-rule trees are guaranteed to be topologically consistent and acyclic.
3. **Annotating the Original Tree:**  
   In standard practice, researchers do not publish the consensus tree itself; instead, they take the **original tree reconstructed from the full dataset** and print the calculated bootstrap percentage values directly onto its corresponding internal nodes.

---

### 4. Critical Interpretation: What Bootstrap Values Do and Do Not Mean

```
  Bootstrap Support Range    Methodological Assessment & Publication Standard
  -------------------------------------------------------------------------------------------------
  >= 90% to 100%             Strongly supported clade; high confidence. Considered authoritative
                             evidence of common evolutionary descent.
  70% to 89%                 Moderately supported; biologically plausible, but sensitive to taxon
                             sampling. Should be discussed with hedging in scientific text.
  50% to 69%                 Weakly supported; low confidence. Authors should note the relationship
                             is unresolved.
  < 50%                      Completely unsupported. The node MUST be collapsed into a polytomy.
```

#### The Major Epistemological Trap:
A bootstrap value of $95\%$ is **NOT** a Bayesian posterior probability:
- It does **NOT** mean: *"There is a 95% probability that this clade is the true historical tree."*
- It **DOES** mean: *"If we were to re-sample character sites from this alignment under the identical distribution, the clade would be recovered in 95% of experiments."*

#### Systematic Error and Long-Branch Attraction (LBA):
If an alignment suffers from systematic biases—such as extreme compositional GC bias or **Long-Branch Attraction** (where two fast-evolving, distantly related taxa share convergent mutations)—Maximum Parsimony will recover the incorrect grouping in 100% of bootstrap replicates. In such cases, the bootstrap will report **100% confidence for an incorrect tree**. Bootstrap measures **precision (repeatability)**, not **accuracy (truth)**.

---

### 5. Phylogenetic File Formats

#### A. The Newick Tree Format
Adopted by the Society of Systematic Biologists at Newick's restaurant in 1986, this format represents nested trees using matching parentheses:

$$\texttt{((HBB\_HUMAN:0.005,HBB\_CHIMP:0.005)99:0.035,HBD\_HUMAN:0.040)100:0.610;}$$

- **Commas (`,`)** separate sister taxa.
- **Parentheses (`( ... )`)** enclose monophyletic clades.
- **Colons (`:`)** precede branch length values (e.g. `:0.005`).
- **Numbers following parentheses** denote bootstrap support percentages (e.g. `99`).
- **Semicolon (`;`)** terminates the tree statement.

#### B. The NEXUS Format (Maddison et al., 1997)
Used by PAUP* and MrBayes, NEXUS divides phylogenetic data into modular blocks:

```nexus
#NEXUS
BEGIN TAXA;
  DIMENSIONS NTAX=4;
  TAXLABELS HBB_HUMAN HBB_CHIMP HBD_HUMAN MB_HUMAN;
END;
BEGIN TREES;
  TREE Tree1 = ((HBB_HUMAN:0.005,HBB_CHIMP:0.005)99:0.035,HBD_HUMAN:0.040,MB_HUMAN:0.650);
END;
```

---

## Worked Example: Simulating a Bootstrap Resampling Round

### Problem:
Consider an alignment of $N = 4$ taxa across $C = 6$ nucleotide columns:

```
  Taxon           Col 1   Col 2   Col 3   Col 4   Col 5   Col 6
  -------------------------------------------------------------
  HBB_HUMAN         A       T       G       C       A       T
  HBB_CHIMP         A       T       G       C       G       T
  HBD_HUMAN         A       C       G       A       G       A
  MB_HUMAN          A       C       G       A       A       A
```

Simulate one bootstrap pseudo-replicate draw using the randomly generated column indices:  
$$\text{Indices drawn with replacement: } [ \mathbf{2, 2, 3, 5, 5, 6} ]$$

1. Construct the complete pseudo-replicate alignment $M^*$.
2. Identify which original columns were duplicated and which were omitted.
3. Evaluate whether Column 2's phylogenetic split is preserved or amplified.

---

### Step 1: Construct the Pseudo-Replicate Alignment ($M^*$)
Map the drawn indices to the columns:

```
  Taxon           Col 2   Col 2   Col 3   Col 5   Col 5   Col 6
  -------------------------------------------------------------
  HBB_HUMAN         T       T       G       A       A       T
  HBB_CHIMP         T       T       G       G       G       T
  HBD_HUMAN         C       C       G       G       G       A
  MB_HUMAN          C       C       G       A       A       A
```

---

### Step 2: Characterize Omissions and Duplications
- **Omitted Columns:** Column 1 and Column 4 were **NOT drawn** ($2 / 6 = \mathbf{33.3\%}$ omitted, closely matching the theoretical $e^{-1} \approx 36.8\%$).
- **Duplicated Columns:** Column 2 and Column 5 were each **drawn twice**.
- **Singletons:** Column 3 and Column 6 were drawn once.

---

### Step 3: Evaluate Phylogenetic Signal in $M^*$
- In the original alignment, **Column 2** has `T` in `HBB_HUMAN` and `HBB_CHIMP`, and `C` in `HBD_HUMAN` and `MB_HUMAN`. This informative site strongly supports grouping `(HBB_HUMAN, HBB_CHIMP)` together.
- In the pseudo-replicate alignment $M^*$, Column 2 was selected **twice** (occupying columns 1 and 2 of $M^*$).
- As a consequence, the phylogenetic signal uniting human beta-globin with chimpanzee beta-globin is **doubled in weight** in this replicate, ensuring that Tree $T^*$ strongly recovers the `(HBB_HUMAN, HBB_CHIMP)` clade!

---

## Formative In-Class Checks

### Question 1
**Prompt:** A student generates a Neighbor-Joining tree of vertebrate globins and observes that the node grouping mouse and rat beta-globins has a bootstrap support value of **100%**, while the node grouping human beta-globin with rabbit beta-globin has a bootstrap support value of **52%**.  
1. How should the student report the human-rabbit relationship in the results section?  
2. If this tree were converted into a 70% majority-rule consensus tree, what would happen to the human-rabbit node?

**Model Answer:**
1. **Reporting the human-rabbit node:** The student must report that the relationship between human and rabbit beta-globin is **weakly supported and statistically unresolved** (bootstrap support of only 52%). The author cannot claim definitive evolutionary kinship based on this node.
2. **Effect on 70% consensus tree:** In a 70% majority-rule consensus tree, any internal node with $< 70\%$ bootstrap support is **collapsed into a polytomy** (an unresolved multifurcation). The human-rabbit branch would be dissolved, showing human, rabbit, and their sister taxa radiating simultaneously from a single parent node.

---

### Question 2
**Prompt:** Why does calculating a bootstrap analysis for a Maximum Likelihood tree require significantly more computational time than calculating a bootstrap analysis for a Neighbor-Joining tree?

**Model Answer:**
- **Neighbor-Joining (NJ)** is a fast algorithmic clustering method with polynomial time complexity $\mathcal{O}(N^3)$. Computing 1,000 NJ trees takes only a few seconds.
- **Maximum Likelihood (ML)** is an optimality-criterion method that evaluates the probabilistic substitution model across all alignment columns and executes an extensive heuristic search across tree space (evaluating branch-swapping moves like NNI, SPR, and TBR) to find the tree maximizing likelihood. Repeating this compute-intensive heuristic optimization 1,000 independent times can require hours or days of high-performance compute time.

---

### Question 3
**Prompt:** In Newick format, translate the following string into an ASCII cladogram and state the bootstrap support value for the clade containing Taxon A and Taxon B:  
`((A:0.04, B:0.04)98:0.02, (C:0.05, D:0.05)85:0.01);`

**Model Answer:**
- **ASCII Cladogram:**
```
       +--- Taxon A (0.04)
  (98) +---|
       |   +--- Taxon B (0.04)
  -----+
       |   +--- Taxon C (0.05)
  (85) +---|
           +--- Taxon D (0.05)
```
- **Bootstrap Support:** The clade uniting Taxon A and Taxon B has a **bootstrap support value of 98%**, indicating extremely high statistical confidence.
