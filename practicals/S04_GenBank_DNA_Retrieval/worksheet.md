# Practical Worksheet 04: GenBank Sequence Retrieval and Biological Data Formats

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S04 (Syllabus Practical P4)  
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
- [ ] Retrieved RefSeq mRNA record `NM_000518.5` from NCBI Nucleotide.
- [ ] Inspected and dissected all fields of the GenBank flat file header.
- [ ] Parsed the Feature Table (gene, exon, CDS, UTRs, regulatory signals).
- [ ] Viewed the ASN.1 / XML structural data models.
- [ ] Executed format conversion to FASTA, EMBL, and GCG using `seqret` / Biopython.
- [ ] Analyzed the mathematical relationship between CDS coordinates and protein length.

---

### 2. File Conversion Execution Record

Record your format conversion commands and file size outputs:
- **Conversion Command (GB to FASTA):** `[                                                      ]`
- **Conversion Command (GB to EMBL):**  `[                                                      ]`
- **Generated File Verification (`ls -lh`):**
  ```
  [                                                                                      ]
  [                                                                                      ]
  [                                                                                      ]
  ```

---

### 3. Structured Observation Tables

#### Table 4.1: GenBank Flat File Structural Anatomy (`NM_000518.5`)
| Section / Token | Extracted Value / Coordinates | Biological / Informatics Significance |
|---|---|---|
| `LOCUS` | `[________________________________]` | Locus identifier, length, molecule type, date |
| `DEFINITION` | `[________________________________]` | Sequence descriptive title |
| `ACCESSION` vs `VERSION` | Accession: `[_________________]`<br>Version: `[_________________]` | Immutable base accession vs revision number |
| `SOURCE` / `ORGANISM` | `[________________________________]` | Source organism & full taxonomic lineage |
| `FEATURES` : `gene` | `[________________________________]` | Total gene span on transcript |
| `FEATURES` : `CDS` | `[________________________________]` | Coding sequence coordinates |
| `FEATURES` : `/codon_start` | `[________________________________]` | Offset frame for translation |
| `FEATURES` : `/protein_id` | `[________________________________]` | Corresponding RefSeq protein accession |
| 5' UTR Span | Coordinates: `[_________________]` | Leader non-coding sequence |
| 3' UTR Span | Coordinates: `[_________________]` | Trailer non-coding sequence |
| Poly-A Signal Sequence | Coordinates: `[_________________]`<br>Motif: `[_________________]` | Cleavage and polyadenylation signal |
| `ORIGIN` End Token | `[________________________________]` | Flat file termination delimiter |

#### Table 4.2: Comparison of Biological Sequence Formats
| Feature / Characteristic | GenBank (`.gb`) | FASTA (`.fasta`) | EMBL (`.embl`) | GCG (`.gcg`) |
|---|---|---|---|---|
| Header Identifier Token | `LOCUS` | `>` | `ID` | Line with `..` |
| Feature Table Support (Yes/No) | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| Literature Citations Included (Yes/No) | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| Output File Size for `NM_000518` | `[__________]` | `[__________]` | `[__________]` | `[__________]` |
| Primary Use Case | Full curation | Alignment/Search | European archiving | Legacy GCG suite |

---

### 4. Converted File Header Comparison Box
*Paste the first 10 lines of `hbb_converted.embl` below:*

```
+-----------------------------------------------------------------------------------------+
|                                EMBL FLAT FILE HEADER                                    |
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

**Q1. Coding Sequence Mathematics:** The CDS is annotated as `51..494`. Calculate the total length of the coding region in nucleotides. How many amino acids does this encode (accounting for the termination stop codon)? Does this match the 147 aa length of `NP_000509.1`? Show your calculation.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Accession vs. Version Numbering:** Suppose a sequencing update corrects a single base call in the 3' UTR of `NM_000518.5`. What happens to the accession number, and what happens to the version number? Why is this essential for reproducibility?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. The `/codon_start` Qualifier:** What does the qualifier `/codon_start=1` indicate? If a fragmented cDNA sequence has `/codon_start=3`, how must an automated translation algorithm adjust?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. GenBank vs. EMBL Flat File Syntax:** Contrast the syntax used by GenBank and EMBL to denote feature tables. How does GenBank indicate qualifiers versus EMBL's two-character column codes?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. Machine-Readable ASN.1:** Why is it computationally error-prone to parse GenBank flat files with regular expressions compared to parsing structured ASN.1 or XML schemas?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Paste your Python script and the extracted exon coordinates:*
- **Script / Output:**
```
[                                                                                         ]
[                                                                                         ]
[                                                                                         ]
```

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Navigation** | 2 | | Understanding of GenBank flat file structure |
| **Format Conversion Execution** | 4 | | Successful generation of FASTA, EMBL, and GCG files |
| **Observation Tables & Accuracy** | 2 | | Accurate extraction of CDS, UTRs, and format comparison |
| **Discussion Questions & Critical Viva** | 2 | | Accurate calculations (CDS math) and conceptual explanations |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
