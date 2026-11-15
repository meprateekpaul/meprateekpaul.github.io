---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 24 Slides: Motifs, Patterns, and Domains"
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
# Lecture 24 — Motifs, Patterns, and Domains
### Concepts of Bioinformatics (CBBI-501)
**Unit 09:** Predictive Methods using Protein Sequence  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Modular Hierarchy of Proteins

```text
Topic: Deciphering the Grammar of Polypeptides

[Visual: Conceptual Hierarchy:
  1. Primary Sequence: Raw amino acid tape (N-...-C)
  2. Motifs / Patterns: Short functional signatures (3 to 20 aa; e.g. Walker loop)
  3. Profiles / HMMs: Position-specific probabilistic models
  4. Structural Domains: Independently folding, compact globular units (50 to 300 aa)
  5. Multidomain Architectures: Complete physiological machines]
```

**Speaker Talking Points:**  
* Proteins are not monolithic polymers; they are modular constructions.
* Identifying conserved motifs and domains allows bioinformaticians to assign
  biological function to uncharacterized sequences even in the absence of full homology.

---

## Slide 2: PROSITE Pattern Syntax

```text
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
```

**Speaker Talking Points:**  
* PROSITE patterns are deterministic: a sequence either matches 100%, or it fails.

---

## Slide 3: Classic Signatures in Molecular Biology

```text
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
```

**Speaker Talking Points:**  
* A single consensus pattern can identify an enzymatic mechanism instantly.

---

## Slide 4: The Limitations of Strict Patterns

```text
Topic: Why Regular Expressions Break Down

[Visual: The "All-or-Nothing" Dilemma:
  Homolog 1: [A] - x(4) - G - K - [S]  --> MATCH (Score: YES)
  Homolog 2: [A] - x(4) - G - K - [T]  --> MATCH (Score: YES)
  Homolog 3: [A] - x(4) - G - R - [S]  --> (Lys mutates to Arg: structurally fine!)
             FAILS PATTERN ENTIRELY! (Score: NO)]
```

**Speaker Talking Points:**  
* Biology is probabilistic, not deterministic.
* A single conservative substitution can break a rigid PROSITE pattern.
* Solution: **Profile Hidden Markov Models (HMMs)** that score probabilities!

---

## Slide 5: Profile HMMs and the Pfam Database

```text
Topic: Sean Eddy's HMMER Architecture

[Visual: Plan7 Profile HMM Architecture:
  Match States (M_1, M_2, M_3) with amino acid emission probabilities
  Insert States (I_1, I_2) and Delete States (D_1, D_2) with transition probabilities]

The Pfam Database:
* **Pfam-A:** Curated collection of ~20,000 protein domain families based on
  manually reviewed "seed alignments" and strict Gathering Thresholds (`GA`).
* **Pfam-B:** Automated clusters of unannotated domains.
```

**Speaker Talking Points:**  
* Pfam maps structural domains (e.g. `Pfam: PF00042` = Globin domain).

---

## Slide 6: InterPro: The Universal Meta-Search Engine

```text
Topic: 13 Databases Under One Roof

[Visual: InterPro Architecture:
  Central Query -> InterProScan
                    |-- PROSITE (Patterns & Profiles)
                    |-- Pfam (HMMs)
                    |-- SMART (Signaling domains)
                    |-- PRINTS (Fingerprints)
                    |-- CATH-Gene3D / SUPERFAMILY (Structural domains)
                    `-- CDD (NCBI Conserved Domain Database)]
```

**Speaker Talking Points:**  
* Never search individual databases one by one; use **InterProScan** to query
  all 13 world signature databases in a single automated pass.

---

## Slide 7: Specialized Structural Features: Signal Peptides & TM Helices

```text
Topic: Subcellular Addressing Signals

1. Signal Peptides (Predicted by **SignalP**):
   * N-terminal 15-30 aa directing proteins to the ER / secretory pathway.
   * Tripartite structure: basic n-region -> hydrophobic h-core -> polar c-region.
   * Cleaved by Signal Peptidase at the (-3, -1) von Heijne motif: `A-x-B`.

2. Transmembrane Helices (Predicted by **TMHMM**):
   * 18-25 apolar residues spanning the lipid bilayer.
   * Governed by the **Positive-Inside Rule** (cytosolic loops enriched in Arg/Lys).
```

**Speaker Talking Points:**  
* Mature insulin possesses a signal peptide cleaved during proinsulin processing.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 24

* PROSITE patterns represent deterministic regular expressions (`N-{P}-[ST]-{P}`).
* Profile HMMs (Pfam) capture probabilistic position-specific domain models.
* InterPro consolidates global domain signatures.
* SignalP and TMHMM predict subcellular localization and membrane insertion.
* Next Lecture: Secondary Structure Prediction — Chou-Fasman, GOR, PSIPRED,
  and calculating Q3 accuracy!
```

