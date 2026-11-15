# Lecture 10 — Biological Basis and Dot Plots

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 5:** Sequence Alignment and Database Searching  
**Syllabus Topic:** Introduction, Evolutionary Basis of Sequence Alignment, Optimal alignment method  
**Primary Learning Outcome:** LO3 — Explain global, local, and heuristic alignment, and interpret dot plots and sequence homology.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Why Align Biological Sequences?
================================================================================
Topic: The Rosetta Stone of Molecular Biology

[Visual: Two aligned protein strings showing conserved residues (*) and mutations (: .)
  HBB_HUMAN   VHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFESFGDLSTPDAVMGNPK
              |||||:||:|| |||||||||| ||||||||||||||||||||||||||:|||||||||
  HBB_CHIMP   VHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFESFGDLSSPDAVMGNPK]

Speaker Bullets:
* Sequence alignment is the single most fundamental algorithm in bioinformatics.
* Primary sequences are evolutionary tapes: mutations accumulate over millions of years.
* Alignment places homologous residues into equivalent vertical columns to reveal
  functional constraints, catalytic active sites, and phylogenetic history.
```

```
================================================================================
SLIDE 2: Homology vs Similarity vs Identity
================================================================================
Topic: Clarifying the Most Abused Vocabulary in Biology

+--------------------+-------------------------+------------------------------+
| Term               | Nature of Definition    | Quantifiability              |
+--------------------+-------------------------+------------------------------+
| **Identity**       | Mathematical Fact       | Exact percentage (e.g. 78%)  |
| **Similarity**     | Physicochemical Score   | Metric from scoring matrix   |
| **Homology**       | Evolutionary Hypothesis | **BINARY**: Yes or No!       |
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* Two sequences are either homologous (descended from a common ancestor) or they are not.
* It is biologically nonsensical to state: "these genes are 70% homologous"!
* Correct phrasing: "These sequences share 70% identity and are inferred to be homologous."
```

```
================================================================================
SLIDE 3: The Tree of Homology: Orthologues, Paralogues, Xenologues
================================================================================
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

Speaker Bullets:
* **Orthologues:** Genes separated by a **speciation event** (Human Beta vs Mouse Beta).
  Usually retain identical biological function.
* **Paralogues:** Genes separated by a **gene duplication event** (Human Alpha vs Human Beta).
  Often evolve new functions (neo-functionalization) or split tasks (sub-functionalization).
* **Xenologues:** Genes acquired through **horizontal gene transfer (HGT)**.
```

```
================================================================================
SLIDE 4: Mutational Mechanisms: Substitutions and Indels
================================================================================
Topic: How Sequences Diverge

1. Substitutions (Point Mutations):
   * Transitions: Purine <-> Purine (A <-> G) or Pyrimidine <-> Pyrimidine (C <-> T).
   * Transversions: Purine <-> Pyrimidine (e.g., A <-> T in HbS Glu6Val!).
   * Evolutionary constraint: Transitions are biochemically ~2x more frequent than transversions.

2. Indels (Insertions and Deletions):
   * Caused by DNA replication slippage or unequal recombination.
   * In coding exons, indels that are not multiples of 3 cause catastrophic frameshifts.
   * In sequence alignments, indels are represented as gap characters (`-`).

Speaker Bullets:
* Alignments must penalize indels because creating an insertion/deletion disrupts
  the reading frame and macromolecular backbone geometry.
```

```
================================================================================
SLIDE 5: The First Visual Alignment: The Dot Plot
================================================================================
Topic: 2D Matrix Visualization (Gibbs & McIntyre, 1970)

  Sequence 2 ->  V   H   L   T   P   E
  Sequence 1 v
      V          *
      H              *
      L                  *
      T                      *
      P                          *
      E                              *

Speaker Bullets:
* A 2D grid where Sequence 1 labels the rows and Sequence 2 labels the columns.
* In the simplest dot plot, place a dot at position $(i, j)$ if residue $S_1[i] == S_2[j]$.
* Perfect identity produces an unbroken diagonal line from top-left to bottom-right.
```

```
================================================================================
SLIDE 6: Filtering Noise: Window Size (w) and Stringency (s)
================================================================================
Topic: Eliminating Spurious Random Matches

[Visual: Unfiltered Dot Plot (solid field of random dots)
         vs Filtered Window Dot Plot (crisp, clean diagonal lines)]

Algorithm:
  A dot is plotted at the center of window `w` ONLY if at least `s` residues match!
  Example: Window = 5, Stringency = 4 (at least 4 out of 5 residues must match).

Speaker Bullets:
* In large sequences, individual amino acids match by random chance (1 in 20).
* A sliding window calculates local similarity, suppressing random background noise
  while preserving significant evolutionary signals.
```

```
================================================================================
SLIDE 7: Interpreting Biological Patterns in Dot Plots
================================================================================
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

Speaker Bullets:
* Dot plots are unbeatable for rapid visual discovery of large-scale genomic rearrangements.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 10

* Alignment reflects evolutionary descent with modification.
* Homology is binary; similarity and identity are quantifiable measurements.
* Orthologues diverge by speciation; paralogues diverge by duplication.
* Dot plots provide the first 2D visual map of sequence relationships.
* Next Lecture: Optimal Global Alignment — The Needleman-Wunsch algorithm worked
  by hand step by step!
```

---

## Detailed Comprehensive Technical Notes

### 1. The Evolutionary Basis of Sequence Alignment

The core premise of molecular evolution is **descent with modification**. When an ancestral biological sequence replicates over generations, its nucleotide tape is subject to spontaneous chemical alterations and enzymatic replication errors:

$$\text{Ancestral Sequence } S_0 \xrightarrow{\text{Mutations + Natural Selection}} \text{Modern Sequences } S_1, S_2$$

Natural selection acts as an evolutionary filter:
- **Deleterious mutations:** Amino acid substitutions that disrupt critical active-site residues, destabilize the hydrophobic core, or introduce premature stop codons decrease organismal fitness and are purged by negative (purifying) selection.
- **Neutral mutations:** Substitutions that exchange biochemically similar amino acids (e.g., Leucine to Isoleucine, or Glutamate to Aspartate) or mutations residing in non-conserved, solvent-exposed loops often have minimal phenotypic effect and drift to fixation via neutral genetic drift.
- **Beneficial mutations:** Rare alterations that confer novel adaptive advantages (e.g., altered oxygen affinity or pathogen resistance) are favored by positive selection.

When we align modern sequences, our computational objective is to **reconstruct historical evolutionary homology**: placing residues into vertical columns that share a common ancestral origin.

---

### 2. Homology vs Similarity vs Identity: Rigorous Definitions

In scientific writing and examinations, confusing these three concepts is a major technical error:

```
  Concept       Nature of Terminology          Operational Definition
  -------------------------------------------------------------------------------------------------
  Identity      Objective Mathematical Fact    The exact percentage of identical, unmutated residues 
                                               aligned in matching positions:
                                               Identity % = (Identical Matches / Alignment Length) * 100

  Similarity    Quantitative Physicochemical   The percentage of aligned residues that share similar
                Score                          biochemical properties (charge, size, hydrophobicity)
                                               as evaluated by a substitution scoring matrix.

  Homology      Evolutionary Inference /       The biological conclusion that two sequences are 
                Hypothesis                     descended from a common ancestral sequence.
                                               Homology is strictly qualitative and BINARY.
```

#### The Grammatical Fallacy of "Percentage Homology":
Two genes are either homologous, or they are not. Just as two human beings cannot be "60% pregnant" or "75% biological siblings", two sequences cannot be "70% homologous". They share **70% sequence identity**, from which we infer with high statistical confidence that they are **homologous**.

---

### 3. The Taxonomy of Homology: Orthologues, Paralogues, Xenologues

When two homologous sequences are compared, their evolutionary divergence can arise through three distinct biological mechanisms (defined by Walter Fitch in 1970):

```
                                 Ancestral Globin
                                        |
                            [Duplication Event: ~500 Mya]
                                        |
                     +------------------+------------------+
                     |                                     |
                Alpha-Chain                            Beta-Chain
                     |                                     |
             [Speciation Event]                    [Speciation Event]
              /              \                      /              \
         Human Alpha    Chimp Alpha            Human Beta     Chimp Beta
```

1. **Orthologues:**  
   Homologous genes in different species that diverged as a direct consequence of a **speciation event**.  
   *Example:* Human beta-globin (*HBB*) and Chimpanzee beta-globin (*HBB*).  
   *Functional Consequence:* Orthologues typically retain identical biological functions, substrate specificities, and physiological roles. When transferring functional annotation across genomes, orthologues are the only reliable conduits.
2. **Paralogues:**  
   Homologous genes that diverged as a consequence of an intra-genomic **gene duplication event**.  
   *Example:* Human alpha-globin (*HBA1*) and Human beta-globin (*HBB*), which duplicated over 450 million years ago.  
   *Functional Consequence:* Following duplication, selective constraints on one copy are relaxed. Paralogues often diverge into specialized sub-functions (sub-functionalization, e.g., fetal gamma-globin *HBG1* having higher oxygen affinity than adult *HBB*) or evolve entirely novel functions (neo-functionalization).
3. **Xenologues:**  
   Homologous sequences that diverged via **Horizontal Gene Transfer (HGT)** between distinct species, bypassing vertical organismal reproduction (frequent in prokaryotes acquiring antibiotic resistance plasmids).

---

### 4. Dot Plots: 2D Matrix Comparison

The **Dot Plot** (introduced by A. J. Gibbs and G. A. McIntyre in 1970) is the earliest computational technique for comparative sequence analysis.

#### Mathematical Formulation:
Let sequence $X = x_1 x_2 \dots x_m$ and sequence $Y = y_1 y_2 \dots y_n$. A dot plot is a discrete 2D matrix $M$ of dimensions $m \times n$:

$$M(i, j) = \begin{cases} 1 \text{ (plot a dot)} & \text{if } x_i = y_j \\ 0 \text{ (blank space)} & \text{if } x_i \neq y_j \end{cases}$$

#### The Signal-to-Noise Problem:
For two random protein sequences over an alphabet of 20 amino acids, the background probability of two random residues matching is:
$$P(\text{random match}) = \sum_{k=1}^{20} p_k^2 \approx \frac{1}{20} = 5\%$$
For two 1,000-amino acid proteins, an unfiltered dot plot contains approximately $1000 \times 1000 \times 0.05 = \mathbf{50,000\text{ random noise dots}}$, completely obscuring subtle diagonals.

#### The Sliding Window and Stringency Filter:
To suppress noise, a sliding window of length $w$ (where $w$ is odd) and a stringency threshold $s \le w$ are applied:
A dot is placed at the center coordinate $\left(i + \frac{w-1}{2}, j + \frac{w-1}{2}\right)$ if and only if:
$$\sum_{k=0}^{w-1} \delta(x_{i+k}, y_{j+k}) \ge s$$
where $\delta(a, b) = 1$ if $a=b$, and $0$ otherwise.

```
  Window Parameter Selection Guidelines:
  * For finding closely related sequences: Window = 5, Stringency = 4 or 5
  * For identifying distantly related homologs: Window = 15 to 21, Stringency = 7 to 9
  * For nucleotide dot plots: Window = 11 to 21, Stringency = 14 to 18 (due to 4-letter alphabet)
```

---

### 5. Biological Signatures in Dot Plots

```
  Pattern Schematic                 Visual Appearance              Biological Event
  -------------------------------------------------------------------------------------------------
  Main Diagonal                     Continuous line from (1,1)     Unbroken sequence identity / 
                                    to (m, n)                      strong evolutionary conservation
  Shifted Parallel Diagonal         Line offset horizontally       Internal sequence duplication
                                    or vertically from main        or tandem repeat arrays
  Horizontal / Vertical Gap         Diagonal breaks, steps         Insertion or Deletion (Indel)
                                    sideways, then resumes         in one of the sequences
  Perpendicular Line                Anti-diagonal line forming     Chromosomal Inversion
  (Anti-diagonal)                   an 'X' across the main         (reverse-complement match)
  Blank Interruption                Gap along the diagonal         Variable loop region or 
                                                                   non-conserved domain
```

---

## Worked Example: Hand Construction of a Dot Plot

### Objective:
Construct an unfiltered dot plot comparing two short peptides:
- **Sequence 1 ($X$ - Rows):** `V H L T P E` (Human HbA wild-type fragment)
- **Sequence 2 ($Y$ - Columns):** `V H L T P V` (Human HbS sickle-cell fragment)

```
        Y ->    V     H     L     T     P     V
  X v
  ------------------------------------------------
  V    (1)  |   *     .     .     .     .     *
  H    (2)  |   .     *     .     .     .     .
  L    (3)  |   .     .     *     .     .     .
  T    (4)  |   .     .     .     *     .     .
  P    (5)  |   .     .     .     .     *     .
  E    (6)  |   .     .     .     .     .     .
```

### Observations and Biological Interpretation:
1. **The Conserved Diagonal:** Positions $(1,1), (2,2), (3,3), (4,4), (5,5)$ form an unbroken diagonal line representing the conserved `V-H-L-T-P` tract.
2. **The Terminal Mismatch:** At position $(6,6)$, there is no dot because $X[6] = \text{'E'}$ while $Y[6] = \text{'V'}$. The diagonal terminates, visually marking the point mutation.
3. **Off-Diagonal Match (Noise):** Notice the dot at coordinate $(1, 6)$! $X[1] = \text{'V'}$ matches $Y[6] = \text{'V'}$. This is a spurious off-diagonal match caused by the amino acid alphabet repetition. In an unfiltered plot, such dots create visual clutter.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A biotechnology journal manuscript claims: *"Gene X from zebrafish is 82% homologous to human TP53."* As a peer reviewer, write a two-sentence correction explaining the biological error and providing the correct terminology.

**Model Answer:**
The statement is scientifically erroneous because homology is a qualitative, binary evolutionary condition (two genes either share common ancestry or they do not; genes cannot be partially homologous). The sentence should be corrected to read: *"Gene X from zebrafish shares 82% sequence identity with human TP53, indicating that they are homologous orthologues."*

---

### Question 2
**Prompt:** You run a self-comparison dot plot of a 2,000-bp human genomic DNA sequence against itself ($X = Y$). In addition to the main diagonal running from $(1,1)$ to $(2000, 2000)$, you observe four equally spaced parallel diagonal lines shifted 200 base pairs away from the main diagonal. What biological structure is present in this genomic region?

**Model Answer:**
The presence of equally spaced parallel diagonal lines shifted off the main diagonal indicates a **tandem repeat array** (direct repeats). The 200-bp offset indicates that a 200-base pair sequence element has been duplicated multiple times in tandem within this locus.

---

### Question 3
**Prompt:** Why does a nucleotide dot plot require a much larger window size (e.g., $w=15, s=12$) than an amino acid dot plot (e.g., $w=5, s=4$) to achieve equivalent signal-to-noise clarity?

**Model Answer:**
Nucleic acids are composed of an alphabet of only 4 bases ($\Sigma = \{A, C, G, T\}$), giving an expected random match probability of $P = 4 \times (0.25)^2 = 0.25$ (a 25% chance of two random bases matching). Proteins utilize an alphabet of 20 amino acids, where the random match probability is only $\approx 5\%$. Because random nucleotide background noise is five times higher, nucleotide dot plots require significantly wider sliding windows and higher stringency thresholds to filter out spurious random matches.
