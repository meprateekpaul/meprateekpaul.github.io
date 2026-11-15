# Lecture 04 — Advanced Query Building and MeSH

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 2:** Information Retrieval from Biological Databases  
**Syllabus Topic:** Integrated information Retrieval (Entrez System), Retrieving database entries  
**Primary Learning Outcome:** LO1, LO2 — Retrieve nucleotide, protein, structure, and literature records using targeted Entrez queries, and parse database linkages.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Precision vs Recall in Biological Information Retrieval
================================================================================
Topic: Navigating the Ocean of Sequence and Literature Data

[Visual: Precision vs Recall Trade-off Curve
         Precision = TP / (TP + FP)   vs   Recall = TP / (TP + FN)]

Speaker Bullets:
* Naive keyword search fails in bioinformatics: searching "HBB" in PubMed returns
  over 25,000 papers, including irrelevant homonyms and acronyms.
* In biological databases, false positives (noise) waste researcher time, while false
  negatives (missed records) can derail clinical genetic diagnosis.
* Advanced Entrez query syntax enables surgical precision: retrieving exactly the
  relevant records by exploiting database field schemas and controlled vocabularies.
```

```
================================================================================
SLIDE 2: Entrez Field Qualifiers (Search Tags)
================================================================================
Topic: Constraining Queries to Specific Database Columns

+--------------------+--------------------+-----------------------------------+
| Field Tag          | Name               | Target Data Content               |
+--------------------+--------------------+-----------------------------------+
| `[ORGN]`           | Organism           | NCBI Taxonomy scientific/common name|
| `[GENE]`           | Gene Symbol        | Official gene symbol (e.g. HBB)   |
| `[TITL]`           | Title              | Words in article/record title     |
| `[AUTH]`           | Author             | Author name (e.g. Ingram VM[AUTH])|
| `[PDAT]`           | Publication Date   | Date range (YYYY/MM/DD : YYYY)    |
| `[ACCN]`           | Accession          | Accession or accession.version    |
| `[PROP]`           | Property           | Molecule type, biomaterial, RefSeq|
| `[SLEN]`           | Sequence Length    | Sequence length range (min:max)   |
+--------------------+--------------------+-----------------------------------+

Speaker Bullets:
* Field tags are enclosed in square brackets immediately following search terms.
* Without field tags, Entrez performs Automatic Term Mapping (ATM) across all indices.
```

```
================================================================================
SLIDE 3: Boolean Operators and Operator Precedence
================================================================================
Topic: Set Logic in Entrez Queries

  Rules:
  1. Operators MUST be strictly UPPERCASE: `AND`, `OR`, `NOT`.
     (lowercase "and" is treated as a literal search term, not an operator!)
  2. Evaluation is strictly LEFT-TO-RIGHT:
     `A OR B AND C` is evaluated as `(A OR B) AND C`!
  3. Use explicit Parentheses `( ... )` to override default precedence:
     `A AND (B OR C)`

  Visual Set Venn Diagrams:
      A AND B: Intersection (Strict filtering)
      A OR B:  Union (Synonym expansion)
      A NOT B: Difference (Exclusion — use with extreme caution!)

Speaker Bullets:
* Be careful with `NOT`: searching `HBB NOT mouse` will eliminate human papers
  that happen to say "we compared human HBB to mouse models in the discussion"!
```

```
================================================================================
SLIDE 4: Why Query Counts Diverge Across Entrez Databases
================================================================================
Topic: Sequence-Centric vs Locus-Centric Architecture

Query: "Homo sapiens"[ORGN] AND HBB[GENE]

+--------------------+--------------------+-----------------------------------+
| Database Queried   | Result Count       | Architectural Reason              |
+--------------------+--------------------+-----------------------------------+
| NCBI Gene          | Exactly 1 Record   | Locus-centric: represents the single|
|                    | (Gene ID: 3043)    | HBB genomic locus on Chr 11p15.4  |
| Nucleotide (nuccore| >45,000 Records    | Sequence-centric: indexes every   |
|                    |                    | historical clone, EST, patent,    |
|                    |                    | mutant allele, and RefSeq version |
| Protein            | >12,000 Records    | Indexes all translations, mutants,|
|                    |                    | and synthetic constructs          |
+--------------------+--------------------+-----------------------------------+

Speaker Bullets:
* First-year students often panic: "Why did my search give 1 hit in Gene but 40,000
  in Nucleotide?" Understand the data model behind the database you query!
```

```
================================================================================
SLIDE 5: Medical Subject Headings (MeSH)
================================================================================
Topic: The NLM Controlled Biomedical Vocabulary

[Visual: MeSH Tree Structure Hierarchy:
  Analytical, Diagnostic and Therapeutic Techniques and Equipment
    `-- Therapeutics
        `-- Biological Therapy
            `-- Gene Therapy
                `-- Genetic Vectors
                    `-- Lentivirus Vectors]

Speaker Bullets:
* Free-text search is plagued by synonyms: "cancer", "neoplasm", "tumor", "malignancy".
* Professional indexers at the National Library of Medicine (NLM) read each paper
  and assign 10-15 standardized MeSH terms.
* Searching a MeSH term captures all papers regardless of the author's choice of words.
```

```
================================================================================
SLIDE 6: Automatic Explosion and Major Topic Tagging
================================================================================
Topic: MeSH Tree Traversal Mechanics

1. Automatic Explosion:
   * Querying a parent MeSH term automatically retrieves citations indexed with
     ALL child terms underneath it in the hierarchical tree.
   * Query: `Anemia, Hemolytic[MeSH]` automatically includes `Anemia, Sickle Cell`,
     `Thalassemia`, and `Spherocytosis, Hereditary`!

2. Major Topic Tagging (`[MAJR]`):
   * Restricts search to articles where the MeSH term represents the central,
     primary focus of the research (marked with an asterisk in PubMed).
   * Eliminates peripheral mentions in the literature.

Speaker Bullets:
* Use `[MeSH]` for exhaustive recall; use `[MAJR]` for focused, high-precision searches.
```

```
================================================================================
SLIDE 7: Query Translation and History Pipeline
================================================================================
Topic: Inspecting Entrez Query Translation

User inputs: `sickle cell anemia HBB`
Entrez Translates to:
  ("anemia, sickle cell"[MeSH Terms] OR ("anemia"[All Fields] AND "sickle"[All Fields]
  AND "cell"[All Fields]) OR "sickle cell anemia"[All Fields]) AND ("hbb"[Gene Symbol]
  OR "hbb"[All Fields])

Speaker Bullets:
* Always check the "Search Details" box in PubMed/Entrez to see how the search engine
  rewrote your query.
* Combine historical queries using the `#` symbol: `#1 AND #2 NOT #3`.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 04

* Precision vs Recall governs biological retrieval strategy.
* Use field qualifiers (`[ORGN]`, `[GENE]`, `[ACCN]`, `[PROP]`) to avoid false positives.
* Operators must be uppercase (`AND`, `OR`, `NOT`); evaluation is strictly left-to-right.
* MeSH trees provide controlled vocabulary with automatic child-term explosion.
* Next Unit: The NCBI Data Model — ASN.1 specifications, Bioseq, and Seq-feat.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Information Retrieval Problem in Bioinformatics

Biological repositories are expanding at terabyte-to-petabyte scales. However, raw storage is useless without rapid, deterministic retrieval. The fundamental trade-off in Information Retrieval (IR) is characterized by two orthogonal metrics:

$$\text{Precision} = \frac{\text{True Positives (Relevant Retrieved)}}{\text{Total Retrieved Records}} = \frac{TP}{TP + FP}$$

$$\text{Recall} = \frac{\text{True Positives (Relevant Retrieved)}}{\text{Total Relevant in Database}} = \frac{TP}{TP + FN}$$

In a naive search, a user might enter `beta globin` into NCBI Nucleotide:
- **Low Precision:** The query returns tens of thousands of records, including partial synthetic cloning vectors, sequencing artifacts, pseudogenes, unrelated globin family members (*HBD*, *HBG*, *HBE*), and papers where globin was merely a control.
- **Low Recall:** The query fails to return records titled "hemoglobin subunit beta" or "HBB" if the text does not contain the exact string "beta globin".

To achieve maximum precision without sacrificing recall, bioinformaticians employ **Field-Restricted Querying** and **Controlled Vocabularies**.

---

### 2. Entrez Field Qualifiers (Search Tags)

Entrez organizes each database into structured tables with indexed columns. Users target these columns using field tags enclosed in brackets:

```
  Field Tag      Full Name            Syntax / Example                Purpose
  ---------------------------------------------------------------------------------------------------
  [ORGN]         Organism             "Homo sapiens"[ORGN]            Filters by scientific name or tax ID
  [GENE]         Gene Symbol          HBB[GENE]                       Matches official HGNC/NCBI symbol
  [TITL]         Title Words          "sickle cell"[TITL]             Restricts words to title only
  [AUTH]         Author Name          Ingram VM[AUTH]                 Last name + Initials
  [PDAT]         Publication Date     2020:2024[PDAT]                 Filters records within date ranges
  [PROP]         Property             biomol_mrna[PROP]               Filters molecule types (mRNA, genomic)
  [SLEN]         Sequence Length      400:800[SLEN]                   Restricts nucleotide/aa length
  [ACCN]         Accession Number     NM_000518[ACCN]                 Matches specific accession prefix
  [UID]          Unique Identifier    3043[UID]                       Direct retrieval by primary key
  [MAJR]         MeSH Major Topic     "Anemia, Sickle Cell"[MAJR]     Limits to articles where topic is central
```

---

### 3. Boolean Operator Precedence and Logic Pitfalls

Entrez supports three Boolean operators: `AND`, `OR`, and `NOT`. However, failure to understand search engine mechanics leads to severe retrieval errors:

#### Rule 1: Case Sensitivity
Boolean operators **must be entered in uppercase letters**. If a user writes `human and hbb`, Entrez interprets the word "and" as a literal text word, stripping it as a stop-word or searching for records containing the string "and", corrupting the query.

#### Rule 2: Left-to-Right Processing
Entrez processes operations in strict sequential order from left to right, **ignoring traditional mathematical operator precedence** (where `AND` typically takes precedence over `OR`):

$$\text{Query: } A \text{ OR } B \text{ AND } C \implies (A \text{ OR } B) \text{ AND } C$$

#### The Parenthesis Catastrophe:
Consider a researcher attempting to find human records for either beta-globin or insulin:
- **Incorrect Query:** `"Homo sapiens"[ORGN] AND HBB[GENE] OR INS[GENE]`
- **Entrez Evaluation:** `("Homo sapiens"[ORGN] AND HBB[GENE]) OR INS[GENE]`
- **Disastrous Result:** The search returns all human *HBB* records, **PLUS every single insulin record from all organisms on earth** (rats, cows, zebrafish, bacteria)!
- **Correct Query:** `"Homo sapiens"[ORGN] AND (HBB[GENE] OR INS[GENE])`

#### The Peril of `NOT`:
The `NOT` operator executes a set difference ($A \setminus B$). If an investigator queries:
$$\text{Query: } \text{"Anemia, Sickle Cell"[MeSH] NOT "Mouse"[TITL]}$$
Any human clinical paper stating in its abstract, *"We compared our human clinical outcomes to previously published mouse model data,"* will be completely dropped from the search results.

---

### 4. Controlled Biomedical Vocabularies: Medical Subject Headings (MeSH)

Free-text natural language is ambiguous due to synonymy (different words meaning the same thing) and polysemy (the same word having multiple meanings). To standardize biomedical literature indexing, the National Library of Medicine maintains **MeSH (Medical Subject Headings)**.

#### The MeSH Poly-Hierarchy
MeSH is organized as a poly-hierarchical tree spanning 16 top-level categories (e.g., Category A: Anatomy, Category C: Diseases, Category D: Chemicals and Drugs). A single concept can reside under multiple parent branches:

```
  C15 - Hemic and Lymphatic Diseases
    `-- C15.378 - Hematologic Diseases
        `-- C15.378.100 - Anemia
            `-- C15.378.100.100 - Anemia, Hemolytic
                `-- C15.378.100.100.200 - Anemia, Sickle Cell
```

#### Automatic Tree Explosion
When a search is executed using a MeSH term with the `[MeSH]` qualifier, Entrez automatically performs **Tree Explosion**: it builds a Boolean `OR` cascade containing the specified term and **every single descendant term** below it in the tree hierarchy.

$$\text{Query: } \text{"Anemia, Hemolytic"[MeSH]}$$
Automatically evaluates to:
$$\text{"Anemia, Hemolytic"[MeSH]} \text{ OR } \text{"Anemia, Sickle Cell"[MeSH]} \text{ OR } \text{"Thalassemia"[MeSH]} \text{ OR } \dots$$

#### Subheadings / Qualifiers
MeSH terms can be qualified using standardized subheadings to isolate specific facets of a topic:
- `/genetics` (e.g., `Anemia, Sickle Cell/genetics[MeSH]`)
- `/therapy`
- `/pathology`
- `/drug therapy`

---

## Worked Example: Surgical Query Construction for *HBB* RefSeq mRNA

### Objective:
Retrieve exclusively the authentic, curated wild-type human Hemoglobin Subunit Beta (*HBB*) mature mRNA Reference Sequence record, while eliminating all pseudogenes, paralogous globins, uncurated EST clones, and genomic contigs.

### Iterative Query Refinement Table:

| Iteration | Query String | Hit Count (Approx) | Failure Analysis / Unwanted Records |
|---|---|---|---|
| **Attempt 1** | `HBB` | ~48,000 | Returns mouse, rat, clone vectors, papers, non-specific matches |
| **Attempt 2** | `HBB AND human` | ~18,000 | "human" captures free text mentions; contains patent sequences |
| **Attempt 3** | `HBB[GENE] AND "Homo sapiens"[ORGN]` | ~4,200 | Eliminates non-human species, but retains 4,000+ raw population submissions |
| **Attempt 4** | `HBB[GENE] AND "Homo sapiens"[ORGN] AND biomol_mrna[PROP]` | ~650 | Restricts to mRNA molecules, but still contains redundant cDNA clones |
| **Attempt 5** | `HBB[GENE] AND "Homo sapiens"[ORGN] AND biomol_mrna[PROP] AND refseq[FILTER]` | **1 Record** | **Success:** Returns exactly `NM_000518.5`! |

### Direct Command-Line Execution via Entrez Direct (`edirect`):

```bash
# Execute the refined Boolean query using esearch and fetch the summary
esearch -db nuccore -query 'HBB[GENE] AND "Homo sapiens"[ORGN] AND biomol_mrna[PROP] AND refseq[FILTER]' | \
  esummary | \
  xtract -pattern DocumentSummary -element Caption,Title,Length

# Output:
# NM_000518    Homo sapiens hemoglobin subunit beta (HBB), mRNA    626
```

---

## Formative In-Class Checks

### Question 1
**Prompt:** A student enters the following query into the NCBI Nucleotide database:  
`"Homo sapiens"[ORGN] AND (HBB[GENE] OR INS[GENE]) NOT biomol_genomic[PROP]`  
Explain in plain English what records this query will return, and state what the `NOT biomol_genomic[PROP]` clause achieves.

**Model Answer:**
- **What the query returns:** This query retrieves all nucleotide sequence records from modern humans (*Homo sapiens*) that represent either the beta-globin gene (*HBB*) or the insulin gene (*INS*).
- **Function of `NOT biomol_genomic[PROP]`:** It excludes all whole-chromosome assemblies, genomic contigs, BAC clones, and unparsed genomic DNA fragments, restricting the returned pool to expressed mature transcript sequences (mRNAs, cDNAs, or ESTs).

---

### Question 2
**Prompt:** Contrast the operational results in PubMed of searching:  
Query A: `"Anemia, Sickle Cell"[MeSH]`  
Query B: `"Anemia, Sickle Cell"[MAJR]`  
When would a clinical bioinformatics researcher choose Query B over Query A?

**Model Answer:**
- **Query A (`[MeSH]`):** Retrieves every article where the NLM human indexers assigned "Anemia, Sickle Cell" as a descriptive topic, including papers where sickle cell is mentioned peripherally as a secondary comparison or background review. It also automatically explodes to include narrower child concepts.
- **Query B (`[MAJR]`):** Restricts results strictly to articles where "Anemia, Sickle Cell" is indexed as a **Major Topic** (the core research focus of the manuscript).
- **When to choose Query B:** A researcher chooses Query B when conducting a targeted, high-precision systematic review where they want only primary studies focused specifically on sickle cell pathophysiology, filtering out thousands of peripheral papers where the disease is merely cited as an incidental example.

---

### Question 3
**Prompt:** Write a syntactically valid Entrez PubMed query to find all review articles focusing on the genetics of human *TP53* in lung cancer published between 2021 and 2024.

**Model Answer:**
```text
("TP53"[GENE] OR "Genes, p53"[MeSH]) AND "Lung Neoplasms"[MeSH:noexp] AND "Homo sapiens"[ORGN] AND Review[PTYP] AND 2021:2024[PDAT]
```
*(Explanation of syntax: `[GENE]` / `[MeSH]` isolates the locus; `Lung Neoplasms[MeSH]` captures pulmonary cancers; `Review[PTYP]` restricts to the publication type "Review"; `[PDAT]` enforces the 2021 to 2024 date boundary).*
