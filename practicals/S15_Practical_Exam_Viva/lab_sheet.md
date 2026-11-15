# Practical 15: Practical Examination & Viva Voce — Standard Operating Protocol and Guidelines

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S15 (End-Semester Practical Examination & Oral Viva Voce)  
**Total Duration:** 2 Hours (120 Minutes)  
**Total Marks:** 100 Marks (Scaled to 10% of overall course grade)  
**Learning Outcomes Evaluated:** LO1 through LO8  

---

## 1. Examination Structure and Time Schedule

The practical examination is conducted in an active computer laboratory under strict proctored examination conditions. Each student is assigned an isolated workstation and an individually randomized Question Set (Set A, Set B, Set C, or Set D).

```
+-------------------------------------------------------------------------------------------------+
|                                 120-MINUTE EXAMINATION SCHEDULE                                 |
+-------------------+-----------------------------+-----------------------------+-----------------+
|  Minutes 00 – 10  |       Minutes 10 – 55       |       Minutes 55 – 100      | Minutes 100 – 120|
|   (10 Minutes)    |        (45 Minutes)         |        (45 Minutes)         |  (20 Minutes)   |
|   Briefing & ID   |   TASK 1: DATA RETRIEVAL    |     TASK 2: COMPUTATIONAL   | ORAL VIVA VOCE  |
|    Verification   |    & FLAT FILE DISSECTION   |     ALIGNMENT & ANALYSIS    | & VERIFICATION  |
|                   |         (35 Marks)          |         (35 Marks)          |   (30 Marks)    |
+-------------------+-----------------------------+-----------------------------+-----------------+
```

### Time Allocation Breakdown:
1. **00 – 10 min (10 Minutes): Entry, Seating & Briefing:**
   - Identity verification, inspection of hall tickets, random assignment of Question Set (A, B, C, or D), logging into examination workstation terminal.
2. **10 – 55 min (45 Minutes): Task 1 — Data Retrieval, Query Formulation & Flat File Dissection (35 Marks):**
   - Live query formulation in Entrez / NCBI / UniProt, retrieval of assigned gene/protein records, extraction of feature coordinates, CDS math, and format conversion.
3. **55 – 100 min (45 Minutes): Task 2 — Sequence Alignment, Structural Analysis & Feature Prediction (35 Marks):**
   - Execution of BLASTP / FASTA similarity searches, Multiple Sequence Alignment or physicochemical profiling (ProtParam), and secondary structure validation / 3D structural coordinate inspection.
4. **100 – 120 min (20 Minutes): Task 3 — Individual Oral Viva Voce & Final Log Sign-Off (30 Marks):**
   - One-on-one viva examination conducted at the terminal by the external/internal examiners, testing algorithmic depth, theoretical principles, and critical interpretation of on-screen results.

---

## 2. Laboratory Rules and Examination Protocols

1. **Closed-Book Environment:**
   - No textbooks, printed lab manuals, personal notebooks, USB flash drives, or mobile phones are permitted in the laboratory.
   - Any access to unauthorized messaging platforms, generative AI chat interfaces, or external communication channels will result in immediate disqualification under unfair means (UFM) regulations.
2. **Authorized Web Domains:**
   - Workstation web browsers are restricted strictly to official production bioinformatics web servers:
     - NCBI Gateway (`ncbi.nlm.nih.gov`)
     - UniProt Knowledgebase (`uniprot.org`)
     - EMBL-EBI Tools (`ebi.ac.uk`)
     - Expasy SIB (`expasy.org`)
     - RCSB Protein Data Bank (`rcsb.org`)
     - Local filesystem course data (`../../data/`)
3. **Local Emergency Fallback:**
   - If an external internet connection fails or an official server experiences downtime, students must immediately notify the proctor. The student will be instructed to execute the offline fallback pipeline using pre-cached sequence and structure records located in `../../data/` without penalty.
4. **Submission Protocol:**
   - All written observations, tables, calculations, and answers must be recorded directly in the official **Worksheet / Answer Booklet (`worksheet.md`)**.
   - Output text files or terminal command transcripts must be preserved in the student's examination directory: `~/Exam_<RollNumber>/`.

---

## 3. Four Randomized Question Set Allocations

To ensure absolute academic integrity and prevent cross-station collaboration, four distinct problem sets are deployed:

### Set A: Focus on Human Beta-Globin (*HBB*) and Erythroid Paralogues
- **Task 1 (Retrieval):** Human *HBB* RefSeq record `NM_000518.5`. Dissect CDS coordinates, calculate encoded amino acids, extract 5' and 3' UTR boundaries, and convert to EMBL format.
- **Task 2 (Analysis):** BLASTP query of `NP_000509.1` against RefSeq. Interpret bit scores and E-values for delta-globin, alpha-globin, and myoglobin. Load `1A3N.pdb` in Mol*/VMD and measure the coordination distance between heme iron and proximal His-87/92.

### Set B: Focus on Human Tumor Suppressor *TP53* (Guardian of the Genome)
- **Task 1 (Retrieval):** Human *TP53* RefSeq record `NM_000546.6` (Gene ID: `7157`). Dissect the multi-exon organization, extract the major transactivation and DNA-binding domain coordinates, and retrieve UniProt `P04637`.
- **Task 2 (Analysis):** Physicochemical profiling of p53 isoform a using ProtParam. Explain the instability index ($II > 50$) and GRAVY score. Multiple alignment of human, mouse, and zebrafish p53 DNA-binding domains; identify invariant zinc-coordinating cysteines.

### Set C: Focus on Human Preproinsulin (*INS*) and Metabolic Regulators
- **Task 1 (Retrieval):** Human *INS* RefSeq record `NM_000207.3` (Gene ID: `3630`, 11p15.5). Trace the three-domain precursor structure: Signal peptide (1–24), B-chain (25–54), C-peptide (55–89), and A-chain (90–110).
- **Task 2 (Analysis):** Expasy ProtParam profiling of the full precursor vs. mature processed hormone (A+B chains). Identify the 3 conserved disulfide bonds (CysA6-CysA11, CysA7-CysB7, CysA20-CysB19). Load crystal structure `4INS` or `1TRZ` and map the zinc-coordinated hexameric interface.

### Set D: Focus on Muscle Myoglobin (*MB*) and Oxygen Storage
- **Task 1 (Retrieval):** Human *MB* RefSeq record `NM_005368.3` (Gene ID: `4151`) and UniProt `P02144`. Compare chromosomal locus (22q12.2) against hemoglobin loci (11p15.4 and 16p13.3). Contrast monomeric flat file annotation against tetrameric HBB.
- **Task 2 (Analysis):** Pairwise alignment and heuristic database search comparing Myoglobin against Hemoglobin alpha and beta. Calculate $Q_3$ secondary structure prediction accuracy using GOR IV vs. crystallographic ground truth from PDB `1MBO`.

---

## 4. Evaluation Scheme & Marks Breakdown (100 Marks)

| Examination Stage | Maximum Marks | Assessment Criteria |
|---|:---:|---|
| **Task 1: Retrieval & Format Dissection** | **35 Marks** | Formulating precise field-tagged queries (10m), accurate coordinate extraction and CDS mathematics (15m), valid format conversion and header interpretation (10m). |
| **Task 2: Computational Analysis & 3D Mapping** | **35 Marks** | Accurate tool parameter execution (BLAST, MSA, ProtParam, GOR) (15m), complete tabular data and significance interpretation (10m), 3D coordinate inspection and active site geometry (10m). |
| **Task 3: Oral Viva Voce Examination** | **30 Marks** | Algorithmic depth and theoretical principles (15m), critical understanding of experimental vs predicted data (10m), scientific fluency and error defense (5m). |
| **Total Marks** | **100 Marks** | Scaled to **10%** of final grade. |
