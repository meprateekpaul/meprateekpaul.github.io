# Lecture 18 — Trees, Orthologues, and Paralogues

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 7:** Phylogenetic Analysis  
**Syllabus Topic:** Fundamental of Phylogenetic model, Tree interpretation - Paralogues and orthologues  
**Primary Learning Outcome:** LO5 — Build phylogenetic trees, interpret tree topology, and distinguish orthologues from paralogues on the globin tree.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Evolutionary Graph
================================================================================
Topic: Reconstructing the History of Life

[Visual: A rooted phylogenetic tree of globin genes:
  Root (500 Mya) 
    |-- Myoglobin (MB)
    `-- Hemoglobin Ancestor
          |-- Alpha-Globin Cluster (Chr 16)
          `-- Beta-Globin Cluster (Chr 11: Epsilon, Gamma, Delta, Beta)]

Speaker Bullets:
* Nothing in biology makes sense except in the light of evolution (Theodosius Dobzhansky).
* Phylogenetic trees are mathematical graph structures representing the genealogical
  history of genes, genomes, and species.
* Today's focus: Nodes, branches, root placement, and reading orthologues vs paralogues.
```

```
================================================================================
SLIDE 2: Anatomical Elements of a Phylogenetic Tree
================================================================================
Topic: The Graph Theory Vocabulary

+--------------------+-------------------------+------------------------------+
| Element            | Graph Theory Component  | Biological Meaning           |
+--------------------+-------------------------+------------------------------+
| **Terminal Node**  | Leaf / Tip (Degree 1)   | Extant sequences / taxa      |
| **Internal Node**  | Vertex (Degree >= 3)    | Hypothetical common ancestor |
| **Branch (Edge)**  | Directed or Undirected  | Evolutionary lineage         |
| **Branch Length**  | Weight / Metric         | Amount of genetic divergence |
| **Root**           | In-degree 0             | Most recent common ancestor  |
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* In a bifurcating tree, every internal node splits into exactly two daughter branches.
* A **Polytomy** (multifurcation) occurs when an internal node splits into >= 3 branches,
  indicating an unresolved evolutionary divergence or rapid explosive radiation.
```

```
================================================================================
SLIDE 3: Clades and Monophyly
================================================================================
Topic: Defining Evolutionary Groups

[Visual: Monophyletic Clade (Ancestor + ALL descendants enclosed in a loop)
         vs Paraphyletic Group (Ancestor + SOME descendants; e.g. Reptiles without birds)
         vs Polyphyletic Group (Grouped by convergent trait without common ancestor)]

Speaker Bullets:
* **Monophyletic Group (Clade):** An ancestor and ALL of its evolutionary descendants.
  This is the ONLY biologically valid grouping in modern cladistics!
* All vertebrate beta-globins form a strictly monophyletic clade.
```

```
================================================================================
SLIDE 4: Rooted vs Unrooted Trees
================================================================================
Topic: The Direction of Time

  Unrooted Tree:                           Rooted Tree:
       Taxon A       Taxon C                     Root (Time = 0)
          \         /                               |
           \       /                         +------+------+
            Node 1                           |             |
           /      \                       Node 1        Node 2
          /        \                      /    \        /    \
     Taxon B      Taxon D             Taxon A Taxon B Taxon C Taxon D
  (Shows branching order ONLY;        (Establishes the arrow of time:
   direction of time is UNKNOWN)       past to present!)

Speaker Bullets:
* Most tree-building algorithms (e.g. Neighbor-Joining) output UNROOTED trees.
* An unrooted tree specifies kinship, but cannot distinguish ancestors from descendants!
```

```
================================================================================
SLIDE 5: Rooting the Tree: Outgroup vs Midpoint Rooting
================================================================================
Topic: How to Place the Root

1. Outgroup Rooting (The Gold Standard):
   * Include a taxon known from independent fossil/morphological evidence to have
     branched off BEFORE all other taxa in the dataset.
   * Example: Use human **Myoglobin (*MB*)** as an outgroup to root the **Beta-Globin** family.
   * The root is placed at the branch connecting the outgroup to the ingroup.

2. Midpoint Rooting (The Heuristic Fallback):
   * Calculate all pairwise path lengths between all terminal leaves.
   * Find the two leaves separated by the longest total path.
   * Place the root at the exact halfway point along this longest path (assumes molecular clock).

Speaker Bullets:
* Always use an authentic biological outgroup whenever one is available!
```

```
================================================================================
SLIDE 6: Tree Styles: Cladogram vs Phylogram vs Chronogram
================================================================================
Topic: What Do the Branch Lengths Mean?

+---------------+--------------------+----------------------------------------+
| Style         | Branch Length Scale| Meaning of Horizontal Spacing          |
+---------------+--------------------+----------------------------------------+
| **Cladogram** | Arbitrary          | Shows TOPOLOGY ONLY; lengths mean zero.|
| **Phylogram** | Metric (Subst/site)| Length represents accumulated mutations|
| **Chronogram**| Geologic Time (Mya)| Ultrametric; all extant tips line up!  |
+---------------+--------------------+----------------------------------------+

Speaker Bullets:
* Never interpret branch lengths on a cladogram as evolutionary time!
* On a phylogram, a long branch indicates rapid evolutionary divergence.
```

```
================================================================================
SLIDE 7: Gene Trees vs Species Trees
================================================================================
Topic: The Peril of Assuming They Are Identical

[Visual: A gene duplication event occurring inside an ancestral species lineage:
  Species lineage splits -> But gene tree retains two paralogous copies!
  If copy 1 is lost in Species A and copy 2 is lost in Species B:
  The gene tree contradicts the true species tree!]

Speaker Bullets:
* A **Gene Tree** reconstructs the history of a specific genetic locus.
* A **Species Tree** reconstructs the history of reproductive organismal populations.
* Discordance arises from: Gene Duplication & Loss, Incomplete Lineage Sorting (ILS),
  and Horizontal Gene Transfer (HGT).
```

```
================================================================================
SLIDE 8: Summary & The Globin Family Tree
================================================================================
Topic: Core Concepts from Lecture 18

* Monophyletic clades unite a common ancestor with all descendants.
* Unrooted trees show topological proximity; outgroups establish the arrow of time.
* Human HBB and Chimp HBB are **Orthologues** (separated by speciation).
* Human HBB and Human HBA1 are **Paralogues** (separated by gene duplication).
* Next Lecture: Tree Building — UPGMA distance clustering worked by hand and
  Neighbor-Joining.
```

---

## Detailed Comprehensive Technical Notes

### 1. Graph Theoretical Foundations of Phylogenetics

A **phylogenetic tree** is a specialized mathematical graph $T = (V, E)$ consisting of a set of vertices (nodes) $V$ and a set of edges (branches) $E$, satisfying the following properties:
1. **Acyclicity:** The graph contains no closed loops or cycles (every path between two nodes is unique).
2. **Connectedness:** There is a path connecting any two nodes.
3. **Degree Constraints:**
   - **Terminal Nodes (Leaves / Taxa / OTUs):** Have a degree of 1 (connected to exactly one branch). They represent extant, sequenced organisms or genes.
   - **Internal Nodes (HTUs - Hypothetical Taxonomic Units):** Have a degree $\ge 3$ in unrooted bifurcating trees, or degree 2 at the root of a rooted tree. They represent extinct common ancestors where evolutionary lineages diverged.

```
  Graph Terminology      Phylogenetic Equivalent        Biological Interpretation
  -------------------------------------------------------------------------------------------------
  Leaf / Tip             Terminal Node / OTU            Modern sequenced gene (e.g. human HBB)
  Internal Vertex        Internal Node / HTU            Hypothetical ancestral divergence event
  Edge                   Branch                         Lineage accumulating substitutions over time
  Edge Weight            Branch Length                  Evolutionary divergence (substitutions/site)
  Root Vertex            Root                           Most Recent Common Ancestor (MRCA) of all taxa
```

---

### 2. Clades and Monophyly

Phylogenetic classification is based on the cladistic principles formalized by Willi Hennig (1966):

```
                       +--- Taxon A \
                   +---|             >-- MONOPHYLETIC CLADE (A + B + C + Ancestor)
                   |   +--- Taxon B /
             +-----|
             |     +------- Taxon C
       Root -|
             |     +------- Taxon D \
             +-----|                 >-- PARAPHYLETIC GROUP (Ancestor + D, excluding E)
                   +------- Taxon E /
```

1. **Monophyletic Group (Clade):**  
   A taxonomic group containing an ancestor and **ALL** of its evolutionary descendants. In modern evolutionary taxonomy, only monophyletic groups are recognized as natural biological clades (e.g., Mammalia, Aves, or the vertebrate beta-globin family).
2. **Paraphyletic Group:**  
   A group containing a common ancestor and **SOME, but not all**, of its descendants. The classic example is "Class Reptilia": reptiles include turtles, lizards, and crocodiles, but artificially exclude birds (Aves), even though crocodiles are more closely related to birds than they are to lizards.
3. **Polyphyletic Group:**  
   A group whose members do not share a recent common ancestor, grouped together by convergent, independently evolved phenotypic traits (e.g., grouping bats, birds, and insects together into "flying animals").

---

### 3. The Combinatorics of Tree Space

Why is phylogenetic tree reconstruction mathematically challenging? The number of possible tree topologies expands factorially as the number of taxa ($n$) increases.

For $n$ taxa:

#### A. Number of Unrooted Trees ($N_U$):
$$N_U = \prod_{k=3}^{n} (2k - 5) = 1 \times 3 \times 5 \times \dots \times (2n - 5) = \frac{(2n - 5)!}{2^{n-3}(n - 3)!}$$

#### B. Number of Rooted Trees ($N_R$):
Because a root can be placed on any of the $(2n - 3)$ branches of an unrooted tree:
$$N_R = (2n - 3) \times N_U = \prod_{k=2}^{n} (2k - 3) = \frac{(2n - 3)!}{2^{n-2}(n - 2)!}$$

```
  Number of Taxa (n)     Number of Unrooted Trees (N_U)     Number of Rooted Trees (N_R)
  -------------------------------------------------------------------------------------------------
  n = 3                  1                                  3
  n = 4                  3                                  15
  n = 5                  15                                 105
  n = 6                  105                                945
  n = 10                 2,027,025                          34,459,425
  n = 20                 2.22 * 10^20                       8.20 * 10^21
  n = 50                 2.84 * 10^74                       2.75 * 10^76
```

For a modest dataset of 50 homologous globin sequences, the number of possible rooted tree topologies ($\approx 10^{76}$) approaches the total number of atoms in the observable universe. This mathematical reality proves that **exhaustive tree searching is impossible**, requiring heuristic optimization algorithms (such as tree-bisection and reconnection [TBR] or genetic algorithms).

---

### 4. Rooting Methodologies

Most distance-matrix and maximum-likelihood algorithms construct **unrooted trees** because calculating unrooted branch lengths requires evaluating fewer parameters:

```
  Unrooted 4-Taxon Topology:
        HBB_HUMAN            HBB_CHIMP
            \               /
             \    Branch   /
              Node 1-----Node 2
             /             \
            /               \
       HBD_HUMAN          MB_HUMAN
```

To establish the temporal direction of evolution (which lineage branched first), the tree must be **rooted**:

1. **Outgroup Rooting:**  
   The investigator includes an **outgroup**—a taxon known from paleontological, morphological, or independent genetic evidence to have diverged prior to the divergence of all the sequences of interest (the **ingroup**). The root is mathematically placed on the internal branch connecting the outgroup to the ingroup.  
   *Example:* When studying the human $\beta$-globin locus (*HBB*, *HBD*, *HBG*, *HBE*), human **myoglobin (*MB*)** is chosen as the outgroup because myoglobin duplicated $\approx 500\text{ Mya}$, long before the tandem duplications that generated the beta-like globins.
2. **Midpoint Rooting:**  
   If no authentic outgroup exists, midpoint rooting identifies the pair of leaves separated by the greatest patristic branch distance (the longest path across the tree) and places the root at the exact geographic midpoint of that path. *Limitation:* It strictly assumes a constant, uniform rate of evolutionary mutation (a strict molecular clock) across all lineages.

---

### 5. Gene Trees vs Species Trees: Mechanisms of Incongruence

A common pitfall in bioinformatics is equating a **Gene Tree** directly to a **Species Tree**:
- A **Species Tree** depicts the historical divergence, isolation, and speciation of reproductive organismal populations.
- A **Gene Tree** depicts the historical divergence of a specific nucleotide or protein locus.

Gene trees frequently conflict with species trees due to three biological processes:
1. **Gene Duplication and Loss:** If an ancient gene duplicates into Paralogs 1 and 2, and subsequently Paralog 1 is pseudogenized or deleted in Species A while Paralog 2 is deleted in Species B, an investigator comparing the surviving copies will reconstruct an erroneous tree topology.
2. **Incomplete Lineage Sorting (ILS / Deep Coalescence):** If the ancestral population possesses high allelic polymorphism and two speciation events occur in rapid succession, ancestral alleles may fail to coalesce prior to speciation, resulting in a gene tree topology that differs from the species branching order.
3. **Horizontal Gene Transfer (HGT) / Hybridization:** Common in bacteria, archaea, and plants, where genes are transferred horizontally across species boundaries.

---

## Worked Example: Calculating Tree Space for 4 Globin Taxa

### Problem:
Consider $n = 4$ taxa:
- Taxon 1: `HBB_HUMAN`
- Taxon 2: `HBB_CHIMP`
- Taxon 3: `HBD_HUMAN`
- Taxon 4: `MB_HUMAN` (Outgroup)

1. Calculate the exact number of possible unrooted tree topologies.
2. Calculate the exact number of possible rooted tree topologies.
3. Draw/sketch all possible unrooted topologies using Newick-style parentheses.

---

### Step 1: Calculate Number of Unrooted Trees ($N_U$)
$$N_U = \frac{(2n - 5)!}{2^{n-3}(n - 3)!}$$
For $n = 4$:
$$N_U = 2(4) - 5 = 8 - 5 = 3\text{ unrooted trees}$$

---

### Step 2: Calculate Number of Rooted Trees ($N_R$)
$$N_R = (2n - 3) \times N_U = (2(4) - 3) \times 3 = 5 \times 3 = \mathbf{15\text{ rooted trees}}$$

---

### Step 3: Enumerate the 3 Distinct Unrooted Topologies
In an unrooted 4-taxon tree, an internal branch partitions the 4 taxa into two pairs:

- **Topology 1:** Clusters `(HUMAN, CHIMP)` together against `(DELTA, MYOGLOBIN)`:
  $$\text{Newick: } \texttt{((HBB\_HUMAN, HBB\_CHIMP), (HBD\_HUMAN, MB\_HUMAN));}$$
- **Topology 2:** Clusters `(HUMAN, DELTA)` together against `(CHIMP, MYOGLOBIN)`:
  $$\text{Newick: } \texttt{((HBB\_HUMAN, HBD\_HUMAN), (HBB\_CHIMP, MB\_HUMAN));}$$
- **Topology 3:** Clusters `(HUMAN, MYOGLOBIN)` together against `(CHIMP, DELTA)`:
  $$\text{Newick: } \texttt{((HBB\_HUMAN, MB\_HUMAN), (HBB\_CHIMP, HBD\_HUMAN));}$$

**Biological Evaluation:**  
Phylogenetic algorithms evaluating globin alignments overwhelmingly support **Topology 1**, which pairs the two nearly identical beta-globins (`HBB_HUMAN` and `HBB_CHIMP`) on one side of the internal branch, and delta-globin with myoglobin on the other.

---

## Formative In-Class Checks

### Question 1
**Prompt:** In the human genome, both the alpha-globin gene (*HBA1*) and the beta-globin gene (*HBB*) are present. In the chimpanzee genome, both *HBA1* and *HBB* are also present.
1. What is the evolutionary relationship between human *HBB* and chimpanzee *HBB*?
2. What is the evolutionary relationship between human *HBA1* and human *HBB*?
3. Which of these two comparisons is reliable for predicting whether a drug targeting beta-globin in humans will also bind beta-globin in chimpanzees?

**Model Answer:**
1. **Human *HBB* vs Chimpanzee *HBB*:** They are **Orthologues** (separated by a speciation event between the human and chimp lineages $\approx 6\text{ Mya}$).
2. **Human *HBA1* vs Human *HBB*:** They are **Paralogues** (separated by an ancient gene duplication event $\approx 450\text{ Mya}$).
3. **Reliability for drug targeting:** The **orthologous pair (human HBB vs chimp HBB)** is reliable. Orthologues typically retain identical biological functions, active sites, and ligand-binding properties. Paralogues, having diverged hundreds of millions of years ago, frequently possess altered subunit binding affinities and different structural conformations.

---

### Question 2
**Prompt:** A researcher builds an unrooted phylogenetic tree of mammalian globins and notices that the branch leading to mouse beta-globin is three times longer than the branch leading to human beta-globin. What does this branch length difference indicate about the evolutionary rate in mice versus humans?

**Model Answer:**
In a phylogram, branch length represents the **amount of genetic divergence** (number of accumulated amino acid substitutions per site). The branch leading to mouse beta-globin being three times longer indicates that **mouse beta-globin has evolved at a significantly faster evolutionary rate than human beta-globin** since their divergence from their common mammalian ancestor. This is biologically consistent with mice having shorter generation times and higher metabolic rates, leading to more DNA replication cycles and mutational fixation per calendar year.

---

### Question 3
**Prompt:** Why is an unrooted phylogenetic tree incapable of identifying which taxon in a dataset is the most "primitive" or ancestral? How does outgroup rooting resolve this?

**Model Answer:**
- **Why unrooted trees fail:** An unrooted tree specifies only topological neighbor relationships and pairwise branch distances; it contains **no temporal reference point (no origin in time)**. Without a designated root, any internal node could theoretically represent the starting point of evolution, making it mathematically impossible to determine which lineages branched early versus late.
- **How outgroup rooting resolves this:** Adding a known, distantly related outgroup provides an external temporal anchor. Because the outgroup is known to have diverged before any member of the ingroup, connecting the outgroup to the unrooted tree establishes the unique position of the **root (the most recent common ancestor)**, giving a direction to time from the root outward to the tips.
