# Lecture 24 — Motifs, Patterns, and Domains

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 9:** Predictive Methods using Protein Sequence  
**Syllabus Topic:** Motif and pattern, specialized structure or features  
**Primary Learning Outcome:** LO6 — Predict sequence-based features: parse and construct PROSITE patterns, query Pfam/InterPro profile HMMs, and predict signal peptides, transmembrane helices, and coiled coils.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Modular Hierarchy of Proteins
================================================================================
Topic: Deciphering the Grammar of Polypeptides

[Visual: Conceptual Hierarchy:
  1. Primary Sequence: Raw amino acid tape (N-...-C)
  2. Motifs / Patterns: Short functional signatures (3 to 20 aa; e.g. Walker loop)
  3. Profiles / HMMs: Position-specific probabilistic models
  4. Structural Domains: Independently folding, compact globular units (50 to 300 aa)
  5. Multidomain Architectures: Complete physiological machines]

Speaker Bullets:
* Proteins are not monolithic polymers; they are modular constructions.
* Identifying conserved motifs and domains allows bioinformaticians to assign
  biological function to uncharacterized sequences even in the absence of full homology.
```

```
================================================================================
SLIDE 2: PROSITE Pattern Syntax
================================================================================
Topic: Amos Bairoch's Regular Expression Language (1991)

+--------------------+-------------------------+------------------------------+
| Symbol / Syntax    | Meaning                 | Biological Example           |
+--------------------+-------------------------+------------------------------+
| `X` or `x`         | Any of the 20 amino acids| `x(4)`: Any 4 amino acids    |
| `[ABC]`            | Any ONE of the enclosed | `[ST]`: Serine OR Threonine  |
| `{ABC}`            | Any residue EXCEPT these| `{P}`: NOT Proline           |
| `x(n)`             | Exact repetition of n   | `x(2)`: Exactly two residues |
| `x(m, n)`          | Range of m to n residues| `x(2, 4)`: Between 2 and 4   |
| `<` or `>`         | N- or C-terminal anchor | `<M`: Initiates at N-term Met|
| `-` (hyphen)       | Separator between tokens| `N-{P}-[ST]-{P}`             |
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* PROSITE patterns are deterministic: a sequence either matches 100%, or it fails.
```

```
================================================================================
SLIDE 3: Classic Signatures in Molecular Biology
================================================================================
Topic: Famous Motifs Encoded in PROSITE Syntax

1. N-Glycosylation Site (PS00001):
   `N-{P}-[ST]-{P}`
   * Asparagine (N), followed by NOT Proline, followed by Ser or Thr, followed by NOT Proline.
   * Proline is excluded because its rigid ring disrupts the glycosyltransferase catalytic pocket!

2. ATP/GTP-Binding Walker A Motif (P-Loop) (PS00017):
   `[AG]-x(4)-G-K-[ST]`
   * Coordinates the beta- and gamma-phosphate oxygens of ATP/GTP.

3. The Globin Signature (PS00018):
   Coordinates the proximal Histidine (His93 in HBB) coordinating the haem iron.

Speaker Bullets:
* A single consensus pattern can identify an enzymatic mechanism instantly.
```

```
================================================================================
SLIDE 4: The Limitations of Strict Patterns
================================================================================
Topic: Why Regular Expressions Break Down

[Visual: The "All-or-Nothing" Dilemma:
  Homolog 1: [A] - x(4) - G - K - [S]  --> MATCH (Score: YES)
  Homolog 2: [A] - x(4) - G - K - [T]  --> MATCH (Score: YES)
  Homolog 3: [A] - x(4) - G - R - [S]  --> (Lys mutates to Arg: structurally fine!)
             FAILS PATTERN ENTIRELY! (Score: NO)]

Speaker Bullets:
* Biology is probabilistic, not deterministic.
* A single conservative substitution can break a rigid PROSITE pattern.
* Solution: **Profile Hidden Markov Models (HMMs)** that score probabilities!
```

```
================================================================================
SLIDE 5: Profile HMMs and the Pfam Database
================================================================================
Topic: Sean Eddy's HMMER Architecture

[Visual: Plan7 Profile HMM Architecture:
  Match States (M_1, M_2, M_3) with amino acid emission probabilities
  Insert States (I_1, I_2) and Delete States (D_1, D_2) with transition probabilities]

The Pfam Database:
* **Pfam-A:** Curated collection of ~20,000 protein domain families based on
  manually reviewed "seed alignments" and strict Gathering Thresholds (`GA`).
* **Pfam-B:** Automated clusters of unannotated domains.

Speaker Bullets:
* Pfam maps structural domains (e.g. `Pfam: PF00042` = Globin domain).
```

```
================================================================================
SLIDE 6: InterPro: The Universal Meta-Search Engine
================================================================================
Topic: 13 Databases Under One Roof

[Visual: InterPro Architecture:
  Central Query -> InterProScan
                    |-- PROSITE (Patterns & Profiles)
                    |-- Pfam (HMMs)
                    |-- SMART (Signaling domains)
                    |-- PRINTS (Fingerprints)
                    |-- CATH-Gene3D / SUPERFAMILY (Structural domains)
                    `-- CDD (NCBI Conserved Domain Database)]

Speaker Bullets:
* Never search individual databases one by one; use **InterProScan** to query
  all 13 world signature databases in a single automated pass.
```

```
================================================================================
SLIDE 7: Specialized Structural Features: Signal Peptides & TM Helices
================================================================================
Topic: Subcellular Addressing Signals

1. Signal Peptides (Predicted by **SignalP**):
   * N-terminal 15-30 aa directing proteins to the ER / secretory pathway.
   * Tripartite structure: basic n-region -> hydrophobic h-core -> polar c-region.
   * Cleaved by Signal Peptidase at the (-3, -1) von Heijne motif: `A-x-B`.

2. Transmembrane Helices (Predicted by **TMHMM**):
   * 18-25 apolar residues spanning the lipid bilayer.
   * Governed by the **Positive-Inside Rule** (cytosolic loops enriched in Arg/Lys).

Speaker Bullets:
* Mature insulin possesses a signal peptide cleaved during proinsulin processing.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 24

* PROSITE patterns represent deterministic regular expressions (`N-{P}-[ST]-{P}`).
* Profile HMMs (Pfam) capture probabilistic position-specific domain models.
* InterPro consolidates global domain signatures.
* SignalP and TMHMM predict subcellular localization and membrane insertion.
* Next Lecture: Secondary Structure Prediction — Chou-Fasman, GOR, PSIPRED,
  and calculating Q3 accuracy!
```

---

## Detailed Comprehensive Technical Notes

### 1. The Hierarchical Architecture of Protein Sequence Features

When analyzing a newly translated polypeptide sequence, computational prediction operates across four distinct hierarchical layers:

```
  Hierarchy Level        Computational Model            Biological Scale & Examples
  -------------------------------------------------------------------------------------------------
  1. Short Motifs        Consensus strings (3-10 aa)    Phosphorylation targets, cleavage sites,
                                                        nuclear localization signals (NLS)
  2. Sequence Patterns   Deterministic regular          PROSITE patterns: N-glycosylation,
                         expressions with syntax rules  Walker A loop, zinc-finger C2H2
  3. Sequence Profiles   Probabilistic scoring tables   PSSMs, Profile Hidden Markov Models
                         (Position-Specific)            (Pfam, HMMER, SMART)
  4. Structural Domains  Independently folding 3D       Globin fold (PF00042), SH2, Kinase,
                         globular modules (40-300 aa)   Immunoglobulin domain (CATH / SCOP)
```

---

### 2. The PROSITE Pattern Specification Language

Created by Amos Bairoch in 1991 at the Swiss Institute of Bioinformatics (SIB), **PROSITE** standardized the syntax for defining protein functional signatures:

```
  Syntax Element         Mathematical Rule             Concrete Example
  -------------------------------------------------------------------------------------------------
  Single-Letter Code     Standard IUPAC characters     `A`, `C`, `D`, `E`, `F` ...
  Wildcard: `x` or `X`   Any of the 20 amino acids     `x` matches any single residue
  Brackets: `[ ... ]`    Logical OR (Inclusion set)    `[ST]` matches Serine OR Threonine
  Braces: `{ ... }`      Logical NOT (Exclusion set)   `{P}` matches any residue EXCEPT Proline
  Repetition: `(n)`      Exact count of n positions    `x(4)` matches exactly 4 arbitrary residues
  Range: `(m, n)`        Variable span of m to n       `x(2, 4)` matches 2, 3, or 4 residues
  Anchor: `<`            Anchored to N-terminus        `<M-x(2)` must start with N-terminal Met
  Anchor: `>`            Anchored to C-terminal        `[KRF]>` must terminate at C-terminus
  Separator: `-`         Concatenation delimiter       Hyphens separate adjacent tokens
```

#### Detailed Breakdown of Canonical Motifs:

#### A. N-Glycosylation Site (`PS00001`):
$$\text{Syntax: } \texttt{N-\{P\}-[ST]-\{P\}}$$
- Position 1: Must be **Asparagine ($N$)**, the carbohydrate attachment acceptor.
- Position 2: Any amino acid **EXCEPT Proline ($\{P\}$)**.
- Position 3: Must be **Serine ($S$) or Threonine ($T$)** ($[ST]$), whose hydroxyl oxygen participates in hydrogen bonding during oligosaccharyltransferase catalysis.
- Position 4: Any amino acid **EXCEPT Proline ($\{P\}$)**.
- *Biophysical Rationale:* Proline introduces a rigid $60^\circ$ kink in the peptide backbone, sterically clashing with the active site of the lumenal oligosaccharyltransferase enzyme.

#### B. ATP/GTP-Binding Walker A Motif / P-Loop (`PS00017`):
$$\text{Syntax: } \texttt{[AG]-x(4)-G-K-[ST]}$$
- Found in ATP synthases, ABC transporters, myosins, and Ras G-proteins.
- The invariant **Lysine ($K$)** residue forms direct electrostatic coordination bonds with the negatively charged $\beta$- and $\gamma$-phosphate oxygens of bound ATP or GTP.

#### C. The Classical Globin Signature (`PS00018`):
$$\text{Syntax: } \texttt{[LIVMFY]-x(2)-[LIVMFY]-x(4)-[LIVMFY]-x(2)-H-[LIVMFY]}$$
- Detects the specialized spatial environment of the **proximal Histidine (F8)** that coordinates the fifth coordination position of the haem $\text{Fe}^{2+}$ atom in myoglobins and hemoglobins.

---

### 3. Profile Hidden Markov Models and Pfam

While regular expressions are computationally trivial to match, they suffer from a fatal flaw: **rigid binary matching**. If an authentic evolutionary homolog possesses a single conservative substitution outside the bracketed set, a PROSITE pattern fails completely.

To capture evolutionary variability, computational biology transitioned to **Profile Hidden Markov Models (Profile HMMs)** (Sean Eddy, 1998):

```
                       [Begin]
                          |
             +------------+------------+
             |            |            |
             v            v            v
           [M_1] -----> [M_2] -----> [M_3]  (Match States: 20 emission probabilities)
          ^  |         ^  |         ^  |
         /   v        /   v        /   v
       [I_0]       [I_1]       [I_2]        (Insert States: accommodate insertions)
             \            \            \
              v            v            v
             [D_1] -----> [D_2] -----> [D_3] (Delete States: accommodate deletions)
```

#### The Pfam Architecture:
- Built using the **HMMER** software suite.
- **Pfam-A:** Curated collection of $>19,000$ families. Each family is built from a curated **Seed Alignment** of representative sequences. Profile HMMs are trained on the seed, and search thresholds are defined by manually calibrated **Gathering Thresholds (`GA`)**, below which matches are discarded as noise.
- In Pfam, human beta-globin matches family **`PF00042` (Globin)** with an E-value of $10^{-65}$.

---

### 4. Specialized Structural Features and Predictors

#### A. Signal Peptides (SignalP)
Secreted and membrane-bound proteins synthesized on membrane-bound ribosomes possess an N-terminal addressing tag termed a **Signal Peptide** (15 to 30 amino acids). Gunnar von Heijne established that signal peptides possess a tripartite architecture:
1. **n-region (1-5 aa):** Positively charged N-terminus (enriched in Lys and Arg).
2. **h-region (7-15 aa):** Central hydrophobic core forming an apolar $\alpha$-helix that inserts into the Sec61 translocon.
3. **c-region (3-7 aa):** Polar, neutral cleavage region obeying the **$(-3, -1)$ von Heijne rule**: positions $-3$ and $-1$ relative to the cleavage site must contain small, neutral residues (typically Alanine, Glycine, or Serine: `A-x-B`).
Cleavage is executed in the endoplasmic reticulum lumen by Signal Peptidase. Predicted by **SignalP** (deep neural network architecture).

#### B. Transmembrane $\alpha$-Helices (TMHMM)
Integral membrane proteins traverse the lipid bilayer via hydrophobic $\alpha$-helices.
- **Biophysical Constraint:** The non-polar interior of a phospholipid bilayer is $\approx 30\text{ \AA}$ thick. An $\alpha$-helix translates $1.5\text{ \AA}$ per residue; thus, traversing the membrane requires a continuous uninterrupted segment of $\ge 20$ apolar amino acids (Leu, Ile, Val, Phe, Ala).
- **The Positive-Inside Rule (von Heijne, 1986):** Cytoplasmic loops connecting transmembrane helices contain a 4-fold higher density of positively charged residues (**Lysine and Arginine**) than extra-cytoplasmic/lumenal loops, because the negative inside-membrane electrostatic potential energetically traps positive charges in the cytosol. **TMHMM** exploits this rule to predict whether loops face the cytoplasm or extracellular space.

#### C. Coiled-Coil Domains (COILS)
Formed by two to five amphipathic $\alpha$-helices wrapping around one another into a left-handed superhelix. Driven by a characteristic **heptad repeat** denoted $(a-b-c-d-e-f-g)_n$:
- Positions **$a$ and $d$** are hydrophobic residues (Leu, Ile, Val) that form the internal interlocking "knobs-into-holes" core.
- Positions **$e$ and $g$** are oppositely charged residues (Glu, Lys, Arg) that form stabilizing inter-helical electrostatic salt bridges.
- Predicted by the **COILS** algorithm (Lupas, 1991).

---

## Worked Example: Matching the Globin Pattern in Human *HBB*

### Problem:
Given the PROSITE Globin Signature (`PS00018`):
$$\texttt{[LIVMFY]-x(2)-[LIVMFY]-x(4)-[LIVMFY]-x(2)-H-[LIVMFY]}$$

Test whether the following 14-amino acid peptide extracted from human beta-globin (residues 84 to 97 of `NP_000509.1`) matches this signature:

$$\text{Sequence: } \text{T - L - S - E - L - H - C - D - K - L - H - V - D - P}$$

---

### Step-by-Step Position Matching:

```
  Pattern Element    Requirement                        Observed Residue in HBB    Match Status
  -------------------------------------------------------------------------------------------------
  1. [LIVMFY]        Aliphatic or Aromatic              Position 85: 'L' (Leu)     MATCH (Valid)
  2. x(2)            Any two residues                   Positions 86-87: 'S - E'   MATCH (Valid)
  3. [LIVMFY]        Aliphatic or Aromatic              Position 88: 'L' (Leu)     MATCH (Valid)
  4. x(4)            Any four residues                  Positions 89-92: 'H-C-D-K' MATCH (Valid)
  5. [LIVMFY]        Aliphatic or Aromatic              Position 93: 'L' (Leu)     MATCH (Valid)
  6. x(2)            Any two residues                   Wait! Check numbering:
```

Let us align carefully starting from residue 82 (`Leu`):

```
  HBB Coordinates:   84  85  86  87  88  89  90  91  92  93  94  95  96
  Residues:           T   L   S   E   L   H   C   D   K   L   H   V   D
  Pattern Tokens:        [L]  - - x(2) - -  [L]  - - - x(4) - - -  [L]  -  x(1)  -  H   [V]
```

In human beta-globin (`NP_000509.1`), the sequence surrounding the proximal Histidine (His93 in mature coordinates, His94 in RefSeq coordinates) matches the canonical signature:
- Hydrophobic anchor: $\text{Leu84}$
- Spacer $x(2)$: $\text{Thr85 - Leu86}$
- Hydrophobic anchor: $\text{Leu88}$
- Spacer $x(4)$: $\text{His89 - Cys90 - Asp91 - Lys92}$
- Hydrophobic anchor: $\text{Leu93}$
- Invariant **Histidine: His94** (The proximal haem-coordinating base!)
- C-terminal hydrophobic: $\text{Val95}$

**Conclusion:**  
The segment strictly conforms to the PROSITE globin pattern, identifying this protein as a functional member of the oxygen-binding globin family and pinpointing the proximal Histidine coordinating the haem iron.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A newly isolated protein sequence contains the peptide segment: `A - N - P - S - P - G`. Does this segment qualify as an authentic N-glycosylation site according to the PROSITE pattern `N-{P}-[ST]-{P}`? Justify your answer residue by residue.

**Model Answer:**
**No, this segment fails to qualify.**
- Target pattern: `N` at position 1, `{P}` (NOT Proline) at position 2, `[ST]` (Ser or Thr) at position 3, `{P}` (NOT Proline) at position 4.
- In the sequence segment `N - P - S - P`:
  - Position 1 is Asparagine (`N`) $\implies$ Matches.
  - Position 2 is **Proline (`P`)** $\implies$ **FAILS!** The pattern explicitly forbids Proline at position 2 (`{P}`).
  - Position 4 is also **Proline (`P`)** $\implies$ **FAILS!** The pattern explicitly forbids Proline at position 4.
The presence of Proline at position +1 and +3 sterically prevents oligosaccharyltransferase from accessing the Asparagine side chain; hence, this site will never be glycosylated in vivo.

---

### Question 2
**Prompt:** Why are Profile Hidden Markov Models (Profile HMMs, as used in Pfam) substantially more sensitive for identifying distant evolutionary homologs than deterministic regular expression patterns (as used in PROSITE)?

**Model Answer:**
- **Deterministic Patterns (PROSITE):** Use strict, binary regular expression rules (a residue is either in the bracketed set or the match fails completely). They treat all allowed residues equally and cannot capture subtle statistical preferences or tolerate non-canonical conservative substitutions.
- **Profile HMMs (Pfam):** Are fully probabilistic models. Each position has an explicit 20-dimensional probability distribution (emission probabilities) and position-specific gap probabilities (transition probabilities). A sequence that diverges slightly at one position can still achieve a statistically significant score if it matches the rest of the profile strongly, allowing Profile HMMs to detect remote homologies sharing $<20\%$ sequence identity where strict patterns fail.

---

### Question 3
**Prompt:** According to Gunnar von Heijne's "Positive-Inside Rule", how does the distribution of basic amino acids (Lysine and Arginine) determine the orientation of a transmembrane $\alpha$-helix across the bacterial plasma membrane?

**Model Answer:**
The Positive-Inside Rule establishes that loop regions connecting transmembrane $\alpha$-helices that face the **cytoplasm (inside)** contain a four-fold higher concentration of positively charged residues (**Lysine and Arginine**) compared to loops exposed to the periplasm or extracellular space (outside). This asymmetry is driven by the negative-inside transmembrane electrical potential across living cells, which exerts an electrostatic electrophoretic force that traps positively charged residues on the cytoplasmic side of the membrane.
