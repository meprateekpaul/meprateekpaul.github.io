# Analytical Assessment Rubric: Mini-Project (CBBI-501)

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Assessment:** End-to-End Gene Family Characterisation Mini-Project  
**Total Points:** 20.0 Points (Scaled to 10% Continuous Internal Assessment)  
**Evaluation Model:** Analytical Rubric across 5 Core Technical Dimensions (4.0 Points Max per Dimension)  

---

## Rubric Scoring Dimensions at a Glance

| Dimension | Focus Area | Max Score | Weight |
| :---: | :--- | :---: | :---: |
| **D1** | Dataset Assembly, Sequence Retrieval & BLAST Analysis | **4.0 Pts** | 20% |
| **D2** | Multiple Sequence Alignment & Functional Motif Architecture | **4.0 Pts** | 20% |
| **D3** | Phylogenetic Reconstruction, Orthology & Evolutionary Interpretation | **4.0 Pts** | 20% |
| **D4** | Physicochemical Profiling, Secondary Structure & 3D Visualisation | **4.0 Pts** | 20% |
| **D5** | Scientific Writing, Methodological Rigor & Viva Voce Defense | **4.0 Pts** | 20% |
| **Total** | **Comprehensive Project Grade** | **20.0 Pts** | **100%** |

---

## Detailed Performance Level Descriptors

### Dimension 1: Dataset Assembly, Retrieval & BLAST Analysis (4.0 Points)

* **Exemplary (3.6 – 4.0 Points):**  
  Assembles an impeccable dataset of 12–16 sequences spanning broad, representative taxonomic clades (mammals, birds, reptiles, amphibians, teleosts, and invertebrate outgroup). All accessions are authentic, curated RefSeq/Swiss-Prot records. BLASTp analysis is thorough with complete tabular reporting of bit scores, $E$-values, coverage, and identity. Demonstrates sophisticated understanding of Karlin–Altschul statistics to rule out random alignment artifacts.
* **Proficient (2.8 – 3.5 Points):**  
  Assembles 10–12 sequences with reasonable taxonomic breadth, though 1–2 major vertebrate clades may be omitted. Accessions are valid; BLAST hit table is complete with $E$-values and bit scores. Statistical justification is present but basic.
* **Developing (1.6 – 2.7 Points):**  
  Dataset contains $<10$ sequences or suffers from taxonomic redundancy (e.g., almost all mammalian sequences). Missing an appropriate outgroup. BLAST reporting lacks coverage or bit score metrics.
* **Inadequate (0.0 – 1.5 Points):**  
  Fragmented, malformed dataset; unverified accessions; incorrect BLAST flavour executed; no statistical evaluation of homology.

---

### Dimension 2: Multiple Sequence Alignment & Motif Architecture (4.0 Points)

* **Exemplary (3.6 – 4.0 Points):**  
  Executes a rigorous alignment using Clustal Omega, MUSCLE, or MAFFT with documented gap penalties. Alignment is beautifully presented in Jalview with appropriate conservation shading. Accurately identifies invariant catalytic residues, metal coordination centers, or structural disulfides. Successfully integrates PROSITE/InterPro signature patterns with exact sequence coordinates. Generates a clear, informative Sequence Logo.
* **Proficient (2.8 – 3.5 Points):**  
  Generates a clean alignment with appropriate software; identifies major conserved blocks and active site residues. PROSITE patterns are identified, but sequence coordinates or Sequence Logo analysis are incomplete.
* **Developing (1.6 – 2.7 Points):**  
  Alignment displays poorly placed gaps or contains un-trimmed non-homologous sequence tails that distort profiles. Active sites are mentioned vaguely without mapping to alignment columns. No PROSITE grammar analysis.
* **Inadequate (0.0 – 1.5 Points):**  
  Severe alignment errors; unaligned sequences presented; failure to recognize invariant family residues; absent motif analysis.

---

### Dimension 3: Phylogenetic Reconstruction & Evolutionary Interpretation (4.0 Points)

* **Exemplary (3.6 – 4.0 Points):**  
  Constructs a mathematically sound tree in MEGA/IQ-TREE using Neighbor-Joining or Maximum Likelihood under a justified amino acid substitution model with gamma rate correction. Tree is properly rooted on a designated outgroup taxon. Bootstrap analysis ($\ge 500$ replicates) is correctly executed and displayed. Flawlessly differentiates orthologues (speciation nodes) from paralogues (gene duplications) and evaluates gene tree vs species tree concordance.
* **Proficient (2.8 – 3.5 Points):**  
  Constructs a valid tree with bootstrap support values; tree is rooted correctly. Identifies primary orthologous relationships, but discussion of ancient gene duplications (paralogues) is limited or lacks depth.
* **Developing (1.6 – 2.7 Points):**  
  Tree is unrooted or utilizes an inappropriate ingroup taxon as root. Bootstrap values are missing or $<100$ replicates. Confuses orthology with paralogy.
* **Inadequate (0.0 – 1.5 Points):**  
  Unresolved, distorted tree topology; arbitrary branching; no evolutionary model specified; inability to read or interpret a phylogenetic tree.

---

### Dimension 4: Physicochemical Profiling & 3D Structural Visualisation (4.0 Points)

* **Exemplary (3.6 – 4.0 Points):**  
  Complete, comparative ProtParam analysis (MW, pI, charge, extinction coefficient, instability index, GRAVY) across 3 divergent taxa. Hydropathy plots clearly distinguish hydrophobic cores vs solvent-accessible loops. GOR/PSIPRED secondary structure predictions are critically compared to DSSP assignments. Embeds a stunning, high-resolution 3D macromolecular figure (VMD/PyMOL/Mol*) with secondary structure cartoon and labeled active site/ligand sticks. Includes Ramachandran stereochemical validation.
* **Proficient (2.8 – 3.5 Points):**  
  ProtParam metrics and hydropathy plots are complete. Secondary structure predictions and folding classes are accurately identified. 3D PDB structure is identified and rendered cleanly, though residue labeling or lighting in graphics could be improved.
* **Developing (1.6 – 2.7 Points):**  
  ProtParam data is recorded without comparative biological interpretation. Secondary structure percentages omitted. 3D image is a low-resolution default screenshot without active site highlighting or structural caption.
* **Inadequate (0.0 – 1.5 Points):**  
  Missing physicochemical calculations; incorrect PDB ID; failure to generate a 3D structural model; absent stereochemical analysis.

---

### Dimension 5: Scientific Writing, Methodological Rigor & Viva Voce (4.0 Points)

* **Exemplary (3.6 – 4.0 Points):**  
  Report strictly adheres to the 4-page limit and `report_template.md` structure. Written in professional, publication-grade academic prose with zero typographical errors. Figures and tables have exhaustive, informative captions. References follow strict Vancouver style. In the oral viva voce, all group members demonstrate deep technical mastery, fluidly answering algorithmic, biological, and software-specific questions.
* **Proficient (2.8 – 3.5 Points):**  
  Well-written report conforming to page limits and template structure. Minor formatting or citation inconsistencies. Viva voce defense is solid, with students demonstrating competent command of the workflow.
* **Developing (1.6 – 2.7 Points):**  
  Report exceeds 4-page limit or exhibits noticeable formatting flaws. Weak discussion connecting computational results to biological meaning. Viva defense reveals uneven contributions or lack of algorithmic understanding.
* **Inadequate (0.0 – 1.5 Points):**  
  Severely disorganized report; rampant grammatical errors; missing references; signs of direct plagiarism; inability to answer basic questions during the viva defense.
