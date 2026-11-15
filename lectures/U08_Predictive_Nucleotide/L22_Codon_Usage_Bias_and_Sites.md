# Lecture 22 — Codon Usage Bias and Sites

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 8:** Predictive Methods using Nucleotide Sequence  
**Syllabus Topic:** Codon bias detection, detecting functional site in DNA  
**Primary Learning Outcome:** LO6 — Predict sequence-based features: calculate Codon Usage Bias (RSCU), and detect functional sequence signals (promoters, splice junctions, Kozak context, and CpG islands).

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Synonymous Choices Are Not Equal
================================================================================
Topic: The Non-Random Nature of the Genetic Code

[Visual: 61 Sense Codons -> 20 Amino Acids:
  Leucine has 6 codons: TTA, TTG, CTT, CTC, CTA, CTG
  In human HBB: CTG is used 14 times; TTA is used ZERO times!]

Speaker Bullets:
* Because the genetic code is degenerate, multiple triplet codons specify the same amino acid.
* In natural genomes, synonymous codons do NOT appear with equal probability.
* Organisms exhibit strong, evolutionarily conserved preferences termed
  **Codon Usage Bias (CUB)**.
```

```
================================================================================
SLIDE 2: Biological Forces Driving Codon Usage Bias
================================================================================
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

Speaker Bullets:
* In highly expressed genes (like HBB and ribosomal proteins), codon bias is extreme.
```

```
================================================================================
SLIDE 3: Quantifying Codon Bias: Relative Synonymous Codon Usage (RSCU)
================================================================================
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

Speaker Bullets:
* RSCU normalizes codon frequencies independent of amino acid composition.
```

```
================================================================================
SLIDE 4: Functional Promoter Elements
================================================================================
Topic: Signaling the Start of Transcription

  Bacterial Promoters (Sigma-70):
    -35 Hexamer              17 +/- 1 bp spacer             -10 Hexamer (Pribnow)
    5'- T T G A C A --------------------------------------- T A T A A T -3'

  Eukaryotic Core Promoters:
    BRE                     TATA Box (-30 to -25)          Inr (Initiator)
    5'- S S R C G C C ----- T A T A W A W ----------------- Y Y A N W Y Y -3'

Speaker Bullets:
* Promoters are recognized by sequence-specific DNA-binding proteins.
* Consensus motifs represent the mathematical average of binding site affinities.
```

```
================================================================================
SLIDE 5: Translation Initiation Context
================================================================================
Topic: Guiding the Ribosome to the Authentic Start

1. Prokaryotes: The Shine-Dalgarno Sequence:
   * 5'- A G G A G G -3' located ~8 bp upstream of the ATG start codon.
   * Base-pairs directly with the 3' anti-Shine-Dalgarno sequence of 16S rRNA!

2. Eukaryotes: The Kozak Consensus Sequence (Marilyn Kozak, 1987):
   * 5'- (gcc)gccRcc A U G G -3'   (where R = Purine: A or G)
   * The Purine at position -3 and the Guanine at position +4 are CRITICAL.
   * Modulates ribosomal scanning efficiency in eukaryotic cytoplasm.

Speaker Bullets:
* Not all ATGs are start codons! The surrounding nucleotide context dictates whether
  the ribosome halts and initiates translation.
```

```
================================================================================
SLIDE 6: Eukaryotic Splicing Signals: The Invariant GT-AG Rule
================================================================================
Topic: Excising Introns with Single-Base Precision

[Visual: Eukaryotic Intron-Exon Boundary Architecture:
  EXON 1 ---------[ 5' Donor ]------------[ Branch Point ]---[ PPT ]---[ 3' Acceptor ]--------- EXON 2
  ... A G        | G T R A G T ...           C U R A Y         Y_n      N C A G | G ...
                 ^ (Invariant GT)               ^ (Invariant A)                 ^ (Invariant AG)]

Speaker Bullets:
* Canonical splicing strictly obeys Chambon's **GT-AG Rule**:
  - Introns begin with 5' GT (GU in RNA).
  - Introns terminate with 3' AG.
* The branch point Adenine residue attacks the 5' donor site to form the lariat intermediate!
```

```
================================================================================
SLIDE 7: Epigenetic Beacons: CpG Islands
================================================================================
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

Speaker Bullets:
* CpG islands mark the active promoters of over 60% of human genes (including HBB).
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
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

---

## Detailed Comprehensive Technical Notes

### 1. Codon Usage Bias (CUB): Mechanisms and Dynamics

In the Standard Genetic Code, 61 triplet codons specify 20 amino acids. Aside from Methionine (`ATG`) and Tryptophan (`TGG`), all amino acids are encoded by between two and six synonymous codons.

**Codon Usage Bias (CUB)** is the non-random frequency of synonymous codon occurrence in protein-coding genes. Across taxa, genomes exhibit distinct codon signatures:
- In *Escherichia coli*, Leucine is encoded by `CTG` 52% of the time, while `CTA` is used less than 4% of the time.
- In *Saccharomyces cerevisiae*, Leucine is encoded by `TTA` 28% of the time, while `CTA` is used only 13% of the time.

```
  Biological Factor           Mechanistic Consequence
  -------------------------------------------------------------------------------------------------
  tRNA Pool Co-Adaptation     Cells produce high copy numbers of tRNAs cognate to preferred codons.
                              Translating preferred codons minimizes ribosomal pausing, preventing
                              ribosome collisions and abortive translation events.
  Translational Accuracy      In essential catalytic cores, natural selection enforces the use of
                              optimal codons with high cognate tRNA binding fidelity to prevent
                              deleterious missense misincorporation errors during elongation.
  mRNA Secondary Structure    Selection avoids synonymous codons that create stable RNA stem-loops
                              near the 5' transcription start site, ensuring unhindered ribosome entry.
  Recombinant Expression      Cloning a human gene into *E. coli* fails if the human cDNA contains codons
                              (e.g., `AGG`, `AGA` for Arg) whose cognate tRNAs are rare in bacteria,
                              triggering premature translation arrest (ribosome stalling).
```

---

### 2. Mathematical Metrics of Codon Bias

#### Relative Synonymous Codon Usage (RSCU)
Formulated by Paul Sharp, Kenneth Wolfe, and colleagues (1986), **RSCU** measures the observed frequency of a codon divided by its expected frequency under the assumption of equal synonymous codon usage:

$$\text{RSCU}_{ij} = \frac{X_{ij}}{\frac{1}{k_i} \sum_{j=1}^{k_i} X_{ij}}$$

where:
- $X_{ij}$: The observed count of the $j$-th codon for amino acid $i$.
- $k_i$: The degeneracy of amino acid $i$ ($k_i \in \{2, 3, 4, 6\}$).
- The denominator represents the average frequency of all synonymous codons for that amino acid.

```
  RSCU Value Range    Interpretation
  -------------------------------------------------------------------------------------------------
  RSCU = 1.0          Zero bias; codon is used at exactly the expected random frequency.
  RSCU > 1.0          Positive bias; codon is used MORE frequently than expected (preferred).
  RSCU < 1.0          Negative bias; codon is used LESS frequently than expected (disfavored / rare).
```

#### Codon Adaptation Index (CAI)
The **Codon Adaptation Index (CAI)** (Sharp & Li, 1987) measures the directional adaptiveness of a gene's entire sequence relative to a reference set of highly expressed genes:
- For each codon $k$, calculate relative adaptiveness: $w_k = \frac{\text{RSCU}_k}{\text{RSCU}_{\max}}$.
- The CAI of a gene of length $L$ codons is the geometric mean:
  $$\text{CAI} = \exp\left( \frac{1}{L} \sum_{k=1}^{L} \ln(w_k) \right) = \left( \prod_{k=1}^{L} w_k \right)^{1/L}$$
CAI ranges from $0$ to $1.0$, where values approaching $1.0$ indicate that a gene utilizes exclusively the most optimal codons in that organism.

---

### 3. Detecting Functional Sequence Sites in DNA

Genomic DNA contains precise, sequence-specific docking signals recognized by cellular enzymes:

#### A. Promoters
- **Bacterial $\sigma^{70}$ Promoters:** Characterized by two conserved hexamers separated by an optimal spacer of $17 \pm 1\text{ bp}$:
  - **$-35$ Hexamer:** `5'-TTGACA-3'` (initial binding site for the sigma factor).
  - **$-10$ Hexamer (Pribnow Box):** `5'-TATAAT-3'` (region of DNA duplex melting / open complex formation).
- **Eukaryotic RNA Polymerase II Promoters:**
  - **TATA Box:** Located at $-30$ to $-25\text{ bp}$ relative to the transcription start site ($+1$). Consensus: `5'-TATAWAW-3'` (where $W = A/T$). Bound by TATA-Binding Protein (TBP).
  - **Initiator (Inr):** Encompasses the $+1$ start site. Consensus: `5'-YYANWYY-3'` (where $Y = C/T, N = \text{any}, W = A/T$).

#### B. Translation Initiation Signals
- **Bacterial Shine-Dalgarno (SD) Sequence:** Consensus `5'-AGGAGG-3'`, located 6 to 10 base pairs upstream of the initiating `AUG`. It forms antiparallel Watson-Crick base pairs with the $3'$ terminal sequence of the $16S\text{ rRNA}$ (`3'-UCCUCC-5'`) within the 30S ribosomal subunit.
- **Eukaryotic Kozak Consensus (Marilyn Kozak, 1987):** Eukaryotic ribosomes do not bind internal sequences; the 40S small subunit binds the $5'$ 7-methylguanosine cap and scans downstream ($5' \to 3'$) until encountering an optimal initiation context:
  $$\text{Kozak Motif: } 5'\text{- (gcc)gccRcc A U G G -3'}$$
  The **Purine at position $-3$** (typically an $A$) and the **Guanine at position $+4$** (immediately following the $AUG$) are thermodynamically critical for ribosomal recognition.

#### C. Pre-mRNA Splicing Signals
Eukaryotic spliceosomes excise introns following precise sequence rules:
- **$5'$ Donor Splice Site:** Consists of the canonical dinucleotide **`GT`** (in DNA) or **`GU`** (in RNA) at the $5'$ end of the intron. Consensus: `5'-...AG | GTRAGT...-3'`.
- **$3'$ Acceptor Splice Site:** Consists of the canonical dinucleotide **`AG`** at the $3'$ end of the intron. Consensus: `5'-...Y_n NCAG | G...-3'`.
- **Branch Point Sequence:** Located 20 to 50 nucleotides upstream of the $3'$ acceptor site. Consensus: `5'-CURAY-3'` (where $R = A/G, Y = C/T$). The **invariant Adenine ($A$)** provides the $2'\text{-OH}$ group that performs the nucleophilic attack on the $5'$ splice junction, forming the covalently closed lariat loop.
- **Polypyrimidine Tract (PPT):** A run of 15 to 20 consecutive pyrimidines ($C$ and $T$) between the branch point and $3'$ acceptor site, recognized by U2AF65.

---

### 4. Epigenetic Beacons: CpG Islands

In vertebrate genomes, the dinucleotide pair $5'\text{-CpG-}3'$ occurs at a frequency four to five times lower than mathematically expected ($Obs/Exp \approx 0.20$).

#### The Biochemical Mechanism of CpG Depletion:
1. DNA methyltransferases methylate the 5-position of Cytosine in CpG dinucleotides to form **5-methylcytosine ($5\text{-mC}$)**.
2. Spontaneous hydrolytic deamination of unmethylated Cytosine produces Uracil ($U$), an unnatural base in DNA that is instantly recognized and excised by Uracil-DNA Glycosylase (UDG), restoring Cytosine.
3. However, spontaneous deamination of **5-methylcytosine** directly yields **Thymine ($T$)**:
   $$\text{5-methylcytosine} \xrightarrow{\text{Spontaneous Deamination}} \text{Thymine}$$
4. The resulting $T:G$ mismatch is poorly repaired by mismatch repair pathways, frequently mutating the original $C \to T$. Over hundreds of millions of years of vertebrate evolution, methylated CpGs have been irreversibly depleted.

#### Definition of a CpG Island (Gardiner-Garden & Frommer, 1987):
Regions of genomic DNA that remain unmethylated in the germline escape deamination. These regions maintain their ancestral density of CpG dinucleotides:
- **Length:** $\ge 200\text{ base pairs}$ (modern criteria often use $\ge 500\text{ bp}$).
- **GC Content:** $\ge 50\%$.
- **Observed-to-Expected CpG Ratio:** $\ge 0.60$, calculated as:

$$\text{Obs/Exp CpG} = \frac{\text{Count}(\text{CpG}) \times N}{\text{Count}(C) \times \text{Count}(G)}$$

where $N$ is the total length of the sequence window. CpG islands overlap the transcription start sites and promoters of $>60\%$ of human genes (including the human beta-globin cluster on 11p15.4).

---

## Worked Example: Calculating RSCU and CpG Island Ratios by Hand

### Part 1: Hand Calculation of RSCU for Alanine Codons
In a newly sequenced bacterial gene, the amino acid Alanine occurs a total of 100 times across four synonymous codons (`GCA`, `GCC`, `GCG`, `GCT`):
- Observed counts:
  - `GCA`: 10
  - `GCC`: 60
  - `GCG`: 20
  - `GCT`: 10
  - Total Alanine count: $10 + 60 + 20 + 10 = \mathbf{100}$.

#### Step 1: Determine Degeneracy ($k_i$)
Alanine has 4 synonymous codons: $k_i = 4$.

#### Step 2: Calculate Expected Count per Codon
$$\text{Expected Count} = \frac{\text{Total Alanine Count}}{k_i} = \frac{100}{4} = \mathbf{25.0}$$

#### Step 3: Compute RSCU for Each Codon
$$\text{RSCU} = \frac{\text{Observed Count}}{\text{Expected Count}} = \frac{\text{Observed}}{25.0}$$

```
  Codon    Observed Count    Expected Count    RSCU Calculation    RSCU Value    Bias Direction
  -------------------------------------------------------------------------------------------------
  GCA      10                25.0              10 / 25.0           0.40          Negative (Rare)
  GCC      60                25.0              60 / 25.0           2.40          STRONG POSITIVE
  GCG      20                25.0              20 / 25.0           0.80          Slight Negative
  GCT      10                25.0              10 / 25.0           0.40          Negative (Rare)
  -------------------------------------------------------------------------------------------------
  Sum:     100                                                     4.00 (Exactly equals k_i!)
```
`GCC` exhibits extreme positive codon usage bias ($\text{RSCU} = 2.40$).

---

### Part 2: Evaluating a CpG Island
A genomic DNA window of length $N = 200\text{ bp}$ contains:
- Cytosine ($C$) count: $60$
- Guanine ($G$) count: $60$
- Dinucleotide `CpG` count: $24$

Does this region qualify as a CpG island under the Gardiner-Garden & Frommer criteria?

#### Criterion 1: Sequence Length
- Length $= 200\text{ bp} \ge 200\text{ bp} \implies$ **PASSES (True)**

#### Criterion 2: GC Content Percentage
$$\text{GC Content} = \frac{\text{Count}(G) + \text{Count}(C)}{N} \times 100\% = \frac{60 + 60}{200} \times 100\% = \frac{120}{200} \times 100\% = \mathbf{60.0\%}$$
- Since $60.0\% \ge 50\% \implies$ **PASSES (True)**

#### Criterion 3: Observed-to-Expected CpG Ratio
$$\text{Obs/Exp CpG} = \frac{\text{Count}(\text{CpG}) \times N}{\text{Count}(C) \times \text{Count}(G)}$$
Substitute values:
$$\text{Obs/Exp CpG} = \frac{24 \times 200}{60 \times 60} = \frac{4800}{3600} \approx \mathbf{1.33}$$
- Since $1.33 \ge 0.60 \implies$ **PASSES (True)**

**Conclusion:**  
All three quantitative criteria are met ($N \ge 200$, $\text{GC} = 60\% \ge 50\%$, $\text{Obs/Exp} = 1.33 \ge 0.60$). This sequence represents an authentic, hypomethylated **CpG Island**, indicative of an active promoter.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A biotechnology company synthesizes a recombinant human erythropoietin gene for expression in Chinese Hamster Ovary (CHO) cells. They observe that the native human cDNA has an RSCU value of $0.25$ for three consecutive Arginine codons (`CGA`). How will these codons affect protein translation yield, and what computational technique should be used before gene synthesis?

**Model Answer:**
- **Effect on translation yield:** An RSCU of $0.25$ indicates rare, disfavored codons. In CHO cells, tRNAs cognate to `CGA` are present in extremely low abundance. When the ribosome encounters three consecutive `CGA` triplets, it pauses (ribosome stalling), leading to ribosomal dissociation, premature termination, truncated peptides, and dramatically reduced recombinant protein yield.
- **Computational Technique:** The company must perform **Codon Optimization**. Bioinformatic software replaces the rare `CGA` codons with synonymous codons preferred by CHO cells (such as `CGC` or `CGT`, which have high RSCU values in rodents) without altering the translated amino acid sequence.

---

### Question 2
**Prompt:** In eukaryotic pre-mRNA splicing, what biochemical catastrophe occurs if a point mutation alters the invariant $5'$ splice donor dinucleotide from `GT` to `AT`?

**Model Answer:**
The canonical $5'$ donor dinucleotide `GT` (`GU` in RNA) is biochemically essential because it forms base pairs with the U1 small nuclear RNA (snRNA) within the spliceosome. If mutated to `AT`:
1. The spliceosome fails to recognize the authentic donor site.
2. The entire downstream intron may be retained in the mature mRNA (intron retention), introducing in-frame premature stop codons that trigger nonsense-mediated mRNA decay.
3. Alternatively, the spliceosome will search for and activate a cryptic splice donor site upstream or downstream, causing aberrant exon truncation or inclusion of pseudo-exons that frameshifts the coding sequence.

---

### Question 3
**Prompt:** Why is an unmethylated CpG dinucleotide evolutionarily stable, while a methylated CpG dinucleotide is prone to rapid mutational loss in vertebrate genomes?

**Model Answer:**
- **Unmethylated Cytosine** spontaneously deaminates to **Uracil ($U$)**. Because Uracil is an unnatural base in DNA, cellular Uracil-DNA Glycosylase (UDG) immediately recognizes the error, excises Uracil, and restores the original Cytosine, preserving the CpG dinucleotide.
- **Methylated Cytosine (5-methylcytosine)** spontaneously deaminates directly into **Thymine ($T$)**, a standard, natural DNA base. The resulting $T:G$ mismatch is recognized inefficiently by DNA repair machinery, leading to permanent $C \to T$ transitional fixation. Over evolutionary time, methylated CpGs are lost, leaving unmethylated promoter CpG islands as protected relics.
