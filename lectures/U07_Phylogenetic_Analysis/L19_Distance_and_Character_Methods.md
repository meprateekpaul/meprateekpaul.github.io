# Lecture 19 — Distance and Character Methods

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 7:** Phylogenetic Analysis  
**Syllabus Topic:** Tree building and tree evaluation, Phylogenetic software  
**Primary Learning Outcome:** LO5 — Build phylogenetic trees, execute UPGMA distance calculations by hand, and explain Neighbor-Joining, Maximum Parsimony, and Maximum Likelihood.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Two Philosophical Schools of Tree Reconstruction
================================================================================
Topic: Distance-Matrix vs Character-Based Methods

[Visual: Two Paradigms:
  Multiple Alignment -> [Pairwise Distances] -> Distance Matrix -> UPGMA / NJ
  Multiple Alignment -> [Inspect Columns Directly] -> Parsimony / Maximum Likelihood]

Speaker Bullets:
* Tree reconstruction methods divide into two primary mathematical families:
  1. **Distance-Matrix Methods:** Condense the alignment into pairwise distances (loss of data).
  2. **Character-Based Methods:** Evaluate every alignment column directly (retains all data).
* We balance computational speed against biological model sophistication.
```

```
================================================================================
SLIDE 2: Correcting Evolutionary Distances: The Saturation Problem
================================================================================
Topic: Multiple Hits Obscure Real Time

[Visual: Divergence Curve:
  Observed Difference (p) plateaus at 75% for DNA due to multiple substitutions!
  Jukes-Cantor corrected distance d curves upward toward infinity!]

Formula (Jukes-Cantor, 1969):
  d = - (3/4) * ln( 1 - (4/3) * p )

Speaker Bullets:
* Observed sequence difference $p$ underestimates true evolutionary distance.
* If a site mutates $A \to G \to C \to T$, we observe only 1 mutation, but 3 occurred!
* Substitution models correct for hidden multiple hits and homoplasy.
```

```
================================================================================
SLIDE 3: The UPGMA Algorithm
================================================================================
Topic: Unweighted Pair Group Method with Arithmetic Mean (Sokal & Michener, 1958)

  UPGMA In a Nutshell:
  1. Find the smallest distance d(A, B) in distance matrix.
  2. Cluster A and B into a composite node (AB).
  3. Set node height h(AB) = d(A, B) / 2.
  4. Recalculate average distance from (AB) to all remaining taxa.
  5. Repeat until all taxa are merged into the root.

Speaker Bullets:
* UPGMA is the simplest, most intuitive distance-based clustering algorithm.
* It produces an **Ultrametric Tree** where all tips are equidistant from the root.
```

```
================================================================================
SLIDE 4: The Fatal Flaw of UPGMA: The Molecular Clock Assumption
================================================================================
Topic: When Rates Differ, UPGMA Produces Wrong Topologies!

[Visual: Unequal evolutionary rates:
  Lineage A evolves 5x faster than B and C.
  UPGMA incorrectly clusters B and C together first, corrupting the tree!]

Speaker Bullets:
* UPGMA assumes a constant, uniform rate of evolution across all lineages (strict molecular clock).
* In biology, rodents evolve faster than primates; viruses mutate faster than hosts.
* When rate constancy is violated, UPGMA is guaranteed to output the WRONG tree!
```

```
================================================================================
SLIDE 5: The Neighbor-Joining (NJ) Algorithm
================================================================================
Topic: Saitou & Nei's Nobel-Caliber Solution (1987)

[Visual: Star Decomposition:
  Step 1: Start with all taxa radiating from a single central star node.
  Step 2: Calculate transformed Q-matrix (subtracts total divergence of each taxon).
  Step 3: Pair the two taxa that minimize Q(i, j) into a new internal branch.
  Step 4: Repeat until fully resolved into an unrooted bifurcating tree!]

Speaker Bullets:
* Neighbor-Joining does NOT assume a molecular clock.
* Lineages can have completely different branch lengths (accommodates fast and slow evolvers).
* Extremely fast: $\mathcal{O}(N^3)$, runs in seconds for hundreds of taxa.
```

```
================================================================================
SLIDE 6: Character-Based: Maximum Parsimony (MP)
================================================================================
Topic: Occam's Razor in Phylogenetics

  Principle:
  "The tree topology requiring the MINIMUM total number of evolutionary mutational
   steps to explain the observed alignment is the best tree."

[Visual: Evaluating two alternative tree topologies across an informative column:
  Topology 1 requires 1 mutation: A -> G. (Parsimony score = 1) [WINNER!]
  Topology 2 requires 2 independent mutations: A -> G and A -> G. (Score = 2)]

Speaker Bullets:
* Maximum Parsimony evaluates informative columns without relying on pairwise distances.
* Weakness: Long-Branch Attraction (LBA) can mislead parsimony on divergent sequences.
```

```
================================================================================
SLIDE 7: Probabilistic Methods: Maximum Likelihood (ML)
================================================================================
Topic: Ronald Fisher's Statistical Framework Applied to Phylogeny

Formula:
  Likelihood L = P( Multiple Alignment | Tree Topology, Substitution Model )

Speaker Bullets:
* Maximum Likelihood finds the tree topology and branch lengths that maximize the
  probability of observing the actual sequence data.
* Explicitly incorporates substitution models (JC69, K2P, GTR, WAG) and rate variation (+Gamma).
* Statistically robust, but computationally intensive: requires searching tree space.
```

```
================================================================================
SLIDE 8: Summary & Comparison of Methods
================================================================================
Topic: Which Method to Choose?

+---------------+--------------------+--------------------+-------------------+
| Method        | Underlying Model   | Computational Speed| Key Limitation    |
+---------------+--------------------+--------------------+-------------------+
| **UPGMA**     | Strict Mol. Clock  | Extremely Fast     | Assumes clock     |
| **NJ**        | Variable rates     | Fast: O(N^3)       | Condenses data    |
| **Parsimony** | Occam's Razor      | Moderate           | Long-Branch Attract|
| **ML**        | Full Probabilistic | Slow (Hours/Days)  | High compute cost |
+---------------+--------------------+--------------------+-------------------+

Speaker Bullets:
* In practice: use Neighbor-Joining for preliminary exploration; use Maximum Likelihood
  or Bayesian methods (MrBayes) for final publication.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Two Foundational Paradigms

```
  Attribute              Distance-Matrix Methods (Phenetic)     Character-Based Methods (Cladistic)
  -------------------------------------------------------------------------------------------------
  Input Data Structure   Pairwise distance matrix D             Multiple sequence alignment columns
  Information Retained   Reduces entire alignment to a single   Retains every position, site variation,
                         numerical distance per pair (Lossy)    and character identity (Lossless)
  Optimality Criterion   Algorithmic clustering (UPGMA, NJ)     Statistical optimality (Parsimony, ML)
  Computational Speed    Fast: O(N^3)                           NP-hard search over tree space
  Representative Tools   MEGA, PHYLIP neighbor                  PAUP*, RAxML, PhyML, IQ-TREE
```

---

### 2. Evolutionary Distance Correction Models

When two sequences diverge, the observed fraction of mismatched sites ($p = \frac{\text{mismatches}}{\text{length}}$) underestimates the true number of historical substitutions due to **homoplasy** (hidden multiple hits, back mutations, and parallel substitutions at the same site).

#### A. Jukes-Cantor One-Parameter Model (JC69)
Assumes that all four nucleotide bases occur at equal frequencies ($p_A = p_C = p_G = p_T = 0.25$) and mutate into one another at an identical substitution rate ($\alpha$):

$$d = - \frac{3}{4} \ln\left( 1 - \frac{4}{3} p \right)$$

*Mathematical Boundary:* If $p \ge 0.75$ (75% divergence), the term $(1 - \frac{4}{3}p) \le 0$, and the natural logarithm becomes mathematically undefined ($d \to \infty$). At 75% nucleotide divergence, sequences have reached complete mutational saturation (identical to random sequences).

#### B. Kimura Two-Parameter Model (K2P / K80)
Recognizes that transitions ($A \leftrightarrow G, C \leftrightarrow T$) occur at a biochemically higher rate ($\alpha$) than transversions ($A/G \leftrightarrow C/T$, rate $\beta$):

$$d = - \frac{1}{2} \ln(1 - 2P - Q) - \frac{1}{4} \ln(1 - 2Q)$$

where $P$ is the observed proportion of transitional differences, and $Q$ is the observed proportion of transversional differences.

---

### 3. The UPGMA Clustering Algorithm

Published by Robert Sokal and Charles Michener in 1958, **UPGMA (Unweighted Pair Group Method with Arithmetic Mean)** is a hierarchical clustering algorithm that produces an **ultrametric tree**.

#### The Core Equations:
1. When two clusters $A$ and $B$ are merged into a composite node $(AB)$, the node is positioned at height:
   $$h(AB) = \frac{d(A, B)}{2}$$
2. The distance from the new cluster $(AB)$ to any other cluster $C$ is the arithmetic average:
   $$d((AB), C) = \frac{1}{|A| \cdot |B|} \sum_{x \in A} \sum_{y \in B} d(x, y) = \frac{|A| \cdot d(A, C) + |B| \cdot d(B, C)}{|A| + |B|}$$
3. The branch length leading from parent node $(AB)$ to daughter node $A$ is:
   $$\text{Branch}(A) = h(AB) - h(A)$$

---

## Worked Mathematical Example: Complete 4-Taxon UPGMA Tree Calculation

### Initial Problem:
Given a pairwise evolutionary distance matrix between four vertebrate taxa: $A, B, C, D$, representing hemoglobin beta (*HBB*) orthologues across vertebrates ($A$: Human *HBB*, $B$: Chimpanzee *HBB*, $C$: Mouse *Hbb*, $D$: Chicken *HBB*):

```
        A     B     C     D
  A     0     4     8    10
  B     4     0     8    10
  C     8     8     0     6
  D    10    10     6     0
```

---

### Step 1: Find the Closest Pair of Taxa
Scan the matrix for the minimum non-zero distance:
$$\min d(i, j) = d(A, B) = \mathbf{4}$$

1. Cluster Taxa $A$ and $B$ into composite node **$(AB)$**.
2. Calculate node height:
   $$h(AB) = \frac{d(A, B)}{2} = \frac{4}{2} = \mathbf{2.0}$$
3. Calculate branch lengths to leaves $A$ and $B$:
   $$\text{Branch}(A) = h(AB) - h(A) = 2.0 - 0 = \mathbf{2.0}$$
   $$\text{Branch}(B) = h(AB) - h(B) = 2.0 - 0 = \mathbf{2.0}$$

---

### Step 2: Recalculate Distance Matrix with Cluster $(AB)$
Calculate distances from $(AB)$ to the remaining unclustered taxa ($C$ and $D$):

$$d((AB), C) = \frac{d(A, C) + d(B, C)}{2} = \frac{8 + 8}{2} = \mathbf{8.0}$$
$$d((AB), D) = \frac{d(A, D) + d(B, D)}{2} = \frac{10 + 10}{2} = \mathbf{10.0}$$

The updated $3 \times 3$ distance matrix is:

```
          (AB)      C       D
  (AB)      0      8.0    10.0
  C        8.0      0      6.0
  D       10.0     6.0      0
```

---

### Step 3: Find the Next Closest Pair
Scan the updated matrix for the minimum distance:
$$\min d(i, j) = d(C, D) = \mathbf{6.0}$$

1. Cluster Taxa $C$ and $D$ into composite node **$(CD)$**.
2. Calculate node height:
   $$h(CD) = \frac{d(C, D)}{2} = \frac{6.0}{2} = \mathbf{3.0}$$
3. Calculate branch lengths to leaves $C$ and $D$:
   $$\text{Branch}(C) = h(CD) - h(C) = 3.0 - 0 = \mathbf{3.0}$$
   $$\text{Branch}(D) = h(CD) - h(D) = 3.0 - 0 = \mathbf{3.0}$$

---

### Step 4: Recalculate Distance Between Cluster $(AB)$ and Cluster $(CD)$
The updated distance between the two remaining clusters is:

$$d((AB), (CD)) = \frac{d(A, C) + d(A, D) + d(B, C) + d(B, D)}{|AB| \times |CD|}$$
$$d((AB), (CD)) = \frac{8 + 10 + 8 + 10}{2 \times 2} = \frac{36}{4} = \mathbf{9.0}$$

The final $2 \times 2$ distance matrix is:

```
          (AB)    (CD)
  (AB)      0      9.0
  (CD)     9.0      0
```

---

### Step 5: Merge the Final Two Clusters to Form the Root Node
1. Merge cluster $(AB)$ and cluster $(CD)$ to create the **Root Node** $((AB), (CD))$.
2. Calculate Root height:
   $$h(\text{Root}) = \frac{d((AB), (CD))}{2} = \frac{9.0}{2} = \mathbf{4.5}$$
3. Calculate internal branch lengths connecting the Root to internal nodes $(AB)$ and $(CD)$:
   $$\text{Branch}((AB)) = h(\text{Root}) - h(AB) = 4.5 - 2.0 = \mathbf{2.5}$$
   $$\text{Branch}((CD)) = h(\text{Root}) - h(CD) = 4.5 - 3.0 = \mathbf{1.5}$$

---

### Step 6: Construct and Verify the Ultrametric Tree

```
  Height Scale:
  0.0                      2.0             3.0                      4.5 (Root)
   |                        |               |                         |
   Leaf A ------------------+ (Branch = 2.0)                          |
                            |                                         |
   Leaf B ------------------+ (Branch = 2.0)                          |
                            |                                         |
                            +-----------------------------------------+ (Branch = 2.5)
                                                                      |
                            +-----------------------------------------+ (Branch = 1.5)
                            |
   Leaf C ------------------+ (Branch = 3.0)
                            |
   Leaf D ------------------+ (Branch = 3.0)
```

#### Newick Representation with Branch Lengths:
$$\texttt{(((A:2.0, B:2.0):2.5, (C:3.0, D:3.0):1.5):0.0);}$$

#### Verification of the Ultrametric Molecular Clock:
Total patristic distance from Root to any terminal leaf must be identical:
- Path to $A$: $2.5 + 2.0 = \mathbf{4.5}$
- Path to $B$: $2.5 + 2.0 = \mathbf{4.5}$
- Path to $C$: $1.5 + 3.0 = \mathbf{4.5}$
- Path to $D$: $1.5 + 3.0 = \mathbf{4.5}$
All terminal leaves are exactly 4.5 units of evolutionary distance from the root.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A bioinformatician performs Jukes-Cantor distance correction on an alignment of two diverged viral genomes and calculates an observed mismatch proportion of $p = 0.78$. What will happen when this value is plugged into the Jukes-Cantor equation? What is the biological meaning of this result?

**Model Answer:**
- **Mathematical Result:** The formula $d = -\frac{3}{4} \ln(1 - \frac{4}{3} p)$ will fail because $1 - \frac{4}{3}(0.78) = 1 - 1.04 = -0.04$. The natural logarithm of a negative number is undefined ($\text{NaN}$ or $-\infty$).
- **Biological Meaning:** A divergence of $p = 78\%$ exceeds the maximum theoretical saturation threshold for a 4-letter nucleotide alphabet ($75\%$). The sequences have undergone complete mutational saturation (every site has mutated multiple times), obliterating all phylogenetic signal. The two sequences are statistically indistinguishable from random noise.

---

### Question 2
**Prompt:** Explain why the Neighbor-Joining (NJ) algorithm is vastly superior to UPGMA when analyzing real biological sequence datasets from diverse organisms (such as humans, birds, and lungfish).

**Model Answer:**
UPGMA strictly assumes a **constant molecular clock** (ultrametric evolution), meaning every lineage must mutate at the exact same evolutionary rate over time. In real biology, different organismal lineages mutate at vastly different rates due to differences in metabolic rate, generation time, and DNA polymerase proofreading fidelity. When evolutionary rates vary, UPGMA clusters fast-evolving lineages incorrectly, producing distorted topologies. **Neighbor-Joining does not assume a molecular clock**: its $Q$-matrix algorithm subtracts the total divergence of each taxon, allowing lineages to possess unequal branch lengths and correctly resolving true phylogenetic relationships.

---

### Question 3
**Prompt:** In the context of Maximum Parsimony, what is an "informative site" in a multiple sequence alignment? Give an example of a 4-taxon alignment column that is informative versus one that is uninformative.

**Model Answer:**
- **Definition:** An **informative site** is an alignment column that contains at least two different character states (residues), each of which is present in at least two different taxa. Only informative sites can distinguish between alternative tree topologies under the parsimony criterion.
- **Informative Column Example:**
  Taxon 1: `A`, Taxon 2: `A`, Taxon 3: `G`, Taxon 4: `G`.  
  *(Contains two states: `A` and `G`, each appearing in 2 taxa. This column supports grouping Taxon 1 with 2 against Taxon 3 with 4).*
- **Uninformative Column Example:**
  Taxon 1: `A`, Taxon 2: `A`, Taxon 3: `A`, Taxon 4: `G`.  
  *(Contains a singleton mutation. Every possible tree topology requires exactly one mutational step to explain this column; therefore, it cannot distinguish between topologies).*
