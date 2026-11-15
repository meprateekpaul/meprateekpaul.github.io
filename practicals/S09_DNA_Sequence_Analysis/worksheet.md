# Practical Worksheet 09: DNA Sequence Feature Analysis (ORFs, EMBOSS, Codon Bias)

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S09 (Syllabus Practical P7)  
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
- [ ] Submitted *HBB* mRNA (`NM_000518.5`) to NCBI ORFfinder.
- [ ] Mapped the authentic coding sequence across 6 reading frames.
- [ ] Calculated GC percentage using EMBOSS `geecee`.
- [ ] Generated a codon usage table for *HBB* CDS using EMBOSS `cusp`.
- [ ] Identified overlapping reading frames in Bacteriophage $\Phi$X174.
- [ ] Evaluated repetitive elements and masking strategies via RepeatMasker.

---

### 2. Execution Log & Terminal Command History

Record the commands executed for EMBOSS analysis:
- **GC Content Command (`geecee`):** `[                                                         ]`
- **Codon Usage Command (`cusp`):**    `[                                                         ]`
- **Six-Frame Translation (`transeq`):** `[                                                    ]`

---

### 3. Structured Observation Tables

#### Table 9.1: ORFfinder Prediction Summary for Human *HBB* mRNA (`NM_000518.5`)
| ORF Rank | Reading Frame ($+1$ to $-3$) | Start Coordinate | Stop Coordinate | Length (nt) | Length (aa) | Matches Curated Protein? (Yes/No) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| **ORF 1 (Primary)** | `[_____]` | 51 | 494 | 444 | 147 | Yes (`NP_000509.1`) |
| **ORF 2** | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[__________]` |
| **ORF 3** | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[__________]` |
| **ORF 4** | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[_____]` | `[__________]` |

#### Table 9.2: EMBOSS `geecee` and `cusp` Codon Usage Profile for *HBB* CDS
| Amino Acid | Codon | Total Count in HBB | Frequency per 1000 | Fraction (Relative Synonymous Usage) |
|---|:---:|:---:|:---:|:---:|
| **Valine (Val)** | `GTG` | `[_____]` | `[__________]` | `[__________]` |
| | `GTC` | `[_____]` | `[__________]` | `[__________]` |
| | `GTT` | `[_____]` | `[__________]` | `[__________]` |
| | `GTA` | `[_____]` | `[__________]` | `[__________]` |
| **Glutamic Acid (Glu)** | `GAG` | `[_____]` | `[__________]` | `[__________]` |
| | `GAA` | `[_____]` | `[__________]` | `[__________]` |
| **Leucine (Leu)** | `CTG` | `[_____]` | `[__________]` | `[__________]` |
| | `CTC` | `[_____]` | `[__________]` | `[__________]` |
| Overall % GC (mRNA) | — | — | — | `[__________]%` |
| Overall % GC (CDS) | — | — | — | `[__________]%` |

---

### 4. ORFfinder Graphical Display Screenshot Box
*Paste a screenshot showing the NCBI ORFfinder six-frame graphical map for human HBB mRNA:*

```
+-----------------------------------------------------------------------------------------+
|                                ORFFINDER SCREENSHOT                                     |
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

**Q1. Biological Significance of 5' and 3' UTRs:** The authentic coding ORF spans `51..494` in a 626 bp mRNA. What are the biological functions of the 50 bp 5' UTR and the 132 bp 3' UTR?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Kozak Consensus Context:** What sequence motif surrounds the authentic initiation codon at base 51 (`accatgG`)? Explain the role of the eukaryotic Kozak consensus in translation.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. Translational Selection and Codon Bias:** Why does the highly expressed beta-globin gene favor `CTG` over `CTA` for leucine, and `GTG` over `GTA` for valine? How does this correlate with tRNA abundance?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Overlapping Reading Frames in Viruses:** In Bacteriophage $\Phi$X174, Gene B is translated within Gene A in a different frame. How does a single nucleotide mutation impact both viral proteins?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. RepeatMasker in NGS Pipelines:** Why is running RepeatMasker a mandatory first step before assembling eukaryotic genomes or running genome-wide BLAST searches?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your calculated Relative Synonymous Codon Usage (RSCU) values for Valine codons:*
- **GTG RSCU:** `[__________]` &nbsp;&nbsp;&nbsp;&nbsp; **GTC RSCU:** `[__________]`
- **GTT RSCU:** `[__________]` &nbsp;&nbsp;&nbsp;&nbsp; **GTA RSCU:** `[__________]`
- **Interpretation:** `[                                                                        ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & ORF Navigation** | 2 | | Understanding of 6 reading frames and start/stop rules |
| **EMBOSS Tool Execution & Metrics** | 4 | | Accurate GC percentage and codon usage counts |
| **Observation Tables & Accuracy** | 2 | | Complete recording of Table 9.1 and Table 9.2 |
| **Discussion Questions & Critical Viva** | 2 | | Rigorous understanding of UTRs, Kozak context, and codon bias |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
