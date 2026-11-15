# Lecture 23 — Physicochemical Properties

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 9:** Predictive Methods using Protein Sequence  
**Syllabus Topic:** Protein identification based on composition, Physical properties based on sequence  
**Primary Learning Outcome:** LO6 — Predict sequence-based features: calculate molecular weight, theoretical isoelectric point (pI), extinction coefficient, instability index, and hydropathy plots (ProtParam).

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: From 1D Sequence to Physical Chemistry
================================================================================
Topic: Macroscopic Biophysics from Microscopic Letters

[Visual: A 1D string of letters: N-MVHLTPEEKSAVTALWGKV...-C
         Transforming into:
         * Molecular Weight: 15,998 Da
         * Isoelectric Point (pI): 6.87
         * Extinction Coeff (280nm): 14,080 M^-1 cm^-1
         * Kyte-Doolittle Hydropathy Profile Curve]

Speaker Bullets:
* Before a biochemist purifies a recombinant protein in the lab, they compute its
  physical properties from sequence alone.
* Knowing the molecular weight, net charge, and solubility guides chromatography column
  selection, buffer design, and crystallisation conditions.
* Primary bioinformatics tool: **Expasy ProtParam**.
```

```
================================================================================
SLIDE 2: Molecular Weight Computation
================================================================================
Topic: Accounting for Condensation Chemistry

Formula:
  M_r(Protein) = [ Sum_{i=1}^N M_r(Amino Acid_i) ] - [ (N - 1) * 18.015 Da ]

  * Each peptide bond formation releases one molecule of water (H2O = 18.015 Da).
  * Monoisotopic Mass (Exact mass of most abundant isotope: 12C, 1H, 14N, 16O).
  * Average Mass (Weighted by natural isotopic abundance across elements).

Speaker Bullets:
* For human beta-globin (147 aa): Average mass = 15,998 Da (~16 kDa).
* Mass spectrometry measures mass with sub-dalton precision to confirm intact chains.
```

```
================================================================================
SLIDE 3: The Theoretical Isoelectric Point (pI)
================================================================================
Topic: Where Net Charge Equals Zero

  Definition:
  The isoelectric point (pI) is the exact pH at which the net electrical charge
  of the protein molecule is exactly ZERO: Q(pH) = 0.

[Visual: Net Charge Curve Q(pH) vs pH:
  At pH < pI: Net Charge is POSITIVE (+) --> Binds Cation Exchanger
  At pH = pI: Net Charge is ZERO (0)    --> Protein precipitates / least soluble!
  At pH > pI: Net Charge is NEGATIVE (-) --> Binds Anion Exchanger]

Speaker Bullets:
* At its pI, a protein has no electrostatic repulsion and often aggregates.
```

```
================================================================================
SLIDE 4: The 7 Ionizable Amino Acid Groups
================================================================================
Topic: Henderson-Hasselbalch Dissociation Constants

+--------------------+--------------------+--------------------+--------------+
| Ionizable Group    | Residue Class      | Average pKa (Bjellqvist) | State at pH 7|
+--------------------+--------------------+--------------------+--------------+
| C-Terminal Carboxyl| Terminal alpha-COOH| 3.6                | Deprotonated (-1)
| Aspartate (Asp, D) | Beta-Carboxyl      | 3.9                | Deprotonated (-1)
| Glutamate (Glu, E) | Gamma-Carboxyl     | 4.1                | Deprotonated (-1)
| Histidine (His, H) | Imidazole ring     | 6.0 - 6.5          | Neutral / +0.1
| N-Terminal Amino   | Terminal alpha-NH3+| 8.6                | Protonated (+1)
| Cysteine (Cys, C)  | Thiol (-SH)        | 8.5                | Neutral (0)
| Tyrosine (Tyr, Y)  | Phenolic -OH       | 10.1               | Neutral (0)
| Lysine (Lys, K)    | Epsilon-NH3+       | 10.5               | Protonated (+1)
| Arginine (Arg, R)  | Guanidinium        | 12.5               | Protonated (+1)
+--------------------+--------------------+--------------------+--------------+

Speaker Bullets:
* The net charge is the algebraic sum of all positive and negative groups.
* The algorithm uses the **Bisection Method** to iterate across pH [0..14] to find Q = 0.
```

```
================================================================================
SLIDE 5: The Sickle Cell Shift: Charge Alteration
================================================================================
Topic: Glu6Val Alters the Isoelectric Point

  Wild-Type Beta-Globin (HbA):
    Position 6: Glutamic Acid (Glu, E) --> Negative Charge (-1 at pH 7)
    Theoretical pI: **6.87**

  Sickle-Cell Variant (HbS):
    Position 6: Valine (Val, V)        --> Neutral Hydrophobic (0 charge)
    Theoretical pI: **7.10**

Speaker Bullets:
* Replacing one carboxyl group eliminates a negative charge, shifting the pI upwards!
* In 1949, Linus Pauling used moving-boundary electrophoresis at pH 8.6 to separate
  HbS from HbA, inaugurating the era of **Molecular Medicine**.
```

```
================================================================================
SLIDE 6: Molar Extinction Coefficient (Epsilon_280)
================================================================================
Topic: Quantifying Protein Concentration by UV Light

  Beer-Lambert Law: A = Epsilon * c * l

  Pace & Edelhoch Method (at 280 nm in 6M Guanidine-HCl):
    Epsilon_280 = (Count(Trp) * 5,500) + (Count(Tyr) * 1,490) + (Count(Cystine) * 125)

Speaker Bullets:
* Tryptophan and Tyrosine are the primary chromophores absorbing at 280 nm.
* Knowing $\epsilon_{280}$ allows you to calculate exact protein concentration in a spectrophotometer!
```

```
================================================================================
SLIDE 7: In Vitro Stability and Hydropathy Profiling
================================================================================
Topic: Guruprasad's Instability Index & Kyte-Doolittle

1. Guruprasad Instability Index (II):
   * Statistical weightings of dipeptide combinations:
     - II < 40  --> Predicted STABLE in test tube.
     - II > 40  --> Predicted UNSTABLE (half-life < 5 hours in vitro).
   * Human HBB: II ≈ 33.6 (Stable!).

2. Hydropathy Profiling (Kyte & Doolittle, 1982):
   * Assigns numerical hydropathy scores: Isoleucine (+4.5) to Arginine (-4.5).
   * Sliding window 9: Maps hydrophobic core vs surface-exposed loops.
   * Sliding window 19-21: Identifies 20-residue Transmembrane Helices!

Speaker Bullets:
* Hydropathy peaks spanning >+1.6 over 20 residues reliably predict membrane anchors.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 23

* Primary sequence determines mass, net charge, extinction, and stability.
* Theoretical pI is solved via bisection of the Henderson-Hasselbalch equation.
* Sickle-cell HbS (Glu6Val) increases pI from 6.87 to 7.10 via loss of an acid group.
* Extinction coefficient $\epsilon_{280}$ derives from Trp, Tyr, and Cystine counts.
* Kyte-Doolittle hydropathy plots identify transmembrane domains and surface loops.
* Next Lecture: Motifs, Patterns (PROSITE syntax), Pfam Domains, and InterPro.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Physics of Polypeptide Primary Structure

The primary amino acid sequence of a protein dictates its macroscopic biophysical behavior in solution. When an uncharacterized gene is translated, computational tools can predict:
- Its exact formula weight for mass spectrometry identification.
- Its net electrical charge across the physiological pH spectrum for ion-exchange chromatography.
- Its molar absorptivity ($\epsilon_{280}$) for optical spectrophotometric quantification.
- Its in vitro half-life and thermodynamic stability.
- Its hydropathy profile for identifying transmembrane membrane-spanning domains.

---

### 2. Theoretical Molecular Weight Computation

The molecular weight ($M_r$) of a protein of $N$ amino acid residues is calculated by summing the average atomic masses of all constituent amino acids and subtracting the mass of water molecules released during peptide bond condensation:

$$M_r(\text{Protein}) = \left( \sum_{i=1}^{N} M_r(\text{Residue}_i) \right) - (N - 1) \cdot M_r(\text{H}_2\text{O})$$

where $M_r(\text{H}_2\text{O}) = 18.0153\text{ Da}$.

#### Monoisotopic Mass vs Average Mass:
- **Monoisotopic Mass:** Calculated using the exact atomic mass of the single most abundant natural isotope of each element ($^{12}\text{C} = 12.0000$, $^{1}\text{H} = 1.0078$, $^{14}\text{N} = 14.0031$, $^{16}\text{O} = 15.9949$, $^{32}\text{S} = 31.9721$). Used in high-resolution Orbitrap mass spectrometry of small peptides.
- **Average Molecular Weight:** Calculated using the standard atomic weights of elements averaged across terrestrial isotopic abundances ($C = 12.011$, $H = 1.008$, $N = 14.007$, $O = 15.999$, $S = 32.065$). Used for whole proteins and routine biochemical assays.

For human beta-globin (`NP_000509.1`, 147 residues):
- Chemical Formula: $\text{C}_{722}\text{H}_{1166}\text{N}_{194}\text{O}_{214}\text{S}_3$
- Average Molecular Weight: $\mathbf{15,998.15\text{ Da}}$ ($\approx 16.0\text{ kDa}$).

---

### 3. The Theoretical Isoelectric Point (pI)

The **isoelectric point (pI)** is the specific environmental pH at which the net electrical charge of the protein molecule is exactly zero ($Q(\text{pH}) = 0$).

#### Henderson-Hasselbalch Formulation:
A protein is a polyampholyte bearing multiple weakly acidic and basic functional groups. According to the Henderson-Hasselbalch equation:
- The fraction of an acidic group that is negatively charged (deprotonated carboxylate, $-\text{COO}^-$) is:
  $$f_{\text{acid}} = \frac{10^{\text{pH} - pK_a}}{1 + 10^{\text{pH} - pK_a}} = \frac{1}{1 + 10^{pK_a - \text{pH}}}$$
- The fraction of a basic group that is positively charged (protonated amine, $-\text{NH}_3^+$) is:
  $$f_{\text{base}} = \frac{1}{1 + 10^{\text{pH} - pK_a}}$$

The net molecular charge $Q(\text{pH})$ of a protein containing $N_{\text{pos}}$ basic groups and $N_{\text{neg}}$ acidic groups is:

$$Q(\text{pH}) = \sum_{i=1}^{N_{\text{pos}}} \frac{1}{1 + 10^{\text{pH} - pK_i}} - \sum_{j=1}^{N_{\text{neg}}} \frac{1}{1 + 10^{pK_j - \text{pH}}}$$

```
  Standard pKa Scale in Proteins (Bjellqvist / Expasy Standard):
  * C-terminal alpha-carboxyl:  3.55
  * Aspartate (Asp, D):         4.05
  * Glutamate (Glu, E):         4.45
  * Cysteine (Cys, C):          9.00  (free -SH)
  * Tyrosine (Tyr, Y):          10.00 (phenolic -OH)
  * Histidine (His, H):         5.98  (imidazole ring)
  * N-terminal alpha-amino:     7.59
  * Lysine (Lys, K):            10.00 (epsilon-amino)
  * Arginine (Arg, R):          12.00 (guanidinium)
```

#### The Computational Algorithm: Bisection Search
Because the net charge equation $Q(\text{pH}) = 0$ is a monotonically decreasing non-linear function, software tools (such as Expasy **ProtParam**) solve for pI using the **Bisection Method**:
1. Set search interval: $\text{pH}_{\min} = 0.0$ (where $Q > 0$) and $\text{pH}_{\max} = 14.0$ (where $Q < 0$).
2. Calculate midpoint: $\text{pH}_{\text{mid}} = \frac{\text{pH}_{\min} + \text{pH}_{\max}}{2}$.
3. Evaluate $Q(\text{pH}_{\text{mid}})$.
4. If $|Q(\text{pH}_{\text{mid}})| < \epsilon$ (tolerance $10^{-4}$), report $\text{pH}_{\text{mid}}$ as the pI.
5. If $Q(\text{pH}_{\text{mid}}) > 0$, set $\text{pH}_{\min} = \text{pH}_{\text{mid}}$; otherwise, set $\text{pH}_{\max} = \text{pH}_{\text{mid}}$.
6. Repeat until convergence.

#### The Biophysical Consequence of Sickle Cell Anemia (*HbS*):
- In normal adult beta-globin (*HbA*), codon 6 encodes Glutamic acid, possessing a negatively charged carboxylate side chain ($pK_a \approx 4.45$). The theoretical pI of human beta-globin is **$\mathbf{6.87}$**.
- In sickle-cell beta-globin (*HbS*), codon 6 is mutated to Valine, a neutral aliphatic side chain ($-\text{CH(CH}_3)_2$).
- The loss of a negative carboxylate charge removes an acidic group from the net charge equation, shifting the net charge curve upward. Consequently, the theoretical pI of the HbS subunit shifts to **$\mathbf{7.10}$**.
- In 1949, Linus Pauling, Harvey Itano, S. J. Singer, and Ibert Wells performed moving-boundary electrophoresis on hemoglobin at $\text{pH} = 8.6$. At this pH:
  - HbA ($pI \approx 6.87$) has a net charge of $\approx -14$.
  - HbS ($pI \approx 7.10$) has a net charge of $\approx -12$ (two units less negative per $\alpha_2\beta_2$ tetramer).
  - HbA migrated significantly faster toward the positive anode than HbS, proving for the first time in human history that a genetic disease was caused by a specific physical alteration in the molecular charge of a protein.

---

### 4. Molar Extinction Coefficient ($\epsilon_{280}$)

According to the **Beer-Lambert Law**, the optical absorbance $A$ of a protein solution at wavelength $\lambda$ is:

$$A = \epsilon \cdot c \cdot l$$

where $\epsilon$ is the molar extinction coefficient ($\text{M}^{-1}\text{cm}^{-1}$), $c$ is molar concentration ($\text{mol/L}$), and $l$ is the pathlength of the quartz cuvette ($1.0\text{ cm}$).

Proteins absorb ultraviolet light strongly at $280\text{ nm}$ primarily due to the aromatic rings of **Tryptophan ($W$)** and **Tyrosine ($Y$)**, with a minor contribution from covalent **Cystine disulfide bonds ($-S-S-$)**.

Using the experimentally calibrated Edelhoch method (Pace et al., 1995) in $6.0\text{ M}$ Guanidine hydrochloride buffer:

$$\epsilon_{280} = (\text{Count}(W) \times 5,500) + (\text{Count}(Y) \times 1,490) + (\text{Count}(\text{Cystine}) \times 125) \quad [\text{M}^{-1}\text{cm}^{-1}]$$

---

### 5. In Vitro Stability and Hydropathy Profiling

#### Guruprasad's Instability Index ($II$)
K. Guruprasad, B. V. Reddy, and M. W. Pandit (1990) surveyed 32 proteins of known in vivo stability and discovered that a protein's stability is correlated with the occurrence of specific dipeptide combinations. They calculated a $20 \times 20$ statistical dipeptide weight matrix $DIWV$:

$$II = \frac{10}{L} \sum_{i=1}^{L-1} DIWV(x_i, x_{i+1})$$

- If $II < 40$: The protein is predicted to be **stable in vitro**.
- If $II > 40$: The protein is predicted to be **unstable in vitro** (susceptible to rapid proteolytic degradation; half-life $< 5\text{ hours}$ in reticulocyte lysates).
- For human beta-globin, $II \approx \mathbf{33.6}$, correctly classifying it as an exceptionally stable globular protein.

#### Kyte-Doolittle Hydropathy Profiling
Published by Jack Kyte and Russell Doolittle in 1982, this algorithm assigns an empirical hydropathy value to each of the 20 amino acids based on water-vapor transfer free energies and interior-versus-exterior distribution in known crystal structures:
- Most hydrophobic: **Isoleucine ($+4.5$)**, **Valine ($+4.2$)**, **Leucine ($+3.8$)**, **Phenylalanine ($+2.8$)**.
- Most hydrophilic: **Arginine ($-4.5$)**, **Lysine ($-3.9$)**, **Aspartate ($-3.5$)**, **Glutamate ($-3.5$)**.

A sliding window of width $W$ computes the average hydropathy score across the protein tape:
1. **Window Size $W = 9$:** Optimal for identifying surface-exposed hydrophilic turns and buried hydrophobic globular cores.
2. **Window Size $W = 19 \text{ to } 21$:** Optimal for detecting **transmembrane $\alpha$-helices**. A continuous span of 20 amino acids requires an average Kyte-Doolittle score $\ge +1.6$ to spontaneously traverse the $30\text{ \AA}$ hydrophobic hydrocarbon core of a phospholipid bilayer.

---

## Worked Example: Hand Calculations of Extinction Coefficient and Net Charge

### Part 1: Calculating $\epsilon_{280}$ for Human Beta-Globin
Examining the primary sequence of human beta-globin (`NP_000509.1`, 147 amino acids):
- Tryptophan ($W$) count: **2** (Trp15, Trp37)
- Tyrosine ($Y$) count: **3** (Tyr35, Tyr130, Tyr145)
- Cysteine ($C$) count: **2** (Cys93, Cys112) — In mature cytoplasmic hemoglobin, these exist as free reduced thiols ($-SH$), with **0 disulfide bonds**.

#### Calculation:
$$\epsilon_{280} = (2 \times 5,500) + (3 \times 1,490) + (0 \times 125)$$
$$\epsilon_{280} = 11,000 + 4,470 + 0 = \mathbf{15,470\text{ M}}^{-1}\text{cm}^{-1}$$

If an absorbance of $A_{280} = 0.7735$ is measured in a 1-cm cuvette:
$$c = \frac{A}{\epsilon \cdot l} = \frac{0.7735}{15,470 \times 1.0} = 5.0 \times 10^{-5}\text{ M} = \mathbf{50\text{ }\mu\text{M}}$$
Multiplying by molecular weight ($15,998\text{ g/mol}$):
$$\text{Concentration} = (50 \times 10^{-6}\text{ mol/L}) \times 15,998\text{ g/mol} \approx \mathbf{0.80\text{ mg/mL}}$$

---

### Part 2: Estimating Net Charge of a Peptide at pH 7.0
Consider the N-terminal tripeptide fragment of beta-globin:
$$\text{Sequence: } \text{N-terminal - Val - His - Leu - C-terminal}$$
Ionizable groups present:
1. N-terminal $\alpha$-amino group: $pK_a \approx 8.6$
2. Histidine imidazole ring: $pK_a \approx 6.0$
3. C-terminal $\alpha$-carboxyl group: $pK_a \approx 3.6$

#### Charge Calculation at pH 7.0:
1. **N-terminal Amino ($pK_a = 8.6$):**
   $$\text{Charge} = +\frac{1}{1 + 10^{7.0 - 8.6}} = +\frac{1}{1 + 10^{-1.6}} = +\frac{1}{1 + 0.025} \approx \mathbf{+0.975}$$
2. **Histidine Imidazole ($pK_a = 6.0$):**
   $$\text{Charge} = +\frac{1}{1 + 10^{7.0 - 6.0}} = +\frac{1}{1 + 10^{1.0}} = +\frac{1}{1 + 10} = +\frac{1}{11} \approx \mathbf{+0.091}$$
3. **C-terminal Carboxyl ($pK_a = 3.6$):**
   $$\text{Charge} = -\frac{1}{1 + 10^{3.6 - 7.0}} = -\frac{1}{1 + 10^{-3.4}} = -\frac{1}{1 + 0.0004} \approx \mathbf{-1.000}$$

#### Net Charge Sum:
$$Q(\text{pH } 7.0) = (+0.975) + (+0.091) + (-1.000) = \mathbf{+0.066} \approx \mathbf{0}$$
At physiological pH 7.0, this tripeptide is virtually neutral, with its isoelectric point located very close to $\text{pH} \approx 7.3$.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A biochemist attempts to measure the concentration of a purified 10-kDa recombinant protein using UV spectrophotometry at $280\text{ nm}$. The spectrophotometer reads an absorbance of $0.000$, yet a Bradford dye-binding assay reveals high protein concentration. Inspection of the amino acid sequence reveals that the protein completely lacks Tryptophan and Tyrosine residues. Explain why the $280\text{ nm}$ measurement failed, and what alternative UV wavelength could be utilized.

**Model Answer:**
- **Why $280\text{ nm}$ failed:** Optical absorbance at $280\text{ nm}$ depends almost exclusively on the conjugated aromatic ring systems of Tryptophan ($\epsilon = 5,500$) and Tyrosine ($\epsilon = 1,490$). If a protein lacks Trp and Tyr residues, its molar extinction coefficient $\epsilon_{280} \approx 0$, making it completely invisible to UV spectrophotometers at $280\text{ nm}$.
- **Alternative Wavelength:** Measure absorbance in the **far-UV range at $205\text{ nm}$ or $214\text{ nm}$**. At this wavelength, light is absorbed by the repeating **peptide bonds** ($-CO-NH-$) of the polypeptide backbone, allowing universal quantification of all proteins regardless of aromatic residue composition.

---

### Question 2
**Prompt:** Why does a Kyte-Doolittle hydropathy window of size $W = 7$ fail to identify transmembrane $\alpha$-helices in membrane transport proteins, whereas a window of $W = 19$ detects them with high accuracy?

**Model Answer:**
- **Window Size $W = 7$:** A 7-residue window is too narrow; it captures short local fluctuations in hydrophobicity, such as the hydrophobic face of an amphipathic surface helix or buried interior loop, producing excessive high-frequency noise.
- **Window Size $W = 19$:** An $\alpha$-helix requires 3.6 amino acids per turn, with a translation of $1.5\text{ \AA}$ per residue. To span the hydrocarbon core of a standard biological lipid bilayer ($30\text{ \AA}$ thick), an $\alpha$-helix must be at least $\frac{30\text{ \AA}}{1.5\text{ \AA/residue}} = \mathbf{20\text{ residues}}$ long. A window of size 19 to 21 matches the physical thickness of the cell membrane, smoothing out short fluctuations and selectively highlighting continuous hydrophobic transmembrane anchors.

---

### Question 3
**Prompt:** If human normal hemoglobin (HbA) and sickle-cell hemoglobin (HbS) are subjected to isoelectric focusing on a gel with a immobilized pH gradient spanning from pH 6.0 to pH 8.0, which protein will stop migrating closer to the cathode (negative electrode)? Explain why based on pI.

**Model Answer:**
In isoelectric focusing, proteins migrate through an electrical field until they reach the exact pH corresponding to their isoelectric point ($pI$), where their net charge becomes zero and electrical migration halts. 
- Normal HbA has a theoretical $pI \approx 6.87$.
- Sickle-cell HbS (due to the loss of a negatively charged Glutamic acid residue at position 6) has a higher $pI \approx 7.10$.
- Because higher pH values are located toward the **cathode (negative electrode)**, **sickle-cell hemoglobin (HbS) will migrate further toward the cathode** and focus at $\text{pH } 7.10$, while normal HbA will focus closer to the anode at $\text{pH } 6.87$.
