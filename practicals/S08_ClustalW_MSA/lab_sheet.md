# Practical 08: Multiple Sequence Alignment Using Clustal Omega, ClustalW, and Jalview

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S08 (Syllabus Practical P10)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO5 — Construct multiple sequence alignments, interpret progressive alignment algorithms, decipher Clustal consensus conventions, and visualize alignments in Jalview.

---

## 1. Aim & Objectives

### Aim
To construct, visualize, and critically evaluate multiple sequence alignments (MSAs) of the human globin gene family and vertebrate hemoglobin orthologues using progressive alignment tools (Clustal Omega and ClustalW), master alignment visualization in Jalview, identify invariant functional residues, and interpret guide trees.

### Objectives
1. Understand the mathematical basis of progressive multiple sequence alignment and the rationale behind the heuristic "once a gap, always a gap" principle.
2. Execute multiple sequence alignments using Clustal Omega and ClustalW at EMBL-EBI on 7 human globin paralogues (`globin_family_proteins.fasta`).
3. Decipher the standard Clustal consensus line annotation tokens:
   - Asterisk (`*`) : Fully conserved, invariant single residue across all sequences.
   - Colon (`:`) : Conservation between groups of strongly similar properties ($>0.5$ in PAM250).
   - Period (`.`) : Conservation between groups of weakly similar properties ($\le 0.5$ in PAM250).
   - Space (` `) : Non-conserved or divergent position.
4. Launch the alignment in **Jalview**, apply Taylor and Clustalx residue coloring schemes, and analyze Conservation, Quality, and Consensus histograms.
5. Identify the universally conserved globin fold hallmarks: the proximal histidine (His-F8) and distal histidine (His-E7) coordinating the oxygen-binding heme iron.
6. Generate a Neighbor-Joining (NJ) phylogenetic guide tree from the alignment and distinguish gene duplication events from speciation events.

---

## 2. Background & Scientific Principle

### Why Multiple Sequence Alignment?
While pairwise alignment compares two sequences, **Multiple Sequence Alignment (MSA)** aligns three or more biological sequences simultaneously. MSAs are essential for:
1. Identifying highly conserved catalytic residues, binding pockets, and structural motifs that are invisible in pairwise comparisons.
2. Reconstructing evolutionary relationships and building phylogenetic trees.
3. Defining position-specific scoring matrices (PSSMs) and Hidden Markov Models (HMMs) for protein family classification (e.g., Pfam, InterPro).
4. Predicting secondary and tertiary protein structures based on correlated mutational patterns.

### The Progressive Alignment Algorithm (Feng-Doolittle / Clustal)
Finding an exact mathematically optimal MSA using multi-dimensional dynamic programming has a computational complexity of $\mathcal{O}(L^N)$, where $L$ is sequence length and $N$ is the number of sequences. For even 5 sequences of 200 residues, this requires evaluating $200^5 = 3.2 \times 10^{11}$ matrix cells, which is computationally intractable.

In 1987, Da-Fei Feng and Russell F. Doolittle introduced the **progressive alignment** heuristic, implemented most famously by Des Higgins in the **Clustal** series (ClustalV, ClustalW, ClustalX, and Clustal Omega):

```
[N Input Sequences]
       │
       ▼
[Stage 1: All-against-all Pairwise Alignment] (Calculate N*(N-1)/2 pairwise distance scores)
       │
       ▼
[Stage 2: Guide Tree Construction] (Build a Neighbor-Joining or UPGMA guide tree)
       │
       ▼
[Stage 3: Progressive Profile Alignment] (Align most similar pair first; merge sequences/profiles along tree branches)
       │
       ▼
[Final Multiple Sequence Alignment]
```

### The "Once a Gap, Always a Gap" Heuristic Rule
In progressive alignment, once an alignment is formed between two sequences (or two profiles), **gaps introduced at that stage become permanent and frozen**. If an erroneous gap was introduced during an early alignment step due to local sequence anomalies, downstream steps cannot remove or shift the gap. 

### Modern Tools: ClustalW vs. Clustal Omega
- **ClustalW (1994):** Uses traditional dynamic programming for pairwise steps and Neighbor-Joining for guide trees. Slower for large datasets ($\mathcal{O}(N^2)$).
- **Clustal Omega (2011):** The modern state-of-the-art replacement. Employs fast $k$-tuple feature embedding and the mBed algorithm to generate guide trees in $\mathcal{O}(N \log N)$ time, and uses HHalign (profile-profile HMMs) to build highly accurate alignments across thousands of sequences.

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & Desktop Viewers
- EMBL-EBI Clustal Omega: [https://www.ebi.ac.uk/Tools/msa/clustalo/](https://www.ebi.ac.uk/Tools/msa/clustalo/)
- EMBL-EBI ClustalW2 (Archive): [https://www.ebi.ac.uk/Tools/msa/clustalw2/](https://www.ebi.ac.uk/Tools/msa/clustalw2/)
- Jalview Desktop / Web Viewer: [https://www.jalview.org/](https://www.jalview.org/)

### Input Datasets
- Human Globin Family Paralogues: `../../data/sequences/globin_family_proteins.fasta` (7 sequences: HBA1, HBB, HBD, HBG1, MB, NGB, CYGB).
- Vertebrate HBB Orthologues: `../../data/sequences/hbb_vertebrate_orthologues.fasta` (9 sequences).
- Pre-computed Reference Alignment: `../../data/alignments/globin_family.aln`.

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Running Clustal Omega at EMBL-EBI
1. Open [https://www.ebi.ac.uk/Tools/msa/clustalo/](https://www.ebi.ac.uk/Tools/msa/clustalo/).
2. In the input box, paste the contents of `../../data/sequences/globin_family_proteins.fasta`.
3. Confirm **Protein** is selected.
4. Set Output Format to **Clustal w/ numbers**.
5. Click **Submit**.
6. When the job completes, click on the **Alignments** tab:
   - Examine the aligned sequences.
   - Scroll horizontally and observe the consensus annotation line at the bottom.
7. Click on the **Phylogenetic Tree / Guide Tree** tab:
   - Notice how HBB clusters closely with HBD, followed by HBG1, then HBA1, with Myoglobin, Cytoglobin, and Neuroglobin forming more divergent outgroups.
8. Click **Download Alignment File** and save it as `globin_family.aln`.

### Phase 2: Visualizing and Curating in Jalview
1. Launch Jalview on your workstation (or use JalviewJS in-browser at `www.jalview.org`).
2. Go to **File** $\rightarrow$ **Input Alignment** $\rightarrow$ **From File**, and select `globin_family.aln` (or the local file `../../data/alignments/globin_family.aln`).
3. Apply color schemes:
   - Go to **Colour** $\rightarrow$ select **Clustalx**. Notice how hydrophobic residues are colored blue, positive charges red, negative charges magenta, polar green, and glycines orange when conserved.
   - Switch to **Colour** $\rightarrow$ **Hydrophobicity** to view hydrophobic core packing.
4. Inspect the bottom annotation tracks:
   - **Consensus:** Displays the consensus residue and percentage agreement.
   - **Quality:** Measures the chemical property conservation of each column.
   - **Conservation:** Numeric score (0–11, where `*` or `+` denotes complete invariance).

### Phase 3: Locating Invariant Functional Landmarks (His-E7 and His-F8)
1. Locate human HBB (`NP_000509.1`) in the alignment.
2. Find the **Proximal Histidine (His-93 / His-F8)**:
   - In HBB, His-93 directly coordinates the $Fe^{2+}$ ion in the heme prosthetic group.
   - Look across all 7 globin sequences at this column. Confirm that an invariant Histidine (`H`) with an asterisk (`*`) is present in every globin without exception.
3. Find the **Distal Histidine (His-64 / His-E7)**:
   - In HBB, His-64 stabilizes the bound oxygen molecule ($O_2$) via hydrogen bonding.
   - Verify that this column also maintains high conservation across the globin family.
4. Find the **Sickle Cell Mutation Site (Position 6 / 7)**:
   - Locate the N-terminal region of HBB (`MVHLTPEEKS...`).
   - Observe residue Glu-7 (mature Glu-6). Look across the other globin family paralogues at this column. Is this glutamic acid conserved in alpha-globin or myoglobin? (Note that it is variable).

### Phase 4: Constructing a Neighbor-Joining Tree
1. Inside Jalview, select **Calculations** $\rightarrow$ **Calculate Tree or PCA**.
2. Select **Neighbor Joining** using **BLOSUM62**.
3. Click **Calculate**.
4. An interactive tree window will open:
   - Identify the sister-group relationship between beta-globin and delta-globin (recent gene duplication).
   - Identify the earliest branching globin lineage (Neuroglobin / Cytoglobin).

---

## 5. Offline Fallback Note

If the EBI server or internet is unavailable:
- Open the local pre-computed alignment `../../data/alignments/globin_family.aln` directly in Jalview or in any standard text editor.
- The alignment file contains the full 7-sequence Clustal alignment with consensus symbols ready for analysis.

---

## 6. Observations Table

### Table 8.1: Invariant and Critical Functional Residues in the Globin Family MSA
| Functional Landmark | HBB Residue & Position | Aligned Column No. in MSA | Residue in HBA1 | Residue in MB | Residue in NGB | Clustal Consensus Token (`*`, `:`, `.`, space) | Biological Role |
|---|:---:|:---:|:---:|:---:|:---:|:---:|---|
| **Distal Histidine (His-E7)** | His-64 | | | | | | Stabilizes bound $O_2$ ligand |
| **Proximal Histidine (His-F8)** | His-93 | | | | | | Covalently binds heme iron |
| **Invariant Phenylalanine (CD1)** | Phe-43 | | | | | | Wedges heme ring in hydrophobic pocket |
| **Sickle Cell Site (E6V)** | Glu-7 | | | | | | Surface charge; mutates to Val in HbS |

### Table 8.2: Clustal Consensus Symbol Interpretation
| Symbol | Mathematical / Property Definition | Count in Globin Family Alignment | Biological Significance |
|:---:|---|:---:|---|
| `*` (Asterisk) | 100% identical residue across all sequences | | Critical structural or catalytic constraint |
| `:` (Colon) | Strongly similar physico-chemical group ($>0.5$ in PAM250) | | Conservative replacement preserving charge/size |
| `.` (Period) | Weakly similar physico-chemical group ($\le 0.5$ in PAM250) | | Semi-conservative replacement |
| ` ` (Space) | No conservation / divergent properties | | Tolerant to evolutionary drift |

---

## 7. Interpretation & Discussion Questions

1. **The "Once a Gap, Always a Gap" Flaw:** Explain why the progressive alignment strategy cannot correct an alignment error made in the initial pairwise steps. Describe how modern iterative algorithms (such as MUSCLE or MAFFT) overcome this limitation.
2. **Proximal vs. Distal Histidine Invariance:** Why is the proximal histidine (His-F8) so strictly invariant across all globins, including deep outgroups like neuroglobin and leghemoglobin, whereas the distal histidine (His-E7) can occasionally be replaced by glutamine in certain invertebrate globins?
3. **Reading the Guide Tree (Orthologues vs. Paralogues):** In the globin family tree, explain why HBB, HBA1, and MB are **paralogues** (derived from ancient gene duplications), whereas human HBB and chimpanzee HBB are **orthologues** (derived from speciation).
4. **Coloring Schemes in Jalview:** Why is coloring an MSA by residue hydrophobicity particularly useful when inspecting globular proteins like hemoglobin? What pattern do you observe regarding the spatial alternation of hydrophobic and polar residues in alpha helices?
5. **Impact of Adding Divergent Sequences:** If a researcher adds a bacterial truncated globin or plant leghemoglobin to this alignment, what will happen to the total number of asterisk (`*`) consensus positions? Why?

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Perform a multiple sequence alignment using the 9 vertebrate HBB orthologues from `../../data/sequences/hbb_vertebrate_orthologues.fasta`.
2. Calculate the overall percentage of identical columns across all 9 vertebrate species.
3. Identify which vertebrate species displays the greatest number of amino acid differences compared to human HBB, and explain this in terms of vertebrate evolutionary divergence times (e.g., Mammals vs. Birds vs. Fish).
