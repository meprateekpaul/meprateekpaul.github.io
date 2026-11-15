---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 25 Slides: Secondary Structure Prediction"
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
# Lecture 25 — Secondary Structure Prediction
### Concepts of Bioinformatics (CBBI-501)
**Unit 09:** Predictive Methods using Protein Sequence  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Secondary Structure Bridge

```text
Topic: From 1D Letters to 3D Shapes

[Visual: Hierarchy: Primary Sequence -> Secondary Structure (Helices & Sheets)
         -> Tertiary Fold -> Quaternary Complex]
```

**Speaker Talking Points:**  
* Before predicting full 3D coordinates, we predict the local secondary structure:
  which segments form rigid $\alpha$-helices, extended $\beta$-sheets, or flexible loops?
* Secondary structure prediction provides essential spatial constraints for fold recognition,
  homology modeling, and functional site prediction.

---

## Slide 2: Biophysical Geometries of Pauling & Corey (1951)

```text
Topic: Hydrogen-Bonding Patterns in Polypeptide Backbones

1. The Alpha-Helix:
   * Right-handed spiral: 3.6 residues per turn; pitch = 5.4 Angstroms.
   * Backbone H-bond between C=O of residue i and N-H of residue i+4.
   * Ramachandran angles: phi ≈ -57 degrees, psi ≈ -47 degrees.

2. The Beta-Strand / Beta-Sheet:
   * Extended conformation: 3.2 to 3.4 Angstroms per residue.
   * Inter-strand H-bonding between adjacent parallel or antiparallel strands.
   * Ramachandran angles: phi ≈ -120 to -140 degrees, psi ≈ +130 to +150 degrees.
```

**Speaker Talking Points:**  
* Secondary structures satisfy backbone hydrogen-bonding requirements in hydrophobic interiors.

---

## Slide 3: The DSSP Standard 3-State Reduction

```text
Topic: Kabsch & Sander's Ground Truth Definition (1983)

+--------------------+-------------------------+------------------------------+
| DSSP 8-State Code  | Structural Description  | 3-State Reduced Class        |
+--------------------+-------------------------+------------------------------+
| `H`                | Standard alpha-helix    | **H (Helix)**                |
| `G`                | 3_10-helix (i -> i+3)   | **H (Helix)**                |
| `I`                | pi-helix (i -> i+5)     | **H (Helix)**                |
| `E`                | Extended beta-strand    | **E (Sheet / Strand)**       |
| `B`                | Isolated beta-bridge    | **E (Sheet / Strand)**       |
| `T`                | H-bonded turn           | **C (Coil / Loop)**          |
| `S`                | High-curvature bend     | **C (Coil / Loop)**          |
| ` ` (blank)        | Irregular unstructured  | **C (Coil / Loop)**          |
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* Experimental 3D structures from PDB are assigned secondary structure using **DSSP**.
* Predictors output a simplified 3-letter alphabet: **H**, **E**, or **C**.

---

## Slide 4: First-Generation Predictors: Chou-Fasman (~50%)

```text
Topic: Single-Sequence Statistical Propensities (1974)

  The Chou-Fasman Method:
  * Calculated empirical propensity tables P(alpha), P(beta), P(turn) from 15 crystal structures.
  * Strong Helix formers: Ala, Glu, Leu, Met (P_alpha > 1.2).
  * Strong Sheet formers: Val, Ile, Tyr, Phe (P_beta > 1.2).
  * Helix breakers: Proline (rigid ring), Glycine (too flexible).

  Nucleation Rule:
  * A cluster of 4 out of 6 helical formers nucleates a helix; extend until terminated by breakers.
```

**Speaker Talking Points:**  
* Limitation: Evaluates isolated single sequences; completely ignores evolutionary conservation.
* Accuracy plateaued at ~50-55% (barely better than a random coin toss!).

---

## Slide 5: Second-Generation Predictors: The GOR Method (~65%)

```text
Topic: Information Theory (Garnier, Osgood & Robson, 1978)

[Visual: 17-Residue Sliding Window:
  Residue under evaluation (i) centered among 8 flanking residues on each side:
  [ i-8, i-7, ..., i-1,  ( i ),  i+1, ..., i+7, i+8 ]
  Calculates directional information probabilities based on pair frequencies!]
```

**Speaker Talking Points:**  
* GOR recognized that secondary structure depends on local context (8 residues upstream/downstream).
* Accuracy reached ~60-65% (the practical theoretical limit for single-sequence prediction).

---

## Slide 6: Third-Generation Revolution: PSIPRED (>80%)

```text
Topic: David Jones' Evolutionary Breakthrough (1999)

[Visual: PSIPRED Architecture:
  Query Sequence -> PSI-BLAST -> Position-Specific Scoring Matrix (PSSM)
                     |
                     v
  Neural Network 1 (Predicts initial H, E, C probabilities from PSSM)
                     |
                     v
  Neural Network 2 (Filters unrealistic predictions; e.g. single-residue helices)
                     |
                     v
  Final Publication-Quality Secondary Structure Prediction (>80% accuracy!)]
```

**Speaker Talking Points:**  
* Crucial Insight: Structure is far more conserved than primary sequence across evolution!
* By feeding evolutionary profiles (PSSMs) into neural networks, accuracy shattered
  the 80% barrier.

---

## Slide 7: Evaluating Predictor Accuracy: The Q3 Metric

```text
Topic: Quantifying Prediction Quality

Formula:
  Q_3 = [ (N_H + N_E + N_C) / N_total ] * 100%

  * N_H: Number of correctly predicted Helical residues
  * N_E: Number of correctly predicted Sheet residues
  * N_C: Number of correctly predicted Coil residues
  * N_total: Total residues in the benchmark dataset
```

**Speaker Talking Points:**  
* Evaluated against ground-truth DSSP assignments from high-resolution X-ray structures.
* Complemented by the Matthews Correlation Coefficient (MCC) to account for class imbalance.

---

## Slide 8: Protein Folding Classes (SCOP & CATH)

```text
Topic: Levitt & Chothia Structural Architecture (1976)

1. All-Alpha: Dominated exclusively by alpha-helices.
   * Example: **Globin Fold** (Human HBB, Myoglobin) — 8 alpha-helices (A to H).
2. All-Beta: Dominated exclusively by beta-sheets.
   * Example: Immunoglobulin fold, beta-barrels (Plastocyanin).
3. Alpha / Beta: Alternating helices and parallel beta-strands.
   * Example: TIM barrel (Triosephosphate isomerase).
4. Alpha + Beta: Segregated helical and beta-sheet regions.
   * Example: Lysozyme, Ribonuclease A.
```

**Speaker Talking Points:**  
* Human beta-globin is a quintessential **All-Alpha** protein.

