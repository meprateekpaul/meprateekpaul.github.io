---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 21 Slides: Repeats and Open Reading Frames"
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
# Lecture 21 — Repeats and Open Reading Frames
### Concepts of Bioinformatics (CBBI-501)
**Unit 08:** Predictive Methods using Nucleotide Sequence  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Predictive Challenge of Raw DNA

```text
Topic: Deciphering the Unannotated Tape

[Visual: A 100-kilobase string of raw A, C, G, T characters:
  Where are the genes? Where are the promoters? Where are the repetitive parasites?]
```

**Speaker Talking Points:**  
* Modern high-throughput sequencing produces terabases of raw genomic contigs.
* Experimental validation of every gene is impossible; we must predict functional
  elements computationally from primary DNA sequence alone.
* The first two steps in predictive genomics:
  1. Mask repetitive DNA elements.
  2. Map all possible Open Reading Frames (ORFs) across 6 reading frames.

---

## Slide 2: The Eukaryotic Genome Landscape

```text
Topic: Coding vs Non-Coding DNA

[Visual: Pie chart of the Human Genome:
  * Protein-coding exons: ONLY ~1.5%!
  * Introns: ~26%
  * Repetitive transposable elements: >45-50%!
  * Unique non-coding & heterochromatin: Balance]
```

**Speaker Talking Points:**  
* Less than 2% of the human genome encodes proteins!
* Nearly half of the human genome consists of repetitive DNA: molecular fossils
  and transposable elements that replicate within our chromosomes.

---

## Slide 3: Classification of Repetitive DNA

```text
Topic: Tandem vs Interspersed Repeats

1. Tandem Repeats (Head-to-Tail Arrays):
   * Satellite DNA: Megabase-long centromeric arrays (e.g. alpha-satellite).
   * Minisatellites (VNTRs): 10 to 100 bp repeat units; DNA fingerprinting.
   * Microsatellites (STRs): 1 to 6 bp units (e.g. (CA)_n); forensic CODIS markers.

2. Interspersed Repeats (Transposable Elements):
   * SINEs: Non-autonomous (e.g., Alu elements; ~1.2 million copies in humans!).
   * LINEs: Autonomous retrotransposons (e.g., LINE-1 / L1; ~500,000 copies).
   * LTR Retrotransposons & Endogenous Retroviruses (HERVs).
   * DNA Transposons.
```

**Speaker Talking Points:**  
* Tandem repeats expand via replication slippage; interspersed repeats expand via transposition.

---

## Slide 4: Marking Repetitive DNA: RepeatMasker

```text
Topic: Cleaning Genomes Before Analysis

[Visual: Raw Sequence -> RepeatMasker Engine (Screens against Dfam / RepBase)
         -> Masked Sequence (Repeats converted to 'N' or lowercase)]

Command:
  `RepeatMasker -species human -xsmall genomic_contig.fasta`
```

**Speaker Talking Points:**  
* If you run BLAST on an unmasked 50-kb human contig, an Alu element will trigger
  500,000 spurious hits, crashing your browser!
* **RepeatMasker** compares raw contigs against curated consensus repeat libraries
  (Dfam / RepBase) and masks them before gene finding.

---

## Slide 5: Open Reading Frames (ORFs): The Six Reading Frames

```text
Topic: Reading the Triplet Tape in Both Directions

  Double-Stranded DNA:
    Forward Strand 5' --> 3':
      Frame +1: Begins at nucleotide 1  [1, 2, 3] [4, 5, 6] ...
      Frame +2: Begins at nucleotide 2  [2, 3, 4] [5, 6, 7] ...
      Frame +3: Begins at nucleotide 3  [3, 4, 5] [6, 7, 8] ...

    Reverse Strand 5' <-- 3' (Antiparallel):
      Frame -1: Begins at 3' terminal nucleotide reading backwards
      Frame -2: Offset by 1 base
      Frame -3: Offset by 2 bases
```

**Speaker Talking Points:**  
* Any piece of double-stranded DNA can be conceptually translated in **six distinct frames**.
* A frameshift mutation of +1 or -1 completely alters the translated amino acid string.

---

## Slide 6: What Defines an Authentic ORF?

```text
Topic: Start Codons, Stop Codons, and Length Cutoffs

  Definition of an ORF:
  * Starts with an Initiation Codon: `ATG` (Methionine).
  * Followed by a series of triplet sense codons.
  * Ends with an in-frame Termination Codon: `TAA`, `TAG`, or `TGA`.

  Statistical Reality:
  * In random DNA, a Stop codon occurs by chance every ~21 codons (3 / 64).
  * An uninterrupted ORF of >= 100 amino acids (>= 300 bp) has P < 0.01 by chance!
  * Standard rule of thumb: ORFs >= 100 codons are flagged as candidate coding genes.
```

**Speaker Talking Points:**  
* Small ORFs (<50 codons) occur randomly throughout all 6 frames.
* Authentic protein-coding genes maintain long, open reading frames free of stop codons.

---

## Slide 7: Prokaryotic vs Eukaryotic Gene Architecture

```text
Topic: Why Gene Prediction Differs Fundamentally Across Domains

+--------------------+-------------------------+------------------------------+
| Feature            | Prokaryotes (Bacteria)  | Eukaryotes (Human / Yeast)   |
+--------------------+-------------------------+------------------------------+
| Coding Density     | High (~85-90% coding)   | Low (<2% coding in human)    |
| Introns            | ABSENT (Continuous CDS) | PRESENT (Interrupting exons) |
| Ribosome Binding   | Shine-Dalgarno (AGGAGG) | Kozak Consensus (gccRccAUGG) |
| Transcript Format  | Polycistronic (Operons) | Monocistronic (1 gene / mRNA)|
| ORF Finding Method | Direct 6-frame scanning | Ab initio HMMs (Augustus)    |
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* In bacteria, finding long ORFs immediately identifies genes!
* In humans, genes are fragmented into small exons (average 150 bp) separated
  by massive introns (thousands of bp); simple ORF finders completely fail!

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 21

* Genomes must be screened and masked with **RepeatMasker** before predictive analysis.
* Interspersed repeats (Alu, LINE-1) dominate the eukaryotic non-coding landscape.
* Double-stranded DNA possesses six conceptual reading frames (+1, +2, +3, -1, -2, -3).
* An ORF begins with `ATG` and ends with an in-frame stop (`TAA, TAG, TGA`).
* Next Lecture: Codon Usage Bias (RSCU, CAI) and Functional Sequence Signals
  (Promoters, Splice Sites, and CpG Islands).
```

