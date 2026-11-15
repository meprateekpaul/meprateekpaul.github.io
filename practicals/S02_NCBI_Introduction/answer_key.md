# Instructor Answer Key & Evaluation Manual: Practical 02 (Introduction to NCBI)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S02 (Syllabus Practical P2)  
**Curriculum Topic:** Introduction to NCBI and Gene Database Navigation  

---

## 1. Expected Outputs & Reference Solutions

### Table 2.1: NCBI Gene Profile for Human *HBB* (Gene ID: 3043) (Completed)
| Parameter / Field | Observed Value / Description |
|---|---|
| Official Gene Symbol | `HBB` |
| Official Full Name | `hemoglobin subunit beta` |
| NCBI Gene ID | `3043` |
| Organism & Taxonomy ID | `Homo sapiens` (Taxonomy ID: `9606`) |
| Chromosomal Location & Cytogenetic Band | Chromosome 11; `11p15.4` |
| Genomic Coordinates (GRCh38.p14) | From: `5,225,464` To: `5,227,071` (NC_000011.10) |
| Strand Orientation (+ forward / - complement) | `-` (Minus strand / reverse complement) |
| Total Genomic Span (bp) | `1,608` bp (from start to end of transcribed primary unit) |
| Number of Exons / Introns | `3` Exons / `2` Introns |
| Curated RefSeq mRNA Accession | `NM_000518.5` (length: 626 bp) |
| Curated RefSeq Protein Accession | `NP_000509.1` (length: 147 aa) |
| Primary Associated Disease Phenotypes (OMIM) | `141900` (Hemoglobin beta locus / Beta-Thalassemia), `603903` (Sickle Cell Anemia) |

### Table 2.2: Cross-Gene Comparative Analysis (Completed)
| Metric | *HBB* | *INS* | *TP53* |
|---|---|---|---|
| NCBI Gene ID | `3043` | `3630` | `7157` |
| Chromosome | `11` | `11` | `17` |
| Cytogenetic Band | `11p15.4` | `11p15.5` | `17p13.1` |
| Primary mRNA Accession | `NM_000518.5` | `NM_000207.3` | `NM_000546.6` |
| Protein Length (aa) | `147` | `110` | `393` |
| Biological Function | Adult oxygen carrier (beta chain) | Glucose homeostasis peptide hormone | Tumor suppressor / cell cycle checkpoint |

---

## 2. Sample Screenshot / Layout Guide

```
+------------------------------------------------------------------------------------------------+
| NCBI Gene: HBB hemoglobin subunit beta [ Homo sapiens (human) ]                  Gene ID: 3043 |
+------------------------------------------------------------------------------------------------+
| Official Symbol: HBB provided by HGNC                                                         |
| Organism: Homo sapiens | Lineage: Eukaryota; Metazoa; Chordata; Mammalia; Primates; Hominidae   |
| Primary source: HGNC:HGNC:4827                                                                 |
| See related: MIM: 141900, MIM: 603903                                                         |
|                                                                                                |
| Genomic Context (GRCh38.p14 Primary Assembly):                                                 |
| Chromosome: 11; Location: 11p15.4                                                              |
| Annotation release: 109.20210514 | Chromosome 11 - NC_000011.10 (5225464..5227071, complement)  |
|                                                                                                |
| Genomic regions, transcripts, and products:                                                    |
| [Exon 1]====(Intron 1)====[Exon 2]========(Intron 2)========[Exon 3]                           |
|  NM_000518.5 (626 nt) ---> NP_000509.1 (147 aa)                                                |
+------------------------------------------------------------------------------------------------+
```

---

## 3. Model Answers to Discussion Questions

### Q1. RefSeq vs. GenBank Architecture
- **Model Answer:** GenBank is an archival primary repository whose core mandate is to preserve an unedited historical record of all direct submissions from individual researchers and genome centers. It contains massive redundancy, inconsistent nomenclature, sequencing errors, unverified annotations, and fragment clones. In contrast, RefSeq provides a non-redundant, manually and computationally curated reference standard. Relying solely on primary GenBank records in automated computational pipelines leads to extreme skewing (e.g., highly studied genes having thousands of duplicate hits, artificial inflation of gene counts, and propagation of author-submitted sequencing artifacts).

### Q2. Genomic Strand Orientation
- **Model Answer:** Because *HBB* is on the minus (`-`) strand of Chromosome 11 (`NC_000011.10: complement(5225464..5227071)`), RNA polymerase II transcribes using the chromosomal top strand (5' $\rightarrow$ 3' as reported in the assembly) as the template strand. Consequently, the transcribed pre-mRNA and the resulting mature mRNA (`NM_000518.5`) correspond to the **reverse complement** of the chromosomal sequence as listed from lower to higher coordinate values. The 5' cap of the mRNA maps to the higher chromosomal coordinate (~5,227,071), and the poly-A tail maps to the lower coordinate (~5,225,464).

### Q3. Physical Linkage (*HBB* vs. *INS*)
- **Model Answer:** Both genes are located on the short arm (p) of human chromosome 11. *INS* is located at `11p15.5` (coordinates ~2,159,779 to ~2,161,209 on GRCh38), whereas *HBB* is at `11p15.4` (coordinates ~5,225,464 to ~5,227,071). They are physically separated by approximately 3.06 megabases (Mb) of genomic DNA. Despite their chromosomal co-localization, they do not share transcriptional regulation: *HBB* is controlled by the upstream Beta-Globin Locus Control Region (LCR) specifically active in erythroid lineages, while *INS* is regulated by pancreatic beta-cell specific transcription factors (PDX1, NeuroD1, MafA).

### Q4. Gene ID Stability
- **Model Answer:** Gene symbols are human-assigned text tokens that change frequently due to historical reclassification, nomenclature revisions (HGNC updates), or competing laboratory names (e.g., *p53* vs. *TP53*, *OCT4* vs. *POU5F1*). Furthermore, symbols can create typographical errors or be corrupted by spreadsheet software (e.g., *SEPT2* interpreted as a date). An integer Gene ID (e.g., `3043`) is an immutable, language-agnostic, unique database key that permanently anchors cross-database queries across relational schemas.

### Q5. Entrez Interlinking
- **Model Answer:** Entrez utilizes an underlying associative network ("LinkOut" and neighbor graphs) driven by NCBI's ASN.1 data model. A specific pathogenic mutation in ClinVar (e.g., `VCV000015091` for HBB Glu6Val) is explicitly indexed with its RefSeq CDS position, dbSNP identifier (`rs334`), and Gene ID (`3043`). This relational graph links directly to PubMed literature IDs (PMIDs) documenting the clinical trial, to MMDB/PDB structure coordinates (`2HBS`) displaying the mutant valine pocket, and to UniProtKB entries via cross-reference tables.

---

## 4. Solution to Extension / Challenge Task

1. **Taxonomic Hierarchy for *Homo sapiens* (TaxID 9606):**
   `cellular organisms` $\rightarrow$ `Eukaryota` $\rightarrow$ `Opisthokonta` $\rightarrow$ `Metazoa` $\rightarrow$ `Eumetazoa` $\rightarrow$ `Bilateria` $\rightarrow$ `Deuterostomia` $\rightarrow$ `Chordata` $\rightarrow$ `Craniata` $\rightarrow$ `Vertebrata` $\rightarrow$ `Gnathostomata` $\rightarrow$ `Teleostomi` $\rightarrow$ `Euteleostomi` $\rightarrow$ `Sarcopterygii` $\rightarrow$ `Dipnotetrapodomorpha` $\rightarrow$ `Tetrapoda` $\rightarrow$ `Amniota` $\rightarrow$ `Mammalia` $\rightarrow$ `Theria` $\rightarrow$ `Eutheria` $\rightarrow$ `Boreoeutheria` $\rightarrow$ `Euarchontoglires` $\rightarrow$ `Primates` $\rightarrow$ `Haplorrhini` $\rightarrow$ `Simiiformes` $\rightarrow$ `Catarrhini` $\rightarrow$ `Hominoidea` $\rightarrow$ `Hominidae` $\rightarrow$ `Homininae` $\rightarrow$ `Homo` $\rightarrow$ `Homo sapiens`.
2. **Total Entrez Records:** Hundreds of thousands of nucleotide/protein records in GenBank/RefSeq.
3. **Role of `taxdump.tar.gz`:** Contains relational flat files (`names.dmp`, `nodes.dmp`, `merged.dmp`) mapping every NCBI TaxID to its scientific name, rank, and parent TaxID node. Metagenomic classifiers (e.g., Kraken2, Centrifuge, Kaiju) require this archive locally to assign Lowest Common Ancestor (LCA) taxonomic classifications to short sequencing reads in milliseconds without querying remote NCBI servers.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & Gene Query** | 2.0 | Deduct 0.5 if query strings lack field tags (`[GENE]`, `[ORGN]`). |
| **Data Extraction (Table 2.1 & 2.2)** | 4.0 | Deduct 0.5 per missing coordinate, incorrect chromosome band, or missing accession. |
| **Accuracy of Comparative Analysis** | 2.0 | Deduct 0.5 if INS or TP53 data is incomplete or inaccurate. |
| **Discussion Questions & Critical Thinking** | 2.0 | Award 0.4 marks per question for scientifically rigorous explanation. |
| **Total** | **10.0** | |
