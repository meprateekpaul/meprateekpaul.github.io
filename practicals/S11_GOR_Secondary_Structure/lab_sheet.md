# Practical 11: Protein Secondary Structure Prediction Using GOR IV, PSIPRED, and Crystallographic Validation

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S11 (Syllabus Practical P13)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO6 — Predict protein secondary structure from sequence, contrast statistical propensity algorithms (GOR) with evolutionary neural networks (PSIPRED), and calculate three-state prediction accuracy ($Q_3$) against crystallographic ground truth (DSSP).

---

## 1. Aim & Objectives

### Aim
To predict the secondary structural states (alpha-helix, beta-sheet, coil/loop) of human hemoglobin beta (`NP_000509.1`) using the statistical GOR IV algorithm and the profile-based neural network server PSIPRED, validate predictions against the experimental crystallographic secondary structure (DSSP from PDB `1A3N`), and manually calculate the three-state accuracy metric ($Q_3$).

### Objectives
1. Understand the biophysical and stereochemical principles governing secondary structure formation (Ramachandran $\phi, \psi$ angles and hydrogen-bonding networks).
2. Execute secondary structure prediction using the **GOR IV** algorithm (Garnier-Osguthorpe-Robson) on the PBIL NPS@ server.
3. Execute secondary structure prediction using **PSIPRED V4.0** (Position-Specific Iterated PSSM-based two-stage neural network) at UCL Bioinf.
4. Extract the true experimental crystallographic secondary structure assignment defined by the **DSSP** algorithm (Dictionary of Secondary Structure of Proteins) from PDB entry `1A3N` (Chain B).
5. Align the predicted strings against the ground truth and compute the three-state accuracy metric ($Q_3$) by hand:
   $$Q_3 = \frac{N_{\text{correct}}}{N_{\text{total}}} \times 100\%$$
6. Critically evaluate why GOR IV predicts spurious beta-strands in an all-$\alpha$ helical globin fold, and explain how evolutionary profile information (PSI-BLAST checkpoints) enables PSIPRED to achieve superior accuracy ($>80\%$).

---

## 2. Background & Scientific Principle

### Secondary Structure and the Three-State Representation
Protein secondary structure refers to regular local conformations of the polypeptide backbone stabilized by hydrogen bonds between peptide amide ($N\text{--}H$) and carbonyl ($C\text{=O}$) groups:
- **$\alpha$-Helix ($H$):** Right-handed spiral with $3.6$ residues per turn; hydrogen bonds form between residue $i$ and residue $i+4$.
- **$\beta$-Strand ($E$ for Extended):** Stretched polypeptide chains ($3.3\text{ \AA}$ per residue) organized into parallel or anti-parallel $\beta$-sheets via inter-strand hydrogen bonds.
- **Coil / Loop ($C$ or $T$):** Non-repetitive turns, loops, and flexible coils connecting regular secondary structures.

In computational prediction benchmarks, structures are standardized into a **three-state alphabet**:
$$\Sigma = \{H, E, C\}$$

### Evolution of Prediction Methods
1. **First-Generation Methods (1970s, Single Residue Propensities):**
   - *Chou-Fasman:* Assigned empirical conformational parameters ($P_{\alpha}, P_{\beta}, P_{\text{turn}}$) based on residue frequencies in small crystal structures (~50% accuracy).
2. **Second-Generation Methods (1980s, Information Theory & Segment Propensities):**
   - *GOR Method (Garnier, Osguthorpe, Robson):* Formulated on information theory. GOR posits that the structural state of residue $i$ is influenced not only by itself, but by a symmetric sliding window of 17 adjacent residues (8 residues upstream and 8 downstream: $i-8$ to $i+8$).
   - *GOR IV:* Uses all pairwise residue correlations within the 17-residue window. Reaches ~64% $Q_3$ accuracy, but lacks evolutionary information.
3. **Third-Generation Methods (Late 1990s–Present, Evolutionary Profiles & Machine Learning):**
   - *PSIPRED (Jones, 1999):* Recognizes that structure is far more conserved during evolution than sequence. PSIPRED runs PSI-BLAST to generate a Position-Specific Scoring Matrix (PSSM), reflecting evolutionary mutational tolerances. The PSSM is fed into a two-stage feed-forward neural network (filtering window of 15 residues), achieving $Q_3 > 80\%$.

### Ground Truth Validation: The DSSP Algorithm
Kabsch and Sander (1983) developed **DSSP** to assign secondary structure unambiguously from experimental atomic 3D coordinates ($X, Y, Z$) stored in PDB files. DSSP evaluates electrostatic hydrogen-bond energy:
$$E = q_1 q_2 \left( \frac{1}{r_{\text{ON}}} + \frac{1}{r_{\text{CH}}} - \frac{1}{r_{\text{OH}}} - \frac{1}{r_{\text{CN}}} \right) \times 332\text{ kcal/mol}$$
A hydrogen bond is defined when $E < -0.5\text{ kcal/mol}$. DSSP assigns an 8-state classification ($H, G, I, E, B, T, S, C$), which is reduced to the 3-state alphabet ($H/G \rightarrow H$, $E/B \rightarrow E$, others $\rightarrow C$).

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & URLs
- PBIL NPS@ GOR IV Server: [https://npsa-prabi.ibcp.fr/cgi-bin/npsa_automat.pl?page=/NPSA/npsa_gor4.html](https://npsa-prabi.ibcp.fr/cgi-bin/npsa_automat.pl?page=/NPSA/npsa_gor4.html)
- UCL PSIPRED V4.0 Server: [https://bioinf.cs.ucl.ac.uk/psipred/](https://bioinf.cs.ucl.ac.uk/psipred/)
- RCSB PDB Structure Gateway: [https://www.rcsb.org/structure/1A3N](https://www.rcsb.org/structure/1A3N)

### Input Datasets & Local Files
- Query Sequence: Human HBB (`NP_000509.1`, 147 aa)
  - File: `../../data/sequences/hbb_human_protein.fasta`
- Pre-computed Expected Server Outputs:
  - `../../data/expected/gor4_hbb_secondary_structure.txt`
  - `../../data/expected/psipred_hbb_secondary_structure.txt`
  - `../../data/expected/dssp_hbb_1a3n.txt`

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Running GOR IV on PBIL NPS@
1. Open the PBIL NPS@ GOR IV web interface:
   `https://npsa-prabi.ibcp.fr/cgi-bin/npsa_automat.pl?page=/NPSA/npsa_gor4.html`
2. In the sequence box, paste the 147-amino-acid human HBB protein sequence from `../../data/sequences/hbb_human_protein.fasta`.
3. Leave default options selected.
4. Click **Submit**.
5. When the calculation finishes, inspect the output:
   - Examine the probability curves for Helix ($H$), Sheet ($E$), and Coil ($C$).
   - Record the predicted state sequence string ($H, E, C$).
   - Record the overall predicted percentages: % Helix, % Extended, % Coil.
   - Note particularly whether GOR IV predicts any extended $\beta$-strands (`E`) in the region between residues 40 and 60.

### Phase 2: Running PSIPRED V4.0 at UCL
1. Open the UCL PSIPRED server:
   `https://bioinf.cs.ucl.ac.uk/psipred/`
2. Enter your email address (or proceed as guest).
3. Paste the same human HBB sequence (`NP_000509.1`).
4. Select the prediction method: **PSIPRED 4.0 (Predict Secondary Structure)**.
5. Click **Submit**.
6. When the job completes, open the results page:
   - Inspect the graphical cartoon representation showing pink cylinders for $\alpha$-helices, yellow arrows for $\beta$-strands, and black lines for coils.
   - Notice the **Confidence (Conf)** track beneath the prediction (scores from 0 to 9).
   - Download or copy the single-letter text prediction string.

### Phase 3: Extracting Ground Truth DSSP Assignment from PDB 1A3N
1. Inspect the pre-computed crystallographic DSSP assignment from `../../data/expected/dssp_hbb_1a3n.txt`.
2. Notice the true experimental distribution of secondary structures for Chain B of human deoxyhemoglobin:
   - The globin fold is an **all-$\alpha$ helical protein** comprising 8 canonical $\alpha$-helices (labeled A, B, C, D, E, F, G, H) connected by non-helical loops.
   - The true crystallographic structure contains **0% $\beta$-sheet ($E$)**!

### Phase 4: Computing the Three-State Accuracy ($Q_3$) by Hand
1. Align the three 147-character strings vertically (Sequence, DSSP ground truth, GOR IV prediction, and PSIPRED prediction).
2. For GOR IV:
   - Compare each predicted state against the DSSP state at that exact position.
   - Mark `1` for match, `0` for mismatch.
   - Sum the total number of matches ($N_{\text{correct}}$).
   - Calculate:
     $$Q_3(\text{GOR IV}) = \frac{N_{\text{correct}}}{147} \times 100\%$$
3. For PSIPRED:
   - Repeat the position-by-position comparison against DSSP.
   - Sum the matches and calculate:
     $$Q_3(\text{PSIPRED}) = \frac{N_{\text{correct}}}{147} \times 100\%$$
4. Record your calculations in Table 11.2.

---

## 5. Offline Fallback Note

If the PBIL or UCL web servers are slow or queued:
- Use the complete pre-computed output files in `../../data/expected/`:
  - `gor4_hbb_secondary_structure.txt`
  - `psipred_hbb_secondary_structure.txt`
  - `dssp_hbb_1a3n.txt`
- All strings are 147 characters long and aligned for direct manual calculation.

---

## 6. Observations Table

### Table 11.1: Secondary Structure Composition Comparison for Human HBB
| Structural State | Crystallographic Truth (DSSP 1A3N Chain B) | GOR IV Prediction | PSIPRED V4.0 Prediction |
|---|:---:|:---:|:---:|
| **$\alpha$-Helix ($H$)** (Residue Count / %) | | | |
| **$\beta$-Strand ($E$)** (Residue Count / %) | 0 / 0.0% | | |
| **Coil / Loop ($C$)** (Residue Count / %) | | | |
| Total Residues | 147 / 100.0% | 147 / 100.0% | 147 / 100.0% |

### Table 11.2: Three-State Prediction Accuracy ($Q_3$) Calculation
| Method | Total Residues ($N_{\text{total}}$) | Correctly Predicted Residues ($N_{\text{correct}}$) | Number of Mismatches | Calculated $Q_3$ Accuracy (%) |
|---|:---:|:---:|:---:|:---:|
| **GOR IV** | 147 | | | |
| **PSIPRED V4.0** | 147 | | | |

### Table 11.3: Alignment of Ground Truth vs. Predictions (First 40 Residues)
```
Residue No: 1         10        20        30        40
Sequence:   MVHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQ
DSSP 1A3N:  CCHHHHHHHHHHHHHHHCCCCCCCCHHHHHHHHHHHCCCH
GOR IV:     [                                      ]
PSIPRED:    [                                      ]
```

---

## 7. Interpretation & Discussion Questions

1. **Why GOR IV Predicts Spurious $\beta$-Strands:** Inspect residues 40 to 46 (`FFESFGD`) in the GOR IV output. Why does GOR IV predict an extended $\beta$-strand (`EEEEEE`) in this region, whereas the true crystal structure has an $\alpha$-helix or loop? What local amino acid residues trigger this false-positive prediction?
2. **The Power of Evolutionary Profiles:** Why does PSIPRED achieve substantially higher accuracy ($>80\%$) than GOR IV (~65%)? How does incorporating a PSI-BLAST Position-Specific Scoring Matrix (PSSM) provide critical structural information that a single raw sequence cannot provide?
3. **The All-$\alpha$ Globin Fold:** Historically, hemoglobin and myoglobin were the first protein crystal structures solved (by Kendrew and Perutz). How many $\alpha$-helices comprise the canonical globin fold, and what structural feature maintains the stability of these helices in the absence of $\beta$-sheets?
4. **Limits of $Q_3$ Evaluation:** Why is the simple $Q_3$ percentage metric sometimes misleading when evaluating a protein with extreme class imbalance (e.g., a coiled-coil protein that is 95% $\alpha$-helical)? What complementary metrics (e.g., Matthew’s Correlation Coefficient, MCC, or Segment Overlap score, SOV) provide a fairer assessment?
5. **Modern Machine Learning in Secondary Structure:** Contemporary tools (AlphaFold2, ESMFold) bypass traditional three-state secondary structure prediction and predict full 3D atomic coordinates directly from multiple sequence alignments. Does this render secondary structure prediction obsolete, or does it still play a role in computational biology?

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Calculate the **Segment Overlap ($SOV$)** concept: Explain why predicting an $\alpha$-helix shifted by 1 residue produces a low $Q_3$ penalty per residue, but breaking a continuous 15-residue helix into two fragments severely damages structural modeling.
2. Inspect the confidence scores in PSIPRED: Are residues with confidence score $9$ significantly more accurate than residues with confidence score $2$? Compute the $Q_3$ accuracy restricted solely to high-confidence residues ($\text{Conf} \ge 7$).
