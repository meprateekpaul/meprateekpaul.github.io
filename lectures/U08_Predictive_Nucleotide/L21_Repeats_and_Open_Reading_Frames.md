# Lecture 21 — Repeats and Open Reading Frames

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 8:** Predictive Methods using Nucleotide Sequence  
**Syllabus Topic:** Introduction, Marking repetitive DNA, Database search  
**Primary Learning Outcome:** LO6 — Predict sequence-based features: identify Open Reading Frames (ORFs) across six frames, and classify and mask repetitive DNA.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Predictive Challenge of Raw DNA
================================================================================
Topic: Deciphering the Unannotated Tape

[Visual: A 100-kilobase string of raw A, C, G, T characters:
  Where are the genes? Where are the promoters? Where are the repetitive parasites?]

Speaker Bullets:
* Modern high-throughput sequencing produces terabases of raw genomic contigs.
* Experimental validation of every gene is impossible; we must predict functional
  elements computationally from primary DNA sequence alone.
* The first two steps in predictive genomics:
  1. Mask repetitive DNA elements.
  2. Map all possible Open Reading Frames (ORFs) across 6 reading frames.
```

```
================================================================================
SLIDE 2: The Eukaryotic Genome Landscape
================================================================================
Topic: Coding vs Non-Coding DNA

[Visual: Pie chart of the Human Genome:
  * Protein-coding exons: ONLY ~1.5%!
  * Introns: ~26%
  * Repetitive transposable elements: >45-50%!
  * Unique non-coding & heterochromatin: Balance]

Speaker Bullets:
* Less than 2% of the human genome encodes proteins!
* Nearly half of the human genome consists of repetitive DNA: molecular fossils
  and transposable elements that replicate within our chromosomes.
```

```
================================================================================
SLIDE 3: Classification of Repetitive DNA
================================================================================
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

Speaker Bullets:
* Tandem repeats expand via replication slippage; interspersed repeats expand via transposition.
```

```
================================================================================
SLIDE 4: Marking Repetitive DNA: RepeatMasker
================================================================================
Topic: Cleaning Genomes Before Analysis

[Visual: Raw Sequence -> RepeatMasker Engine (Screens against Dfam / RepBase)
         -> Masked Sequence (Repeats converted to 'N' or lowercase)]

Command:
  `RepeatMasker -species human -xsmall genomic_contig.fasta`

Speaker Bullets:
* If you run BLAST on an unmasked 50-kb human contig, an Alu element will trigger
  500,000 spurious hits, crashing your browser!
* **RepeatMasker** compares raw contigs against curated consensus repeat libraries
  (Dfam / RepBase) and masks them before gene finding.
```

```
================================================================================
SLIDE 5: Open Reading Frames (ORFs): The Six Reading Frames
================================================================================
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

Speaker Bullets:
* Any piece of double-stranded DNA can be conceptually translated in **six distinct frames**.
* A frameshift mutation of +1 or -1 completely alters the translated amino acid string.
```

```
================================================================================
SLIDE 6: What Defines an Authentic ORF?
================================================================================
Topic: Start Codons, Stop Codons, and Length Cutoffs

  Definition of an ORF:
  * Starts with an Initiation Codon: `ATG` (Methionine).
  * Followed by a series of triplet sense codons.
  * Ends with an in-frame Termination Codon: `TAA`, `TAG`, or `TGA`.

  Statistical Reality:
  * In random DNA, a Stop codon occurs by chance every ~21 codons (3 / 64).
  * An uninterrupted ORF of >= 100 amino acids (>= 300 bp) has P < 0.01 by chance!
  * Standard rule of thumb: ORFs >= 100 codons are flagged as candidate coding genes.

Speaker Bullets:
* Small ORFs (<50 codons) occur randomly throughout all 6 frames.
* Authentic protein-coding genes maintain long, open reading frames free of stop codons.
```

```
================================================================================
SLIDE 7: Prokaryotic vs Eukaryotic Gene Architecture
================================================================================
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

Speaker Bullets:
* In bacteria, finding long ORFs immediately identifies genes!
* In humans, genes are fragmented into small exons (average 150 bp) separated
  by massive introns (thousands of bp); simple ORF finders completely fail!
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 21

* Genomes must be screened and masked with **RepeatMasker** before predictive analysis.
* Interspersed repeats (Alu, LINE-1) dominate the eukaryotic non-coding landscape.
* Double-stranded DNA possesses six conceptual reading frames (+1, +2, +3, -1, -2, -3).
* An ORF begins with `ATG` and ends with an in-frame stop (`TAA, TAG, TGA`).
* Next Lecture: Codon Usage Bias (RSCU, CAI) and Functional Sequence Signals
  (Promoters, Splice Sites, and CpG Islands).
```

---

## Detailed Comprehensive Technical Notes

### 1. The Genomic Landscape: Why Prediction is Mandatory

The sequencing revolution has outpaced our capacity to experimentally validate gene function. In newly sequenced eukaryotic genomes, less than 2% of the nucleotide sequence directly codes for mature polypeptides. The remaining 98% comprises introns, regulatory promoters, structural heterochromatin, pseudogenes, and massive arrays of repetitive elements.

Before any gene-finding algorithm can predict exons or splice junctions, the raw genomic sequence must undergo two foundational computational processing steps:
1. **Repeat Identification and Masking.**
2. **Six-Frame Open Reading Frame (ORF) Mapping.**

---

### 2. Classification and Biology of Repetitive DNA

Repetitive DNA elements in eukaryotic genomes are classified into two broad mechanistic classes based on their genomic distribution:

```
                                  Repetitive DNA
                                        |
                     +------------------+------------------+
                     |                                     |
              Tandem Repeats                        Interspersed Repeats
         (Adjacent head-to-tail)                   (Transposable Elements)
                     |                                     |
        +------------+------------+           +------------+------------+
        |            |            |           |                         |
    Satellite   Minisatellite  Microsatellite Retrotransposons       DNA Transposons
   (Megabases)    (VNTRs)      (STRs: 1-6bp)   (Copy & Paste)        (Cut & Paste)
                                              |
                                     +--------+--------+
                                     |                 |
                                   LINEs             SINEs
                                (Autonomous)    (Non-autonomous)
                                (e.g. L1: 6kb)   (e.g. Alu: 300bp)
```

#### A. Tandem Repeats
Units of DNA sequence repeated immediately adjacent to one another in head-to-tail orientation:
- **Satellite DNA:** Very large arrays spanning hundreds of kilobases to megabases, typically localized at centromeres and telomeres. Example: human $\alpha$-satellite DNA (171-bp monomer repeat) essential for kinetochore assembly.
- **Minisatellites (VNTRs - Variable Number of Tandem Repeats):** Arrays of 10 to 100 bp repeat units spanning 1 to 20 kb. Historically utilized by Sir Alec Jeffreys in 1985 to invent DNA fingerprinting.
- **Microsatellites (STRs - Short Tandem Repeats):** Very short units of 1 to 6 base pairs (e.g., $(CA)_n$, $(GATA)_n$). Highly polymorphic across human populations due to DNA replication slippage. The FBI CODIS forensic database uses 20 standardized STR loci to establish human legal identity.

#### B. Interspersed Repeats (Transposable Elements)
Mobile genetic elements dispersed throughout the genome:
1. **SINEs (Short Interspersed Nuclear Elements):**  
   Non-autonomous retrotransposons of length 100 to 400 bp. They lack protein-coding capacity and parasitize the enzymatic machinery of LINEs to replicate.  
   *The Human Alu Element:* Derived from the 7SL RNA gene, an Alu element is $\approx 300\text{ bp}$ long containing an internal cleavage site for the *Alu*I restriction endonuclease. The human genome harbors over **1.2 million Alu copies**, accounting for $\approx 11\%$ of our entire nuclear DNA mass!
2. **LINEs (Long Interspersed Nuclear Elements):**  
   Autonomous retrotransposons of length 6 to 8 kb. They encode two functional open reading frames: an RNA-binding protein (ORF1) and a bifunctional protein possessing reverse transcriptase and endonuclease activities (ORF2). The dominant human family, **LINE-1 (L1)**, comprises $\approx 500,000$ copies ($\approx 17\%$ of the human genome).
3. **LTR Retrotransposons & Endogenous Retroviruses (HERVs):**  
   Remnants of ancient germline retroviral infections flanked by Long Terminal Repeats (LTRs).

---

### 3. Computational Repeat Masking: RepeatMasker

When an unmasked genomic contig containing an Alu or LINE element is submitted to BLAST or an *ab initio* gene finder:
- The repeat element triggers thousands of false-positive alignments against unrelated genes across the database.
- Gene-finding algorithms mistake repetitive open reading frames (e.g. LINE-1 reverse transcriptase) for host human genes.

To solve this, researchers pre-process raw contigs using **RepeatMasker** (Arian Smit, Robert Hubley, and Phil Green).

#### How RepeatMasker Operates:
1. Reads the input FASTA sequence.
2. Compares the sequence against **Dfam** (an open-access database of repetitive DNA families represented by Profile Hidden Markov Models) and **RepBase** (curated consensus repeats).
3. Identifies matching transposons, low-complexity regions, and simple repeats.
4. Generates a masked sequence:
   - **Hard Masking:** Overwrites repeat bases with `N` (e.g., `ATGCGNNNNNNNNNCGTA`).
   - **Soft Masking:** Converts repeat bases to lowercase (e.g., `ATGCGaaaaaaatttCGTA`).

---

### 4. Open Reading Frames (ORFs) and the Six Reading Frames

Because DNA is a double-stranded, antiparallel helical polymer, and the ribosome translates mRNA in non-overlapping triplet codons, any double-stranded genomic DNA fragment possesses **six potential reading frames**:

```
  5'-  A  T  G  G  T  G  C  A  C  C  T  G  A  C  T  C  C  T  -3'  (Forward Strand)
       \_____/  \_____/  \_____/  \_____/  \_____/  \_____/
       Frame +1: Begins at base 1 (Codons: ATG, GTG, CAC, CTG, ACT, CCT)
          \_____/  \_____/  \_____/  \_____/  \_____/
          Frame +2: Begins at base 2 (Codons: TGG, TGC, ACC, TGA [STOP!])
             \_____/  \_____/  \_____/  \_____/  \_____/
             Frame +3: Begins at base 3 (Codons: GGT, GCA, CCT, GAC, TCC)

  3'-  T  A  C  C  A  C  G  T  G  G  A  C  T  G  A  G  G  A  -5'  (Reverse Strand)
       <-----------------------------------------------------
  Transcribed antiparallel:
       Frame -1, Frame -2, Frame -3 (Read 5' to 3' along the reverse-complement strand)
```

#### Definition of a Formal ORF:
An **Open Reading Frame (ORF)** is a continuous stretch of DNA sequence that:
1. Initiates with a valid **Start Codon**: standardly `ATG` (encoding Methionine; occasionally `GTG` or `TTG` in prokaryotes).
2. Contains a contiguous run of **sense triplet codons** uninterrupted by stop signals.
3. Terminates at an in-frame **Stop Codon**: `TAA` (ochre), `TAG` (amber), or `TGA` (opal).

#### The Probability of Encountering a Random Stop Codon:
Assume a random DNA sequence where the four bases are present in equal proportions ($p_A = p_T = p_G = p_C = 0.25$).
The probability that any randomly selected triplet codon is one of the three standard stop codons ($TAA, TAG, TGA$) is:

$$P(\text{Stop}) = P(TAA) + P(TAG) + P(TGA) = 3 \times (0.25 \times 0.25 \times 0.25) = \frac{3}{64} \approx \mathbf{0.046875}$$

The expected distance between two stop codons in random non-coding DNA is:

$$\text{Expected Length} = \frac{1}{P(\text{Stop})} = \frac{64}{3} \approx \mathbf{21.3\text{ codons (approx 64 base pairs)}}$$

The probability that an unconstrained random non-coding sequence remains open for $L$ consecutive codons without hitting a stop codon is:

$$P(\text{No Stop for } L \text{ codons}) = \left( 1 - \frac{3}{64} \right)^L = (0.953125)^L$$

```
  ORF Length (L in codons)   Length in Base Pairs   Probability by Random Chance (P)
  -------------------------------------------------------------------------------------------------
  L = 20 codons              60 bp                  (0.9531)^20  ≈ 0.383  (38.3% - Frequent!)
  L = 50 codons              150 bp                 (0.9531)^50  ≈ 0.090  (9.0%  - Common)
  L = 100 codons             300 bp                 (0.9531)^100 ≈ 0.0082 (0.82% - Rare)
  L = 200 codons             600 bp                 (0.9531)^200 ≈ 0.000067 (0.0067% - Very Rare)
```

**Computational Significance:**  
Because the probability of an unconstrained random non-coding sequence maintaining an open frame for $\ge 100$ codons is less than $1\%$, bioinformatic tools (such as NCBI **ORFfinder** or EMBOSS **`getorf`**) set a standard minimum threshold of **$\ge 100$ amino acids ($\ge 300\text{ bp}$)** to filter out background statistical noise.

---

## Worked Example: 6-Frame Conceptual Translation

### Objective:
Given the following 24-nucleotide synthetic DNA fragment representing the $5'$ terminus of the human beta-globin coding region:

$$\text{Forward Strand: } 5'\text{- A T G G T G C A C C T G A C T C C T G A G G A G -3'}$$

1. Determine the reverse-complement strand ($5' \to 3'$).
2. Translate the first 6 codons of the Forward Strand in **Frame +1**.
3. Identify if any premature stop codons occur in **Frame +2**.

---

### Step 1: Generate the Reverse-Complement Strand
- Original $5' \to 3'$: `A T G G T G C A C C T G A C T C C T G A G G A G`
- Complementary $3' \to 5'$: `T A C C A C G T G G A C T G A G G A C T C C T C`
- Reverse to write $5' \to 3'$:  
  $$\text{Reverse-Complement: } 5'\text{- C T C C T C A G G A G T C A G G T G C A C C A T -3'}$$

---

### Step 2: Translate Forward Strand in Frame +1
Reading codons from base 1:

```
  Codon 1:  A T G  -->  Methionine (Met, M)   [START CODON]
  Codon 2:  G T G  -->  Valine (Val, V)
  Codon 3:  C A C  -->  Histidine (His, H)
  Codon 4:  C T G  -->  Leucine (Leu, L)
  Codon 5:  A C T  -->  Threonine (Thr, T)
  Codon 6:  C C T  -->  Proline (Pro, P)
  Codon 7:  G A G  -->  Glutamic Acid (Glu, E)
  Codon 8:  G A G  -->  Glutamic Acid (Glu, E)
```

**Frame +1 Translation:** `M - V - H - L - T - P - E - E`  
This matches the authentic wild-type human beta-globin polypeptide sequence (`NP_000509.1`).

---

### Step 3: Inspect Forward Strand in Frame +2
Reading codons starting from base 2:

```
  Base 1 'A' is skipped as an offset:
  Codon 1:  T G G  -->  Tryptophan (Trp, W)
  Codon 2:  T G C  -->  Cysteine (Cys, C)
  Codon 3:  A C C  -->  Threonine (Thr, T)
  Codon 4:  T G A  -->  *** STOP CODON (Opal) ***
```

**Frame +2 Translation:** `W - C - T - [STOP]`  
Notice that in Frame +2, an in-frame termination codon (`TGA`) appears at codon 4! Frame +2 is closed immediately after 3 residues, confirming it is an invalid, non-coding reading frame.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A forensic geneticist is analyzing Short Tandem Repeats (STRs) to match DNA from a crime scene, while a comparative genomicist is analyzing Alu elements to reconstruct primate evolution. Contrast the biological mechanisms that generate STRs versus Alu elements, and explain why both are classified as repetitive DNA.

**Model Answer:**
- **Biological Mechanisms:**
  - **STRs (Microsatellites):** Tandem repeats of 1 to 6 base pairs (e.g. $(GATA)_n$) that expand and contract due to **replication slippage** by DNA polymerase during lagging-strand synthesis.
  - **Alu Elements (SINEs):** Interspersed retrotransposons of $\approx 300\text{ bp}$ that replicate via **retrotransposition**: they are transcribed into RNA, reverse-transcribed into cDNA by LINE-encoded reverse transcriptase, and integrated into new chromosomal loci via target-primed reverse transcription.
- **Why both are repetitive DNA:** Both elements exist in thousands to millions of nearly identical copies across the nuclear genome rather than being unique, single-copy coding genes.

---

### Question 2
**Prompt:** Why does a naive six-frame ORF-finding program (such as NCBI ORFfinder) successfully predict complete, accurate protein sequences in bacterial genomes like *Escherichia coli*, but fails completely when run over human genomic DNA?

**Model Answer:**
- **In Bacteria (*E. coli*):** Genomes are compact ($\approx 88\%$ coding) and **lack spliceosomal introns**. Bacterial genes consist of uninterrupted, continuous coding sequences that span hundreds to thousands of base pairs. A simple 6-frame ORF scanner setting a threshold of $>100$ codons easily detects the full-length protein.
- **In Humans:** Eukaryotic genes are **discontinuous**, interrupted by extensive non-coding introns. An average human exon is only $\approx 150\text{ bp}$ long ($\approx 50\text{ codons}$). A simple ORF finder with a 100-codon cutoff will discard these real 50-codon exons as background noise, or will attempt to translate across the donor splice site into the adjacent intron, immediately hitting an intronic stop codon. Predicting eukaryotic genes requires sophisticated *ab initio* Hidden Markov Models (like Augustus) that model intron-exon splice signals.

---

### Question 3
**Prompt:** If a genomic DNA fragment contains 600 base pairs, what is the maximum possible number of amino acids that could be encoded by an unbroken ORF contained within this fragment?

**Model Answer:**
$$\text{Total Codons} = \frac{600\text{ bp}}{3\text{ bp/codon}} = 200\text{ codons}$$
Because an authentic completed ORF must terminate with a non-coding stop codon ($TAA, TAG, TGA$) that does not specify an amino acid:
$$\text{Maximum Amino Acids} = 200 - 1 = \mathbf{199\text{ amino acids}}$$
The maximum polypeptide length is 199 amino acid residues.
