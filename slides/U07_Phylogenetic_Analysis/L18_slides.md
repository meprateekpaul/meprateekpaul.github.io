---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 18 Slides: Trees, Orthologues, and Paralogues"
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
# Lecture 18 — Trees, Orthologues, and Paralogues
### Concepts of Bioinformatics (CBBI-501)
**Unit 07:** Phylogenetic Analysis  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Evolutionary Graph

```text
Topic: Reconstructing the History of Life

[Visual: A rooted phylogenetic tree of globin genes:
  Root (500 Mya) 
    |-- Myoglobin (MB)
    `-- Hemoglobin Ancestor
          |-- Alpha-Globin Cluster (Chr 16)
          `-- Beta-Globin Cluster (Chr 11: Epsilon, Gamma, Delta, Beta)]
```

**Speaker Talking Points:**  
* Nothing in biology makes sense except in the light of evolution (Theodosius Dobzhansky).
* Phylogenetic trees are mathematical graph structures representing the genealogical
  history of genes, genomes, and species.
* Today's focus: Nodes, branches, root placement, and reading orthologues vs paralogues.

---

## Slide 2: Anatomical Elements of a Phylogenetic Tree

```text
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
```

**Speaker Talking Points:**  
* In a bifurcating tree, every internal node splits into exactly two daughter branches.
* A **Polytomy** (multifurcation) occurs when an internal node splits into >= 3 branches,
  indicating an unresolved evolutionary divergence or rapid explosive radiation.

---

## Slide 3: Clades and Monophyly

```text
Topic: Defining Evolutionary Groups

[Visual: Monophyletic Clade (Ancestor + ALL descendants enclosed in a loop)
         vs Paraphyletic Group (Ancestor + SOME descendants; e.g. Reptiles without birds)
         vs Polyphyletic Group (Grouped by convergent trait without common ancestor)]
```

**Speaker Talking Points:**  
* **Monophyletic Group (Clade):** An ancestor and ALL of its evolutionary descendants.
  This is the ONLY biologically valid grouping in modern cladistics!
* All vertebrate beta-globins form a strictly monophyletic clade.

---

## Slide 4: Rooted vs Unrooted Trees

```text
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
```

**Speaker Talking Points:**  
* Most tree-building algorithms (e.g. Neighbor-Joining) output UNROOTED trees.
* An unrooted tree specifies kinship, but cannot distinguish ancestors from descendants!

---

## Slide 5: Rooting the Tree: Outgroup vs Midpoint Rooting

```text
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
```

**Speaker Talking Points:**  
* Always use an authentic biological outgroup whenever one is available!

---

## Slide 6: Tree Styles: Cladogram vs Phylogram vs Chronogram

```text
Topic: What Do the Branch Lengths Mean?

+---------------+--------------------+----------------------------------------+
| Style         | Branch Length Scale| Meaning of Horizontal Spacing          |
+---------------+--------------------+----------------------------------------+
| **Cladogram** | Arbitrary          | Shows TOPOLOGY ONLY; lengths mean zero.|
| **Phylogram** | Metric (Subst/site)| Length represents accumulated mutations|
| **Chronogram**| Geologic Time (Mya)| Ultrametric; all extant tips line up!  |
+---------------+--------------------+----------------------------------------+
```

**Speaker Talking Points:**  
* Never interpret branch lengths on a cladogram as evolutionary time!
* On a phylogram, a long branch indicates rapid evolutionary divergence.

---

## Slide 7: Gene Trees vs Species Trees

```text
Topic: The Peril of Assuming They Are Identical

[Visual: A gene duplication event occurring inside an ancestral species lineage:
  Species lineage splits -> But gene tree retains two paralogous copies!
  If copy 1 is lost in Species A and copy 2 is lost in Species B:
  The gene tree contradicts the true species tree!]
```

**Speaker Talking Points:**  
* A **Gene Tree** reconstructs the history of a specific genetic locus.
* A **Species Tree** reconstructs the history of reproductive organismal populations.
* Discordance arises from: Gene Duplication & Loss, Incomplete Lineage Sorting (ILS),
  and Horizontal Gene Transfer (HGT).

---

## Slide 8: Summary & The Globin Family Tree

```text
Topic: Core Concepts from Lecture 18

* Monophyletic clades unite a common ancestor with all descendants.
* Unrooted trees show topological proximity; outgroups establish the arrow of time.
* Human HBB and Chimp HBB are **Orthologues** (separated by speciation).
* Human HBB and Human HBA1 are **Paralogues** (separated by gene duplication).
* Next Lecture: Tree Building — UPGMA distance clustering worked by hand and
  Neighbor-Joining.
```

