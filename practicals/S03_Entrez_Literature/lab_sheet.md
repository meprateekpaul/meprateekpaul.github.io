# Practical 03: Using Entrez to Search Biomedical Literature Databases (PubMed & MeSH)

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S03 (Syllabus Practical P3)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO2 — Retrieve biomedical literature, formulate precision field-tagged queries, apply MeSH controlled vocabularies, and construct historical query pipelines.

---

## 1. Aim & Objectives

### Aim
To master precision information retrieval in biomedical literature databases using the NCBI Entrez search engine, structured Boolean logic, field qualification tags, Medical Subject Headings (MeSH), and advanced query history management in PubMed.

### Objectives
1. Understand the indexing architecture of MEDLINE and PubMed within the Entrez retrieval system.
2. Formulate Boolean search strategies (`AND`, `OR`, `NOT`) and understand the operational rules of precedence and capitalization.
3. Apply field tags (`[AU]`, `[TITL]`, `[JOUR]`, `[PDAT]`, `[MESH]`) to constrain search spaces and eliminate irrelevant noise.
4. Utilize the MeSH (Medical Subject Headings) database to navigate hierarchical controlled vocabularies, identify Major Topics (`[MAJR]`), and apply targeted subheadings.
5. Track and refine multi-stage search workflows using PubMed **Advanced Search** and the **Search History** statement builder (`#1 AND #2`).
6. Retrieve seminal landmark papers in molecular medicine: Linus Pauling’s 1949 sickle cell paper, Max Perutz’s 1968 hemoglobin structure paper, and contemporary CRISPR gene-editing therapies (Casgevy).

---

## 2. Background & Scientific Principle

### Literature Informatics and the MEDLINE/PubMed Nexus
Scientific discoveries in bioinformatics are inextricably linked to peer-reviewed literature. PubMed comprises more than 36 million citations from MEDLINE, life science journals, and online books.
- **MEDLINE:** The National Library of Medicine’s premier bibliographic database. What distinguishes MEDLINE from raw web search engines (like Google Scholar) is **human expert indexing**: trained medical indexers inspect full-text articles and assign standardized descriptor terms from the **MeSH** vocabulary.
- **PMID (PubMed Identifier):** A unique, persistent integer assigned to each citation upon indexing (e.g., Linus Pauling’s landmark 1949 paper has PMID `15395398`).

### Boolean Operators and Search Logic
Entrez interprets search strings as formal algebraic sets:
- `AND` (Intersection): Both terms must be present. Restricts the search space.
- `OR` (Union): Either term (or both) may be present. Expands the search space; used for synonyms, variant spellings, and related acronyms.
- `NOT` (Difference / Exclusion): Excludes records containing the specified term. Must be used with extreme caution to prevent unintentional exclusion of relevant multi-topic literature.
- **Syntax Rule:** Boolean operators in Entrez **must be written in uppercase** (`AND`, `OR`, `NOT`). Lowercase words are treated as plain text stopwords.
- **Evaluation Order:** Entrez processes queries strictly left-to-right. Parentheses `(...)` must be used to group terms and force precedence:
  ```
  ("sickle cell"[TITL] OR drepanocytosis[TITL]) AND (therapy[TITL] OR treatment[TITL])
  ```

### Field Qualification Tags
By default, PubMed executes "Automatic Term Mapping" (ATM), searching across all fields. Precision retrieval requires restricting terms to specific database fields using bracketed abbreviations:
- `[AU]` or `[AUTH]` : Author name (Format: `LastName Initials`, e.g., `Pauling L[AU]`).
- `[TITL]` or `[TI]` : Title field only.
- `[TIAB]` : Title and Abstract fields.
- `[JOUR]` or `[TA]` : Journal title or ISO abbreviation (e.g., `Science[JOUR]`, `Nature[JOUR]`).
- `[PDAT]` or `[DP]` : Date of publication (Format: `YYYY`, `YYYY/MM`, or range `1949:1960[PDAT]`).
- `[MESH]` or `[MH]` : Medical Subject Headings descriptor term.
- `[MAJR]` : MeSH Major Topic (indicates the primary focus of the paper).

### Medical Subject Headings (MeSH)
Natural language suffers from synonymy (different words meaning the same concept: *sickle cell disease*, *drepanocytosis*, *HbS disease*, *sickle cell anemia*) and polysemy (one word having multiple meanings). MeSH organizes biomedical terminology into an 11-level hierarchical tree. When a query uses a MeSH descriptor, Entrez automatically "explodes" the term, searching for that concept and all its narrower child terms in the hierarchy.

---

## 3. Required Software, Tools, and Datasets

### Web Portals & URLs
- PubMed Home: [https://pubmed.ncbi.nlm.nih.gov/](https://pubmed.ncbi.nlm.nih.gov/)
- PubMed Advanced Search: [https://pubmed.ncbi.nlm.nih.gov/advanced/](https://pubmed.ncbi.nlm.nih.gov/advanced/)
- MeSH Database Browser: [https://www.ncbi.nlm.nih.gov/mesh/](https://www.ncbi.nlm.nih.gov/mesh/)

### Target Case Studies & Accessions
1. **Case 1: The First Molecular Disease**
   - Topic: Linus Pauling’s demonstration that sickle cell anemia is caused by an abnormal hemoglobin molecule.
   - Author: Pauling L
   - Year: 1949
   - Target PMID: `15395398`
2. **Case 2: 3D Structure of Hemoglobin**
   - Topic: Atomic resolution crystal structure of hemoglobin.
   - Author: Perutz MF
   - Target PMID: `5685605` (Nature, 1968)
3. **Case 3: Hydroxyurea in Sickle Cell Anemia**
   - Topic: Landmark clinical trials establishing fetal hemoglobin induction by hydroxyurea.
4. **Case 4: CRISPR Therapeutics for Hemoglobinopathies**
   - Topic: *BCL11A* enhancer editing (Casgevy / exagamglogene autotemcel) clinical trials.

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Basic vs. Precision Search (Field Tags)
1. Open [https://pubmed.ncbi.nlm.nih.gov/](https://pubmed.ncbi.nlm.nih.gov/).
2. In the search box, run an unconstrained naive query:
   ```
   sickle cell anemia
   ```
   Record the total number of hits returned (often >40,000).
3. Restrict the concept strictly to the article title using the `[TITL]` tag:
   ```
   "sickle cell anemia"[TITL]
   ```
   Observe and record how drastically the result set shrinks to highly specific articles.
4. Retrieve Linus Pauling's 1949 seminal paper by combining author, title, and journal tags:
   ```
   Pauling L[AU] AND "molecular disease"[TITL] AND Science[JOUR]
   ```
5. Click on the result. Record its exact title, publication date, volume/issue, and PMID.

### Phase 2: Exploring the MeSH Database
1. Navigate to the MeSH Browser: [https://www.ncbi.nlm.nih.gov/mesh/](https://www.ncbi.nlm.nih.gov/mesh/).
2. In the MeSH search bar, enter `sickle cell anemia` and click **Search**.
3. Select the entry **Anemia, Sickle Cell**.
4. Examine the record:
   - Read the standardized **Definition**.
   - Note the **Subheadings** available (e.g., `genetics`, `therapy`, `drug therapy`).
   - Scroll down to inspect the **MeSH Tree Structures**. Notice where it sits under *Hemic and Lymphatic Diseases* and *Genetic Diseases, Inborn*.
5. Select the subheading **genetics** by checking its box.
6. Check the box for **Restrict to MeSH Major Topic**.
7. Click the button on the right: **Add to search builder**, then click **Search PubMed**.
8. Record the exact formulated query string and the number of citations retrieved.

### Phase 3: Advanced Search and Query History Pipeline
1. In PubMed, click the **Advanced** link underneath the primary search box.
2. Scroll down to the **History and Search Details** section. Notice that every query you have run in this browser session is logged as `#1`, `#2`, etc.
3. Formulate the following multi-step literature pipeline using the query builder:
   - **Query A (Target Concept):** Build a search for *BCL11A* gene in title or abstract:
     `BCL11A[TIAB]`
   - **Query B (Technological Approach):** Build a search for CRISPR or Cas9:
     `(CRISPR[TIAB] OR "Cas9"[TIAB])`
   - **Query C (Clinical Disease Focus):** Build a search for Sickle Cell Disease:
     `"Anemia, Sickle Cell"[MESH]`
4. Combine the three statements using history statement identifiers in the query box:
   ```
   #A AND #B AND #C
   ```
   *(Replace with your actual history numbers, e.g., `#3 AND #4 AND #5`).*
5. Execute the combined query. Identify recent clinical trial reports (e.g., Frangoul et al., NEJM).

### Phase 4: Filtering and Citation Export
1. On the search results page, look at the left sidebar filter options:
   - Under **Article Type**, select **Clinical Trial**.
   - Under **Publication Date**, select **5 years**.
2. Note how the result set focuses specifically on translational medicine.
3. Click the **Save** button at the top of the results list.
4. Set Selection to **All results**, Format to **PMID**, and save the text file.

---

## 5. Offline Fallback Note

If the PubMed web service is down or network access is restricted:
- Use the curated reading list in `../../references/reading_list.md`.
- Inspect the citation metadata and abstract extracts provided in the instructor answer key to analyze Boolean logic and MeSH tree relationships offline.

---

## 6. Observations Table

### Table 3.1: Query Formulation, Specificity, and Entrez Metrics
| Step | Exact Query String Formulated | Field Tags & Boolean Operators Used | Number of Hits | Scientific Focus / Precision |
|---|---|---|:---:|---|
| 1 | `sickle cell anemia` | None (Automatic Term Mapping) | | Unfiltered; broad background |
| 2 | `"sickle cell anemia"[TITL]` | Title tag `[TITL]`, phrase quotes | | High precision; title focus |
| 3 | `Pauling L[AU] AND "molecular disease"[TITL]` | Author `[AU]`, Title `[TITL]`, `AND` | | Historical landmark discovery |
| 4 | `"Anemia, Sickle Cell/genetics"[MAJR]` | MeSH Major Topic with subheading | | Curated genetic etiology |
| 5 | `BCL11A[TIAB] AND (CRISPR[TIAB] OR Cas9[TIAB]) AND "Anemia, Sickle Cell"[MESH]` | Title/Abstract `[TIAB]`, MeSH, parentheses | | Gene editing clinical trials |

### Table 3.2: Landmark Citation Metadata Extraction
| Parameter | Linus Pauling Landmark (1949) | Max Perutz Hemoglobin Landmark (1968) |
|---|---|---|
| Complete Article Title | | |
| First & Senior Author | | |
| Journal & Year | | |
| Volume, Issue & Pages | | |
| PubMed Identifier (PMID) | | |
| Key Biological Conclusion | | |

---

## 7. Interpretation & Discussion Questions

1. **Precedence and Parentheses:** Consider the two queries:
   - Query 1: `sickle cell AND therapy OR cure`
   - Query 2: `sickle cell AND (therapy OR cure)`
   Explain why Query 1 will return thousands of irrelevant papers discussing cancer therapy or diabetes cures, and describe how Entrez interprets operator precedence.
2. **Automatic Term Mapping (ATM):** How does PubMed’s ATM interpret an untagged multi-word term such as *cold shock protein*? What translation tables (MeSH translation table, Journals translation table, Author index) does it consult?
3. **MeSH Subheadings:** Why is querying `"Anemia, Sickle Cell/drug therapy"[MESH]` far more biologically informative than searching `sickle cell AND drugs`?
4. **Limits of the `NOT` Operator:** Suppose an investigator wants to study non-sickle hemoglobinopathies and enters `hemoglobinopathy NOT "sickle cell"`. Why might this investigator inadvertently lose crucial papers that compare thalassemia directly against sickle cell disease? What alternative search strategy is safer?
5. **MeSH Explosion:** What is meant by "exploding" a MeSH term? If you query `"Globin"[MESH]`, will papers indexed under *Hemoglobins*, *Myoglobin*, and *Neuroglobin* be automatically included?

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Use PubMed Advanced Search to formulate a query that identifies all articles published by researchers affiliated with IIIT Delhi (`"Indraprastha Institute of Information Technology"[AD]`) in the year 2023 or 2024.
2. Combine this with the term `Bioinformatics[TIAB] OR "Computational Biology"[TIAB]`.
3. Record the total number of hits and extract the PMID of the two most recent publications.
