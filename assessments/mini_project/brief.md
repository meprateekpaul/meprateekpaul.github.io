# Mini-Project Brief: End-to-End Gene Family Characterisation

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Weightage:** 10% of Continuous Internal Assessment  
**Group Size:** Collaborative teams of 2 to 3 students  
**Timeline:**
* **Issued:** Week 12 (Lecture 24)
* **Dedicated Lab Session:** Week 14 (Practical Session S14)
* **Report Due:** Week 15 (Start of Practical Session S15)
* **Viva Voce Presentation:** Week 15 (Practical Exam Session)

---

## 1. Project Overview & Learning Objectives

The Mini-Project represents the capstone practical milestone of the *Concepts of Bioinformatics* course. Over the semester, you have developed proficiency in disconnected computational techniques: database query formulation, dynamic programming, heuristic searching (BLAST), multiple sequence alignment, molecular phylogenetics, protein physicochemical analysis, and 3D macromolecular visualization.

In this project, your team will integrate these methods into a single, cohesive, publication-quality **End-to-End Gene Family Characterisation Pipeline**. Each team will select (or be assigned) one of the 12 pre-screened gene families listed in `gene_families.md`. Starting from a human reference gene, your team will trace the family's evolutionary history across vertebrates and invertebrates, discover conserved active site motifs, determine structural stability constraints, and examine its 3D macromolecular architecture.

---

## 2. Seven-Stage Computational Methodology Workflow

Every group must systematically execute and document the following seven stages:

```
[Stage 1: Literature & Database Retrieval]
                   │
                   ▼
[Stage 2: Taxonomic Sampling & Dataset Assembly (12–16 Taxa)]
                   │
                   ▼
[Stage 3: BLAST Similarity & Orthology Validation]
                   │
                   ▼
[Stage 4: Multiple Sequence Alignment & Motif Extraction]
                   │
                   ▼
[Stage 5: Phylogenetic Reconstruction (Tree, Orthologues, Paralogues)]
                   │
                   ▼
[Stage 6: Physicochemical Profiling & Secondary Structure Prediction]
                   │
                   ▼
[Stage 7: 3D Macromolecular Modeling & Active Site Visualisation]
```

### Stage 1: Literature Curation & Entrez Retrieval
* Query PubMed using MeSH terms and Boolean field tags to identify foundational papers describing your gene family's discovery, physiological function, and disease associations.
* Retrieve the gold-standard human reference mRNA (`NM_...`) and protein (`NP_...` / UniProt Swiss-Prot `P...`) records.

### Stage 2: Diverse Taxonomic Sampling (12 to 16 Sequences)
* Assemble a curated FASTA dataset comprising 12 to 16 homologous sequences representing broad evolutionary divergence:
  - **Mammals:** Human, Chimpanzee, Rodent (Mouse/Rat), Artiodactyl (Bovine/Horse)
  - **Birds:** Chicken (*Gallus gallus*)
  - **Reptiles / Amphibians:** Lizard / *Xenopus tropicalis*
  - **Fish:** Zebrafish (*Danio rerio*) / Fugu
  - **Invertebrates / Outgroup:** Fruit fly (*Drosophila*), Nematode (*C. elegans*), or an ancient paralogue / outgroup.
* Ensure all records are saved in standardized multi-FASTA format with descriptive headers (`>Gene_Species_Accession`).

### Stage 3: BLAST Search & Statistical Validation
* Perform `blastp` searches against the RefSeq database using the human reference query.
* Record bit scores, $E$-values, query coverage, and percentage identity across taxonomic boundaries.
* Verify that your selected sequences are true homologues rather than compositionally biased false-positives.

### Stage 4: Multiple Sequence Alignment & Motif Architecture
* Align your sequence dataset using **Clustal Omega**, **MUSCLE**, or **MAFFT**.
* Inspect and shade the alignment in **Jalview** (color by Clustalx or percentage identity).
* Scan the family against **PROSITE** and **InterPro** to identify family signature patterns, catalytic triads, metal-coordinating residues, or invariant cysteines forming disulfide bonds.
* Generate a **Sequence Logo** for the primary catalytic/conserved motif.

### Stage 5: Molecular Phylogenetic Analysis
* Import your trimmed alignment into **MEGA** (or **PhyML** / **IQ-TREE**).
* Construct a phylogenetic tree using **Neighbor-Joining (NJ)** or **Maximum Likelihood (ML)** under an appropriate amino acid substitution model (e.g., JTT, WAG, or Dayhoff with gamma-distributed rates).
* Conduct **Bootstrap Analysis** with at least 500 pseudo-replicates.
* Root the tree using your designated outgroup taxon.
* Unambiguously label **Orthology** vs **Paralogy** divergence nodes on the tree.

### Stage 6: Physicochemical Profiling
* Process the human reference and two divergent orthologues through **Expasy ProtParam**.
* Tabulate and compare: Molecular Weight, theoretical pI, Extinction Coefficient, Instability Index, and GRAVY score.
* Generate a comparative **Kyte–Doolittle hydropathy plot** (ProtScale) to assess conserved hydrophobic cores or transmembrane domains.

### Stage 7: 3D Macromolecular Visualisation
* Retrieve the primary experimental 3D structure from the **RCSB PDB**.
* Using **VMD**, **PyMOL**, or **Mol***:
  - Render a secondary structure cartoon colored by chain or fold domain.
  - Highlight key functional active site residues, catalytic residues, or bound ligands/prosthetic groups in sticks with explicit atom coloring and residue labels.
  - Validate backbone stereochemistry using a **Ramachandran Plot**.

---

## 3. Required Deliverables and Submission Instructions

By **Week 15**, each team must submit:

1. **Formal Scientific Report (PDF):**  
   - Maximum **4 pages** (strict adherence to `report_template.md`).  
   - Structured into: Title, Authors, Abstract, Introduction, Methods, Results & Discussion, Conclusion, References.
2. **Supplementary Data Archive (.zip):**  
   - Raw multi-FASTA sequence file (`unaligned_sequences.fasta`).  
   - Aligned FASTA / Clustal file (`aligned_sequences.aln`).  
   - Newick phylogenetic tree file (`tree.nwk`).  
   - High-resolution 300 DPI 3D molecular rendering image (.png).
3. **Oral Defense & Viva Voce (10 Minutes):**  
   - 6-minute slide presentation (max 6 slides) during the Practical Examination session, followed by 4 minutes of individual technical questioning by the instructor.

---

## 4. Assessment Criteria Summary

Evaluation is strictly analytical, following the 20-point rubric in `rubric.md`:
* **Dataset Quality & Retrieval:** 4 Points
* **MSA & Motif Analysis:** 4 Points
* **Phylogenetic Reconstruction:** 4 Points
* **3D Structural Visualisation:** 4 Points
* **Scientific Writing & Viva Voce:** 4 Points  
*(Total 20 Points = 10% Continuous Evaluation Grade).*
