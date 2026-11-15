# Question Bank: Unit 7 — Phylogenetic Analysis

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Syllabus Topic:** Fundamental of Phylogenetic model, Tree interpretation — Paralogues and orthologues, Tree building and tree evaluation, Phylogenetic software  
**Primary Learning Outcome:** LO5 (Reconstruct and interpret phylogenetic trees, understand distance vs character methods, and evaluate bootstrap support)  

---

## Section A: Multiple Choice Questions (15 MCQs)

### Q01
In a phylogenetic tree, what does an internal node represent biologically?  
a) An extant living species sampled in the laboratory  
b) The hypothetical most recent common ancestor (MRCA) of the descendant lineages that bifurcate from it  
c) A sequencing sequencing error in the read  
d) The physical length of the chromosome  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) The hypothetical most recent common ancestor (MRCA) of the descendant lineages that bifurcate from it  
* **Rationale:** In phylogenetic graph theory, terminal nodes (leaves) represent sampled operational taxonomic units (extant or fossil taxa). Internal nodes represent hypothetical ancestral divergence points from which descendant lineages split.

### Q02
What is the defining biological difference between a cladogram and a phylogram?  
a) A cladogram displays only branching topology (relationships), whereas a phylogram scales branch lengths proportional to the amount of evolutionary change or nucleotide substitutions  
b) Cladograms are used only for plants; phylograms are used only for animals  
c) Cladograms require DNA sequences, while phylograms use protein sequences  
d) Cladograms can never have roots  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) A cladogram displays only branching topology (relationships), whereas a phylogram scales branch lengths proportional to the amount of evolutionary change or nucleotide substitutions  
* **Rationale:** A cladogram represents relative recency of common ancestry without conveying evolutionary divergence magnitude. A phylogram encodes evolutionary divergence directly into the horizontal branch lengths (e.g., substitutions per site).

### Q03
Human alpha-globin and human beta-globin are homologous genes present within the same organism that arose via an ancient gene duplication event. These genes are classified as:  
a) Orthologues  
b) Paralogues  
c) Xenologues  
d) Analogues  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Paralogues  
* **Rationale:** Paralogues are genes related by gene duplication events within a single genome. Over evolutionary time, paralogues can evolve specialized or diverged functions (e.g., alpha- and beta-globin subunits forming the adult hemoglobin tetramer).

### Q04
Which of the following taxonomic groups constitutes a strictly "monophyletic" group (clade)?  
a) A group containing an ancestral species and all of its evolutionary descendants  
b) A group containing an ancestor and some, but not all, of its descendants  
c) A group of organisms sharing similar morphological traits derived from convergent evolution without a recent common ancestor  
d) A collection of organisms whose phylogenetic tree has no root  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) A group containing an ancestral species and all of its evolutionary descendants  
* **Rationale:** A monophyletic group (or clade) comprises a common ancestor and ALL of its descendants. Paraphyletic groups exclude some descendants (e.g., traditional "Reptilia" excluding birds), and polyphyletic groups unite unrelated taxa lacking immediate common ancestry.

### Q05
What is the primary biological purpose of including an "outgroup" taxon when constructing a phylogenetic tree?  
a) To increase the bootstrap values of all internal nodes to 100%  
b) To establish the position of the root, thereby polarizing the direction of evolutionary change from ancestral to derived states  
c) To provide an extra sequence in case one sequence file is corrupted  
d) To prove that the molecular clock is strictly constant  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) To establish the position of the root, thereby polarizing the direction of evolutionary change from ancestral to derived states  
* **Rationale:** An outgroup is a taxon known to have branched off prior to the radiation of the ingroup taxa. Rooting the tree along the branch leading to the outgroup defines the root node, allowing researchers to determine which traits are ancestral (plesiomorphic) versus derived (apomorphic).

### Q06
What critical evolutionary assumption does the UPGMA (Unweighted Pair Group Method with Arithmetic Mean) algorithm make that frequently produces incorrect tree topologies?  
a) It assumes all sequences mutate at completely random positions  
b) It assumes a strict molecular clock (an equal, constant rate of evolutionary change across all lineages)  
c) It assumes that gaps can never occur in protein sequences  
d) It assumes that all species are diploid  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) It assumes a strict molecular clock (an equal, constant rate of evolutionary change across all lineages)  
* **Rationale:** UPGMA generates ultrametric trees where all terminal leaves are equidistant from the root. This forces a strict molecular clock assumption. If one lineage evolved significantly faster than others (unequal evolutionary rates), UPGMA groups slow-evolving lineages together incorrectly.

### Q07
How does the Neighbor-Joining (NJ) method improve upon UPGMA?  
a) NJ does not assume a constant rate of evolution across lineages, produces additive trees with unequal branch lengths, and operates via star decomposition  
b) NJ evaluates every possible tree topology in the universe to guarantee the global optimum  
c) NJ aligns sequences without using a substitution matrix  
d) NJ produces rooted trees automatically without needing an outgroup  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) NJ does not assume a constant rate of evolution across lineages, produces additive trees with unequal branch lengths, and operates via star decomposition  
* **Rationale:** Saitou and Nei's Neighbor-Joining method removes the molecular clock constraint. Starting from an unresolved star topology, it uses normalized $Q$-matrix criteria to pair neighbors that minimize total tree length, producing unrooted additive trees where branch lengths reflect true lineage-specific substitution rates.

### Q08
Which tree construction approach is classified as a "character-based" method rather than a "distance-based" method?  
a) UPGMA  
b) Neighbor-Joining (NJ)  
c) Maximum Parsimony (MP)  
d) Minimum Evolution (ME)  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** c) Maximum Parsimony (MP)  
* **Rationale:** Distance methods (UPGMA, NJ, ME) compress alignment data into a single summary distance matrix before building the tree. Character-based methods (Maximum Parsimony, Maximum Likelihood, Bayesian inference) evaluate individual alignment columns (characters) directly throughout tree evaluation.

### Q09
What is the governing optimality criterion of the Maximum Parsimony method in phylogenetics?  
a) The tree that requires the maximum number of mutations is preferred  
b) The tree that requires the minimum total number of evolutionary character-state changes (mutations) to explain the observed alignment is chosen as optimal  
c) The tree that yields the highest mathematical probability under a GTR model  
d) The tree that has the shortest runtime on a computer  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The tree that requires the minimum total number of evolutionary character-state changes (mutations) to explain the observed alignment is chosen as optimal  
* **Rationale:** Maximum Parsimony invokes Occam's razor: the simplest biological hypothesis is best. It searches for the tree topology that minimizes the total number of mutational steps across all informative sites.

### Q10
In a multiple sequence alignment evaluated for Maximum Parsimony, which of the following columns represents a "parsimony-informative site"?  
a) A column where all four species possess the identical nucleotide `A`  
b) A column where three species have `A` and one species has `T`  
c) A column where two species have nucleotide `A` and two species have nucleotide `G`  
d) A column containing only gaps across all species  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** c) A column where two species have nucleotide `A` and two species have nucleotide `G`  
* **Rationale:** A site is parsimony-informative if and only if it contains at least two different character states, each occurring in at least two separate taxa. An invariant column or a site where a mutation occurs in only one taxon (autapomorphy) requires the same number of steps on all possible topologies and cannot differentiate between trees.

### Q11
What phenomenon can cause Maximum Parsimony to select an incorrect tree topology with high statistical confidence when lineages exhibit vastly different evolutionary rates?  
a) Long-branch attraction (LBA)  
b) Profile drift  
c) Transposon silencing  
d) Codon usage bias  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) Long-branch attraction (LBA)  
* **Rationale:** Long-Branch Attraction (Felsenstein zone) occurs when two distantly related, rapidly evolving lineages independently accumulate random convergent mutations. Parsimony misinterprets these parallel homoplasies as shared derived synapomorphies, falsely grouping the two long branches together.

### Q12
How is the statistical robustness of individual nodes in a phylogenetic tree evaluated using Felsenstein's bootstrap analysis?  
a) By sequencing 1,000 additional biological specimens in the wet lab  
b) By generating pseudo-replicate alignments via randomly resampling alignment columns with replacement, reconstructing trees for each replicate, and calculating the percentage of times each clade is recovered  
c) By calculating the GC content of every branch  
d) By computing the Gibbs free energy of the DNA double helix  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) By generating pseudo-replicate alignments via randomly resampling alignment columns with replacement, reconstructing trees for each replicate, and calculating the percentage of times each clade is recovered  
* **Rationale:** Non-parametric bootstrapping resamples columns from the original alignment with replacement to create hundreds of pseudo-alignments of equal length. Trees are reconstructed from each replicate; the bootstrap support value at a node indicates the percentage of replicate trees that contain that exact bipartition.

### Q13
What is the standard consensus interpretation of a bootstrap proportion of 95% at an internal node?  
a) The node has a 5% chance of being an animal  
b) The phylogenetic split is strongly supported by the sequence data; in 95% of resampled pseudo-alignments, the descendant taxa clustered together as a clade  
c) 95% of the residues in the alignment are adenines  
d) The tree was reconstructed in 95 seconds  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The phylogenetic split is strongly supported by the sequence data; in 95% of resampled pseudo-alignments, the descendant taxa clustered together as a clade  
* **Rationale:** A bootstrap proportion $\ge 70\%$ is generally considered moderate support, and $\ge 90\text{--}95\%$ is considered strong statistical evidence that the grouping is robustly supported across the aligned characters.

### Q14
Which desktop software package is widely used in bioinformatics education for comprehensive sequence alignment, model testing, and phylogenetic tree reconstruction using distance, parsimony, and maximum likelihood methods?  
a) MEGA (Molecular Evolutionary Genetics Analysis)  
b) VMD  
c) RepeatMasker  
d) EMBOSS transeq  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) MEGA (Molecular Evolutionary Genetics Analysis)  
* **Rationale:** MEGA (Kumar et al.) is the standard, user-friendly desktop suite for molecular phylogenetics, incorporating sequence alignment (Clustal/MUSCLE), nucleotide/protein substitution model selection, tree reconstruction (NJ, ME, MP, ML), and tree visualization.

### Q15
What is the fundamental difference between a "gene tree" and a "species tree"?  
a) A gene tree traces the evolutionary history of an individual homologous gene family, which may diverge from the true organismal species tree due to gene duplication, loss, or incomplete lineage sorting  
b) Gene trees are always circular, while species trees are always rectangular  
c) Gene trees apply only to viruses, while species trees apply to mammals  
d) There is no difference; they are always identical  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) A gene tree traces the evolutionary history of an individual homologous gene family, which may diverge from the true organismal species tree due to gene duplication, loss, or incomplete lineage sorting  
* **Rationale:** A gene tree reflects the genealogy of a single genomic locus. Gene duplications (creating paralogues), gene losses, horizontal gene transfers, and incomplete lineage sorting (ILS) can cause the topology of a gene tree to differ significantly from the true species phylogeny.

---

## Section B: Short Answer Questions (6 SAQs)

### SAQ 01: Orthologues, Paralogues, and Xenologues (3 Marks)
**Question:** Differentiate between orthologues, paralogues, and xenologues. Provide a concrete biological example of how orthologues and paralogues appear within the vertebrate globin gene family.  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Orthologues:** Homologous genes in different species that diverged via a **speciation event**. They typically perform the exact same physiological function in both organisms.  
  * *Globin Example:* Human beta-globin (*HBB*) and chimpanzee beta-globin (*HBB*).
* **Paralogues:** Homologous genes that diverged following an intragenomic **gene duplication event**. They often evolve distinct biological roles or expression patterns.  
  * *Globin Example:* Human alpha-globin (*HBA1*) and human beta-globin (*HBB*), or adult *HBB* vs fetal gamma-globin (*HBG1*).
* **Xenologues:** Homologous genes acquired through **horizontal gene transfer (HGT)** between phylogenetically distant organisms (e.g., bacterial antibiotic resistance genes transferred via plasmids).

**Marking Scheme:**  
* 1.5 Marks: 0.5 marks for each accurate evolutionary definition (speciation, duplication, HGT).  
* 1.5 Marks: Clear biological globin examples illustrating orthologues and paralogues.

---

### SAQ 02: Cladogram vs Phylogram vs Ultrametric Tree (3 Marks)
**Question:** Compare a cladogram, a phylogram, and an ultrametric tree (chronogram) in terms of branch length interpretation and biological utility.  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Analyze  

**Model Answer:**  
1. **Cladogram:** Branch lengths are arbitrary and carry no numerical meaning. Only the branching pattern (topology) is meaningful, indicating relative recency of common ancestry. Useful for simple cladistic classification.
2. **Phylogram:** Branch lengths are scaled proportional to the amount of evolutionary character change (e.g., number of nucleotide or amino acid substitutions per site). Allows researchers to visualize variable evolutionary rates across different lineages.
3. **Ultrametric Tree (Chronogram):** All branch tips (terminal leaves) are equidistant from the root node. Branch lengths represent absolute or relative geological time, assuming a constant molecular clock calibrated with fossil dates.

**Marking Scheme:**  
* 1 Mark per tree class accurately explained with branch length meaning and utility.

---

### SAQ 03: Distance-Based vs Character-Based Tree Methods (4 Marks)
**Question:** Contrast distance-based phylogenetic methods (e.g., Neighbor-Joining) with character-based methods (e.g., Maximum Likelihood) across four criteria: input data representation, computational speed, handling of evolutionary models, and ability to reconstruct ancestral sequence states.  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Analyze  

**Model Answer:**  

| Criterion | Distance-Based Methods (e.g., NJ) | Character-Based Methods (e.g., ML / MP) |
| :--- | :--- | :--- |
| **Input Data Representation** | Collapses the entire alignment into a single pairwise numerical distance matrix ($N \times N$). | Retains and evaluates every individual column (character site) in the multiple sequence alignment. |
| **Computational Speed** | Extremely fast ($O(N^3)$); easily constructs trees for thousands of sequences in seconds. | Computationally demanding; evaluates complex mathematical likelihoods across tree topologies. |
| **Evolutionary Models** | Evolutionary models (Jukes-Cantor, Kimura) are applied upfront only during distance calculation. | Incorporates explicit, sophisticated probabilistic substitution models throughout the entire tree search. |
| **Ancestral Reconstruction** | Cannot reconstruct ancestral sequences at internal nodes because site identities are discarded. | Readily infers the most probable ancestral character states at every internal node of the tree. |

**Marking Scheme:**  
* 1 Mark per row accurately contrasted.

---

### SAQ 04: The Molecular Clock and UPGMA Failure (3 Marks)
**Question:** Explain the "molecular clock hypothesis". What happens when UPGMA is used to construct a tree for sequences that violate the molecular clock, and why does Neighbor-Joining avoid this error?  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand / Analyze  

**Model Answer:**  
* **Molecular Clock Hypothesis:** Proposes that nucleotide or amino acid substitutions accumulate at an approximately constant rate over geological time across all evolutionary lineages.
* **UPGMA Failure:** UPGMA assumes strict ultrametricity (equal mutation rates across all branches). If one lineage experiences accelerated evolution (e.g., rodent genes mutating faster than primate genes), UPGMA groups the slow-evolving lineages together artificially, distorting the true branching order.
* **Why Neighbor-Joining Succeeds:** Neighbor-Joining uses a normalized rate-correction matrix ($Q$-matrix) that subtracts average divergence to all other taxa. It calculates branch lengths independently for each lineage, producing additive trees where unequal rates are faithfully represented without altering the true topological grouping.

**Marking Scheme:**  
* 1 Mark: Accurate definition of the molecular clock hypothesis.  
* 1 Mark: Detailed explanation of how rate acceleration causes UPGMA topological errors.  
* 1 Mark: Clear explanation of how Neighbor-Joining rate-correction handles lineage-specific variation.

---

### SAQ 05: Interpreting Parsimony-Informative Sites (4 Marks)
**Question:** Examine the following 4-taxon multiple sequence alignment of 5 nucleotide sites:  

```text
Taxon 1:  A  C  T  G  A
Taxon 2:  A  C  T  G  C
Taxon 3:  A  G  A  C  A
Taxon 4:  A  G  A  G  C
```

For each of the five sites (Columns 1 through 5), determine whether the site is:  
a) Invariant,  
b) Uninformative (autapomorphic / variable), or  
c) Parsimony-informative. Justify your classification for each site.  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Criterion:** A site is parsimony-informative if it contains at least two distinct character states, each occurring in at least two separate taxa.
1. **Site 1 (`A, A, A, A`):** **Invariant.** All taxa possess nucleotide `A`. Requires 0 steps on any tree; uninformative.
2. **Site 2 (`C, C, G, G`):** **Parsimony-Informative.** Contains two states (`C` and `G`), each appearing exactly twice (Taxa 1 & 2 have `C`; Taxa 3 & 4 have `G`). It supports grouping $(T_1, T_2)$ together against $(T_3, T_4)$.
3. **Site 3 (`T, T, A, A`):** **Parsimony-Informative.** Contains two states (`T` and `A`), each appearing twice (Taxa 1 & 2 have `T`; Taxa 3 & 4 have `A`). It supports grouping $(T_1, T_2)$ together.
4. **Site 4 (`G, G, C, G`):** **Uninformative (Variable / Autapomorphic).** Contains two states (`G` and `C`), but `C` appears in only ONE taxon (Taxon 3). A single mutation on the branch leading to Taxon 3 accounts for this site on all possible trees; thus, it cannot discriminate between tree topologies.
5. **Site 5 (`A, C, A, C`):** **Parsimony-Informative.** Contains two states (`A` and `C`), each appearing twice (Taxa 1 & 3 have `A`; Taxa 2 & 4 have `C`). It supports grouping $(T_1, T_3)$ together against $(T_2, T_4)$.

**Marking Scheme:**  
* 4 Marks: 0.8 marks per site correctly classified with complete mathematical/biological justification.

---

### SAQ 06: Non-Parametric Bootstrap Mechanics (3 Marks)
**Question:** Explain the step-by-step procedure of non-parametric bootstrap analysis in phylogenetics. What does a bootstrap value of 85% at a specific clade indicate?  
* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Step-by-Step Procedure:**  
  1. Starting from an alignment of length $N$ columns, generate a "pseudo-replicate alignment" of length $N$ by randomly sampling columns **with replacement** (some columns are sampled multiple times, others omitted).
  2. Reconstruct a phylogenetic tree from this pseudo-replicate alignment using the chosen tree-building method.
  3. Repeat this process $B$ times (typically $B = 500$ or $1,000$ iterations) to generate a collection of $B$ bootstrap trees.
  4. Compute a consensus tree. For each internal node, calculate the proportion of the $B$ trees in which that specific clade appears.
* **Interpretation of 85%:**  
  An 85% bootstrap value means that the specific grouping of taxa was recovered in 850 out of 1,000 resampled pseudo-alignments, providing strong confidence that the clade is supported across diverse character sites rather than being an artifact of a single unusual site.

**Marking Scheme:**  
* 2 Marks: Clear 4-step sequence (resampling with replacement, tree reconstruction, $B$ iterations, consensus percentage calculation).  
* 1 Mark: Precise statistical interpretation of an 85% bootstrap score.

---

## Section C: Long Answer / Problem Questions (2 LAQs)

### LAQ 01: Complete Step-by-Step UPGMA Tree Reconstruction (10 Marks)
**Question:**  
You are investigating the evolutionary relationships among four primate species ($A, B, C, D$) based on an alignment of their mitochondrial cytochrome b genes. Pairwise sequence divergence calculations yield the following distance matrix $D$ (expressed as percentage divergence):  

```text
       A      B      C      D
A      0      4      8      10
B      4      0      8      10
C      8      8      0       6
D     10     10      6       0
```

Using the **UPGMA (Unweighted Pair Group Method with Arithmetic Mean)** algorithm:  
a) Identify the closest pair of taxa, cluster them into a single node, and calculate the branch lengths/height of this initial node. (2 Marks)  
b) Recompute the updated distance matrix between the new cluster and the remaining taxa, explicitly showing all arithmetic averages. (3 Marks)  
c) Identify the next clustering event, update the matrix, and calculate the height of all remaining internal nodes. (3 Marks)  
d) Draw the complete, fully labeled ultrametric phylogenetic tree. Specify the exact branch lengths connecting each node and confirm that all leaves are equidistant from the root. (2 Marks)  

* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Apply / Analyze  

**Model Solution:**  
**a) Initial Clustering: Taxa A and B (2 Marks):**  
* The smallest off-diagonal value in matrix $D$ is $D(A, B) = 4\%$.  
* Cluster taxa $A$ and $B$ into node $(AB)$.  
* The branch height of node $(AB)$ is:  
  $$h(AB) = \frac{D(A, B)}{2} = \frac{4}{2} = \mathbf{2.0}$$  
* Branch length from $(AB)$ to leaf $A = 2.0$; branch length from $(AB)$ to leaf $B = 2.0$.

**b) Recomputing Distance Matrix 1 (3 Marks):**  
Calculate distances from cluster $(AB)$ to remaining taxa $C$ and $D$:  
* $D((AB), C) = \frac{D(A, C) + D(B, C)}{2} = \frac{8 + 8}{2} = \mathbf{8.0}$  
* $D((AB), D) = \frac{D(A, D) + D(B, D)}{2} = \frac{10 + 10}{2} = \mathbf{10.0}$  
* $D(C, D) = \mathbf{6.0}$

*Updated Matrix 1:*  
```text
           (AB)     C      D
(AB)         0     8.0   10.0
C          8.0       0    6.0
D         10.0     6.0      0
```

**c) Second and Final Clustering Steps (3 Marks):**  
* **Step 2:** The smallest distance in Updated Matrix 1 is $D(C, D) = 6.0$.  
  Cluster taxa $C$ and $D$ into node $(CD)$.  
  Branch height of node $(CD)$ is:  
  $$h(CD) = \frac{D(C, D)}{2} = \frac{6.0}{2} = \mathbf{3.0}$$  
  Branch length from $(CD)$ to leaf $C = 3.0$; branch length from $(CD)$ to leaf $D = 3.0$.

* **Step 3: Final Root Node $((AB), (CD))$:**  
  Calculate distance between cluster $(AB)$ and cluster $(CD)$:  
  $$D((AB), (CD)) = \frac{D(A, C) + D(A, D) + D(B, C) + D(B, D)}{4} = \frac{8 + 10 + 8 + 10}{4} = \frac{36}{4} = \mathbf{9.0}$$  
  The root node height is:  
  $$h(\text{Root}) = \frac{D((AB), (CD))}{2} = \frac{9.0}{2} = \mathbf{4.5}$$

* **Calculating Internal Branch Lengths:**  
  - Branch from Root to node $(AB)$: $h(\text{Root}) - h(AB) = 4.5 - 2.0 = \mathbf{2.5}$  
  - Branch from Root to node $(CD)$: $h(\text{Root}) - h(CD) = 4.5 - 3.0 = \mathbf{1.5}$

**d) Final Ultrametric Tree Diagram and Verification (2 Marks):**  

```text
Height:  4.5 (Root)       3.0                2.0               0.0 (Leaves)
          |                |                  |                 |
          +-----------------------------------+---------------- A (len = 2.0)
          |                                   |
          |                                   +---------------- B (len = 2.0)
          |
          +----------------+----------------------------------- C (len = 3.0)
                           |
                           +----------------------------------- D (len = 3.0)
```

* **Verification of Ultrametric Distances to Leaves:**  
  - Leaf $A$: Root $\rightarrow (AB) (2.5) + (AB) \rightarrow A (2.0) = \mathbf{4.5}$  
  - Leaf $B$: Root $\rightarrow (AB) (2.5) + (AB) \rightarrow B (2.0) = \mathbf{4.5}$  
  - Leaf $C$: Root $\rightarrow (CD) (1.5) + (CD) \rightarrow C (3.0) = \mathbf{4.5}$  
  - Leaf $D$: Root $\rightarrow (CD) (1.5) + (CD) \rightarrow D (3.0) = \mathbf{4.5}$  
  All leaves are exactly 4.5 units from the root, confirming perfect ultrametricity.

**Marking Scheme Breakdown:**  
* 2 Marks: Correct identification of pair $(A, B)$ and initial node height $2.0$.  
* 3 Marks: Flawless distance recalculations for cluster $(AB)$ to $C$ ($8.0$) and $D$ ($10.0$).  
* 3 Marks: Correct clustering of $(C, D)$ at height $3.0$, root calculation at height $4.5$, and internal branch lengths ($2.5$ and $1.5$).  
* 2 Marks: Clear ultrametric tree drawing with all branch lengths and mathematical distance verification.

---

### LAQ 02: Molecular Phylogenetic Models, Character-Based Inference, and Tree Evaluation (10 Marks)
**Question:**  
You are analyzing a multiple sequence alignment of 5 vertebrate species (Human, Chimp, Gorilla, Mouse, Zebrafish) to resolve primate relationships.

a) Contrast the **Jukes–Cantor (JC69)** model with the **Kimura Two-Parameter (K2P)** model of nucleotide substitution. Explain why K2P is biologically superior for phylogenetic reconstruction. (3 Marks)  
b) Describe the mathematical framework of **Maximum Likelihood (ML)** tree reconstruction: define the likelihood function $L = P(D \mid T, \theta)$, explain what each variable represents, and explain why ML is statistically superior to Maximum Parsimony on deep evolutionary lineages. (4 Marks)  
c) Outline the interpretation of the resulting phylogenetic tree shown below:  

```text
+-- Zebrafish (Outgroup)
|
`--+ (Bootstrap = 100%)
   |-- Mouse
   |
   `--+ (Bootstrap = 98%)
      |-- Gorilla
      |
      `--+ (Bootstrap = 94%)
         |-- Human
         `-- Chimpanzee
```

   1. State which taxon serves as the outgroup and explain what rooting with this outgroup establishes.  
   2. Identify whether the grouping (Human, Chimpanzee, Gorilla) forms a monophyletic or paraphyletic clade.  
   3. Critically evaluate the biological reliability of the (Human, Chimpanzee) sister relationship based on its bootstrap value. (3 Marks)  

* **Learning Outcome:** LO5  
* **Bloom's Taxonomy Level:** Analyze / Synthesize  

**Model Solution:**  
**a) Jukes–Cantor (JC69) vs Kimura Two-Parameter (K2P) (3 Marks):**  
* **Jukes–Cantor (JC69):** The simplest nucleotide substitution model. It assumes:
  1. Equal equilibrium base frequencies ($p_A = p_C = p_G = p_T = 0.25$).
  2. A single uniform substitution rate $\alpha$ across all pairs of nucleotides.
* **Kimura Two-Parameter (K2P):** Distinguishes between two classes of mutations:
  1. **Transitions ($\alpha$):** Purine-to-purine ($A \leftrightarrow G$) or pyrimidine-to-pyrimidine ($C \leftrightarrow T$) changes.
  2. **Transversions ($\beta$):** Purine-to-pyrimidine or pyrimidine-to-purine changes ($A \leftrightarrow C, A \leftrightarrow T, G \leftrightarrow C, G \leftrightarrow T$).
* **Biological Superiority of K2P:** In biological DNA replication, transitions occur biochemically 2 to 4 times more frequently than transversions due to tautomeric shifts and DNA polymerase mispairing geometry. JC69 treats them equally, underestimating true evolutionary divergence over time. K2P incorporates the transition/transversion ratio ($\kappa = \alpha/\beta$), providing vastly more accurate branch length estimates.

**b) Maximum Likelihood Framework and Parsimony Comparison (4 Marks):**  
* **The Likelihood Formulation:**  
  $$L = P(D \mid T, \theta)$$  
  Where:
  - $D$: The observed multiple sequence alignment (the data).
  - $T$: The proposed phylogenetic tree topology and its associated branch lengths.
  - $\theta$: The parameter vector of the evolutionary substitution model (e.g., base frequencies, transition/transversion ratio $\kappa$, gamma distribution shape parameter $\alpha$ for among-site rate variation).
* **Evaluation:** For a given tree $T$ and model $\theta$, ML computes the probability of generating the exact observed alignment columns, summing probabilities over all possible ancestral states at internal nodes. It searches tree space to find the tree topology that maximizes $\ln L$.
* **Why ML is Statistically Superior to Parsimony on Deep Lineages:**
  1. **Resistant to Long-Branch Attraction (LBA):** Parsimony assumes mutations are rare; on deep branches, multiple hits (convergent substitutions) occur, misleading parsimony into falsely grouping long branches together. ML explicitly models multiple hits and rate variation across sites (via $+G$), correctly accounting for parallel mutations.
  2. **Statistical Consistency:** Under a realistic substitution model, ML is statistically consistent: as the number of aligned sites approaches infinity, ML is mathematically guaranteed to converge on the true species tree.

**c) Tree Interpretation and Biological Evaluation (3 Marks):**  
1. **Outgroup and Rooting:** Zebrafish serves as the outgroup because teleost fish diverged prior to the tetrapod/mammalian radiation. Rooting the tree on the branch leading to Zebrafish polarizes the tree, establishing that the Mouse lineage diverged before the diversification of primates, and identifying the root node of the mammalian ingroup.
2. **Monophyly of (Human, Chimpanzee, Gorilla):** This group is strictly **monophyletic** (forming the family Hominidae / subfamily Homininae). It comprises the internal ancestral node and ALL descendant lineages arising from that common ancestor.
3. **Reliability of (Human, Chimpanzee) Sister Relationship:** The internal node uniting Human and Chimpanzee displays a bootstrap support proportion of **94%**. In phylogenetic practice, bootstrap values $\ge 90\text{--}95\%$ indicate strong statistical confidence. This demonstrates that across 94% of resampled pseudo-replicates, Human and Chimp clustered exclusively together to the exclusion of Gorilla, confirming with high confidence that Chimpanzees are the closest extant sister taxon to modern humans.

**Marking Scheme Breakdown:**  
* 3 Marks: Accurate contrast of JC69 vs K2P (1.5 marks) and biological justification of transition bias ($\alpha > \beta$) (1.5 marks).  
* 4 Marks: Formal definition of $L = P(D \mid T, \theta)$ with all variables defined (2 marks); rigorous analysis of multiple hits and resistance to Long-Branch Attraction over Parsimony (2 marks).  
* 3 Marks: 1 mark for outgroup identification and polarization role; 1 mark for correct monophyletic classification; 1 mark for rigorous statistical interpretation of the 94% bootstrap score.
