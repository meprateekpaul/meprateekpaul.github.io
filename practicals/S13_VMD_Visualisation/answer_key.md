# Instructor Answer Key & Evaluation Manual: Practical 13 (VMD Visualisation)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S13 (Syllabus Practical P12)  
**Curriculum Topic:** Visualisation of Protein Structure Using VMD and Mol*  

---

## 1. Expected Outputs & Reference Solutions

### Table 13.1: Structural Geometry and Coordinate Measurements in `1A3N` (Completed)
| Measurement / Structural Feature | Subunit / Chain | Atoms / Residues Involved | Measured Distance ($\text{\AA}$) | Expected Theoretical Range ($\text{\AA}$) |
|---|:---:|:---:|:---:|:---:|
| **Proximal Histidine Coordination** | Chain A ($\alpha$) | Fe (HEM 142) to NE2 (His 87) | **2.10 Å** | 2.05 – 2.15 $\text{\AA}$ (Covalent coordination bond) |
| **Proximal Histidine Coordination** | Chain B ($\beta$) | Fe (HEM 147) to NE2 (His 92) | **2.09 Å** | 2.05 – 2.15 $\text{\AA}$ (Covalent coordination bond) |
| **Distal Histidine Distance** | Chain A ($\alpha$) | Fe (HEM 142) to NE2 (His 58) | **4.12 Å** | 3.8 – 4.2 $\text{\AA}$ (Unbonded, open $O_2$ pocket) |
| **Distal Histidine Distance** | Chain B ($\beta$) | Fe (HEM 147) to NE2 (His 63) | **3.98 Å** | 3.8 – 4.2 $\text{\AA}$ (Unbonded, open $O_2$ pocket) |
| **Sickle Site Residue Identity** | Chain B | Residue 6 in mature sequence | **Glu-6 (E)** | Wild-type: Acidic, charged carboxylate |

### Table 13.2: Molecular Representation and Color Mapping Schemes (Completed)
| Representation Layer | Selection Syntax (VMD atomsel) | Drawing Method | Coloring Method | Biological Information Revealed |
|---|---|---|---|---|
| Whole Protein Backbone | `protein` | NewCartoon | Chain | Heterotetrameric quaternary stoichiometry ($\alpha_1\beta_1$ and $\alpha_2\beta_2$) |
| Secondary Structure Flow | `protein` | NewCartoon | Secondary Structure | Canonical 8-$\alpha$-helical globin fold (purple cylinders) |
| Prosthetic Groups | `resname HEM` | Licorice | Element / CPK | Planar protoporphyrin IX ring coordination geometry |
| Central Metal Ion | `name FE` | VDW (Scale 0.8) | Orange (ColorID) | Ferrous catalytic center displaced out of plane |
| Sickle Mutant Residue | `chain B and resid 6` | VDW Spheres | Red | Hydrophobic Val protrusion driving 14-strand polymer fibers |

---

## 2. Sample Rendered Structural Layout Guide

### View 1: Tetrameric Hemoglobin Cartoon (1A3N)
- **Visual Presentation:** Four intertwining NewCartoon helical chains forming an orthogonal bundle. Chain A (Alpha-1, colored cyan), Chain B (Beta-1, colored yellow), with symmetry mates forming the complete $\alpha_2\beta_2$ tetramer surrounding a central solvent-filled cavity. Four red/orange planar heme disks are embedded symmetrically in hydrophobic crevices.

### View 2: Isolated Heme Oxygen-Binding Pocket
- **Visual Presentation:** A high-magnification close-up centered on the central iron atom (orange sphere).
  - Emerging from underneath: The imidazole ring of **His-F8 (His-92)** forming an axial coordinate bond directly to $Fe$ ($d = 2.09\text{ \AA}$).
  - Situated above the iron: The imidazole ring of **Distal His-E7 (His-63)** positioned ~4.0 $\text{\AA}$ away, leaving a steric pocket for diatomic oxygen.

### View 3: Sickle-Cell Contact in `2HBS`
- **Visual Presentation:** The red van der Waals sphere of **Val-6** on beta-chain 1 nesting snugly into a hydrophobic depression on beta-chain 2 of an adjacent tetramer, framed by the aromatic ring of **Phe-85** and the branched aliphatic side chain of **Leu-88**.

---

## 3. Model Answers to Discussion Questions

### Q1. Proximal vs. Distal Coordination Geometry
- **Model Answer:**
  - The proximal histidine (His-F8) distance of **2.10 $\text{\AA}$** corresponds to a genuine, covalent coordinate dative bond between the lone pair electrons of the imidazole nitrogen (`NE2`) and the empty $d$-orbitals of the ferrous iron atom ($Fe^{2+}$).
  - The distal histidine (His-E7) distance of **~4.0 $\text{\AA}$** is far too long for a covalent bond (covalent bonds require $<2.2\text{ \AA}$). This spatial gap is biologically essential: it leaves an open, sterically protected coordination pocket into which diatomic oxygen ($O_2$) enters and binds to the sixth coordination site of the iron atom. When oxygen binds, the distal histidine forms a stabilizing hydrogen bond with the bound $O_2$ molecule.

### Q2. Out-of-Plane Iron Displacement (The Perutz Mechanism)
- **Model Answer:** In deoxyhemoglobin (the T-state, `1A3N`), the ferrous iron atom is high-spin ($S=2$) with electrons occupying antibonding $d_{x^2-y^2}$ and $d_{z^2}$ orbitals. Its atomic radius is too large to fit into the central hole of the porphyrin ring; consequently, it sits displaced **~0.4 $\text{\AA}$ out of the porphyrin plane** toward the proximal histidine.
  - When oxygen binds, the iron transitions to a low-spin state ($S=0$). Its effective ionic radius shrinks, allowing it to snap into the plane of the porphyrin ring.
  - As the iron moves into the plane, it pulls the covalently attached proximal histidine (His-F8) with it. This movement pulls Helix F, transmitting mechanical strain through the $\alpha_1\beta_2$ dimer interface, rupturing inter-subunit salt bridges, and triggering the cooperative $15^\circ$ quaternary transition from the low-affinity T-state to the high-affinity R-state.

### Q3. The Hydrophobic Val-6 "Sticky Patch"
- **Model Answer:** The sickle mutation replaces charged Glu-6 with hydrophobic Val-6. However, polymer fiber formation occurs **exclusively in deoxygenated erythrocytes**:
  - In the deoxygenated **T-state**, the quaternary arrangement of the beta subunit exposes a hydrophobic receptor pocket composed of **Phenylalanine-85 and Leucine-88**. The mutant Val-6 side chain on an adjacent tetramer fits precisely into this pocket via non-polar van der Waals interactions.
  - When hemoglobin binds oxygen, it allosterically shifts to the **R-state**. In the R-state, Helix F shifts, the C-terminal region relocates, and the Phe-85 / Leu-88 pocket changes conformation, sterically occluding Val-6 binding. Hence, oxygenation instantly dissociates the polymer fibers back into soluble individual tetramers.

### Q4. Comparing Molecular Surfaces vs. Cartoons
- **Model Answer:** A cartoon representation (NewCartoon/Ribbon) displays only an abstract mathematical spline following the $C_\alpha$ backbone. It completely hides:
  1. **Physical Volume and Steric Boundaries:** The true spatial extent occupied by electron clouds (van der Waals radii).
  2. **Topographical Shape:** Deep binding pockets, shallow clefts, and internal solvent cavities.
  3. **Electrostatic Potential Distribution:** Continuous positive (basic/blue) and negative (acidic/red) surface charge fields.
  In drug discovery, a small molecule binds to the solvent-accessible van der Waals surface of the receptor; visualizing surfaces is indispensable for assessing steric complementarity and shape matching.

### Q5. VMD Atom Selection Syntax
- **Model Answer:**
  ```
  (chain A and polar within 4.0 of resname HEM) or (chain A and charged within 4.0 of resname HEM)
  ```
  *(Or more explicitly: `chain A and (resname ARG LYS HIS ASP GLU SER THR ASN GLN TYR) and within 4.0 of resname HEM`)*.

---

## 4. Solution to Extension / Challenge Task

1. **Quaternary Structural Superposition:**
   - Superposing `1A3N` (Deoxy T-state) onto `1HHO` (Oxy R-state) by their $\alpha_1\beta_1$ dimer reveals that the $\alpha_2\beta_2$ dimer rotates by **approximately $15^\circ$** and translates by **$0.8\text{ \AA}$** relative to $\alpha_1\beta_1$.
2. **Central Cavity Narrowing:**
   - In the deoxy T-state, the central water-filled cavity is wide, accommodating the allosteric effector 2,3-bisphosphoglycerate (2,3-BPG) between the two beta chains.
   - Upon oxygenation to the R-state, the beta chains move closer together, narrowing the central cavity by ~6 $\text{\AA}$ and physically expelling the 2,3-BPG molecule.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & VMD/Mol* Navigation** | 2.0 | Deduct 0.5 if student struggles with 3D translation or zooming. |
| **Three Rendered Views (Views 1, 2, 3)** | 4.0 | Award 1.5 marks for View 1, 1.5 for View 2, 1.0 for View 3. Deduct 0.5 per cluttered or mislabeled view. |
| **Observation Tables & Geometry** | 2.0 | Deduct 0.5 for missing iron coordination distances or inaccurate values. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question (must explain the Perutz out-of-plane iron shift). |
| **Total** | **10.0** | |
