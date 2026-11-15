---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 30 Slides: Synteny and Comparative Genomics"
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
# Lecture 30 — Synteny and Comparative Genomics
### Concepts of Bioinformatics (CBBI-501)
**Unit 11:** Comparative Genome Analysis  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Power of Comparative Genomics

```text
Topic: Understanding One Genome Through the Prism of Many

[Visual: Comparing whole chromosomes across 5 mammalian species:
  Conserved chromosomal blocks preserved across 100 million years of divergence!]
```

**Speaker Talking Points:**  
* Sequencing a single genome gives an unannotated parts list; comparing genomes
  reveals the operating manual of evolution.
* Foundational Axiom: **What is functional is conserved by natural selection;
  what is non-functional drifts and diverges.**
* Today's capstone: Synteny, chromosomal evolution, and the grand synthesis
  of our semester-long journey tracking Human Beta-Globin (*HBB*).

---

## Slide 2: Synteny: Conservation of Gene Order

```text
Topic: Collinearity Along Chromosomal Blocks

  Definitions:
  * Classical Synteny: Genes residing on the same physical chromosome.
  * Modern Operational Synteny (Collinearity):
    Conservation of the **linear physical order and transcriptional orientation**
    of homologous genes along a chromosomal segment across different species.

  Scale:
  * Microsynteny: Local collinearity across a small cluster of genes (e.g. globin cluster).
  * Macrosynteny: Large-scale conservation across whole chromosome arms.
```

**Speaker Talking Points:**  
* When gene order is preserved over 100 million years, it implies coordinated regulation!

---

## Slide 3: Chromosomal Evolution: Shuffling the Deck

```text
Topic: Mechanisms of Large-Scale Genomic Rearrangements

+-------------------------+---------------------------------------------------+
| Rearrangement Type      | Biological Mechanism & Example                    |
+-------------------------+---------------------------------------------------+
| **Inversion**           | A chromosomal segment flips 180 degrees           |
|                         | (Paracentric or Pericentric)                      |
| **Translocation**       | Non-homologous chromosomes exchange segments      |
| **Chromosome Fusion**   | End-to-end fusion of two chromosomes              |
|                         | (**Human Chr 2** fused from chimp 2A & 2B!)       |
| **Whole-Genome Dupl**   | 2R Hypothesis: Two rounds of WGD in vertebrates   |
+-------------------------+---------------------------------------------------+
```

**Speaker Talking Points:**  
* Synteny maps trace how modern mammalian karyotypes evolved from ancestral genomes.

---

## Slide 4: Whole-Genome Alignment Tools

```text
Topic: Aligning Gigabases Across Species

1. MUMmer (NUCmer / PROmer — Salzberg & Delcher):
   * Uses Suffix Trees to identify Maximal Unique Matches (MUMs).
   * Aligns whole bacterial and mammalian chromosomes in minutes.

2. Mauve (Darling et al.):
   * Identifies Locally Collinear Blocks (LCBs) across multiple rearranged genomes.

3. Circos Plots (Martin Krzywinski):
   * Circular ideograms displaying chromosomes around a circle with colored
     syntenic ribbons connecting homologous loci across species.
```

**Speaker Talking Points:**  
* Whole-genome alignment is the foundation for detecting evolutionary innovations.

---

## Slide 5: Finding the Unseen: Ultraconserved Non-Coding Elements

```text
Topic: Conserved Non-Coding Elements (CNEs)

[Visual: UCSC Genome Browser Conservation Track (PhastCons):
  Exons: High peaks
  Intergenic Desert: SUDDEN 500-bp SHARP PEAK (100% identity human vs chicken!)]

The Beta-Globin Locus Control Region (LCR):
* Located 50 kb upstream of the HBB cluster on Chr 11p15.4.
* Contains 5 DNase I hypersensitive sites (HS1 to HS5).
* Loops in 3D space to activate embryonic (epsilon), fetal (gamma), and adult (beta) globins!
```

**Speaker Talking Points:**  
* Comparative genomics revealed that non-coding regulatory elements can be
  more conserved than protein-coding exons!

---

## Slide 6: The Capstone Synthesis: HBB Across All 11 Units

```text
Topic: One Molecule, Complete Bioinformatics Mastery

[Visual: The 11-Unit Journey of Human Beta-Globin (HBB):
  U01: Central dogma tape      U05: Needleman-Wunsch & BLAST   U09: ProtParam & pI
  U02: Entrez NM_000518        U06: Globin family MSA          U10: PDB 1A3N 3D fold
  U03: ASN.1 Bioseq-set        U07: Globin phylogenetic tree   U11: 11p15.4 Synteny
  U04: GenBank flat file       U08: Codon bias & CpG island]
```

**Speaker Talking Points:**  
* You have witnessed how a single nucleotide transversion (GAG -> GTG / Glu6Val)
  ripples across every computational layer: from bits to 3D polymers to human pathology.

---

## Slide 7: The Bridge to Advanced Bioinformatics

```text
Topic: Your Curriculum Roadmap

  Semester II (CBBI-501: Concepts of Bioinformatics)
  Foundations: Data models, DP, BLAST, MSA, Trees, PDB, Genomes
             |
             +-----------------------+-----------------------+
             |                       |                       |
             v                       v                       v
      CBBI-504                CBBI-507                CBBI-508 / 604
  Genomics & Proteomics   Computational Analysis    Biological Databases &
  (RNA-seq, ChIP-seq)     of Biomolecules (MD, QM)  Phyloinformatics (Trees)
```

**Speaker Talking Points:**  
* Concepts of Bioinformatics is your foundational gateway.
* Everything you learned by hand this semester will be automated in Python and R.

---

## Slide 8: Course Conclusion & Final Takeaway

```text
Topic: Congratulations, Bioinformaticians!

* You now understand:
  1. Where biological data lives (INSDC, RefSeq, UniProt, PDB).
  2. How algorithms compute homology (Dynamic Programming, Karlin-Altschul, Trees).
  3. How sequence dictates 3D structure and physiological function.
* The genome is the ultimate software program written by nature:
  You now possess the computational tools to read, parse, and analyze it.
```

