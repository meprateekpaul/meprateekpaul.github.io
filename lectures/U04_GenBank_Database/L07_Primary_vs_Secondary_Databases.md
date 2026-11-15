# Lecture 07 — Primary vs Secondary Databases

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 4:** GenBank Sequence Database  
**Syllabus Topic:** Introduction to structure, Primary and secondary database, Format vs Content: Computer vs. Human, Databases, Genbank Flat file, GCG  
**Primary Learning Outcome:** LO2 — Retrieve nucleotide, protein, structure, and literature records, and distinguish between primary archival and secondary curated databases.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Spectrum of Biological Databases
================================================================================
Topic: Navigating Archival Records vs Curated Knowledge

[Visual: Funnel Diagram:
  Raw Data Flow: Sequencers -> Primary Repositories (GenBank / ENA / DDBJ)
                                     |
                                     v [Expert Curation & Filtering]
                               Secondary Databases (RefSeq / Swiss-Prot / Pfam)]

Speaker Bullets:
* Not all biological databases serve the same function.
* Primary databases act as permanent, archival patent offices of raw scientific claims.
* Secondary databases act as authoritative encyclopedias that filter noise, remove
  redundancy, and synthesize consensus biological knowledge.
```

```
================================================================================
SLIDE 2: Primary (Archival) Databases: The INSDC Pillars
================================================================================
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

Speaker Bullets:
* Primary repositories accept direct sequence submissions from experimentalists.
* Key rule: **NCBI staff will NOT alter or correct an author's sequence.**
* The record represents a historical legal record of what the author submitted on that date.
```

```
================================================================================
SLIDE 3: The Pitfalls of Primary Archival Repositories
================================================================================
Topic: Redundancy, Sequencing Errors, and Misannotation

  Major Vulnerabilities of Primary Repositories:
  1. High Redundancy: >40,000 distinct entries for human beta-globin (clones, ESTs).
  2. Sequencing Artifacts: Sanger dye blobs, NGS indels causing artificial frameshifts.
  3. Contamination: Vector DNA (pUC19, cloning linkers) submitted as human genomic DNA.
  4. Transitive Misannotation: An author mislabels an enzyme -> deposits in GenBank ->
     other researchers run BLAST -> copy the misannotation -> errors cascade globally!

Speaker Bullets:
* Never assume a sequence in GenBank is 100% correct simply because it is in the database!
```

```
================================================================================
SLIDE 4: Secondary (Curated / Derived) Databases: RefSeq
================================================================================
Topic: Non-Redundant, Gold-Standard Reference Sequences

[Visual: 10,000 Redundant GenBank submissions 
         Collapsed into -> ONE Authoritative RefSeq Entry (NM_000518.5)]

Speaker Bullets:
* NCBI created the **RefSeq** project in 2000 to resolve GenBank's redundancy crisis.
* RefSeq provides ONE authoritative, non-redundant reference standard per molecule.
* Unlike GenBank, RefSeq records can be updated, corrected, and merged by NCBI staff
  as new biological evidence emerges.
```

```
================================================================================
SLIDE 5: RefSeq Curation Review Tiers
================================================================================
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

Speaker Bullets:
* Always check the `COMMENT` section of a RefSeq record for the curation status tag.
* Human *HBB* (`NM_000518.5`) is a `REVIEWED` gold-standard record.
```

```
================================================================================
SLIDE 6: UniProtKB: Swiss-Prot vs TrEMBL
================================================================================
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

Speaker Bullets:
* Swiss-Prot represents the pinnacle of manual protein curation.
* TrEMBL captures newly sequenced genomes automatically until curators can review them.
```

```
================================================================================
SLIDE 7: GenBank Historical Taxonomic Divisions
================================================================================
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

Speaker Bullets:
* GenBank historically partitioned flat files into 3-letter codes for FTP distribution.
* Found on the `LOCUS` line of every flat file.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 07

* Primary repositories (GenBank, ENA, DDBJ) are archival, redundant, and submitter-owned.
* Secondary databases (RefSeq, Swiss-Prot) are curated, non-redundant, and authoritative.
* For routine experiments and primer design, always select curated secondary records.
* Next Lecture: Dissecting the GenBank Flat File line by line — LOCUS, FEATURES,
  and Location syntax.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Epistemological Divide: Primary vs Secondary Data

Biological sequence databases are fundamentally divided into two philosophical categories based on data provenance, ownership, and maintenance:

```
  Property               Primary Databases (Archival)           Secondary Databases (Curated/Derived)
  ---------------------------------------------------------------------------------------------------
  Core Mandate           Permanent legal record of submission   Authoritative biological consensus
  Ownership              Owned exclusively by original author   Maintained and curated by database staff
  Redundancy             Extremely high (thousands of copies)   Strictly non-redundant (1 record / entity)
  Curation               Minimal (automated syntax checks only) Deep manual and computational review
  Error Correction       Staff cannot alter; author must update Staff can edit, merge, or correct records
  Primary Examples       GenBank, ENA, DDBJ, PDB, SRA           RefSeq, UniProtKB/Swiss-Prot, Pfam
```

#### The Archival Mandate of Primary Repositories
The International Nucleotide Sequence Database Collaboration (INSDC: GenBank, ENA, DDBJ) operates under the principle of **archival permanence**. When a research team sequences a gene and submits it to GenBank to obtain an accession number for publication, that submission represents a historical, legal public disclosure. Even if subsequent research reveals that the sequenced clone contained PCR amplification errors or bacterial vector contamination, NCBI staff are legally and procedurally prohibited from altering or deleting the record without explicit authorization from the original submitter.

---

### 2. The Quality Crisis in Primary Data

Because primary repositories accept data unconditionally from thousands of laboratories worldwide, they suffer from systemic errors:

1. **Massive Sequence Redundancy:**  
   Searching GenBank for a medically important gene such as human beta-globin (*HBB*) yields tens of thousands of individual records. Most represent truncated cDNAs, partial genomic clones, PCR primers, and population re-sequencing fragments. A researcher seeking the wild-type reference sequence cannot easily determine which record is correct.
2. **Sequencing Artifacts and Base Errors:**  
   Sanger sequencing artifacts (compression bands, dye blobs) and next-generation sequencing errors (homopolymeric indels in pyrosequencing/semiconductor sequencing) introduce false substitutions and frameshifts. In primary databases, these artifacts are frequently presented as real novel biological variants.
3. **Cloning Vector Contamination:**  
   Historically, researchers cutting recombinant plasmids often accidentally sequenced flanking cloning vector fragments (e.g., pUC19, polylinkers, bacteriophage M13 tags) and deposited the hybrid chimeras into GenBank without trimming.
4. **Transitive Misannotation (Error Cascades):**  
   If Submitter A accidentally mislabels an *ABC transporter* as a *kinase* and deposits it in GenBank, Submitter B sequencing a related gene runs a BLAST search, identifies Submitter A's record as the closest hit, and labels their own gene a *kinase*. This transitive error propagates virally across thousands of entries.

---

### 3. The NCBI Reference Sequence (RefSeq) Solution

To solve the redundancy and misannotation crisis, NCBI initiated the **RefSeq** project in 2000 under the leadership of Kim Pruitt. 

RefSeq creates a centralized, non-redundant, expertly curated database of reference standards for genomic, transcriptomic, and proteomic sequences.

```
                  +----------------------------------------------+
                  |           Primary GenBank Submissions        |
                  |  (Thousands of partial, redundant cDNAs/ESTs)|
                  +----------------------+-----------------------+
                                         |
                                         v
                         NCBI Curation & Quality Pipelines
                         * Merge overlapping transcripts
                         * Trim cloning vector artifacts
                         * Reconcile splice junctions with genome
                         * Cross-check with peer-reviewed literature
                                         |
                                         v
                  +----------------------------------------------+
                  |         Authoritative RefSeq Record          |
                  |           NM_000518.5 (Human HBB)            |
                  +----------------------------------------------+
```

#### RefSeq Curation Review Status Tiers:
Inside the `COMMENT` block of every RefSeq flat file, NCBI assigns an explicit curation status tag:
- **`REVIEWED`:** The gold standard. A human NCBI staff biologist has read the primary literature, validated the full-length sequence, confirmed start/stop codons and splice junctions, and compiled curated bibliography cross-references.
- **`VALIDATED`:** The sequence has passed automated computational quality checks and has been verified against full-length cDNAs, but has not yet undergone comprehensive human manual literature review.
- **`PROVISIONAL`:** Initial computational entry created by merging reliable EST/mRNA data; awaiting formal review.
- **`PREDICTED`:** Generated completely by automated *ab initio* gene prediction algorithms (such as GNOMON) running over whole-genome assemblies (designated by `XM_` / `XP_` prefixes).
- **`INFERRED`:** Sequence structure derived from physical mapping data or homologous cross-species evidence.

---

### 4. UniProtKB: The Global Proteomic Landscape

In the protein domain, the primary curated resource is **UniProtKB (Universal Protein Resource)**, maintained by the UniProt Consortium (EMBL-EBI, the Swiss Institute of Bioinformatics [SIB], and the Protein Information Resource [PIR]).

UniProtKB is structurally partitioned into two distinct tiers:

```
                                +--------------------------------+
                                |           UniProtKB            |
                                +---------------+----------------+
                                                |
                       +------------------------+------------------------+
                       |                                                 |
                       v                                                 v
           +-----------------------+                         +-----------------------+
           | UniProtKB/Swiss-Prot  |                         |   UniProtKB/TrEMBL    |
           +-----------------------+                         +-----------------------+
           | Curated & Reviewed    |                         | Unreviewed Automated  |
           | ~570,000 records      |                         | >250,000,000 records  |
           | Gold-standard quality |                         | High-throughput scale |
           | P68871 (HBB_HUMAN)    |                         | Direct INSDC trans.   |
           +-----------------------+                         +-----------------------+
```

#### A. UniProtKB/Swiss-Prot (Curated)
Created by Amos Bairoch in 1986, Swiss-Prot is manually curated by professional biocurators. Curators extract experimental biochemical data from published literature, annotating:
- Active sites and catalytic residues (with Enzyme Commission numbers).
- Post-translational modifications (phosphorylation, glycosylation, acetylation).
- 3D structural domain boundaries.
- Experimentally validated single amino acid polymorphisms (e.g. HbS Glu6Val).

#### B. UniProtKB/TrEMBL (Translated EMBL)
Because manual curation requires hours of human labor per protein, Swiss-Prot could not keep pace with high-throughput genomic sequencing. In 1996, the consortium introduced **TrEMBL**. TrEMBL automatically translates every coding sequence (CDS) feature deposited in the INSDC, applies automated computational annotations via rule-based systems (UniRule, ARBA), and makes the protein immediately retrievable. Once a biocurator reviews a TrEMBL entry, it is promoted to Swiss-Prot and deleted from TrEMBL.

---

### 5. GenBank Historical Divisions

When GenBank distributed sequence data via magnetic tapes and early FTP networks in the 1980s, storage and network bandwidth constraints required splitting the database into smaller, manageable files. NCBI established 3-letter division codes that remain visible on the `LOCUS` line:

```
  Traditional Taxonomic Divisions        High-Throughput / Specialized Divisions
  -------------------------------------------------------------------------------------------------
  PRI: Primates (Human, Chimpanzee)      EST: Expressed Sequence Tags (partial cDNA single reads)
  ROD: Rodents (Mouse, Rat)              GSS: Genome Survey Sequences (single-pass genomic reads)
  MAM: Other Mammals (Cow, Dog, Pig)     HTG: High-Throughput Genomic (unfinished BAC contigs)
  VRT: Other Vertebrates (Fish, Frog)    HTC: High-Throughput cDNA
  INV: Invertebrates (Fly, Worm)         WGS: Whole Genome Shotgun contig assemblies
  PLN: Plants, Algae, and Fungi          TSA: Transcriptome Shotgun Assembly
  BCT: Bacteria                          SYN: Synthetic molecules, cloning vectors, linkers
  VRL: Viruses                           PAT: Patent sequences deposited via patent offices
  PHG: Bacteriophages                    ENV: Environmental / Metagenomic environmental samples
```

---

## Worked Example: Tracking Human *HBB* Across Database Tiers

Let us compare how the identical biological entity (human beta-globin) is represented across three distinct database tiers:

```
  Tier 1: Primary Archival Submission (GenBank)
          Accession: V00491.1
          Authors: Marotta CA, Forget BG, et al. (1977)
          Title: "Human beta-globin messenger RNA. Nucleotide sequence of the 5'-terminal region"
          Characteristics: Historical archival cDNA clone; partial 5' sequence; cannot be modified
                          by NCBI; contains historical sequencing ambiguities.

  Tier 2: Secondary Curated Reference Standard (NCBI RefSeq)
          Accession.Version: NM_000518.5
          Curation Status: REVIEWED
          Characteristics: Exactly 626 bp mature full-length mRNA; CDS: bases 51..494;
                          manually validated against 50+ experimental papers; consensus standard.

  Tier 3: Secondary Expert Protein Knowledgebase (UniProtKB/Swiss-Prot)
          Accession / Entry Name: P68871 (HBB_HUMAN)
          Curation Status: Reviewed (Swiss-Prot)
          Characteristics: 147 amino acids; detailed manual annotations of haem-binding
                          residues (His93, His64), Bohr effect salt bridges (His147),
                          and sickle cell variant (E7V / dbSNP rs334).
```

---

## Formative In-Class Checks

### Question 1
**Prompt:** A laboratory isolates a cDNA clone from a diseased tissue and discovers a 2-base pair insertion inside the *HBB* coding sequence that is not present in RefSeq `NM_000518.5`. If they submit this sequence to GenBank, will it be accepted? What happens if an NCBI reviewer believes the insertion is a PCR amplification error?

**Model Answer:**
- **Will it be accepted?** Yes. GenBank is an archival primary repository; it will accept the submission provided it meets basic formatting and syntactic standards, assigning a permanent primary accession number.
- **What happens if an NCBI reviewer suspects an error?** The NCBI reviewer may contact the author to ask for confirmation, but **NCBI staff cannot reject, alter, or edit the sequence data**. The author owns the record. If the author insists on submitting it, GenBank publishes it as submitted, because primary repositories archive scientific claims, leaving validation to the wider scientific community.

---

### Question 2
**Prompt:** In UniProtKB, what is the functional difference between an entry with accession `P68871` and an entry with accession `A0A024RBG1`? Which entry should you consult to understand the active-site stereochemistry of human beta-globin?

**Model Answer:**
- **`P68871` (`HBB_HUMAN`):** Belongs to **UniProtKB/Swiss-Prot**. It is a manually reviewed, expert-curated entry with validated literature cross-references, functional annotations, and structural binding sites.
- **`A0A024RBG1`:** Belongs to **UniProtKB/TrEMBL**. It is an unreviewed, computationally generated translation produced automatically from an INSDC nucleotide submission without human literature review.
- **Which to consult:** To understand active-site stereochemistry and haem binding, you must consult **`P68871` (Swiss-Prot)**, because Swiss-Prot records contain manually verified, experimental annotations of catalytic residues and ligand coordination.

---

### Question 3
**Prompt:** Explain why high-throughput genomic data divisions such as `EST` (Expressed Sequence Tags) and `GSS` (Genome Survey Sequences) were historically segregated from the standard organismal taxonomic divisions (`PRI`, `ROD`, `BCT`) in GenBank.

**Model Answer:**
In the late 1990s, high-throughput automated sequencing facilities generated millions of single-pass, unedited, error-prone reads (ESTs and GSS). 
1. If these low-quality reads had been mixed into the standard organismal divisions (`PRI`, `ROD`), the sheer volume of fragmented, noisy data would have overwhelmed standard database searches and crashed computational indexing engines.
2. Segregating them into dedicated divisions (`EST`, `GSS`) allowed researchers performing targeted searches in standard taxonomic divisions (`PRI`) to avoid wading through millions of redundant, low-quality fragments, while allowing specialized researchers to query or filter high-throughput datasets separately.
