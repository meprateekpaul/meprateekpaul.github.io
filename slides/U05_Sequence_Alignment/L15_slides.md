---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 15 Slides: BLAST Artifacts and PSSMs"
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
# Lecture 15 — BLAST Artifacts and PSSMs
### Concepts of Bioinformatics (CBBI-501)
**Unit 05:** Sequence Alignment and Database Searching  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Dark Side of Sequence Searching

```text
Topic: When High Scores Do Not Mean Homology

[Visual: A massive BLAST hit table with 500 hits having E = 10^-80...
         all aligning to a 40-residue tract of pure Proline repeats (Poly-Pro)!]
```

**Speaker Talking Points:**  
* A statistically significant E-value does not automatically prove common ancestry.
* Search artifacts (low-complexity regions, compositional bias, coiled-coils)
  generate false-positive alignments that corrupt biological interpretations.
* A trained bioinformatician must inspect alignments critically, mask artifacts,
  and know when to deploy profile-based models (PSSMs).

---

## Slide 2: Low-Complexity Regions and Simple Repeats

```text
Topic: The Anatomy of Sequence Bias

Examples of Low-Complexity Sequences:
* Homopolymeric tracts: `AAAAAAAAAAAA` (Poly-A) or `QQQQQQQQQQQQ` (Huntingtin Poly-Q)
* Short tandem repeats: `(CA)_n` or `(GGC)_n`
* Compositionally biased regions: Collagen triple-helix `(Gly-Pro-Hyp)_n`
* Charge clusters: Poly-basic tracts `KKKKRRRRKKR`
```

**Speaker Talking Points:**  
* These regions did not evolve via traditional point-mutation descent from a common ancestor;
  they expand via replication slippage.
* Two completely unrelated proteins containing Poly-Q tracts will align with astronomical
  scores simply because Glutamine-Glutamine matches score positively!

---

## Slide 3: Masking Algorithms: SEG and DUST

```text
Topic: Filtering Entropy Deficits

  The SEG Algorithm (Wootton & Federhen, 1993):
  * Scans proteins using a sliding window (length 12) measuring **Shannon Entropy** (H):
    H = - Sum [ p_i * log_2(p_i) ]
  * Typical globular proteins: H ≈ 3.5 to 4.2 bits.
  * Low-complexity repeats: H drops below threshold (e.g. H < 2.2 bits).
  * Flagged segments are filtered before seed generation!

  The DUST Algorithm:
  * Masks low-complexity trinucleotide repeats in DNA sequences.
```

**Speaker Talking Points:**  
* SEG filters the query before BLAST generates neighborhood words.

---

## Slide 4: Hard Masking vs Soft Masking

```text
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
```

**Speaker Talking Points:**  
* Hard masking completely blinds BLAST to those coordinates.
* Soft masking (NCBI default) is superior: it prevents spurious seed triggering
  while permitting valid extensions that originate in authentic flanking sequence.

---

## Slide 5: The Limitation of Standard Matrices (Context-Blindness)

```text
Topic: Why BLOSUM62 Reaches a Plateau

[Visual: Two Leucine residues in human beta-globin:
  Leu68 (Deep in hydrophobic haem pocket: strictly invariant across all vertebrates)
  Leu3  (On flexible, solvent-exposed N-terminus: mutates freely to Val, Ala, Ile)
  BLOSUM62 treats both Leucines IDENTICALLY, awarding +4 for a match at both sites!]
```

**Speaker Talking Points:**  
* Standard matrices have no memory of position: a match scores the same everywhere.
* In reality, certain positions in an active site tolerate ZERO mutations, while loop
  positions tolerate almost anything.
* Solution: **Position-Specific Scoring Matrices (PSSMs)**.

---

## Slide 6: The Architecture of a PSSM

```text
Topic: Custom Scoring Vectors per Alignment Column

  Multiple Alignment Block (Columns 1 to L):
  Pos 1:  H   H   H   H   H   --> 100% His (Coordination site) -> High score for H only!
  Pos 2:  V   I   L   V   M   --> Hydrophobic core -> Scores for V, I, L, M all positive
  Pos 3:  A   G   S   T   P   --> Flexible loop -> Broad, permissive scores

  PSSM Structure:
  An (L x 20) matrix where EVERY position has its own unique 20-amino acid scoring column!
```

**Speaker Talking Points:**  
* A PSSM captures the unique evolutionary conservation profile of a protein family.

---

## Slide 7: PSI-BLAST: Position-Specific Iterated BLAST

```text
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
```

**Speaker Talking Points:**  
* PSI-BLAST detects distant evolutionary relationships in the "Twilight Zone" (20-30% id).

---

## Slide 8: The Fatal Trap: Profile Drift

```text
Topic: When a Single Impostor Corrupts the Search

[Visual: Contamination cascading across iterations:
  Round 1: Globin query pulls in 1 spurious coiled-coil protein (e.g. Myosin).
  Round 2: PSSM incorporates coiled-coil heptad repeat bias.
  Round 3: PSSM pulls in 2,000 kinesins, myosins, and keratins!
  Result: The globin profile is completely destroyed (Profile Drift / Corruption).]
```

**Speaker Talking Points:**  
* Never run PSI-BLAST unattended!
* Set strict inclusion thresholds ($E \le 10^{-4}$) and verify hits between rounds.

