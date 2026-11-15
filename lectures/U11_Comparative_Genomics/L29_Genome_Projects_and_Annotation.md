# Lecture 29 — Genome Projects and Annotation

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 11:** Comparative Genome Analysis  
**Syllabus Topic:** Introduction, application, genome analysis and annotation  
**Primary Learning Outcome:** LO8 — Explain comparative genomics workflows, calculate genome assembly metrics (N50, L50), and distinguish structural from functional annotation.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Era of Whole-Genome Sequencing
================================================================================
Topic: From Individual Genes to Complete Genomic Blueprints

[Visual: Timeline of Genomic Milestones:
  1977: PhiX174 Bacteriophage (5,386 bp - Sanger)
  1995: Haemophilus influenzae (1.8 Mb - First cellular organism)
  2001: Draft Human Genome Project (3.0 Gb - $3 Billion, 13 years!)
  2024: Telomere-to-Telomere (T2T) gapless human genome ($300 in 24 hours!)]

Speaker Bullets:
* Biology has transitioned from studying isolated genes to analyzing entire genomes.
* Generating raw sequence reads is only the first phase; transforming reads into
  an assembled, annotated, biologically meaningful chromosome is the core task of bioinformatics.
```

```
================================================================================
SLIDE 2: Sequencing Paradigms: Short Reads vs Long Reads
================================================================================
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

Speaker Bullets:
* Short reads fail to assemble across repetitive regions longer than read length.
* Long reads span through repeats, assembling complete chromosome arms from end to end.
```

```
================================================================================
SLIDE 3: Genome Assembly Paradigms: OLC vs De Bruijn Graphs
================================================================================
Topic: The Mathematical Engines of Assembly

1. Overlap-Layout-Consensus (OLC) — For Long Reads:
   * Calculates all-against-all read overlaps.
   * Builds an overlap graph; finds a path traversing each read once (Hamiltonian path).

2. De Bruijn Graphs (DBG) — For Short-Read NGS:
   * Breaks billions of reads into short words of length k (k-mers).
   * Graph nodes are (k-1)-mers; directed edges are k-mers!
   * Finds an Eulerian path visiting every edge once: avoids O(N^2) pairwise comparisons!

Speaker Bullets:
* De Bruijn graphs enabled computing assemblies on standard servers with billions of reads.
```

```
================================================================================
SLIDE 4: Measuring Assembly Quality: Contigs, Scaffolds, and N50
================================================================================
Topic: Quantifying Contiguity

[Visual: Contigs (continuous sequence) 
         -> Linked by paired-end mate bridges across gaps (NNNNNN)
         -> Scaffolds (ordered, oriented chains)]

The N50 Metric:
  "The contig length such that 50% of the entire genome assembly is contained
   in contigs of this length or longer."

Speaker Bullets:
* Higher N50 = superior, more contiguous assembly.
* L50: The smallest *number* of contigs required to reach 50% of the genome (lower is better!).
```

```
================================================================================
SLIDE 5: Structural Annotation: Mapping the Genetic Real Estate
================================================================================
Topic: Where Are the Functional Elements?

[Visual: Layered Annotation Tracks along a Chromosome:
  Track 1: RepeatMasker (Alu, LINE-1, simple repeats masked)
  Track 2: Non-coding RNAs (tRNAs, rRNAs, microRNAs)
  Track 3: Ab initio gene predictions (Augustus, GeneMark HMMs)
  Track 4: Transcript mapping (RNA-seq spliced alignments via HISAT2/STAR)
  Track 5: Verified Exon-Intron Gene Model (5' UTR -> Exons -> 3' UTR)]

Speaker Bullets:
* Structural annotation answers: "What is the physical coordinate boundaries of every gene?"
```

```
================================================================================
SLIDE 6: Functional Annotation: Assigning Biological Meaning
================================================================================
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

Speaker Bullets:
* Functional annotation transforms raw gene coordinates into actionable biochemistry.
```

```
================================================================================
SLIDE 7: Standard Annotation Formats: GFF3 and GTF
================================================================================
Topic: The Tab-Delimited Syntax of Annotation

  GFF3 Format (9 Tab-Delimited Columns):
  chr11  RefSeq  gene   5225464  5227071  .  -  .  ID=gene-HBB;Dbxref=GeneID:3043
  chr11  RefSeq  mRNA   5225464  5227071  .  -  .  ID=rna-NM_000518.5;Parent=gene-HBB
  chr11  RefSeq  exon   5225464  5225724  .  -  .  ID=exon-1;Parent=rna-NM_000518.5
  chr11  RefSeq  CDS    5225597  5225724  .  -  0  ID=cds-NP_000509.1;Parent=rna-NM_000518.5

Speaker Bullets:
* GFF3 uses parent-child hierarchical attributes to link genes, mRNAs, exons, and CDS.
```

```
================================================================================
SLIDE 8: Summary & Navigating Genome Browsers
================================================================================
Topic: Exploring Genomes Visually

* **UCSC Genome Browser:** Track hub pioneer; displays conservation, epigenetics, SNPs.
* **Ensembl (EMBL-EBI):** Focus on vertebrate comparative genomics and gene trees.
* **NCBI Genome Data Viewer (GDV):** Direct integration with Entrez and RefSeq.
* Next Lecture: Synteny and Comparative Genomics — The final capstone tracing
  the HBB gene family across vertebrate chromosomes!
```

---

## Detailed Comprehensive Technical Notes

### 1. The Technological Evolution of Genome Projects

The field of whole-genome sequencing has progressed across three technological epochs:

```
  Metric                 First Generation (1990-2005)   Second Generation (2006-2016)  Third Generation (2016-Present)
  -------------------------------------------------------------------------------------------------
  Dominant Technology    Sanger Dideoxy Sequencing      Illumina Sequencing-by-Synthesis PacBio HiFi / Oxford Nanopore
  Read Length            700 to 1,000 base pairs        100 to 300 base pairs (Paired)  15,000 to >100,000 base pairs
  Primary Assembly Graph Overlap-Layout-Consensus (OLC) De Bruijn Graph (k-mers)        String Graphs / Modern OLC
  Error Profile & Rate   Very low (<0.01% substitution) Extremely low (~0.1% subst)     HiFi: <0.1% accurate reads
  Resolution of Repeats  Moderate (limited by clones)   Poor; collapses repeats >300 bp Spans long tandem repeats,
                                                                                        centromeres, and segmental dups
  Milestone Landmark     Human Genome Project (2001)    1,000 Genomes Project (2012)    Telomere-to-Telomere (T2T, 2022)
```

#### The Repeat Collapse Problem in Assembly:
If an organism possesses an identical 1,000-bp transposable element (e.g. an Alu or LINE) present in 50 distinct chromosomal loci, short 150-bp reads originating from within that element cannot be uniquely mapped to any single locus. In a short-read assembly, all 50 distinct repeat loci collapse into a single over-represented contig, shattering the assembly into thousands of fragmented pieces. Long reads (>20 kb) span across the entire repeat into unique flanking sequence on both sides, resolving repeat copies unambiguously.

---

### 2. Algorithmic Paradigms: OLC vs De Bruijn Graphs

#### A. Overlap-Layout-Consensus (OLC)
Used historically for Sanger sequencing and modern long-read sequencing:
1. **Overlap:** Compute all-against-all pairwise sequence alignments between reads to identify suffix-to-prefix overlaps exceeding a minimum length threshold.
2. **Layout:** Construct an **Overlap Graph** where nodes represent reads and directed edges represent valid overlaps. The assembly problem reduces to finding a path that visits every read once (a Hamiltonian path).
3. **Consensus:** Align overlapping reads along the path and calculate the most probable consensus nucleotide sequence.
*Computational Limit:* Calculating all-against-all overlaps for 1 billion short reads requires $\mathcal{O}(N^2) \approx 10^{18}$ comparisons, which is computationally intractable.

#### B. De Bruijn Graphs (DBG)
Developed by Pavel Pevzner (2001) to assemble short reads without all-against-all comparisons:
1. Every read of length $L$ is decomposed into $(L - k + 1)$ overlapping substrings of length $k$ (**$k$-mers**).
2. Construct a **De Bruijn Graph**:
   - **Nodes:** Unique substrings of length $k - 1$.
   - **Directed Edges:** The observed $k$-mers that connect a $(k-1)$-mer prefix to its $(k-1)$-mer suffix.
3. The assembly reduces to finding an **Eulerian Path**—a path that visits every directed edge in the graph exactly once.
*Computational Breakthrough:* An Eulerian path can be solved in linear time $\mathcal{O}(E)$, allowing short-read assemblers (Velvet, SPAdes, SOAPdenovo) to assemble billions of reads efficiently.

---

### 3. Quantitative Assembly Contiguity Metrics: N50 and L50

When an assembler finishes, it outputs a collection of assembled fragments called **contigs** (continuous sequences without gaps). When paired-end reads or optical maps link contigs across unsequenced gaps of estimated length, they are chained into **scaffolds**.

To evaluate the contiguity of an assembly, bioinformaticians calculate **$N50$** and **$L50$**:

```
  Sorted Contig Lengths (Descending):
  [ ====== 50 kb ====== ] [ ==== 30 kb ==== ] [ === 20 kb === ] [ = 10 kb = ]
  |<-------------------------- 50% Genome Size ------------------------->|
                                             ^ (N50 Contig!)
```

#### Mathematical Definitions:
1. Order all contigs in descending order of length: $L_1 \ge L_2 \ge \dots \ge L_m$.
2. Calculate the cumulative sum of contig lengths until the running sum reaches or exceeds **$50\%$ of the total assembly length** (or estimated genome size):
   $$\sum_{i=1}^{k} L_i \ge 0.50 \times L_{\text{total}}$$
3. **N50 Metric:** The length of contig $k$ ($L_k$). It represents the length of the shortest contig in that 50% subset. **Larger N50 = higher contiguity**.
4. **L50 Metric:** The integer count $k$ of contigs required to achieve 50% of the total assembly. **Smaller L50 = higher contiguity**.

---

### 4. Genome Annotation: Structural vs Functional

A newly assembled genome is merely an unpunctuated string of gigabases. **Genome Annotation** is the multi-stage bioinformatics process that demarcates biological coordinates and functional roles.

```
                               Raw Genome Assembly
                                        |
                     +------------------+------------------+
                     |                                     |
           Structural Annotation                 Functional Annotation
        "Where are the components?"              "What do they do?"
                     |                                     |
         * RepeatMasking (Transposons)         * Homology Transfer (BLASTP)
         * ncRNA mapping (tRNAs, rRNAs)        * Domain Architecture (InterPro)
         * Spliced Transcript Mapping          * Gene Ontology (GO Terms)
           (RNA-seq / Iso-Seq alignments)      * Metabolic Pathways (KEGG)
         * Ab initio HMM Exon Prediction       * Enzyme Commission (EC Numbers)
           (Augustus, GeneMark)
```

---

### 5. Standard Annotation File Formats: GFF3

The **Generic Feature Format version 3 (GFF3)** is the universal, tab-delimited standard for encoding structural genome annotations. It consists of nine required columns:

```
  Col   Field Name   Description & Example Syntax
  -------------------------------------------------------------------------------------------------
  1     seqid        Chromosome or scaffold landmark (e.g. `chr11`, `NC_000011.10`)
  2     source       Software or database that generated the feature (e.g. `RefSeq`, `Augustus`)
  3     type         SO (Sequence Ontology) feature type (e.g. `gene`, `mRNA`, `exon`, `CDS`)
  4     start        1-based integer start coordinate (inclusive) (e.g. `5225464`)
  5     end          1-based integer end coordinate (inclusive) (e.g. `5227071`)
  6     score        Floating point score or E-value (period `.` if omitted)
  7     strand       Strand orientation: `+` (forward), `-` (reverse), or `.` (unstranded)
  8     phase        For CDS features: reading frame phase offset: `0`, `1`, or `2`
  9     attributes   Semicolon-separated key=value tags: `ID=...;Name=...;Parent=...`
```

---

## Worked Example: Calculating $N50$ and $L50$ by Hand

### Problem:
A de novo bacterial genome assembly yields $M = 8$ contigs with the following lengths (in kilobases):
$$20\text{ kb}, \quad 80\text{ kb}, \quad 10\text{ kb}, \quad 150\text{ kb}, \quad 40\text{ kb}, \quad 100\text{ kb}, \quad 30\text{ kb}, \quad 70\text{ kb}$$

1. Calculate the total assembly length ($L_{\text{total}}$).
2. Determine the 50% assembly threshold.
3. Calculate the **$N50$** length metric.
4. Determine the **$L50$** count metric.

---

### Step 1: Calculate Total Assembly Length
$$L_{\text{total}} = 20 + 80 + 10 + 150 + 40 + 100 + 30 + 70 = \mathbf{500\text{ kb}}$$

---

### Step 2: Calculate the 50% Assembly Threshold
$$\text{Threshold} = 0.50 \times L_{\text{total}} = 0.50 \times 500\text{ kb} = \mathbf{250\text{ kb}}$$

---

### Step 3: Sort Contigs in Descending Order and Track Cumulative Sum

```
  Rank (k)   Contig Length (kb)   Cumulative Assembly Length (kb)   Reached 250 kb?
  ---------------------------------------------------------------------------------
  1          150                  150                               No (< 250)
  2          100                  250 (150 + 100)                   **YES (>= 250!)**
  3           80                  330                               Yes
  4           70                  400                               Yes
  5           40                  440                               Yes
  6           30                  470                               Yes
  7           20                  490                               Yes
  8           10                  500                               Yes
```

---

### Step 4: Extract Metrics
- At Rank $k = 2$, the cumulative sum reaches exactly $250\text{ kb}$ ($\ge 50\%$ of the genome).
- The contig length at Rank 2 is **$100\text{ kb}$**.
  $$\mathbf{N50 = 100\text{ kb}}$$
- The number of contigs required to reach the threshold is $2$.
  $$\mathbf{L50 = 2}$$

**Conclusion:**  
Fifty percent of this genome assembly is contained in just 2 large contigs of length $100\text{ kb}$ or greater.

---

## Formative In-Class Checks

### Question 1
**Prompt:** An avian genomics consortium publishes two competing assemblies of the chicken genome:
- **Assembly 1:** Total size $= 1.05\text{ Gb}$; Number of contigs $= 120$; $N50 = 24.5\text{ Mb}$; $L50 = 14$.
- **Assembly 2:** Total size $= 1.02\text{ Gb}$; Number of contigs $= 4,500$; $N50 = 450\text{ kb}$; $L50 = 620$.
Which assembly is superior for comparative synteny analysis? Justify your decision using the metrics.

**Model Answer:**
**Assembly 1 is overwhelmingly superior.**
- **$N50$ Comparison:** Assembly 1 has an $N50$ of $24.5\text{ Mb}$ (megabases), meaning half the genome is assembled into massive, chromosome-arm-length contigs. Assembly 2 has an $N50$ of only $450\text{ kb}$ (kilobases), representing a fragmented draft.
- **$L50$ Comparison:** Assembly 1 reaches half the genome in just $14$ contigs ($L50 = 14$), closely approximating the biological karyotype of avian macrochromosomes. Assembly 2 requires $620$ fragmented contigs ($L50 = 620$).
- Comparative synteny requires long, contiguous chromosomal blocks to verify gene order and detect inversions; Assembly 1 provides the necessary contiguity.

---

### Question 2
**Prompt:** In a GFF3 structural annotation file, what is the mathematical and biological distinction between a feature of type `exon` and a feature of type `CDS` for human *HBB* (`NM_000518.5`)?

**Model Answer:**
- **`exon` Feature:** Represents the transcribed ribonucleotide segments present in the mature processed mRNA. In human *HBB*, Exon 1 spans coordinates `51..142` (plus the $5'$ UTR from bases 1 to 50, total `1..142`). Exons include non-coding untranslated regions ($5'$ UTR and $3'$ UTR).
- **`CDS` (Coding Sequence) Feature:** Represents strictly the translated protein-coding codons that are translated by the ribosome into amino acids, beginning at the initiating Methionine start codon (`ATG`) and ending at the termination stop codon. The CDS excludes the $5'$ UTR and $3'$ UTR, spanning only coordinates `51..494`.

---

### Question 3
**Prompt:** Why is an *ab initio* gene prediction program (like Augustus) that uses Hidden Markov Models prone to high false-positive rates when run on eukaryotic genomic DNA without supporting transcriptomic evidence (RNA-seq)?

**Model Answer:**
*Ab initio* predictors rely purely on probabilistic mathematical models of sequence features (codon bias, hexamer frequencies, donor/acceptor consensus motifs). In eukaryotic genomes:
1. Massive non-coding introns and intergenic deserts contain thousands of **pseudo-splice sites** and random open reading frames that match statistical consensus motifs by chance.
2. The algorithm cannot distinguish between real transcribed genes, transcriptionally silent pseudogenes, and non-functional random genomic matches without physical experimental evidence (such as spliced RNA-seq read alignments) demonstrating that the predicted transcript is actively expressed in living tissue.
