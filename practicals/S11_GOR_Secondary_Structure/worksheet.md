# Practical Worksheet 11: Protein Secondary Structure Prediction and Validation

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S11 (Syllabus Practical P13)  
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
- [ ] Submitted human HBB sequence (`NP_000509.1`) to PBIL NPS@ GOR IV.
- [ ] Submitted sequence to UCL PSIPRED V4.0.
- [ ] Retrieved crystallographic ground-truth DSSP annotation from PDB `1A3N` (Chain B).
- [ ] Aligned 147-character prediction strings with ground truth.
- [ ] Computed three-state accuracy ($Q_3$) by hand for GOR IV and PSIPRED.
- [ ] Evaluated the biological significance of spurious $\beta$-strands in the globin fold.

---

### 2. Prediction Execution Log & Server Parameters

Record your server runs:
- **GOR IV Server URL & Method:** `[                                                            ]`
- **PSIPRED Job Identifier & Date:** `[                                                        ]`
- **PDB Reference Structure Used:** `[                                                         ]`

---

### 3. Structured Observation Tables

#### Table 11.1: Secondary Structure Composition Comparison for Human HBB
| Structural State | Crystallographic Truth (DSSP 1A3N Chain B) | GOR IV Prediction | PSIPRED V4.0 Prediction |
|---|:---:|:---:|:---:|
| **$\alpha$-Helix ($H$)** (Residue Count / %) | `[_____]` / `[____]%` | `[_____]` / `[____]%` | `[_____]` / `[____]%` |
| **$\beta$-Strand ($E$)** (Residue Count / %) | 0 / 0.0% | `[_____]` / `[____]%` | `[_____]` / `[____]%` |
| **Coil / Loop ($C$)** (Residue Count / %) | `[_____]` / `[____]%` | `[_____]` / `[____]%` | `[_____]` / `[____]%` |
| Total Residues | 147 / 100.0% | 147 / 100.0% | 147 / 100.0% |

#### Table 11.2: Three-State Prediction Accuracy ($Q_3$) Calculation
| Method | Total Residues ($N_{\text{total}}$) | Correctly Predicted Residues ($N_{\text{correct}}$) | Number of Mismatches | Calculated $Q_3$ Accuracy (%) |
|---|:---:|:---:|:---:|:---:|
| **GOR IV** | 147 | `[__________]` | `[__________]` | `[__________]%` |
| **PSIPRED V4.0** | 147 | `[__________]` | `[__________]` | `[__________]%` |

#### Table 11.3: Alignment of Ground Truth vs. Predictions
```
Residue No: 1         10        20        30        40
Sequence:   MVHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQ
DSSP 1A3N:  CCHHHHHHHHHHHHHHHCCCCCCCCHHHHHHHHHHHCCCH
GOR IV:     [                                      ]
PSIPRED:    [                                      ]

Residue No: 41        50        60        70        80
Sequence:   RFFESFGDLSTPDAVMGNPKVKAHGKKVLGAFSDGLAHLD
DSSP 1A3N:  HHHHHHHCCCCCCCCCCCHHHHHHHHHHHHHHCCCCCHHH
GOR IV:     [                                      ]
PSIPRED:    [                                      ]

Residue No: 81        90        100       110       120
Sequence:   NLKGTFATLSELHCDKLHVDPENFRLLGNVLVCVLAHHFG
DSSP 1A3N:  HHHHHHHHHHHHHHHCCCCCCCCCHHHHHHHHHHHHHHHH
GOR IV:     [                                      ]
PSIPRED:    [                                      ]

Residue No: 121       130       140     147
Sequence:   KEFTPPVQAAYQKVVAGVANALAHKYH
DSSP 1A3N:  CCCCCCCHHHHHHHHHHHHHHHHHHHCCC
GOR IV:     [                           ]
PSIPRED:    [                           ]
```

---

### 4. PSIPRED Graphic Output Screenshot Box
*Paste a screenshot showing the PSIPRED secondary structure cartoon and confidence histogram:*

```
+-----------------------------------------------------------------------------------------+
|                                PSIPRED OUTPUT GRAPHIC                                   |
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

**Q1. Why GOR IV Predicts Spurious $\beta$-Strands:** Inspect residues 40 to 46 (`FFESFGD`) in the GOR IV output. Why does GOR IV predict an extended $\beta$-strand (`EEEEEE`) here when the crystal structure has an $\alpha$-helix or loop?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. The Power of Evolutionary Profiles:** Why does PSIPRED achieve substantially higher accuracy ($>80\%$) than GOR IV (~65%)? How does a PSI-BLAST PSSM supply critical information that raw sequence lacks?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. The All-$\alpha$ Globin Fold:** How many $\alpha$-helices comprise the canonical globin fold, and what structural feature maintains the stability of these helices in the absence of $\beta$-sheets?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Limits of $Q_3$ Evaluation:** Why is the $Q_3$ percentage metric sometimes misleading for proteins with extreme class imbalance (e.g., 95% helical)? What complementary metrics provide a fairer assessment?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. Modern Machine Learning in Secondary Structure:** AlphaFold2 predicts full 3D atomic coordinates directly from MSAs. Does this render secondary structure prediction obsolete, or does it still play a role?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your findings on Segment Overlap (SOV) and PSIPRED confidence correlation:*
- **Accuracy on High-Confidence Residues ($\text{Conf} \ge 7$):** `[__________]%`
- **Importance of Segment Overlap ($SOV$) over $Q_3$:**
  `[                                                                                             ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Server Execution** | 2 | | Proper execution of GOR IV and PSIPRED |
| **Observation Tables & String Alignment** | 4 | | Complete recording of Table 11.1, 11.2, and 11.3 |
| **$Q_3$ Calculation Accuracy** | 2 | | Accurate manual calculation of $Q_3$ percentage |
| **Discussion Questions & Critical Viva** | 2 | | Sound scientific reasoning regarding PSSMs, GOR flaws, and DSSP |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
