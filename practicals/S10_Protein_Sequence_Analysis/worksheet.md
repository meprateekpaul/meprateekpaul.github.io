# Practical Worksheet 10: Protein Physicochemical Profiling and Domain Analysis

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S10 (Syllabus Practical P6)  
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
- [ ] Computed physicochemical parameters of HBB (`P68871`) using ProtParam.
- [ ] Computed parameters for the sickle-cell variant (HbS) and compared pI values.
- [ ] Analyzed preproinsulin (`P01308`) as a comparative control.
- [ ] Generated Kyte-Doolittle hydropathy plots in ProtScale ($W=9$ vs. $W=19$).
- [ ] Scanned the sequence in PROSITE for globin signatures.
- [ ] Mapped Pfam and InterPro domain architectures.

---

### 2. Tool Execution Log

Record your tool parameters:
- **ProtParam Accessions Evaluated:** `[                                                         ]`
- **ProtScale Hydropathy Scale & Window Sizes:** `[                                            ]`
- **ScanProsite Pattern ID Detected:** `[                                                      ]`
- **InterPro Family ID:** `[                                                                   ]`

---

### 3. Structured Observation Tables

#### Table 10.1: Comparative Physicochemical Profiles (ProtParam)
| Physicochemical Parameter | Wild-Type HBB (`P68871`) | Sickle-Cell HbS Variant | Human Preproinsulin (`P01308`) |
|---|:---:|:---:|:---:|
| Sequence Length (aa) | 147 | 147 | 110 |
| Molecular Weight ($M_r$, Da) | 15,998.18 | `[__________]` | `[__________]` |
| Theoretical Isoelectric Point ($pI$) | 6.75 | `[__________]` | `[__________]` |
| Total Negative Residues (Asp + Glu) | 14 | `[_____]` | `[_____]` |
| Total Positive Residues (Arg + Lys) | 14 | `[_____]` | `[_____]` |
| Extinction Coefficient ($\epsilon_{280}$, $\text{M}^{-1}\text{cm}^{-1}$) | 8,480 | `[__________]` | `[__________]` |
| Instability Index ($II$) | 33.74 | `[__________]` | `[__________]` |
| Classification (Stable / Unstable) | Stable | `[__________]` | `[__________]` |
| Aliphatic Index | 91.09 | `[__________]` | `[__________]` |
| Grand Average Hydropathicity (GRAVY) | -0.111 | `[__________]` | `[__________]` |
| Primary Cellular Localization | Cytosolic | Cytosolic | Secreted / Hormone |

#### Table 10.2: Functional Motif and Domain Annotations (PROSITE & InterPro)
| Database | Accession / Identifier | Domain / Motif Name | Span Coordinates | Biological / Structural Function |
|---|:---:|:---:|:---:|---|
| **PROSITE** | `PS00017` | `GLOBLN` | `[__________]` | Characteristic globin signature motif |
| **Pfam** | `PF00042` | Globin | `[__________]` | All-alpha helical globin fold |
| **InterPro** | `IPR000971` | Globin | `[__________]` | Oxygen-binding hemeprotein family |
| **CATH / Gene3D** | `1.10.490.10` | Globin-like | `[__________]` | Orthogonal alpha-helical bundle |

---

### 4. ProtScale Hydropathy Plot Screenshot Box
*Paste a screenshot showing the Kyte-Doolittle hydropathy curve for HBB (Window Size = 9):*

```
+-----------------------------------------------------------------------------------------+
|                                HYDROPATHY PLOT SCREENSHOT                               |
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

**Q1. Electrophoretic Shift of Sickle Hemoglobin:** Based on your ProtParam calculations for Table 10.1, explain why HbS migrates differently from HbA in alkaline gel electrophoresis (pH 8.6).  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Molecular Basis of HbS Polymerization:** The E6V mutation substitutes charged Glu with hydrophobic Val. What hydrophobic pocket on the adjacent subunit does this mutant valine insert into under deoxygenated conditions?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. Interpreting the Instability Index:** What does Guruprasad's Instability Index ($II = 33.74$) signify regarding the *in vitro* stability of HBB? If an engineered enzyme yields $II = 58.2$, what does this predict?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Aliphatic Index and Thermostability:** HBB has an aliphatic index of $91.09$. Which specific amino acids contribute to this index, and how do they stabilize globular proteins?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. GRAVY Score Thresholds:** Explain the physical significance of a negative GRAVY score ($-0.111$) for HBB versus a strongly positive GRAVY score ($>+0.8$) for a multi-pass membrane protein.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your findings for Human Rhodopsin (P08100) Kyte-Doolittle profiling:*
- **Window Size Used:** `[_____]`
- **Number of Peaks Exceeding +1.6:** `[_____]`
- **Agreement with 7-Transmembrane Architecture:** `[                                           ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & ProtParam Execution** | 2 | | Correct retrieval of physicochemical metrics |
| **Comparative Profiling (Table 10.1 & 10.2)** | 4 | | Accurate recording of HbA vs HbS and InterPro domains |
| **Hydropathy Analysis (ProtScale)** | 2 | | Proper interpretation of Kyte-Doolittle curve & window sizes |
| **Discussion Questions & Critical Viva** | 2 | | Rigorous understanding of pI shifts, instability, and GRAVY |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
