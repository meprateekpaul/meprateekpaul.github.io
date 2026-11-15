# Practical Worksheet 07: Sequence Similarity Searching Using the FASTA Suite

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S07 (Syllabus Practical P9)  
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
- [ ] Submitted a protein FASTA query at EMBL-EBI with human HBB (`NP_000509.1`).
- [ ] Executed FASTA with default parameters ($ktup=2$, BLOSUM50).
- [ ] Extracted and recorded $init1$, $initn$, $opt$, and $E$-value metrics.
- [ ] Resubmitted the search with $ktup=1$ and observed changes in sensitivity.
- [ ] Executed an exhaustive SSEARCH (Smith-Waterman) run for comparison.
- [ ] Contrasted the four-stage heuristic of FASTA against BLAST's seed-and-extend approach.

---

### 2. Search Execution Parameters Log

Record your parameter configurations at EMBL-EBI:
- **Server URL:** `[                                                                            ]`
- **Query Sequence Accession:** `[                                                             ]`
- **Target Database:** `[                                                                      ]`
- **Scoring Matrix & Gap Penalties:** `[                                                       ]`

---

### 3. Structured Observation Tables

#### Table 7.1: FASTA Search Results for Human HBB (`NP_000509.1`) against UniProtKB/Swiss-Prot
| Subject Protein (Accession & Description) | Alignment Length | % Identity | $init1$ Score | $initn$ Score | $opt$ Score | Expect Value ($E$) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| `P68871` (HBB_HUMAN, Hemoglobin beta) | 147 | 100.0% | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| `P02042` (HBD_HUMAN, Hemoglobin delta) | 147 | 95.2% | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| `P69891` (HBG1_HUMAN, Hemoglobin gamma-1) | 147 | 73.5% | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| `P69905` (HBA_HUMAN, Hemoglobin alpha) | 144 | 43.1% | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| `P02144` (MYG_HUMAN, Myoglobin) | 144 | 28.5% | `[__________]` | `[__________]` | `[__________]` | `[__________]` |

#### Table 7.2: Methodological Comparison (FASTA $ktup=2$ vs. $ktup=1$ vs. SSEARCH vs. BLASTP)
| Metric / Parameter | FASTA ($ktup=2$) | FASTA ($ktup=1$) | SSEARCH (Smith-Waterman) | NCBI BLASTP |
|---|---|---|---|---|
| Execution Speed (Relative) | Fast | Moderate | Slow (Exhaustive) | Very Fast |
| Myoglobin Identity (%) | 28.5% | 28.5% | 28.5% | 28.5% |
| Myoglobin $E$-value | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| Neuroglobin Detected? (Yes/No) | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| Algorithmic Basis | Hashing ($ktup=2$) + Diagonals + Band DP | Hashing ($ktup=1$) + Diagonals + Band DP | Exhaustive Dynamic Programming | Seeding ($W=3$) + Word Neighborhood + Extension |

---

### 4. FASTA Alignment Screenshot Box
*Paste a screenshot showing the FASTA pairwise alignment and score banner for human HBB aligned with Myoglobin:*

```
+-----------------------------------------------------------------------------------------+
|                                FASTA ALIGNMENT SCREENSHOT                               |
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

**Q1. The Four FASTA Scores:** Explain the specific biological and computational meaning of each of the four scores reported by the FASTA algorithm: $init1$, $initn$, $opt$, and $Z$-score / $E$-value. Why does $opt \ge initn \ge init1$?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. The $ktup$ Parameter:** What happens mathematically when $ktup$ is reduced from 2 to 1 in a protein FASTA search? Why does sensitivity for remote homologues increase, and what is the trade-off in computation time?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. Diagonal Joining with Gap Penalties:** In Stage 3 of the FASTA pipeline, how does the algorithm decide whether to join two high-scoring sub-alignments on different diagonals? What biological event does a shift from one diagonal to another represent?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. FASTA vs. BLAST Word Construction:** Contrast how FASTA identifies initial seed matches using $k$-tuples versus how BLAST identifies seeds using neighborhood words and threshold $T$. Which method is more mathematically dependent on the choice of substitution matrix during the initial seeding phase?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. Why SSEARCH is the Golden Benchmark:** Why do bioinformaticians use SSEARCH when evaluating the accuracy of newly developed heuristic alignment algorithms, rather than using BLAST or FASTA as the benchmark?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your analysis of the Gumbel Extreme Value Distribution and length normalization in FASTA:*
- **Explanation of Z-score Length Regression:**
  `[                                                                                             ]`
  `[                                                                                             ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Parameter Setup** | 2 | | Understanding of FASTA stages and EBI interface |
| **FASTA Execution & Table 7.1** | 4 | | Correct recording of init1, initn, opt, and E-values |
| **Comparative Analysis (Table 7.2)** | 2 | | Accurate comparison across ktup=2, ktup=1, SSEARCH, BLAST |
| **Discussion Questions & Critical Viva** | 2 | | Clear explanations of diagonal shifts, scores, and SSEARCH |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
