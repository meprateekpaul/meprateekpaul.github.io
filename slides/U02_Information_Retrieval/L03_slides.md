---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 03 Slides: Entrez Database Architecture"
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
# Lecture 03 — Entrez Database Architecture
### Concepts of Bioinformatics (CBBI-501)
**Unit 02:** Information Retrieval from Biological Databases  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Beyond Flat File Silos

```text
Topic: The Challenge of Biological Data Fragmentation

[Visual: Isolated database silos (GenBank, Swiss-Prot, PubMed, PDB)
         vs Unified interconnected web of Entrez]
```

**Speaker Talking Points:**  
* In the early 1990s, biological databases were isolated FTP silos; a researcher had
  to query literature on Medline, sequences on GenBank, and structures on Brookhaven.
* NCBI introduced the Entrez system to create an "integrated information retrieval"
  engine where biological records are cross-linked into a traversable graph.
* Today, Entrez indexes over 35 distinct databases spanning literature, genes,
  genomes, proteins, chemical compounds, and 3D structures.

---

## Slide 2: The Core Philosophy of Entrez: The Dual-Graph Model

```text
Topic: Links vs Neighbors

                  +--------------------------------+
                  |         Entrez Record          |
                  |     (e.g., HBB Gene 3043)      |
                  +---------------+----------------+
                                  |
         +------------------------+------------------------+
         |                                                 |
         v                                                 v
  "Hard Links" (Links)                             "Neighbors" (Similarity)
  Cross-database biological bridges                Intra-database computational kinship
  * Gene -> Nucleotide (NM_000518.5)              * PubMed Related Articles (TF-IDF)
  * Gene -> Protein (NP_000509.1)                  * BLAST-based sequence neighbors
  * Gene -> OMIM (141900: Sickle Cell)             * VAST-based 3D structural neighbors
  * Gene -> PubMed (Cited primary literature)
```

**Speaker Talking Points:**  
* Hard Links represent direct biological associations curated by authors or staff.
* Neighbors represent pre-computed computational similarities calculated nightly
  by NCBI algorithms (BLAST for sequences, vector-space TF-IDF for text).

---

## Slide 3: Major Core Databases Connected in Entrez

```text
Topic: The Primary Entrez Verticals

+--------------------+--------------------+-----------------------------------+
| Database Name      | Entrez Key         | Primary Content                   |
+--------------------+--------------------+-----------------------------------+
| PubMed             | `pubmed`           | Biomedical bibliographic citations|
| Nucleotide         | `nuccore`          | GenBank, RefSeq, EMBL, DDBJ DNA/RNA|
| Protein            | `protein`          | Translated GenPept, RefSeq, SwissProt|
| Gene               | `gene`             | Gene-centric loci and nomenclature|
| Structure (MMDB)   | `structure`        | Macromolecular 3D models from PDB |
| Taxonomy           | `taxonomy`         | Hierarchical organismal tree      |
| OMIM               | `omim`             | Mendelian human genetic disorders |
| ClinVar            | `clinvar`          | Genomic variations and human health|
+--------------------+--------------------+-----------------------------------+
```

**Speaker Talking Points:**  
* Notice the difference between `nuccore` (sequence-centric) and `gene` (locus-centric).
* One gene locus (*HBB*, Gene ID 3043) maps to multiple transcript variants,
  thousands of population submissions, and hundreds of mutant alleles.

---

## Slide 4: The Evolution of Sequence Identifiers

```text
Topic: Accession vs Version vs GI Number

  Historical (Pre-2016):
    Accession:      NM_000518
    GI Number:      4504348 (GenInfo Identifier — sequential integer)
    Version:        NM_000518.5

  Modern (Post-2016):
    Accession.Version:  NM_000518.5  [GI retired September 2016!]
```

**Speaker Talking Points:**  
* An Accession is a permanent, unique alphanumeric label assigned to a record.
* The Version suffix (`.1`, `.2`, `.5`) increments whenever the underlying sequence
  data or coordinates are updated.
* GI numbers were 32-bit/64-bit integer keys used internally; NCBI formally retired
  GI numbers because the sequence explosion exhausted integer spaces and distributed
  systems required globally unique accession.version tokens.

---

## Slide 5: RefSeq Accession Prefix Nomenclature

```text
Topic: Decoding NCBI Curated Accession Types

+------------------+------------------+---------------------------------------+
| Prefix Format    | Molecule Type    | Status / Methodology                  |
+------------------+------------------+---------------------------------------+
| `NM_123456`      | mRNA             | Curated, manual/computational review  |
| `NP_123456`      | Protein          | Curated translation from NM_ record   |
| `NR_123456`      | Non-coding RNA   | Curated microRNA, lncRNA, rRNA        |
| `NC_123456`      | Genomic DNA      | Complete chromosome or mitochondrial  |
| `NG_123456`      | Genomic DNA      | Incomplete genomic region (gene locus)|
| `XM_123456`      | mRNA             | Model / automated GNOMON prediction   |
| `XP_123456`      | Protein          | Model / predicted protein translation |
+------------------+------------------+---------------------------------------+
```

**Speaker Talking Points:**  
* Rule of thumb: 'N' stands for Curated RefSeq; 'X' stands for Model (Predicted).
* 'M' = mRNA, 'P' = Protein, 'R' = RNA (non-coding), 'C' = Chromosome, 'G' = Genomic locus.
* For *HBB*: `NM_000518.5` translates to `NP_000509.1`.

---

## Slide 6: Under the Hood: Inverted Indices and Postings Lists

```text
Topic: How Entrez Returns Queries in Milliseconds

  Query Term: "HBB"
  Inverted Term Dictionary:
    Term          Document Frequency     Postings List (Record UIDs)
    -----------------------------------------------------------------
    "HBB"         4                      [ 3043, 4504348, 141900, 7040 ]
    "Homo"        10,000,000             [ 1, 2, 3, ..., 3043, ... ]
    "Hemoglobin"  15,400                 [ 3043, 3044, 3045, 141900, ... ]

  Boolean AND Evaluation:
    Intersection of Postings Lists: [3043, 4504348, 141900] INTERSECT [3043, ...]
    Result: Instantaneous retrieval without scanning gigabytes of flat text!
```

**Speaker Talking Points:**  
* Entrez does not scan text files on the fly. It builds high-performance inverted
  indices (term dictionaries mapping words to lists of record UIDs).
* Boolean operations (`AND`, `OR`, `NOT`) are executed as set intersections,
  unions, and differences of sorted UID arrays.

---

## Slide 7: Traversal Path: Walking the Entrez Web

```text
Topic: Following the Molecular Trail of Sickle Cell Anemia

[Visual: Directed graph traversal:
  PubMed (Ingram 1957 paper)
     |
     v
  OMIM (141900: Hemoglobin - Beta Locus; Sickle Cell Disease)
     |
     v
  Gene (Gene ID 3043: HBB Homo sapiens)
     +-----------------------+
     |                       |
     v                       v
  Nucleotide (NM_000518.5) Protein (NP_000509.1)
     |                       |
     \___________+___________/
                 |
                 v
  Structure (MMDB / PDB 1A3N: Deoxyhemoglobin)]
```

**Speaker Talking Points:**  
* Starting from a clinical paper, a researcher traverses directly to genomic loci,
  transcripts, proteins, and the atomic coordinates of the mutant complex.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 03

* Entrez is a unified network connecting >35 NCBI biological databases.
* Hard links represent biologically curated inter-database connections; neighbors
  represent pre-computed intra-database statistical/computational similarity.
* RefSeq prefixes (`NM_`, `NP_`, `NC_`, `XM_`, `XP_`) immediately convey curation
  level and molecule type.
* Accession.Version is the sole surviving unique identifier; GI numbers are historical.
* Next Lecture: Mastering advanced query syntax, field tags, Boolean operators,
  and Medical Subject Headings (MeSH).
```

