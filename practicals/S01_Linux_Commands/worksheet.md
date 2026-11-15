# Practical Worksheet 01: Understanding Linux Operating System and Shell Commands

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S01 (Syllabus Practical P1)  
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
- [ ] Logged into Linux workstation / terminal environment.
- [ ] Navigated filesystem tree and identified working directory (`pwd`, `cd`, `ls`).
- [ ] Created working directory `~/CBBI_Lab/S01_Linux`.
- [ ] Copied reference sequence datasets from `data/sequences/`.
- [ ] Inspected FASTA sequence records using `head`, `tail`, `cat`, and `less`.
- [ ] Quantified lines, words, and characters using `wc`.
- [ ] Extracted FASTA definition headers and filtered lines using `grep`.
- [ ] Built multi-command text processing pipelines using `|`, `>`, and `>>`.

---

### 2. Command Execution Log & Output Records

Record the exact command invocations executed during the session:

1. **Working Directory Verification:**
   ```bash
   $ pwd
   [                                                                            ]
   ```

2. **Directory Creation & Path Transition:**
   ```bash
   $ mkdir -p ~/CBBI_Lab/S01_Linux && cd ~/CBBI_Lab/S01_Linux
   $ pwd
   [                                                                            ]
   ```

3. **File Copy Operation:**
   ```bash
   $ cp <SOURCE_PATH>/hbb_human_mrna.fasta .
   $ ls -la
   [                                                                            ]
   ```

---

### 3. Structured Observation Tables

#### Table 1.1: File Navigation and Basic Metrics
| Command Executed | Target File | Output / Value Observed | Biological / Operational Meaning |
|---|---|---|---|
| `pwd` | N/A | `[________________________________]` | Current working path |
| `ls -lh hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | `[________________________________]` | File permissions, size, modification date |
| `wc -l hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | `[________________________________]` | Total physical text lines |
| `wc -c hbb_human_mrna.fasta` | `hbb_human_mrna.fasta` | `[________________________________]` | File size in bytes / characters |
| `grep -c "^>" globin_family_proteins.fasta` | `globin_family_proteins.fasta` | `[________________________________]` | Number of distinct FASTA sequence records |
| `grep -c "^>" hbb_vertebrate_orthologues.fasta` | `hbb_vertebrate_orthologues.fasta` | `[________________________________]` | Number of vertebrate orthologue sequences |

#### Table 1.2: Header Identification from Multi-FASTA Files
| File | Total Records Found | Extracted Header Lines (First 3 Records) |
|---|---|---|
| `globin_family_proteins.fasta` | `[_____]` | 1. `[____________________________________________________]`<br>2. `[____________________________________________________]`<br>3. `[____________________________________________________]` |
| `hbb_vertebrate_orthologues.fasta` | `[_____]` | 1. `[____________________________________________________]`<br>2. `[____________________________________________________]`<br>3. `[____________________________________________________]` |

---

### 4. Terminal Output / Execution Verification Box
*Paste your verified terminal transcript below (showing execution of `grep -c "^>"` and the pipe pipeline to count net amino acid residues):*

```
+-----------------------------------------------------------------------------------------+
|                                TERMINAL TRANSCRIPT                                      |
+-----------------------------------------------------------------------------------------+
| $                                                                                       |
|                                                                                         |
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

**Q1. Header Identification Syntax:** Why is it computationally essential to search for `"^>"` rather than simply `">"` when counting or parsing FASTA files with `grep`? What error could occur if a sequence annotation line contains `>`?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Line Count vs. Sequence Length:** Why does running `wc -l hbb_human_mrna.fasta` give 11 lines, whereas the actual mRNA transcript length is 626 nucleotides? Explain the difference between physical newline characters and biological coordinates.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. Pipes vs. Intermediate Files:** Contrast using a Unix pipe (`grep -v "^>" file.fasta | tr -d '\n' | wc -m`) versus creating temporary intermediate text files on disk. Why is piping superior for gigabyte-scale NGS data?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Redirection Safeguards:** What is the critical operational danger of confusing `>` with `>>` when logging analytical output from a long-running computational experiment?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. Character Counting:** Why does running `wc -m` directly on `hbb_human_mrna.fasta` report 699 characters when the official NCBI RefSeq record length is exactly 626 nucleotides? What do the extra characters represent?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your one-line script and the resulting output table:*
- **Command:** `[                                                                               ]`
- **Output:**
```
[                                                                                         ]
[                                                                                         ]
[                                                                                         ]
```

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Navigation** | 2 | | Understanding of path syntaxes and filesystem hierarchy |
| **Practical Conduct & Command Execution** | 4 | | Proper execution of file handling, grep, and pipes |
| **Observation Tables & Accuracy** | 2 | | Correct metrics and records recorded |
| **Discussion Questions & Critical Viva** | 2 | | Accurate answers to concept questions |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
