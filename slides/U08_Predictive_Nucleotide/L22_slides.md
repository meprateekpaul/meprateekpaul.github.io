---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 22 Slides: Codon Usage Bias and Sites"
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
# Lecture 22 — Codon Usage Bias and Sites
### Concepts of Bioinformatics (CBBI-501)
**Unit 08:** Predictive Methods using Nucleotide Sequence  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Synonymous Choices Are Not Equal

```text
Topic: The Non-Random Nature of the Genetic Code

[Visual: 61 Sense Codons -> 20 Amino Acids:
  Leucine has 6 codons: TTA, TTG, CTT, CTC, CTA, CTG
  In human HBB: CTG is used 14 times; TTA is used ZERO times!]
```

**Speaker Talking Points:**  
* Because the genetic code is degenerate, multiple triplet codons specify the same amino acid.
* In natural genomes, synonymous codons do NOT appear with equal probability.
* Organisms exhibit strong, evolutionarily conserved preferences termed
  **Codon Usage Bias (CUB)**.

---

## Slide 2: Biological Forces Driving Codon Usage Bias

```text
Topic: Why Does a Cell Care Which Codon is Used?

1. Co-Adaptation with the tRNA Pool:
   * Cells do not produce all tRNA isoacceptors in equal abundance.
   * Preferred codons match the most abundant cytoplasmic tRNAs!
   * Translating "optimal codons" maximizes elongation speed and prevents ribosome stalling.

2. Translational Accuracy:
   * Highly conserved structural positions utilize optimal codons to minimize
     amino acid misincorporation errors during rapid protein synthesis.

3. Mutational & GC-Biased Gene Conversion:
   * Genomes with high GC-content (e.g. Actinobacteria) strongly prefer G/C at third positions.
```

**Speaker Talking Points:**  
* In highly expressed genes (like HBB and ribosomal proteins), codon bias is extreme.

---

## Slide 3: Quantifying Codon Bias: Relative Synonymous Codon Usage (RSCU)

```text
Topic: Sharp & Li's Mathematical Formulation (1986)

Formula:
  RSCU_ij = X_ij / [ (1 / k_i) * Sum_{j=1}^{k_i} X_ij ]

  * X_ij: Observed count of codon j for amino acid i
  * k_i:  Degeneracy of amino acid i (number of synonymous codons)
  * Denominator: Expected count if all synonymous codons were used equally

Interpretation:
  * RSCU = 1.0  --> No bias (used at random expectation)
  * RSCU > 1.0  --> POSITIVE BIAS (preferred codon)
  * RSCU < 1.0  --> NEGATIVE BIAS (disfavored / rare codon)
```

**Speaker Talking Points:**  
* RSCU normalizes codon frequencies independent of amino acid composition.

---

## Slide 4: Functional Promoter Elements

```text
Topic: Signaling the Start of Transcription

  Bacterial Promoters (Sigma-70):
    -35 Hexamer              17 +/- 1 bp spacer             -10 Hexamer (Pribnow)
    5'- T T G A C A --------------------------------------- T A T A A T -3'

  Eukaryotic Core Promoters:
    BRE                     TATA Box (-30 to -25)          Inr (Initiator)
    5'- S S R C G C C ----- T A T A W A W ----------------- Y Y A N W Y Y -3'
```

**Speaker Talking Points:**  
* Promoters are recognized by sequence-specific DNA-binding proteins.
* Consensus motifs represent the mathematical average of binding site affinities.

---

## Slide 5: Translation Initiation Context

```text
Topic: Guiding the Ribosome to the Authentic Start

1. Prokaryotes: The Shine-Dalgarno Sequence:
   * 5'- A G G A G G -3' located ~8 bp upstream of the ATG start codon.
   * Base-pairs directly with the 3' anti-Shine-Dalgarno sequence of 16S rRNA!

2. Eukaryotes: The Kozak Consensus Sequence (Marilyn Kozak, 1987):
   * 5'- (gcc)gccRcc A U G G -3'   (where R = Purine: A or G)
   * The Purine at position -3 and the Guanine at position +4 are CRITICAL.
   * Modulates ribosomal scanning efficiency in eukaryotic cytoplasm.
```

**Speaker Talking Points:**  
* Not all ATGs are start codons! The surrounding nucleotide context dictates whether
  the ribosome halts and initiates translation.

---

## Slide 6: Eukaryotic Splicing Signals: The Invariant GT-AG Rule

```text
Topic: Excising Introns with Single-Base Precision

[Visual: Eukaryotic Intron-Exon Boundary Architecture:
  EXON 1 ---------[ 5' Donor ]------------[ Branch Point ]---[ PPT ]---[ 3' Acceptor ]--------- EXON 2
  ... A G        | G T R A G T ...           C U R A Y         Y_n      N C A G | G ...
                 ^ (Invariant GT)               ^ (Invariant A)                 ^ (Invariant AG)]
```

**Speaker Talking Points:**  
* Canonical splicing strictly obeys Chambon's **GT-AG Rule**:
  - Introns begin with 5' GT (GU in RNA).
  - Introns terminate with 3' AG.
* The branch point Adenine residue attacks the 5' donor site to form the lariat intermediate!

---

## Slide 7: Epigenetic Beacons: CpG Islands

```text
Topic: Escaping the Methylation Mutational Trap

  The Mutational Trap:
  * Cytosines in CpG dinucleotides are methylated to 5-methylcytosine.
  * Spontaneous deamination of 5-mC yields THYMINE (C -> T mutation!).
  * Result: Over evolutionary time, CpG dinucleotides are depleted across 98% of the genome.

  CpG Islands:
  * Unmethylated promoter regions that escape deamination:
    1. Length >= 200 bp
    2. GC Content >= 50%
    3. Observed-to-Expected CpG ratio >= 0.60
```

**Speaker Talking Points:**  
* CpG islands mark the active promoters of over 60% of human genes (including HBB).

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 22

* Codon Usage Bias (RSCU, CAI) reflects tRNA abundance and translational kinetics.
* Functional sites are defined by consensus sequences:
  - Promoters: -10/-35 (bacteria) and TATA box (eukaryotes).
  - Ribosome binding: Shine-Dalgarno (bacteria) and Kozak (eukaryotes).
  - Splicing: Canonical 5' GT and 3' AG boundaries.
* CpG islands identify hypomethylated promoter oases in vertebrate genomes.
* Next Unit: Predictive Methods Using Protein Sequence — Physicochemical properties,
  ProtParam, and hydropathy plots.
```

