# Official Practical Examination Question Paper & Answer Booklet (CBBI-501 / CBBI-502)

**Course Title:** Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Examination Session:** S15 (End-Semester Practical Exam & Viva Voce)  
**Total Time Allowed:** 2 Hours (120 Minutes)  
**Maximum Marks:** 100 Marks  

---

### Student Identification & Examination Station Details
- **Student Full Name:** __________________________________________________________________
- **University Roll Number:** _____________________________________________________________
- **Examination Lab Station / PC No.:** ___________________________________________________
- **Assigned Question Set:** `[ ] SET A` &nbsp;&nbsp;&nbsp;&nbsp; `[ ] SET B` &nbsp;&nbsp;&nbsp;&nbsp; `[ ] SET C` &nbsp;&nbsp;&nbsp;&nbsp; `[ ] SET D`
- **Date & Time of Examination:** ________________________________________________________
- **Invigilator / Proctor Signature:** ___________________________________________________

---

## SECTION 1: CANDIDATE INSTRUCTIONS
1. Write your full name, roll number, and assigned Question Set code clearly above.
2. Complete Task 1 (Retrieval & Dissection, 35 Marks) and Task 2 (Computational Analysis & 3D Mapping, 35 Marks) directly in this booklet.
3. Be prepared to present your live screen outputs to the examiners during Task 3 (Oral Viva Voce, 30 Marks).
4. Strictly no external communication or unauthorized websites.

---

## SECTION 2: TASK 1 — DATA RETRIEVAL & FLAT FILE DISSECTION (35 MARKS)
*(Refer to your assigned Question Set instructions provided by the proctor).*

### 1.1 Live Query Formulation & Database Identifier Log (10 Marks)
- **Primary Search Query String Used:**  
  `[                                                                                             ]`
- **NCBI Gene ID Retrieved:** `[____________________]` &nbsp;&nbsp;&nbsp;&nbsp; **Cytogenetic Location:** `[____________________]`
- **RefSeq mRNA Accession & Version:** `[____________________]` &nbsp;&nbsp;&nbsp;&nbsp; **Total Transcript Length:** `[_____] bp`
- **RefSeq Protein Accession & Version:** `[____________________]` &nbsp;&nbsp;&nbsp;&nbsp; **Total Amino Acid Length:** `[_____] aa`
- **Primary UniProtKB Accession & Status:** `[____________________]` &nbsp;&nbsp;&nbsp;&nbsp; `[ ] Reviewed` / `[ ] Unreviewed`

### 1.2 Feature Table Coordinate Dissection & CDS Mathematics (15 Marks)
1. **CDS Coordinate Range:** From nucleotide `[__________]` to nucleotide `[__________]`.
2. **Coding Region Nucleotide Span Calculation:**
   $$\text{Span Length} = (\text{Stop Coordinate} - \text{Start Coordinate} + 1) = [__________________________________] = [_____]\text{ nt}$$
3. **Number of Encoded Triplets (Codons):** `[_____] / 3 = [_____] codons`.
4. **Accounting for the Termination Stop Codon:** `[_____] codons - 1 stop codon = [_____] amino acids`.
5. **Does your calculated length match the RefSeq protein record length?** `[ ] YES` &nbsp;&nbsp; `[ ] NO`
6. **5' UTR Boundary Coordinates:** `[__________]` to `[__________]` (Length: `[_____] bp`).
7. **3' UTR Boundary Coordinates:** `[__________]` to `[__________]` (Length: `[_____] bp`).
8. **Polyadenylation Regulatory Signal Motif & Coordinates:** `[__________________________________]`.

### 1.3 Sequence Format Conversion & Anatomy Verification (10 Marks)
- **Command Used for Conversion (`seqret` / Biopython):**  
  `[                                                                                             ]`
- **Identify the 2-letter Line Codes in the resulting EMBL file for:**
  - Sequence Identification: `[_____]` &nbsp;&nbsp;&nbsp;&nbsp; Primary Accession: `[_____]`
  - Organism Species: `[_____]` &nbsp;&nbsp;&nbsp;&nbsp; Feature Table Header: `[_____]` &nbsp;&nbsp;&nbsp;&nbsp; Sequence Data: `[_____]`
- **Flat File End-of-Record Token (GenBank vs. EMBL):**  
  GenBank: `[__________]` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; EMBL: `[__________]`

---

## SECTION 3: TASK 2 — SEQUENCE ALIGNMENT & STRUCTURAL ANALYSIS (35 MARKS)

### 2.1 Database Similarity Search / Alignment Hit Table (15 Marks)
Execute the assigned search (BLASTP or FASTA) and record the top four biological hits:

| Hit Rank | Subject Accession | Full Protein Description | Query Cover (%) | % Sequence Identity | Bit Score ($S'$) | Expect Value ($E$) |
|:---:|---|---|:---:|:---:|:---:|:---:|
| **1 (Self)** | | | | | | |
| **2** | | | | | | |
| **3** | | | | | | |
| **4** | | | | | | |

- **Scoring Matrix Used:** `[____________________]` &nbsp;&nbsp;&nbsp;&nbsp; **Word Size:** `[_____]`
- **Effect of Changing Scoring Matrix (e.g., BLOSUM62 vs. BLOSUM45 / PAM250):**  
  `[                                                                                             ]`  
  `[                                                                                             ]`  

### 2.2 Sequence Feature Prediction or Physicochemical Profiling (10 Marks)
Record the assigned parameter calculations (ProtParam or Secondary Structure $Q_3$):

| Parameter / Feature Evaluated | Observed Value | Expected Biological Interpretation |
|---|:---:|---|
| **Molecular Weight ($M_r$, Da)** | | Total calculated molecular mass |
| **Theoretical Isoelectric Point ($pI$)** | | pH of zero net electrical charge |
| **Total Negative / Positive Residues** | (-) `[____]` / (+) `[____]` | Electrostatic charge balance |
| **Instability Index ($II$) & Status** | | Classified: `[ ] Stable` / `[ ] Unstable` |
| **GRAVY Score** | | Hydropathic nature (hydrophilic vs hydrophobic) |
| **Conserved Active Site / Motif ID** | | PROSITE / Pfam identifier |

### 2.3 3D Macromolecular Structure Coordinate Inspection (10 Marks)
Load the assigned PDB file into VMD or Mol* and record structural measurements:

- **Target PDB ID:** `[________]` &nbsp;&nbsp;&nbsp;&nbsp; **Resolution:** `[________] Å` &nbsp;&nbsp;&nbsp;&nbsp; **Experimental Method:** `[____________________]`
- **Total Chains in Asymmetric Unit:** `[_____]` &nbsp;&nbsp;&nbsp;&nbsp; **Biological Assembly Stoichiometry:** `[____________________]`
- **Key Catalytic / Prosthetic Ligand Name:** `[________]`
- **Measured Active Site Atomic Distance (e.g., Metal-Ligand or Salt Bridge):**
  - Atom 1: `[____________________]` to Atom 2: `[____________________]`
  - Measured Distance: `[__________] Å`
  - Biological Significance: `[                                                                 ]`

---

## SECTION 4: TASK 3 — ORAL VIVA VOCE EXAMINATION (30 MARKS)
*(To be completed and signed by the Official Examiners during the viva interview).*

| Question No. | Learning Outcome Evaluated | Specific Viva Question Tested | Max Marks | Marks Awarded |
|:---:|:---:|---|:---:|:---:|
| **V1** | **LO1 / LO2** | Database architecture, INSDC, RefSeq vs GenBank, or Entrez tags | 6 | |
| **V2** | **LO3 / LO4** | Pairwise alignment, dynamic programming vs BLAST heuristics, E-value math | 6 | |
| **V3** | **LO5** | Multiple sequence alignment, progressive heuristic flaws, or reading trees | 6 | |
| **V4** | **LO6** | Sequence feature prediction (ORFs, codon bias, hydropathy, or GOR/PSIPRED) | 6 | |
| **V5** | **LO7 / LO8** | Macromolecular structure, resolution, R-free, B-factors, or comparative genomics | 6 | |
| **Total** | | **Oral Viva Voce Score** | **30** | |

---

## SECTION 5: FINAL SCORE SUMMARY & OFFICIAL ENDORSEMENT

| Examination Component | Maximum Marks | Marks Awarded | Examiner Remarks |
|---|:---:|:---:|---|
| **Task 1: Data Retrieval & Flat File Dissection** | 35 | | |
| **Task 2: Sequence Alignment & Structural Analysis**| 35 | | |
| **Task 3: Oral Viva Voce Examination** | 30 | | |
| **Total Examination Score** | **100** | | Scaled to 10% Course Grade |

- **Name of Internal Examiner:** _______________________________ &nbsp;&nbsp; **Signature:** _____________________
- **Name of External Examiner:** _______________________________ &nbsp;&nbsp; **Signature:** _____________________
- **Date of Evaluation:** _______________________________________
