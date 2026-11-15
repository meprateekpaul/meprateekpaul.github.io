# Lecture 25 — Secondary Structure Prediction

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 9:** Predictive Methods using Protein Sequence  
**Syllabus Topic:** Secondary structure and folding classes, specialized structure or features, Tertiary structures  
**Primary Learning Outcome:** LO6 — Predict sequence-based features: calculate Q3 prediction accuracy, evaluate Chou-Fasman, GOR, and PSIPRED algorithms, and classify protein folding classes.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Secondary Structure Bridge
================================================================================
Topic: From 1D Letters to 3D Shapes

[Visual: Hierarchy: Primary Sequence -> Secondary Structure (Helices & Sheets)
         -> Tertiary Fold -> Quaternary Complex]

Speaker Bullets:
* Before predicting full 3D coordinates, we predict the local secondary structure:
  which segments form rigid $\alpha$-helices, extended $\beta$-sheets, or flexible loops?
* Secondary structure prediction provides essential spatial constraints for fold recognition,
  homology modeling, and functional site prediction.
```

```
================================================================================
SLIDE 2: Biophysical Geometries of Pauling & Corey (1951)
================================================================================
Topic: Hydrogen-Bonding Patterns in Polypeptide Backbones

1. The Alpha-Helix:
   * Right-handed spiral: 3.6 residues per turn; pitch = 5.4 Angstroms.
   * Backbone H-bond between C=O of residue i and N-H of residue i+4.
   * Ramachandran angles: phi ≈ -57 degrees, psi ≈ -47 degrees.

2. The Beta-Strand / Beta-Sheet:
   * Extended conformation: 3.2 to 3.4 Angstroms per residue.
   * Inter-strand H-bonding between adjacent parallel or antiparallel strands.
   * Ramachandran angles: phi ≈ -120 to -140 degrees, psi ≈ +130 to +150 degrees.

Speaker Bullets:
* Secondary structures satisfy backbone hydrogen-bonding requirements in hydrophobic interiors.
```

```
================================================================================
SLIDE 3: The DSSP Standard 3-State Reduction
================================================================================
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

Speaker Bullets:
* Experimental 3D structures from PDB are assigned secondary structure using **DSSP**.
* Predictors output a simplified 3-letter alphabet: **H**, **E**, or **C**.
```

```
================================================================================
SLIDE 4: First-Generation Predictors: Chou-Fasman (~50%)
================================================================================
Topic: Single-Sequence Statistical Propensities (1974)

  The Chou-Fasman Method:
  * Calculated empirical propensity tables P(alpha), P(beta), P(turn) from 15 crystal structures.
  * Strong Helix formers: Ala, Glu, Leu, Met (P_alpha > 1.2).
  * Strong Sheet formers: Val, Ile, Tyr, Phe (P_beta > 1.2).
  * Helix breakers: Proline (rigid ring), Glycine (too flexible).

  Nucleation Rule:
  * A cluster of 4 out of 6 helical formers nucleates a helix; extend until terminated by breakers.

Speaker Bullets:
* Limitation: Evaluates isolated single sequences; completely ignores evolutionary conservation.
* Accuracy plateaued at ~50-55% (barely better than a random coin toss!).
```

```
================================================================================
SLIDE 5: Second-Generation Predictors: The GOR Method (~65%)
================================================================================
Topic: Information Theory (Garnier, Osgood & Robson, 1978)

[Visual: 17-Residue Sliding Window:
  Residue under evaluation (i) centered among 8 flanking residues on each side:
  [ i-8, i-7, ..., i-1,  ( i ),  i+1, ..., i+7, i+8 ]
  Calculates directional information probabilities based on pair frequencies!]

Speaker Bullets:
* GOR recognized that secondary structure depends on local context (8 residues upstream/downstream).
* Accuracy reached ~60-65% (the practical theoretical limit for single-sequence prediction).
```

```
================================================================================
SLIDE 6: Third-Generation Revolution: PSIPRED (>80%)
================================================================================
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

Speaker Bullets:
* Crucial Insight: Structure is far more conserved than primary sequence across evolution!
* By feeding evolutionary profiles (PSSMs) into neural networks, accuracy shattered
  the 80% barrier.
```

```
================================================================================
SLIDE 7: Evaluating Predictor Accuracy: The Q3 Metric
================================================================================
Topic: Quantifying Prediction Quality

Formula:
  Q_3 = [ (N_H + N_E + N_C) / N_total ] * 100%

  * N_H: Number of correctly predicted Helical residues
  * N_E: Number of correctly predicted Sheet residues
  * N_C: Number of correctly predicted Coil residues
  * N_total: Total residues in the benchmark dataset

Speaker Bullets:
* Evaluated against ground-truth DSSP assignments from high-resolution X-ray structures.
* Complemented by the Matthews Correlation Coefficient (MCC) to account for class imbalance.
```

```
================================================================================
SLIDE 8: Protein Folding Classes (SCOP & CATH)
================================================================================
Topic: Levitt & Chothia Structural Architecture (1976)

1. All-Alpha: Dominated exclusively by alpha-helices.
   * Example: **Globin Fold** (Human HBB, Myoglobin) — 8 alpha-helices (A to H).
2. All-Beta: Dominated exclusively by beta-sheets.
   * Example: Immunoglobulin fold, beta-barrels (Plastocyanin).
3. Alpha / Beta: Alternating helices and parallel beta-strands.
   * Example: TIM barrel (Triosephosphate isomerase).
4. Alpha + Beta: Segregated helical and beta-sheet regions.
   * Example: Lysozyme, Ribonuclease A.

Speaker Bullets:
* Human beta-globin is a quintessential **All-Alpha** protein.
```

---

## Detailed Comprehensive Technical Notes

### 1. Biophysical Principles of Secondary Structure

In 1951, Linus Pauling and Robert Corey published the stereochemical principles governing protein secondary structure before any experimental crystal structure of a protein had been solved.

The polypeptide backbone is constrained by the partial double-bond character ($\approx 40\%$) of the planar peptide bond ($-CO-NH-$), which restricts rotational freedom to two torsional angles per residue:
- **$\phi$ (phi):** Rotation about the $N-C_\alpha$ bond.
- **$\psi$ (psi):** Rotation about the $C_\alpha-C$ bond.

```
  Secondary Structure    Hydrogen-Bonding Pattern       Geometry & Pitch               Ramachandran Angles
  -------------------------------------------------------------------------------------------------
  alpha-Helix            i -> i+4 (C=O of residue i     Right-handed; 3.6 residues/    phi ≈ -57 degrees,
                         bonds with N-H of i+4)         turn; pitch = 5.4 Angstroms    psi ≈ -47 degrees
  3_10-Helix             i -> i+3 (Tighter helical turn)3.0 residues/turn; pitch 6.0 A phi ≈ -49 degrees, psi ≈ -26 degrees
  pi-Helix               i -> i+5 (Wider, bulging helix)4.4 residues/turn; pitch 5.2 A phi ≈ -57 degrees, psi ≈ -70 degrees
  Parallel beta-Sheet    Inter-strand H-bonds slanted   3.2 Angstroms per residue      phi ≈ -119 deg, psi ≈ +113 deg
  Antiparallel beta-SheetInter-strand H-bonds linear    3.4 Angstroms per residue      phi ≈ -139 deg, psi ≈ +135 deg
  beta-Turn (Reverse)    i -> i+3 H-bond reverses chain 4 residues; sharp 180 deg turn Type I, Type II (Pro/Gly)
```

---

### 2. The DSSP Ground-Truth Standard

To train and evaluate computational predictors, researchers need an objective standard for determining which residues in a solved crystal structure belong to helices, sheets, or coils. 

In 1983, Wolfgang Kabsch and Chris Sander developed **DSSP (Dictionary of Secondary Structure of Proteins)**, which evaluates the electrostatic hydrogen-bond energy $E$ between all backbone carbonyls and amides using Coulomb's law:

$$E = q_1 q_2 \left( \frac{1}{r_{ON}} + \frac{1}{r_{CH}} - \frac{1}{r_{OH}} - \frac{1}{r_{CN}} \right) \cdot f$$

A hydrogen bond is defined if $E < -0.5\text{ kcal/mol}$.

DSSP classifies residues into **eight discrete states**:
- $H$: $\alpha$-helix ($i \to i+4$)
- $G$: $3_{10}$-helix ($i \to i+3$)
- $I$: $\pi$-helix ($i \to i+5$)
- $E$: Extended $\beta$-strand participating in a $\beta$-ladder
- $B$: Isolated $\beta$-bridge (single-pair $\beta$-sheet hydrogen bond)
- $T$: Hydrogen-bonded turn
- $S$: High-curvature bend
- $C$ / Blank: Irregular loop or coil

For computational machine learning and evaluation, these 8 states are universally reduced to the **Three-State Alphabet ($H, E, C$)**:
$$\mathbf{H} \in \{H, G, I\}, \quad \mathbf{E} \in \{E, B\}, \quad \mathbf{C} \in \{T, S, C\}$$

---

### 3. The Three Generations of Predictors

```
  Generation      Era        Primary Tools              Input Data Used             Average Accuracy (Q3)
  -------------------------------------------------------------------------------------------------
  First           1970s      Chou-Fasman, Lim           Single primary sequence     ~50% to 55%
  Second          1980s      GOR I-IV, Levin            Single sequence + 17-aa     ~60% to 65%
                                                        statistical sliding window
  Third           1990s+     PSIPRED, JPred, PHD        Evolutionary MSA / PSSM     **> 80% to 84%**
                                                        fed into Neural Networks
```

#### A. First Generation: Chou-Fasman (1974)
Peter Chou and Gerald Fasman calculated statistical propensities $P(\alpha)$, $P(\beta)$, and $P(\text{turn})$ for each amino acid from a tiny dataset of 15 proteins:
- Helical formers: Ala ($1.42$), Glu ($1.51$), Leu ($1.21$), Met ($1.45$).
- Sheet formers: Val ($1.70$), Ile ($1.60$), Tyr ($1.47$), Phe ($1.38$).
- Breakers: Proline (cannot form $i \to i+4$ H-bond; forces structural kink), Glycine (high conformational entropy destabilizes rigid folds).
*Why it failed:* Prediction accuracy plateaued at $\approx 50\%$. Local amino acid propensities account for less than half of secondary structure determination; tertiary packing and non-local interactions play a dominant role.

#### B. Second Generation: The GOR Method (1978)
Jean Garnier, David Osgood, and Barry Robson developed an information-theory model. GOR uses a **sliding window of 17 amino acids** (the target residue $i$ flanked by 8 residues on each side: $i-8$ to $i+8$).
The probability that residue $i$ is in conformation $S$ ($S \in \{H, E, C\}$) is computed as the log-odds information difference:

$$I(S_i; R_{i-8} \dots R_{i+8}) = \log \frac{P(S_i \mid R_{i-8} \dots R_{i+8})}{P(S_i)}$$

GOR IV incorporates directional residue-pair correlations, pushing accuracy to $\approx 64.4\%$.

#### C. Third Generation: PSIPRED (David Jones, 1999)
David Jones recognized that while primary sequences diverge rapidly, **secondary structure is strictly conserved across evolutionary homologs**.
1. **Step 1 (PSI-BLAST Profile):** The query sequence is searched against the non-redundant database using PSI-BLAST for three iterations to generate a rich Position-Specific Scoring Matrix (PSSM).
2. **Step 2 (First Neural Network):** An artificial neural network with a sliding window of 15 positions processes the $15 \times 20$ PSSM matrix elements to generate initial raw probabilities for $H$, $E$, and $C$.
3. **Step 3 (Filtering Neural Network):** A second cascaded neural network processes the raw prediction stream to filter out physically impossible structural artifacts (such as a single isolated helical residue `...C-H-C...`, which cannot exist because an $\alpha$-helix requires at least 3 consecutive residues to form a single hydrogen bond turn).
4. **Result:** PSIPRED consistently achieves a $Q_3$ accuracy of **$80\%$ to $84\%$**, representing the gold-standard benchmark in modern bioinformatics.

---

### 4. Quantitative Evaluation Metrics

#### A. Three-State Accuracy ($Q_3$)
The overall percentage of correctly predicted residues across all three classes:

$$Q_3 = \frac{N_H + N_E + N_C}{N_{\text{total}}} \times 100\% = \frac{\sum_{k \in \{H, E, C\}} \text{True Positives}_k}{N_{\text{total}}} \times 100\%$$

#### B. The Confusion Matrix
A $3 \times 3$ contingency table cross-tabulating observed (experimental DSSP) vs predicted states:

```
                      PREDICTED STATE
                  Helix (H)   Sheet (E)   Coil (C)     Total Observed
  OBSERVED  H       TP_H        E_as_H      C_as_H          Obs_H
  (DSSP)    E       H_as_E      TP_E        C_as_E          Obs_E
            C       H_as_C      E_as_C      TP_C            Obs_C
  -------------------------------------------------------------------
  Total Pred        Pred_H      Pred_E      Pred_C          N_total
```

#### C. Matthews Correlation Coefficient ($\text{MCC}_k$)
Because coils and helices are generally more abundant than $\beta$-sheets in biological databases, $Q_3$ can be misleading if a predictor simply over-predicts the dominant class. The **Matthews Correlation Coefficient** provides a balanced metric ranging from $-1.0$ (complete disagreement) through $0.0$ (random guessing) to $+1.0$ (perfect prediction):

$$\text{MCC}_k = \frac{(TP_k \cdot TN_k) - (FP_k \cdot FN_k)}{\sqrt{(TP_k + FP_k)(TP_k + FN_k)(TN_k + FP_k)(TN_k + FN_k)}}$$

---

### 5. Protein Folding Classes (Levitt & Chothia, 1976)

Based on the composition and spatial arrangement of secondary structure elements, Michael Levitt and Cyrus Chothia classified protein folds into **four primary classes**:

1. **All-$\alpha$:** Structures dominated almost entirely by $\alpha$-helices packed together against one another, connected by short loops.
   - *Archetype:* The **Globin Fold** (Human Hemoglobin Beta, Myoglobin). Composed of **8 amphipathic $\alpha$-helices** designated $A, B, C, D, E, F, G, H$ forming a rigid, solvent-excluding pocket that cradles the planar haem group.
2. **All-$\beta$:** Structures dominated by antiparallel or parallel $\beta$-sheets forming sandwich or barrel topologies.
   - *Archetype:* The **Immunoglobulin Fold** (antibodies, T-cell receptors, titin) and $\beta$-barrel proteins (porins, green fluorescent protein [GFP]).
3. **$\alpha/\beta$:** Structures containing alternating $\alpha$-helices and parallel $\beta$-strands ($(\beta-\alpha-\beta)_n$). The $\beta$-strands typically form an internal parallel sheet shielded on both sides by outer $\alpha$-helices.
   - *Archetype:* The **TIM Barrel** (Triosephosphate isomerase: $(\beta-\alpha)_8$ barrel) and the Rossmann dinucleotide-binding fold.
4. **$\alpha+\beta$:** Structures containing segregated clusters of $\alpha$-helices and $\beta$-sheets that do not alternate along the linear sequence.
   - *Archetype:* Lysozyme, Ribonuclease A.

---

## Worked Mathematical Example: Computing $Q_3$ and the Confusion Matrix by Hand

### Problem:
A newly developed secondary structure predictor evaluates a 20-residue peptide fragment from human beta-globin.  
The experimental ground-truth assigned by DSSP from PDB crystal structure `1A3N` and the algorithmic prediction are:

```
  Position:   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18  19  20
  Residue:    V   H   L   T   P   E   E   K   S   A   V   T   A   L   W   G   K   V   N   V
  DSSP Truth: C   C   C   C   C   H   H   H   H   H   H   H   H   H   H   H   H   H   C   C
  Prediction: C   C   C   H   C   H   H   H   E   H   H   H   H   H   H   H   H   H   C   H
```

1. Construct the complete $3 \times 3$ **Confusion Matrix**.
2. Calculate the number of True Positives for each state: $N_H, N_E, N_C$.
3. Calculate the overall **Three-State Accuracy ($Q_3$)**.
4. Calculate the Matthews Correlation Coefficient for Helix ($\text{MCC}_H$).

---

### Step 1: Residue-by-Residue Comparison Table

```
  Pos   Residue   Truth   Pred   Evaluation
  -------------------------------------------------------------
  1     V         C       C      Correct Coil (TP_C)
  2     H         C       C      Correct Coil (TP_C)
  3     L         C       C      Correct Coil (TP_C)
  4     T         C       H      False Positive Helix / False Negative Coil (C predicted as H)
  5     P         C       C      Correct Coil (TP_C)
  6     E         H       H      Correct Helix (TP_H)
  7     E         H       H      Correct Helix (TP_H)
  8     K         H       H      Correct Helix (TP_H)
  9     S         H       E      False Positive Sheet / False Negative Helix (H predicted as E)
  10    A         H       H      Correct Helix (TP_H)
  11    V         H       H      Correct Helix (TP_H)
  12    T         H       H      Correct Helix (TP_H)
  13    A         H       H      Correct Helix (TP_H)
  14    L         H       H      Correct Helix (TP_H)
  15    W         H       H      Correct Helix (TP_H)
  16    G         H       H      Correct Helix (TP_H)
  17    K         H       H      Correct Helix (TP_H)
  18    V         H       H      Correct Helix (TP_H)
  19    N         C       C      Correct Coil (TP_C)
  20    V         C       H      False Positive Helix / False Negative Coil (C predicted as H)
```

---

### Step 2: Construct the $3 \times 3$ Confusion Matrix

```
                      PREDICTED STATE
                  Helix (H)   Sheet (E)   Coil (C)     Total Observed
  OBSERVED  H        12           1           0             13
  (DSSP)    E         0           0           0              0
            C         2           0           5              7
  -------------------------------------------------------------------
  Total Pred         14           1           5             20
```

---

### Step 3: Count True Positives
- **Correct Helices ($N_H$):** $12$ (Positions 6, 7, 8, 10, 11, 12, 13, 14, 15, 16, 17, 18)
- **Correct Sheets ($N_E$):** $0$ (No sheets were present in the true peptide)
- **Correct Coils ($N_C$):** $5$ (Positions 1, 2, 3, 5, 19)
- Total correctly predicted residues:
  $$N_{\text{correct}} = N_H + N_E + N_C = 12 + 0 + 5 = \mathbf{17\text{ residues}}$$

---

### Step 4: Calculate $Q_3$ Accuracy
$$Q_3 = \frac{N_H + N_E + N_C}{N_{\text{total}}} \times 100\% = \frac{17}{20} \times 100\% = \mathbf{85.0\%}$$
The algorithm achieved a $Q_3$ accuracy of **85.0%** on this peptide.

---

### Step 5: Compute Matthews Correlation for Helix ($\text{MCC}_H$)
For the Helix class:
- $TP_H = 12$
- $FP_H = 2$ (Positions 4 and 20 were Coils predicted as Helices)
- $FN_H = 1$ (Position 9 was a Helix predicted as a Sheet)
- $TN_H = 5$ (Positions 1, 2, 3, 5, 19 were non-helices correctly predicted as non-helices)

Apply the MCC formula:
$$\text{MCC}_H = \frac{(TP \cdot TN) - (FP \cdot FN)}{\sqrt{(TP + FP)(TP + FN)(TN + FP)(TN + FN)}}$$
$$\text{Numerator} = (12 \times 5) - (2 \times 1) = 60 - 2 = \mathbf{58}$$
$$\text{Denominator} = \sqrt{(12 + 2)(12 + 1)(5 + 2)(5 + 1)} = \sqrt{14 \times 13 \times 7 \times 6}$$
$$\text{Denominator} = \sqrt{182 \times 42} = \sqrt{7644} \approx \mathbf{87.43}$$
$$\text{MCC}_H = \frac{58}{87.43} \approx \mathbf{+0.663}$$
An MCC of $+0.663$ indicates strong, positive predictive correlation for the $\alpha$-helical state.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A bioinformatician designs a naive secondary structure predictor that classifies every single residue in every protein as "Coil" ($C$). If evaluated against a database of typical globular proteins where the true distribution is 35% Helix, 20% Sheet, and 45% Coil:
1. What $Q_3$ score will this trivial predictor achieve?  
2. Why does the Matthews Correlation Coefficient (MCC) expose this predictor as completely worthless?

**Model Answer:**
1. **$Q_3$ Score:** Because 45% of residues in the database are coils, classifying every residue as coil will achieve a $Q_3$ score of **45.0%** ($N_C = 45$, $N_H = 0$, $N_E = 0$), despite possessing zero real predictive capability.
2. **Why MCC exposes it:** For Helix and Sheet, True Positives ($TP$) will be zero, causing the numerator of the MCC formula to become zero or negative. The Matthews Correlation Coefficients for Helix and Sheet will be $\text{MCC}_H = 0.0$ and $\text{MCC}_E = 0.0$ (or undefined), correctly revealing that the predictor has zero correlation with physical reality.

---

### Question 2
**Prompt:** Why does an isolated single-residue $\alpha$-helix (such as predicting `...C-H-C...`) represent a physically impossible secondary structure prediction in protein biophysics? How do filtering neural networks in PSIPRED eliminate such artifacts?

**Model Answer:**
- **Physical Impossibility:** An $\alpha$-helix is defined by a continuous backbone hydrogen bond between the carbonyl oxygen ($C=O$) of residue $i$ and the amide hydrogen ($N-H$) of residue $i+4$. To form even a single turn of an $\alpha$-helix, at least three to four consecutive residues must adopt the helical $(\phi, \psi)$ dihedral angles simultaneously. A single isolated amino acid cannot form an $i \to i+4$ hydrogen bond on its own.
- **PSIPRED Filtering:** PSIPRED employs a second, cascaded neural network that scans the output of the first network with a structural grammar filter. If it detects physically unfeasible patterns (such as an isolated `H` surrounded by coils or sheets), it automatically smooths the prediction, converting the isolated residue to coil.

---

### Question 3
**Prompt:** According to the Levitt & Chothia structural classification, human beta-globin belongs to the **All-$\alpha$** folding class. Describe the secondary structure composition of the globin fold, and state the total number of $\alpha$-helices present in a mature beta-globin subunit.

**Model Answer:**
- **Globin Fold Composition:** The globin fold is composed almost exclusively of $\alpha$-helices connected by short, flexible non-helical loop segments, containing **zero $\beta$-sheets**.
- **Number of Helices:** A mature human beta-globin subunit contains **eight distinct $\alpha$-helices**, traditionally designated alphabetically from the N-terminus to the C-terminus as **Helices A, B, C, D, E, F, G, and H**. These eight helices fold into a compact globular bundle surrounding the central hydrophobic haem cleft, where the distal Histidine (His64 on Helix E) and proximal Histidine (His93 on Helix F) coordinate the oxygen-binding iron atom.
