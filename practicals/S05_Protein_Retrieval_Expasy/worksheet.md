# Practical Worksheet 05: Protein Retrieval from NCBI Protein and UniProtKB/Expasy

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S05 (Syllabus Practical P5)  
**Semester:** B.Tech. Bioinformatics, Semester II  

---

### Student Identification Details
- **Student Name:** __________________________________________________
- **Roll Number:** ____________________________________________________
- **Lab Station / PC No.:** ___________________________________________
- **Date of Practical Performance:** __________________________________
- **Date of Report Submission:** ______________________________________

---

### 1. Pre-Lab Checklist & Learning Objectives Tracker
- [ ] Retrieved RefSeq protein record `NP_000509.1` from NCBI Protein.
- [ ] Retrieved Swiss-Prot curated record `P68871` from UniProtKB.
- [ ] Differentiated between Swiss-Prot (Reviewed) and TrEMBL (Unreviewed).
- [ ] Documented functional annotations, subunit stoichiometry, and PTMs.
- [ ] Resolved the amino acid numbering discrepancy (E6V vs. E7V).
- [ ] Downloaded and inspected the UniProt flat file (`.txt`) syntax.

---

### 2. Search Statement & Identifier Verification Log

Record your identifiers and retrieval timestamps:
- **NCBI Protein Query:** `[                                                                    ]`
- **UniProtKB Primary Accession & Entry Name:** `[                                             ]`
- **Curation Status & Annotation Score:** `[                                                   ]`

---

### 3. Structured Observation Tables

#### Table 5.1: Comparative Annotation Matrix (NCBI Protein vs. UniProtKB Swiss-Prot)
| Feature / Annotation Field | NCBI RefSeq (`NP_000509.1`) | UniProtKB Swiss-Prot (`P68871`) |
|---|---|---|
| Primary Database Category | Automated / RefSeq Curated | Expert Manual Literature Curation |
| Primary Identifier / Accession | `[________________________]` | `[________________________]` |
| Review / Curation Status | `[________________________]` | `[________________________]` |
| Total Sequence Length (aa) | `[_____]` aa | `[_____]` aa |
| Mature Chain Coordinates | `[________________________]` | `[________________________]` |
| Functional Mechanism & Quaternary Structure | `[________________________]` | `[________________________]` |
| Post-Translational Modifications (PTMs) | `[________________________]` | `[________________________]` |
| Natural Variants & Phenotypes Curated | `[________________________]` | `[________________________]` |
| Cross-References to PDB Structures | `[________________________]` | `[________________________]` |
| Cross-References to Medical Genetics | `[________________________]` | `[________________________]` |

#### Table 5.2: Natural Variant Comparison (Sickle Cell Mutation)
| Attribute | Clinical Historical Standard | UniProtKB Curated Coordinate | NCBI RefSeq Coordinate |
|---|---|---|---|
| Mutation Notation | Glu6Val (E6V) | `[____________________]` | `[____________________]` |
| Wild-type Residue | Glutamic acid (Glu / E) | `[____________________]` | `[____________________]` |
| Mutant Residue | Valine (Val / V) | `[____________________]` | `[____________________]` |
| Position Number | 6 | `[__________]` | `[__________]` |
| Biological Explanation for Difference | Circulating mature peptide cleaved | `[____________________________________________________]` | `[____________________________________________________]` |

---

### 4. UniProt Flat File Excerpt Placement Box
*Paste the `FT` (Feature Table) lines from the UniProt entry `P68871` showing the mature `CHAIN` and sickle cell `VARIANT`:*

```
+-----------------------------------------------------------------------------------------+
|                                UNIPROT FLAT FILE EXCERPT                                |
+-----------------------------------------------------------------------------------------+
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
+-----------------------------------------------------------------------------------------+
```

---

### 5. Interpretation & Discussion Questions

**Q1. Swiss-Prot vs. TrEMBL Growth Rates:** Why is UniProtKB/TrEMBL growing exponentially at orders of magnitude faster than UniProtKB/Swiss-Prot? What bottlenecks limit Swiss-Prot manual curation?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Initiator Methionine Cleavage:** Explain why mature circulating human beta-globin contains 146 amino acids, while `NP_000509.1` reports 147 residues. Which enzyme performs this cleavage?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. HbA1c Clinical Biomarker:** In `P68871`, locate the PTM annotation for glycated hemoglobin (HbA1c). Which specific residue is glycated, and why is HbA1c measured in diabetes monitoring?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Primary Accession Stability:** If two distinct Swiss-Prot entries are merged because experimental evidence proves they are the same protein, how does UniProt handle their accession numbers?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. Database Cross-Referencing:** How does UniProtKB integrate functional proteomics with 3D structural biology? Name three structural databases cross-referenced in `P68871`.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your comparison between human HBB (P68871) and mouse HBB (P02088):*
- **Reviewed Mammalian HBB Orthologues Count:** `[__________]`
- **Mouse HBB Initiator Methionine Cleavage Status:** `[                                        ]`
- **Key Conserved Features:** `[                                                               ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Navigation** | 2 | | Understanding of NCBI Protein vs UniProtKB curation tiers |
| **Data Extraction & Comparative Profiling** | 4 | | Thorough completion of Table 5.1 and UniProt feature parsing |
| **Variant Analysis (E6V vs E7V)** | 2 | | Clear biological explanation of initiator methionine removal |
| **Discussion Questions & Critical Viva** | 2 | | Accurate explanations of Swiss-Prot/TrEMBL, HbA1c, and accessions |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
