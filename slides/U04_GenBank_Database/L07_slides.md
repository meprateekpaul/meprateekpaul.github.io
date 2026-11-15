---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 07 Slides: Primary vs Secondary Databases"
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
# Lecture 07 — Primary vs Secondary Databases
### Concepts of Bioinformatics (CBBI-501)
**Unit 04:** GenBank Sequence Database  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Spectrum of Biological Databases

```text
Topic: Navigating Archival Records vs Curated Knowledge

[Visual: Funnel Diagram:
  Raw Data Flow: Sequencers -> Primary Repositories (GenBank / ENA / DDBJ)
                                     |
                                     v [Expert Curation & Filtering]
                               Secondary Databases (RefSeq / Swiss-Prot / Pfam)]
```

**Speaker Talking Points:**  
* Not all biological databases serve the same function.
* Primary databases act as permanent, archival patent offices of raw scientific claims.
* Secondary databases act as authoritative encyclopedias that filter noise, remove
  redundancy, and synthesize consensus biological knowledge.

---

## Slide 2: Primary (Archival) Databases: The INSDC Pillars

```text
Topic: Direct Submissions and Archival Invariance

+--------------------+--------------------+-----------------------------------+
| Repository         | Institution        | Geographical Node                 |
+--------------------+--------------------+-----------------------------------+
| GenBank            | NCBI / NLM         | Bethesda, Maryland, USA           |
| ENA (European      | EMBL-EBI           | Hinxton, Cambridge, UK            |
| Nucleotide Archive)|                    |                                   |
| DDBJ               | National Institute | Mishima, Shizuoka, Japan          |
|                    | of Genetics        |                                   |
+--------------------+--------------------+-----------------------------------+
```

**Speaker Talking Points:**  
* Primary repositories accept direct sequence submissions from experimentalists.
* Key rule: **NCBI staff will NOT alter or correct an author's sequence.**
* The record represents a historical legal record of what the author submitted on that date.

---

## Slide 3: The Pitfalls of Primary Archival Repositories

```text
Topic: Redundancy, Sequencing Errors, and Misannotation

  Major Vulnerabilities of Primary Repositories:
  1. High Redundancy: >40,000 distinct entries for human beta-globin (clones, ESTs).
  2. Sequencing Artifacts: Sanger dye blobs, NGS indels causing artificial frameshifts.
  3. Contamination: Vector DNA (pUC19, cloning linkers) submitted as human genomic DNA.
  4. Transitive Misannotation: An author mislabels an enzyme -> deposits in GenBank ->
     other researchers run BLAST -> copy the misannotation -> errors cascade globally!
```

**Speaker Talking Points:**  
* Never assume a sequence in GenBank is 100% correct simply because it is in the database!

---

## Slide 4: Secondary (Curated / Derived) Databases: RefSeq

```text
Topic: Non-Redundant, Gold-Standard Reference Sequences

[Visual: 10,000 Redundant GenBank submissions 
         Collapsed into -> ONE Authoritative RefSeq Entry (NM_000518.5)]
```

**Speaker Talking Points:**  
* NCBI created the **RefSeq** project in 2000 to resolve GenBank's redundancy crisis.
* RefSeq provides ONE authoritative, non-redundant reference standard per molecule.
* Unlike GenBank, RefSeq records can be updated, corrected, and merged by NCBI staff
  as new biological evidence emerges.

---

## Slide 5: RefSeq Curation Review Tiers

```text
Topic: Understanding Confidence Levels in RefSeq

+------------------+----------------------------------------------------------+
| Status Tag       | Biological Meaning & Curation Level                      |
+------------------+----------------------------------------------------------+
| `REVIEWED`       | Manually curated by NCBI staff; literature validated     |
| `VALIDATED`      | Screened computationally and verified against full cDNA  |
| `PROVISIONAL`    | Initial automated entry awaiting expert manual review    |
| `PREDICTED`      | Automated computational gene prediction (GNOMON pipeline)|
| `INFERRED`       | Sequence derived from physical mapping data              |
+------------------+----------------------------------------------------------+
```

**Speaker Talking Points:**  
* Always check the `COMMENT` section of a RefSeq record for the curation status tag.
* Human *HBB* (`NM_000518.5`) is a `REVIEWED` gold-standard record.

---

## Slide 6: UniProtKB: Swiss-Prot vs TrEMBL

```text
Topic: The World's Authoritative Protein Knowledgebase

                    +------------------------------------+
                    |             UniProtKB              |
                    +-----------------+------------------+
                                      |
         +----------------------------+----------------------------+
         |                                                         |
         v                                                         v
  UniProtKB/Swiss-Prot                                      UniProtKB/TrEMBL
  * Manually annotated by expert curators                   * Unreviewed automated translations
  * Verified against scientific literature                  * Direct computationally parsed CDS
  * Non-redundant (~570,000 curated proteins)               * Massive volume (>250,000,000 records)
  * Example: P68871 (HBB_HUMAN)                             * High speed, lower confidence
```

**Speaker Talking Points:**  
* Swiss-Prot represents the pinnacle of manual protein curation.
* TrEMBL captures newly sequenced genomes automatically until curators can review them.

---

## Slide 7: GenBank Historical Taxonomic Divisions

```text
Topic: 3-Letter File Categorization Codes

+-------------+-----------------------+-------------+-------------------------+
| Division    | Organismal Clade      | Division    | High-Throughput Class   |
+-------------+-----------------------+-------------+-------------------------+
| `PRI`       | Primate (Human HBB)   | `EST`       | Expressed Sequence Tags |
| `ROD`       | Rodent (Mouse, Rat)   | `GSS`       | Genome Survey Sequences |
| `MAM`       | Other Mammals         | `HTG`       | High-Throughput Genomic |
| `VRT`       | Other Vertebrates     | `WGS`       | Whole Genome Shotgun    |
| `BCT`       | Bacteria              | `SYN`       | Synthetic / Cloning     |
| `PLN`       | Plants and Fungi      | `PAT`       | Patent Sequences        |
+-------------+-----------------------+-------------+-------------------------+
```

**Speaker Talking Points:**  
* GenBank historically partitioned flat files into 3-letter codes for FTP distribution.
* Found on the `LOCUS` line of every flat file.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 07

* Primary repositories (GenBank, ENA, DDBJ) are archival, redundant, and submitter-owned.
* Secondary databases (RefSeq, Swiss-Prot) are curated, non-redundant, and authoritative.
* For routine experiments and primer design, always select curated secondary records.
* Next Lecture: Dissecting the GenBank Flat File line by line — LOCUS, FEATURES,
  and Location syntax.
```

