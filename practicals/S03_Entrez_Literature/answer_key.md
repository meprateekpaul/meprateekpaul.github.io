# Instructor Answer Key & Evaluation Manual: Practical 03 (Entrez Literature)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S03 (Syllabus Practical P3)  
**Curriculum Topic:** Using Entrez to Search Biomedical Literature Databases (PubMed & MeSH)  

---

## 1. Expected Outputs & Reference Solutions

### Table 3.1: Query Formulation, Specificity, and Entrez Metrics (Completed)
*(Note: Exact hit counts fluctuate slightly as new literature is indexed daily; orders of magnitude and relative ratios remain consistent).*

| Step | Exact Query String Formulated | Field Tags & Boolean Operators Used | Representative Hits | Scientific Focus / Precision |
|---|---|---|:---:|---|
| 1 | `sickle cell anemia` | None (Automatic Term Mapping) | ~42,000 – 46,000 | Broad search catching all papers mentioning any variant |
| 2 | `"sickle cell anemia"[TITL]` | `[TITL]`, quotes for exact phrase | ~14,000 – 16,000 | High specificity; restricted to papers where disease is in the title |
| 3 | `Pauling L[AU] AND "molecular disease"[TITL]` | `[AU]`, `[TITL]`, `AND` | 1 | Pinpoint precision: retrieves the exact 1949 seminal discovery |
| 4 | `"Anemia, Sickle Cell/genetics"[MAJR]` | `[MAJR]` (Major Topic), `/genetics` subheading | ~3,500 – 4,000 | Focuses strictly on articles whose primary biological theme is genetics |
| 5 | `BCL11A[TIAB] AND (CRISPR[TIAB] OR Cas9[TIAB]) AND "Anemia, Sickle Cell"[MESH]` | `[TIAB]`, `[MESH]`, nested `OR` within `AND` | ~150 – 250 | Highly focused on modern therapeutic genome editing |

### Table 3.2: Landmark Citation Metadata Extraction (Completed)
| Parameter | Linus Pauling Landmark (1949) | Max Perutz Hemoglobin Landmark (1968) |
|---|---|---|
| Complete Article Title | *Sickle Cell Anemia, a Molecular Disease* | *Structure of Haemoglobin: A Three-Dimensional Fourier Synthesis at 5.5-Å. Resolution, Obtained by X-Ray Analysis* |
| First & Senior Author | Pauling L, Itano HA, Singer SJ, Wells IC | Perutz MF, Muirhead H, Cox JM, Goaman LCG |
| Journal & Year | *Science*, 1949 | *Nature*, 1968 |
| Volume, Issue & Pages | Vol. 110, Issue 2865, pp. 543–548 | Vol. 219, Issue 5150, pp. 131–139 |
| PubMed Identifier (PMID) | `15395398` | `5685605` |
| Key Biological Conclusion | First proof that a human genetic disease originates from a specific physical abnormality in a protein molecule (differing electrophoretic mobility of sickle hemoglobin). | Elucidated the full three-dimensional atomic coordinates and stereochemistry of oxy- and deoxyhemoglobin, explaining cooperative oxygen binding. |

---

## 2. Sample Search History Pipeline Layout Guide

```
History and Search Details:
#5  Search: #1 AND #2 AND #3                                                    Hits: 184
#4  Search: "Anemia, Sickle Cell"[MESH]                                         Hits: 39,210
#3  Search: (CRISPR[TIAB] OR "Cas9"[TIAB])                                      Hits: 48,150
#2  Search: BCL11A[TIAB]                                                         Hits: 2,840
#1  Search: Pauling L[AU] AND "molecular disease"[TITL]                          Hits: 1
```

---

## 3. Model Answers to Discussion Questions

### Q1. Precedence and Parentheses
- **Model Answer:** Entrez evaluates Boolean expressions strictly **from left to right**. 
  - In `Query 1: sickle cell AND therapy OR cure`, the system first computes the set `(sickle cell AND therapy)`. It then takes the **union** (`OR`) of that entire set with the unconstrained word `cure`. Consequently, any paper in the entire MEDLINE database that contains the word "cure" (whether discussing HIV cure, oncological cures, hepatitis C cures, or dental care) is included in the output, generating tens of thousands of irrelevant hits.
  - In `Query 2: sickle cell AND (therapy OR cure)`, the parentheses force the union `(therapy OR cure)` to be evaluated first, and that concept is subsequently intersected with `sickle cell`, ensuring every returned record is relevant to sickle cell therapeutics.

### Q2. Automatic Term Mapping (ATM)
- **Model Answer:** When a user enters an unqualified multi-word query without field tags or quotes (e.g., *cold shock protein*), PubMed executes Automatic Term Mapping (ATM) by sequentially checking four internal translation tables:
  1. **MeSH Translation Table:** Maps the text to recognized MeSH descriptors, pharmacological substances, or tree terms (e.g., maps to `"Cold-Shock Response"` or specific cold shock domains).
  2. **Journals Translation Table:** Checks if the words correspond to full or abbreviated journal titles.
  3. **Author Catalog / Index:** Evaluates whether terms represent author names (e.g., `Protein CS`).
  4. **Full-text / Title-Abstract Fallback:** If no MeSH/Journal/Author match is found, searches the terms as individual text words across all fields separated by `AND`.

### Q3. MeSH Subheadings
- **Model Answer:** Querying with free-text keywords like `sickle cell AND drugs` retrieves any paper that merely mentions the word "drugs" anywhere in its abstract or text (e.g., patient adherence, illegal substance abuse among chronic pain patients, general pharmaceutical economics). By contrast, `"Anemia, Sickle Cell/drug therapy"[MESH]` leverages human professional medical indexing: the `/drug therapy` subheading is assigned *only* when the article specifically reports therapeutic administration, pharmacological mechanisms, dosage, or clinical efficacy of therapeutic agents (e.g., hydroxyurea, voxelotor, crizanlizumab) in treating sickle cell pathology.

### Q4. Limits of the `NOT` Operator
- **Model Answer:** The Boolean `NOT` is a blunt exclusion operator. If a researcher runs `hemoglobinopathy NOT "sickle cell"`, the engine removes every single citation containing the string "sickle cell" anywhere in its record. This creates severe scientific omissions:
  - High-impact review articles comparing beta-thalassemia and sickle cell disease are eliminated.
  - Clinical trial guidelines addressing multiple hemoglobin disorders simultaneously are discarded.
  - Studies examining compound heterozygosity (e.g., HbS/Beta-thalassemia) are eliminated.
  - **Safer Strategy:** Rather than excluding terms with `NOT`, the searcher should specify positive inclusions, such as `"Thalassemia"[MESH] OR "Hemoglobin C Disease"[MESH]`, or use field restriction tags (`[TITL]`).

### Q5. MeSH Explosion
- **Model Answer:** "Explosion" is an automatic Entrez feature where querying a higher-level MeSH descriptor automatically retrieves that heading plus **all narrower descriptor terms situated below it** in the hierarchical MeSH tree. Because *Hemoglobins*, *Myoglobin*, and *Neuroglobin* are child nodes located underneath the broader parent heading *Globins* in the chemical/protein hierarchy, querying `"Globins"[MESH]` automatically includes records indexed to all three specific proteins without requiring the user to type them individually.

---

## 4. Solution to Extension / Challenge Task

### Query Formulation
```
"Indraprastha Institute of Information Technology"[AD] AND (Bioinformatics[TIAB] OR "Computational Biology"[TIAB]) AND ("2023"[PDAT] : "2024"[PDAT])
```
*(Or using the institution's common abbreviation `IIIT Delhi[AD]`)*.

### Expected Output
- Generates 25 to 50 citations depending on exact affiliation string indexing.
- Returns recent papers published in high-impact computational biology journals (e.g., *Bioinformatics*, *Briefings in Bioinformatics*, *PLOS Computational Biology*, *Journal of Chemical Information and Modeling*).

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & Field Tag Formulation** | 2.0 | Deduct 0.5 if Boolean operators are in lowercase (e.g., `and`) or tags lack brackets. |
| **MeSH Query Execution** | 4.0 | Deduct 1.0 if student fails to demonstrate MeSH subheading or Advanced Search history logic. |
| **Observation Tables (Table 3.1 & 3.2)** | 2.0 | Deduct 0.5 for missing PMID or incorrect citation metadata. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question for clear, accurate, and comprehensive explanations. |
| **Total** | **10.0** | |
