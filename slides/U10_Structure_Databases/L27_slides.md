---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 27 Slides: PDB Format and Visualization"
footer: "B.Tech. Bioinformatics (SHUATS-inspired) · Prateek Paul"
style: |
  section {
    font-family: 'Inter', sans-serif;
    font-size: 18px;
    padding: 30px;
    background: #0f172a;
    color: #f8fafc;
  }
  h1, h2, h3 {
    color: #38bdf8;
  }
  pre {
    background: #020617;
    color: #a5f3fc;
    border: 1px solid #1e293b;
    border-radius: 8px;
    padding: 12px;
    font-size: 13px;
  }
  footer, header {
    font-size: 11px;
    color: #64748b;
  }
---

<!-- _class: lead -->
# Lecture 27 — PDB Format and Visualization
### Concepts of Bioinformatics (CBBI-501)
**Unit 10:** Structure Databases  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Coordinates of Macromolecular Life

```text
Topic: Capturing 3D Geometry in Plain Text

[Visual: A 3D render of human deoxyhemoglobin (PDB 1A3N: alpha_2 beta_2 tetramer)
         side by side with the raw 80-column text of a PDB file:
  ATOM      1  N   VAL A   1       8.520  34.210  12.150  1.00 24.12           N]
```

**Speaker Talking Points:**  
* At its core, a macromolecular 3D structure is a list of atoms, their chemical identities,
  and their orthogonal Cartesian (x, y, z) coordinates in space.
* Designed in the era of 80-column Hollerith punched cards (1971), the **PDB format**
  remains the most widely recognized coordinate format in computational biophysics.

---

## Slide 2: Anatomy of the Legacy PDB Format: Columnar Grammar

```text
Topic: Strict Fixed-Width 80-Column Layout

  ATOM     32  CA  HIS B   2      12.450  24.120  -5.320  1.00 18.50           C
  \____/ \___/ \_/ \_/ | \_/      \____/  \____/  \____/  \__/ \___/           |
   1-6    7-11 13- 18- 22 23-     31-38   39-46   47-54   55-  61-66          77-78
   Type   Atom 16  20  Ch 26        X       Y       Z     60   Temp            Elem
          Num  Name Res ID SeqNum  (Angstroms float 8.3)  Occ  (B-factor)
```

**Speaker Talking Points:**  
* Columns 1-6: Record Name (`ATOM  ` or `HETATM`).
* Columns 31-54: (x, y, z) Cartesian coordinates in Ångströms with 3 decimal places.
* PDB parsers read by columnar slices (`line[30:38]`), NOT by whitespace splitting!

---

## Slide 3: The Crucial Distinction: ATOM vs HETATM

```text
Topic: Standard Polymers vs Heterogeneous Ligands

1. ATOM Records:
   * Standard polymeric building blocks: the 20 standard L-amino acids and
     4 standard RNA/DNA nucleotides.
   * Linked by standard covalent peptide or phosphodiester backbones.

2. HETATM (Hetero-Atom) Records:
   * Non-standard chemical entities:
     - Bound prosthetic groups (e.g. `HEM` - Protoporphyrin IX with Fe in hemoglobin).
     - Bound metal ions: `FE`, `ZN`, `MG`, `CA`.
     - Ordered solvent water molecules: `HOH`.
     - Synthetic pharmaceutical drug ligands and crystallization buffer salts.
```

**Speaker Talking Points:**  
* Never mistake a prosthetic group or solvent water for an amino acid!

---

## Slide 4: SEQRES vs ATOM Records: The Disordered Loop Problem

```text
Topic: Why the Chemical Sequence Does Not Match the Coordinates

  In PDB 1A3N (Beta Chain):
    SEQRES lists 146 amino acids (1 to 146).
    ATOM records list residues 1 to 146... BUT what if a loop is flexible?
```

**Speaker Talking Points:**  
* `SEQRES` lists the complete, authentic chemical sequence of the construct placed
  in the crystallization drop.
* `ATOM` records exist ONLY for atoms that scatter X-rays into discernible electron density.
* If a 10-residue surface loop flutters dynamically in the crystal, its electron density
  is smeared into oblivion; those 10 residues are omitted from the ATOM coordinate list!

---

## Slide 5: Temperature Factor (B-Factor) & Occupancy

```text
Topic: Quantifying Atomic Mobility in Space

1. Temperature Factor (B-Factor):
   B = 8 * pi^2 * <u^2>    (where <u^2> is mean-square thermal displacement)
   * High B-factor (>50 A^2): Flexible, fluctuating loops or disordered surface residues.
   * Low B-factor (<15 A^2): Rigid, tightly packed hydrophobic core or active-site catalytic triad.

2. Occupancy Factor:
   * The fraction of unit cells in the crystal that harbor that atom in that position.
   * Typically 1.00; splits into 0.50 if an amino acid adopts two alternative rotamer poses!
```

**Speaker Talking Points:**  
* Color by B-factor: Blue (rigid) to Red (dynamic).

---

## Slide 6: The Column Overflow Crisis: Transition to mmCIF

```text
Topic: Why the Legacy PDB Format Reached Its Expiration Date

  The Limits of Fixed-Width 80 Columns:
  * Atom serial number: 5 digits max -> Overflow at 99,999 atoms!
  * Chain ID: 1 character (A-Z)     -> Overflow at 62 chains!

  The Modern Solution: mmCIF (PDBx/mmCIF):
  * Macromolecular Crystallographic Information Framework.
  * In 2014, wwPDB made mmCIF the master archive format.
  * Capable of handling massive megadalton complexes (e.g. 70S ribosome with >250,000 atoms).
```

**Speaker Talking Points:**  
* Learn PDB for quick inspection; use mmCIF for modern high-performance pipelines.

---

## Slide 7: Molecular Visualization: Rendering Styles

```text
Topic: Seeing the Invisible

+--------------------+-------------------------+------------------------------+
| Visual Style       | Physical Feature Shown  | Best Biological Use Case     |
+--------------------+-------------------------+------------------------------+
| **Wireframe/Line** | Chemical bonds only     | Rapid inspection of backbone |
| **Stick**          | Covalent cylinders      | Active sites, ligand binding |
| **CPK / Sphere**   | Van der Waals radii     | Steric clashes, cavity volume|
| **Cartoon/Ribbon** | Helices, sheets, loops  | Overall 3D fold & topology   |
| **Surface (SASA)** | Solvent-accessible envelope| Epitopes, hydrophobic clefts|
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* A cartoon representation clarifies quaternary folding; stick displays show the haem pocket.

---

## Slide 8: Summary & Molecular Viewers

```text
Topic: Software for 3D Exploration

* **VMD (Visual Molecular Dynamics):** The syllabus standard. High-performance
  molecular dynamics trajectory viewer.
* **PyMOL:** Industry standard for publication-quality ray-traced figures.
* **ChimeraX:** Superb Cryo-EM map visualization and density docking.
* **Mol* (Mol-Star):** Ultra-fast WebGL in-browser 3D viewer at RCSB PDB.
* Next Lecture: Structure Comparison (RMSD, Kabsch algorithm) and Advanced Modeling
  (Homology modeling & AlphaFold).
```

