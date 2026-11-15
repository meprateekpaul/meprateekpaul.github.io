# Practical 14: Guided Mini-Project Laboratory Session — End-to-End Characterization of a Biological Gene Family

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S14 (Mini-Project Guided Laboratory Session)  
**Duration:** 2 Hours (In-lab execution and TA consultation; independent report finalization)  
**Learning Outcomes (LO):** LO1 through LO8 (Comprehensive synthesis of database retrieval, alignment, phylogenetics, sequence feature prediction, and structural mapping).

---

## 1. Operational Overview & Project Aim

### Aim
To execute an integrated, multi-stage bioinformatic pipeline that characterizes an assigned biological gene family from initial database retrieval to 3D macromolecular mapping, synthesizing every computational tool mastered across Sessions S01 through S13, and authoring a publication-quality 4-page scientific report.

### Project Organization & Team Charter
- **Team Size:** Groups of 2 to 3 students (or individual assignment as designated by the instructor).
- **Course Weight:** 10% of total course marks.
- **In-Lab Milestone:** Verification and TA sign-off on the 6 pipeline execution milestones during this 2-hour laboratory session.
- **Deliverable:** A standardized 4-page formal scientific report adhering strictly to the structured template detailed in Section 5.

---

## 2. Gene Family Allocations

Each student group is assigned one of the following five benchmark gene families:

### Family 1: The Globin Family (Oxygen Transport & Sensing)
- **Primary Human Anchor:** Hemoglobin subunit beta (*HBB*, `NP_000509.1`, PDB `1A3N`).
- **Family Paralogues to Retrieve:** HBA1, HBB, HBD, HBG1, HBG2, HBE1, HBZ, MB (Myoglobin), NGB (Neuroglobin), CYGB (Cytoglobin).
- **Core Biological Question:** How did ancestral monomeric globins evolve into specialized cooperative tetrameric blood oxygen carriers vs. high-affinity tissue storage molecules?

### Family 2: The Insulin / IGF Family (Metabolic & Growth Signaling)
- **Primary Human Anchor:** Preproinsulin (*INS*, `NP_000198.1`, PDB `4INS` / `1TRZ`).
- **Family Paralogues to Retrieve:** INS, IGF1 (Insulin-like growth factor 1), IGF2, INSL3, INSL4, INSL5, INSL6, Relaxin-1 (RLN1), Relaxin-2 (RLN2).
- **Core Biological Question:** How is the core three-disulfide-bonded structural core conserved across diverse metabolic hormones despite post-translational cleavage of the C-peptide?

### Family 3: The Serpin Superfamily (Serine Protease Inhibitors)
- **Primary Human Anchor:** Alpha-1-antitrypsin (*SERPINA1*, `NP_000286.3`, PDB `1QLP`).
- **Family Paralogues to Retrieve:** SERPINA1, SERPINA3 (Antichymotrypsin), SERPINC1 (Antithrombin-III), SERPIND1 (Heparin cofactor II), SERPINE1 (PAI-1).
- **Core Biological Question:** What conserved sequence motifs drive the dramatic "stressed-to-relaxed" (S-to-R) suicide inhibitory conformational transition?

### Family 4: The Nuclear Hormone Receptor DNA-Binding Domain Family
- **Primary Human Anchor:** Estrogen Receptor Alpha (*ESR1*, `NP_000116.2`, PDB `1HCQ`).
- **Family Paralogues to Retrieve:** ESR1, ESR2, AR (Androgen receptor), PGR (Progesterone receptor), NR3C1 (Glucocorticoid receptor), NR3C2 (Mineralocorticoid receptor).
- **Core Biological Question:** How do conserved C4-type zinc finger coordination motifs maintain high-affinity DNA response element binding across distinct steroid receptors?

### Family 5: The Cytochrome P450 Monooxygenase Family (CYP450)
- **Primary Human Anchor:** Cytochrome P450 2D6 (*CYP2D6*, `NP_000097.3`, PDB `3TDA`).
- **Family Paralogues to Retrieve:** CYP2D6, CYP2C9, CYP2C19, CYP3A4, CYP1A2, CYP2E1.
- **Core Biological Question:** How does the invariant cysteine thiolate coordination motif maintain heme-dependent drug oxidation across polymorphic drug-metabolizing enzymes?

---

## 3. The 6-Stage End-to-End Bioinformatics Pipeline

Every team must execute the following six standardized analytical stages:

```
[Stage 1: Primary Retrieval] -> [Stage 2: Homology Search] -> [Stage 3: Multiple Alignment]
           │                                                                 │
           ▼                                                                 ▼
[Stage 6: 3D Structure Mapping] <- [Stage 5: Physicochemical Profiling] <- [Stage 4: Phylogenetics]
```

### Stage 1: Database Information Retrieval (LO1, LO2)
1. Query NCBI Gene and UniProtKB for the anchor gene.
2. Record chromosomal location, RefSeq mRNA (`NM_`), RefSeq protein (`NP_`), and UniProt accession.
3. Retrieve full-length protein sequences in FASTA format for at least 6–8 human paralogues and 5 vertebrate orthologues.
4. Verify sequence cleanliness (no unverified clones, no truncated fragments).

### Stage 2: Database Similarity Searching (LO3, LO4)
1. Run **blastp** querying the primary human anchor against the RefSeq database.
2. Record hit tables: evaluate Query Coverage, % Identity, Bit Score ($S'$), and $E$-value.
3. Test BLOSUM62 vs. BLOSUM45 to determine sensitivity limits for ancient paralogues.
4. Run a parallel search in **FASTA36** at EMBL-EBI; record $init1$, $initn$, and $opt$ scores.

### Stage 3: Multiple Sequence Alignment & Motif Discovery (LO5, LO6)
1. Combine all family sequences into a single clean multi-FASTA file.
2. Execute multiple sequence alignment using **Clustal Omega** at EMBL-EBI.
3. Export the alignment in Clustal format (`.aln`) and load into **Jalview**.
4. Identify all 100% invariant columns (`*`).
5. Scan the primary sequence in **PROSITE** and **InterPro** to identify family signatures, Pfam domains, and functional active-site residues.

### Stage 4: Molecular Phylogenetic Reconstruction (LO5)
1. In Jalview (or MEGA / IQ-TREE / PhyML), calculate a **Neighbor-Joining (NJ)** phylogenetic tree based on the alignment using the BLOSUM62 distance metric.
2. Root the tree using a biologically appropriate distant outgroup.
3. Identify all internal nodes representing **gene duplication events** (paralogues) versus **speciation events** (orthologues).
4. Evaluate branch lengths and evolutionary divergence patterns.

### Stage 5: Physicochemical & Structural Propensity Profiling (LO6)
1. Run **Expasy ProtParam** on all family members.
2. Compile a comparative table: Molecular Weight, Theoretical $pI$, Extinction Coefficient, Instability Index, Aliphatic Index, and GRAVY score.
3. Generate **Kyte-Doolittle hydropathy plots** in ProtScale ($W=9$ and $W=19$).
4. Run secondary structure prediction using **GOR IV** and **PSIPRED** on the primary anchor.

### Stage 6: 3D Macromolecular Structure Mapping (LO7)
1. Identify high-resolution crystal structures ($<2.5\text{ \AA}$) in RCSB PDB for the anchor protein.
2. Record experimental method, resolution, $R_{\text{work}}$, $R_{\text{free}}$, and bound ligands.
3. Open the structure in **VMD** or **Mol\***.
4. Map the conserved sequence motifs identified in Stage 3 directly onto the 3D structure.
5. Render two publication-quality figures:
   - Figure A: Whole quaternary complex cartoon colored by chain/domain with ligands in licorice.
   - Figure B: High-magnification close-up of the active site/ligand binding pocket with coordination distances labeled.

---

## 4. In-Lab Milestones & Verification Protocol

During the 2-hour practical session, each team must present their intermediate screen outputs to the Laboratory Instructor / TA for milestone verification sign-offs:

- [ ] **Milestone 1 (Minute 20):** Multi-FASTA file constructed and verified in terminal (`grep -c "^>"`).
- [ ] **Milestone 2 (Minute 40):** BLAST hit table and matrix sensitivity comparison completed.
- [ ] **Milestone 3 (Minute 60):** Clustal Omega alignment loaded in Jalview with invariant columns marked.
- [ ] **Milestone 4 (Minute 80):** Phylogenetic tree calculated and rooted with outgroup.
- [ ] **Milestone 5 (Minute 100):** ProtParam comparative matrix and PSIPRED prediction completed.
- [ ] **Milestone 6 (Minute 120):** 3D structural rendering displayed in VMD/Mol* with labeled pocket distances.

---

## 5. Report Template Structure (4-Page Standard)

The final mini-project deliverable is a **strict 4-page scientific manuscript** formatted in PDF/Markdown according to the following structure:

### Page 1: Title, Abstract, Background, and Data Provenance
- **Project Title:** Descriptive, scientific title (e.g., *Evolutionary Diversification and Structural Specialization of the Human Globin Family*).
- **Authors:** Student Names, Roll Numbers, Lab Station, Course Code.
- **Abstract (~200 words):** Concise summary of background, methods used, primary findings, and evolutionary conclusions.
- **Section 1: Biological Background & Family Architecture:** Physiological importance, disease associations, known biological functions.
- **Section 2: Primary Data Retrieval & Accessions:** Complete table of NCBI Gene IDs, RefSeq accessions (`NM_`, `NP_`), UniProt IDs, and PDB codes.

### Page 2: Sequence Alignment, Motif Discovery, and Phylogenetics
- **Section 3: Database Similarity Searching Analysis:** BLASTP vs. FASTA metrics ($S'$, $E$-value, matrix effects).
- **Section 4: Multiple Sequence Alignment & Consensus Analysis:** Aligned fragment figure showing conserved active-site motifs with Clustal annotation symbols (`*`, `:`, `.`).
- **Section 5: Phylogenetic Reconstruction:** Rendered phylogenetic tree figure with labeled duplication and speciation nodes, bootstrap support values (if run), and evolutionary interpretation.

### Page 3: Physicochemical Profiling and Secondary Structure Prediction
- **Section 6: Comparative Physicochemical Matrix:** Comprehensive ProtParam table across all family members (MW, $pI$, charges, instability, GRAVY).
- **Section 7: Hydropathy and Membrane-Spanning Analysis:** ProtScale Kyte-Doolittle curve figure with interpretation of hydrophobic peaks and solvent-exposed troughs.
- **Section 8: Secondary Structure Prediction vs. Ground Truth:** Aligned GOR IV and PSIPRED prediction strings compared against crystallographic DSSP assignment, with calculated $Q_3$ accuracy.

### Page 4: 3D Macromolecular Mapping, Discussion, and References
- **Section 9: Macromolecular Structure & Pocket Mapping:** Two high-resolution rendered 3D figures (Quaternary overview and active-site close-up with atomic distances).
- **Section 10: Biological Synthesis & Critical Discussion:** Synthesis answering the core biological question, addressing mutational tolerance and evolutionary conservation.
- **Section 11: References:** 6–10 formatted bibliographic citations (including primary structural papers and tool citations).

---

## 6. Evaluation Matrix & Rubric (100% Scaled to 10% Course Grade)

| Evaluation Component | Maximum Marks | Specific Criteria |
|---|:---:|---|
| **In-Lab Milestones & TA Sign-offs** | 20 | Completion and verification of all 6 analytical milestones during the lab session. |
| **Data Retrieval & Search Rigor** | 15 | Accuracy of accessions, thoroughness of BLAST/FASTA parameter exploration. |
| **MSA & Phylogenetic Accuracy** | 20 | Quality of alignment curation, correct identification of invariant residues, accurate tree rooting and interpretation. |
| **Physicochemical & Secondary Profiling** | 15 | Accurate ProtParam metrics, clear hydropathy analysis, sound $Q_3$ calculation. |
| **3D Structural Rendering & Pocket Mapping** | 15 | Quality of VMD/Mol* renders, accurate labeling of coordination geometry and residues. |
| **Discussion, Synthesis & Report Polish** | 15 | Depth of scientific reasoning, formatting compliance (strict 4 pages), proper literature citations. |
| **Total Marks** | **100** | Scaled to **10%** of total semester course grade. |
