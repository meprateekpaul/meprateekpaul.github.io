# Instructor Answer Key & Evaluation Manual: Practical 10 (Protein Sequence Analysis)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S10 (Syllabus Practical P6)  
**Curriculum Topic:** Analyzing Protein Sequences: ProtParam, ProtScale, and PROSITE/InterPro  

---

## 1. Expected Outputs & Reference Solutions

### Table 10.1: Comparative Physicochemical Profiles (Completed)
*(Values calculated using Expasy ProtParam for NP_000509.1, HbS mutant, and P01308).*

| Physicochemical Parameter | Wild-Type HBB (`P68871`) | Sickle-Cell HbS Variant | Human Preproinsulin (`P01308`) |
|---|:---:|:---:|:---:|
| Sequence Length (aa) | 147 | 147 | 110 |
| Molecular Weight ($M_r$, Da) | 15,998.18 | 15,968.19 | 11,980.70 |
| Theoretical Isoelectric Point ($pI$) | **6.75** | **6.99** | **5.35** |
| Total Negative Residues (Asp + Glu) | 14 (Asp 3, Glu 11) | 13 (Asp 3, Glu 10) | 9 (Asp 0, Glu 9) |
| Total Positive Residues (Arg + Lys) | 14 (Arg 3, Lys 11) | 14 (Arg 3, Lys 11) | 6 (Arg 4, Lys 2) |
| Extinction Coefficient ($\epsilon_{280}$, $\text{M}^{-1}\text{cm}^{-1}$) | 8,480 | 8,480 | 5,840 |
| Instability Index ($II$) | 33.74 | 33.74 | 64.91 |
| Classification (Stable / Unstable) | **Stable** ($II < 40$) | **Stable** ($II < 40$) | **Unstable** ($II > 40$, prepro-form) |
| Aliphatic Index | 91.09 | 93.74 | 93.64 |
| Grand Average Hydropathicity (GRAVY) | **-0.111** | **-0.082** | **+0.125** (Signal peptide) |
| Primary Cellular Localization | Soluble Cytosolic | Soluble / Polymerizes | Secreted (Endoplasmic Reticulum) |

### Table 10.2: Functional Motif and Domain Annotations (Completed)
| Database | Accession / Identifier | Domain / Motif Name | Span Coordinates | Biological / Structural Function |
|---|:---:|:---:|:---:|---|
| **PROSITE** | `PS00017` | `GLOBLN` | ~Residues 50–110 | Globin proximal and distal heme pocket signature |
| **Pfam** | `PF00042` | Globin | 5–142 | Canonical globin fold comprising 8 $\alpha$-helices (A–H) |
| **InterPro** | `IPR000971` | Globin | 1–146 | Integrated family entry encompassing hemoglobins and myoglobins |
| **CATH / Gene3D** | `1.10.490.10` | Globin-like | 1–146 | Up-and-down orthogonal $\alpha$-helical bundle |

---

## 2. Sample ProtScale Hydropathy Output Guidance

```
ProtScale output for P68871 (HBB)
Scale: Kyte & Doolittle, Window: 9

   Hydropathy
     +2.0 |            *                    *           *
     +1.0 |           * *                  * *         * *
      0.0 |----------*---*----------------*---*-------*---*----- (Baseline)
     -1.0 |         *     *              *     *     *     *
     -2.0 |        *       *      *     *       *   *       *
     -3.0 |                 *    * *   *         * *
          +----------------------------------------------------> Residue Position
          1        25        50        75       100       125   147
          
Key Observations:
1. Peaks at residues 25-35 (B-helix), 70-80 (E-helix), and 110-120 (G-helix) correspond to
   buried hydrophobic core residues packing against the heme porphyrin ring.
2. Strong negative troughs correspond to surface loop turns (AB, CD, EF) and the hydrophilic
   distal/proximal histidines.
3. No segment exceeds +1.6, confirming the absence of transmembrane helices.
```

---

## 3. Model Answers to Discussion Questions

### Q1. Electrophoretic Shift of Sickle Hemoglobin
- **Model Answer:** At an alkaline pH of 8.6 (the standard buffer for clinical hemoglobin electrophoresis):
  - In wild-type HbA, the glutamic acid residue carries a fully ionized carboxylate group ($-1$ charge). The total net negative charge of the beta-chain tetramer is higher, causing HbA to migrate rapidly toward the positive anode ($+$).
  - In HbS, the E6V mutation replaces the negatively charged Glu with uncharged, neutral Valine. Each beta chain loses one negative charge, so the $\alpha_2\beta_2^S$ tetramer has **two fewer negative charges** (a net charge difference of $+2$ relative to HbA). Consequently, HbS experiences weaker electrostatic attraction to the anode and **migrates significantly more slowly toward the anode**, creating the distinct diagnostic electrophoretic band discovered by Linus Pauling.

### Q2. Molecular Basis of HbS Polymerization
- **Model Answer:** The E6V mutation positions a non-polar, branched hydrophobic valine side chain on the exposed surface of the A-helix. In the deoxygenated **T (tense) quaternary state**, hemoglobin undergoes an allosteric conformational shift that exposes a complementary hydrophobic pocket on the surface of an adjacent beta-chain, formed by **Phe-85 and Leu-88**. The mutant Val-6 fits into this hydrophobic pocket through van der Waals interactions. This intermolecular hydrophobic contact repeats across tetramers, driving the catastrophic crystallization of hemoglobin into long, insoluble 14-strand helical polymers that distort the erythrocyte into a rigid sickle shape.

### Q3. Interpreting the Instability Index
- **Model Answer:** Guruprasad’s Instability Index ($II$) evaluates the occurrence frequencies of 400 possible dipeptide pairs against an empirical threshold of $40$. 
  - For HBB, $II = 33.74$ ($<40$), predicting that the protein is thermodynamically and structurally **stable** *in vitro* (with a long intracellular half-life in reticulocytes).
  - If an engineered enzyme exhibits $II = 58.2$ ($>40$), it contains an overrepresentation of dipeptide combinations associated with rapid protein degradation, disordered segments, or protease susceptibility, predicting high susceptibility to unfolding, aggregation, or short *in vitro* shelf life.

### Q4. Aliphatic Index and Thermostability
- **Model Answer:** The aliphatic index is defined as the relative volume occupied by aliphatic side chains:
  $$\text{Aliphatic Index} = X(\text{Ala}) + a \cdot X(\text{Val}) + b \cdot (X(\text{Ile}) + X(\text{Leu}))$$
  where $a=2.9$ and $b=3.9$. For HBB, Alanine, Valine, and Leucine account for over 35% of the total sequence. These bulky aliphatic side chains pack tightly in the interior core of the globin fold, establishing extensive van der Waals contacts and excluding water molecules, which substantially increases the thermal denaturation melting temperature ($T_m$).

### Q5. GRAVY Score Thresholds
- **Model Answer:** The Grand Average of Hydropathicity (GRAVY) is the arithmetic mean of all Kyte-Doolittle residue values.
  - A negative value ($-0.111$ for HBB) indicates an overall hydrophilic, water-soluble globular protein that readily dissolves in aqueous cytosolic environments.
  - A strongly positive GRAVY score ($>+0.8$, as in bacteriorhodopsin or GPCRs) indicates a predominantly hydrophobic protein containing multiple stretches of 20–25 non-polar amino acids capable of thermodynamically integrating into the hydrocarbon interior of the lipid bilayer membrane.

---

## 4. Solution to Extension / Challenge Task

1. **Human Rhodopsin (P08100, 348 aa) ProtScale Analysis:**
   - Setting Kyte-Doolittle hydropathy scale with a window size of $W=21$ filters out minor local variations and isolates 20-residue spans.
2. **Resulting Profile:**
   - Yields **exactly 7 prominent peaks** exceeding the $+1.6$ hydropathy threshold:
     - Peak 1: ~Residues 35–55 (TM Helix 1)
     - Peak 2: ~Residues 72–95 (TM Helix 2)
     - Peak 3: ~Residues 108–130 (TM Helix 3)
     - Peak 4: ~Residues 150–172 (TM Helix 4)
     - Peak 5: ~Residues 200–225 (TM Helix 5)
     - Peak 6: ~Residues 250–275 (TM Helix 6)
     - Peak 7: ~Residues 285–310 (TM Helix 7)
3. **Biological Confirmation:** This profile matches the classical 7-transmembrane (7-TM) G-protein coupled receptor (GPCR) architecture.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & ProtParam Execution** | 2.0 | Deduct 0.5 if student fails to compute theoretical pI or MW. |
| **Comparative Table (Table 10.1 & 10.2)** | 4.0 | Deduct 0.5 per missing parameter or incorrect charge count. |
| **Hydropathy Analysis & ProtScale** | 2.0 | Deduct 0.5 if window size impact ($W=9$ vs $W=19$) is not understood. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question (HbS electrophoretic shift must be clearly explained). |
| **Total** | **10.0** | |
