# Practical Worksheet 06: Sequence Alignment and Similarity Searching Using BLAST

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S06 (Syllabus Practical P8)  
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
- [ ] Formulated and submitted a blastp query using human HBB (`NP_000509.1`).
- [ ] Restricted database searching to `refseq_protein` and organism `Homo sapiens`.
- [ ] Evaluated graphical summary bars and alignment segment colors.
- [ ] Recorded and interpreted Bit Scores ($S'$) and Expect Values ($E$).
- [ ] Tested parameter variations: BLOSUM62 vs. BLOSUM45 vs. PAM250.
- [ ] Executed a blastx search using *HBB* mRNA (`NM_000518.5`) and identified the coding frame.

---

### 2. Search Execution Parameters Log

Record your parameter configurations:
- **Query Accession & Length:** `[                                                             ]`
- **Target Database & Organism:** `[                                                           ]`
- **Default Word Size ($W$) & Threshold ($T$):** `[                                            ]`
- **Gap Penalties (Existence / Extension):** `[                                                ]`

---

### 3. Structured Observation Tables

#### Table 6.1: Tabular BLASTP Hits for Human HBB (`NP_000509.1`) vs. Human RefSeq
| Subject Accession | Protein Name / Paralog Description | Query Cover (%) | % Identity | Positives (%) | Bit Score ($S'$) | Expect Value ($E$) |
|---|---|:---:|:---:|:---:|:---:|:---:|
| `NP_000509.1` | Hemoglobin subunit beta | 100% | 100.00% | 100% | `[__________]` | `[__________]` |
| `NP_000510.1` | Hemoglobin subunit delta | 100% | 95.24% | `[______]` | `[__________]` | `[__________]` |
| `NP_000550.2` | Hemoglobin subunit gamma-1 | 100% | 73.47% | `[______]` | `[__________]` | `[__________]` |
| `NP_000508.1` | Hemoglobin subunit alpha | 97% | 43.06% | `[______]` | `[__________]` | `[__________]` |
| `NP_005359.1` | Myoglobin | 97% | 28.47% | `[______]` | `[__________]` | `[__________]` |
| `NP_067080.1` | Neuroglobin | 95% | 24.11% | `[______]` | `[__________]` | `[__________]` |

#### Table 6.2: Matrix Sensitivity Comparison for Distant Paralogues
| Target Homologue | Metric | Default (BLOSUM62) | Divergent (BLOSUM45) | Ancient (PAM250) |
|---|---|:---:|:---:|:---:|
| **Myoglobin** (`NP_005359.1`) | Bit Score ($S'$) | `[__________]` | `[__________]` | `[__________]` |
| | Expect Value ($E$) | `[__________]` | `[__________]` | `[__________]` |
| **Neuroglobin** (`NP_067080.1`) | Bit Score ($S'$) | `[__________]` | `[__________]` | `[__________]` |
| | Expect Value ($E$) | `[__________]` | `[__________]` | `[__________]` |

---

### 4. BLAST Output Alignment Screenshot Box
*Paste a screenshot showing the pairwise alignment between HBB query and the Myoglobin subject hit:*

```
+-----------------------------------------------------------------------------------------+
|                                ALIGNMENT SCREENSHOT                                     |
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

**Q1. Bit Score vs. Raw Score:** Why is it scientifically invalid to compare raw alignment scores ($S$) obtained using BLOSUM62 against raw scores obtained using PAM250? How does the bit score ($S'$) solve this?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Database Size Dependence of $E$-value:** If the NCBI RefSeq database doubles in size, what happens to the $E$-value of an identical alignment between HBB and Myoglobin? What happens to the bit score?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. The "Twilight Zone" of Sequence Identity:** Myoglobin shares only 28.5% sequence identity with HBB, placing it in the "twilight zone". Why can we be confident that Myoglobin is truly homologous to HBB despite this low identity? (Cite two specific metrics).  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. BLOSUM Matrix Numbering vs. PAM Numbering:** Explain the opposite numbering conventions of BLOSUM and PAM matrices: Why is BLOSUM45 used for *distant* relatives while PAM250 is used for *distant* relatives?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. Heuristic Seeding Trade-offs:** What happens to BLAST sensitivity and execution run time if the protein word size $W$ is decreased from $W=3$ to $W=2$? Why does NCBI blastp default to $W=3$ or $W=6$?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your findings comparing blastn (nucleotide) versus blastp (protein) detection of distant globin relatives:*
- **Did blastn detect Myoglobin or Neuroglobin?** `[                                             ]`
- **Scientific explanation (codon degeneracy / synonymous saturation):**
  `[                                                                                             ]`
  `[                                                                                             ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Parameter Setup** | 2 | | Correct query, database selection, and algorithm parameters |
| **BLAST Execution & Tabular Data** | 4 | | Accurate recording of scores, E-values, and identities |
| **Matrix Sensitivity Profiling** | 2 | | Accurate comparison between BLOSUM62, BLOSUM45, and PAM250 |
| **Discussion Questions & Critical Viva** | 2 | | Rigorous understanding of E-value math, bit score, and twilight zone |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
