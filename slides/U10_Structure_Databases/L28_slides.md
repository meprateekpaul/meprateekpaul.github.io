---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 28 Slides: Structure Comparison and Modeling"
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
# Lecture 28 — Structure Comparison and Modeling
### Concepts of Bioinformatics (CBBI-501)
**Unit 10:** Structure Databases  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Structure is More Conserved than Sequence

```text
Topic: Cyrus Chothia & Arthur Lesk's Law (1986)

[Visual: Superposition of Human Hemoglobin Beta vs Sperm Whale Myoglobin:
  Sequence Identity: ONLY 26% (Diverged ~500 million years ago!)
  Backbone RMSD: 1.45 Angstroms! (The 8 alpha-helices superimpose almost perfectly!)]
```

**Speaker Talking Points:**  
* Primary sequences diverge through neutral mutations and genetic drift.
* Secondary and tertiary folding topology is fiercely protected by natural selection.
* Over evolutionary time, **3D structure is 3 to 10 times more conserved than sequence**.
* Structural comparison reveals ancient evolutionary homologies invisible to BLAST.

---

## Slide 2: Quantifying Structural Similarity: RMSD

```text
Topic: The Root-Mean-Square Deviation

Formula:
  RMSD = sqrt[ (1 / N) * Sum_{i=1}^N d_i^2 ]
       = sqrt[ (1 / N) * Sum_{i=1}^N ||x_i - y_i||^2 ]

  * N: Number of aligned equivalent atoms (typically C_alpha backbone atoms).
  * d_i: Euclidean distance between equivalent atom i in Structure 1 and Structure 2.

Interpretation:
  * RMSD < 1.5 A  --> High structural identity (Close homologs or identical folds).
  * RMSD 1.5 - 3 A--> Same global fold; variations confined to flexible loops.
  * RMSD > 5.0 A  --> Different tertiary architectures.
```

**Speaker Talking Points:**  
* Before computing RMSD, the two structures must be optimally superimposed in space!

---

## Slide 3: Structural Superimposition: The Kabsch Algorithm (1976)

```text
Topic: Wolfgang Kabsch's Rigid-Body SVD Optimization

[Visual: Rotating and translating Structure Y onto Structure X:
  Step 1: Translate centroids of both structures to the origin (0, 0, 0).
  Step 2: Compute Covariance Matrix of equivalent atomic coordinates.
  Step 3: Perform Singular Value Decomposition (SVD) -> Extract optimal 3x3 Rotation Matrix U.
  Step 4: Rotate Structure Y to MINIMIZE the sum of squared distances!]
```

**Speaker Talking Points:**  
* RMSD cannot be calculated until the optimal rotation matrix $U$ and translation vector $t$
  are solved. The Kabsch algorithm finds the global minimum analytically.

---

## Slide 4: Structural Similarity Search Engines: DALI vs VAST+

```text
Topic: Searching the PDB for 3D Structural Neighbors

1. DALI (Distance Alignment Matrix — Liisa Holm & Chris Sander):
   * Internal 2D contact distance matrices (coordinate frame independent).
   * Aligns internal contact patterns like a fingerprint.

2. VAST / VAST+ (Vector Alignment Search Tool — NCBI MMDB):
   * Represents secondary structure elements (helices and sheets) as 3D vectors.
   * Aligns vector geometry rapidly to identify structural neighbors across the PDB.
```

**Speaker Talking Points:**  
* When a novel protein structure is solved, DALI and VAST instantly reveal whether
  its fold has ever been observed before.

---

## Slide 5: The Three Classic Modeling Paradigms

```text
Topic: Predicting 3D Structure from Sequence

+--------------------+-------------------------+------------------------------+
| Modeling Paradigm  | Target Sequence Identity| Underlying Strategy          |
+--------------------+-------------------------+------------------------------+
| **Homology**       | > 30% sequence identity | Copy coordinates from solved |
| (Comparative)      | with solved PDB template| homologous template (MODBLOCK)
| **Threading**      | 15% to 30% identity     | Fit sequence onto a library  |
| (Fold Recognition) | (The "Twilight Zone")   | of all known PDB folds       |
| **Ab Initio**      | No detectable homologs  | Physics/chemistry force fields|
| (De Novo)          | (Unknown fold)          | fragment assembly (Rosetta)  |
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* If a close homolog exists in the PDB (>30% identity), use Homology Modeling.

---

## Slide 6: Stereochemical Model Validation: The Ramachandran Plot

```text
Topic: Gopalasamudram Ramachandran's Dihedral Map (1963)

[Visual: Ramachandran Plot (phi vs psi angles):
  Top-Left: Beta-Sheet Region (phi ≈ -120, psi ≈ +130)
  Middle-Left: Right-Handed Alpha-Helix (phi ≈ -57, psi ≈ -47)
  Top-Right: Left-Handed Alpha-Helix (Glycine only!)
  White Space: Disallowed steric clash regions (atoms bump into each other!)]
```

**Speaker Talking Points:**  
* Non-bonded atoms cannot occupy the same physical space (steric hindrance).
* A high-quality model (checked via PROCHECK / MolProbity) must have **>90%** of
  residues in the most favored core regions.

---

## Slide 7: The Deep Learning Revolution: AlphaFold

```text
Topic: John Jumper & Demis Hassabis (Nobel Prize in Chemistry, 2024)

[Visual: AlphaFold 2 Architecture:
  Query Sequence + Multiple Sequence Alignment (MSA)
       |
       v
  Evoformer Neural Network (Iteratively updates MSA & Pairwise Residue Distances)
       |
       v
  Structure Module (Invariant Point Attention -> Predicts 3D Backbone Coordinates)
       |
       v
  Atomic Structure + Confidence Scores (pLDDT & PAE)]
```

**Speaker Talking Points:**  
* AlphaFold 2 solved the 50-year-old protein folding challenge at CASP14.
* Replaces classical molecular dynamics with attention-based deep learning.

---

## Slide 8: Reading AlphaFold Confidence: pLDDT and PAE

```text
Topic: How to Interpret an AlphaFold Prediction

  pLDDT (Predicted Local Distance Difference Test: 0 to 100):
  * > 90 (Dark Blue):  VERY HIGH confidence; reliable down to side-chain rotamers.
  * 70 - 90 (Light Blue): CONFIDENT; backbone topology highly reliable.
  * 50 - 70 (Yellow):     LOW confidence; overall fold plausible, loops uncertain.
  * < 50 (Orange):        VERY LOW confidence; represents **Intrinsically Disordered**
                          Regions (IDRs) that have no fixed 3D structure!
```

**Speaker Talking Points:**  
* Never mistake low pLDDT for an AlphaFold failure; it usually reflects true biological disorder!

