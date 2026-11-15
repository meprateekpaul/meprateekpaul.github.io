# End-Semester Examination: Concepts of Bioinformatics

**Course Code:** CBBI-501 (printed in university syllabus as CBBI-502)  
**Course Title:** Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Duration:** 3 Hours (180 Minutes)  
**Maximum Marks:** 100 Marks  
**Coverage:** Comprehensive (Units 1 to 11, weighted towards Units 5 to 11)  
**Instructions to Candidates:**
1. This paper contains THREE sections: Section A (20 Marks), Section B (40 Marks), and Section C (40 Marks).
2. Answer ALL questions in Section A.
3. Answer any EIGHT out of ten questions in Section B.
4. Answer ALL FOUR questions in Section C.
5. Non-programmable scientific calculators are permitted.

---

## Part I: Question Paper

### Section A: Objective & Direct Concept Checks (20 Marks)
*(Answer ALL twenty questions. Each question carries 1 Mark).*

1. Which internet protocol is specifically optimized for bulk file transfers of gigabyte-scale genomic flat files? `[1 Mark]`
2. In the Entrez search engine, which field tag restricts the search strictly to an author's name? `[1 Mark]`
3. What is the standard RefSeq accession prefix for a curated, non-redundant mature messenger RNA (mRNA)? `[1 Mark]`
4. In the NCBI data model, which composite data object groups a nucleotide sequence along with its translated protein products? `[1 Mark]`
5. Identify the three-letter GenBank division code assigned to bacterial sequence records. `[1 Mark]`
6. What does the delimiter `//` on a line by itself signify in a GenBank flat file? `[1 Mark]`
7. Differentiate between sequence **identity** and sequence **similarity**. `[1 Mark]`
8. In an affine gap penalty function $W(k) = W_g + (k-1)W_s$, what do $W_g$ and $W_s$ represent? `[1 Mark]`
9. Which substitution matrix is derived from un-gapped local multiple alignments clustered at 62% identity? `[1 Mark]`
10. In Karlin–Altschul statistics, what does the Expectation value ($E$-value) represent? `[1 Mark]`
11. State the primary algorithmic limitation of progressive multiple sequence alignment known as "once a gap, always a gap". `[1 Mark]`
12. In a molecular phylogenetic tree, what does an internal node represent? `[1 Mark]`
13. Which phylogenetic tree construction algorithm assumes a strict molecular clock, producing ultrametric trees? `[1 Mark]`
14. How many possible reading frames must be inspected computationally on double-stranded DNA when searching for Open Reading Frames (ORFs)? `[1 Mark]`
15. Name the purine-rich consensus sequence located upstream of the start codon that recruits ribosomes in prokaryotic mRNAs. `[1 Mark]`
16. In Expasy ProtParam, what threshold value of the **Instability Index** separates stable proteins from unstable proteins in vitro? `[1 Mark]`
17. What do square brackets `[ ]` versus curly braces `{ }` designate in PROSITE motif syntax? `[1 Mark]`
18. In an 80-column PDB coordinate file, which record type specifies the coordinates of non-polymer hetero groups such as heme and water? `[1 Mark]`
19. What does the metric **RMSD** quantify when comparing two superimposed protein 3D structures? `[1 Mark]`
20. What is the **C-value paradox** in eukaryotic genomics? `[1 Mark]`

---

### Section B: Analytical & Methodological Concepts (40 Marks)
*(Answer any EIGHT out of the following ten questions. Each question carries 5 Marks).*

21. **Primary vs Secondary Sequence Databases & INSDC Exchange (5 Marks):**  
    Contrast primary sequence databases (GenBank/ENA/DDBJ) with curated secondary databases (RefSeq, Swiss-Prot) across data provenance, redundancy, curation level, and record ownership. Explain how the daily INSDC synchronization ensures global data integrity.

22. **Entrez Inverted Index Architecture & Boolean Operations (5 Marks):**  
    Explain the internal architecture of an inverted index in Entrez (term dictionaries and posting lists of UIDs). Show how the query `HBB[GENE] AND "Homo sapiens"[ORGN]` is evaluated mathematically in linear time.

23. **The NCBI Abstract Data Model: Bioseq and Seq-feat (5 Marks):**  
    Explain why NCBI adopted ASN.1 and an object data model rather than relying purely on text flat files. Describe how a eukaryotic spliced coding sequence (CDS) is represented internally using `Bioseq`, `Seq-feat`, and `Seq-loc`.

24. **PAM vs BLOSUM Substitution Matrices (5 Marks):**  
    Compare Margaret Dayhoff's PAM matrices with Henikoff's BLOSUM matrices across underlying dataset, derivation of distant scores, and numbering convention. Which matrix from each family is optimal for detecting distant evolutionary homologues (~25% identity)?

25. **Multiple Sequence Alignment Heuristics (5 Marks):**  
    Compare ClustalW, Clustal Omega, and MUSCLE. Explain how Clustal Omega achieves scalability for $>100,000$ sequences using $mBed$ seed embedding, and explain how MUSCLE uses iterative refinement to correct early progressive gap errors.

26. **Molecular Phylogenetics: Distance vs Character Methods (5 Marks):**  
    Contrast the Neighbor-Joining (NJ) method with the Maximum Parsimony (MP) method. Explain what a "parsimony-informative site" is and describe how Long-Branch Attraction (LBA) can mislead parsimony.

27. **Eukaryotic Gene Architecture, Splicing & CpG Islands (5 Marks):**  
    Diagram a eukaryotic gene from promoter to poly(A) site, labeling the 5' cap, 5' UTR, exons, introns, branch point, invariant splice junctions (`GT...AG`), 3' UTR, and poly(A) signal (`AATAAA`). Define a CpG island and explain why CpGs are depleted in vertebrate genomes.

28. **Protein Physicochemical Profiling & Hydropathy Analysis (5 Marks):**  
    Explain how Expasy ProtParam calculates: (a) theoretical isoelectric point (pI) using the Henderson–Hasselbalch equation, (b) molar extinction coefficient ($\epsilon_{280}$), and (c) Grand Average of Hydropathicity (GRAVY). How does a Kyte–Doolittle hydropathy plot identify transmembrane alpha-helices?

29. **Protein Secondary Structure Prediction & Folding Classes (5 Marks):**  
    Explain the $Q_3$ accuracy metric. Contrast single-sequence prediction methods (Chou–Fasman and GOR IV) with profile-based machine learning methods (PSIPRED). Differentiate between the $\alpha/\beta$ and $\alpha+\beta$ structural folding classes.

30. **Genome Annotation & Synteny Mapping (5 Marks):**  
    Distinguish between **structural annotation** and **functional annotation** of a newly sequenced genome. Explain what synteny is and describe how whole-genome synteny dot-plots reveal chromosomal inversions and segmental duplications.

---

### Section C: Comprehensive Numerical, Alignment & Design Problems (40 Marks)
*(Answer ALL FOUR questions. Each question carries 10 Marks).*

31. **Optimal Dynamic Programming Hand Alignment (10 Marks):**  
    You are given two peptide fragments:  
    * **Sequence $X$ (Row):** `H - E - A - G - A - W`  
    * **Sequence $Y$ (Column):** `H - E - A - W - A - W`  

    **Scoring Scheme:**  
    * Match: $+2$  
    * Mismatch: $-1$  
    * Linear gap penalty ($d$): $-2$ per gap character  

    a) Construct and fully populate the $7 \times 7$ dynamic programming matrix for the **Needleman–Wunsch global alignment**. Show the three-way calculation for cell $(1,1)$, cell $(1,2)$, and cell $(6,6)$. `[4 Marks]`  
    b) Draw all directional traceback arrows in the matrix. Trace back from cell $(6,6)$ to cell $(0,0)$ to derive the optimal global alignment, and report the final alignment score. `[3 Marks]`  
    c) Formulate the **Smith–Waterman local alignment** recurrence relation. Explain how the zero lower bound alters matrix initialization and cell evaluation. State the score and coordinates of the maximal local alignment cell for this pair of sequences. `[3 Marks]`

32. **Step-by-Step Molecular Phylogenetic Reconstruction (10 Marks):**  
    You are given the following pairwise evolutionary distance matrix $D$ (percentage divergence) for four vertebrate globin genes ($A, B, C, D$):  

```text
       A      B      C      D
A      0      4      8     10
B      4      0      8     10
C      8      8      0      6
D     10     10      6      0
```

    a) Using the **UPGMA (Unweighted Pair Group Method with Arithmetic Mean)** algorithm, reconstruct the phylogenetic tree step by step:  
       - Show all distance matrix recalculations.  
       - Calculate the branch heights of all internal nodes. `[5 Marks]`  
    b) Draw the final ultrametric phylogenetic tree, showing all branch lengths connecting nodes and confirming that all leaf taxa are equidistant from the root. `[2 Marks]`  
    c) Explain the **molecular clock hypothesis**. Why does UPGMA produce an erroneous tree topology if one lineage evolves significantly faster than the others, and how does the Neighbor-Joining (NJ) method avoid this error? `[3 Marks]`

33. **Macromolecular Structure Parsing, Validation & Homology Modeling (10 Marks):**  
    Examine the following excerpt from a crystal structure of human beta-globin (PDB 1A3N):  

```text
REMARK   2 RESOLUTION.    1.80 ANGSTROMS.
REMARK   3 REFINEMENT.  R VALUE (WORKING SET) : 0.178
REMARK   3              FREE R VALUE          : 0.215
ATOM    489  NE2 HIS A  92      23.040  13.720  10.990  1.00 16.20           N
HETATM 1120 FE   FE  A 147      24.120  12.450   9.320  1.00 14.50          FE
```

    a) Evaluate the experimental quality of this X-ray structure: interpret the resolution ($1.80\text{ \AA}$), working $R$-value ($0.178$), and Free $R$-value ($0.215$). Explain why $R_{\text{free}}$ prevents crystallographic overfitting. `[3 Marks]`  
    b) Using the 3D Cartesian coordinates provided, calculate the exact Euclidean bond distance (in $\text{\AA}$) between the proximal histidine nitrogen `NE2` and the heme iron `FE`. State whether this distance confirms coordinate covalent binding. `[3 Marks]`  
    c) Outline the five core steps of template-based **homology modeling**. How does a **Ramachandran plot** validate backbone stereochemistry, and what threshold percentage of residues in the core favored region defines a reliable model? `[4 Marks]`

34. **Comparative Genomics, Pathogenicity Islands & Horizontal Gene Transfer (10 Marks):**  
    A public health genomics lab investigates an emerging multidrug-resistant bacterial pathogen isolated from an intensive care unit.  
    a) Outline the computational workflow to assemble, structurally annotate (e.g., via Prokka), and functionally annotate (via BLAST, Pfam, and KEGG) the bacterial genome from raw Illumina paired-end reads. `[3 Marks]`  
    b) Describe how you would conduct comparative pan-genome analysis (e.g., using Roary) against a benign reference strain to partition the genome into **core** vs **accessory** genes. Why are antibiotic resistance genes typically found in the accessory genome? `[3 Marks]`  
    c) Synteny mapping reveals a 45 kb genomic region present exclusively in the pathogen. Detail three distinct computational lines of evidence (GC-skew, codon usage, flanking repeats/tRNAs) that would prove this region is a horizontally acquired **Pathogenicity Island (PAI)**. `[4 Marks]`

---
---

## Part II: Complete Model Answer Paper & Scoring Key

### Section A: Objective Model Answers (20 Marks)
1. **Bulk Transfer Protocol:** FTP (File Transfer Protocol) / rsync. `[1 Mark]`
2. **Author Field Tag:** `[AUTH]` (or `[Author]`). `[1 Mark]`
3. **Curated RefSeq mRNA Prefix:** `NM_`. `[1 Mark]`
4. **Composite Nucleotide-Protein Container:** `Bioseq-set` (specifically a `nuc-prot` set). `[1 Mark]`
5. **Bacterial Division Code:** `BCT`. `[1 Mark]`
6. **Meaning of `//`:** End of record delimiter. `[1 Mark]`
7. **Identity vs Similarity:** Identity is the exact match of identical residues; similarity includes conservative substitutions with positive matrix scores. `[1 Mark]`
8. **Affine Gap Terms:** $W_g$ is the gap opening penalty; $W_s$ is the gap extension penalty. `[1 Mark]`
9. **BLOSUM Matrix at 62% Identity:** `BLOSUM62`. `[1 Mark]`
10. **$E$-value Definition:** The expected number of random chance alignments with a score $\ge S$ in a database of size $N$. `[1 Mark]`
11. **"Once a Gap, Always a Gap":** In progressive alignment, gaps introduced in early alignments are permanently frozen and cannot be repositioned as more sequences are added. `[1 Mark]`
12. **Internal Node Biological Meaning:** The hypothetical most recent common ancestor (MRCA) of descendant lineages. `[1 Mark]`
13. **Molecular Clock Tree Algorithm:** UPGMA (produces ultrametric trees). `[1 Mark]`
14. **Number of Reading Frames:** Six reading frames (+1, +2, +3 on forward strand; -1, -2, -3 on reverse strand). `[1 Mark]`
15. **Prokaryotic Ribosome Binding Site:** Shine–Dalgarno consensus sequence ($5'\text{-AGGAGGU-}3'$). `[1 Mark]`
16. **Instability Index Threshold:** Value of **40** ($<40$ is stable; $>40$ is unstable in vitro). `[1 Mark]`
17. **PROSITE Syntax:** `[ ]` indicates permitted residues; `{ }` indicates forbidden residues. `[1 Mark]`
18. **PDB Hetero Record:** `HETATM`. `[1 Mark]`
19. **RMSD Definition:** Root Mean Square Deviation of atomic coordinates between superimposed structures. `[1 Mark]`
20. **C-value Paradox:** The lack of correlation between the total haploid DNA content (genome size) of an organism and its morphological or biological complexity. `[1 Mark]`

---

### Section B: Analytical Questions Scoring Key (40 Marks)
*(Each question is marked out of 5 Marks).*

#### 21. Primary vs Secondary Databases & INSDC Exchange (5 Marks)
* **Comparative Criteria (3.0 Marks):**  
  - *Provenance & Curation:* Primary databases (GenBank, ENA, DDBJ) store raw researcher submissions with no editorial modification; secondary databases (RefSeq, Swiss-Prot) derive curated, non-redundant reference records with literature annotations.  
  - *Redundancy:* Primary is highly redundant (hundreds of clones per gene); secondary is strictly non-redundant (one reference per locus).  
  - *Ownership:* Primary records are owned exclusively by the submitter; secondary records are maintained and updated by database staff biocurators.
* **INSDC Synchronization (2.0 Marks):** Daily automated diff transfers exchange new, updated, and retracted records across NCBI, ENA, and DDBJ, ensuring universal access and international geographical disaster recovery.

#### 22. Entrez Inverted Index Architecture (5 Marks)
* **Structure (2.5 Marks):** An inverted index consists of: (1) a standardized dictionary of terms extracted from specific fields, and (2) associated posting lists containing ordered arrays of Unique Identifiers (UIDs) where each term occurs.
* **Query Execution (2.5 Marks):** For `HBB[GENE] AND "Homo sapiens"[ORGN]`:  
  - Looks up `HBB` in Gene index $\rightarrow$ Posting list $\{3043, 11025, \dots\}$.  
  - Looks up `Homo sapiens` in Organism index $\rightarrow$ Posting list $\{9606, \dots\}$.  
  - Intersects the two pre-sorted integer arrays in linear time $O(L_1 + L_2)$ without scanning gigabytes of flat files on disk.

#### 23. NCBI Abstract Data Model: Bioseq and Seq-feat (5 Marks)
* **Rationale for Data Model (2.0 Marks):** Flat files suffer from brittle text parsing (shifting spaces, line wraps, delimiter errors). ASN.1 defines rigorous, strongly typed object schemas that enable automated parsing, type checking, and format invariance.
* **CDS Representation (3.0 Marks):** A spliced CDS is represented as a `Seq-feat` of type `cdregion`. Its location is a composite `Seq-loc` (`packed-int` or `mix`) joining coordinate intervals across genomic parent coordinates (`join(1..142, 273..495, ...)`), preserving genomic context while linking the translated protein `Bioseq`.

#### 24. PAM vs BLOSUM Substitution Matrices (5 Marks)
* **Comparative Breakdown (3.0 Marks):**  
  - *Dataset:* PAM (Dayhoff) is derived from global alignments of closely related proteins ($\ge 85\%$ identity); BLOSUM (Henikoff) is derived from un-gapped local blocks in the BLOCKS database.  
  - *Distant Matrix Derivation:* PAM extrapolates distant scores by taking mathematical powers of PAM1 ($PAM250 = PAM1^{250}$); BLOSUM calculates scores directly from blocks clustered at lower identity thresholds.  
  - *Numbering Scale:* In PAM, higher numbers denote greater divergence ($PAM1 \rightarrow PAM250$); in BLOSUM, lower numbers denote greater divergence ($BLOSUM80 \rightarrow BLOSUM45$).
* **Matrix Selection for Distant Homologues (2.0 Marks):** For ~25% identity (twilight zone), choose **PAM250** or **BLOSUM45** (or BLOSUM50).

#### 25. Multiple Sequence Alignment Heuristics (5 Marks)
* **Clustal Omega Scalability (2.5 Marks):** Traditional ClustalW requires $N(N-1)/2$ pairwise alignments ($O(N^2)$). Clustal Omega implements $mBed$ seed embedding, representing sequences as distance vectors to $\sim \log_2(N)$ seeds, generating guide trees in $O(N \log N)$ time and aligning profile HMMs via HHalign.
* **MUSCLE Iterative Refinement (2.5 Marks):** After initial progressive alignment, MUSCLE systematically cuts tree edges, dividing the alignment into two sub-profiles, and realigns them via profile-profile dynamic programming. If the Log-Expectation score improves, the new alignment is accepted, correcting early frozen gap errors.

#### 26. Molecular Phylogenetics: NJ vs Maximum Parsimony (5 Marks)
* **Contrast (2.0 Marks):** NJ is a distance-based method operating on a pairwise distance matrix in $O(N^3)$ time; MP is a character-based method evaluating individual alignment columns to minimize total mutational steps.
* **Parsimony-Informative Sites (1.5 Marks):** A site containing at least two distinct character states, each occurring in at least two separate taxa.
* **Long-Branch Attraction (1.5 Marks):** Rapidly evolving lineages independently accumulate convergent mutations by chance. Parsimony misinterprets parallel homoplasies as shared derived synapomorphies, falsely grouping long branches together.

#### 27. Eukaryotic Gene Structure & CpG Islands (5 Marks)
* **Gene Anatomy (3.0 Marks):**  
  Promoter (TATA) $\rightarrow$ Transcription Start Site (TSS) $\rightarrow$ 5' UTR (with 7mG cap) $\rightarrow$ Exon 1 $\rightarrow$ 5' Splice Donor (`GT`) $\rightarrow$ Intron (with branch point Adenosine and polypyrimidine tract) $\rightarrow$ 3' Splice Acceptor (`AG`) $\rightarrow$ Exon 2 (with stop codon) $\rightarrow$ 3' UTR $\rightarrow$ Poly(A) signal (`AATAAA`) $\rightarrow$ Poly(A) tail.
* **CpG Islands & Depletion (2.0 Marks):** Regions $\ge 200\text{ bp}$ with $\%GC \ge 50\%$ and Obs/Exp CpG $\ge 0.60$, marking unmethylated promoters. Depleted in bulk genomes because 5-methylcytosine spontaneously deaminates into thymine ($C \rightarrow T$ transitions).

#### 28. Protein Physicochemical Profiling (5 Marks)
* **ProtParam Metrics (3.0 Marks):**  
  - *pI:* Iterative binary bisection finding the pH where net charge $Q(\text{pH}) = 0$ using Henderson–Hasselbalch equations on all ionizable groups.  
  - *$\epsilon_{280}$:* Weighted sum of aromatic chromophores: $(N_{\text{Trp}} \times 5500) + (N_{\text{Tyr}} \times 1490) + (N_{\text{cystine}} \times 125)$.  
  - *GRAVY:* Sum of Kyte–Doolittle hydropathy values divided by protein length; positive = hydrophobic, negative = hydrophilic.
* **Hydropathy Plots (2.0 Marks):** A sliding window of 19–21 residues scans the sequence. Peaks exceeding $+1.6$ correspond to $\sim 30\text{ \AA}$ hydrophobic alpha-helices spanning the lipid bilayer.

#### 29. Secondary Structure Prediction & Fold Classes (5 Marks)
* **$Q_3$ Metric (1.5 Marks):** $Q_3 = \frac{TP_H + TP_E + TP_C}{N_{\text{total}}} \times 100\%$, measuring three-state prediction accuracy against DSSP ground truth.
* **Single-Sequence vs Machine Learning (1.5 Marks):** Chou–Fasman and GOR IV use single sequence statistics ($Q_3 \approx 55\text{--}65\%$). PSIPRED feeds evolutionary information from PSI-BLAST PSSM profiles into two-stage neural networks ($Q_3 > 80\%$).
* **$\alpha/\beta$ vs $\alpha+\beta$ Classes (2.0 Marks):** $\alpha/\beta$ features alternating $\beta$-strands and $\alpha$-helices forming parallel sheets (e.g., TIM barrel); $\alpha+\beta$ features segregated, distinct regions of anti-parallel $\beta$-sheets and $\alpha$-helices (e.g., lysozyme).

#### 30. Genome Annotation & Synteny Mapping (5 Marks)
* **Structural vs Functional Annotation (2.5 Marks):** Structural annotation delineates physical genomic coordinates of genes, exons, introns, and ncRNAs (using Augustus/Genscan). Functional annotation assigns biological descriptions, GO terms, EC enzyme numbers, and KEGG pathways to those predicted genes.
* **Synteny & Chromosomal Rearrangements (2.5 Marks):** Synteny is the conservation of gene order on chromosomal blocks. In synteny dot-plots, continuous positive diagonals ($/$) indicate colinearity, inverted negative diagonals ($\backslash$) indicate inversions, and offset parallel lines indicate segmental duplications.

---

### Section C: Comprehensive Problems Scoring Key (40 Marks)

#### 31. Optimal Dynamic Programming Hand Alignment (10 Marks)
* **a) Matrix Construction & Calculations (4 Marks):**  
  - $M=6$ (`HEAGAW`), $N=6$ (`HEAWAM`). Match $= +2$, Mismatch $= -1$, Gap $= -2$.  
  - Row 0 / Col 0 initialized with $-2 \cdot i$ ($0, -2, -4, -6, -8, -10, -12$).  
  - Cell $(1,1)$ [$H,H$]: $\max\{0+2, -4, -4\} = \mathbf{+2}$ ($\nwse$).  
  - Cell $(1,2)$ [$H,E$]: $\max\{-2-1, -6, 2-2\} = \mathbf{0}$ ($\leftarrow$).  
  - Cell $(6,6)$ [$W,W$]: Match $+2$. $F(5,5) = +7$. $\max\{7+2, 5-2, 5-2\} = \mathbf{+9}$ ($\nwse$).
* **b) Populated Matrix & Global Traceback (3 Marks):**  
  - Traceback walks along main diagonal: $(6,6) \rightarrow (5,5) \rightarrow (4,4) \rightarrow (3,3) \rightarrow (2,2) \rightarrow (1,1) \rightarrow (0,0)$.  
  - **Optimal Global Alignment:**  
    ```text
    Seq X:  H - E - A - G - A - W
            |   |   |   :   |   |
    Seq Y:  H - E - A - W - A - W
    Score:  +9
    ```
* **c) Smith–Waterman Local Alignment (3 Marks):**  
  - Recurrence: $F(i,j) = \max\{0, \text{Diag}, \text{Up}, \text{Left}\}$.  
  - Row 0 and Col 0 initialized with zeros ($F(i,0)=0, F(0,j)=0$).  
  - Zero bound resets negative scores, allowing local alignments to terminate and restart.  
  - Max cell score is $+9$ at $(6,6)$ (or $+6$ at $(3,3)$ for `HEA`). Local alignment yields `HEAGAW` vs `HEAWAM` with score $+9$ (or `HEA` vs `HEA` with score $+6$).

#### 32. Step-by-Step Molecular Phylogenetic Reconstruction (10 Marks)
* **a) Stepwise UPGMA Construction (5 Marks):**  
  - Min distance is $D(A,B) = 4\%$. Cluster $(AB)$ at height $h = 4/2 = \mathbf{2.0}$.  
  - Updated distances:  
    $D((AB), C) = (8+8)/2 = 8.0$; $D((AB), D) = (10+10)/2 = 10.0$; $D(C,D) = 6.0$.  
  - Min distance in updated matrix is $D(C,D) = 6.0$. Cluster $(CD)$ at height $h = 6/2 = \mathbf{3.0}$.  
  - Final distance between clusters:  
    $D((AB), (CD)) = (8 + 10 + 8 + 10)/4 = 36/4 = 9.0$.  
  - Root height $h = 9.0/2 = \mathbf{4.5}$.  
  - Internal branch lengths: Root $\rightarrow (AB) = 4.5 - 2.0 = \mathbf{2.5}$; Root $\rightarrow (CD) = 4.5 - 3.0 = \mathbf{1.5}$.
* **b) Tree Diagram & Ultrametric Check (2 Marks):**  
  - Tree: `((A:2.0, B:2.0):2.5, (C:3.0, D:3.0):1.5);`  
  - All leaves are equidistant from root ($2.0 + 2.5 = 4.5$; $3.0 + 1.5 = 4.5$).
* **c) Molecular Clock & NJ Comparison (3 Marks):**  
  - Molecular clock assumes constant substitution rates across all lineages.  
  - If one lineage evolves faster, UPGMA groups slow-evolving lineages together artificially.  
  - Neighbor-Joining uses a normalized rate-correction matrix ($Q$-matrix) that subtracts average divergence to all other taxa, producing unrooted additive trees with unequal branch lengths that preserve correct topology.

#### 33. Macromolecular Structure, Parsing & Modeling (10 Marks)
* **a) Structure Quality & $R_{\text{free}}$ (3 Marks):**  
  - Resolution $1.80\text{ \AA}$: High-resolution structure resolving side-chain rotamers.  
  - Working $R = 0.178$: Excellent agreement ($<0.20$) between model and observed diffraction.  
  - $R_{\text{free}} = 0.215$: Evaluated on a 5–10% withheld test set. Prevents crystallographic overfitting; a gap $<0.05$ confirms the model is not overfitted to noise.
* **b) Euclidean Distance Calculation (3 Marks):**  
  - NE2: $(23.040, 13.720, 10.990)$; FE: $(24.120, 12.450, 9.320)$.  
  - $\Delta x = 1.080 \implies \Delta x^2 = 1.1664$.  
  - $\Delta y = -1.270 \implies \Delta y^2 = 1.6129$.  
  - $\Delta z = -1.670 \implies \Delta z^2 = 2.7889$.  
  - Distance: $d = \sqrt{1.1664 + 1.6129 + 2.7889} = \sqrt{5.5682} \approx \mathbf{2.36\text{ \AA}}$.  
  - Confirms authentic coordinate covalent bonding ($2.1\text{--}2.4\text{ \AA}$).
* **c) Homology Modeling & Ramachandran Validation (4 Marks):**  
  - Five steps: Template identification, Target-template alignment, Backbone coordinate generation, Loop/side-chain modeling, Refinement & validation.  
  - Ramachandran plot displays backbone $\phi$ vs $\psi$ dihedral angles, confirming sterically allowed conformations. A reliable, publication-quality model requires $\ge 90\%$ of residues in core favored regions and $\le 1\%$ in disallowed regions.

#### 34. Comparative Genomics, Pan-Genomics & PAIs (10 Marks)
* **a) Bacterial Assembly & Annotation Pipeline (3 Marks):**  
  - QC with FastQC/Trimmomatic $\rightarrow$ De novo assembly with SPAdes (De Bruijn graph) $\rightarrow$ Structural annotation with Prokka (Prodigal for CDS, tRNAscan for tRNAs) $\rightarrow$ Functional annotation via BLASTp, Pfam HMMs, and KEGG pathway mapping.
* **b) Core vs Accessory Pan-Genome (3 Marks):**  
  - Core genome: Genes present in 100% of analyzed strains (conserved housekeeping machinery used for phylogenetics).  
  - Accessory genome: Strain-specific genes present in a subset of isolates.  
  - Antibiotic resistance genes are typically acquired horizontally on plasmids/transposons in response to clinical selective pressure, residing in the mobile accessory genome.
* **c) Three Lines of Evidence for a Pathogenicity Island (4 Marks):**  
  1. *GC-Content Anomaly:* The 45 kb region displays an atypical GC percentage deviating significantly from the host species average.  
  2. *Atypical Codon Bias:* Codon usage frequencies reflect the donor organism rather than the host.  
  3. *Flanking Signatures & Mobility:* Flanked by direct sequence repeats, integrated adjacent to a conserved tRNA gene, and encoding mobility enzymes (integrase, transposase, type III secretion toxins).
