# Lecture 27 — PDB Format and Visualization

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 10:** Structure Databases  
**Syllabus Topic:** Structure file format, visualizing structure information, Structure viewers  
**Primary Learning Outcome:** LO7 — Read a PDB entry, parse structure file records (ATOM, HETATM, SEQRES), and render 3D macromolecular visual representations in VMD and Mol*.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Coordinates of Macromolecular Life
================================================================================
Topic: Capturing 3D Geometry in Plain Text

[Visual: A 3D render of human deoxyhemoglobin (PDB 1A3N: alpha_2 beta_2 tetramer)
         side by side with the raw 80-column text of a PDB file:
  ATOM      1  N   VAL A   1       8.520  34.210  12.150  1.00 24.12           N]

Speaker Bullets:
* At its core, a macromolecular 3D structure is a list of atoms, their chemical identities,
  and their orthogonal Cartesian (x, y, z) coordinates in space.
* Designed in the era of 80-column Hollerith punched cards (1971), the **PDB format**
  remains the most widely recognized coordinate format in computational biophysics.
```

```
================================================================================
SLIDE 2: Anatomy of the Legacy PDB Format: Columnar Grammar
================================================================================
Topic: Strict Fixed-Width 80-Column Layout

  ATOM     32  CA  HIS B   2      12.450  24.120  -5.320  1.00 18.50           C
  \____/ \___/ \_/ \_/ | \_/      \____/  \____/  \____/  \__/ \___/           |
   1-6    7-11 13- 18- 22 23-     31-38   39-46   47-54   55-  61-66          77-78
   Type   Atom 16  20  Ch 26        X       Y       Z     60   Temp            Elem
          Num  Name Res ID SeqNum  (Angstroms float 8.3)  Occ  (B-factor)

Speaker Bullets:
* Columns 1-6: Record Name (`ATOM  ` or `HETATM`).
* Columns 31-54: (x, y, z) Cartesian coordinates in Ångströms with 3 decimal places.
* PDB parsers read by columnar slices (`line[30:38]`), NOT by whitespace splitting!
```

```
================================================================================
SLIDE 3: The Crucial Distinction: ATOM vs HETATM
================================================================================
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

Speaker Bullets:
* Never mistake a prosthetic group or solvent water for an amino acid!
```

```
================================================================================
SLIDE 4: SEQRES vs ATOM Records: The Disordered Loop Problem
================================================================================
Topic: Why the Chemical Sequence Does Not Match the Coordinates

  In PDB 1A3N (Beta Chain):
    SEQRES lists 146 amino acids (1 to 146).
    ATOM records list residues 1 to 146... BUT what if a loop is flexible?

Speaker Bullets:
* `SEQRES` lists the complete, authentic chemical sequence of the construct placed
  in the crystallization drop.
* `ATOM` records exist ONLY for atoms that scatter X-rays into discernible electron density.
* If a 10-residue surface loop flutters dynamically in the crystal, its electron density
  is smeared into oblivion; those 10 residues are omitted from the ATOM coordinate list!
```

```
================================================================================
SLIDE 5: Temperature Factor (B-Factor) & Occupancy
================================================================================
Topic: Quantifying Atomic Mobility in Space

1. Temperature Factor (B-Factor):
   B = 8 * pi^2 * <u^2>    (where <u^2> is mean-square thermal displacement)
   * High B-factor (>50 A^2): Flexible, fluctuating loops or disordered surface residues.
   * Low B-factor (<15 A^2): Rigid, tightly packed hydrophobic core or active-site catalytic triad.

2. Occupancy Factor:
   * The fraction of unit cells in the crystal that harbor that atom in that position.
   * Typically 1.00; splits into 0.50 if an amino acid adopts two alternative rotamer poses!

Speaker Bullets:
* Color by B-factor: Blue (rigid) to Red (dynamic).
```

```
================================================================================
SLIDE 6: The Column Overflow Crisis: Transition to mmCIF
================================================================================
Topic: Why the Legacy PDB Format Reached Its Expiration Date

  The Limits of Fixed-Width 80 Columns:
  * Atom serial number: 5 digits max -> Overflow at 99,999 atoms!
  * Chain ID: 1 character (A-Z)     -> Overflow at 62 chains!

  The Modern Solution: mmCIF (PDBx/mmCIF):
  * Macromolecular Crystallographic Information Framework.
  * In 2014, wwPDB made mmCIF the master archive format.
  * Capable of handling massive megadalton complexes (e.g. 70S ribosome with >250,000 atoms).

Speaker Bullets:
* Learn PDB for quick inspection; use mmCIF for modern high-performance pipelines.
```

```
================================================================================
SLIDE 7: Molecular Visualization: Rendering Styles
================================================================================
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

Speaker Bullets:
* A cartoon representation clarifies quaternary folding; stick displays show the haem pocket.
```

```
================================================================================
SLIDE 8: Summary & Molecular Viewers
================================================================================
Topic: Software for 3D Exploration

* **VMD (Visual Molecular Dynamics):** The syllabus standard. High-performance
  molecular dynamics trajectory viewer.
* **PyMOL:** Industry standard for publication-quality ray-traced figures.
* **ChimeraX:** Superb Cryo-EM map visualization and density docking.
* **Mol* (Mol-Star):** Ultra-fast WebGL in-browser 3D viewer at RCSB PDB.
* Next Lecture: Structure Comparison (RMSD, Kabsch algorithm) and Advanced Modeling
  (Homology modeling & AlphaFold).
```

---

## Detailed Comprehensive Technical Notes

### 1. The Historical Legacy of the PDB Column Format

The Protein Data Bank was established in 1971 by Walter Hamilton at Brookhaven National Laboratory. At the time, data was encoded on standard 80-column IBM punched cards. To ensure uniformity, every structural property was assigned a strict, non-negotiable horizontal column range.

A standard PDB record line is an 80-byte ASCII string terminated by a newline.

#### Complete Column Specification for Coordinate Records (`ATOM` and `HETATM`):

```
  Columns   Field Name        Data Type      Example        Description
  -------------------------------------------------------------------------------------------------
  1 - 6     Record Name       String (6)     `ATOM  `       Record type: ATOM or HETATM
  7 - 11    Atom Serial No    Integer (5)    `   32`        Unique sequential atom index (1 to 99,999)
  13 - 16   Atom Name         String (4)     ` CA `         Atom name (left-justified: elements < 2 chars
                                                            begin at col 14, e.g. " CA ", " N  ", " O  ")
  17        AltLoc            Character (1)  ` `            Alternate location indicator ('A', 'B')
  18 - 20   Residue Name      String (3)     `HIS`          Three-letter amino acid or ligand code
  22        Chain Identifier  Character (1)  `B`            Polypeptide chain label (A, B, C, etc.)
  23 - 26   Residue Seq No    Integer (4)    `   2`         Residue sequence number in primary chain
  27        Insertion Code    Character (1)  ` `            Code for insertions (e.g. 'A' in 100A)
  31 - 38   X Coordinate      Float (8.3)    `  12.450`     Orthogonal X coordinate in Angstroms
  39 - 46   Y Coordinate      Float (8.3)    `  24.120`     Orthogonal Y coordinate in Angstroms
  47 - 54   Z Coordinate      Float (8.3)    `  -5.320`     Orthogonal Z coordinate in Angstroms
  55 - 60   Occupancy         Float (6.2)    `  1.00`       Crystallographic occupancy fraction
  61 - 66   Temperature FactorFloat (6.2)    ` 18.50`       Isotropic displacement B-factor in A^2
  77 - 78   Element Symbol    String (2)     ` C`           Chemical element symbol, right-justified
  79 - 80   Formal Charge     String (2)     `  `           Charge on atom (e.g. "2+", "1-")
```

---

### 2. Deep Dive: `ATOM` vs `HETATM`

In structural bioinformatics, confusing `ATOM` and `HETATM` records is a frequent source of programming errors.

```
  Record Tag     Biological Scope                             Examples
  -------------------------------------------------------------------------------------------------
  ATOM           Standard polymeric macromolecules            The 20 canonical L-amino acids (ALA to TYR),
                 connected by continuous backbones            the 4 standard RNA ribonucleotides (A, C, G, U),
                                                              the 4 standard DNA deoxyribonucleotides.
  HETATM         Heterogeneous, non-polymeric chemical        Prosthetic groups (`HEM` in hemoglobin),
                 species, solvent, or non-standard residues   metal co-factors (`FE`, `MG`, `ZN`), solvent
                                                              water molecules (`HOH`), crystallizing buffer
                                                              salts (`SO4`, `PO4`), synthetic drug ligands.
```

#### The Special Case of Water (`HOH`):
In an X-ray crystal structure, individual water molecules that form stable, immobilized hydrogen bonds with the protein surface scatter X-rays and appear in electron density maps. They are recorded as `HETATM` records with residue name `HOH` or `WAT`, containing only an oxygen atom (`O`). In high-resolution hemoglobin structures (e.g. PDB `1A3N`), there are hundreds of discrete `HOH` records.

#### Covalent Connectivity: The `CONECT` Record
Because standard peptide and phosphodiester bonds have predictable stereochemical geometry, PDB files do not list bonds between `ATOM` records. However, for `HETATM` ligands and prosthetic groups, covalent bonds and coordination bonds must be explicitly recorded using **`CONECT` records**:

```
CONECT 2145 2146 2147 2148 1042
```
This specifies that the iron atom (atom 2145) in the haem group forms coordination bonds with the four pyrrole nitrogens of protoporphyrin IX (atoms 2146, 2147, 2148) and the imidazole nitrogen $N_\epsilon$ of the proximal Histidine residue (atom 1042).

---

### 3. Temperature Factors (B-Factors) and Structural Mobility

The **B-factor** (also known as the Debye-Waller factor or isotropic temperature factor) models the thermal vibration and static disorder of an atom about its mean equilibrium position:

$$B = 8 \pi^2 \langle u^2 \rangle$$

where $\langle u^2 \rangle$ is the mean-square atomic displacement in $\text{\AA}^2$.

```
  B-Factor Value Range       Structural Reality & Interpretation
  -------------------------------------------------------------------------------------------------
  B < 15 Angstroms^2         Extremely rigid atom; deeply buried in hydrophobic core; highly ordered.
  15 <= B <= 35 Angstroms^2  Typical average value for well-ordered globular proteins.
  B > 50 Angstroms^2         Highly mobile, flexible surface loop, dynamic terminal residue,
                             or partially disordered crystallization solvent region.
```

Bioinformaticians routinely color protein structures in visualization programs by **B-factor** using a cool-to-warm gradient:
- **Blue / Violet:** Rigid structural core (low B-factor).
- **Orange / Red:** Thermally mobile, flexible surface loops (high B-factor).

---

### 4. The mmCIF / PDBx Revolution

By the early 2010s, the legacy PDB format faced an existential computational crisis caused by its rigid 80-column fixed-width specification:
1. **The 99,999 Atom Overflow:** Columns 7–11 allow only 5 digits for the atom serial number. When crystallographers and cryo-EM microscopists solved massive macromolecular machines (such as the intact 70S ribosome, containing over 250,000 atoms), the atom numbering wrapped around to `00000` or crashed standard parsers.
2. **The 62 Chain Identifier Limit:** Column 22 allows only a single character for the chain ID (`A-Z`, `a-z`, `0-9` = 62 unique chains). Large viral capsids containing hundreds of protein subunits ran out of chain letters.

In 2014, the Worldwide Protein Data Bank consortium (wwPDB) made **mmCIF (macromolecular Crystallographic Information File)** the master standard format:
- Free-format, tag-value syntax independent of column boundaries.
- Uses explicit category tokens (e.g., `_atom_site.id`, `_atom_site.Cartn_x`).
- Handles unlimited numbers of atoms, unlimited chain identifiers (e.g. `chain "AAA"`), and rich experimental metadata dictionaries.

---

### 5. Molecular Visualization: Styles and Software

#### Visual Representations:
1. **Wireframe / Lines:** Draws single lines connecting covalent bonds. Minimal GPU load; useful for rapid inspection of full complexes.
2. **Stick Representation:** Displays bonds as solid cylinders. Essential for inspecting catalytic triads, active-site stereochemistry, hydrogen-bonding networks, and small-molecule drug coordination.
3. **CPK (Corey-Pauling-Koltun) / Space-Filling Spheres:** Renders each atom as a full sphere scaled to its empirical **Van der Waals radius** ($C = 1.7\text{ \AA}, N = 1.55\text{ \AA}, O = 1.52\text{ \AA}$). Critical for evaluating steric clashes, packing density, and ligand-binding cavity fit.
4. **Cartoon / Ribbon (Richardson Style):** Represents the polypeptide backbone as smooth ribbons: coiled spirals for $\alpha$-helices, flat arrows pointing $N \to C$ for $\beta$-strands, and thin tubes for coils. Unbeatable for understanding overall 3D folding topology.
5. **Molecular Surface (SASA / Connolly Surface):** Renders the solvent-accessible envelope calculated by rolling a spherical probe representing a water molecule ($r = 1.4\text{ \AA}$) over the Van der Waals surface. Essential for mapping surface electrostatic potential and identifying drug-binding pockets.

#### Software Tools:
- **VMD (Visual Molecular Dynamics - Univ. of Illinois):** Specified in the university practical syllabus. Optimized for massive systems, molecular dynamics trajectories, and secondary structure coloring.
- **PyMOL (Schrödinger):** Industry standard for creating publication-quality ray-traced images.
- **UCSF ChimeraX:** Modern GPU-accelerated engine specialized for Cryo-EM map fitting and density rendering.
- **Mol* (Mol-Star):** Ultra-fast, open-source WebGL library powering the 3D viewers on RCSB PDB and AlphaFold DB.

---

## Worked Example: Parsing Coordinates and Calculating Distances in PDB `1A3N`

### Problem:
Consider the following two atomic coordinate records extracted from Chain B (Beta-Globin) of human deoxyhemoglobin (PDB `1A3N`):

```
ATOM    784  CA  VAL B   1       8.520  34.210  12.150  1.00 24.12           C
...
ATOM    821  CA  GLU B   6      14.820  28.110  18.450  1.00 19.85           C
```

1. Parse each field for Atom 784 and Atom 821.
2. Calculate the 3D Euclidean spatial distance ($d$) between the alpha-carbon ($C_\alpha$) of Valine 1 and the alpha-carbon of Glutamic acid 6 (the site of the sickle-cell mutation!).
3. State whether these two residues could form a direct backbone hydrogen bond.

---

### Step 1: Parse the Coordinate Fields

```
  Field                  Atom 1 (Line 1)          Atom 2 (Line 2)
  -------------------------------------------------------------------------
  Record Name            `ATOM  `                 `ATOM  `
  Atom Serial Number     784                      821
  Atom Name              `CA` (Alpha-Carbon)      `CA` (Alpha-Carbon)
  Residue Name           `VAL` (Valine)           `GLU` (Glutamic acid)
  Chain ID               `B` (Beta-Globin)        `B` (Beta-Globin)
  Residue Sequence No    1                        6
  X Coordinate           8.520 Angstroms          14.820 Angstroms
  Y Coordinate           34.210 Angstroms         28.110 Angstroms
  Z Coordinate           12.150 Angstroms         18.450 Angstroms
  Occupancy              1.00                     1.00
  B-factor               24.12 A^2                19.85 A^2
  Element Symbol         `C` (Carbon)             `C` (Carbon)
```

---

### Step 2: Compute the Euclidean Distance ($d$)

The 3D Cartesian distance formula is:
$$d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2 + (z_2 - z_1)^2}$$

Compute spatial differences:
$$\Delta x = 14.820 - 8.520 = \mathbf{6.300\text{ \AA}}$$
$$\Delta y = 28.110 - 34.210 = \mathbf{-6.100\text{ \AA}}$$
$$\Delta z = 18.450 - 12.150 = \mathbf{6.300\text{ \AA}}$$

Square each delta:
$$(\Delta x)^2 = (6.300)^2 = 39.69$$
$$(\Delta y)^2 = (-6.100)^2 = 37.21$$
$$(\Delta z)^2 = (6.300)^2 = 39.69$$

Sum of squares:
$$\text{Sum} = 39.69 + 37.21 + 39.69 = \mathbf{116.59\text{ \AA}}^2$$

Square root:
$$d = \sqrt{116.59} \approx \mathbf{10.80\text{ \AA}}$$

---

### Step 3: Biophysical Evaluation
- The calculated $C_\alpha - C_\alpha$ distance between Val1 and Glu6 is **$10.80\text{ \AA}$**.
- Standard non-covalent hydrogen bonds operate across distances of $2.7 \text{ to } 3.2\text{ \AA}$ (between donor and acceptor heteroatoms).
- **Conclusion:** A spatial distance of $10.80\text{ \AA}$ is far too large for direct chemical contact. Residues 1 and 6 reside on the solvent-exposed N-terminal tail and Helix A, separated by an extended structural turn, confirming they do not interact directly.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A bioinformatician writes a Python script to parse a PDB file using `line.split()`. In Chain A, an atom has coordinates:  
`ATOM    142  CA  ALA A  19     -10.450-104.230  12.150  1.00 15.00           C`  
Why will `line.split()` corrupt the parsing of this line? How should PDB files be parsed properly?

**Model Answer:**
- **Why it fails:** In this line, the Y-coordinate ($-104.230$) is a large negative number that overflows its allotted column space, merging directly into the X-coordinate ($-10.450$) without any separating whitespace (`-10.450-104.230`). Calling `line.split()` splits strictly on whitespace; it will treat the merged X and Y coordinates as a single corrupted token, shifting all downstream columns (Z-coordinate, occupancy, B-factor) into the wrong array indices.
- **Proper Parsing:** PDB files must be parsed using **strict fixed-width character columnar slicing** according to the official wwPDB specification:  
  `x = float(line[30:38])`, `y = float(line[38:46])`, `z = float(line[46:54])`, or by using dedicated parser libraries such as Biopython's `Bio.PDB.PDBParser`.

---

### Question 2
**Prompt:** In a high-resolution PDB structure of an enzyme, why does the header list an occupancy of $0.50$ for the active-site Serine residue at two different coordinate lines labeled with alternate location indicators `A` and `B`?

**Model Answer:**
An occupancy of **$0.50$** with alternate location indicators `A` and `B` signifies **conformational polymorphism (split rotamers)** in the crystal. In 50% of the unit cells across the crystal, the Serine side chain adopts conformation `A`, while in the other 50% of unit cells, it adopts conformation `B`. Crystallographic refinement software models both rotamer poses, assigning each a 50% occupancy factor so that the total electron density sums to 1.00.

---

### Question 3
**Prompt:** In structural visualization software like VMD or PyMOL, what physical feature of a protein does a "Cartoon" representation reveal that a "Space-Filling (CPK)" representation obscures? Conversely, what does CPK reveal that Cartoon obscures?

**Model Answer:**
- **Cartoon Representation:** Reveals the **overall 3D secondary structure folding topology** (the spatial arrangement of $\alpha$-helices, $\beta$-strands, and loop connections) and allows the viewer to see deep into the interior of the macromolecule, which is completely hidden in CPK.
- **Space-Filling (CPK) Representation:** Reveals the **physical Van der Waals volume and steric surface topography**. It clearly shows atomic packing density, steric clashes, internal solvent cavities, and whether a ligand binding pocket is open or occluded by surrounding side chains.
