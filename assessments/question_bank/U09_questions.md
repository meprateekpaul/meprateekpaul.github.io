# Question Bank: Unit 9 — Predictive Methods using Protein Sequence

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Syllabus Topic:** Protein identification based on composition, Physical properties based on sequence, Motif and pattern, Secondary structure and folding classes, specialized structure or features, Tertiary structures  
**Primary Learning Outcome:** LO6 (Compute physicochemical properties, scan PROSITE motifs, evaluate secondary structure methods, and categorize fold classes)  

---

## Section A: Multiple Choice Questions (15 MCQs)

### Q01
When calculating the theoretical molecular weight of a linear polypeptide from its amino acid sequence, why cannot one simply sum the molecular weights of all individual free amino acids?  
a) Free amino acids contain heavy isotopes that disappear in proteins  
b) For every peptide bond formed between two adjacent amino acids during ribosomal synthesis, one molecule of water ($H_2O$, $18.015\text{ Da}$) is eliminated via a condensation reaction  
c) The genetic code compresses amino acids when translated  
d) Amino acids lose their alpha-carbons when incorporated into a chain  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) For every peptide bond formed between two adjacent amino acids during ribosomal synthesis, one molecule of water ($H_2O$, $18.015\text{ Da}$) is eliminated via a condensation reaction  
* **Rationale:** Peptide bond formation is a condensation reaction. For a protein of $N$ residues, $N-1$ peptide bonds are formed, releasing $N-1$ water molecules. Thus: $\text{MW}_{\text{protein}} = \sum (\text{MW}_{\text{free aa}}) - (N-1) \times 18.015\text{ Da}$.

### Q02
What is the definition of the theoretical isoelectric point (pI) of a protein?  
a) The temperature at which the protein unfolds completely  
b) The specific pH at which the net electrical charge of the protein molecule equals exactly zero  
c) The pH at which the protein reaches its maximum enzymatic velocity  
d) The percentage of hydrophobic residues present in the interior core  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) The specific pH at which the net electrical charge of the protein molecule equals exactly zero  
* **Rationale:** The isoelectric point (pI) is the pH at which the sum of positive charges on basic groups ($N$-terminus, Lys, Arg, His) equals the sum of negative charges on acidic groups ($C$-terminus, Asp, Glu, Cys, Tyr), yielding a net molecular charge of zero.

### Q03
Which two aromatic amino acid residues contribute predominantly to the molar extinction coefficient ($\epsilon$) of a protein at 280 nm in near-UV spectrophotometry?  
a) Glycine and Alanine  
b) Tryptophan and Tyrosine  
c) Aspartate and Glutamate  
d) Leucine and Isoleucine  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Tryptophan and Tyrosine  
* **Rationale:** Tryptophan ($\epsilon_{280} \approx 5500\text{ M}^{-1}\text{cm}^{-1}$) and Tyrosine ($\epsilon_{280} \approx 1490\text{ M}^{-1}\text{cm}^{-1}$) contain conjugated aromatic ring systems that absorb strongly at 280 nm. Cystine disulfides provide minor absorbance ($\epsilon_{280} \approx 125\text{ M}^{-1}\text{cm}^{-1}$).

### Q04
In the Expasy ProtParam tool, what does an **Instability Index** value greater than 40 indicate regarding the protein's behavior in experimental biochemical assays?  
a) The protein is predicted to be thermostable up to 100 degrees Celsius  
b) The protein is predicted to be biochemically unstable in vitro (short half-life, prone to degradation)  
c) The protein is an integral membrane channel  
d) The protein contains more than 10 disulfide bonds  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The protein is predicted to be biochemically unstable in vitro (short half-life, prone to degradation)  
* **Rationale:** Guruprasad et al. (1990) correlated dipeptide composition with in vivo protein half-lives. A computed instability index $<40$ predicts in vitro stability; an index $>40$ flags the protein as unstable.

### Q05
What does a positive Grand Average of Hydropathicity (GRAVY) score calculated by ProtParam indicate about a protein?  
a) The protein is highly hydrophilic and globally soluble in aqueous buffers  
b) The protein is overall hydrophobic (characteristic of integral membrane proteins or hydrophobic core domains)  
c) The protein has a basic isoelectric point ($pI > 9$)  
d) The protein has an abnormal number of glycine residues  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The protein is overall hydrophobic (characteristic of integral membrane proteins or hydrophobic core domains)  
* **Rationale:** On the Kyte–Doolittle hydropathy scale, hydrophobic residues have positive values (e.g., Isoleucine $= +4.5$) and hydrophilic residues have negative values (e.g., Arginine $= -4.5$). The GRAVY score is the sum of hydropathy values divided by protein length; positive values denote hydrophobicity.

### Q06
When constructing a Kyte–Doolittle hydropathy plot to identify putative transmembrane alpha-helices, what is the standard recommended sliding window size?  
a) 3 to 5 residues  
b) 7 to 9 residues  
c) 19 to 21 residues  
d) 50 to 60 residues  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** c) 19 to 21 residues  
* **Rationale:** A biological lipid bilayer has a hydrophobic core of approximately $30\text{ \AA}$. Spanning this distance in a standard alpha-helix ($1.5\text{ \AA}$ rise per residue) requires roughly $30 / 1.5 = 20$ amino acids. A window of 19–21 residues matches this physical dimension. Windows of 7–9 are used to find surface loops/antigenic sites.

### Q07
Examine the following PROSITE pattern: `[LIVMF]-x(2)-[DE]-x-[LIVMF]`. Which of the following pentapeptides strictly matches this pattern?  
a) `L - A - G - D - K - V`  
b) `L - A - D - K - V`  
c) `K - A - G - D - K - L`  
d) `V - A - G - R - K - I`  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** a) `L - A - G - D - K - V`  
* **Rationale:** Deconstructing `[LIVMF]-x(2)-[DE]-x-[LIVMF]`:  
  - Pos 1: One of L, I, V, M, F $\rightarrow$ `L` (match)  
  - Pos 2-3: Exactly 2 arbitrary residues $\rightarrow$ `A - G` (match)  
  - Pos 4: One of D or E $\rightarrow$ `D` (match)  
  - Pos 5: Exactly 1 arbitrary residue $\rightarrow$ `K` (match)  
  - Pos 6: One of L, I, V, M, F $\rightarrow$ `V` (match)  
  Total length is 6 residues. Option (a) matches every position perfectly.

### Q08
In PROSITE syntax, what does an expression enclosed in curly braces `{ }` designate?  
a) Any amino acid belonging to the enclosed set is accepted  
b) Any amino acid EXCEPT the enclosed residues is accepted (forbidden residues)  
c) The enclosed residues must be repeated three times  
d) The sequence is located at the carboxyl terminus  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Any amino acid EXCEPT the enclosed residues is accepted (forbidden residues)  
* **Rationale:** In PROSITE grammar, square brackets `[ ]` specify permitted residues (e.g., `[ALT]` means Ala, Leu, or Thr). Curly braces `{ }` specify forbidden residues (e.g., `{P}` means any amino acid except Proline).

### Q09
What biological rule (the "positive-inside rule" discovered by Gunnar von Heijne) governs the topological orientation of integral transmembrane proteins?  
a) Transmembrane helices contain only positively charged residues  
b) Positively charged residues (Lysine and Arginine) are significantly more abundant in the cytosolic (intracellular) loops connecting transmembrane helices than in the extracytosolic/periplasmic loops  
c) Proteins only insert into membranes if the outside buffer pH is positive  
d) The carboxyl terminus must always carry a net $+5$ charge  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Positively charged residues (Lysine and Arginine) are significantly more abundant in the cytosolic (intracellular) loops connecting transmembrane helices than in the extracytosolic/periplasmic loops  
* **Rationale:** The electrical membrane potential of cells is interior-negative. Translocation of positively charged basic residues (Lys, Arg) across the membrane is energetically unfavorable, causing them to be retained on the cytosolic side (the positive-inside rule used by tools like TMHMM).

### Q10
What structural repeating motif characterizes the alpha-helical coiled-coil domain?  
a) A 10-residue repeat containing alternating prolines  
b) A continuous stretch of 30 glycine residues  
c) A heptad repeat of seven residues designated `(a-b-c-d-e-f-g)_n`, where positions `a` and `d` are predominantly apolar/hydrophobic amino acids  
d) A zinc-finger coordination sequence containing 4 histidines  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** c) A heptad repeat of seven residues designated `(a-b-c-d-e-f-g)_n`, where positions `a` and `d` are predominantly apolar/hydrophobic amino acids  
* **Rationale:** Coiled coils (e.g., leucine zippers) feature heptad repeats $(a\text{-}b\text{-}c\text{-}d\text{-}e\text{-}f\text{-}g)_n$. Because an alpha-helix has ~3.6 residues per turn, positions $a$ and $d$ align on the same face of the helix, creating a hydrophobic stripe that buries against a partner helix in a left-handed supercoil. Positions $e$ and $g$ are typically charged, forming inter-helical salt bridges.

### Q11
How does the GOR (Garnier–Osgood–Robson) secondary structure prediction algorithm evaluate whether a residue adopts an alpha-helix, beta-sheet, or coil state?  
a) By downloading AlphaFold structures from the web  
b) By evaluating the joint probability and information theory parameters within a sliding 17-residue window ($j-8$ to $j+8$) centered on the target residue  
c) By checking whether the residue is hydrophobic or hydrophilic  
d) By counting only the overall amino acid composition of the full protein  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) By evaluating the joint probability and information theory parameters within a sliding 17-residue window ($j-8$ to $j+8$) centered on the target residue  
* **Rationale:** GOR uses directional information theory. It accounts for the conformational influence of 8 flanking residues on either side of the target residue ($j-8$ to $j+8$, a 17-residue window), summing information functions $I(S_j; R_{j+m})$ for Helix, Sheet, and Coil.

### Q12
Why does the PSIPRED secondary structure prediction method achieve dramatically higher accuracy ($Q_3 \approx 81\text{--}84\%$) than single-sequence methods like Chou–Fasman or GOR IV ($Q_3 \approx 60\text{--}65\%$)?  
a) PSIPRED uses experimental X-ray crystallography during prediction  
b) PSIPRED feeds evolutionary information in the form of a PSI-BLAST Position-Specific Scoring Matrix (PSSM) into a two-stage artificial neural network  
c) PSIPRED evaluates only short sequences under 50 residues  
d) PSIPRED predicts only alpha-helices and ignores beta-sheets  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) PSIPRED feeds evolutionary information in the form of a PSI-BLAST Position-Specific Scoring Matrix (PSSM) into a two-stage artificial neural network  
* **Rationale:** Secondary structure is far more conserved than primary sequence. A PSSM profile derived from PSI-BLAST captures evolutionary conservation and positional substitution tolerances across dozens of homologues, providing vastly richer biophysical signals to the neural network than a single isolated sequence.

### Q13
How is the three-state secondary structure prediction accuracy metric $Q_3$ calculated?  
a) The ratio of alpha-helices to beta-sheets in the structure  
b) The total number of residues correctly predicted as Helix, Sheet, or Coil divided by the total number of residues, expressed as a percentage: $Q_3 = \frac{N_\alpha + N_\beta + N_C}{N_{\text{total}}} \times 100\%$  
c) The root mean square deviation of atomic coordinates  
d) The crystallization resolution divided by the R-factor  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) The total number of residues correctly predicted as Helix, Sheet, or Coil divided by the total number of residues, expressed as a percentage: $Q_3 = \frac{N_\alpha + N_\beta + N_C}{N_{\text{total}}} \times 100\%$  
* **Rationale:** $Q_3$ is the standard benchmark metric: the percentage of all sequence residues whose predicted conformational state ($H, E, C$) matches the true state assigned from experimental coordinates by DSSP.

### Q14
Into which major structural folding class does human haemoglobin beta (*HBB*, globin fold) fall according to the SCOP and CATH structural classification hierarchies?  
a) All-beta  
b) All-alpha  
c) Alpha/Beta ($\alpha/\beta$) alternating  
d) Alpha + Beta ($\alpha+\beta$) segregated  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) All-alpha  
* **Rationale:** The globin fold is a classic all-alpha protein structure consisting of 8 distinct alpha-helices (designated helices A through H) folded into a compact globular bundle that encapsulates the heme prosthetic group, devoid of beta-strands.

### Q15
What is the structural hierarchy used by the CATH protein domain classification database?  
a) Class, Architecture, Topology (Fold family), Homologous superfamily  
b) Domain, Phylum, Class, Order  
c) Alpha, Beta, Loop, Coil  
d) Primary, Secondary, Tertiary, Quaternary  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) Class, Architecture, Topology (Fold family), Homologous superfamily  
* **Rationale:** CATH hierarchically classifies protein domain structures into: **C** (Class: secondary structure content, e.g. mainly alpha), **A** (Architecture: spatial arrangement of secondary structures), **T** (Topology: connectivity and fold family), and **H** (Homologous superfamily: proven common ancestry).

---

## Section B: Short Answer Questions (6 SAQs)

### SAQ 01: Hand Calculation of Molar Extinction Coefficient (3 Marks)
**Question:** A purified recombinant human protein contains 3 Tryptophan (Trp) residues, 6 Tyrosine (Tyr) residues, and 4 Cysteine residues that form 2 internal disulfide bonds (cystines). Using standard molar extinction coefficients at 280 nm ($\epsilon_{\text{Trp}} = 5500\text{ M}^{-1}\text{cm}^{-1}$, $\epsilon_{\text{Tyr}} = 1490\text{ M}^{-1}\text{cm}^{-1}$, $\epsilon_{\text{cystine}} = 125\text{ M}^{-1}\text{cm}^{-1}$), calculate the theoretical total molar extinction coefficient ($\epsilon_{280}$) of the folded protein.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Formula:**  
  $$\epsilon_{280} = (N_{\text{Trp}} \times 5500) + (N_{\text{Tyr}} \times 1490) + (N_{\text{cystine}} \times 125)$$  
* **Step-by-Step Arithmetic:**  
  - For 3 Trp: $3 \times 5500 = 16,500\text{ M}^{-1}\text{cm}^{-1}$  
  - For 6 Tyr: $6 \times 1490 = 8,940\text{ M}^{-1}\text{cm}^{-1}$  
  - For 2 cystine disulfide bonds: $2 \times 125 = 250\text{ M}^{-1}\text{cm}^{-1}$  
  $$\text{Total } \epsilon_{280} = 16,500 + 8,940 + 250 = \mathbf{25,690\text{ M}^{-1}\text{cm}^{-1}}$$  
*(Note: If cysteines are reduced to free thiols, $\epsilon_{\text{cystine}} = 0$, yielding $25,440\text{ M}^{-1}\text{cm}^{-1}$).*

**Marking Scheme:**  
* 1 Mark: Correct formula stating contribution of Trp, Tyr, and cystine disulfides.  
* 2 Marks: Flawless multiplication and addition yielding $25,690\text{ M}^{-1}\text{cm}^{-1}$ (or $25,440$ if reduced thiols noted).

---

### SAQ 02: Deconstructing PROSITE Pattern Grammar (4 Marks)
**Question:** Translate the following PROSITE syntax pattern into plain English and explain the biochemical significance of each component:  
`[FY]-x-[LIVM]-x(2)-{P}-G-[DE]`  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Residue-by-Residue Translation:**  
  1. `[FY]`: Position 1 must be an aromatic residue—either Phenylalanine (F) or Tyrosine (Y).
  2. `-x-`: Position 2 can be any of the 20 standard amino acids.
  3. `[LIVM]`: Position 3 must be an aliphatic/hydrophobic core residue—Leucine (L), Isoleucine (I), Valine (V), or Methionine (M).
  4. `-x(2)-`: Positions 4 and 5 represent a spacer of exactly two arbitrary amino acids.
  5. `{P}`: Position 6 can be ANY amino acid EXCEPT Proline (proline is strictly forbidden, likely to preserve an unconstrained backbone conformation).
  6. `-G-`: Position 7 must be an invariant Glycine (G), typically providing conformational flexibility or accommodating tight steric packing.
  7. `[DE]`: Position 8 must be a negatively charged acidic residue—Aspartate (D) or Glutamate (E), frequently acting in electrostatic coordination or catalysis.
* **Total Length:** Matches a specific octapeptide motif (8 amino acids long).

**Marking Scheme:**  
* 3 Marks: 0.5 marks per correctly explained segment (`[FY]`, `x`, `[LIVM]`, `x(2)`, `{P}`, `G`, `[DE]`).  
* 1 Mark: Clear identification of total pattern length (8 residues) and biochemical rationale for `{P}` (proline avoidance) and `[DE]` (acidic charge).

---

### SAQ 03: Architecture of Signal Peptides (3 Marks)
**Question:** Describe the three distinct structural domains that comprise a canonical eukaryotic secretory signal peptide (n-region, h-region, c-region) and state the "$-3, -1$ rule" of signal peptidase cleavage.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Three Structural Regions:**  
  1. **n-region (N-terminal domain):** Short ($1\text{--}5$ residues) carrying a net positive charge (contains basic residues like Arg or Lys) that interacts with the translocon.
  2. **h-region (Hydrophobic core):** Central uninterrupted stretch of 7 to 15 strongly hydrophobic, uncharged residues (Leu, Ala, Val, Phe) forming an alpha-helix that inserts into the Sec61 translocation channel.
  3. **c-region (C-terminal cleavage domain):** Short ($3\text{--}7$ residues) of neutral, polar amino acids that presents a recognizable cleavage motif to signal peptidase.
* **The "$-3, -1$ Rule" (von Heijne):** Residues at positions $-3$ and $-1$ relative to the cleavage site must be small and neutral (typically Ala, Gly, or Ser; never bulky, aromatic, or charged residues) to fit into the catalytic pocket of signal peptidase.

**Marking Scheme:**  
* 1.5 Marks: 0.5 marks for accurate description of n-region, h-region, and c-region.  
* 1.5 Marks: Detailed statement of the "$-3, -1$ rule" requiring small neutral residues (Ala/Gly/Ser).

---

### SAQ 04: The Henderson-Hasselbalch Equation in pI Calculation (3 Marks)
**Question:** Explain how bioinformatics software (such as Expasy Compute pI/Mw) calculates the isoelectric point of a protein sequence using the Henderson–Hasselbalch equation and binary bisection search.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Net Charge Equation:** For any pH, the net electrical charge $Q(\text{pH})$ is calculated by summing the fractional ionization states of all ionizable groups:  
  $$Q(\text{pH}) = \sum \frac{1}{1 + 10^{\text{pH} - pK_a(\text{basic})}} - \sum \frac{1}{1 + 10^{pK_a(\text{acidic}) - \text{pH}}}$$  
  Where basic groups include the $N$-terminus, Lys, Arg, and His; acidic groups include the $C$-terminus, Asp, Glu, Cys, and Tyr.
* **Binary Bisection Iteration:** Because $Q(\text{pH})$ is a monotonically decreasing function:
  1. The software tests a midpoint pH (e.g., pH 7.0) between bounds [0, 14].
  2. If $Q > 0$, the true pI lies at a higher pH (set lower bound = 7.0). If $Q < 0$, it lies at a lower pH (set upper bound = 7.0).
  3. The algorithm bisects the interval repeatedly until $|Q| < 0.001$, converging on the theoretical pI in $<15$ computational steps.

**Marking Scheme:**  
* 1.5 Marks: Clear formulation of fractional ionization based on Henderson-Hasselbalch for basic and acidic side chains.  
* 1.5 Marks: Clear explanation of monotonic charge behavior and iterative binary bisection search convergence.

---

### SAQ 05: Chou-Fasman vs GOR Methods (3 Marks)
**Question:** Contrast the Chou–Fasman method with the GOR IV method for secondary structure prediction across three criteria: underlying theoretical framework, window size considered, and reported $Q_3$ prediction accuracy.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Analyze  

**Model Answer:**  

| Criterion | Chou–Fasman Method (1974) | GOR IV Method (Garnier et al., 1996) |
| :--- | :--- | :--- |
| **Theoretical Framework** | Empirical statistical propensity tables ($P_\alpha, P_\beta, P_{\text{turn}}$) with manual nucleation/propagation rules. | Information theory and Bayesian probability calculating mutual information functions $I(S; R)$. |
| **Window Size** | Nucleation cores (e.g., 4 out of 6 residues for helix; 3 out of 5 for sheet). | Fixed sliding window of 17 residues ($j-8$ to $j+8$) evaluating flanking residue influences. |
| **$Q_3$ Accuracy** | Approximately 50% to 55% (barely better than random guessing on modern benchmark datasets). | Approximately 64% to 65%. |

**Marking Scheme:**  
* 1 Mark per table row accurately contrasted.

---

### SAQ 06: Folding Classes: $\alpha/\beta$ vs $\alpha+\beta$ (4 Marks)
**Question:** In structural biology classification (SCOP and CATH), distinguish between the **Alpha/Beta ($\alpha/\beta$)** folding class and the **Alpha + Beta ($\alpha+\beta$)** folding class. Provide one classic protein example of each.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Alpha/Beta ($\alpha/\beta$) Class:**  
  - *Structural Topology:* Consists of alternating alpha-helices and beta-strands along the polypeptide chain ($\beta\text{-}\alpha\text{-}\beta$ units). The beta-strands are predominantly **parallel** and form an internal central core (beta-barrel or open beta-sheet) surrounded by an exterior sheath of amphipathic alpha-helices.  
  - *Classic Example:* Triosephosphate Isomerase (TIM barrel fold) or the Rossmann fold (nucleotide-binding dehydrogenases).
* **Alpha + Beta ($\alpha+\beta$) Class:**  
  - *Structural Topology:* Alpha-helices and beta-strands are segregated into distinct, separate regions of the primary sequence and 3D structure. The beta-strands are predominantly **anti-parallel** and form a sheet in one structural sector, while alpha-helices cluster in an independent adjacent sector.  
  - *Classic Example:* Lysozyme, Ribonuclease A, or T4 Lysozyme.

**Marking Scheme:**  
* 1.5 Marks: Detailed topological description of alternating $\alpha/\beta$ parallel architectures.  
* 1.5 Marks: Detailed topological description of segregated $\alpha+\beta$ anti-parallel architectures.  
* 1 Mark: 0.5 marks for an accurate example of each class (TIM barrel vs Lysozyme/RNase A).

---

## Section C: Long Answer / Problem Questions (2 LAQs)

### LAQ 01: Complete Physicochemical Profile Calculation and Hydropathy Analysis (10 Marks)
**Question:**  
You are provided with the amino acid sequence of a short synthetic therapeutic peptide designed to target bacterial membranes:  
`Sequence: M - K - F - L - A - A - L - E - K - V` (10 residues)

The following biophysical parameters are provided:  
* **Molecular Weights of Free Amino Acids:**  
  `M: 149.2, K: 146.2, F: 165.2, L: 131.2, A: 89.1, E: 147.1, V: 117.1 Da`  
  Water ($H_2O$) = $18.0\text{ Da}$
* **$pK_a$ Values of Ionizable Groups:**  
  $N$-terminus $= 9.6$, $C$-terminus $= 2.2$, Lysine ($\epsilon$-amino) $= 10.5$, Glutamate ($\gamma$-carboxyl) $= 4.2$
* **Kyte–Doolittle Hydropathy Index Values:**  
  `M: +1.9, K: -3.9, F: +2.8, L: +3.8, A: +1.8, E: -3.5, V: +4.2`

a) Calculate the exact theoretical molecular weight of the intact 10-residue peptide. (2 Marks)  
b) Determine the net electrical charge of the peptide at:  
   1. $\text{pH} = 1.0$  
   2. $\text{pH} = 7.0$  
   3. $\text{pH} = 13.0$  
   Estimate the approximate theoretical isoelectric point (pI) of this peptide. (4 Marks)  
c) Calculate the Grand Average of Hydropathicity (GRAVY) score of this peptide. State whether the peptide is overall hydrophobic or hydrophilic. (2 Marks)  
d) If this peptide forms an ideal amphipathic alpha-helix, map residues onto an alpha-helical wheel projection (3.6 residues per turn). Explain how an amphipathic helix allows the peptide to disrupt bacterial lipid bilayers. (2 Marks)  

* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply / Analyze  

**Model Solution:**  
**a) Molecular Weight Calculation (2 Marks):**  
* Sum of free amino acid masses:  
  - $1 \times \text{M} = 149.2$  
  - $2 \times \text{K} = 2 \times 146.2 = 292.4$  
  - $1 \times \text{F} = 165.2$  
  - $2 \times \text{L} = 2 \times 131.2 = 262.4$  
  - $2 \times \text{A} = 2 \times 89.1 = 178.2$  
  - $1 \times \text{E} = 147.1$  
  - $1 \times \text{V} = 117.1$  
  $$\sum \text{Free Mass} = 149.2 + 292.4 + 165.2 + 262.4 + 178.2 + 147.1 + 117.1 = \mathbf{1311.6\text{ Da}}$$
* Peptide bond condensation loss:  
  For 10 residues, 9 peptide bonds form, eliminating 9 water molecules:  
  $$9 \times 18.0\text{ Da} = \mathbf{162.0\text{ Da}}$$
* **Net Polypeptide Weight:**  
  $$\text{MW} = 1311.6 - 162.0 = \mathbf{1149.6\text{ Da}}$$

**b) Net Charge Calculation Across pH and pI Estimation (4 Marks):**  
The ionizable groups in `M-K-F-L-A-A-L-E-K-V` are:
- $N$-terminal $\alpha$-amino ($pK_a = 9.6$): basic ($+1$ protonated, $0$ deprotonated)
- $C$-terminal $\alpha$-carboxyl ($pK_a = 2.2$): acidic ($0$ protonated, $-1$ deprotonated)
- $2 \times$ Lys side chains ($pK_a = 10.5$): basic ($+1$ protonated each)
- $1 \times$ Glu side chain ($pK_a = 4.2$): acidic ($0$ protonated, $-1$ deprotonated)

1. **At pH 1.0:**  
   - All groups are fully protonated ($\text{pH} \ll pK_a$).  
   - $N$-term $= +1$, $2 \times \text{Lys} = +2$.  
   - $C$-term $= 0$, $\text{Glu} = 0$.  
   $$\text{Net Charge at pH 1.0} = +1 + 2 + 0 + 0 = \mathbf{+3}$$
2. **At pH 7.0:**  
   - $N$-term ($pK_a 9.6$): protonated $= +1$.  
   - $2 \times \text{Lys}$ ($pK_a 10.5$): protonated $= +2$.  
   - $C$-term ($pK_a 2.2$): deprotonated $= -1$.  
   - $\text{Glu}$ ($pK_a 4.2$): deprotonated $= -1$.  
   $$\text{Net Charge at pH 7.0} = (+1) + (+2) + (-1) + (-1) = \mathbf{+1}$$
3. **At pH 13.0:**  
   - All groups are fully deprotonated ($\text{pH} \gg pK_a$).  
   - $N$-term $= 0$, $2 \times \text{Lys} = 0$.  
   - $C$-term $= -1$, $\text{Glu} = -1$.  
   $$\text{Net Charge at pH 13.0} = 0 + 0 + (-1) + (-1) = \mathbf{-2}$$
* **Isoelectric Point (pI) Estimation:**  
  At pH 7.0, net charge is $+1$. Deprotonation of the next group with lowest $pK_a$ (the $N$-terminal amino group, $pK_a = 9.6$) drops the charge from $+1$ to $0$. The subsequent ionization occurs at Lys ($pK_a = 10.5$).  
  $$\text{Theoretical pI} = \frac{pK_a(N\text{-term}) + pK_a(\text{Lys})}{2} = \frac{9.6 + 10.5}{2} = \mathbf{10.05}$$

**c) GRAVY Score Calculation (2 Marks):**  
Sum of Kyte-Doolittle hydropathy values:
- M: $+1.9$
- K: $-3.9$
- F: $+2.8$
- L: $+3.8$
- A: $+1.8$
- A: $+1.8$
- L: $+3.8$
- E: $-3.5$
- K: $-3.9$
- V: $+4.2$  
$$\sum \text{Hydropathy} = 1.9 - 3.9 + 2.8 + 3.8 + 1.8 + 1.8 + 3.8 - 3.5 - 3.9 + 4.2 = \mathbf{+8.8}$$  
$$\text{GRAVY} = \frac{\sum \text{Hydropathy}}{L} = \frac{+8.8}{10} = \mathbf{+0.88}$$  
* **Conclusion:** Because the GRAVY score is strongly positive ($+0.88$), the peptide is classified as **overall hydrophobic**.

**d) Helical Wheel Projection and Membrane Disruption (2 Marks):**  
* **Helical Wheel Mapping (100° per residue):**  
  - Residues 1 (`M`), 3 (`F`), 4 (`L`), 6 (`A`), 7 (`L`), 10 (`V`) cluster on one spatial face of the alpha-helix, forming a continuous hydrophobic face.  
  - Residues 2 (`K`), 8 (`E`), 9 (`K`) cluster on the opposite face, forming a charged, polar face.
* **Mechanism of Bacterial Membrane Disruption:**  
  1. The positively charged face (Lysine $+2$ net charge) is electrostatically attracted to the negatively charged phospholipid headgroups (phosphatidylglycerol / lipid A) of the bacterial outer leaflet.  
  2. Upon binding, the peptide folds into an amphipathic helix; the hydrophobic face inserts directly into the fatty acid core of the membrane bilayer, creating toroidal pores or carpet-like disruption that lyses the bacterial cell.

**Marking Scheme Breakdown:**  
* 2 Marks: Flawless molecular weight calculation ($1149.6\text{ Da}$) showing water loss subtraction.  
* 4 Marks: Stepwise net charge determination at pH 1 ($+3$), pH 7 ($+1$), and pH 13 ($-2$) with correct pI derivation ($10.05$).  
* 2 Marks: Flawless GRAVY calculation ($+0.88$) and correct hydrophobic classification.  
* 2 Marks: Clear description of amphipathic face segregation on a helical wheel and electrostatic/hydrophobic bacterial membrane lysis mechanism.

---

### LAQ 02: Evaluating Secondary Structure Prediction: Confusion Matrix and Q3 Benchmark (10 Marks)
**Question:**  
A bioinformatics student benchmarks a newly developed machine-learning secondary structure predictor against the real DSSP-assigned structure of human beta-globin (*HBB*, length $L = 140$ test residues). The comparison yields the following $3 \times 3$ confusion matrix:  

```text
                     Observed Structure (DSSP Ground Truth)
Predicted Structure     Helix (H)     Sheet (E)     Coil (C)     Total Predicted
  Helix (H)                80             2            8               90
  Sheet (E)                 4            16            5               25
  Coil (C)                  6             2           17               25
Total Observed             90            20           30              140
```

a) Define the $Q_3$ metric. Using the values from the confusion matrix, calculate the overall three-state prediction accuracy ($Q_3$) of this algorithm. (3 Marks)  
b) Calculate the **Sensitivity** (Recall) and **Specificity** (Positive Predictive Value / Precision) specifically for the **Helix (H)** state. Show all calculations. (3 Marks)  
c) Analyze the performance disparity across the three conformational states (Helix, Sheet, Coil). Explain why secondary structure prediction methods historically achieve significantly higher accuracy on alpha-helices than on beta-strands. (2 Marks)  
d) Describe how modern deep learning approaches (such as AlphaFold) shifted structural bioinformatics from simple 1D 3-state strings ($Q_3$) to full 3D coordinate prediction using Evoformer attention and structural loss functions. Explain what the pLDDT confidence score represents. (2 Marks)  

* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Analyze / Apply  

**Model Solution:**  
**a) $Q_3$ Definition and Calculation (3 Marks):**  
* **Definition:** $Q_3$ is the percentage of all residues for which the predicted secondary structural state ($H, E, C$) matches the experimentally assigned state:  
  $$Q_3 = \frac{\sum_{i \in \{H, E, C\}} \text{True Positives}_i}{N_{\text{total}}} \times 100\% = \frac{TP_H + TP_E + TP_C}{N_{\text{total}}} \times 100\%$$
* **Calculation:**  
  - Correctly predicted Helices ($TP_H$): 80  
  - Correctly predicted Sheets ($TP_E$): 16  
  - Correctly predicted Coils ($TP_C$): 17  
  - Total correctly predicted residues: $80 + 16 + 17 = 113$  
  - Total residues ($N_{\text{total}}$): 140  
  $$Q_3 = \frac{113}{140} \times 100\% = \mathbf{80.71\%}$$

**b) Helix Sensitivity and Precision Calculations (3 Marks):**  
1. **Sensitivity (Recall for Helix):**  
   Measures the proportion of actual observed helices that were correctly identified:  
   $$\text{Sensitivity}_H = \frac{TP_H}{\text{Total Observed}_H} = \frac{80}{90} = \mathbf{0.8889 \quad (88.89\%)}$$
2. **Precision (Positive Predictive Value for Helix):**  
   Measures the proportion of predicted helices that are truly helices:  
   $$\text{Precision}_H = \frac{TP_H}{\text{Total Predicted}_H} = \frac{80}{90} = \mathbf{0.8889 \quad (88.89\%)}$$  
*(Both values happen to be $80/90$ due to matrix totals).*

**c) Performance Disparity: Helices vs Sheets (2 Marks):**  
* **Disparity:** Alpha-helices exhibit high accuracy (~89%), while beta-strands have lower accuracy ($16/20 = 80\%$ recall, but $16/25 = 64\%$ precision with notable cross-prediction).
* **Physical & Biological Reason:**  
  - **Local vs Non-Local Interactions:** Alpha-helices are stabilized by strictly **local** hydrogen bonds between residue $i$ and residue $i+4$. A local sliding window of 10–15 residues captures all physical interactions required to form a helix.
  - Beta-sheets are stabilized by hydrogen bonds between distinct beta-strands that are often separated by dozens or hundreds of residues in primary sequence, or reside on entirely separate polypeptide chains. Local window methods cannot capture long-range tertiary pairing interactions, leading to higher error rates in strand prediction.

**d) Deep Learning Revolution: AlphaFold and pLDDT (2 Marks):**  
* **From 1D $Q_3$ to 3D End-to-End Structure:** Rather than predicting isolated 1D strings of secondary structure states, AlphaFold processes multiple sequence alignments (MSAs) and pairwise residue representations through an "Evoformer" neural network. It iteratively refines spatial residue-pair geometry via invariant point attention, outputting full 3D Cartesian coordinates $(x, y, z)$ directly.
* **The pLDDT Metric (predicted Local Distance Difference Test):**  
  - pLDDT measures AlphaFold's per-residue confidence on a 0 to 100 scale:  
    - **$>90$ (Very High):** Highly reliable backbone and side-chain rotamers (comparable to high-resolution X-ray structures).  
    - **$70\text{--}90$ (Confident):** Reliable backbone topology.  
    - **$50\text{--}70$ (Low):** Uncertain backbone orientation.  
    - **$<50$ (Very Low):** Often indicates intrinsically disordered regions (IDRs) or flexible, unstructured loops.

**Marking Scheme Breakdown:**  
* 3 Marks: Formal definition of $Q_3$ and flawless arithmetic yielding $Q_3 = 80.71\%$.  
* 3 Marks: Stepwise sensitivity ($88.89\%$) and precision ($88.89\%$) calculations with explicit formulas.  
* 2 Marks: Physical biophysical explanation contrasting local $i \rightarrow i+4$ helical hydrogen bonding with long-range non-local beta-sheet pairing.  
* 2 Marks: Clear overview of AlphaFold end-to-end 3D coordinate prediction and precise calibration bands of the pLDDT metric.
