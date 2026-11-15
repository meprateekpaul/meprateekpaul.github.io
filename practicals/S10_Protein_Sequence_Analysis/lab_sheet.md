# Practical 10: Physicochemical Profiling and Functional Domain Analysis of Protein Sequences

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S10 (Syllabus Practical P6)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO6 — Predict protein properties from primary sequence, compute physicochemical parameters (MW, pI, GRAVY, instability), analyze hydropathy profiles, and identify functional sequence motifs/domains using PROSITE and InterPro.

---

## 1. Aim & Objectives

### Aim
To compute and interpret the fundamental physicochemical parameters of protein sequences using Expasy ProtParam, map hydropathy and membrane-spanning propensities using Expasy ProtScale, and identify signature sequence motifs, fingerprint patterns, and conserved evolutionary domains using PROSITE and InterPro.

### Objectives
1. Compute the molecular weight ($M_r$), theoretical isoelectric point ($pI$), amino acid composition, atomic composition, extinction coefficient, half-life, instability index ($II$), aliphatic index, and Grand Average of Hydropathicity (GRAVY) for human hemoglobin subunit beta (`P68871`).
2. Compare the physicochemical profile of wild-type HBB against the sickle cell variant HbS (`hbs_human_protein.fasta`), analyzing the biophysical impact of the Glu6Val substitution on net charge and solubility.
3. Contrast a soluble cytosolic globular protein (HBB) against a secreted/membrane-associated protein (Human Preproinsulin, `P01308` / `ins_human_protein.fasta`).
4. Generate and interpret Kyte-Doolittle hydropathy plots in Expasy ProtScale with varying sliding window sizes ($W=7, 9, 19, 21$).
5. Screen protein sequences against the **PROSITE** database of functional motifs and patterns to identify globin family signatures (e.g., `PS00017` / `GLOBLN`).
6. Query **InterPro** to integrate cross-database domain family annotations (Pfam, SMART, CDD, SUPERFAMILY).

---

## 2. Background & Scientific Principle

### Physicochemical Parameters from Primary Sequence
A protein's primary amino acid sequence dictates its three-dimensional tertiary structure and biochemical behavior. Key computational parameters include:
1. **Molecular Weight ($M_r$):** The sum of the average isotopic masses of all amino acids minus the mass of water molecules ($18.015\text{ Da}$) lost during peptide bond condensation.
2. **Theoretical Isoelectric Point ($pI$):** The specific pH at which the net electrical charge of the protein molecule equals zero. Below its $pI$, a protein carries a net positive charge; above its $pI$, it carries a net negative charge. At pH = $pI$, electrostatic repulsion between protein molecules is minimized, making proteins least soluble and most prone to precipitation.
3. **Extinction Coefficient ($\epsilon$):** Quantifies light absorption at $\lambda = 280\text{ nm}$ in water:
   $$\epsilon_{280} = (\text{Count}_{\text{Trp}} \times 5500) + (\text{Count}_{\text{Tyr}} \times 1490) + (\text{Count}_{\text{Cystine}} \times 125)\quad [\text{M}^{-1}\text{cm}^{-1}]$$
4. **Instability Index ($II$):** Developed by Guruprasad et al. (1990) to predict *in vitro* protein stability. Dipeptide combinations are assigned statistical weight values based on occurrence frequencies in stable vs. unstable proteins. A value $<40$ classifies the protein as **stable**; a value $>40$ predicts it is **unstable**.
5. **Grand Average of Hydropathicity (GRAVY):** The sum of the hydropathy values of all amino acids divided by sequence length. Negative values indicate **hydrophilic, soluble globular proteins**; positive values indicate **hydrophobic, transmembrane or membrane-associated proteins**.

### Hydropathy Profiling (The Kyte-Doolittle Method)
Jack Kyte and Russell Doolittle (1982) assigned an empirical hydropathy value to each of the 20 standard amino acids based on water-vapor transfer free energies and interior-versus-surface structural distributions (e.g., Isoleucine $= +4.5$, Valine $= +4.2$, Arginine $= -4.5$).
- A **sliding window** of size $W$ moves along the sequence one residue at a time. The average hydropathy of residues within the window is plotted against the central window position.
- **Window size selection:**
  - $W = 7$ to $9$ : Optimal for revealing surface hydrophilic turns, flexible antigenic loops, and solvent-exposed patches.
  - $W = 19$ to $21$ : Optimal for identifying 20-residue **transmembrane $\alpha$-helices** spanning the hydrophobic lipid bilayer (peaks exceeding $+1.6$).

### Motifs, Signatures, and Domain Databases
- **PROSITE:** A curated database of biologically significant sequence motifs and patterns. A regular expression pattern defines strict consensus rules (e.g., `[LIVMF]-x-H-x(3)-[DENQ]`).
- **Pfam / InterPro:** Uses probabilistic Profile Hidden Markov Models (HMMs) to capture position-specific amino acid variability, allowing detection of divergent domain families that rigid regular expression patterns miss.

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & URLs
- Expasy ProtParam: [https://web.expasy.org/protparam/](https://web.expasy.org/protparam/)
- Expasy ProtScale: [https://web.expasy.org/protscale/](https://web.expasy.org/protscale/)
- ScanProsite: [https://prosite.expasy.org/scanprosite/](https://prosite.expasy.org/scanprosite/)
- EMBL-EBI InterPro: [https://www.ebi.ac.uk/interpro/](https://www.ebi.ac.uk/interpro/)

### Input Datasets & Accessions
- Human Hemoglobin Beta (Wild-type): `NP_000509.1` / UniProt `P68871` (147 aa)
  - File: `../../data/sequences/hbb_human_protein.fasta`
- Sickle Cell Hemoglobin Beta (E6V Variant): HbS (147 aa)
  - File: `../../data/sequences/hbs_human_protein.fasta`
- Human Preproinsulin: `NP_000198.1` / UniProt `P01308` (110 aa)
  - File: `../../data/sequences/ins_human_protein.fasta`

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Physicochemical Analysis with Expasy ProtParam
1. Open [https://web.expasy.org/protparam/](https://web.expasy.org/protparam/).
2. In the query box, enter the UniProt accession `P68871` (or paste the FASTA sequence from `hbb_human_protein.fasta`).
3. Click **Compute Parameters**.
4. Examine the detailed output report and record:
   - Number of amino acids: `147`
   - Molecular weight: `15,998.18 Da` (~16.0 kDa)
   - Theoretical isoelectric point ($pI$): `6.75`
   - Total number of negatively charged residues (Asp + Glu): `14`
   - Total number of positively charged residues (Arg + Lys): `14`
   - Atomic formula ($C_{724}H_{1118}N_{194}O_{214}S_3$, Total atoms = `2,253`)
   - Extinction coefficient ($\epsilon_{280}$ with all Cys forming cystines vs. reduced Cys)
   - Estimated half-life in mammalian reticulocytes ($>30\text{ hours}$)
   - Instability index: `33.74` (Classified: **stable**)
   - Aliphatic index: `91.09`
   - Grand average of hydropathicity (GRAVY): `-0.111`
5. Repeat the calculation for the sickle-cell variant sequence from `../../data/sequences/hbs_human_protein.fasta`.
   - Observe how mutating Glu (negatively charged) to Val (neutral, hydrophobic) alters the total negative charges ($13$ vs. $14$) and shifts the theoretical $pI$ upwards.
6. Repeat for Human Preproinsulin (`P01308`). Record its values in Table 10.1.

### Phase 2: Hydropathy Profiling with Expasy ProtScale
1. Open [https://web.expasy.org/protscale/](https://web.expasy.org/protscale/).
2. Paste the human HBB sequence (`P68871`).
3. From the list of over 50 amino acid scales, select **Hphob. / Kyte & Doolittle**.
4. Click **Continue**.
5. Set parameters:
   - Window size: Enter **9** (standard for globular protein domain inspection).
   - Weight options: Default (uniform or linear).
6. Click **Submit**.
7. Examine the generated hydropathy curve:
   - Identify the peaks (positive values above 0) representing the interior hydrophobic faces of the alpha helices (e.g., residues ~25–35, ~65–75, ~110–120).
   - Identify the valleys (negative values below 0) corresponding to solvent-exposed hydrophilic loops and active site histidines.
8. Re-run the plot with Window size = **19**. Notice how the curve becomes much smoother. Observe that no peak exceeds $+1.6$, confirming that HBB is entirely soluble and lacks transmembrane spans.

### Phase 3: Motif and Domain Scanning with ScanProsite
1. Open [https://prosite.expasy.org/scanprosite/](https://prosite.expasy.org/scanprosite/).
2. In Option 1, enter `P68871`.
3. Check the box to exclude high-probability patterns (e.g., non-specific phosphorylation or N-glycosylation sites).
4. Click **Scan**.
5. Inspect the hit results:
   - Locate the signature: **`PS00017` / `GLOBLN`** (Globin family profile).
   - Read the documented consensus pattern describing the proximal and distal histidine pockets.

### Phase 4: Comprehensive Domain Annotation with InterPro
1. Navigate to EMBL-EBI InterPro: [https://www.ebi.ac.uk/interpro/](https://www.ebi.ac.uk/interpro/).
2. In the search box, paste the HBB sequence or enter `P68871`. Click **Search**.
3. View the integrated domain architecture:
   - **InterPro Entry:** `IPR000971` (Globin) and `IPR002339` (Globin-like superfamily).
   - Cross-database members:
     - Pfam: `PF00042` (Globin)
     - PROSITE Profile: `PS51061`
     - CATH / Gene3D: `1.10.490.10` (Orthogonal bundle)
     - SUPERFAMILY: `SSF46458` (Globin-like)

---

## 5. Offline Fallback Note

If Expasy or InterPro servers are unreachable:
- Compute basic physicochemical parameters using Python's `Bio.SeqUtils.ProtParam` package locally in the terminal:
  ```python
  from Bio.SeqUtils.ProtParam import ProteinAnalysis

  seq = "MVHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFESFGDLSTPDAVMGNPKVKAHGKKVLGAFSDGLAHLDNLKGTFATLSELHCDKLHVDPENFRLLGNVLVCVLAHHFGKEFTPPVQAAYQKVVAGVANALAHKYH"
  X = ProteinAnalysis(seq)
  print(
      f"MW: {X.molecular_weight():.2f}, pI: {X.isoelectric_point():.2f}, GRAVY:"
      f" {X.gravy():.3f}"
  )
  ```
- Detailed reference values and hydropathy tables are available in the instructor answer key.

---

## 6. Observations Table

### Table 10.1: Comparative Physicochemical Profiles (ProtParam)
| Physicochemical Parameter | Wild-Type HBB (`P68871`) | Sickle-Cell HbS Variant | Human Preproinsulin (`P01308`) |
|---|:---:|:---:|:---:|
| Sequence Length (aa) | 147 | 147 | 110 |
| Molecular Weight ($M_r$, Da) | 15,998.18 | | |
| Theoretical Isoelectric Point ($pI$) | 6.75 | | |
| Total Negative Residues (Asp + Glu) | 14 | | |
| Total Positive Residues (Arg + Lys) | 14 | | |
| Extinction Coefficient ($\epsilon_{280}$, $\text{M}^{-1}\text{cm}^{-1}$) | 8,480 | | |
| Instability Index ($II$) | 33.74 | | |
| Classification (Stable / Unstable) | Stable | | |
| Aliphatic Index | 91.09 | | |
| Grand Average Hydropathicity (GRAVY) | -0.111 | | |
| Primary Cellular Localization | Cytosolic | Cytosolic | Secreted / Hormone |

### Table 10.2: Functional Motif and Domain Annotations (PROSITE & InterPro)
| Database | Accession / Identifier | Domain / Motif Name | Span Coordinates | Biological / Structural Function |
|---|:---:|:---:|:---:|---|
| **PROSITE** | `PS00017` | `GLOBLN` | | Characteristic globin signature motif |
| **Pfam** | `PF00042` | Globin | | All-alpha helical globin fold |
| **InterPro** | `IPR000971` | Globin | | Oxygen-binding hemeprotein family |
| **CATH / Gene3D** | `1.10.490.10` | Globin-like | | Orthogonal alpha-helical bundle |

---

## 7. Interpretation & Discussion Questions

1. **Electrophoretic Shift of Sickle Hemoglobin:** Linus Pauling (1949) separated wild-type hemoglobin (HbA) from sickle-cell hemoglobin (HbS) using moving-boundary electrophoresis. Based on your ProtParam calculations for Table 10.1, explain why HbS migrates more slowly toward the positive anode (or faster toward the cathode) compared to HbA at alkaline pH (e.g., pH 8.6).
2. **Molecular Basis of HbS Polymerization:** The E6V mutation substitutes a charged, hydrophilic glutamic acid for a neutral, branched-chain valine on the outer surface of the A-helix. In deoxygenated T-state hemoglobin, what hydrophobic pocket on the adjacent beta-globin subunit does this mutant valine insert into, and why does this cause fiber polymer formation?
3. **Interpreting the Instability Index:** What does Guruprasad's Instability Index ($II = 33.74$) signify regarding the *in vitro* thermodynamic stability of HBB? If an engineered industrial enzyme yields an instability index of $58.2$, what does this predict about its bench-top degradation rate?
4. **Aliphatic Index and Thermostability:** The aliphatic index of HBB is relatively high ($91.09$). Which specific amino acids contribute to this index, and how does aliphatic side-chain packing contribute to globular stability?
5. **GRAVY Score Thresholds:** Explain the physical significance of a negative GRAVY score ($-0.111$) for HBB versus a strongly positive GRAVY score ($>+0.8$) for a multi-pass membrane protein like bacteriorhodopsin.

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Obtain the sequence of a classical multi-pass transmembrane protein (e.g., Human Rhodopsin, UniProt `P08100`, 348 aa).
2. Run Expasy ProtScale with the Kyte-Doolittle scale and a window size of $W=21$.
3. Count how many distinct peaks exceed the standard $+1.6$ hydropathy threshold.
4. Verify whether the number of high-hydropathy peaks matches the experimentally established number of transmembrane segments (7-transmembrane GPCR architecture).
