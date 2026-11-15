# Lecture 26 — Macromolecular Structure Determination

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 10:** Structure Databases  
**Syllabus Topic:** Introduction to Structure, PDB, MMDB  
**Primary Learning Outcome:** LO7 — Query the PDB/MMDB, interpret experimental structure determination methods (X-ray, NMR, Cryo-EM), and evaluate resolution and R-factor.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The 3D Physical Reality of Biology
================================================================================
Topic: Moving Beyond One-Dimensional Sequence Tapes

[Visual: 1D Sequence Tape -> Folding Thermodynamics -> 3D Atomic Architecture
  Human HBB: 147 amino acids -> Folded into 8 alpha-helices cradling a haem group
  Quaternary: alpha_2 beta_2 tetramer transporting 4 oxygen molecules]

Speaker Bullets:
* DNA and mRNA are informational tapes; proteins are nanomachines that execute
  biochemical work in three-dimensional space.
* To understand drug binding, enzyme catalysis, and pathological aggregation (HbS),
  we must determine the exact (x, y, z) Cartesian coordinates of every atom.
```

```
================================================================================
SLIDE 2: The Experimental Triad
================================================================================
Topic: How Macromolecular Structures Are Solved

+--------------------+-------------------------+------------------------------+
| Method             | Physical State          | Physical Basis               |
+--------------------+-------------------------+------------------------------+
| **X-Ray Diff**     | Solid Single Crystal    | Diffraction of X-rays by     |
|                    |                         | electron clouds (Bragg's Law)|
| **Solution NMR**   | Liquid Solution         | Nuclear spin resonance & NOE |
|                    |                         | distance restraints (< 5 A)  |
| **Cryo-EM**        | Vitrified Thin Ice      | Single-particle transmission |
|                    | (Amorphous state)       | electron microscopy          |
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* ~85% of historical PDB structures were solved via X-ray crystallography.
* Cryo-EM has undergone a "Resolution Revolution", solving massive complexes without crystals.
```

```
================================================================================
SLIDE 3: X-Ray Crystallography: From Diffraction to Electrons
================================================================================
Topic: Solving the Phase Problem

[Visual: Pipeline Diagram:
  Protein Crystal -> X-Ray Beam -> Diffraction Pattern (Spots / Intensities)
                      |
                      v Fourier Transform + Phases (Molecular Replacement)
  3D Electron Density Map rho(x, y, z) -> Model Building -> Atomic Coordinates]

Speaker Bullets:
* Detectors measure the INTENSITY of diffraction spots, but lose the PHASE.
* The "Phase Problem" is solved via Molecular Replacement (using homologous PDB structures),
  MIR (Heavy-atom isomorphous replacement), or MAD/SAD (anomalous dispersion).
```

```
================================================================================
SLIDE 4: Assessing X-Ray Quality: Resolution (d_min)
================================================================================
Topic: What Can You Actually See at Different Angstrom Scales?

+--------------------+--------------------------------------------------------+
| Resolution (A)     | Atomic Details Discernible in Electron Density Map     |
+--------------------+--------------------------------------------------------+
| < 1.2 A            | Atomic resolution: individual hydrogen atoms visible!  |
| **1.5 to 2.0 A**   | High resolution: side-chain rotamers unambiguous,      |
|                    | bound water molecules distinct (PDB 1A3N is 1.80 A)    |
| 2.0 to 3.0 A       | Medium resolution: backbone clear, bulky rings resolved|
| > 3.5 A            | Low resolution: only alpha-helical cylinders visible   |
+--------------------+--------------------------------------------------------+

Speaker Bullets:
* A smaller number means HIGHER resolution (greater resolving power).
* For virtual drug screening and docking, structures must have resolution < 2.5 A.
```

```
================================================================================
SLIDE 5: Assessing Model Quality: R-factor & R_free
================================================================================
Topic: Cross-Validating Crystallographic Models

  R-factor Formula:
    R = Sum ||F_obs| - |F_calc|| / Sum |F_obs|

  * R_work: Measures agreement between calculated model and experimental data.
    (Typical high-quality target: R_work < 0.20 or 20%).

  * R_free (The Cross-Validation Safeguard):
    Calculated on a randomly withheld 5-10% test set of reflections NEVER used
    during model refinement. Prevents over-fitting!
    Rule: R_free should be within 3-5% of R_work (e.g. R_work=0.17, R_free=0.21).

Speaker Bullets:
* If R_free is >0.28 while R_work is 0.15, the crystallographer over-fitted the data!
```

```
================================================================================
SLIDE 6: Solution NMR Spectroscopy
================================================================================
Topic: Capturing Molecular Dynamics in Solution

[Visual: A superposition of 20-40 flexible conformers (NMR Ensemble)
         Rigid secondary structures overlap tightly; loops flutter dynamically!]

Speaker Bullets:
* No crystallization required: protein is analyzed in aqueous physiological buffer.
* Measures Nuclear Overhauser Effect (NOE) inter-proton distances (< 5 Angstroms).
* Output is not a single static model, but an **ensemble of 20-30 conformers**
  satisfying distance restraints, capturing conformational flexibility in solution.
* Historical limit: molecular weight < 30 to 50 kDa.
```

```
================================================================================
SLIDE 7: The Cryo-EM Revolution
================================================================================
Topic: Single-Particle Cryo-Electron Microscopy

[Visual: Flash-freezing in liquid ethane -> Amorphous vitreous ice
         -> Thousands of random 2D projections -> 2D Class Averaging
         -> 3D Fourier Reconstruction (FSC = 0.143 gold standard)]

Speaker Bullets:
* Jacques Dubochet, Joachim Frank, and Richard Henderson (Nobel Prize in Chemistry, 2017).
* Resolves massive megadalton macromolecular assemblies (ribosomes, spliceosomes,
  ion channels, intact viral capsids) without requiring crystals.
```

```
================================================================================
SLIDE 8: The Global Repositories: wwPDB & MMDB
================================================================================
Topic: Where Structural Data Lives

1. Worldwide Protein Data Bank (wwPDB Consortium):
   * RCSB PDB (USA - Rutgers/UCSD)
   * PDBe (Europe - Hinxton, UK)
   * PDBj (Japan - Osaka University)
   * BMRB (BioMagResBank - NMR)

2. NCBI MMDB (Molecular Modeling Database):
   * Converts PDB coordinate files into structured ASN.1 objects.
   * Cross-links structural neighbors via VAST+ secondary structure vector alignments.

Speaker Bullets:
* Next Lecture: Dissecting the PDB format line-by-line (ATOM vs HETATM) and
  3D molecular visualization in VMD and Mol*.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Experimental Modalities of Structural Biology

While genomic and transcriptomic sequencing can be performed in high-throughput automated instruments, resolving the three-dimensional atomic coordinates of a macromolecule requires rigorous physical chemistry. The Protein Data Bank (PDB) currently houses over 210,000 macromolecular structures determined by three primary biophysical modalities:

```
  Metric                 X-Ray Crystallography       Solution NMR Spectroscopy   Single-Particle Cryo-EM
  -------------------------------------------------------------------------------------------------
  Relative PDB Share     ~83% of total archive       ~6% of total archive        ~11% (Rapidly exploding)
  Sample Physical State  Dehydrated single crystal   Soluble aqueous solution    Vitrified in amorphous ice
  Primary Data Recorded  Diffraction spot intensity  Chemical shifts, J-couplings, Thousands of low-dose 2D
                         (reciprocal space lattice)  NOE distance restraints     electron transmission images
  Resolution Benchmark   Bragg spacing (d_min in A)  Number of NOE restraints    Fourier Shell Correlation
                                                     per residue                 (FSC cutoff = 0.143)
  Model Representation   Single static coordinate    Ensemble of 20-40 plausible 3D volumetric Coulomb
                         set + thermal B-factors     conformers                  potential electron density
  Size Limitations       Must crystallize; no mass   Historically limited to     Historically required >100 kDa;
                         limit (Ribosome to virus)   small proteins (<35-50 kDa) now resolving down to 50 kDa
```

---

### 2. X-Ray Crystallography: The Mechanics of Resolution

In X-ray crystallography, proteins are induced to precipitate into an ordered, three-dimensional crystalline lattice through hanging-drop or sitting-drop vapor diffusion against precipitating buffers (PEG, ammonium sulfate).

#### A. Diffraction and Bragg's Law
Because the wavelength of X-rays ($\lambda \approx 0.5 \text{ to } 1.5\text{ \AA}$) matches the length of covalent chemical bonds ($C-C \approx 1.54\text{ \AA}$), X-ray photons interact with the electron clouds of the atoms in the crystal lattice. Constructive interference of scattered waves occurs according to **Bragg's Law**:

$$n\lambda = 2d \sin\theta$$

where $d$ is the interplanar spacing between crystalline lattice planes, and $\theta$ is the scattering angle.

#### B. The Phase Problem
An X-ray detector records the position and **intensity** ($I_{hkl}$) of each diffraction spot (reflection). The structure factor amplitude is proportional to the square root of intensity:
$$|F_{hkl}| \propto \sqrt{I_{hkl}}$$
However, physical detectors measure only photon energy; the **phase angle** ($\phi_{hkl}$) of the electromagnetic wave is completely lost. Without phases, a direct inverse Fourier transform cannot be computed to reconstruct the real-space 3D electron density map $\rho(x, y, z)$.

**Solutions to the Phase Problem:**
1. **Molecular Replacement (MR):** If an experimentally solved homolog exists in the PDB ($>30\%$ sequence identity), its coordinates are computationally rotated and translated into the target unit cell to provide initial trial phases.
2. **Isomorphous Replacement (MIR / SIR):** Crystals are soaked with heavy-metal salts ($\text{Hg}^{2+}, \text{Pt}^{2+}, \text{Au}^{3+}$), which scatter X-rays anomalously to deduce phases.
3. **Anomalous Dispersion (MAD / SAD):** Recombinant proteins are expressed incorporating Selenomethionine (Se-Met) instead of natural Methionine, allowing tuning of synchrotron X-ray wavelengths to extract phases directly.

#### C. Resolution ($d_{\min}$):
The resolution represents the shortest interplanar spacing ($d_{\min}$) of reflections observed on the outer edge of the diffraction detector.

```
  Resolution Metric      Biochemical Quality and Interpretive Reliability
  -------------------------------------------------------------------------------------------------
  1.0 to 1.2 Angstroms   True atomic resolution. Individual carbon, nitrogen, oxygen atoms 
                         resolved as distinct spherical density peaks; hydrogen atoms visible.
  1.5 to 2.0 Angstroms   High resolution. Polypeptide backbone traced unambiguously; side-chain
                         rotamers distinct; bound co-factors (haem) and structural waters clear.
                         **PDB 1A3N (Human Deoxyhemoglobin) is 1.80 Angstroms.**
  2.5 to 3.0 Angstroms   Medium resolution. Backbone trace reliable, but peptide planes and 
                         flexible side chains must be inferred from geometric rotamer libraries.
  > 3.5 Angstroms        Low resolution. Individual side chains cannot be resolved; only alpha-helical
                         cylinders and broad beta-sheet envelopes are visible.
```

#### D. The Crystallographic R-Factor and $R_{\text{free}}$:
To measure how accurately an atomic model matches the experimental diffraction data, crystallographers calculate the **R-factor ($R_{\text{work}}$)**:

$$R_{\text{work}} = \frac{\sum_{hkl} ||F_{\text{obs}}(hkl)| - |F_{\text{calc}}(hkl)||}{\sum_{hkl} |F_{\text{obs}}(hkl)|}$$

where $F_{\text{obs}}$ is the experimentally measured structure factor amplitude and $F_{\text{calc}}$ is the amplitude calculated mathematically from the atomic coordinates. For a model to be publishable, $R_{\text{work}}$ must typically be below **$0.20\text{ (20\%)}$**.

**The Invention of $R_{\text{free}}$ (Axel Brünger, 1992):**  
Because a crystallographer can artificially decrease $R_{\text{work}}$ by introducing hundreds of arbitrary parameters (over-fitting/over-refinement), Brünger introduced **$R_{\text{free}}$**. Before refinement begins, a random 5% to 10% subset of experimental reflections is set aside and never used during model building. $R_{\text{free}}$ is calculated exclusively on this withheld test set:
- In a well-refined, authentic structure: $R_{\text{free}}$ is within **$3\%$ to $5\%$** of $R_{\text{work}}$ (e.g., $R_{\text{work}} = 0.17$, $R_{\text{free}} = 0.21$).
- If $R_{\text{free}} - R_{\text{work}} > 0.08$ (e.g., $R_{\text{work}} = 0.15$ but $R_{\text{free}} = 0.28$), the model suffers from severe over-fitting and false coordinate placement.

---

### 3. Nuclear Magnetic Resonance (NMR) Spectroscopy

Unlike X-ray crystallography, NMR spectroscopy determines macromolecular structures directly in **liquid aqueous solution**, avoiding crystal packing artifacts and capturing conformational dynamics under physiological conditions.

#### Biophysical Mechanism:
1. Samples are enriched in stable NMR-active isotopes with non-zero nuclear spin: $^{1}\text{H}$, $^{13}\text{C}$, and $^{15}\text{N}$.
2. Placed in an ultra-high magnetic field (600 to 900 MHz), radiofrequency pulses excite nuclear spin transitions.
3. **NOESY (Nuclear Overhauser Effect Spectroscopy):** Measures through-space dipole-dipole cross-relaxation between protons located within **$< 5.0\text{ \AA}$** of each other.
4. Computational distance-geometry and simulated annealing algorithms generate an **ensemble of 20 to 40 conformers** that all satisfy the observed experimental distance restraints.
5. In PDB files (e.g., PDB `1G03`), the NMR entry contains multiple structural models overlaid on one another; regions of high structural convergence indicate rigid secondary elements, while divergent "frayed" regions represent dynamic, disordered loops.

---

### 4. Cryo-Electron Microscopy (Cryo-EM)

Over the past decade, Cryo-EM has transformed structural biology (Nobel Prize in Chemistry 2017: Jacques Dubochet, Joachim Frank, and Richard Henderson).

#### Single-Particle Analysis (SPA) Workflow:
1. **Rapid Vitrification:** A few microliters of aqueous protein solution are applied to a carbon grid and plunged into liquid ethane cooled by liquid nitrogen (cooling rate $>100,000\text{ K/s}$). This ultra-fast cooling prevents water molecules from organizing into crystalline ice, freezing them into amorphous, glass-like **vitreous ice** that preserves native macromolecular architecture without damage.
2. **Transmission Electron Microscopy:** High-energy electron beams (200–300 kV) image the grid at cryogenic temperatures, capturing thousands of individual macromolecular particles in random orientations.
3. **2D Class Averaging:** Software aligns and clusters hundreds of thousands of noisy 2D particle images, canceling out noise to yield crisp 2D projection classes.
4. **3D Reconstruction:** Mathematical back-projection algorithms combine the 2D angular classes into a 3D Coulomb potential density map.
5. **Resolution Metric (FSC):** The map resolution is calculated using the **Fourier Shell Correlation (FSC)** between two independently refined half-datasets, using the gold-standard **$\text{FSC} = 0.143$ threshold**.

---

## Worked Example: Evaluating Crystallographic Validation Parameters for PDB `1A3N`

### Problem:
Examine the following authentic metadata extracted from the `REMARK 2` and `REMARK 3` header records of PDB entry **`1A3N`** (Human Deoxyhemoglobin, T-State, complexed with haem):

```
REMARK   2 RESOLUTION.    1.80 ANGSTROMS.
...
REMARK   3   FIT TO DATA USED IN REFINEMENT.
REMARK   3    CROSS-VALIDATION METHOD          : THROUGHOUT
REMARK   3    FREE R VALUE TEST SET SELECTION   : RANDOM
REMARK   3    R VALUE     (WORKING + TEST SET) : 0.169
REMARK   3    R VALUE            (WORKING SET) : 0.167
REMARK   3    FREE R VALUE                     : 0.215
REMARK   3    FREE R VALUE TEST SET SIZE   (%) : 5.0
```

1. State the experimental resolution ($d_{\min}$) and evaluate its quality.
2. Assess the refinement reliability using $R_{\text{work}}$ and $R_{\text{free}}$.
3. Determine whether this coordinate file is suitable for atomic-resolution molecular docking of small-molecule sickle-cell polymerization inhibitors.

---

### Analytical Evaluation:

1. **Resolution Assessment:**
   - Resolution is **$1.80\text{ \AA}$**.
   - A resolution of $1.80\text{ \AA}$ falls squarely into the **high-resolution bracket** ($1.5 - 2.0\text{ \AA}$). At $1.80\text{ \AA}$, the electron density map unambiguously traces the polypeptide backbone, side-chain rotamer orientations are clearly resolved, and individual ordered water molecules coordinating the haem pocket are distinct.
2. **R-Factor Reliability Assessment:**
   - $R_{\text{work}} = 0.167$ ($16.7\%$). This is well below the standard quality threshold of $0.20$ ($20\%$), indicating strong agreement between the atomic coordinates and experimental diffraction spot intensities.
   - $R_{\text{free}} = 0.215$ ($21.5\%$). The difference between $R_{\text{free}}$ and $R_{\text{work}}$ is:
     $$\Delta R = R_{\text{free}} - R_{\text{work}} = 0.215 - 0.167 = 0.048\text{ (4.8\%)}$$
   - A gap of $4.8\%$ is within the acceptable $3-5\%$ tolerance for well-refined structures, confirming that the model has not been over-fitted or biased by excessive free parameters.
3. **Suitability for Molecular Drug Docking:**
   - **Conclusion:** **Highly suitable.**
   - For molecular docking, errors in side-chain coordinates or active-site geometry will produce false steric clashes and corrupted binding energies. PDB `1A3N` provides atomic-level precision ($1.80\text{ \AA}$, $R_{\text{free}} = 0.215$), making it an ideal gold-standard structural template for modeling small-molecule inhibitors designed to bind near residue 6 (Valine in HbS) to prevent pathological deoxyhemoglobin polymerization.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A pharmaceutical structural biologist is comparing two crystal structures of a drug target in the PDB: Structure A has a reported resolution of $1.60\text{ \AA}$, while Structure B has a reported resolution of $3.20\text{ \AA}$. Explain why Structure A is superior for computational drug design, citing two specific chemical features visible at $1.6\text{ \AA}$ that cannot be resolved at $3.2\text{ \AA}$.

**Model Answer:**
- **Why Structure A is superior:** In X-ray crystallography, a smaller numerical resolution value represents greater resolving power and higher optical detail. Structure A ($1.60\text{ \AA}$) provides atomic-level detail, whereas Structure B ($3.20\text{ \AA}$) provides only low-to-medium resolution envelope density.
- **Two specific features visible at $1.6\text{ \AA}$ but invisible at $3.2\text{ \AA}$:**
  1. **Side-Chain Rotamer Conformations:** At $1.6\text{ \AA}$, individual side-chain rotamers (e.g. the exact dihedral angles of active-site Lys, Arg, and Tyr residues) are unambiguously resolved. At $3.2\text{ \AA}$, side-chain density is blurred, forcing the modeler to guess rotamer orientations.
  2. **Ordered Water Molecules:** At $1.6\text{ \AA}$, bound solvent water molecules mediating critical hydrogen bonds between the drug and protein are resolved as discrete spherical peaks. At $3.2\text{ \AA}$, water molecules cannot be distinguished from background noise.

---

### Question 2
**Prompt:** In X-ray crystallography, why is the Phase Problem considered the central barrier to calculating an electron density map? Name two experimental or computational methods used to solve it.

**Model Answer:**
- **The Phase Problem:** When X-rays scatter off electrons in a crystal, detectors record only the intensity ($I_{hkl}$) of each reflection (from which wave amplitudes $|F_{hkl}|$ are derived). The phase angle ($\phi_{hkl}$) of the electromagnetic wave is completely lost. Because calculating the real-space 3D electron density map $\rho(x, y, z)$ requires performing a Fourier summation over both amplitudes *and* phases, structural determination cannot proceed without estimating or recovering the lost phase angles.
- **Two Methods to Solve It:**
  1. **Molecular Replacement (MR):** Uses the known 3D coordinates of an homologous protein ($>30\%$ sequence identity) as a trial phasing model.
  2. **Single or Multi-Wavelength Anomalous Dispersion (SAD / MAD):** Incorporates anomalous X-ray scatterers (such as Selenomethionine) and tunes synchrotron radiation to directly extract phase angles from anomalous diffraction differences.

---

### Question 3
**Prompt:** When viewing an NMR-determined structure entry in the PDB, why does the coordinate file contain 20 or 30 complete structural models overlaid on one another, whereas an X-ray crystallography entry contains only one?

**Model Answer:**
- **X-Ray Crystallography:** Derives coordinates by fitting atoms into a single, time- and space-averaged 3D electron density map averaged across billions of unit cells in a rigid crystal lattice, producing a single static consensus coordinate set.
- **Solution NMR:** Measures distance restraints (primarily $<5\text{ \AA}$ proton-proton NOEs) in aqueous solution. Because macromolecules in solution are dynamic and flexible, many slightly different 3D conformations can satisfy the same experimental distance restraints equally well. NMR software calculates an **ensemble of 20 to 30 conformers** that all conform to the experimental restraints, capturing the true thermodynamic flexibility and conformational landscape of the protein in liquid solution.
