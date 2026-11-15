# Practical Worksheet 08: Multiple Sequence Alignment Using Clustal Omega and Jalview

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S08 (Syllabus Practical P10)  
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
- [ ] Submitted 7 human globin sequences to Clustal Omega at EMBL-EBI.
- [ ] Parsed the Clustal formatted output and decoded consensus symbols (`*`, `:`, `.`).
- [ ] Exported and opened the alignment `globin_family.aln` in Jalview.
- [ ] Applied Clustalx and Hydrophobicity color palettes.
- [ ] Located the invariant proximal and distal histidine residues.
- [ ] Computed a Neighbor-Joining phylogenetic tree from the alignment.

---

### 2. Execution Log & Tool Workflow

Record your tool settings:
- **Server / Program Used:** `[                                                                ]`
- **Alignment Output File Name:** `[                                                           ]`
- **Number of Sequences Aligned:** `[__________]`
- **Jalview Version / Platform:** `[                                                           ]`

---

### 3. Structured Observation Tables

#### Table 8.1: Invariant and Critical Functional Residues in the Globin Family MSA
| Functional Landmark | HBB Residue & Position | Aligned Column No. in MSA | Residue in HBA1 | Residue in MB | Residue in NGB | Clustal Consensus Token (`*`, `:`, `.`, space) | Biological Role |
|---|:---:|:---:|:---:|:---:|:---:|:---:|---|
| **Distal Histidine (His-E7)** | His-64 | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[_____]` | Stabilizes bound $O_2$ ligand |
| **Proximal Histidine (His-F8)** | His-93 | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[_____]` | Covalently binds heme iron |
| **Invariant Phenylalanine (CD1)** | Phe-43 | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[_____]` | Wedges heme ring in hydrophobic pocket |
| **Sickle Cell Site (E6V)** | Glu-7 | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[_____]` | Surface charge; mutates to Val in HbS |

#### Table 8.2: Clustal Consensus Symbol Interpretation
| Symbol | Mathematical / Property Definition | Count in Globin Family Alignment | Biological Significance |
|:---:|---|:---:|---|
| `*` (Asterisk) | 100% identical residue across all sequences | `[__________]` | Critical structural or catalytic constraint |
| `:` (Colon) | Strongly similar physico-chemical group ($>0.5$ in PAM250) | `[__________]` | Conservative replacement preserving charge/size |
| `.` (Period) | Weakly similar physico-chemical group ($\le 0.5$ in PAM250) | `[__________]` | Semi-conservative replacement |
| ` ` (Space) | No conservation / divergent properties | `[__________]` | Tolerant to evolutionary drift |

---

### 4. Jalview Alignment & Tree Screenshot Box
*Paste a screenshot showing the Jalview window displaying Clustalx coloring and the calculated Neighbor-Joining tree:*

```
+-----------------------------------------------------------------------------------------+
|                                JALVIEW SCREENSHOT                                       |
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

**Q1. The "Once a Gap, Always a Gap" Flaw:** Explain why the progressive alignment strategy cannot correct an alignment error made in early pairwise steps. How do iterative algorithms (e.g., MUSCLE, MAFFT) solve this?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Proximal vs. Distal Histidine Invariance:** Why is the proximal histidine (His-F8) strictly invariant across all globins, including deep outgroups, while distal histidine (His-E7) can occasionally vary?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. Reading the Guide Tree (Orthologues vs. Paralogues):** In the globin family tree, explain why HBB, HBA1, and MB are **paralogues**, while human HBB and chimpanzee HBB are **orthologues**.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Coloring Schemes in Jalview:** Why is coloring an MSA by hydrophobicity particularly useful when inspecting globular proteins like hemoglobin? What periodic pattern do you observe in alpha helices?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. Impact of Adding Divergent Sequences:** If a researcher adds a bacterial truncated globin or plant leghemoglobin to this alignment, what will happen to the total number of asterisk (`*`) consensus positions? Why?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your analysis of the 9 vertebrate HBB orthologues:*
- **Total Identical Columns Across 9 Species:** `[__________]`
- **Most Divergent Vertebrate Species from Human HBB:** `[                                      ]`
- **Evolutionary Divergence Explanation:**
  `[                                                                                             ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & MSA Execution** | 2 | | Understanding of progressive alignment and Clustal execution |
| **Consensus & Landmark Identification** | 4 | | Correct identification of His-E7, His-F8, Phe-CD1, and symbol counts |
| **Jalview Visualization & Tree Analysis** | 2 | | Proper coloring scheme application and guide tree interpretation |
| **Discussion Questions & Critical Viva** | 2 | | Rigorous answers to progressive alignment flaws and orthology/paralogy |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
