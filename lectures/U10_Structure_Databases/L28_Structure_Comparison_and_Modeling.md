# Lecture 28 — Structure Comparison and Modeling

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 10:** Structure Databases  
**Syllabus Topic:** Structure similarity searching, Advanced structure modeling  
**Primary Learning Outcome:** LO7 — Compare macromolecular structures using RMSD, query structural neighbors (VAST/DALI), evaluate homology models, and interpret AlphaFold predictions.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Structure is More Conserved than Sequence
================================================================================
Topic: Cyrus Chothia & Arthur Lesk's Law (1986)

[Visual: Superposition of Human Hemoglobin Beta vs Sperm Whale Myoglobin:
  Sequence Identity: ONLY 26% (Diverged ~500 million years ago!)
  Backbone RMSD: 1.45 Angstroms! (The 8 alpha-helices superimpose almost perfectly!)]

Speaker Bullets:
* Primary sequences diverge through neutral mutations and genetic drift.
* Secondary and tertiary folding topology is fiercely protected by natural selection.
* Over evolutionary time, **3D structure is 3 to 10 times more conserved than sequence**.
* Structural comparison reveals ancient evolutionary homologies invisible to BLAST.
```

```
================================================================================
SLIDE 2: Quantifying Structural Similarity: RMSD
================================================================================
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

Speaker Bullets:
* Before computing RMSD, the two structures must be optimally superimposed in space!
```

```
================================================================================
SLIDE 3: Structural Superimposition: The Kabsch Algorithm (1976)
================================================================================
Topic: Wolfgang Kabsch's Rigid-Body SVD Optimization

[Visual: Rotating and translating Structure Y onto Structure X:
  Step 1: Translate centroids of both structures to the origin (0, 0, 0).
  Step 2: Compute Covariance Matrix of equivalent atomic coordinates.
  Step 3: Perform Singular Value Decomposition (SVD) -> Extract optimal 3x3 Rotation Matrix U.
  Step 4: Rotate Structure Y to MINIMIZE the sum of squared distances!]

Speaker Bullets:
* RMSD cannot be calculated until the optimal rotation matrix $U$ and translation vector $t$
  are solved. The Kabsch algorithm finds the global minimum analytically.
```

```
================================================================================
SLIDE 4: Structural Similarity Search Engines: DALI vs VAST+
================================================================================
Topic: Searching the PDB for 3D Structural Neighbors

1. DALI (Distance Alignment Matrix — Liisa Holm & Chris Sander):
   * Internal 2D contact distance matrices (coordinate frame independent).
   * Aligns internal contact patterns like a fingerprint.

2. VAST / VAST+ (Vector Alignment Search Tool — NCBI MMDB):
   * Represents secondary structure elements (helices and sheets) as 3D vectors.
   * Aligns vector geometry rapidly to identify structural neighbors across the PDB.

Speaker Bullets:
* When a novel protein structure is solved, DALI and VAST instantly reveal whether
  its fold has ever been observed before.
```

```
================================================================================
SLIDE 5: The Three Classic Modeling Paradigms
================================================================================
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

Speaker Bullets:
* If a close homolog exists in the PDB (>30% identity), use Homology Modeling.
```

```
================================================================================
SLIDE 6: Stereochemical Model Validation: The Ramachandran Plot
================================================================================
Topic: Gopalasamudram Ramachandran's Dihedral Map (1963)

[Visual: Ramachandran Plot (phi vs psi angles):
  Top-Left: Beta-Sheet Region (phi ≈ -120, psi ≈ +130)
  Middle-Left: Right-Handed Alpha-Helix (phi ≈ -57, psi ≈ -47)
  Top-Right: Left-Handed Alpha-Helix (Glycine only!)
  White Space: Disallowed steric clash regions (atoms bump into each other!)]

Speaker Bullets:
* Non-bonded atoms cannot occupy the same physical space (steric hindrance).
* A high-quality model (checked via PROCHECK / MolProbity) must have **>90%** of
  residues in the most favored core regions.
```

```
================================================================================
SLIDE 7: The Deep Learning Revolution: AlphaFold
================================================================================
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

Speaker Bullets:
* AlphaFold 2 solved the 50-year-old protein folding challenge at CASP14.
* Replaces classical molecular dynamics with attention-based deep learning.
```

```
================================================================================
SLIDE 8: Reading AlphaFold Confidence: pLDDT and PAE
================================================================================
Topic: How to Interpret an AlphaFold Prediction

  pLDDT (Predicted Local Distance Difference Test: 0 to 100):
  * > 90 (Dark Blue):  VERY HIGH confidence; reliable down to side-chain rotamers.
  * 70 - 90 (Light Blue): CONFIDENT; backbone topology highly reliable.
  * 50 - 70 (Yellow):     LOW confidence; overall fold plausible, loops uncertain.
  * < 50 (Orange):        VERY LOW confidence; represents **Intrinsically Disordered**
                          Regions (IDRs) that have no fixed 3D structure!

Speaker Bullets:
* Never mistake low pLDDT for an AlphaFold failure; it usually reflects true biological disorder!
```

---

## Detailed Comprehensive Technical Notes

### 1. The Conservation Principle of Macromolecular Structure

In 1986, Cyrus Chothia and Arthur M. Lesk published an empirical benchmark that became a cornerstone of structural biology: the relationship between sequence divergence and structural divergence.

Analyzing homologous protein families, they demonstrated that as sequence identity drops:
- Across the range of **$100\%$ down to $\approx 35\%$ sequence identity**, the core secondary structure backbones superimpose tightly, with root-mean-square deviations ($\text{RMSD}$) remaining below **$1.5\text{ \AA}$**.
- Below $30\%$ sequence identity (the "Twilight Zone"), primary sequence alignments become highly error-prone, yet the overall tertiary architecture (folding topology) is maintained.
- Amino acid substitutions that preserve side-chain volume and hydrophobicity within the interior core allow millions of years of sequence divergence while preserving the identical 3D scaffold.

---

### 2. Mathematical Measurement of Structural Similarity: RMSD

To compare two protein structures, their atomic coordinates must be superimposed into a common reference frame. The universal metric of structural divergence is the **Root-Mean-Square Deviation (RMSD)**.

Given two structures $X$ and $Y$ sharing $N$ equivalent aligned atoms (standardly the $\text{C}_\alpha$ backbone atoms):
- Let $\mathbf{x}_i = (x_{i, 1}, x_{i, 2}, x_{i, 3})$ denote the Cartesian coordinates of atom $i$ in Structure $X$.
- Let $\mathbf{y}_i = (y_{i, 1}, y_{i, 2}, y_{i, 3})$ denote the Cartesian coordinates of atom $i$ in Structure $Y$ **after optimal rigid-body transformation**.

The RMSD is defined as:

$$\text{RMSD} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} d_i^2} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} ||\mathbf{x}_i - \mathbf{y}_i||^2}$$

$$\text{RMSD} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} \left[ (x_{i} - y_{i})^2 + (y_{i} - y_{i})^2 + (z_{i} - z_{i})^2 \right]}$$

#### The Kabsch Algorithm (Wolfgang Kabsch, 1976):
Calculating RMSD requires finding the optimal translation vector $\mathbf{t}$ and $3 \times 3$ proper orthogonal rotation matrix $U$ ($\det(U) = +1, U^T U = I$) that minimizes the objective function:

$$E(U, \mathbf{t}) = \sum_{i=1}^{N} ||\mathbf{x}_i - (U \mathbf{y}_i + \mathbf{t})||^2$$

The Kabsch algorithm solves this analytically in four steps:
1. **Centroid Alignment:** Translate both structures so their centers of mass coincide at the coordinate origin $(0, 0, 0)$:
   $$\mathbf{x}_i' = \mathbf{x}_i - \frac{1}{N}\sum \mathbf{x}_k, \quad \mathbf{y}_i' = \mathbf{y}_i - \frac{1}{N}\sum \mathbf{y}_k$$
2. **Covariance Matrix:** Compute the $3 \times 3$ cross-dispersion matrix:
   $$R = \sum_{i=1}^{N} \mathbf{y}_i' (\mathbf{x}_i')^T$$
3. **Singular Value Decomposition (SVD):** Decompose $R$ using SVD:
   $$R = V S W^T$$
4. **Optimal Rotation:** The optimal rotation matrix minimizing RMSD is:
   $$U = W \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & \det(W V^T) \end{pmatrix} V^T$$

#### Limitations of RMSD and the TM-Score:
While universal, RMSD suffers from two major mathematical flaws:
1. It is dominated by a few localized, flexible outlier loops: two structures sharing identical cores but differing in one mobile loop can have an artificially inflated RMSD of $>4\text{ \AA}$.
2. It scales with protein length $N$ (a 1,000-residue alignment naturally has a higher RMSD than a 50-residue peptide).

To overcome this, Yang Zhang and Jeffrey Skolnick (2004) developed the **TM-Score (Template Modeling Score)**:

$$\text{TM-Score} = \frac{1}{L_{\text{target}}} \sum_{i=1}^{L_{\text{common}}} \frac{1}{1 + \left( \frac{d_i}{d_0(L_{\text{target}})} \right)^2}$$

where $d_0 = 1.24 \sqrt[3]{L - 15} - 1.8$. 
- The TM-Score ranges strictly from **$0.0$ to $1.0$**.
- **$\text{TM-Score} > 0.5$:** Confirms that the two proteins share the **same global tertiary fold** with statistical significance ($P < 10^{-5}$), independent of protein length.
- **$\text{TM-Score} < 0.17$:** Indicates a random, non-homologous structural match.

---

### 3. Structural Similarity Search Engines

When an experimentalist solves a new structure whose primary sequence shows no BLAST hits, they query 3D structural search engines:

1. **DALI (Distance Alignment Matrix — Liisa Holm & Chris Sander):**  
   DALI completely bypasses coordinate superimposition by calculating internal **2D contact distance matrices** (the distance between every atom $i$ and atom $j$ within the protein). Because internal distances are invariant to spatial rotation or translation, DALI aligns overlapping sub-matrices like a 2D contact fingerprint.
2. **VAST / VAST+ (Vector Alignment Search Tool — NCBI MMDB):**  
   VAST simplifies the complexity of atomic coordinates by reducing every $\alpha$-helix and $\beta$-strand into a 3D geometric line vector. It aligns the relative angles, lengths, and spatial distances of these vectors, rapidly screening the entire PDB in seconds.

---

### 4. Computational Structure Modeling Pipelines

```
  Step 1: Template Selection (BLAST / HHpred against PDB; select template with >30% identity)
             |
             v
  Step 2: Target-Template Alignment (Needleman-Wunsch / Profile alignment; resolve gaps in loops)
             |
             v
  Step 3: Backbone Generation (Copy coordinates from template for aligned core regions)
             |
             v
  Step 4: Loop Modeling (Model insertions/deletions via ab initio or fragment database insertion)
             |
             v
  Step 5: Side-Chain Rotamer Packing (Select optimal low-energy rotamers from backbone-dependent libraries)
             |
             v
  Step 6: Energy Minimization (Resolve steric clashes using molecular mechanics force fields: AMBER/CHARMM)
             |
             v
  Step 7: Stereochemical Validation (Ramachandran plot, MolProbity, PROCHECK, QMEAN)
```

#### The Ramachandran Plot (G. N. Ramachandran, 1963):
Evaluates the torsional angles $\phi$ ($C-N-C_\alpha-C$) and $\psi$ ($N-C_\alpha-C-N$) of the polypeptide backbone. Because non-bonded atoms cannot approach closer than their Van der Waals radii:
- **Core / Favored Regions:** Stereochemically optimal conformations corresponding to right-handed $\alpha$-helices (around $\phi \approx -60^\circ, \psi \approx -50^\circ$) and $\beta$-sheets (around $\phi \approx -130^\circ, \psi \approx +140^\circ$).
- **Allowed Regions:** Marginally acceptable angles.
- **Disallowed Regions:** Sterically forbidden conformations where the carbonyl oxygen or $\beta$-carbon atoms clash violently with backbone amides.
- *Exceptions:* **Glycine** lacks a $\beta$-carbon (side chain is $-H$), permitting it to adopt conformations throughout all four quadrants of the plot. **Proline** has its side chain cyclized back onto the backbone nitrogen, locking $\phi$ rigidly to $-65^\circ \pm 15^\circ$.

---

### 5. The AlphaFold Deep Learning Paradigm

In 2020 at the 14th Critical Assessment of Structure Prediction (CASP14), **AlphaFold 2** (developed by DeepMind under John Jumper and Demis Hassabis) demonstrated atomic accuracy comparable to experimental X-ray crystallography, fundamentally solving the computational protein folding problem.

#### Key Architectural Innovations:
1. **End-to-End Deep Learning:** Replaced fragmented homology/force-field pipelines with a unified, differentiable neural network architecture.
2. **The Evoformer:** An iterative 48-block neural module that simultaneously processes evolutionary co-variation from Multiple Sequence Alignments (MSAs) and spatial residue-pair geometry. It performs axial self-attention, allowing evolutionary conservation and spatial contact predictions to communicate and refine each other.
3. **The Structure Module:** Utilizes **Invariant Point Attention (IPA)** to directly predict 3D rotations and translations of each amino acid residue frame in Euclidean space without requiring intermediate 2D distance contact maps.

#### Reading AlphaFold Confidence Metrics:
- **pLDDT (Predicted Local Distance Difference Test):**  
  A per-residue confidence metric ranging from **$0$ to $100$**:
  - **$\mathbf{> 90}$ (Dark Blue):** Very high confidence. Backbone and side-chain rotamers are highly accurate; suitable for drug discovery and molecular docking.
  - **$\mathbf{70 - 90}$ (Light Blue):** Confident. Reliable backbone trace; overall fold correct.
  - **$\mathbf{50 - 70}$ (Yellow):** Low confidence. Backbone trace should be treated with caution.
  - **$\mathbf{< 50}$ (Orange):** Very low confidence. In most proteins, residues with $\text{pLDDT} < 50$ represent **Intrinsically Disordered Regions (IDRs)**—functional segments that are dynamically unstructured in isolation and fold only upon binding biological partners.
- **Predicted Aligned Error (PAE) Plots:**  
  A 2D matrix evaluating the expected positional error (in Ångströms) of residue $x$ when the structure is aligned on residue $y$. Essential for evaluating whether two domains in a multidomain protein maintain a rigid, fixed spatial orientation (low inter-domain PAE) or are connected by a flexible linker allowing independent motion (high inter-domain PAE).

---

## Worked Example: Hand Calculations of RMSD and Model Validation

### Problem:
A structural biologist superimposes an AlphaFold model of human beta-globin onto the experimental X-ray crystal structure `1A3N`. After optimal Kabsch alignment, three equivalent alpha-carbon ($C_\alpha$) atoms exhibit the following coordinate errors ($d_i$):
- Residue 1 (Val1 $C_\alpha$): $d_1 = \mathbf{0.80\text{ \AA}}$
- Residue 2 (His2 $C_\alpha$): $d_2 = \mathbf{1.20\text{ \AA}}$
- Residue 3 (Leu3 $C_\alpha$): $d_3 = \mathbf{1.00\text{ \AA}}$

1. Calculate the **Root-Mean-Square Deviation (RMSD)** for this 3-residue backbone segment.
2. If this trend holds across the full 147 residues of beta-globin, state whether the AlphaFold model has achieved experimental-grade accuracy.

---

### Step 1: Calculate the Square of Each Distance Error ($d_i^2$)
$$d_1^2 = (0.80)^2 = \mathbf{0.64\text{ \AA}}^2$$
$$d_2^2 = (1.20)^2 = \mathbf{1.44\text{ \AA}}^2$$
$$d_3^2 = (1.00)^2 = \mathbf{1.00\text{ \AA}}^2$$

---

### Step 2: Compute the Mean Squared Error
$$\text{Mean} = \frac{1}{N} \sum_{i=1}^{N} d_i^2 = \frac{0.64 + 1.44 + 1.00}{3} = \frac{3.08}{3} \approx \mathbf{1.0267\text{ \AA}}^2$$

---

### Step 3: Compute the Square Root (RMSD)
$$\text{RMSD} = \sqrt{1.0267} \approx \mathbf{1.013\text{ \AA}}$$

### Evaluation:
- The backbone RMSD is **$1.01\text{ \AA}$**.
- In structural biology, an RMSD of $\approx 1.0\text{ \AA}$ is considered **experimental crystal-grade accuracy** (within the margin of thermal B-factor vibration and crystal lattice packing differences).
- The AlphaFold model faithfully recapitulates the experimental ground-truth structure of human beta-globin.

---

## Formative In-Class Checks

### Question 1
**Prompt:** You align the 3D structures of human beta-globin (PDB `1A3N`) and lupin leghemoglobin (PDB `1GDJ`). They share only 15% primary sequence identity, yet their backbone RMSD across 120 aligned residues is $1.65\text{ \AA}$. What evolutionary principle does this result demonstrate?

**Model Answer:**
This result demonstrates the fundamental evolutionary principle that **macromolecular 3D structure is far more conserved over evolutionary time than primary amino acid sequence**. Despite accumulating extensive neutral mutations that degraded sequence identity down to the 15% twilight zone over hundreds of millions of years of divergence between plants and animals, purifying natural selection strictly maintained the tertiary packing of the eight $\alpha$-helices and the geometry of the haem-binding pocket to preserve the essential physiological function of reversible oxygen transport.

---

### Question 2
**Prompt:** A researcher predicts the 3D structure of a 500-residue human cell-surface receptor using AlphaFold. The AlphaFold DB entry shows that residues 1 to 350 have a pLDDT score of 93 (colored dark blue), while residues 351 to 500 have a pLDDT score of 35 (colored orange). The researcher claims: *"AlphaFold crashed on the C-terminus because the algorithm made a mistake."* Explain why the researcher's interpretation is scientifically incorrect, and provide the correct biological explanation.

**Model Answer:**
- **Why the claim is incorrect:** A low pLDDT score ($<50$) does not indicate an algorithmic bug or failure of AlphaFold. AlphaFold was trained on experimental crystal structures and learned the physical features that distinguish stably folded domains from unstructured segments.
- **Correct Biological Explanation:** Residues with $\text{pLDDT} < 50$ represent an **Intrinsically Disordered Region (IDR)** or flexible cytoplasmic tail. In living cells, this 150-residue C-terminal segment does not adopt a single static 3D fold in isolation; it exists as a dynamic, fluctuating conformational ensemble (often involved in cellular signaling, phosphorylation, or protein-protein interactions) that adopts a structured conformation only upon binding a partner protein.

---

### Question 3
**Prompt:** In a PROCHECK stereochemical validation report of a homology model, 12% of the amino acid residues fall into the "Disallowed" regions of the Ramachandran plot. Can this model be utilized for virtual drug screening? What biochemical defects does this high percentage indicate?

**Model Answer:**
- **Can it be utilized:** **No, this model must be rejected.** Publication-quality and drug-screening models require that $>90\%$ of residues reside in favored regions and $<1\%$ in disallowed regions.
- **Biochemical Defects:** A 12% disallowed rate indicates severe **steric clashes and distorted backbone geometry**. Non-bonded atoms (such as main-chain carbonyl oxygens and side-chain $\beta$-carbons) are positioned closer together than their allowed Van der Waals contact distances, violating basic laws of chemical physics. Running drug docking on this model would yield meaningless binding energies because the binding pockets are warped.
