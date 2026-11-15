# Quiz 4: Units 8–10 — Sequence Prediction, Motifs & Macromolecular Structure

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Units Covered:** Unit 8 (Predictive Methods - DNA), Unit 9 (Predictive Methods - Protein), Unit 10 (Structure Databases)  
**Time Allowed:** 15 Minutes  
**Maximum Marks:** 10 Marks  
**Nature of Examination:** Closed Book, Individual Assessment  

---

## Part I: Student Test Paper

### Instructions to Candidates
1. Answer all questions in the allotted space.
2. Maintain computational clarity and show calculation steps where appropriate.

---

### Question 1: Multiple Choice Concept Checks (4 Marks)

**(a)** In the canonical eukaryotic pre-mRNA splicing process, which invariant dinucleotide pair defines the 5' splice donor and 3' splice acceptor junctions? `[1 Mark]`  
[  ] A) `AT...GC`  
[  ] B) `GT...AG`  
[  ] C) `AG...GT`  
[  ] D) `CT...GA`  

**(b)** What does an **Instability Index** value of 48.5 calculated by Expasy ProtParam indicate about a protein? `[1 Mark]`  
[  ] A) The protein is predicted to be stable in vitro ($<40$)  
[  ] B) The protein is predicted to be unstable in vitro ($>40$)  
[  ] C) The protein has a melting point of 48.5 degrees Celsius  
[  ] D) The protein is an integral membrane receptor  

**(c)** In a standard PDB flat file, what record type specifies non-polymer coordinates such as crystallographic water molecules (`HOH`) and heme prosthetic groups (`HEM`)? `[1 Mark]`  
[  ] A) `ATOM  `  
[  ] B) `SEQRES`  
[  ] C) `HETATM`  
[  ] D) `CONECT`  

**(d)** What does a smaller numerical **resolution** value (e.g., $1.4\text{ \AA}$ vs $3.2\text{ \AA}$) signify in X-ray crystallography? `[1 Mark]`  
[  ] A) Higher experimental detail where individual atoms are distinctly resolved  
[  ] B) Lower experimental detail  
[  ] C) Faster computer processing speed  
[  ] D) Higher rate of radiation damage to the crystal  

---

### Question 2: ProtParam Physicochemical Calculations (3 Marks)

A short biological peptide has the sequence: `Trp - Tyr - Tyr - Cys - Cys` (5 amino acids).  
* The two Cysteine residues form one internal disulfide bond (cystine).  
* Molar extinction coefficients at 280 nm:  
  $\epsilon_{\text{Trp}} = 5500\text{ M}^{-1}\text{cm}^{-1}$, $\epsilon_{\text{Tyr}} = 1490\text{ M}^{-1}\text{cm}^{-1}$, $\epsilon_{\text{cystine}} = 125\text{ M}^{-1}\text{cm}^{-1}$.

1. Calculate the total theoretical molar extinction coefficient ($\epsilon_{280}$) of this folded peptide. Show your arithmetic. `[2 Marks]`  
2. If this peptide is measured in a standard $1\text{ cm}$ path-length quartz cuvette and displays an absorbance $A_{280} = 0.86$, estimate the molar concentration of the peptide solution using the Beer–Lambert law ($A = \epsilon \cdot c \cdot l$). `[1 Mark]`  

---

### Question 3: PROSITE Pattern Decoding & PDB B-factors (3 Marks)

1. Deconstruct the PROSITE pattern `C-x(2,4)-C-x(12)-H-x(3)-H` (classic $C_2H_2$ Zinc Finger motif). State the exact residues and spacing required. `[2 Marks]`  
2. What does an abnormally high **B-factor** ($>60\text{ \AA}^2$) in an `ATOM` record indicate regarding that residue's physical behavior in the crystal? `[1 Mark]`  

---
---

## Part II: Instructor Answer Key & Marking Scheme

### Question 1: Multiple Choice Answers (4 Marks)
* **(a)** **B) `GT...AG`** `[1 Mark]`  
  *Rationale:* Canonical nuclear introns begin with invariant $5'\text{-GT-}3'$ (donor) and end with invariant $5'\text{-AG-}3'$ (acceptor).
* **(b)** **B) The protein is predicted to be unstable in vitro ($>40$)** `[1 Mark]`  
  *Rationale:* Guruprasad's instability index classifies values $<40$ as stable, and $>40$ as unstable.
* **(c)** **C) `HETATM`** `[1 Mark]`  
  *Rationale:* `HETATM` records hetero atoms (ligands, prosthetic groups, water). Standard amino acids use `ATOM`.
* **(d)** **A) Higher experimental detail where individual atoms are distinctly resolved** `[1 Mark]`  
  *Rationale:* Resolution measures minimum plane spacing; smaller Angstrom values denote higher spatial resolving power.

---

### Question 2: ProtParam Physicochemical Calculations (3 Marks)

* **1. Molar Extinction Coefficient Calculation (2 Marks):**  
  * Formula: $\epsilon_{280} = (1 \times \epsilon_{\text{Trp}}) + (2 \times \epsilon_{\text{Tyr}}) + (1 \times \epsilon_{\text{cystine}})$  
  * Values:  
    - $1 \times \text{Trp} = 1 \times 5500 = 5500$  
    - $2 \times \text{Tyr} = 2 \times 1490 = 2980$  
    - $1 \times \text{cystine} = 1 \times 125 = 125$  
  * Total $\epsilon_{280} = 5500 + 2980 + 125 = \mathbf{8605\text{ M}^{-1}\text{cm}^{-1}}$ `[2 Marks]`  
    *(Give 1.5 marks if cystine is omitted yielding 8480).*

* **2. Beer–Lambert Concentration Calculation (1 Mark):**  
  $$c = \frac{A}{\epsilon \cdot l} = \frac{0.86}{8605\text{ M}^{-1}\text{cm}^{-1} \times 1\text{ cm}} \approx 0.0000999\text{ M} \approx \mathbf{0.10\text{ mM}} \quad (100\text{ }\mu\text{M})$$ `[1 Mark]`

---

### Question 3: PROSITE Pattern Decoding & PDB B-factors (3 Marks)

* **1. PROSITE Pattern Deconstruction (2 Marks):**  
  `C-x(2,4)-C-x(12)-H-x(3)-H`  
  - Invariant Cysteine (`C`), followed by a variable spacer of 2 to 4 arbitrary amino acids (`x(2,4)`).  
  - Second invariant Cysteine (`C`), followed by a fixed spacer of exactly 12 amino acids (`x(12)`).  
  - Invariant Histidine (`H`), followed by a fixed spacer of exactly 3 amino acids (`x(3)`).  
  - Second invariant Histidine (`H`).  
  *(Function: Coordinates a structural $Zn^{2+}$ ion between the 2 Cys and 2 His residues).* `[2 Marks]`

* **2. High B-factor Meaning (1 Mark):**  
  A high B-factor ($>60\text{ \AA}^2$) indicates high **thermal mobility, static conformational disorder, or flexible surface loop movement**, meaning the atom fluctuates widely around its mean position in the crystal lattice. `[1 Mark]`
