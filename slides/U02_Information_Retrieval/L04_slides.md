---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 04 Slides: Advanced Query Building and MeSH"
footer: "B.Tech. Bioinformatics (SHUATS-inspired) · Prateek Paul"
style: |
  section {
    font-family: 'Inter', sans-serif;
    font-size: 18px;
    padding: 30px;
    background: #0f172a;
    color: #f8fafc;
  }
  h1, h2, h3 {
    color: #38bdf8;
  }
  pre {
    background: #020617;
    color: #a5f3fc;
    border: 1px solid #1e293b;
    border-radius: 8px;
    padding: 12px;
    font-size: 13px;
  }
  footer, header {
    font-size: 11px;
    color: #64748b;
  }
---

<!-- _class: lead -->
# Lecture 04 — Advanced Query Building and MeSH
### Concepts of Bioinformatics (CBBI-501)
**Unit 02:** Information Retrieval from Biological Databases  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Precision vs Recall in Biological Information Retrieval

```text
Topic: Navigating the Ocean of Sequence and Literature Data

[Visual: Precision vs Recall Trade-off Curve
         Precision = TP / (TP + FP)   vs   Recall = TP / (TP + FN)]
```

**Speaker Talking Points:**  
* Naive keyword search fails in bioinformatics: searching "HBB" in PubMed returns
  over 25,000 papers, including irrelevant homonyms and acronyms.
* In biological databases, false positives (noise) waste researcher time, while false
  negatives (missed records) can derail clinical genetic diagnosis.
* Advanced Entrez query syntax enables surgical precision: retrieving exactly the
  relevant records by exploiting database field schemas and controlled vocabularies.

---

## Slide 2: Entrez Field Qualifiers (Search Tags)

```text
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
```

**Speaker Talking Points:**  
* Field tags are enclosed in square brackets immediately following search terms.
* Without field tags, Entrez performs Automatic Term Mapping (ATM) across all indices.

---

## Slide 3: Boolean Operators and Operator Precedence

```text
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
```

**Speaker Talking Points:**  
* Be careful with `NOT`: searching `HBB NOT mouse` will eliminate human papers
  that happen to say "we compared human HBB to mouse models in the discussion"!

---

## Slide 4: Why Query Counts Diverge Across Entrez Databases

```text
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
```

**Speaker Talking Points:**  
* First-year students often panic: "Why did my search give 1 hit in Gene but 40,000
  in Nucleotide?" Understand the data model behind the database you query!

---

## Slide 5: Medical Subject Headings (MeSH)

```text
Topic: The NLM Controlled Biomedical Vocabulary

[Visual: MeSH Tree Structure Hierarchy:
  Analytical, Diagnostic and Therapeutic Techniques and Equipment
    `-- Therapeutics
        `-- Biological Therapy
            `-- Gene Therapy
                `-- Genetic Vectors
                    `-- Lentivirus Vectors]
```

**Speaker Talking Points:**  
* Free-text search is plagued by synonyms: "cancer", "neoplasm", "tumor", "malignancy".
* Professional indexers at the National Library of Medicine (NLM) read each paper
  and assign 10-15 standardized MeSH terms.
* Searching a MeSH term captures all papers regardless of the author's choice of words.

---

## Slide 6: Automatic Explosion and Major Topic Tagging

```text
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
```

**Speaker Talking Points:**  
* Use `[MeSH]` for exhaustive recall; use `[MAJR]` for focused, high-precision searches.

---

## Slide 7: Query Translation and History Pipeline

```text
Topic: Inspecting Entrez Query Translation

User inputs: `sickle cell anemia HBB`
Entrez Translates to:
  ("anemia, sickle cell"[MeSH Terms] OR ("anemia"[All Fields] AND "sickle"[All Fields]
  AND "cell"[All Fields]) OR "sickle cell anemia"[All Fields]) AND ("hbb"[Gene Symbol]
  OR "hbb"[All Fields])
```

**Speaker Talking Points:**  
* Always check the "Search Details" box in PubMed/Entrez to see how the search engine
  rewrote your query.
* Combine historical queries using the `#` symbol: `#1 AND #2 NOT #3`.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 04

* Precision vs Recall governs biological retrieval strategy.
* Use field qualifiers (`[ORGN]`, `[GENE]`, `[ACCN]`, `[PROP]`) to avoid false positives.
* Operators must be uppercase (`AND`, `OR`, `NOT`); evaluation is strictly left-to-right.
* MeSH trees provide controlled vocabulary with automatic child-term explosion.
* Next Unit: The NCBI Data Model — ASN.1 specifications, Bioseq, and Seq-feat.
```

