# Practical Worksheet 13: Macromolecular Structure Visualization with VMD and Mol*

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Session:** S13 (Syllabus Practical P12)  
**Semester:** B.Tech. Bioinformatics, Semester II  

---

### Student Identification Details
- **Student Name:** __________________________________________________
- **Roll Number:** ____________________________________________________
- **Lab Station / PC No.:** ___________________________________________
- **Date of Practical Performance:** __________________________________
- **Date of Report Submission:** ______________________________________

---

### 1. Pre-Lab Checklist & Learning Objectives Tracker
- [ ] Successfully loaded `1A3N.pdb` into VMD / Mol*.
- [ ] Navigated 3D space (rotations, translations, zoom, clipping).
- [ ] Built multi-layer representations: NewCartoon, Licorice, VDW, and Surface.
- [ ] Isolated and measured the oxygen-binding heme pocket ($Fe$-His coordination).
- [ ] Loaded `2HBS.pdb` and mapped the sickle-cell Glu6Val mutation site.
- [ ] Visualized the intermolecular hydrophobic contact between Val-6 and Phe-85/Leu-88.

---

### 2. Visualization Log & Software Environment

Record your software details:
- **Primary Viewer Used (VMD or Mol\*):** `[                                                    ]`
- **VMD / Mol\* Version:** `[                                                                  ]`
- **Local PDB Files Loaded:** `[                                                               ]`

---

### 3. Structured Observation Tables

#### Table 13.1: Structural Geometry and Coordinate Measurements in `1A3N`
| Measurement / Structural Feature | Subunit / Chain | Atoms / Residues Involved | Measured Distance ($\text{\AA}$) | Expected Theoretical Range ($\text{\AA}$) |
|---|:---:|:---:|:---:|:---:|
| **Proximal Histidine Coordination** | Chain A ($\alpha$) | Fe (HEM 142) to NE2 (His 87) | `[__________] Å` | 2.05 – 2.15 $\text{\AA}$ |
| **Proximal Histidine Coordination** | Chain B ($\beta$) | Fe (HEM 147) to NE2 (His 92) | `[__________] Å` | 2.05 – 2.15 $\text{\AA}$ |
| **Distal Histidine Distance** | Chain A ($\alpha$) | Fe (HEM 142) to NE2 (His 58) | `[__________] Å` | 3.8 – 4.2 $\text{\AA}$ (Unbonded) |
| **Distal Histidine Distance** | Chain B ($\beta$) | Fe (HEM 147) to NE2 (His 63) | `[__________] Å` | 3.8 – 4.2 $\text{\AA}$ (Unbonded) |
| **Sickle Site Residue Identity** | Chain B | Residue 6 in mature sequence | `[__________]` | Wild-type: Glu (Acidic) |

#### Table 13.2: Molecular Representation and Color Mapping Schemes
| Representation Layer | Selection Syntax (VMD atomsel) | Drawing Method | Coloring Method | Biological Information Revealed |
|---|---|---|---|---|
| Whole Protein Backbone | `protein` | NewCartoon | Chain | Overall quaternary stoichiometry |
| Secondary Structure Flow | `protein` | NewCartoon | Secondary Structure | $\alpha$-helices (purple) vs loops (white) |
| Prosthetic Groups | `resname HEM` | Licorice | Element / CPK | Porphyrin ring planarity & orientation |
| Central Metal Ion | `name FE` | VDW (Scale 0.8) | Orange (ColorID) | Active catalytic metal center |
| Sickle Mutant Residue | `chain B and resid 6` | VDW Spheres | Red | Bulky hydrophobic patch on outer surface |

---

### 4. Rendered Figure Submission Boxes

#### View 1: Whole Tetramer Cartoon by Chain (1A3N)
```
+-----------------------------------------------------------------------------------------+
|                         VIEW 1: HEMOGLOBIN TETRAMER CARTOON                             |
+-----------------------------------------------------------------------------------------+
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
+-----------------------------------------------------------------------------------------+
```

#### View 2: Isolated Heme Pocket (Iron, Proximal His, Distal His)
```
+-----------------------------------------------------------------------------------------+
|                             VIEW 2: OXYGEN BINDING POCKET                               |
+-----------------------------------------------------------------------------------------+
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
+-----------------------------------------------------------------------------------------+
```

#### View 3: Sickle-Cell HbS Mutation Site & Polymer Contact (2HBS)
```
+-----------------------------------------------------------------------------------------+
|                             VIEW 3: SICKLE CELL CONTACT (2HBS)                          |
+-----------------------------------------------------------------------------------------+
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
|                                                                                         |
+-----------------------------------------------------------------------------------------+
```

---

### 5. Interpretation & Discussion Questions

**Q1. Proximal vs. Distal Coordination Geometry:** Explain why the distance between iron and proximal histidine is ~2.1 $\text{\AA}$, whereas the distance to distal histidine is ~4.0 $\text{\AA}$. What binds in the intervening space?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q2. Out-of-Plane Iron Displacement (The Perutz Mechanism):** In deoxyhemoglobin (T-state, `1A3N`), the iron atom is displaced by ~0.4 $\text{\AA}$ out of the porphyrin plane toward proximal His. What happens to the iron atom and F-helix upon $O_2$ binding?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q3. The Hydrophobic Val-6 "Sticky Patch":** In `2HBS`, why does the hydrophobic contact between Val-6 and Phe-85/Leu-88 occur *only* in the deoxy (T) state, and why does oxygenation (R-state) dissolve the sickle fiber?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q4. Comparing Molecular Surfaces vs. Cartoons:** Why is a molecular surface representation superior to a cartoon when evaluating drug binding pockets? What physical attribute does a cartoon omit?  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  
`[                                                                                             ]`  

**Q5. VMD Atom Selection Syntax:** Write the exact VMD atom selection string required to select all polar and charged amino acids located within 4.0 Angstroms of the heme group in Chain A.  
**Student Answer:**  
`[                                                                                             ]`  
`[                                                                                             ]`  

---

### 6. Extension / Challenge Task Output
*Record your quaternary structural comparison (T-state vs R-state):*
- **Rigid-body Rotation Observed:** `[__________] degrees`
- **Change in Central Cavity Dimension:** `[                                                    ]`

---

### 7. Evaluation & Marking Scheme (Instructor / TA Use Only)

| Evaluation Component | Maximum Marks | Marks Awarded | Comments / Remarks |
|---|:---:|:---:|---|
| **Pre-Lab Knowledge & Navigation** | 2 | | Fluent 3D navigation and selection syntax in VMD/Mol* |
| **Rendered Figures (Views 1, 2, 3)** | 4 | | Three clean, correctly colored, properly zoomed views |
| **Observation Tables & Distances** | 2 | | Accurate distance measurements (Fe-His proximal and distal) |
| **Discussion Questions & Critical Viva** | 2 | | Sound scientific reasoning regarding Perutz mechanism and HbS |
| **Total Marks** | **10** | | |

**Instructor / TA Signature:** _______________________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Date:** _______________
