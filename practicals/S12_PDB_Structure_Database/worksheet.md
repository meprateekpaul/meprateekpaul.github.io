# Practical Worksheet 12: Protein Data Bank (PDB) Navigation and Record Dissection

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S12 (Syllabus Practical P11)  
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
- [ ] Queried RCSB PDB for deoxyhemoglobin entry `1A3N`.
- [ ] Recorded experimental method, resolution, and R-factors.
- [ ] Differentiated the Asymmetric Unit from the Biological Assembly.
- [ ] Inspected and parsed 80-column PDB flat file records (`ATOM`, `HETATM`, `REMARK`).
- [ ] Compared `1A3N` against high-resolution `4HHB` and sickle polymer `2HBS`.
- [ ] Evaluated the physical meaning of the crystallographic $B$-factor.

---

### 2. Search Statement & File Verification Log

Record your structure accessions and terminal commands:
- **PDB Codes Evaluated:** `[                                                                  ]`
- **Local PDB Files Inspected (`ls -lh ../../data/structures/`):**
  ```
  [                                                                                      ]
  [                                                                                      ]
  [                                                                                      ]
  ```

---

### 3. Structured Observation Tables

#### Table 12.1: RCSB PDB Structure Profile for Human Deoxyhemoglobin (`1A3N`)
| Structural Metadata Field | Extracted Record Value | Significance / Explanation |
|---|---|---|
| PDB ID Code | `1A3N` | Unique 4-character identifier |
| Structure Title | `[____________________________________________________]` | Experimental publication title |
| Experimental Method | `[____________________________________________________]` | Primary determination technique |
| Crystallographic Resolution ($\text{\AA}$) | `[__________] Å` | Limiting diffraction detail |
| $R_{\text{work}}$ / $R_{\text{free}}$ | $R_{\text{work}}$: `[_______]` &nbsp; $R_{\text{free}}$: `[_______]` | Agreement between model and observed diffraction |
| Space Group Symmetry | `[____________________________________________________]` | Unit cell symmetry operators |
| Number of Chains in Asymmetric Unit | `[_____]` Chains | Chains in crystallographic asymmetric unit |
| Identity of Chains in Asymmetric Unit | `[____________________________________________________]` | Polypeptide chains present |
| Stoichiometry of Biological Assembly | `[____________________________________________________]` | Physiological quaternary complex |
| Bound Ligands / Cofactors (`HETATM`) | `[____________________________________________________]` | Prosthetic groups & non-protein entities |
| Total Atom Count in File | `[__________]` Atoms | ATOM + HETATM records |

#### Table 12.2: Cross-Structure Comparative Quality Metrics
| Metric | `1A3N` (Standard Deoxy) | `4HHB` (High Resolution) | `2HBS` (Sickle Hemoglobin) |
|---|:---:|:---:|:---:|
| Resolution ($\text{\AA}$) | 2.00 $\text{\AA}$ | `[__________] Å` | `[__________] Å` |
| $R$-factor ($R_{\text{work}}$) | 0.177 | `[__________]` | `[__________]` |
| Space Group | $P\,2_1\,2_1\,2$ | `[__________]` | `[__________]` |
| Quaternary State | Deoxy (T-state) | `[__________]` | `[__________]` |
| Chains in Asymmetric Unit | 2 (Chains A, B) | `[__________]` | `[__________]` |
| Biological Role / Phenotype | Adult oxygen transport | `[__________]` | `[__________]` |

---

### 4. PDB Flat File Header & ATOM Placement Box
*Paste lines showing REMARK 2 (resolution) and the first ATOM record of 1A3N.pdb:*

```
+-----------------------------------------------------------------------------------------+
|                                PDB FLAT FILE EXCERPT                                    |
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

**Q1. Resolution Numbers vs. Quality:** A novice student claims a 3.5 $\text{\AA}$ crystal structure is of higher quality than a 1.8 $\text{\AA}$ structure because 3.5 is larger. Why is this claim wrong? What physical details can be resolved at 1.8 $\text{\AA}$ vs 3.5 $\text{\AA}$?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. The R-free Cross-Validation Metric:** Why did structural biologists invent $R_{\text{free}}$ in addition to $R_{\text{work}}$? How does $R_{\text{free}}$ detect crystallographic "over-fitting"?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. Asymmetric Unit vs. Biological Unit:** Why does the PDB file for `1A3N` contain atomic coordinates for only two globin chains (A and B), even though functional hemoglobin is a tetramer ($\alpha_2\beta_2$)? How is the tetramer reconstructed?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. ATOM vs. HETATM Distinction:** What is the fundamental operational difference between an `ATOM` record and a `HETATM` record in a PDB file? Which record type is used for the heme cofactor, and which for water molecules?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. The Temperature Factor ($B$-factor):** In an `ATOM` record, what does the $B$-factor (e.g., $B = 48.72\text{ \AA}^2$) represent physically regarding atomic mobility or disorder?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your coordinates and calculated distance between Heme Fe and Proximal Histidine:*
- **Heme Fe Coordinates ($X, Y, Z$):** `[                                                      ]`
- **Proximal His Nitrogen Coordinates ($X, Y, Z$):** `[                                       ]`
- **Calculated Bond Distance ($d$):** `[__________] Å`
- **Biological Validation:** `[                                                                ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Navigation** | 2 | | Understanding of PDB architecture and entry reports |
| **Observation Tables & Flat File Dissection** | 4 | | Complete recording of Table 12.1 and Table 12.2 |
| **Comparative Quality Analysis** | 2 | | Accurate contrast across 1A3N, 4HHB, and 2HBS |
| **Discussion Questions & Critical Viva** | 2 | | Rigorous understanding of resolution, R-free, and ASU vs biological unit |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
