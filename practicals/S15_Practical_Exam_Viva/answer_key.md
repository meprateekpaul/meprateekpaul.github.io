# Examiner Master Grading Key & Viva Voce Manual (Practical 15)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S15 (Practical Exam & Viva Voce)  
**Curriculum Topic:** Comprehensive Practical Examination & Oral Viva Voce  

---

## 1. Master Solutions for Randomized Question Sets

### 1.1 Master Key: SET A (Human Beta-Globin / *HBB*)
- **Task 1 (Retrieval):**
  - Gene ID: `3043`, Cytogenetic Band: `11p15.4`.
  - RefSeq mRNA: `NM_000518.5` (626 bp), RefSeq Protein: `NP_000509.1` (147 aa), UniProt: `P68871` (Reviewed).
  - CDS Coordinates: `51..494`. Length $= 494 - 51 + 1 = 444\text{ nt}$.
  - Codons: $444 / 3 = 148$ triplets. Amino acids $= 148 - 1\text{ (stop codon)} = 147\text{ aa}$ (Matches RefSeq).
  - 5' UTR: `1..50` (50 bp); 3' UTR: `495..626` (132 bp); PolyA signal: `600..605` (`aataaa`).
  - EMBL line codes: `ID` (Identifier), `AC` (Accession), `OS` (Organism Species), `FT` (Feature Table), `SQ` (Sequence). Delimiters: GenBank `//`, EMBL `//`.
- **Task 2 (Analysis & 3D):**
  - BLASTP Top Hits: HBB (100% id, $S'=298$, $E=1.2e-105$), HBD (95.2% id, $S'=279$, $E=3.4e-98$), HBG1 (73.5% id, $S'=212$, $E=2.1e-72$), HBA1 (43.1% id, $S'=121$, $E=4.8e-37$), Myoglobin (28.5% id, $S'=73.6$, $E=1.5e-18$).
  - PDB `1A3N`: Resolution = 2.00 $\text{\AA}$, X-ray diffraction, ASU = 2 chains ($\alpha\beta$ dimer), Biological Assembly = 4 chains ($\alpha_2\beta_2$).
  - Measured Distance: Fe to His-87/92 NE2 = **2.09 – 2.10 $\text{\AA}$** (covalent coordinate bond).

---

### 1.2 Master Key: SET B (Tumor Suppressor *TP53*)
- **Task 1 (Retrieval):**
  - Gene ID: `7157`, Cytogenetic Band: `17p13.1`.
  - RefSeq mRNA: `NM_000546.6` (2,591 bp), RefSeq Protein: `NP_000537.3` (393 aa), UniProt: `P04637` (Reviewed).
  - CDS Coordinates: `251..1432`. Length $= 1432 - 251 + 1 = 1182\text{ nt}$.
  - Codons: $1182 / 3 = 394$ triplets. Amino acids $= 394 - 1 = 393\text{ aa}$.
  - Key Functional Domains: Transactivation domain (1–61), Proline-rich domain (63–97), DNA-binding core domain (98–292), Oligomerization domain (325–356).
- **Task 2 (Analysis & 3D):**
  - ProtParam: $M_r = 43,653\text{ Da}$, Theoretical $pI = 6.44$, Total negative = 47, Total positive = 43, Instability Index $II = 65.52$ (Classified: **Unstable**; intrinsic disorder in termini), GRAVY = **-0.654** (highly hydrophilic).
  - PDB `1TUP`: Resolution = 2.20 $\text{\AA}$. Shows p53 DNA-binding core bound to consensus DNA.
  - Active Site Geometry: Conserved $Zn^{2+}$ ion coordinated by Cys-176, His-179, Cys-238, and Cys-242 (distances ~2.3 $\text{\AA}$). Hotspot mutations (R175, R248, R273) directly contact DNA or stabilize the zinc loop.

---

### 1.3 Master Key: SET C (Human Preproinsulin / *INS*)
- **Task 1 (Retrieval):**
  - Gene ID: `3630`, Cytogenetic Band: `11p15.5`.
  - RefSeq mRNA: `NM_000207.3` (469 bp), RefSeq Protein: `NP_000198.1` (110 aa), UniProt: `P01308` (Reviewed).
  - CDS Coordinates: `60..392`. Length $= 392 - 60 + 1 = 333\text{ nt}$.
  - Codons: $333 / 3 = 111$ triplets. Amino acids $= 111 - 1 = 110\text{ aa}$.
  - Processing Architecture: Signal peptide (1–24), B-chain (25–54, 30 aa), C-peptide (57–87, 31 aa cleaved), A-chain (90–110, 21 aa). Mature active hormone $= \text{A} + \text{B}$ chains (51 aa).
- **Task 2 (Analysis & 3D):**
  - ProtParam Preproinsulin: $M_r = 11,980.7\text{ Da}$, $pI = 5.35$, $II = 64.91$, GRAVY = $+0.125$ (signal peptide hydrophobicity).
  - Mature Hormone (A+B chains): 3 disulfide bonds (Intra-A: CysA6-CysA11; Inter A-B: CysA7-CysB7, CysA20-CysB19).
  - PDB `4INS` (Hodgkin landmark, 1.50 $\text{\AA}$): Two $Zn^{2+}$ ions on the 3-fold symmetry axis coordinating six insulin monomers (His-B10 coordination) to form the storage hexamer.

---

### 1.4 Master Key: SET D (Muscle Myoglobin / *MB*)
- **Task 1 (Retrieval):**
  - Gene ID: `4151`, Cytogenetic Band: `22q12.2`.
  - RefSeq mRNA: `NM_005368.3` (1,154 bp), RefSeq Protein: `NP_005359.1` (154 aa), UniProt: `P02144` (Reviewed).
  - CDS Coordinates: `52..516`. Length $= 516 - 52 + 1 = 465\text{ nt}$.
  - Codons: $465 / 3 = 155$ triplets. Amino acids $= 155 - 1 = 154\text{ aa}$.
  - Contrast with Hemoglobin: Monomeric polypeptide functioning in muscle oxygen storage; hyperbolic oxygen binding curve (lacks cooperative allostery).
- **Task 2 (Analysis & 3D):**
  - Pairwise alignment: Myoglobin vs HBB = 28.5% identity ($E \sim 10^{-18}$ in BLASTP).
  - Secondary Structure: 8 $\alpha$-helices (all-$\alpha$ globin fold). GOR IV $Q_3 \approx 82\%$; PSIPRED $Q_3 \approx 87\%$.
  - PDB `1MBO` (Phillips landmark, 1.4 $\text{\AA}$): Monomeric asymmetric unit containing 1 chain and 1 heme group. Proximal His-93 ($Fe\text{--}N \approx 2.1\text{ \AA}$) and Distal His-64 ($Fe\text{--}N \approx 4.1\text{ \AA}$).

---

## 2. Comprehensive 25-Question Viva Voce Bank (Categorized by LO1–LO8)

Examiners select five questions (one per section) during the oral interview.

### Category 1: Databases, Identifiers & Data Models (LO1, LO2)
1. **Q: What is the International Nucleotide Sequence Database Collaboration (INSDC), and how frequently do its member repositories synchronize data?**  
   *Model Answer:* INSDC is the global partnership between NCBI (GenBank), EMBL-EBI (ENA), and DDBJ. They synchronize direct user sequence submissions, accessions, and flat files daily, ensuring worldwide sequence identity consistency.
2. **Q: Why does NCBI maintain both GenBank and RefSeq? What distinguishes an accession starting with `NM_` from one starting with `XM_`?**  
   *Model Answer:* GenBank is an archival, redundant repository of all historical submissions (including fragments and errors). RefSeq is a non-redundant, curated reference standard. `NM_` denotes a manually or experimentally validated curated mRNA record; `XM_` denotes a provisional model predicted solely by automated computational genome annotation algorithms.
3. **Q: How does the Entrez query engine interpret the Boolean expression `A AND B OR C`? How should parentheses be used?**  
   *Model Answer:* Entrez processes Boolean queries strictly from left to right. Without parentheses, it evaluates `(A AND B)` first, then takes the union with `C`. If `C` is a broad keyword, tens of thousands of irrelevant records enter the result set. Parentheses must be used to force precedence: `A AND (B OR C)`.
4. **Q: What is the difference between a primary accession number and a version number in a GenBank record (e.g., `NM_000518.5`)?**  
   *Model Answer:* The accession (`NM_000518`) is the permanent, unique identifier of the biological locus and never changes. The version number (`.5`) increments by 1 whenever any nucleotide in the sequence is revised or corrected, preserving scientific reproducibility.
5. **Q: Contrast the two tiers of the UniProt knowledgebase: Swiss-Prot vs. TrEMBL.**  
   *Model Answer:* Swiss-Prot is manually reviewed and curated by PhD-level biocurators who extract experimental data from literature. TrEMBL is unreviewed, containing automated computer-translated coding sequences from INSDC, growing exponentially but lacking experimental validation.

---

### Category 2: Sequence Alignment & Substitution Matrices (LO3, LO4)
6. **Q: What is the fundamental difference between the Needleman-Wunsch algorithm and the Smith-Waterman algorithm?**  
   *Model Answer:* Needleman-Wunsch computes an optimal **global alignment** across the entire length of both sequences (matrix initialization initialized with negative gap penalties; traceback starts at bottom-right cell). Smith-Waterman computes an optimal **local alignment** finding the highest scoring local sub-segment (negative matrix values are set to 0; traceback starts at the maximum value cell in the entire matrix and terminates at 0).
7. **Q: Why are affine gap penalties ($P = d + k \cdot e$) biologically superior to linear gap penalties ($P = k \cdot d$)?**  
   *Model Answer:* In molecular evolution, a single mutational event (unequal crossing over, replication slippage) frequently inserts or deletes a multi-residue chunk at once. An affine gap penalty imposes a large penalty to open the gap ($d$), but a small penalty to extend it ($e$), biologically reflecting that extending a deletion is far more probable than opening a brand-new gap.
8. **Q: Explain why BLOSUM62 is named with the number 62, while PAM250 is named with 250.**  
   *Model Answer:* BLOSUM matrices use clustering percentages: BLOSUM62 clusters sequences sharing $\ge 62\%$ identity to prevent bias; lower numbers (BLOSUM45) are for divergent sequences. PAM matrices use evolutionary distance: PAM250 represents 250 point mutations per 100 residues; higher numbers represent greater evolutionary divergence.
9. **Q: What is the mathematical difference between an alignment's Raw Score ($S$) and Bit Score ($S'$)?**  
   *Model Answer:* Raw score ($S$) is the direct sum of matrix scores and gap penalties and cannot be compared across different scoring matrices. Bit score ($S' = \frac{\lambda S - \ln K}{\ln 2}$) normalizes the score using Karlin-Altschul parameters, expressing statistical significance in standard binary information bits independent of the matrix.
10. **Q: If the database searched doubles in size, what happens to the BLAST $E$-value and the Bit Score for an identical match?**  
    *Model Answer:* The Expect value doubles linearly ($E = m \cdot N \cdot 2^{-S'}$), because twice as many false-positive random matches are expected in a database of size $2N$. The bit score ($S'$) remains completely unchanged because it depends solely on the intrinsic sequence quality of the alignment.

---

### Category 3: Multiple Alignment & Molecular Phylogenetics (LO5)
11. **Q: What is the fundamental heuristic flaw in progressive multiple sequence alignment ("once a gap, always a gap")?**  
    *Model Answer:* In progressive alignment (Clustal), sequences are aligned hierarchically following a guide tree. Once an alignment between two sequences/profiles is formed, any gap introduced becomes permanently frozen and cannot be adjusted or removed in later steps, even if subsequent sequences prove the gap was misplaced.
12. **Q: Decode the meaning of the four consensus line tokens in a Clustal alignment: `*`, `:`, `.`, and space.**  
    *Model Answer:* Asterisk (`*`) means 100% identical residue across all sequences; Colon (`:`) means conservation between strongly similar amino acids ($>0.5$ in PAM250); Period (`.`) means conservation between weakly similar amino acids ($\le 0.5$ in PAM250); Space means non-conserved / divergent position.
13. **Q: Distinguish between orthologous genes and paralogous genes with an example from the globin family.**  
    *Model Answer:* Orthologues arise via speciation from a common ancestor and typically retain the same function (e.g., human HBB and chimpanzee HBB). Paralogues arise via gene duplication within a genome and often diverge in function (e.g., human HBB and human Myoglobin).
14. **Q: How does a rooted phylogenetic tree differ from an unrooted tree, and how is an outgroup used to root a tree?**  
    *Model Answer:* An unrooted tree specifies topological relationships and branch lengths between leaves but does not indicate the direction of evolutionary time or the position of the common ancestor. An outgroup is a known distant taxon that branched off prior to the radiation of the ingroup (e.g., neuroglobin for blood globins). The root is placed along the branch connecting the outgroup to the rest of the tree, polarizing evolutionary time.
15. **Q: What does a bootstrap support value of 95% at an internal tree node signify?**  
    *Model Answer:* It means that when the multiple alignment columns are randomly resampled with replacement 1,000 times (pseudo-replicate datasets), the exact same monophyletic clade is reconstructed in 95% of the resulting trees, indicating high statistical robustness against sampling noise.

---

### Category 4: Sequence Features, Codon Bias & Structure Prediction (LO6)
16. **Q: Why does double-stranded genomic DNA have exactly six possible reading frames?**  
    *Model Answer:* DNA is double-stranded and antiparallel. Because the genetic code reads triplets, translation can begin at nucleotide 1, 2, or 3 on the forward strand ($+1, +2, +3$) and at nucleotide 1, 2, or 3 on the complementary reverse strand ($-1, -2, -3$).
17. **Q: What is the biological function of the eukaryotic Kozak consensus sequence (`gccRccAUGG`)?**  
    *Model Answer:* The 40S small ribosomal subunit scans from the 5' $m^7G$ cap along the mRNA until it encounters an AUG codon. The Kozak sequence provides the optimal sequence context (especially purine A/G at $-3$ and G at $+4$) that signals the scanning complex to pause and initiate translation at that specific AUG, preventing spurious initiation at out-of-frame AUGs.
18. **Q: Define Relative Synonymous Codon Usage (RSCU). What does an RSCU value $>1.0$ indicate?**  
    *Model Answer:* RSCU is the ratio of the observed frequency of a codon to the frequency expected if all synonymous codons for that amino acid were used equally. An RSCU $>1.0$ indicates positive codon preference / translational selection, typically matching abundant cellular tRNA species in highly expressed genes.
19. **Q: What is the theoretical isoelectric point ($pI$) of a protein, and why does protein solubility reach a minimum at pH = $pI$?**  
    *Model Answer:* The $pI$ is the pH at which the net electrical charge of the protein molecule equals zero. At pH = $pI$, electrostatic repulsive forces between neighboring protein molecules drop to zero, allowing hydrophobic surface patches to aggregate and precipitate the protein out of solution.
20. **Q: How does PSIPRED achieve superior secondary structure prediction accuracy ($>80\%$) compared to GOR IV (~65%)?**  
    *Model Answer:* GOR IV relies solely on statistical information theory within a single sequence's 17-residue window. PSIPRED runs PSI-BLAST to construct an evolutionary Position-Specific Scoring Matrix (PSSM), capturing evolutionary conservation and mutational constraints across hundreds of homologues, which are fed into a two-stage neural network.

---

### Category 5: 3D Structure, PDB Records & Molecular Modeling (LO7, LO8)
21. **Q: In X-ray crystallography, why is a 1.5 $\text{\AA}$ resolution structure considered vastly superior to a 3.0 $\text{\AA}$ structure?**  
    *Model Answer:* Resolution measures the minimum Bragg spacing ($d_{\text{min}}$). Smaller numbers mean finer detail. At 1.5 $\text{\AA}$, individual atoms, bond lengths, water molecules, and side-chain rotamers are clearly separated in electron density. At 3.0 $\text{\AA}$, individual atoms blur together; only the backbone trace and bulky secondary structure envelopes are discernible.
22. **Q: What is the purpose of the crystallographic $R_{\text{free}}$ value, and what does a large divergence between $R_{\text{work}}$ and $R_{\text{free}}$ indicate?**  
    *Model Answer:* $R_{\text{free}}$ is calculated against a randomly withheld 5%–10% test set of diffraction reflections never used during refinement. It provides an unbiased cross-validation metric. If $R_{\text{work}}$ drops to 0.15 while $R_{\text{free}}$ remains at 0.28, the model has been severely over-fitted to experimental noise.
23. **Q: Explain the difference between an `ATOM` record and a `HETATM` record in a PDB file.**  
    *Model Answer:* `ATOM` records are strictly reserved for standard polymer residues (the 20 canonical amino acids and standard nucleotides) forming continuous chains. `HETATM` records describe non-polymer hetero-groups: prosthetic groups (HEM), metal ions ($Fe, Zn$), enzyme cofactors, small-molecule drug inhibitors, and crystallographic water molecules.
24. **Q: Describe the stereochemical mechanism of hemoglobin cooperativity proposed by Max Perutz.**  
    *Model Answer:* In deoxyhemoglobin (T-state), the high-spin $Fe^{2+}$ ion sits ~0.4 $\text{\AA}$ out of the porphyrin plane toward the proximal histidine. Binding of $O_2$ shifts iron to low-spin, pulling it into the porphyrin plane. This movement pulls the proximal histidine and Helix F, transmitting mechanical strain through the $\alpha_1\beta_2$ interface, breaking inter-subunit salt bridges and rotating the dimers by $15^\circ$ into the high-affinity R-state.
25. **Q: What is the difference between an Asymmetric Unit (ASU) and a Biological Assembly in the Protein Data Bank?**  
    *Model Answer:* The Asymmetric Unit is the smallest structural portion that generates the entire crystal lattice when space group symmetry operations are applied. The Biological Assembly is the functional quaternary oligomer in living cells. In `1A3N`, the ASU contains only an $\alpha\beta$ dimer; crystallographic two-fold symmetry generates the functional $\alpha_2\beta_2$ tetramer.

---

## 3. Official Practical Examination Marking Rubric Matrix

| Grade Band | Percentage Range | Expected Student Performance Characteristics |
|---|:---:|---|
| **Outstanding (O)** | **90% – 100%** | Flawless query formulation; perfect CDS calculations; rapid format conversion; comprehensive BLAST/alignment interpretation; precise 3D pocket distance measurements; articulate, immediate, in-depth responses across all 5 viva categories. |
| **Excellent (A+)** | **80% – 89%** | Accurate retrieval and CDS math; solid BLAST and ProtParam analysis; correct structural measurements; thorough viva responses with minor hesitations on advanced mathematical derivations ($E$-value / $R_{\text{free}}$). |
| **Very Good (A)** | **70% – 79%** | Successful record retrieval; minor errors in UTR boundary identification; accurate tool runs; correct general viva answers, but unable to explain deeper biophysical mechanisms (e.g., Perutz iron shift or PSSM neural networks). |
| **Good (B+)** | **60% – 69%** | Retrieves records with guidance; minor errors in CDS codon mathematics; partial interpretation of BLAST hit tables; basic 3D navigation; basic viva knowledge with notable gaps in algorithms. |
| **Satisfactory (B)**| **50% – 59%** | Significant difficulty with command-line format conversion or field-tagged queries; confused between ASU and biological assembly; superficial or inaccurate viva answers; minimum passing performance. |
| **Fail (F)** | **< 50%** | Inability to retrieve assigned accessions; failure to execute alignment tools; incorrect CDS math; unable to answer fundamental concept questions during viva voce. |
