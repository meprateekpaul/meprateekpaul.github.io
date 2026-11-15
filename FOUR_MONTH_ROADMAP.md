# Four-Month Accelerated Curriculum & Study Roadmap

> **Course:** Concepts of Bioinformatics (CBBI-501) · B.Tech. Bioinformatics, Semester II  
> **Institutional Provenance:** Inspired by and adapted from the foundational B.Tech. Bioinformatics curriculum of **Sam Higginbottom University of Agriculture, Technology and Sciences (SHUATS)**, Prayagraj, Uttar Pradesh, India ([https://shuats.edu.in/](https://shuats.edu.in/)), Department of Computational Biology and Bioinformatics, Jacob Institute of Biotechnology and Bio-Engineering (JIBB, formerly JSBB).  
> **Target Audience:** First-year undergraduates, graduate cross-trainees, and independent researchers.  
> **Duration:** 15 Teaching Weeks (~4 Calendar Months) · **Effort:** 8–10 hours per week (135–150 total hours)

---

## Pedagogical Philosophy: From Zero to Self-Reliant in 4 Months

Bioinformatics is an inherently multidisciplinary science spanning molecular biology, computational algorithms, and macromolecular biophysics. Students starting this course typically have basic high-school biology but zero programming experience. 

This 4-month roadmap is designed to build intuition before formal abstraction:
1. **Month 1:** Data literacy, database architecture, and sequence file formats.
2. **Month 2:** The algorithmic core — pairwise sequence alignment and database searching.
3. **Month 3:** Evolutionary divergence, multiple alignment, phylogenetics, and sequence-based feature prediction.
4. **Month 4:** 3D macromolecular structures, comparative genomics, and an end-to-end gene family research capstone.

---

## Time Budget & Weekly Commitment

| Activity | Hours / Week | 15-Week Total | Focus & Deliverable |
|---|---|---|---|
| **Lectures (2 per week)** | 2.0 hrs | 30 hrs | Conceptual mastery, slide deck reviews, biological context |
| **Laboratory Sessions** | 2.0 hrs | 30 hrs | Hands-on execution with production web tools (NCBI, EBI, Jalview, VMD) |
| **Jupyter Notebooks** | 2.5 hrs | 37.5 hrs | Run-and-modify Python code (`C`), self-check exercises (`P`), quiz self-tests (`Q`) |
| **Textbook Reading & Review** | 2.0 hrs | 30 hrs | Deep reading in Baxevanis, Mount, or Lesk; cheat sheet reviews |
| **Milestone Assessments** | 1.0 hr | 15 hrs | 4 Quizzes, Assignment 1, Mini-Project, Mid-Term & Final Exams |
| **Total Commitment** | **9.5 hrs / week** | **142.5 hrs** | **Standard 3-credit university course calibration** |

### Computational Notebook Tiering & Delivery Guidance
To prevent cognitive overload while accommodating diverse learner backgrounds:
- **Tier 1 (Core / Mandatory):** Lecture course notebooks (`_C1`, `_C2`, `_C3`) demonstrated in class/lab + Practice tasks rated `★☆☆` and `★★☆` + Quiz notebooks (`_Q`).
- **Tier 2 (Enrichment / Honors):** Challenge problems rated `★★★` in Practice notebooks (e.g. custom sliding-window algorithms and matrix parsers) are designated as optional distinction exercises for students seeking advanced honours credit.

### Capstone Mini-Project Team Role Specialization
Student teams (2–3 students) follow a professional tripartite division of labor:
1. **Genomic & Sequence Curator:** Literature retrieval, RefSeq assembly, multi-FASTA quality control, and nucleotide/promoter feature annotation.
2. **Evolutionary & Alignment Specialist:** Clustal Omega/MUSCLE alignment, Jalview conservation analysis, and MEGA/PhyML phylogenetic tree reconstruction with bootstrap testing.
3. **Structural & Biophysical Analyst:** ProtParam profiling, PROSITE motif scanning, PDB/AlphaFold coordinate inspection, VMD/Mol* 3D rendering, and report synthesis.

---

## Month-by-Month Detailed Roadmap

### Month 1: Biological Data Flow, Databases & Sequence Flat Files
*Objective: Understand where biological data lives, how it gets there, and how to programmatically and manually extract clean sequence records.*

#### Week 1: The Bioinformatic Paradigm & Command-Line Foundations
- **Theory (L01–L02):** The Central Dogma as an information flow; explosive data growth; client-server models, HTTP vs. FTP; NCBI, EBI, DDBJ INSDC exchange.
- **Lab (S01):** Linux CLI mastery: navigation (`pwd`, `ls`, `cd`), manipulation (`mkdir`, `cp`, `mv`, `rm`), text inspection (`cat`, `less`, `head`, `tail`, `wc`, `grep`), pipes (`|`), and redirection (`>`).
- **Notebooks:** `U01_C1_Sequences_as_Text`, `U01_P_Sequences_as_Text`, `U01_Q_Bioinformatics_and_Internet`.
- **Milestone:** Count sequences in a multi-FASTA file in the terminal with `grep -c ">"` and compute nucleotide composition in Python.

#### Week 2: Information Retrieval & The Entrez Ecosystem
- **Theory (L03–L04):** Entrez database indexing; cross-database links and neighbors; UID systems; Accession vs. GI; RefSeq prefixes (`NM_`, `NP_`, `NC_`); MeSH vocabulary.
- **Lab (S02–S03):** Guided exploration of NCBI Gene, Nucleotide, and Protein; PubMed Boolean queries and field-tag filters (`[ORGN]`, `[GENE]`, `[TITL]`).
- **Notebooks:** `U02_C1_Entrez_Search_from_Python`, `U02_P_Entrez_Search`, `U02_Q_Information_Retrieval`.
- **Milestone:** Write a query that isolates human *HBB* mRNA without including pseudogenes or related globins.

#### Week 3: The NCBI Data Model
- **Theory (L05–L06):** Why relational tables fail for biological data; ASN.1 data trees; Bioseq, Bioseq-set; Seq-id, Seq-annot, Seq-feat, and Seq-descr.
- **Lab:** Integrated inspection of ASN.1 vs. XML vs. GenBank flat-file presentations.
- **Notebooks:** `U03_C1_Inside_a_Sequence_Record`, `U03_P_NCBI_Data_Model`, `U03_Q_NCBI_Data_Model`.
- **Milestone:** Map flat-file sections onto their underlying ASN.1 objects.

#### Week 4: GenBank Flat File Anatomy & Sequence Formats
- **Theory (L07–L09):** Primary vs. secondary databases (GenBank vs. RefSeq, Swiss-Prot vs. TrEMBL); line-by-line breakdown of LOCUS, DEFINITION, FEATURES, and ORIGIN; FASTA, GenBank, EMBL formats.
- **Lab (S04–S05):** Retrieving *NM_000518*; extracting CDS coordinates; protein retrieval from NCBI Protein and UniProtKB/Swiss-Prot (`P68871`); format conversion via EMBOSS `seqret`.
- **Notebooks:** `U04_C1_GenBank_Flat_File`, `U04_C2_Formats_and_Conversion`, `U04_P_GenBank_and_Formats`, `U04_Q_GenBank_Database`.
- **Assessment:** **Quiz 1 (Units 1–3)**.

> **Month 1 Competency Check:**  
> Can you locate any human gene on NCBI, retrieve its exact RefSeq mRNA and protein translation, explain every feature in its flat file, and slice its coding sequence in Python? If yes, proceed to Month 2.

---

### Month 2: Sequence Alignment & Database Searching (The Algorithmic Core)
*Objective: Master pairwise dynamic programming by hand and understand how heuristic tools (BLAST, FASTA) search millions of sequences in seconds.*

#### Week 5: Evolutionary Basis of Sequence Alignment & Dot Plots
- **Theory (L10):** Homology vs. similarity; orthology vs. paralogy introduced; identity vs. conservative substitution; 2D dot plots for indels, repeats, and inversions.
- **Lab (Preparation):** Building dot matrices for alpha vs. beta globin.
- **Notebooks:** `U05_C1_Dot_Plots_and_Global_Alignment`.
- **Milestone:** Diagnose an inversion and an internal duplication from a dot plot pattern.

#### Week 6: Optimal Pairwise Alignment: Needleman–Wunsch & Smith–Waterman
- **Theory (L11–L12):** Global alignment dynamic programming (Needleman–Wunsch initialization, recurrence, and traceback); local alignment (Smith–Waterman zero-floor rule); linear vs. affine gap penalties.
- **Lab (S06 Part 1):** Calculating hand matrices on toy sequences ($6 \times 6$ residues).
- **Notebooks:** `U05_C2_Local_Alignment_and_Scoring`.
- **Milestone:** Fill a complete $6 \times 6$ Needleman–Wunsch matrix by hand and deduce all optimal traceback paths.

#### Week 7: Substitution Matrices & Alignment Statistics
- **Theory (L13):** Log-odds scoring; derivation of Dayhoff PAM matrices (accepted point mutations); Henikoff BLOSUM matrices (Blocks database); BLOSUM62 vs. BLOSUM45 vs. BLOSUM80; Karlin–Altschul statistics; raw score $S$, bit score $S'$, and Expect value ($E$).
- **Lab (S07):** Sequence similarity searching using FASTA / SSEARCH at EMBL-EBI; comparing Smith–Waterman rigorous search vs. FASTA lookup.
- **Notebooks:** `U05_C3_Reading_BLAST_Results`, `U05_P_Sequence_Alignment`, `U05_Q_Sequence_Alignment`.
- **Assessment:** **Quiz 2 (Hand Alignment Worked Matrix)**.

#### Week 8: Heuristics, Artifacts & Profile Searching
- **Theory (L14–L15):** The BLAST algorithm: word matches ($W$), neighborhood threshold ($T$), high-scoring segment pairs (HSPs), two-hit seed extension; BLAST flavors (`blastn`, `blastp`, `blastx`, `tblastn`, `tblastx`); artifacts (low-complexity filters SEG/DUST, compositional bias); Position-Specific Scoring Matrices (PSSMs) and PSI-BLAST.
- **Lab (S06 Part 2):** Running NCBI BLASTP with human HBB; testing the impact of changing matrices (BLOSUM62 vs. PAM30) and disabling SEG filtering.
- **Assessment:** **Mid-Semester Formal Examination (Units 1–5, 50 Marks)**.

> **Month 2 Competency Check:**  
> Can you calculate an optimal dynamic programming alignment by hand, explain why a bit score is independent of database size, choose between blastp and blastx, and spot a false-positive caused by a low-complexity repeat? If yes, proceed to Month 3.

---

### Month 3: Multi-Sequence Evolution, Phylogenetics & Sequence Prediction
*Objective: Reconstruct the evolutionary history of gene families and predict structural and physical phenotypes directly from sequence.*

#### Week 9: Multiple Sequence Alignment (MSA)
- **Theory (L16–L17):** Why pairwise alignment is insufficient; exact multidimensional dynamic programming complexity ($O(L^N)$); progressive alignment heuristics (guide trees, profile-profile alignment); "once a gap, always a gap" caveat; Clustal Omega, MUSCLE, MAFFT, T-Coffee.
- **Lab (S08):** Building a 7-member globin family MSA using Clustal Omega; visualizing conserved active site residues (distal His63, proximal His92) in Jalview.
- **Notebooks:** `U06_C1_Multiple_Alignment_and_Conservation`, `U06_P_Multiple_Alignment`, `U06_Q_Multiple_Alignment`.
- **Milestone:** Issue **Assignment 1** ("Characterise an Unknown Sequence").

#### Week 10: Phylogenetic Analysis & Tree Interpretation
- **Theory (L18–L20):** Tree terminology (root, node, branch, clade, outgroup); cladogram vs. phylogram; gene trees vs. species trees; distance methods: UPGMA (ultrametric, molecular clock) worked by hand, Neighbor-Joining (NJ, minimum evolution); character methods in outline; bootstrap resampling and statistical support.
- **Lab (Extension of S08):** Computing a distance matrix and generating UPGMA and NJ trees from the globin MSA; interpreting the early divergence of myoglobin and the duplication of alpha and beta lineages.
- **Notebooks:** `U07_C1_Distances_and_Trees`, `U07_P_Phylogenetic_Trees`, `U07_Q_Phylogenetic_Analysis`.
- **Assessment:** **Quiz 3 (Units 6–7)**.

#### Week 11: Predictive Methods for Nucleotide Sequences
- **Theory (L21–L22):** What DNA sequence alone reveals; repetitive elements (transposons, tandem repeats) and RepeatMasker; open reading frames (ORFs) and 6 reading frames; prokaryotic vs. eukaryotic gene architectures; codon usage bias and synonymous codon usage tables; CpG islands and promoter motifs.
- **Lab (S09):** ORF finding on uncharacterized cDNA contigs with NCBI ORFfinder; EMBOSS `geecee`, `cusp`, and `transeq`; identification of splice donor/acceptor consensus sequences.
- **Notebooks:** `U08_C1_ORFs_GC_and_Codon_Usage`, `U08_P_Nucleotide_Analysis`, `U08_Q_Predictive_Nucleotide`.
- **Milestone:** Identify the correct coding frame of an unlabelled transcript containing 5' and 3' UTRs.

#### Week 12: Predictive Methods for Protein Sequences
- **Theory (L23–L25):** Physicochemical properties from primary sequence: molecular weight, isoelectric point (pI), extinction coefficient, instability index, GRAVY hydropathy; Kyte-Doolittle hydrophobicity scales; motifs, signatures, and patterns (PROSITE regex syntax); Pfam and InterPro; secondary structure prediction: Chou–Fasman, GOR IV statistical method, PSIPRED neural networks; $Q_3$ accuracy metric.
- **Lab (S10–S11):** SIB Expasy ProtParam and ProtScale for HBB and membrane transporter; PROSITE pattern scanning for heme-binding signature; running GOR IV and PSIPRED; calculating $Q_3$ prediction accuracy against the crystallographic DSSP assignment.
- **Notebooks:** `U09_C1_Protein_Properties_and_Motifs`, `U09_C2_Secondary_Structure_Prediction_Scoring`, `U09_P_Protein_Prediction`, `U09_Q_Predictive_Protein`.
- **Deliverable:** **Assignment 1 Due**; **Mini-Project Brief Issued**.

> **Month 3 Competency Check:**  
> Can you align 10 homologous proteins, build a rooted phylogenetic tree, identify which nodes represent gene duplication vs. speciation, scan a sequence for functional motifs, and compute $Q_3$ secondary structure accuracy? If yes, proceed to Month 4.

---

### Month 4: Structural Macromolecules, Comparative Genomics & Capstone
*Objective: Transition from 1D sequences to 3D atomic structures, compare full genomes, and synthesize all skills into an independent research report.*

#### Week 13: Macromolecular Structure Databases & 3D Visualization
- **Theory (L26–L27):** Primary, secondary, tertiary, and quaternary structural hierarchies; structure determination methodologies: X-ray crystallography (diffraction, electron density, resolution, $R$-factor), NMR spectroscopy, cryo-EM; the Protein Data Bank (PDB, wwPDB) and NCBI MMDB; anatomical dissection of a PDB file (`HEADER`, `SEQRES`, `ATOM`, `HETATM`, `CONECT`).
- **Lab (S12–S13):** Querying RCSB PDB for deoxyhemoglobin `1A3N` and high-resolution `4HHB`; molecular visualization in VMD / Mol\*: secondary structure cartoon rendering, color by chain, isolating the heme pocket, and highlighting residue 6 (Glu vs. Val in sickle cell `2HBS`).
- **Notebooks:** `U10_C1_Reading_a_PDB_File`, `U10_P_PDB_Structures`, `U10_Q_Structure_Databases`.
- **Milestone:** Generate publication-quality 3D renders displaying the molecular structural consequence of the sickle-cell mutation.

#### Week 14: Structural Comparison, Modeling & Capstone Workshop
- **Theory (L28):** Why structure is 3–10 times more conserved than sequence; structure alignment and similarity searching (DALI, VAST+); principles of homology modeling (template selection, alignment, backbone generation, loop modeling, side-chain placement, energy refinement); introduction to AlphaFold DB and understanding pLDDT confidence scores.
- **Lab (S14):** Dedicated group research session for the **Mini-Project** (gene family characterization).
- **Notebooks:** Mini-project pipeline execution in Python.
- **Assessment:** **Quiz 4 (Units 8–10)**.

#### Week 15: Comparative Genome Analysis, Synthesis & Examination
- **Theory (L29–L30):** Genome project workflows: shotgun sequencing, de novo assembly, structural annotation (gene finders), functional annotation (homology, GO terms); synteny and chromosomal rearrangements; comparative genomics of pathogens vs. commensals; minimal bacterial gene sets; course wrap-up.
- **Lab (S15):** **Practical Examination and Viva Voce** (Randomly drawn sequence retrieval task + computational analysis challenge).
- **Notebooks:** `U11_C1_Comparing_Two_Genomes`, `U11_P_Comparative_Genomics`, `U11_Q_Comparative_Genomics`.
- **Deliverables:** **Mini-Project Report & Presentation Due**; **End-Semester Comprehensive Final Exam (100 Marks)**.

> **Final Competency Check:**  
> A student who completes this 4-month sequence has analyzed real sequence variations, retrieved records from international repositories, computed dynamic programming alignments, evaluated statistical significance, built phylogenetic trees, predicted physical and structural attributes, manipulated 3D atomic models, and compared genomes. They are thoroughly equipped for advanced study in Genomics, Proteomics, Molecular Modeling, and Drug Design.

---

## 4-Month Self-Study vs. University Pacing Adaptations

| Trainee Profile | Recommended Adjustment |
|---|---|
| **University B.Tech. Cohort** | Follow the 15-week schedule exactly. Lab sessions coincide with weekly practicals. Quizzes administered in Weeks 4, 7, 11, and 14. |
| **Intensive Self-Learner (Full-Time)** | Can compress to **8 Weeks** (~18–20 hours/week): Complete 2 units per week. Run notebooks daily. |
| **Part-Time Trainee / Professional** | Keep the **15-Week schedule**: Allocate 2 hours on 4 evenings per week plus a 2-hour weekend practical session. |
