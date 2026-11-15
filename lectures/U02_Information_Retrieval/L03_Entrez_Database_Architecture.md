# Lecture 03 — Entrez Database Architecture

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 2:** Information Retrieval from Biological Databases  
**Syllabus Topic:** Integrated information Retrieval (Entrez System), Retrieving database entries  
**Primary Learning Outcome:** LO1, LO2 — Retrieve nucleotide, protein, structure, and literature records using targeted Entrez queries, and parse database linkages.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Beyond Flat File Silos
================================================================================
Topic: The Challenge of Biological Data Fragmentation

[Visual: Isolated database silos (GenBank, Swiss-Prot, PubMed, PDB)
         vs Unified interconnected web of Entrez]

Speaker Bullets:
* In the early 1990s, biological databases were isolated FTP silos; a researcher had
  to query literature on Medline, sequences on GenBank, and structures on Brookhaven.
* NCBI introduced the Entrez system to create an "integrated information retrieval"
  engine where biological records are cross-linked into a traversable graph.
* Today, Entrez indexes over 35 distinct databases spanning literature, genes,
  genomes, proteins, chemical compounds, and 3D structures.
```

```
================================================================================
SLIDE 2: The Core Philosophy of Entrez: The Dual-Graph Model
================================================================================
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

Speaker Bullets:
* Hard Links represent direct biological associations curated by authors or staff.
* Neighbors represent pre-computed computational similarities calculated nightly
  by NCBI algorithms (BLAST for sequences, vector-space TF-IDF for text).
```

```
================================================================================
SLIDE 3: Major Core Databases Connected in Entrez
================================================================================
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

Speaker Bullets:
* Notice the difference between `nuccore` (sequence-centric) and `gene` (locus-centric).
* One gene locus (*HBB*, Gene ID 3043) maps to multiple transcript variants,
  thousands of population submissions, and hundreds of mutant alleles.
```

```
================================================================================
SLIDE 4: The Evolution of Sequence Identifiers
================================================================================
Topic: Accession vs Version vs GI Number

  Historical (Pre-2016):
    Accession:      NM_000518
    GI Number:      4504348 (GenInfo Identifier — sequential integer)
    Version:        NM_000518.5

  Modern (Post-2016):
    Accession.Version:  NM_000518.5  [GI retired September 2016!]

Speaker Bullets:
* An Accession is a permanent, unique alphanumeric label assigned to a record.
* The Version suffix (`.1`, `.2`, `.5`) increments whenever the underlying sequence
  data or coordinates are updated.
* GI numbers were 32-bit/64-bit integer keys used internally; NCBI formally retired
  GI numbers because the sequence explosion exhausted integer spaces and distributed
  systems required globally unique accession.version tokens.
```

```
================================================================================
SLIDE 5: RefSeq Accession Prefix Nomenclature
================================================================================
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

Speaker Bullets:
* Rule of thumb: 'N' stands for Curated RefSeq; 'X' stands for Model (Predicted).
* 'M' = mRNA, 'P' = Protein, 'R' = RNA (non-coding), 'C' = Chromosome, 'G' = Genomic locus.
* For *HBB*: `NM_000518.5` translates to `NP_000509.1`.
```

```
================================================================================
SLIDE 6: Under the Hood: Inverted Indices and Postings Lists
================================================================================
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

Speaker Bullets:
* Entrez does not scan text files on the fly. It builds high-performance inverted
  indices (term dictionaries mapping words to lists of record UIDs).
* Boolean operations (`AND`, `OR`, `NOT`) are executed as set intersections,
  unions, and differences of sorted UID arrays.
```

```
================================================================================
SLIDE 7: Traversal Path: Walking the Entrez Web
================================================================================
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

Speaker Bullets:
* Starting from a clinical paper, a researcher traverses directly to genomic loci,
  transcripts, proteins, and the atomic coordinates of the mutant complex.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
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

---

## Detailed Comprehensive Technical Notes

### 1. Historical Context: From Disconnected Flat Files to Relational Networks

In the earliest days of computational molecular biology, primary data repositories operated as unlinked, monolithic flat files. If an investigator identified a point mutation in a patient with a hereditary hemoglobinopathy, determining its consequences required manual, disconnected steps:
1. Search bibliographic indices on MEDLINE for clinical reports.
2. Search GenBank flat files on magnetic tape or early FTP servers for the nucleic acid sequence.
3. Manually locate the protein entry in PIR (Protein Information Resource) or Swiss-Prot.
4. Download coordinates from the Brookhaven Protein Data Bank (PDB).

There was no computational mechanism to link a clinical phenotype to a genomic locus, its corresponding transcript, its translated polypeptide, and its 3D atomic structure.

In 1991, the National Center for Biotechnology Information (NCBI), directed by David Lipman and engineered by Jim Ostell, launched the **Entrez** system. Entrez was conceived not merely as a database search interface, but as an **integrated information retrieval system** that structures biological knowledge as a traversable, interconnected graph.

---

### 2. Core Architectural Design: Hard Links vs Computational Neighbors

The foundational design principle of Entrez is the distinction between two classes of relationships:

```
                                    +--------------------+
                                    |    Entrez Query    |
                                    +---------+----------+
                                              |
                                              v
                              +--------------------------------+
                              |      Target Record (UID)       |
                              +---------------+----------------+
                                              |
                     +------------------------+------------------------+
                     |                                                 |
                     v                                                 v
         +-----------------------+                         +-----------------------+
         |     "Hard Links"      |                         |     "Neighbors"       |
         |  (Inter-Database)     |                         |  (Intra-Database)     |
         +-----------+-----------+                         +-----------+-----------+
                     |                                                 |
         Biologically validated                             Statistically pre-computed
         explicit associations:                             probabilistic relationships:
         * Gene -> Nucleotide                               * Related PubMed Articles
         * Transcript -> Protein                            * Related Sequences (BLAST)
         * CDS -> 3D Structure                              * Structural Kinship (VAST+)
```

#### A. Entrez "Hard Links" (Cross-Database Connections)
Hard links represent deterministic biological relationships. They are maintained explicitly in relational mapping tables:
- **Gene $\to$ Nucleotide:** Connects the genomic locus (*HBB*, Gene ID: 3043) to all known mRNA transcripts (`NM_000518.5`) and genomic contigs (`NC_000011.10`).
- **Nucleotide $\to$ Protein:** Connects the coding sequence (CDS feature) directly to its translated polypeptide record (`NP_000509.1`).
- **Protein $\to$ Structure:** Connects the primary sequence to 3D atomic coordinates in the Molecular Modeling Database (MMDB / PDB `1A3N`).
- **Gene $\to$ OMIM:** Connects the locus to human Mendelian disease descriptions in Online Mendelian Inheritance in Man (OMIM `141900`).
- **Record $\to$ PubMed:** Connects any sequence or gene record to primary literature citations deposited by the author or PubMed Central (PMC).

#### B. Entrez "Neighbors" (Intra-Database Algorithmic Similarity)
Neighbors represent pre-computed computational kinship within the same database. Because computing pairwise similarity on the fly across millions of records would bring servers to a halt, Entrez runs offline batch calculations nightly:
1. **PubMed Neighbors ("Related Articles"):**  
   Computed using a probabilistic vector-space term-weighting model. Each article's title, abstract, and MeSH terms are parsed; common words are stripped; and informative words are weighted using a variant of the **TF-IDF** (Term Frequency-Inverse Document Frequency) algorithm. Articles sharing rare, highly informative keywords are linked with pre-computed similarity scores.
2. **Sequence Neighbors (Nucleotide & Protein):**  
   Computed by running all-against-all **BLAST** searches across public sequences. Records sharing alignments with significant bit scores and low expectation values ($E < 10^{-5}$) are registered as sequence neighbors.
3. **Structure Neighbors (VAST / VAST+):**  
   Computed using the **Vector Alignment Search Tool**, which aligns secondary structure elements (helices and sheets) in 3D space to identify structural homologs, even in the complete absence of primary sequence conservation.

---

### 3. The Entrez Identifier Ecosystem

Every entity across the Entrez universe is assigned a unique identifier to ensure unambiguous computational retrieval:

```
  Identifier Type        Example Syntax           Permanence & Scope
  ------------------------------------------------------------------------------------------------
  Unique Identifier (UID)3043 (Gene), 141900 (OMIM)Database-specific integer key
  Accession Number       NM_000518                Stable alphanumeric biological label
  Version Suffix         .5 (in NM_000518.5)      Integer tracking sequence updates
  Accession.Version      NM_000518.5              Globally unique immutable coordinate system
  GI Number (RETIRED)    4504348                  Obsolete sequential integer
```

#### Why NCBI Retired the GI Number in September 2016
For over two decades, NCBI assigned a **GenInfo Identifier (GI)**—a sequential integer (e.g., `GI: 4504348` for human *HBB*)—to every sequence deposited. Whenever a sequence was modified, a new GI number was issued. 

NCBI formally retired GI numbers on September 1, 2016, due to three critical engineering realities:
1. **Integer Space Depletion:** The explosion of high-throughput Next-Generation Sequencing threatened to exhaust the 32-bit signed integer address space ($2^{31}-1 \approx 2.14 \times 10^9$). Migrating to 64-bit integers imposed massive memory penalties across global indexing engines.
2. **Distributed Cloud Synchronization:** In modern distributed cloud databases, issuing centrally locked, sequential, monotonically increasing integers requires a single authoritative master node, creating a severe bottleneck during high-volume submissions.
3. **Redundancy and Confusion:** The global scientific community, publishers, and INSDC partners (EMBL-EBI and DDBJ) universally used `Accession.Version`. Maintaining two parallel identifier systems was redundant and confusing. Today, `Accession.Version` is the sole authoritative standard.

---

### 4. NCBI Reference Sequence (RefSeq) Architecture

Public repositories like GenBank are archival: any researcher can submit a sequence, resulting in massive redundancy (e.g., thousands of identical or partial *HBB* entries, sequencing artifacts, and clone vectors). 

To provide non-redundant, authoritative reference standards, NCBI created **RefSeq (Reference Sequence Database)**. RefSeq records are identified by distinct two-letter prefixes followed by an underscore:

$$\text{\textbf{[Prefix]\_[Six or Nine Digits].[Version]}}$$

```
  Prefix Type    Curated vs Automated  Molecule Type    Biological Example
  -------------------------------------------------------------------------------------------------
  NM_            Curated               mRNA             NM_000518.5 (Human HBB mRNA)
  NP_            Curated               Protein          NP_000509.1 (Human beta-globin protein)
  NR_            Curated               Non-coding RNA   NR_003286.4 (RNU6-1 small nuclear RNA)
  NC_            Curated               Genomic DNA      NC_000011.10 (Human Chromosome 11)
  NG_            Curated               Genomic Region   NG_000007.3 (Beta-globin gene cluster)
  XM_            Automated (Model)     mRNA             XM_011543210.1 (Predicted transcript)
  XP_            Automated (Model)     Protein          XP_011541512.1 (Predicted protein)
  XR_            Automated (Model)     Non-coding RNA   XR_001234567.1 (Predicted ncRNA)
  AP_, YP_       Curated               Viral/Organellar Direct organellar/prokaryotic translations
```

---

## Worked Example: Navigating the Entrez Graph for *HBB*

Let us trace a real-world computational traversal across Entrez, beginning from a genetic phenotype and arriving at atomic structural coordinates:

```
  Step 1: Clinical Phenotype
          Target: Sickle Cell Disease
          Database: OMIM (Online Mendelian Inheritance in Man)
          UID: 141900 ("HEMOGLOBIN--BETA LOCUS; HBB")
             |
             | [Hard Link: OMIM -> Gene]
             v
  Step 2: Gene Locus Definition
          Database: NCBI Gene
          Gene ID: 3043 ("HBB hemoglobin subunit beta [Homo sapiens]")
          Genomic Location: Chromosome 11p15.4; Coordinates: 5,225,464 to 5,227,071
             |
             | [Hard Link: Gene -> Nucleotide (RefSeq)]
             v
  Step 3: Curated Transcript Record
          Database: Nucleotide (nuccore)
          Accession.Version: NM_000518.5 (Length: 626 bp, CDS: 51..494)
             |
             | [Hard Link: CDS feature -> Protein]
             v
  Step 4: Translated Primary Structure
          Database: Protein
          Accession.Version: NP_000509.1 (Length: 147 aa)
          UniProt Cross-Reference: P68871
             |
             | [Hard Link: Protein -> Structure]
             v
  Step 5: Macromolecular 3D Structure
          Database: Structure (MMDB) / RCSB PDB
          PDB Accession: 1A3N ("Deoxy Human Normal Adult Hemoglobin A")
          Experimental Method: X-ray Diffraction; Resolution: 1.80 Angstroms
```

By querying Entrez via automated scripts (such as Python `biopython` or Entrez Direct), this complete 5-database traversal can be executed in a fraction of a second.

---

## Formative In-Class Checks

### Question 1
**Prompt:** Explain the architectural difference between an **Entrez Link** and an **Entrez Neighbor**. Give a concrete biological example of each starting from human *HBB* in NCBI Gene (`Gene ID: 3043`).

**Model Answer:**
- **Entrez Link (Hard Link):** Represents a biologically validated, deterministic association connecting records across two *different* databases. *Example for HBB:* In NCBI Gene (ID: 3043), following the `Gene -> Nucleotide` hard link takes the user directly to the curated RefSeq mRNA record `NM_000518.5`.
- **Entrez Neighbor:** Represents an algorithmically pre-computed statistical similarity connecting records within the *same* database. *Example for HBB:* In the NCBI Protein database, viewing neighbors for `NP_000509.1` reveals other vertebrate globin proteins (such as chimpanzee beta-globin or human delta-globin) that were identified by automated, offline all-against-all BLAST searches meeting statistical significance thresholds ($E < 10^{-5}$).

---

### Question 2
**Prompt:** A researcher needs the authoritative, manually reviewed mRNA sequence for human insulin. They find two accessions in NCBI: `NM_000207.3` and `XM_017017849.2`. Which record should they use for their experimental primer design, and why?

**Model Answer:**
The researcher should exclusively use **`NM_000207.3`**.
- The `NM_` prefix designates a **curated, high-confidence RefSeq transcript** that has been manually reviewed and validated by NCBI staff against published experimental literature and full-length cDNAs.
- The `XM_` prefix designates a **computationally modeled transcript** generated by automated genome annotation pipelines (GNOMON) based on statistical predictions and RNA-seq alignments. Automated models may contain false splice junctions, incorrect transcription start sites, or predictive artifacts, making them unsuitable when a curated `NM_` record is available.

---

### Question 3
**Prompt:** In older scientific papers published prior to 2016, researchers frequently cited numbers such as `GI: 4504348`. Why is this format no longer accepted in modern manuscripts, and what exact identifier must be used instead?

**Model Answer:**
NCBI formally decommissioned and retired the GenInfo Identifier (GI) numbering system in September 2016 because the rapid growth of high-throughput genomic data threatened to exhaust the 32-bit integer address space, and managing sequential integers across distributed database clusters created major synchronization bottlenecks. 

Modern manuscripts and computational pipelines must exclusively use the **`Accession.Version`** string (e.g., `NM_000518.5` for nucleotide or `NP_000509.1` for protein). This token uniquely identifies both the accession lineage and the exact, immutable sequence release.
