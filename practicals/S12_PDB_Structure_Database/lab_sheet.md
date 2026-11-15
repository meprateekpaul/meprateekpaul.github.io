# Practical 12: Introduction to the Protein Data Bank (PDB) and Macromolecular Structure Records

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S12 (Syllabus Practical P11)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO7 — Retrieve macromolecular structures, evaluate experimental quality metrics (resolution, R-factors), parse legacy PDB and mmCIF file records, and distinguish asymmetric units from biological assemblies.

---

## 1. Aim & Objectives

### Aim
To explore the architecture, experimental data models, and entry reports of the Protein Data Bank (RCSB PDB / wwPDB), dissect the anatomy of the classic PDB flat file format (`.pdb`), evaluate experimental validation metrics (resolution, R-value, R-free, Ramachandran outliers), and differentiate asymmetric units from quaternary biological assemblies using human hemoglobin structures (`1A3N`, `4HHB`, `2HBS`).

### Objectives
1. Understand the historical origin, organization, and worldwide governance of the Protein Data Bank (wwPDB: RCSB PDB, PDBe, PDBj).
2. Query RCSB PDB for the crystal structure of human adult deoxyhemoglobin (`1A3N`) and extract comprehensive entry metadata.
3. Critically evaluate structure determination methods (X-ray crystallography, Cryo-Electron Microscopy, NMR spectroscopy) and interpret quality metrics: Resolution ($\text{\AA}$), $R_{\text{work}}$, $R_{\text{free}}$, and clashscore.
4. Distinguish between the **Asymmetric Unit (ASU)** (the minimal crystallographic repeating unit) and the **Biological Assembly** (the functional quaternary complex).
5. Dissect the 80-column PDB flat file architecture: `HEADER`, `TITLE`, `COMPND`, `SOURCE`, `REMARK 2` (Resolution), `SEQRES`, `ATOM`, `HETATM`, `CONECT`, and `END`.
6. Contrast `1A3N` against high-resolution wild-type deoxyhemoglobin (`4HHB`, 1.74 $\text{\AA}$) and sickle-cell hemoglobin (`2HBS`).

---

## 2. Background & Scientific Principle

### The Protein Data Bank and wwPDB
Founded in 1971 at Brookhaven National Laboratory with just 7 structures, the **Protein Data Bank (PDB)** is the single global archive of 3D macromolecular structure data. Today, it is managed by the **Worldwide PDB (wwPDB)** consortium, comprising:
- **RCSB PDB** (Research Collaboratory for Structural Bioinformatics, USA)
- **PDBe** (Protein Data Bank in Europe, EMBL-EBI, UK)
- **PDBj** (Protein Data Bank Japan, Osaka University)
- **BMRB** (Biological Magnetic Resonance Bank, USA)

All four portals share identical atomic coordinates while providing specialized visualization, searching, and validation tools.

### Experimental Structure Determination Methods and Quality Metrics
1. **X-ray Crystallography:**
   - Accounts for ~85% of all PDB entries. Requires growing pure, 3D crystals of the macromolecule and measuring X-ray diffraction patterns (Bragg's law).
   - **Resolution ($d_{\text{min}}$, in Angstroms $\text{\AA}$):** Measures the finest detail resolvable in the electron density map.
     - $<1.5\text{ \AA}$ : Ultra-high resolution; individual atoms and water molecules clearly separated.
     - $1.5\text{ \AA} - 2.5\text{ \AA}$ : High/medium resolution; backbone, side-chain rotamers, and ligand orientations unambiguous (e.g., `4HHB` at 1.74 $\text{\AA}$, `1A3N` at 2.0 $\text{\AA}$).
     - $>3.0\text{ \AA}$ : Low resolution; general fold and helices visible, but atomic coordinates subject to fitting uncertainty.
   - **R-factor ($R_{\text{work}}$) and $R_{\text{free}}$:**
     $$R = \frac{\sum ||F_{\text{obs}}| - |F_{\text{calc}}||}{\sum |F_{\text{obs}}|}$$
     Measures the discrepancy between observed diffraction amplitudes ($F_{\text{obs}}$) and those calculated from the atomic model ($F_{\text{calc}}$).
     - A good crystallographic model typically has $R_{\text{work}} \le 0.20$ (20%).
     - **$R_{\text{free}}$:** Calculated against a randomly chosen 5%–10% test set of reflections never used during refinement, serving as an unbiased cross-validation metric against over-fitting.
2. **Cryo-Electron Microscopy (Cryo-EM):** Imaging vitrified, single macromolecular particles without crystallization; dominant for massive multi-protein complexes.
3. **Nuclear Magnetic Resonance (NMR):** Determines conformational ensembles of small flexible proteins in solution without crystallization.

### Asymmetric Unit vs. Biological Assembly
- **Asymmetric Unit (ASU):** The smallest portion of crystal structure that, to which crystallographic space group symmetry operations are applied, reconstructs the complete repeating crystal unit cell.
  - In `1A3N` (Space Group $P\,2_1\,2_1\,2$), the asymmetric unit contains **one $\alpha\beta$ heterodimer** (Chains A and B).
- **Biological Assembly:** The physiologically active quaternary oligomer in living cells.
  - For adult hemoglobin, the biological assembly is the **$\alpha_2\beta_2$ heterotetramer** (4 globin chains, 4 heme groups), generated by applying a 2-fold non-crystallographic crystallographic symmetry operation to the asymmetric unit.

### PDB Flat File Anatomy
Historically structured around 80-column punched computer cards:
- **`ATOM` Records:** Cartesian coordinates ($X, Y, Z$ in Angstroms), occupancy, and temperature factor ($B$-factor) of atoms belonging to standard amino acids or nucleic acids.
- **`HETATM` Records:** "Hetero-atoms" belonging to non-standard chemical groups: cofactors, prosthetic groups (e.g., `HEM` for heme), ions, inhibitors, and crystallographic water molecules (`HOH`).
- **`CONECT` Records:** Explicit covalent connectivity for ligands and disulfide bonds.

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & URLs
- RCSB PDB Primary Portal: [https://www.rcsb.org/](https://www.rcsb.org/)
- RCSB Entry Page for 1A3N: [https://www.rcsb.org/structure/1A3N](https://www.rcsb.org/structure/1A3N)
- RCSB Entry Page for 4HHB: [https://www.rcsb.org/structure/4HHB](https://www.rcsb.org/structure/4HHB)
- RCSB Entry Page for 2HBS: [https://www.rcsb.org/structure/2HBS](https://www.rcsb.org/structure/2HBS)

### Input Datasets & Local Files
- Local PDB Structure: `../../data/structures/1a3n.pdb` (Deoxyhemoglobin, 2.0 $\text{\AA}$)
- Local PDB Structure: `../../data/structures/4hhb.pdb` (High-resolution deoxyhemoglobin, 1.74 $\text{\AA}$)
- Local PDB Structure: `../../data/structures/2hbs.pdb` (Sickle-cell hemoglobin polymer)

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Querying RCSB PDB for `1A3N`
1. Navigate to [https://www.rcsb.org/](https://www.rcsb.org/).
2. In the top search bar, enter the 4-character PDB code: `1A3N` and press **Enter**.
3. Inspect the primary entry report:
   - **Title:** *Crystal structure of human adult deoxyhemoglobin at 2.0 angstroms resolution.*
   - **DOI:** Documenting Tame J.R. & Vallone B. (2000).
   - **Classification:** OXYGEN TRANSPORT.
   - **Organism:** *Homo sapiens*.
   - **Expression System:** *Escherichia coli*.
4. Inspect the **Experimental Data & Quality Metrics** banner:
   - Method: **X-RAY DIFFRACTION**.
   - Resolution: **2.00 $\text{\AA}$**.
   - $R$-Value Work: **0.177** (17.7%).
   - $R$-Value Free: **0.231** (23.1%).
   - Space Group: **$P\,2_1\,2_1\,2$**.

### Phase 2: Macromolecules, Ligands, and Quaternary Structure
1. Scroll down to the **Macromolecules** table:
   - Identify Entity 1: Hemoglobin subunit alpha (Chain A, 141 aa).
   - Identify Entity 2: Hemoglobin subunit beta (Chain B, 146 aa).
2. Scroll to the **Small Molecules / Ligands** table:
   - Identify the primary prosthetic group: **`HEM`** (Protoporphyrin IX containing $Fe$).
   - Identify buffer/crystallization salts: **`PO4`** (Phosphate ion).
3. Check the **Biological Assembly vs. Asymmetric Unit** toggle above the 3D viewer:
   - Switch between **Assembly 1** (Full $\alpha_2\beta_2$ tetramer, 4 chains) and **Asymmetric Unit** ($\alpha\beta$ dimer, 2 chains).

### Phase 3: Dissecting the PDB Flat File Anatomy (`1A3N.pdb`)
1. Open the local file `../../data/structures/1a3n.pdb` in a text editor (or click **Download Files** $\rightarrow$ **PDB Format** on RCSB).
2. Locate and inspect the following specific record blocks:
   - **Lines 1–10 (`HEADER`, `TITLE`):**
     Notice how columns 1–6 define the record type.
   - **`REMARK 2`:**
     Search for `REMARK   2`. Verify that it explicitly states `RESOLUTION.    2.00 ANGSTROMS.`
   - **`SEQRES`:**
     Observe the primary amino acid sequence listed in 3-letter codes for Chain A and Chain B.
   - **`ATOM` Records:**
     Locate the first atom of Chain A:
     ```
     ATOM      1  N   VAL A   1       6.261  16.744   4.902  1.00 48.72           N
     ```
     - Columns 7–11: Atom serial number (`1`)
     - Columns 13–16: Atom name (`N`, backbone amino nitrogen)
     - Columns 18–20: Residue name (`VAL`)
     - Column 22: Chain identifier (`A`)
     - Columns 23–26: Residue sequence number (`1`)
     - Columns 31–38: Orthogonal $X$ coordinate in $\text{\AA}$ (`6.261`)
     - Columns 39–46: Orthogonal $Y$ coordinate in $\text{\AA}$ (`16.744`)
     - Columns 47–54: Orthogonal $Z$ coordinate in $\text{\AA}$ (`4.902`)
     - Columns 55–60: Occupancy (`1.00`)
     - Columns 61–66: Temperature factor / $B$-factor (`48.72`)
     - Columns 77–78: Element symbol (`N`)
   - **`HETATM` Records:**
     Scroll down past all amino acids to find the `HETATM` records for `HEM` (heme iron and porphyrin carbon/nitrogen atoms) and `HOH` (water molecules).
   - **`CONECT` Records:**
     Notice the lines at the bottom specifying covalent bond connectivity between the heme iron ($Fe$) and the protoporphyrin ring nitrogens.
   - **`END`:** The final line of the record.

### Phase 4: Comparative Structure Analysis (`1A3N` vs. `4HHB` vs. `2HBS`)
1. Repeat the examination for `4HHB` (Fermi et al., 1.74 $\text{\AA}$ resolution).
   - Note the significantly lower (better) $R$-factor and sharper electron density.
2. Repeat for `2HBS` (Sickle-cell hemoglobin fiber).
   - Identify how many tetramers are present in the asymmetric unit (contains multiple tetramers forming the polymer fiber).
   - Locate the mutant residue Val-6 on the beta chains.

---

## 5. Offline Fallback Note

If the RCSB PDB web server is offline:
- All structure files (`1a3n.pdb`, `4hhb.pdb`, `2hbs.pdb`) are permanently archived locally in `../../data/structures/`.
- The PDB headers and remark blocks contain the full validation reports, resolution, space groups, and ligand lists accessible via standard text editors or terminal grep:
  ```bash
  grep "^REMARK   2" ../../data/structures/1a3n.pdb
  grep "^REMARK   3" ../../data/structures/1a3n.pdb | grep "R VALUE"
  ```

---

## 6. Observations Table

### Table 12.1: RCSB PDB Structure Profile for Human Deoxyhemoglobin (`1A3N`)
| Structural Metadata Field | Extracted Record Value | Significance / Explanation |
|---|---|---|
| PDB ID Code | `1A3N` | Unique 4-character alphanumeric identifier |
| Structure Title | | Full experimental title |
| Experimental Method | | X-ray diffraction, Cryo-EM, or NMR |
| Crystallographic Resolution ($\text{\AA}$) | | Limiting Bragg spacing in Angstroms |
| $R_{\text{work}}$ / $R_{\text{free}}$ | | Model vs. observed diffraction agreement |
| Space Group Symmetry | | Crystal unit cell space group |
| Number of Chains in Asymmetric Unit | | Distinct protein chains in ASU |
| Identity of Chains in Asymmetric Unit | | Alpha (Chain A), Beta (Chain B) |
| Stoichiometry of Biological Assembly | | Full functional quaternary oligomer |
| Bound Ligands / Cofactors (`HETATM`) | | Prosthetic groups (e.g., HEM, PO4) |
| Total Atom Count in File | | Sum of ATOM + HETATM records |

### Table 12.2: Cross-Structure Comparative Quality Metrics
| Metric | `1A3N` (Standard Deoxy) | `4HHB` (High Resolution) | `2HBS` (Sickle Hemoglobin) |
|---|:---:|:---:|:---:|
| Resolution ($\text{\AA}$) | 2.00 $\text{\AA}$ | 1.74 $\text{\AA}$ | 2.05 $\text{\AA}$ |
| $R$-factor ($R_{\text{work}}$) | 0.177 | 0.135 | 0.198 |
| Space Group | $P\,2_1\,2_1\,2$ | $P\,1\,2_1\,1$ | $P\,1\,2_1\,1$ |
| Quaternary State | Deoxy (T-state) | Deoxy (T-state) | Deoxy Polymer (HbS) |
| Chains in Asymmetric Unit | 2 (Chains A, B) | 4 (Chains A, B, C, D) | 8 (Chains A–H) |
| Biological Role / Phenotype | Normal adult oxygen transport | High-precision reference | Pathological sickle polymer |

---

## 7. Interpretation & Discussion Questions

1. **Resolution Numbers vs. Quality:** A novice student claims that a 3.5 $\text{\AA}$ crystal structure is of higher quality than a 1.8 $\text{\AA}$ structure because 3.5 is a larger number. Explain why this claim is fundamentally wrong, and describe what physical detail can be resolved at 1.8 $\text{\AA}$ versus 3.5 $\text{\AA}$.
2. **The R-free Cross-Validation Metric:** Why did structural biologists invent $R_{\text{free}}$ in addition to the traditional $R_{\text{work}}$? How does $R_{\text{free}}$ detect crystallographic "over-fitting" or "over-refinement"?
3. **Asymmetric Unit vs. Biological Unit:** Why does the PDB file for `1A3N` contain atomic coordinates for only two globin chains (Chains A and B) in its `ATOM` records, even though functional adult hemoglobin is universally known to be a four-chain tetramer ($\alpha_2\beta_2$)? How does visualization software reconstruct the full tetramer?
4. **ATOM vs. HETATM Distinction:** What is the fundamental operational difference between an `ATOM` record and a `HETATM` record in a PDB file? Which record type is used for the heme cofactor, and which is used for crystallographic water molecules?
5. **The Temperature Factor ($B$-factor):** In an `ATOM` record, what does the $B$-factor (e.g., $B = 48.72\text{ \AA}^2$) represent physically regarding atomic vibration, thermal mobility, or crystal lattice disorder?

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Use Linux command-line utilities (`grep` and `awk`) on `../../data/structures/1a3n.pdb` to extract the coordinates of the **heme iron atom ($Fe$)** in Chain A and Chain B:
   ```bash
   grep "FE   HEM" ../../data/structures/1a3n.pdb
   ```
2. Locate the **proximal histidine nitrogen atom (NE2 of His-87 in Chain A, or His-92 in Chain B)**.
3. Using the 3D Euclidean distance formula:
   $$d = \sqrt{(X_2 - X_1)^2 + (Y_2 - Y_1)^2 + (Z_2 - Z_1)^2}$$
   calculate the bond distance in Angstroms between the iron atom and the proximal histidine nitrogen. Confirm whether it falls within the expected covalent coordination bond length (~2.0 to 2.2 $\text{\AA}$).
