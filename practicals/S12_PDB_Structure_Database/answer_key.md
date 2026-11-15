# Instructor Answer Key & Evaluation Manual: Practical 12 (PDB Structure Database)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S12 (Syllabus Practical P11)  
**Curriculum Topic:** Introduction to the Structure Database PDB and Macromolecular Records  

---

## 1. Expected Outputs & Reference Solutions

### Table 12.1: RCSB PDB Structure Profile for Human Deoxyhemoglobin (`1A3N`) (Completed)
| Structural Metadata Field | Extracted Record Value | Significance / Explanation |
|---|---|---|
| PDB ID Code | `1A3N` | 4-character primary accession code |
| Structure Title | *Crystal structure of human adult deoxyhemoglobin at 2.0 angstroms resolution* | Primary experimental investigation (Tame & Vallone, 2000) |
| Experimental Method | `X-RAY DIFFRACTION` | Single-crystal X-ray diffraction |
| Crystallographic Resolution ($\text{\AA}$) | `2.00 Å` | Minimum Bragg plane inter-planar spacing resolved |
| $R_{\text{work}}$ / $R_{\text{free}}$ | $R_{\text{work}} = 0.177$ (17.7%) / $R_{\text{free}} = 0.231$ (23.1%) | Low values (<0.20) indicate high model accuracy; $\Delta R \approx 5.4\%$ confirms no over-fitting |
| Space Group Symmetry | $P\,2_1\,2_1\,2$ | Primitive orthorhombic with three perpendicular screw axes |
| Number of Chains in Asymmetric Unit | 2 chains | Only the $\alpha\beta$ heterodimer is present in the asymmetric unit |
| Identity of Chains in Asymmetric Unit | Chain A (Alpha globin, 141 aa), Chain B (Beta globin, 146 aa) | Mature processed chains (lacking initiator Met) |
| Stoichiometry of Biological Assembly | Heterotetramer ($\alpha_2\beta_2$, Chains A, B, C, D) | Reconstructed by applying 2-fold crystallographic rotation |
| Bound Ligands / Cofactors (`HETATM`) | `HEM` (Protoporphyrin IX with $Fe$), `PO4` (Phosphate ion), `HOH` (Water) | 2 hemes per asymmetric unit (4 hemes per biological tetramer) |
| Total Atom Count in File | 4,771 lines / ~2,300 non-hydrogen atoms per dimer | Total records in flat file |

### Table 12.2: Cross-Structure Comparative Quality Metrics (Completed)
| Metric | `1A3N` (Standard Deoxy) | `4HHB` (High Resolution) | `2HBS` (Sickle Hemoglobin) |
|---|:---:|:---:|:---:|
| Resolution ($\text{\AA}$) | 2.00 $\text{\AA}$ | **1.74 $\text{\AA}$** | 2.05 $\text{\AA}$ |
| $R$-factor ($R_{\text{work}}$) | 0.177 | **0.135** | 0.198 |
| Space Group | $P\,2_1\,2_1\,2$ | $P\,1\,2_1\,1$ (Monoclinic) | $P\,1\,2_1\,1$ (Monoclinic) |
| Quaternary State | Deoxy (T-state) | Deoxy (T-state) | Deoxy HbS Polymer |
| Chains in Asymmetric Unit | 2 (Chains A, B) | 4 (Chains A, B, C, D) | 8 (Chains A–H, 2 tetramers) |
| Biological Role / Phenotype | Standard adult reference | Benchmark atomic coordinates | Pathological sickle fiber polymer |

---

## 2. Sample PDB Flat File Wireframe (`1A3N.pdb`)

```
HEADER    OXYGEN TRANSPORT                        22-JAN-98   1A3N
TITLE     CRYSTAL STRUCTURE OF HUMAN ADULT DEOXYHEMOGLOBIN AT 2.0
TITLE    2 ANGSTROMS RESOLUTION
COMPND    MOL_ID: 1;
COMPND   2 MOLECULE: HEMOGLOBIN (DEOXY) (ALPHA CHAIN);
COMPND   3 CHAIN: A;
COMPND   4 MOL_ID: 2;
COMPND   5 MOLECULE: HEMOGLOBIN (DEOXY) (BETA CHAIN);
COMPND   6 CHAIN: B;
SOURCE    MOL_ID: 1;
SOURCE   2 ORGANISM_SCIENTIFIC: HOMO SAPIENS;
SOURCE   3 EXPRESSION_SYSTEM: ESCHERICHIA COLI;
REMARK   2
REMARK   2 RESOLUTION.    2.00 ANGSTROMS.
REMARK   3   R VALUE            (WORKING SET) : 0.177
REMARK   3   FREE R VALUE                     : 0.231
SEQRES   1 A  141  VAL LEU SER PRO ALA ASP LYS THR ASN VAL LYS ALA ALA TRP
...
ATOM      1  N   VAL A   1       6.261  16.744   4.902  1.00 48.72           N
ATOM      2  CA  VAL A   1       5.234  16.309   3.931  1.00 43.16           C
ATOM      3  C   VAL A   1       3.921  15.932   4.620  1.00 37.89           C
ATOM      4  O   VAL A   1       3.805  16.035   5.845  1.00 40.89           O
...
HETATM 2262 FE   HEM A 142       3.927  -1.341  -4.789  1.00 13.92          FE
...
CONECT 2262 2263 2264 2265 2266
END
```

---

## 3. Model Answers to Discussion Questions

### Q1. Resolution Numbers vs. Quality
- **Model Answer:** In X-ray crystallography and Cryo-EM, resolution is defined by **limiting inter-planar Bragg spacing ($d_{\text{min}}$)**, representing the minimum spatial distance between two electron density features that can be distinguished as separate entities. Therefore, **a smaller numerical value indicates higher resolution and superior detail**:
  - At **1.8 $\text{\AA}$**, individual atomic positions along the polypeptide backbone and side chains are clearly separated, water molecules are individually resolved, and planar rings (phenylalanine, heme) display distinct central electron density holes.
  - At **3.5 $\text{\AA}$**, individual atoms cannot be resolved; only the general outline of the protein backbone and cylindrical densities corresponding to $\alpha$-helices are visible. Side-chain orientations are largely ambiguous and must be computationally modeled.

### Q2. The R-free Cross-Validation Metric
- **Model Answer:** During crystallographic refinement, atomic coordinates are iteratively adjusted against experimental diffraction intensities. Because an atomic model contains thousands of free parameters ($X, Y, Z, B$ per atom), it is mathematically prone to **over-fitting** (modeling random experimental noise or false density artifacts to artificially lower the conventional $R_{\text{work}}$).
  - To prevent this, Axel Brünger introduced **$R_{\text{free}}$**. Before refinement begins, a random 5% to 10% subset of experimental diffraction reflections is set aside as an independent test set and completely excluded from refinement.
  - $R_{\text{free}}$ is calculated exclusively against this withheld test set. If an investigator over-refines or introduces unphysical coordinates, $R_{\text{work}}$ will decrease while $R_{\text{free}}$ will diverge or increase, exposing model over-fitting.

### Q3. Asymmetric Unit vs. Biological Unit
- **Model Answer:** In X-ray crystallography, the PDB file reports the atomic coordinates of the **asymmetric unit (ASU)**—the smallest unique structural unit from which the entire crystal lattice can be generated by applying the crystallographic space group symmetry operations.
  - In `1A3N` (Space group $P\,2_1\,2_1\,2$), the asymmetric unit consists of one $\alpha\beta$ heterodimer (Chains A and B).
  - The functional adult hemoglobin in human blood is an **$\alpha_2\beta_2$ heterotetramer**.
  - Because the crystal possesses a crystallographic two-fold rotational symmetry axis that runs directly through the center of the hemoglobin tetramer, the other two chains (Chains C and D, forming the second $\alpha\beta$ dimer) are mathematically identical symmetry mates. Molecular viewers reconstruct the biological tetramer by reading the `REMARK 350` rotation/translation matrices and duplicating Chains A and B across the symmetry axis.

### Q4. ATOM vs. HETATM Distinction
- **Model Answer:**
  - **`ATOM` Records:** Strictly reserved for standard polymer building blocks (the 20 canonical amino acids in proteins and standard ribonucleotides/deoxyribonucleotides in RNA/DNA). These records define the continuous covalent polypeptide or polynucleotide backbone.
  - **`HETATM` Records:** "Hetero-atoms" reserved for non-standard chemical moieties, prosthetic groups, cofactors, metal ions, enzyme substrates, small-molecule drug inhibitors, and crystallographic solvent molecules.
  - In `1A3N`, the heme porphyrin and central iron are designated as **`HETATM`** with residue name `HEM`. Crystallographic water molecules are designated as **`HETATM`** with residue name `HOH`.

### Q5. The Temperature Factor ($B$-factor)
- **Model Answer:** The $B$-factor (Debye-Waller temperature factor), measured in $\text{\AA}^2$, quantifies the degree of thermal vibration and static positional disorder of each individual atom around its mean equilibrium position:
  $$B = 8\pi^2 \langle u^2 \rangle$$
  where $\langle u^2 \rangle$ is the mean-square displacement of the atom.
  - Low $B$-factors ($<20\text{ \AA}^2$, as observed in the buried heme iron and hydrophobic core) indicate rigid, well-ordered, immotile regions with sharp, high-confidence electron density.
  - High $B$-factors ($>50\text{ \AA}^2$, as seen at flexible N- or C-termini and solvent-exposed surface loops) indicate dynamic conformational mobility, flexible flapping, or static disorder within the crystal lattice.

---

## 4. Solution to Extension / Challenge Task

### Step 1: Extract Coordinates from `1A3N.pdb`
```bash
grep "FE   HEM A 142" ../../data/structures/1a3n.pdb
grep "NE2 HIS A  87" ../../data/structures/1a3n.pdb
```

- **Heme Fe Atom (Chain A):**
  $X_1 = 3.927$, $Y_1 = -1.341$, $Z_1 = -4.789$
- **Proximal His-87 NE2 Nitrogen (Chain A):**
  $X_2 = 3.518$, $Y_2 = -0.582$, $Z_2 = -2.871$

### Step 2: Calculate Euclidean Distance ($d$)
$$\Delta X = 3.518 - 3.927 = -0.409$$
$$\Delta Y = -0.582 - (-1.341) = +0.759$$
$$\Delta Z = -2.871 - (-4.789) = +1.918$$

$$d = \sqrt{(-0.409)^2 + (0.759)^2 + (1.918)^2} = \sqrt{0.1673 + 0.5761 + 3.6787} = \sqrt{4.4221} \approx \mathbf{2.10\text{ \AA}}$$

**Biological Validation:** A distance of $2.10\text{ \AA}$ falls perfectly within the known physical coordination bond length range ($2.05 - 2.15\text{ \AA}$) between the imidazole nitrogen of the proximal histidine and the ferrous iron atom of the heme porphyrin ring.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & Entry Report** | 2.0 | Deduct 0.5 if student misidentifies determination method or resolution. |
| **Observation Tables (Table 12.1 & 12.2)** | 4.0 | Deduct 0.5 per missing or erroneous metric (R-factors, space group). |
| **PDB Record Dissection** | 2.0 | Deduct 0.5 if ATOM vs HETATM or ASU vs Biological unit is confused. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question for rigorous explanations (resolution math, B-factor). |
| **Total** | **10.0** | |
