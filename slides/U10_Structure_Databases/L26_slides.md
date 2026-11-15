---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 26 Slides: Macromolecular Structure Determination"
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
# Lecture 26 — Macromolecular Structure Determination
### Concepts of Bioinformatics (CBBI-501)
**Unit 10:** Structure Databases  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The 3D Physical Reality of Biology

```text
Topic: Moving Beyond One-Dimensional Sequence Tapes

[Visual: 1D Sequence Tape -> Folding Thermodynamics -> 3D Atomic Architecture
  Human HBB: 147 amino acids -> Folded into 8 alpha-helices cradling a haem group
  Quaternary: alpha_2 beta_2 tetramer transporting 4 oxygen molecules]
```

**Speaker Talking Points:**  
* DNA and mRNA are informational tapes; proteins are nanomachines that execute
  biochemical work in three-dimensional space.
* To understand drug binding, enzyme catalysis, and pathological aggregation (HbS),
  we must determine the exact (x, y, z) Cartesian coordinates of every atom.

---

## Slide 2: The Experimental Triad

```text
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
```

**Speaker Talking Points:**  
* ~85% of historical PDB structures were solved via X-ray crystallography.
* Cryo-EM has undergone a "Resolution Revolution", solving massive complexes without crystals.

---

## Slide 3: X-Ray Crystallography: From Diffraction to Electrons

```text
Topic: Solving the Phase Problem

[Visual: Pipeline Diagram:
  Protein Crystal -> X-Ray Beam -> Diffraction Pattern (Spots / Intensities)
                      |
                      v Fourier Transform + Phases (Molecular Replacement)
  3D Electron Density Map rho(x, y, z) -> Model Building -> Atomic Coordinates]
```

**Speaker Talking Points:**  
* Detectors measure the INTENSITY of diffraction spots, but lose the PHASE.
* The "Phase Problem" is solved via Molecular Replacement (using homologous PDB structures),
  MIR (Heavy-atom isomorphous replacement), or MAD/SAD (anomalous dispersion).

---

## Slide 4: Assessing X-Ray Quality: Resolution (d_min)

```text
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
```

**Speaker Talking Points:**  
* A smaller number means HIGHER resolution (greater resolving power).
* For virtual drug screening and docking, structures must have resolution < 2.5 A.

---

## Slide 5: Assessing Model Quality: R-factor & R_free

```text
Topic: Cross-Validating Crystallographic Models

  R-factor Formula:
    R = Sum ||F_obs| - |F_calc|| / Sum |F_obs|

  * R_work: Measures agreement between calculated model and experimental data.
    (Typical high-quality target: R_work < 0.20 or 20%).

  * R_free (The Cross-Validation Safeguard):
    Calculated on a randomly withheld 5-10% test set of reflections NEVER used
    during model refinement. Prevents over-fitting!
    Rule: R_free should be within 3-5% of R_work (e.g. R_work=0.17, R_free=0.21).
```

**Speaker Talking Points:**  
* If R_free is >0.28 while R_work is 0.15, the crystallographer over-fitted the data!

---

## Slide 6: Solution NMR Spectroscopy

```text
Topic: Capturing Molecular Dynamics in Solution

[Visual: A superposition of 20-40 flexible conformers (NMR Ensemble)
         Rigid secondary structures overlap tightly; loops flutter dynamically!]
```

**Speaker Talking Points:**  
* No crystallization required: protein is analyzed in aqueous physiological buffer.
* Measures Nuclear Overhauser Effect (NOE) inter-proton distances (< 5 Angstroms).
* Output is not a single static model, but an **ensemble of 20-30 conformers**
  satisfying distance restraints, capturing conformational flexibility in solution.
* Historical limit: molecular weight < 30 to 50 kDa.

---

## Slide 7: The Cryo-EM Revolution

```text
Topic: Single-Particle Cryo-Electron Microscopy

[Visual: Flash-freezing in liquid ethane -> Amorphous vitreous ice
         -> Thousands of random 2D projections -> 2D Class Averaging
         -> 3D Fourier Reconstruction (FSC = 0.143 gold standard)]
```

**Speaker Talking Points:**  
* Jacques Dubochet, Joachim Frank, and Richard Henderson (Nobel Prize in Chemistry, 2017).
* Resolves massive megadalton macromolecular assemblies (ribosomes, spliceosomes,
  ion channels, intact viral capsids) without requiring crystals.

---

## Slide 8: The Global Repositories: wwPDB & MMDB

```text
Topic: Where Structural Data Lives

1. Worldwide Protein Data Bank (wwPDB Consortium):
   * RCSB PDB (USA - Rutgers/UCSD)
   * PDBe (Europe - Hinxton, UK)
   * PDBj (Japan - Osaka University)
   * BMRB (BioMagResBank - NMR)

2. NCBI MMDB (Molecular Modeling Database):
   * Converts PDB coordinate files into structured ASN.1 objects.
   * Cross-links structural neighbors via VAST+ secondary structure vector alignments.
```

**Speaker Talking Points:**  
* Next Lecture: Dissecting the PDB format line-by-line (ATOM vs HETATM) and
  3D molecular visualization in VMD and Mol*.

