# Lecture 15 — BLAST Artifacts and PSSMs

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 5:** Sequence Alignment and Database Searching  
**Syllabus Topic:** Database searching Artifacts, Position Specific Scoring Matrices  
**Primary Learning Outcome:** LO3, LO4 — Interpret BLAST output critically, recognize low-complexity search artifacts, and construct PSSMs for PSI-BLAST.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Dark Side of Sequence Searching
================================================================================
Topic: When High Scores Do Not Mean Homology

[Visual: A massive BLAST hit table with 500 hits having E = 10^-80...
         all aligning to a 40-residue tract of pure Proline repeats (Poly-Pro)!]

Speaker Bullets:
* A statistically significant E-value does not automatically prove common ancestry.
* Search artifacts (low-complexity regions, compositional bias, coiled-coils)
  generate false-positive alignments that corrupt biological interpretations.
* A trained bioinformatician must inspect alignments critically, mask artifacts,
  and know when to deploy profile-based models (PSSMs).
```

```
================================================================================
SLIDE 2: Low-Complexity Regions and Simple Repeats
================================================================================
Topic: The Anatomy of Sequence Bias

Examples of Low-Complexity Sequences:
* Homopolymeric tracts: `AAAAAAAAAAAA` (Poly-A) or `QQQQQQQQQQQQ` (Huntingtin Poly-Q)
* Short tandem repeats: `(CA)_n` or `(GGC)_n`
* Compositionally biased regions: Collagen triple-helix `(Gly-Pro-Hyp)_n`
* Charge clusters: Poly-basic tracts `KKKKRRRRKKR`

Speaker Bullets:
* These regions did not evolve via traditional point-mutation descent from a common ancestor;
  they expand via replication slippage.
* Two completely unrelated proteins containing Poly-Q tracts will align with astronomical
  scores simply because Glutamine-Glutamine matches score positively!
```

```
================================================================================
SLIDE 3: Masking Algorithms: SEG and DUST
================================================================================
Topic: Filtering Entropy Deficits

  The SEG Algorithm (Wootton & Federhen, 1993):
  * Scans proteins using a sliding window (length 12) measuring **Shannon Entropy** (H):
    H = - Sum [ p_i * log_2(p_i) ]
  * Typical globular proteins: H ≈ 3.5 to 4.2 bits.
  * Low-complexity repeats: H drops below threshold (e.g. H < 2.2 bits).
  * Flagged segments are filtered before seed generation!

  The DUST Algorithm:
  * Masks low-complexity trinucleotide repeats in DNA sequences.

Speaker Bullets:
* SEG filters the query before BLAST generates neighborhood words.
```

```
================================================================================
SLIDE 4: Hard Masking vs Soft Masking
================================================================================
Topic: Choosing the Filtering Strategy

+--------------------+-------------------------+------------------------------+
| Masking Mode       | Visual Representation   | Algorithmic Behavior         |
+--------------------+-------------------------+------------------------------+
| **Hard Masking**   | `VHLTPEXXXXXXXXAHLD`    | Replaces low-complexity with |
|                    |                         | 'X' (or 'N'). Seeds and      |
|                    |                         | extensions NEVER enter here. |
| **Soft Masking**   | `VHLTPEqqqqqqqqAHLD`    | Replaces with lowercase text.|
|                    |                         | Seeds CANNOT start in repeats|
|                    |                         | but extensions MAY pass thru.|
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* Hard masking completely blinds BLAST to those coordinates.
* Soft masking (NCBI default) is superior: it prevents spurious seed triggering
  while permitting valid extensions that originate in authentic flanking sequence.
```

```
================================================================================
SLIDE 5: The Limitation of Standard Matrices (Context-Blindness)
================================================================================
Topic: Why BLOSUM62 Reaches a Plateau

[Visual: Two Leucine residues in human beta-globin:
  Leu68 (Deep in hydrophobic haem pocket: strictly invariant across all vertebrates)
  Leu3  (On flexible, solvent-exposed N-terminus: mutates freely to Val, Ala, Ile)
  BLOSUM62 treats both Leucines IDENTICALLY, awarding +4 for a match at both sites!]

Speaker Bullets:
* Standard matrices have no memory of position: a match scores the same everywhere.
* In reality, certain positions in an active site tolerate ZERO mutations, while loop
  positions tolerate almost anything.
* Solution: **Position-Specific Scoring Matrices (PSSMs)**.
```

```
================================================================================
SLIDE 6: The Architecture of a PSSM
================================================================================
Topic: Custom Scoring Vectors per Alignment Column

  Multiple Alignment Block (Columns 1 to L):
  Pos 1:  H   H   H   H   H   --> 100% His (Coordination site) -> High score for H only!
  Pos 2:  V   I   L   V   M   --> Hydrophobic core -> Scores for V, I, L, M all positive
  Pos 3:  A   G   S   T   P   --> Flexible loop -> Broad, permissive scores

  PSSM Structure:
  An (L x 20) matrix where EVERY position has its own unique 20-amino acid scoring column!

Speaker Bullets:
* A PSSM captures the unique evolutionary conservation profile of a protein family.
```

```
================================================================================
SLIDE 7: PSI-BLAST: Position-Specific Iterated BLAST
================================================================================
Topic: The Iterative Homology Machine (Altschul et al., 1997)

  Round 1: Standard BLASTP using BLOSUM62 against database.
           |
           v Collect all hits meeting inclusion threshold (E <= 0.005)
  Round 2: Build multiple alignment of hits -> Construct PSSM.
           |
           v Search database AGAIN using the PSSM! (Catches distant homologs)
  Round 3: Add new hits -> Refine PSSM -> Search database again...
           |
           v Repeat until CONVERGENCE (no new sequences found).

Speaker Bullets:
* PSI-BLAST detects distant evolutionary relationships in the "Twilight Zone" (20-30% id).
```

```
================================================================================
SLIDE 8: The Fatal Trap: Profile Drift
================================================================================
Topic: When a Single Impostor Corrupts the Search

[Visual: Contamination cascading across iterations:
  Round 1: Globin query pulls in 1 spurious coiled-coil protein (e.g. Myosin).
  Round 2: PSSM incorporates coiled-coil heptad repeat bias.
  Round 3: PSSM pulls in 2,000 kinesins, myosins, and keratins!
  Result: The globin profile is completely destroyed (Profile Drift / Corruption).]

Speaker Bullets:
* Never run PSI-BLAST unattended!
* Set strict inclusion thresholds ($E \le 10^{-4}$) and verify hits between rounds.
```

---

## Detailed Comprehensive Technical Notes

### 1. Database Searching Artifacts

When interpreting BLAST results, bioinformaticians frequently encounter hits with extremely low expectation values ($E < 10^{-20}$) that do not reflect common ancestry. These represent **search artifacts**:

#### A. Low-Complexity Regions (LCRs)
Segments of protein or nucleic acid sequence dominated by a single residue or short periodic repeat (e.g., poly-Glutamine tracts in transcription factors, Glycine-rich loops, or poly-A tracts in RNA). Because dynamic programming awards positive scores for identical residue pairs, two unrelated proteins that happen to contain low-complexity tracts align with massive scores.

#### B. Coiled-Coil Domains
Coiled-coils consist of characteristic **heptad repeats** $(a-b-c-d-e-f-g)_n$, where positions $a$ and $d$ are apolar hydrophobic residues (Leu, Ile, Val) and positions $e$ and $g$ are charged residues (Glu, Lys, Arg). Because thousands of structurally unrelated structural proteins (myosins, kinesins, keratins, viral fusion glycoproteins) share this exact heptad periodicity, BLAST will falsely align them, producing strong false-positive signals.

#### C. Vector, Linker, and Chimeric Contamination
In primary repositories (GenBank/EST), uncurated sequences occasionally contain cloning vector linkers (such as bacteriophage M13 or plasmid pUC19 sequences) deposited alongside the insert. Querying a sequence containing a cloning linker against GenBank returns thousands of completely unrelated organisms that share the identical cloning vector.

---

### 2. Sequence Masking: The SEG Algorithm

To prevent low-complexity artifacts from triggering spurious alignments, NCBI tools deploy filtering algorithms prior to word generation. For proteins, the standard engine is **SEG** (John Wootton and Scott Federhen, 1993).

#### The Mathematical Foundation of SEG:
SEG calculates the **Shannon Information Entropy** ($H$) within a sliding window of length $W$ (default $W = 12$ for proteins):

$$H = - \sum_{i=1}^{K} p_i \log_2(p_i)$$

where $K \le 20$ is the number of distinct amino acid types observed in the window, and $p_i = \frac{n_i}{W}$ is the relative frequency of amino acid $i$.
- **Maximum Entropy:** If all 20 amino acids are equally represented, $H_{\max} = \log_2(20) \approx \mathbf{4.32\text{ bits}}$. Typical globular proteins have an entropy between $3.2$ and $4.0\text{ bits}$.
- **Zero Entropy:** For a pure homopolymer (e.g. $Q_{12}$), $p_Q = 1 \implies H = - (1 \cdot \log_2(1)) = \mathbf{0\text{ bits}}$.

SEG applies two thresholds: a trigger threshold $K_1$ and an extension threshold $K_2$. If the local entropy drops below the cutoff (e.g., $H < 2.2\text{ bits}$), that window is demarcated as low complexity.

#### Hard Masking vs Soft Masking:
- **Hard Masking (`-seg yes` in legacy BLAST):** Replaces all low-complexity residues with the ambiguity character `X`. BLAST ignores `X` completely during word seeding and extension. *Disadvantage:* Truncates alignments that legitimately extend into or across short repetitive motifs.
- **Soft Masking (`-soft_masking true` in modern BLAST+):** Replaces low-complexity residues with **lowercase characters** (e.g., `acg...` or `vhl...`). The BLAST engine forbids the DFA scanner from creating neighborhood words from lowercase letters; however, once an alignment is initiated from an authentic high-complexity seed in flanking sequence, the extension algorithm is permitted to extend through the lowercase region.

---

### 3. Position-Specific Scoring Matrices (PSSMs)

A fundamental limitation of pairwise alignment matrices like BLOSUM62 is that they are **position-independent**. In human beta-globin:
- Histidine 93 (the proximal His that coordinates the haem iron) is invariant across all functional globins; mutating His93 destroys oxygen transport.
- Histidine 2 (on the solvent-exposed flexible N-terminal tail) can mutate to Valine, Glutamine, or Alanine with virtually zero impact on physiological function.
Yet, BLOSUM62 awards $+8$ for a match to His at both positions!

A **Position-Specific Scoring Matrix (PSSM)** (or profile) solves this by constructing an $L \times 20$ table for a sequence of length $L$, assigning a unique, tailored log-odds score to every amino acid at each specific position $i$.

---

### 4. Mathematical Construction of a PSSM

Constructing a PSSM from an ungapped multiple sequence alignment of $N$ sequences involves four mathematical steps:

```
  Step 1: Raw Observed Counts
          For each position i (1 to L) and amino acid a (1 to 20), count occurrences c_ia.
             |
             v
  Step 2: Pseudocount Addition (Dirichlet Priors or Laplace's Rule)
          Unobserved amino acids cannot have zero probability (log(0) is undefined!).
          Add background pseudocounts to yield estimated probability q_ia:
          q_ia = (c_ia + beta * p_a) / (N + beta)
             |
             v
  Step 3: Log-Odds Scoring Ratio
          Calculate the position-specific score against background frequency p_a:
          M_ia = (1 / lambda) * log_2 [ q_ia / p_a ]
```

---

### 5. PSI-BLAST (Position-Specific Iterated BLAST)

Introduced by Stephen Altschul, Thomas Madden, Alejandro Schäffer, and colleagues in 1997, **PSI-BLAST** provides sensitivity up to 300% greater than standard BLASTP, enabling the detection of ancient evolutionary homologs sharing less than 25% sequence identity ("the Twilight Zone").

#### The PSI-BLAST Iterative Workflow:
1. **Initial Search:** Run standard BLASTP using the query sequence and BLOSUM62 against the target database.
2. **Hit Collection:** Filter results using an **inclusion threshold** (typically $E \le 0.005$). All hits meeting this threshold are aligned to the query.
3. **Profile Generation:** Construct a multiple alignment from the valid hits, calculate position-specific frequencies, add pseudocounts, and compile an authoritative PSSM.
4. **Iterative Search:** Re-search the database using the newly constructed PSSM instead of BLOSUM62. The PSSM searches for sequences that match the *evolutionary conservation profile* of the entire protein family.
5. **Convergence:** Collect new hits, update the PSSM, and repeat until no new sequences achieve an E-value below the threshold (the search is said to have **converged**).

#### The Fatal Trap: Profile Drift (Profile Corruption)
The primary danger in PSI-BLAST is **Profile Drift**:
- If a single non-homologous sequence (e.g. an unmasked coiled-coil protein, or an unrelated protein that matches a single flexible loop) achieves an E-value of $0.004$, it slips into the multiple alignment in Iteration 1.
- In Iteration 2, the PSSM calculates weights incorporating the non-homologous residues of the interloper.
- In Iteration 3, the corrupted PSSM begins searching for the interloper's family, pulling in hundreds of irrelevant sequences. Within two iterations, the globin search is completely overrun by myosins or collagens.
- **Prevention:** Always inspect hits manually between rounds, enforce conservative inclusion thresholds ($E \le 10^{-4}$), and use soft-masking.

---

## Worked Example: Calculating a PSSM Column by Hand

### Problem:
Consider an ungapped multiple sequence alignment of $N = 5$ homologous globin peptides at a conserved 3-residue motif coordinating a hydrophobic interior:

```
  Sequence 1:   V   H   L
  Sequence 2:   V   H   L
  Sequence 3:   I   H   M
  Sequence 4:   V   H   I
  Sequence 5:   L   H   L
```

Calculate the PSSM log-odds scores for **Position 2** (the central Histidine position) for two candidate residues: **Histidine ($H$)** and **Alanine ($A$)**.

### Background Parameters:
- Total sequences in alignment: $N = 5$
- Background frequency of Histidine: $p_H = 0.05$ (5%)
- Background frequency of Alanine: $p_A = 0.10$ (10%)
- Pseudocount weight parameter: $\beta = 1.0$ (Laplace-style pseudocounts)
- Scaling factor: $\lambda = 1.0$ (scores reported in bits)

---

### Step 1: Count Raw Residues at Position 2
Examining column 2 across all 5 sequences:
- All 5 sequences have **Histidine ($H$)**: $c_{2, H} = 5$.
- Alanine ($A$) is not observed: $c_{2, A} = 0$.

---

### Step 2: Compute Estimated Target Probabilities ($q_{2, a}$) with Pseudocounts

Formula:
$$q_{2, a} = \frac{c_{2, a} + \beta \cdot p_a}{N + \beta}$$

Here, the denominator is $N + \beta = 5 + 1.0 = \mathbf{6.0}$.

1. **For Histidine ($H$):**
   $$q_{2, H} = \frac{5 + (1.0 \times 0.05)}{6.0} = \frac{5 + 0.05}{6.0} = \frac{5.05}{6.0} \approx \mathbf{0.8417}$$

2. **For Alanine ($A$):**
   $$q_{2, A} = \frac{0 + (1.0 \times 0.10)}{6.0} = \frac{0.10}{6.0} \approx \mathbf{0.0167}$$

---

### Step 3: Compute Log-Odds PSSM Scores ($M_{2, a}$)

Formula:
$$M_{2, a} = \log_2 \left( \frac{q_{2, a}}{p_a} \right)$$

1. **Score for Histidine at Position 2:**
   $$\text{Ratio} = \frac{q_{2, H}}{p_H} = \frac{0.8417}{0.05} = 16.834$$
   $$M_{2, H} = \log_2(16.834) \approx \mathbf{+4.07\text{ bits}}$$

2. **Score for Alanine at Position 2:**
   $$\text{Ratio} = \frac{q_{2, A}}{p_A} = \frac{0.0167}{0.10} = 0.167$$
   $$M_{2, A} = \log_2(0.167) \approx \mathbf{-2.58\text{ bits}}$$

### Interpretation:
In this PSSM, encountering a Histidine at position 2 is awarded a massive positive bonus of **$+4.07\text{ bits}$**, while encountering an unobserved Alanine incurs a penalty of **$-2.58\text{ bits}$**. If this PSSM is used in PSI-BLAST, any sequence lacking Histidine at position 2 will suffer a severe score reduction.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A researcher runs a BLASTP search for a human zinc-finger transcription factor against the NCBI non-redundant database and observes that the top 50 hits all have E-values $< 10^{-40}$, but all 50 align exclusively to a C-terminal tract consisting of 35 consecutive Proline and Glycine residues. 
1. What biological artifact has occurred?  
2. What concrete setting in BLAST should the researcher enable to eliminate this artifact?

**Model Answer:**
1. **Biological Artifact:** A **low-complexity sequence artifact** (compositional bias). Proline- and Glycine-rich tracts expand via replication slippage and align with non-homologous proline/glycine-rich structural proteins (such as collagen or salivary proteins) purely through positive residue identity matches, generating false-positive E-values.
2. **Corrective Action:** The researcher must enable **filtering/masking** (specifically running the **SEG algorithm** with soft masking: `-soft_masking true` or `-seg yes`), which will mask the low-complexity proline/glycine tract and force BLAST to seed alignments strictly from the biologically meaningful zinc-finger domain.

---

### Question 2
**Prompt:** Why are pseudocounts mathematically mandatory when calculating a Position-Specific Scoring Matrix (PSSM) from a multiple sequence alignment? What fatal error occurs if pseudocounts are omitted?

**Model Answer:**
- In an alignment of a finite number of sequences (e.g. $N = 10$), many of the 20 standard amino acids will never be observed at a given position ($c_{ia} = 0$).
- If raw frequencies are used without pseudocounts, the target probability is calculated as zero ($q_{ia} = 0$).
- In the log-odds formula, $M_{ia} = \log_2(q_{ia} / p_a) = \log_2(0)$, which is **mathematically undefined ($-\infty$)**.
- Pseudocounts incorporate prior background knowledge, ensuring that every amino acid retains a small, non-zero probability of occurrence, allowing valid log-odds scores to be computed without division-by-zero or logarithm-of-zero errors.

---

### Question 3
**Prompt:** Define the phenomenon of **"Profile Drift"** in PSI-BLAST. State two operational precautions a bioinformatician should take to prevent profile drift from ruining a multi-iteration search.

**Model Answer:**
- **Profile Drift:** The progressive corruption of a PSSM across iterative searches caused when a non-homologous false-positive sequence passes the inclusion threshold. The false-positive sequence introduces biased, irrelevant residues into the alignment, corrupting subsequent PSSM weights and causing the profile to drift away from the original query family to pull in thousands of unrelated proteins.
- **Two Operational Precautions:**
  1. **Tighten the inclusion threshold:** Lower the inclusion E-value cutoff from the default $0.005$ to a stringent threshold such as $E \le 10^{-4}$ or $10^{-5}$.
  2. **Manual curation of hit lists:** Visually inspect the hits between iterations to ensure that non-homologous hits (such as coiled-coils or transmembrane domains) are unselected before computing the next round's PSSM.
