---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 29 Slides: Genome Projects and Annotation"
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
# Lecture 29 — Genome Projects and Annotation
### Concepts of Bioinformatics (CBBI-501)
**Unit 11:** Comparative Genome Analysis  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Era of Whole-Genome Sequencing

```text
Topic: From Individual Genes to Complete Genomic Blueprints

[Visual: Timeline of Genomic Milestones:
  1977: PhiX174 Bacteriophage (5,386 bp - Sanger)
  1995: Haemophilus influenzae (1.8 Mb - First cellular organism)
  2001: Draft Human Genome Project (3.0 Gb - $3 Billion, 13 years!)
  2024: Telomere-to-Telomere (T2T) gapless human genome ($300 in 24 hours!)]
```

**Speaker Talking Points:**  
* Biology has transitioned from studying isolated genes to analyzing entire genomes.
* Generating raw sequence reads is only the first phase; transforming reads into
  an assembled, annotated, biologically meaningful chromosome is the core task of bioinformatics.

---

## Slide 2: Sequencing Paradigms: Short Reads vs Long Reads

```text
Topic: The Technological Arsenal

+--------------------+-------------------------+------------------------------+
| Technology         | Read Length             | Strengths & Limitations      |
+--------------------+-------------------------+------------------------------+
| **Sanger**         | 700 to 1,000 bp         | Gold standard accuracy (>99.99%);
| (Dideoxy)          |                         | low throughput, high cost    |
| **Illumina (NGS)** | 100 to 300 bp           | Massive throughput (Terabases);
| (Short-Read)       | (Paired-end)            | cannot span long repeats!    |
| **PacBio / Nanopore| 15,000 to >100,000 bp   | Spans complex tandem repeats |
| (Long-Read)**      | (HiFi / Long-read)      | and centromeres; T2T assemblies|
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* Short reads fail to assemble across repetitive regions longer than read length.
* Long reads span through repeats, assembling complete chromosome arms from end to end.

---

## Slide 3: Genome Assembly Paradigms: OLC vs De Bruijn Graphs

```text
Topic: The Mathematical Engines of Assembly

1. Overlap-Layout-Consensus (OLC) — For Long Reads:
   * Calculates all-against-all read overlaps.
   * Builds an overlap graph; finds a path traversing each read once (Hamiltonian path).

2. De Bruijn Graphs (DBG) — For Short-Read NGS:
   * Breaks billions of reads into short words of length k (k-mers).
   * Graph nodes are (k-1)-mers; directed edges are k-mers!
   * Finds an Eulerian path visiting every edge once: avoids O(N^2) pairwise comparisons!
```

**Speaker Talking Points:**  
* De Bruijn graphs enabled computing assemblies on standard servers with billions of reads.

---

## Slide 4: Measuring Assembly Quality: Contigs, Scaffolds, and N50

```text
Topic: Quantifying Contiguity

[Visual: Contigs (continuous sequence) 
         -> Linked by paired-end mate bridges across gaps (NNNNNN)
         -> Scaffolds (ordered, oriented chains)]

The N50 Metric:
  "The contig length such that 50% of the entire genome assembly is contained
   in contigs of this length or longer."
```

**Speaker Talking Points:**  
* Higher N50 = superior, more contiguous assembly.
* L50: The smallest *number* of contigs required to reach 50% of the genome (lower is better!).

---

## Slide 5: Structural Annotation: Mapping the Genetic Real Estate

```text
Topic: Where Are the Functional Elements?

[Visual: Layered Annotation Tracks along a Chromosome:
  Track 1: RepeatMasker (Alu, LINE-1, simple repeats masked)
  Track 2: Non-coding RNAs (tRNAs, rRNAs, microRNAs)
  Track 3: Ab initio gene predictions (Augustus, GeneMark HMMs)
  Track 4: Transcript mapping (RNA-seq spliced alignments via HISAT2/STAR)
  Track 5: Verified Exon-Intron Gene Model (5' UTR -> Exons -> 3' UTR)]
```

**Speaker Talking Points:**  
* Structural annotation answers: "What is the physical coordinate boundaries of every gene?"

---

## Slide 6: Functional Annotation: Assigning Biological Meaning

```text
Topic: What Does Each Gene Do?

  Pipelines for Assigning Function:
  1. Sequence Homology Transfer:
     * BLAST search against UniProtKB/Swiss-Prot and RefSeq.
  2. Domain Architecture:
     * InterProScan maps Pfam domains, active sites, and signal peptides.
  3. Gene Ontology (GO) Categorization:
     * Molecular Function (e.g. "oxygen transporter activity")
     * Biological Process (e.g. "gas transport")
     * Cellular Component (e.g. "hemoglobin complex")
  4. Metabolic Pathway Integration:
     * Mapping to KEGG and Reactome biological networks.
```

**Speaker Talking Points:**  
* Functional annotation transforms raw gene coordinates into actionable biochemistry.

---

## Slide 7: Standard Annotation Formats: GFF3 and GTF

```text
Topic: The Tab-Delimited Syntax of Annotation

  GFF3 Format (9 Tab-Delimited Columns):
  chr11  RefSeq  gene   5225464  5227071  .  -  .  ID=gene-HBB;Dbxref=GeneID:3043
  chr11  RefSeq  mRNA   5225464  5227071  .  -  .  ID=rna-NM_000518.5;Parent=gene-HBB
  chr11  RefSeq  exon   5225464  5225724  .  -  .  ID=exon-1;Parent=rna-NM_000518.5
  chr11  RefSeq  CDS    5225597  5225724  .  -  0  ID=cds-NP_000509.1;Parent=rna-NM_000518.5
```

**Speaker Talking Points:**  
* GFF3 uses parent-child hierarchical attributes to link genes, mRNAs, exons, and CDS.

---

## Slide 8: Summary & Navigating Genome Browsers

```text
Topic: Exploring Genomes Visually

* **UCSC Genome Browser:** Track hub pioneer; displays conservation, epigenetics, SNPs.
* **Ensembl (EMBL-EBI):** Focus on vertebrate comparative genomics and gene trees.
* **NCBI Genome Data Viewer (GDV):** Direct integration with Entrez and RefSeq.
* Next Lecture: Synteny and Comparative Genomics — The final capstone tracing
  the HBB gene family across vertebrate chromosomes!
```

