# Question Bank: Unit 10 — Structure Databases

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Syllabus Topic:** Introduction to Structure, PDB, MMDB, Structure file format, Visualizing structure information, Structure viewers, Structure similarity searching, Advanced structure modeling  
**Primary Learning Outcome:** LO7 (Navigate PDB/MMDB, parse atomic coordinate records, utilize 3D viewers, evaluate resolution, and understand homology modeling)  

---

## Section A: Multiple Choice Questions (15 MCQs)

### Q01
What is the primary global archive for experimentally determined 3D atomic coordinates of biological macromolecules (proteins, nucleic acids, and complexes)?  
a) GenBank  
b) Worldwide Protein Data Bank (wwPDB)  
c) Swiss-Prot  
d) PubMed Central  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Worldwide Protein Data Bank (wwPDB)  
* **Rationale:** The wwPDB consortium (comprising RCSB PDB, PDBe, PDBj, and BMRB) is the single international archive responsible for maintaining, curating, and distributing 3D atomic coordinates determined by X-ray crystallography, NMR, and Cryo-EM.

### Q02
In a standard 80-column PDB flat file, what is the record name that defines the 3D Cartesian coordinates of standard amino acid residues in a protein backbone?  
a) `HETATM`  
b) `ATOM  `  
c) `SEQRES`  
d) `CONECT`  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) `ATOM  `  
* **Rationale:** The `ATOM  ` record specifies orthogonal Cartesian coordinates ($x, y, z$) for standard chemical components of polymeric biomolecules (amino acids and nucleotides). `HETATM` is reserved for non-polymer hetero groups (water, ions, ligands, heme).

### Q03
Which of the following PDB entries corresponds to the classic deoxy human hemoglobin tetramer structure solved at 1.74 Angstrom resolution?  
a) `4HHB`  
b) `1A3N`  
c) `2HBS`  
d) All of the above are human hemoglobin structures in the PDB  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** d) All of the above are human hemoglobin structures in the PDB  
* **Rationale:** `4HHB` is Fermi's classic deoxyhemoglobin; `1A3N` is T-state deoxyhemoglobin; `2HBS` is the crystal structure of sickle-cell hemoglobin (HbS) exhibiting the pathogenic Glu6Val fiber interaction.

### Q04
In an X-ray crystal structure PDB file, what does a numerical **resolution** of 1.2 Angstroms ($1.2\text{ \AA}$) indicate compared to a resolution of 3.5 Angstroms ($3.5\text{ \AA}$)?  
a) $1.2\text{ \AA}$ represents vastly superior, high-detail structural data where individual atoms and water molecules are clearly resolved in the electron density map  
b) $3.5\text{ \AA}$ represents higher resolution because the number is larger  
c) $1.2\text{ \AA}$ means the protein was crystallized at 1.2 Kelvin  
d) Resolution has no relationship to experimental quality  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) $1.2\text{ \AA}$ represents vastly superior, high-detail structural data where individual atoms and water molecules are clearly resolved in the electron density map  
* **Rationale:** In X-ray crystallography, resolution measures the minimum spatial spacing between crystal lattice planes that diffract X-rays. A smaller numerical value (in Angstroms) means higher resolution: $<1.5\text{ \AA}$ resolves individual atoms, whereas $>3.0\text{ \AA}$ only resolves general backbone traces.

### Q05
What information is recorded in the temperature factor column (also known as the **B-factor** or Debye–Waller factor, columns 61–66) of an `ATOM` record in a PDB file?  
a) The ambient temperature in Celsius of the laboratory room  
b) The thermal mobility and static positional disorder of that specific atom around its mean equilibrium position in the crystal lattice  
c) The melting point of the protein  
d) The number of hydrogen bonds formed by that atom  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The thermal mobility and static positional disorder of that specific atom around its mean equilibrium position in the crystal lattice  
* **Rationale:** The B-factor ($B = 8\pi^2 u^2$) quantifies the mean-square displacement $u^2$ of an atom. Low B-factors ($<20\text{ \AA}^2$) indicate rigid, well-ordered core residues; high B-factors ($>50\text{ \AA}^2$) indicate flexible, mobile surface loops.

### Q06
In a PDB coordinate record, what does the **Occupancy** value (columns 55–60) represent?  
a) The fraction of unit cells in the crystal lattice in which that atom occupies the reported spatial position (ranging from 0.00 to 1.00)  
b) The volume of the atom in cubic Angstroms  
c) The number of solvent water molecules bound to the residue  
d) The percentage of the active site occupied by a drug molecule  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) The fraction of unit cells in the crystal lattice in which that atom occupies the reported spatial position (ranging from 0.00 to 1.00)  
* **Rationale:** Occupancy represents the fraction of crystal copies that contain the atom at the specified $(x, y, z)$ coordinate. It is typically $1.00$ for well-ordered residues, but may be split (e.g., $0.50$ and $0.50$ for alternate conformations A and B of a flexible side chain).

### Q07
Why is the PDB format being progressively replaced by the **PDBx/mmCIF** (macromolecular Crystallographic Information Framework) format?  
a) PDB format files cannot be opened on modern operating systems  
b) The legacy PDB format has a rigid 80-column constraint that cannot handle structures with more than 99,999 atoms or more than 62 distinct chains (such as massive eukaryotic ribosomes and cryo-EM complexes)  
c) mmCIF files do not store 3D coordinates  
d) The United Nations mandated the retirement of four-letter file extensions  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The legacy PDB format has a rigid 80-column constraint that cannot handle structures with more than 99,999 atoms or more than 62 distinct chains (such as massive eukaryotic ribosomes and cryo-EM complexes)  
* **Rationale:** The legacy 1970s PDB format used 5-digit integer columns for atom serial numbers ($99,999$ max) and single-character chain IDs (62 max). Massive complexes like the eukaryotic ribosome ($>200,000$ atoms) break these limits. mmCIF uses flexible tag-value categories without atom or chain count ceilings.

### Q08
Which molecular visualization representation depicts every single non-hydrogen atom as a sphere scaled to its actual van der Waals radius, providing an accurate view of steric packing and molecular surface contours?  
a) Wireframe / Lines  
b) Cartoon / Ribbon  
c) Space-filling / CPK (Corey–Pauling–Koltun)  
d) Trace  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** c) Space-filling / CPK (Corey–Pauling–Koltun)  
* **Rationale:** The CPK (space-filling) model renders each atom as a solid sphere with radius equal to its van der Waals radius. It realistically illustrates molecular volume, surface topography, cavity sizes, and steric clashes, whereas ribbon diagrams trace only secondary structure backbones.

### Q09
What standard CPK color scheme is conventionally applied to render nitrogen, oxygen, carbon, and sulfur atoms in molecular graphics tools like VMD, PyMOL, and Mol*?  
a) Nitrogen = Blue, Oxygen = Red, Carbon = Grey/Black/Green, Sulfur = Yellow  
b) Nitrogen = Red, Oxygen = Blue, Carbon = Yellow, Sulfur = Green  
c) Nitrogen = White, Oxygen = Green, Carbon = Blue, Sulfur = Red  
d) All atoms are colored identically in monochrome grey  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) Nitrogen = Blue, Oxygen = Red, Carbon = Grey/Black/Green, Sulfur = Yellow  
* **Rationale:** The universal CPK element color standard assigns Blue to Nitrogen, Red to Oxygen, White to Hydrogen, Yellow to Sulfur, Orange to Phosphorus, and Grey/Black/Green to Carbon.

### Q10
How does the NCBI Molecular Modeling Database (MMDB) distinguish itself from the raw RCSB PDB repository?  
a) MMDB contains only computationally generated homology models  
b) MMDB reconstructs explicit biological units, adds chemical graph connectivity, and integrates 3D structures directly with NCBI Entrez and VAST+ for structure-similarity querying  
c) MMDB deletes all ligand and water coordinates  
d) MMDB stores structures only in PDF format  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) MMDB reconstructs explicit biological units, adds chemical graph connectivity, and integrates 3D structures directly with NCBI Entrez and VAST+ for structure-similarity querying  
* **Rationale:** MMDB (part of NCBI Structure) parses PDB coordinate files into formal ASN.1 objects, validates chemical bond topology, defines biological assemblies, and pre-calculates structural neighbors using VAST+ (Vector Alignment Search Tool), linking structures to PubMed and GenBank.

### Q11
What metric is universally computed to quantify the structural similarity and spatial superposition error between the $C_\alpha$ backbone atoms of two aligned protein structures?  
a) Bit score  
b) Root Mean Square Deviation (RMSD)  
c) $E$-value  
d) Grand Average of Hydropathicity  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Root Mean Square Deviation (RMSD)  
* **Rationale:** RMSD measures the average distance between equivalent superimposed atoms: $\text{RMSD} = \sqrt{\frac{1}{N}\sum_{i=1}^N d_i^2}$. An RMSD $<2.0\text{ \AA}$ over a substantial core typically indicates identical tertiary folds.

### Q12
In homology (comparative) protein structure modeling, what is the minimum sequence identity threshold below which comparative modeling becomes unreliable due to alignment errors (the "twilight zone")?  
a) 90%  
b) 60%  
c) ~25% to 30%  
d) 5%  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** c) ~25% to 30%  
* **Rationale:** Above ~30% sequence identity, target and template share conserved backbone topology, and standard homology modeling (e.g., SWISS-MODEL, MODELLER) reliably builds accurate models. Below 25–30%, sequence alignments become riddled with shift errors, necessitating threading or deep learning methods (AlphaFold).

### Q13
What is the primary diagnostic plot used to validate the stereochemical quality of the backbone dihedral angles ($\phi$ and $\psi$) in an experimentally determined or computationally modeled protein structure?  
a) Dot plot  
b) Ramachandran plot  
c) Kyte–Doolittle plot  
d) Henderson–Hasselbalch titration curve  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Ramachandran plot  
* **Rationale:** G. N. Ramachandran demonstrated that steric collisions between backbone atoms restrict the torsion angles $\phi$ ($C_\alpha\text{-}N$) and $\psi$ ($C_\alpha\text{-}C$) to favorable energetic regions (alpha-helical and beta-sheet regions). A Ramachandran plot displays $\phi$ vs $\psi$; high-quality structures have $>90\%$ of residues in most-favored regions.

### Q14
What is the function of the `HETATM` record in a PDB file of human deoxyhemoglobin (such as 1A3N)?  
a) It records the amino acid coordinates of the alpha and beta polypeptide chains  
b) It records the coordinates of non-amino-acid hetero groups: the protoporphyrin IX heme rings, central iron ($Fe^{2+}$) ions, and coordinated solvent water molecules  
c) It lists the names of the crystallographers  
d) It specifies the journal article abstract  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) It records the coordinates of non-amino-acid hetero groups: the protoporphyrin IX heme rings, central iron ($Fe^{2+}$) ions, and coordinated solvent water molecules  
* **Rationale:** `HETATM` (Hetero Atom) records coordinates of molecules that are not part of the standard peptide polymer, including the non-protein prosthetic heme group (`HEM`), the catalytic metal atom (`FE`), and crystallographic waters (`HOH`).

### Q15
Which experimental technique determines protein structures by measuring nuclear spin interactions (such as the Nuclear Overhauser Effect - NOE) of proteins in aqueous solution without requiring crystals?  
a) X-ray crystallography  
b) Nuclear Magnetic Resonance (NMR) spectroscopy  
c) Cryo-Electron Microscopy  
d) Circular Dichroism  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Nuclear Magnetic Resonance (NMR) spectroscopy  
* **Rationale:** Solution NMR spectroscopy measures inter-proton distances ($<5\text{ \AA}$) via NOE restraints in aqueous solution. It outputs an ensemble of 20 to 30 low-energy conformers that reflect conformational flexibility in solution, limited to small proteins ($<35\text{ kDa}$).

---

## Section B: Short Answer Questions (6 SAQs)

### SAQ 01: Dissecting an ATOM Coordinate Line (4 Marks)
**Question:** Deconstruct the following authentic PDB `ATOM` line into its constituent fixed-column fields and explain the biological or spatial meaning of each:  
`ATOM     33  CA  VAL A   5      12.450  24.120   8.350  1.00 18.45           C`  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
1. `ATOM`: Record identifier (columns 1–6); specifies standard polymeric biomolecule atom coordinates.
2. `33`: Atom serial number (columns 7–11); unique integer index of this atom in the file.
3. `CA`: Atom name (columns 13–16); denotes the alpha-carbon ($C_\alpha$) of the amino acid backbone.
4. `VAL`: Residue name (columns 18–20); specifies Valine.
5. `A`: Chain identifier (column 22); indicates polypeptide chain A.
6. `5`: Residue sequence number (columns 23–26); specifies position 5 in the sequence.
7. `12.450  24.120   8.350`: Orthogonal Cartesian coordinates $X, Y, Z$ in Angstroms ($\text{\AA}$) relative to the crystal origin (columns 31–38, 39–46, 47–54).
8. `1.00`: Occupancy factor (columns 55–60); indicates 100% presence in this location across crystal unit cells.
9. `18.45`: Temperature factor / B-factor in $\text{\AA}^2$ (columns 61–66); reflects thermal vibration and structural rigidity.
10. `C`: Chemical element symbol (columns 77–78); Carbon.

**Marking Scheme:**  
* 4 Marks: 0.4 marks per correctly identified and explained field.

---

### SAQ 02: PDB vs mmCIF Architecture (3 Marks)
**Question:** Compare the legacy PDB file format with the modern PDBx/mmCIF format across three criteria: maximum atom capacity, data syntax/grammar, and metadata extensibility.  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Analyze  

**Model Answer:**  

| Criterion | Legacy PDB Format | PDBx/mmCIF Format |
| :--- | :--- | :--- |
| **Atom & Chain Capacity** | Strictly capped at 99,999 atoms (5-digit limit) and 62 chains (single alphanumeric characters). | Virtually unlimited atoms and multi-character chain IDs (e.g., `chain_AA1`), easily storing megadalton assemblies. |
| **Data Syntax & Grammar** | Fixed-column 80-character card image format (rigid character positioning). | Category-and-tag dictionary syntax (`_atom_site.Cartn_x`) supporting whitespace-delimited tables and loops. |
| **Metadata Extensibility** | Limited; extra experimental or refinement details crammed into unstructured `REMARK` lines. | Fully extensible; supports rich, standardized relational metadata categories validated against formal dictionaries. |

**Marking Scheme:**  
* 1 Mark per row accurately contrasted.

---

### SAQ 03: X-ray Crystallography vs NMR vs Cryo-EM (4 Marks)
**Question:** Compare the three major experimental methods of protein 3D structure determination (X-ray Crystallography, NMR Spectroscopy, and Cryo-Electron Microscopy) across: physical sample requirement, typical molecular size limitations, and whether the output is a single static coordinate set or a conformational ensemble.  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  

| Experimental Method | Physical Sample Requirement | Molecular Size Limitations | Output Structure Format |
| :--- | :--- | :--- | :--- |
| **X-ray Crystallography** | Highly ordered, 3D single protein crystals. | No strict upper limit; difficult for highly flexible or disordered proteins. | Single static coordinate model (with atomic B-factors representing displacement). |
| **Solution NMR** | Concentrated, stable protein solution labeled with $^{13}C$ and $^{15}N$. | Strictly limited to small-to-medium proteins ($<35\text{--}50\text{ kDa}$). | Conformational ensemble of 20 to 30 low-energy conformers satisfying distance restraints. |
| **Cryo-Electron Microscopy (Cryo-EM)** | Rapidly frozen (vitrified) thin aqueous film; no crystals required. | Optimized for large complexes ($>100\text{ kDa}$ up to gigadalton viruses); difficult for tiny proteins $<50\text{ kDa}$. | Single 3D reconstructed density map and derived atomic coordinate model. |

**Marking Scheme:**  
* 4 Marks: Clear contrast across sample state, size limitations, and static model vs ensemble output.

---

### SAQ 04: Mathematical Formulation of RMSD (3 Marks)
**Question:** Write the mathematical equation for the Root Mean Square Deviation (RMSD) between two aligned protein structures. Define all variables in the equation and state what an RMSD of $0.8\text{ \AA}$ vs $8.5\text{ \AA}$ signifies when superimposing two 150-residue proteins.  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Formula:**  
  $$\text{RMSD} = \sqrt{\frac{1}{N} \sum_{i=1}^N d_i^2} = \sqrt{\frac{1}{N} \sum_{i=1}^N \left( (x_{1,i} - x_{2,i})^2 + (y_{1,i} - y_{2,i})^2 + (z_{1,i} - z_{2,i})^2 \right)}$$  
  Where $N$ is the number of equivalent atom pairs (typically alpha-carbons, $C_\alpha$) and $d_i$ is the Euclidean distance between atom $i$ in Structure 1 and atom $i$ in Structure 2 following optimal rigid-body spatial superposition.
* **Interpretation:**  
  - $\text{RMSD} = 0.8\text{ \AA}$: Extremely close structural identity; the backbones are virtually identical, indicating the same protein solved under different conditions or very close orthologues.  
  - $\text{RMSD} = 8.5\text{ \AA}$: Complete structural divergence; backbones do not superimpose, indicating completely different tertiary folds.

**Marking Scheme:**  
* 1.5 Marks: Correct mathematical formula with $N$ and Euclidean distance $d_i$ defined.  
* 1.5 Marks: Accurate interpretation of $0.8\text{ \AA}$ (virtually identical fold) vs $8.5\text{ \AA}$ (different folds).

---

### SAQ 05: Five Steps of Homology Modeling (3 Marks)
**Question:** List the five core sequential steps involved in building a 3D homology model of a target protein using template-based modeling software (such as SWISS-MODEL or MODELLER).  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
1. **Template Identification:** Query the target sequence against the PDB using BLAST or HHpred to identify homologous experimental structures sharing $>30\%$ sequence identity.
2. **Target–Template Alignment:** Construct a rigorous, error-free pairwise or multiple alignment mapping target residues to template coordinates, ensuring conserved core residues and active sites align properly.
3. **Backbone Model Generation:** Transfer coordinates of aligned regions from the template to the target to construct the core conserved alpha-helical and beta-sheet framework.
4. **Loop Modeling and Side-Chain Rotamer Placement:** Model insertions and deletions (indels) as surface loops using ab initio loop searching or fragment libraries; position amino acid side chains using rotamer conformation libraries.
5. **Model Refinement and Validation:** Minimize steric clashes using energy minimization/molecular dynamics; validate stereochemical geometry using Ramachandran plots (PROCHECK) and energy profiles (Verify3D).

**Marking Scheme:**  
* 3 Marks: 0.6 marks for each correctly named and explained step in proper sequential order.

---

### SAQ 06: Structural Conservation vs Sequence Conservation (3 Marks)
**Question:** "Tertiary structure is significantly more conserved during biological evolution than primary sequence." Provide biophysical evidence supporting this rule and explain its practical utility in bioinformatics.  
* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Biophysical Evidence:**  
  Natural selection primarily acts on macromolecular function, which requires maintaining a stable 3D active site geometry and hydrophobic core folding topology. A polypeptide can accumulate numerous neutral mutations (e.g., conservative substitutions in the interior, or surface variable loops) without destabilizing the core fold. For instance, bacterial leghemoglobin and human myoglobin share only ~15% sequence identity, yet their 3D structures superimpose with an RMSD $<2.0\text{ \AA}$, retaining the classic 8-helix globin fold.
* **Practical Utility in Bioinformatics:**  
  1. Allows structure similarity search tools (DALI, VAST+) to discover ancient evolutionary relationships invisible to BLAST sequence searches.  
  2. Justifies comparative homology modeling: even when sequence identity is modest (30–40%), template backbones provide extraordinarily accurate 3D templates.

**Marking Scheme:**  
* 1.5 Marks: Clear biophysical explanation of selective pressure preserving 3D functional architecture over primary sequence.  
* 1.5 Marks: Concrete biological example (globin family divergence) and practical bioinformatics utility (DALI fold discovery and homology modeling).

---

## Section C: Long Answer / Problem Questions (2 LAQs)

### LAQ 01: Deep Parsing of PDB Records and Active Site Coordination (10 Marks)
**Question:**  
Examine the following excerpt from the crystal structure of deoxy human hemoglobin subunit beta (derived from PDB 1A3N, chain A):  

```text
HEADER    OXYGEN TRANSPORT                        07-MAR-98   1A3N              
COMPND    MOL_ID: 1;                                                            
COMPND   2 MOLECULE: HEMOGLOBIN BETA CHAIN;                                     
REMARK   2 RESOLUTION.    1.80 ANGSTROMS.                                       
REMARK   3 REFINEMENT.  R VALUE (WORKING SET) : 0.178                           
REMARK   3              FREE R VALUE          : 0.215                           
SEQRES   1 A  146  VAL HIS LEU THR PRO GLU GLU LYS SER ALA VAL THR ALA LEU TRP  
SEQRES   2 A  146  GLY LYS VAL ASN VAL ASP GLU VAL GLY GLY GLU ALA LEU GLY ARG  
...
ATOM    480  N   HIS A  92      18.420  15.110  12.300  1.00 14.20           N  
ATOM    481  CA  HIS A  92      19.240  16.280  11.850  1.00 13.80           C  
ATOM    482  C   HIS A  92      18.620  17.580  12.340  1.00 14.10           C  
ATOM    483  O   HIS A  92      19.290  18.590  12.520  1.00 15.30           O  
ATOM    484  CB  HIS A  92      20.680  16.140  12.410  1.00 14.60           C  
ATOM    485  CG  HIS A  92      21.520  15.020  11.870  1.00 15.10           C  
ATOM    486  ND1 HIS A  92      21.150  13.710  12.110  1.00 15.60           N  
ATOM    487  CD2 HIS A  92      22.710  15.010  11.160  1.00 15.40           C  
ATOM    488  CE1 HIS A  92      22.070  12.950  11.580  1.00 15.80           C  
ATOM    489  NE2 HIS A  92      23.040  13.720  10.990  1.00 16.20           N  
...
HETATM 1120 FE   FE  A 147      24.120  12.450   9.320  1.00 14.50          FE  
HETATM 1121  CHA HEM A 147      25.800  14.200   7.800  1.00 16.10           C  
```

a) Evaluate the experimental quality of this structure: interpret the Resolution ($1.80\text{ \AA}$), the $R$-value ($0.178$), and the Free $R$-value ($0.215$). Explain why Free $R$-value was introduced into modern structural refinement. (3 Marks)  
b) Contrast the `SEQRES` record with the `ATOM` coordinate records. If a flexible surface loop is present in the `SEQRES` list but completely missing from the `ATOM` records, explain the physical reason for its absence. (2 Marks)  
c) Histidine 92 represents the critical proximal histidine (F8) that binds the heme iron. Using the 3D Cartesian coordinates provided:  
   - Atom 489: `HIS 92 NE2` at $(23.040, 13.720, 10.990)$  
   - Atom 1120: `FE A 147` at $(24.120, 12.450, 9.320)$  
   Calculate the exact Euclidean physical bond distance (in Angstroms) between the proximal histidine nitrogen `NE2` and the heme iron atom `FE`. Determine whether this distance is consistent with a coordinate covalent bond. (3 Marks)  
d) Explain why the B-factors of the active site atoms (e.g., $13.80\text{--}16.20\text{ \AA}^2$) are significantly lower than those of surface residues (often $>45\text{ \AA}^2$). (2 Marks)  

* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Apply / Analyze  

**Model Solution:**  
**a) Experimental Quality Metrics (3 Marks):**  
* **Resolution ($1.80\text{ \AA}$):** Represents a high-resolution crystal structure. Individual amino acid side chains, peptide bond planes, and ordered water molecules are unambiguously defined in the electron density map.  
* **$R$-value ($0.178$ or $17.8\%$):** Measures discrepancy between observed experimental structure factor amplitudes ($|F_{\text{obs}}|$) and amplitudes calculated from the atomic model ($|F_{\text{calc}}|$). A value $<0.20$ denotes excellent agreement.  
* **Free $R$-value ($R_{\text{free}} = 0.215$):** Computed across a randomly withheld test set of reflections (~5–10% of diffraction data) never used during model refinement.  
* **Why $R_{\text{free}}$ was Introduced:** Traditional $R$-values suffer from mathematical "overfitting" (adjusting hundreds of atomic parameters to fit experimental noise). $R_{\text{free}}$ provides an unbiased statistical cross-validation check; an $R_{\text{free}} - R_{\text{work}}$ gap of $<0.05$ proves the model is not overfitted.

**b) SEQRES vs ATOM Records and Missing Loops (2 Marks):**  
* `SEQRES` lists the complete, chemically intact biological sequence of the protein sample loaded into the crystallization drop.  
* `ATOM` records only those atoms that produce recognizable, interpretable electron density.  
* **Missing Loops:** If a flexible surface loop undergoes dynamic thermal conformational fluctuation, the electron density is smeared out over space. Crystallographers cannot model coordinates into diffuse noise, leaving the residues listed in `SEQRES` but absent from `ATOM` coordinate records.

**c) Euclidean Distance Calculation: Proximal His to Heme Iron (3 Marks):**  
* **Coordinates:**  
  - Point 1 (NE2): $(x_1, y_1, z_1) = (23.040, 13.720, 10.990)$  
  - Point 2 (FE):  $(x_2, y_2, z_2) = (24.120, 12.450, 9.320)$  
* **Coordinate Differences:**  
  - $\Delta x = 24.120 - 23.040 = +1.080\text{ \AA} \implies (\Delta x)^2 = (1.080)^2 = \mathbf{1.1664}$  
  - $\Delta y = 12.450 - 13.720 = -1.270\text{ \AA} \implies (\Delta y)^2 = (-1.270)^2 = \mathbf{1.6129}$  
  - $\Delta z = 9.320 - 10.990 = -1.670\text{ \AA} \implies (\Delta z)^2 = (-1.670)^2 = \mathbf{2.7889}$  
* **Sum of Squares:**  
  $$\sum \Delta^2 = 1.1664 + 1.6129 + 2.7889 = \mathbf{5.5682}$$  
* **Euclidean Distance:**  
  $$d = \sqrt{5.5682} \approx \mathbf{2.36\text{ \AA}}$$  
* **Chemical Consistency:** A coordinate covalent bond between imidazole nitrogen and ferrous iron ($Fe^{2+}$) in deoxyhemoglobin typically spans $2.1\text{ to }2.4\text{ \AA}$. Thus, $2.36\text{ \AA}$ is physically and chemically consistent with authentic coordination.

**d) B-factor Disparity: Active Site Core vs Surface (2 Marks):**  
* **Active Site Rigidity ($B \approx 14\text{--}16\text{ \AA}^2$):** Histidine 92 and the heme iron are buried within the hydrophobic core, anchored by a rigid network of van der Waals contacts and coordinate bonds. Low atomic thermal mobility results in compact electron density and low B-factors.  
* **Surface Residue Mobility ($B > 45\text{ \AA}^2$):** Surface residues contact mobile bulk solvent and experience dynamic conformational fluctuation between multiple rotameric states, broadening the electron density and producing elevated B-factors.

**Marking Scheme Breakdown:**  
* 3 Marks: Clear explanation of resolution ($1.80\text{ \AA}$), working $R$-value, $R_{\text{free}}$, and overfitting prevention.  
* 2 Marks: Precise explanation of `SEQRES` vs `ATOM` records and why high flexibility smears electron density, causing coordinate gaps.  
* 3 Marks: Flawless stepwise 3D Euclidean distance math ($\Delta x^2, \Delta y^2, \Delta z^2$, $\sqrt{5.5682} = 2.36\text{ \AA}$) and confirmation of coordinate covalent coordination.  
* 2 Marks: Physical biophysical justification of low active-site core B-factors vs high solvent-exposed surface B-factors.

---

### LAQ 02: Molecular Modeling Pipelines, Threading, and AlphaFold Structural Evaluation (10 Marks)
**Question:**  
You are leading a computational structural biology team investigating an uncharacterized membrane transporter protein identified from a pathogenic fungus.

a) Construct a decision workflow tree indicating when a structural biologist should employ:  
   1. **Homology (Comparative) Modeling**,  
   2. **Fold Recognition (Threading)**, or  
   3. **Ab Initio / De Novo Deep Learning Modeling (e.g., AlphaFold)** based on sequence identity thresholds and template availability. (3 Marks)  
b) Describe the validation suite applied to evaluate the structural integrity of a newly predicted protein model:  
   - How does a **Ramachandran Plot** assess backbone stereochemistry?  
   - How does **Verify3D** evaluate 3D-1D compatibility?  
   - What threshold percentages define an acceptable, publication-ready model? (3 Marks)  
c) Examine the following AlphaFold structure prediction output for your protein:  
   - Transmembrane helices (residues 30–280): $\text{pLDDT} = 92.4$, low PAE ($<2.5\text{ \AA}$).  
   - N-terminal cytoplasmic domain (residues 1–29): $\text{pLDDT} = 38.1$, high PAE ($>20\text{ \AA}$).  
   Critically interpret these metrics: explain the biological meaning of the pLDDT and Predicted Aligned Error (PAE) values for both regions, and describe how you would present this structure in a publication. (4 Marks)  

* **Learning Outcome:** LO7  
* **Bloom's Taxonomy Level:** Analyze / Synthesize  

**Model Solution:**  
**a) Modeling Strategy Decision Framework (3 Marks):**  
* **Case 1: Sequence Identity $>30\%$ to an Experimental PDB Template:**  
  $\rightarrow$ **Homology / Comparative Modeling (SWISS-MODEL, MODELLER).**  
  *Justification:* Target and template share identical core backbone topology. Alignment is reliable; high-resolution models suitable for virtual drug screening can be generated rapidly.
* **Case 2: Sequence Identity in the "Twilight Zone" ($15\text{--}30\%$), Remote Homologue:**  
  $\rightarrow$ **Fold Recognition / Threading (I-TASSER, Phyre2, HHpred).**  
  *Justification:* Sequence alignment alone fails. Threading fits the query sequence onto known structural folds in the PDB, evaluating energetic compatibility of side-chain packing into candidate fold backbones.
* **Case 3: Sequence Identity $<15\%$ or Completely Novel Fold / Proteome-Wide Modeling:**  
  $\rightarrow$ **Deep Learning / Ab Initio Prediction (AlphaFold2/3, ESMFold).**  
  *Justification:* Utilizes Evoformer neural networks and structural transformers to extract co-evolutionary residue-pair contacts from massive MSAs, synthesizing 3D coordinates without requiring a homologous PDB template.

**b) Model Validation Protocols and Quality Thresholds (3 Marks):**  
* **Ramachandran Plot Validation (PROCHECK / MolProbity):** Evaluates whether backbone dihedral angles ($\phi, \psi$) fall within allowed steric contours.  
  - *Threshold:* A high-quality model requires $\ge 90\%$ of non-glycine/non-proline residues in the **core / most favored regions**, and $\le 1.0\%$ in disallowed regions.
* **Verify3D (3D–1D Compatibility):** Measures the compatibility of each amino acid residue with its 3D structural environment (burial fraction, polar vs nonpolar contacts, secondary structure).  
  - *Threshold:* At least $80\%$ of amino acids must have a 3D-1D score $\ge 0.20$.
* **Overall Stereochemistry:** Tested via ERRAT (non-bonded atomic interactions, threshold $>85$) and QMEAN / ProQ scores for overall fold energetics.

**c) Critical Interpretation of AlphaFold Metrics (4 Marks):**  
1. **Transmembrane Helices (Residues 30–280):**  
   - **pLDDT = 92.4 (Very High Confidence, $>90$):** High accuracy for backbone and side-chain rotamers. The 7-transmembrane bundle is modeled with atomic-level precision comparable to a high-resolution X-ray crystal structure.  
   - **Low PAE ($<2.5\text{ \AA}$):** Predicted Aligned Error between pairs of residues is minimal, proving that the relative spatial positioning and packing of individual helices against one another is determined with high positional certainty.
2. **N-Terminal Cytoplasmic Domain (Residues 1–29):**  
   - **pLDDT = 38.1 (Very Low Confidence, $<50$):** AlphaFold indicates this segment is **Intrinsically Disordered** (an Intrinsically Disordered Region / IDR). It does not adopt a fixed stable 3D conformation in isolation.  
   - **High PAE ($>20\text{ \AA}$):** Indicates undefined relative spatial orientation; the domain moves dynamically relative to the membrane core.
3. **Publication Presentation Protocol:**  
   - Color the 3D ribbon representation strictly by pLDDT confidence (Dark Blue for TM domain $>90$, Light Blue 70–90, Yellow 50–70, Orange/Red $<50$).  
   - Do NOT interpret the N-terminal ribbon as a rigid biological fold; report it explicitly as a predicted intrinsically disordered regulatory or targeting tail.  
   - Provide the 2D PAE matrix plot alongside the structure to substantiate domain-domain orientation certainty.

**Marking Scheme Breakdown:**  
* 3 Marks: Complete decision workflow correctly stratifying $>30\%$ identity (Homology), $15\text{--}30\%$ (Threading), and $<15\%$/novel (AlphaFold).  
* 3 Marks: Detailed explanation of Ramachandran $\phi/\psi$ validation ($>90\%$ favored threshold) and Verify3D 3D-1D environmental scoring ($>80\%$ passing threshold).  
* 4 Marks: Precise interpretation of TM helices ($pLDDT=92.4$, low PAE $\rightarrow$ high confidence atomic fold) vs N-terminus ($pLDDT=38.1$, high PAE $\rightarrow$ intrinsically disordered segment), and professional color-coded publication reporting guidelines.
