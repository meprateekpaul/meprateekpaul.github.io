# Practical Worksheet 03: Literature Information Retrieval using Entrez & PubMed

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S03 (Syllabus Practical P3)  
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
- [ ] Navigated to PubMed portal (`pubmed.ncbi.nlm.nih.gov`).
- [ ] Executed unconstrained naive queries vs. field-qualified searches (`[TITL]`, `[AU]`, `[JOUR]`).
- [ ] Retrieved Linus Pauling’s 1949 landmark molecular disease citation.
- [ ] Navigated the MeSH hierarchy, selected subheadings, and generated MeSH Major Topic queries.
- [ ] Constructed a multi-stage search strategy using PubMed Advanced Search History (`#1 AND #2`).
- [ ] Applied publication date and clinical trial publication type filters.
- [ ] Exported structured PMID citation lists.

---

### 2. Search Statement Formulation Log

Record the exact search strings used for each required task:

1. **Unconstrained Naive Search:**
   `[                                                                            ]`
2. **Title-Restricted Search:**
   `[                                                                            ]`
3. **Historical Landmark Query (Pauling 1949):**
   `[                                                                            ]`
4. **MeSH Major Topic Query with Subheading:**
   `[                                                                            ]`
5. **Combined Advanced Multi-Stage Query:**
   `[                                                                            ]`

---

### 3. Structured Observation Tables

#### Table 3.1: Query Formulation, Specificity, and Entrez Metrics
| Step | Exact Query String Formulated | Field Tags & Boolean Operators Used | Number of Hits | Scientific Focus / Precision |
|---|---|---|:---:|---|
| 1 | `sickle cell anemia` | None (Automatic Term Mapping) | `[__________]` | Broad background search |
| 2 | `"sickle cell anemia"[TITL]` | `[TITL]`, quotes | `[__________]` | Title-specific articles |
| 3 | `Pauling L[AU] AND "molecular disease"[TITL]` | `[AU]`, `[TITL]`, `AND` | `[__________]` | Landmark discovery |
| 4 | `"Anemia, Sickle Cell/genetics"[MAJR]` | `[MAJR]`, subheading | `[__________]` | Genetics as major topic |
| 5 | `BCL11A[TIAB] AND (CRISPR[TIAB] OR Cas9[TIAB]) AND "Anemia, Sickle Cell"[MESH]` | `[TIAB]`, `[MESH]`, `AND`, `OR` | `[__________]` | Modern CRISPR trials |

#### Table 3.2: Landmark Citation Metadata Extraction
| Parameter | Linus Pauling Landmark (1949) | Max Perutz Hemoglobin Landmark (1968) |
|---|---|---|
| Complete Article Title | `[____________________________________________________]` | `[____________________________________________________]` |
| First & Senior Author | `[____________________________________________________]` | `[____________________________________________________]` |
| Journal & Year | `[____________________________________________________]` | `[____________________________________________________]` |
| Volume, Issue & Pages | `[____________________________________________________]` | `[____________________________________________________]` |
| PubMed Identifier (PMID) | `[____________________________________________________]` | `[____________________________________________________]` |
| Key Biological Conclusion | `[____________________________________________________]` | `[____________________________________________________]` |

---

### 4. Advanced Search History Screenshot Box
*Paste a screenshot showing your PubMed Advanced Search History table displaying at least 4 numbered steps (#1, #2, etc.):*

```
+-----------------------------------------------------------------------------------------+
|                                SCREENSHOT PLACEMENT                                     |
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

**Q1. Precedence and Parentheses:** Consider the two queries:
- Query 1: `sickle cell AND therapy OR cure`
- Query 2: `sickle cell AND (therapy OR cure)`
Explain why Query 1 returns thousands of irrelevant non-sickle cell papers, and describe how Entrez evaluates Boolean precedence.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Automatic Term Mapping (ATM):** How does PubMed’s ATM interpret an untagged multi-word term such as *cold shock protein*? What translation tables does it consult?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. MeSH Subheadings:** Why is querying `"Anemia, Sickle Cell/drug therapy"[MESH]` far more biologically informative than searching `sickle cell AND drugs`?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Limits of the `NOT` Operator:** Suppose an investigator wants to study non-sickle hemoglobinopathies and enters `hemoglobinopathy NOT "sickle cell"`. Why might this search inadvertently lose crucial papers? What alternative search strategy is safer?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. MeSH Explosion:** What is meant by "exploding" a MeSH term? If you query `"Globin"[MESH]`, will papers indexed under *Hemoglobins*, *Myoglobin*, and *Neuroglobin* be automatically included?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your search query and findings for IIIT Delhi publications in bioinformatics/computational biology:*
- **Query String:** `[                                                                          ]`
- **Total Hits:** `[__________]`
- **Top 2 PMIDs Retrieved:** 1. `[______________]` &nbsp;&nbsp;&nbsp;&nbsp; 2. `[______________]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Query Formulation** | 2 | | Proper understanding of Boolean syntax and field tags |
| **Practical Conduct & MeSH Navigation** | 4 | | Correct use of MeSH subheadings and Advanced History |
| **Observation Tables & Accuracy** | 2 | | Accurate citation metadata and hit count metrics |
| **Discussion Questions & Critical Viva** | 2 | | Sound scientific reasoning regarding ATM, MeSH, and precedence |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
