---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 23 Slides: Physicochemical Properties"
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
# Lecture 23 — Physicochemical Properties
### Concepts of Bioinformatics (CBBI-501)
**Unit 09:** Predictive Methods using Protein Sequence  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: From 1D Sequence to Physical Chemistry

```text
Topic: Macroscopic Biophysics from Microscopic Letters

[Visual: A 1D string of letters: N-MVHLTPEEKSAVTALWGKV...-C
         Transforming into:
         * Molecular Weight: 15,998 Da
         * Isoelectric Point (pI): 6.87
         * Extinction Coeff (280nm): 14,080 M^-1 cm^-1
         * Kyte-Doolittle Hydropathy Profile Curve]
```

**Speaker Talking Points:**  
* Before a biochemist purifies a recombinant protein in the lab, they compute its
  physical properties from sequence alone.
* Knowing the molecular weight, net charge, and solubility guides chromatography column
  selection, buffer design, and crystallisation conditions.
* Primary bioinformatics tool: **Expasy ProtParam**.

---

## Slide 2: Molecular Weight Computation

```text
Topic: Accounting for Condensation Chemistry

Formula:
  M_r(Protein) = [ Sum_{i=1}^N M_r(Amino Acid_i) ] - [ (N - 1) * 18.015 Da ]

  * Each peptide bond formation releases one molecule of water (H2O = 18.015 Da).
  * Monoisotopic Mass (Exact mass of most abundant isotope: 12C, 1H, 14N, 16O).
  * Average Mass (Weighted by natural isotopic abundance across elements).
```

**Speaker Talking Points:**  
* For human beta-globin (147 aa): Average mass = 15,998 Da (~16 kDa).
* Mass spectrometry measures mass with sub-dalton precision to confirm intact chains.

---

## Slide 3: The Theoretical Isoelectric Point (pI)

```text
Topic: Where Net Charge Equals Zero

  Definition:
  The isoelectric point (pI) is the exact pH at which the net electrical charge
  of the protein molecule is exactly ZERO: Q(pH) = 0.

[Visual: Net Charge Curve Q(pH) vs pH:
  At pH < pI: Net Charge is POSITIVE (+) --> Binds Cation Exchanger
  At pH = pI: Net Charge is ZERO (0)    --> Protein precipitates / least soluble!
  At pH > pI: Net Charge is NEGATIVE (-) --> Binds Anion Exchanger]
```

**Speaker Talking Points:**  
* At its pI, a protein has no electrostatic repulsion and often aggregates.

---

## Slide 4: The 7 Ionizable Amino Acid Groups

```text
Topic: Henderson-Hasselbalch Dissociation Constants

+--------------------+--------------------+--------------------+--------------+
| Ionizable Group    | Residue Class      | Average pKa (Bjellqvist) | State at pH 7|
+--------------------+--------------------+--------------------+--------------+
| C-Terminal Carboxyl| Terminal alpha-COOH| 3.6                | Deprotonated (-1)
| Aspartate (Asp, D) | Beta-Carboxyl      | 3.9                | Deprotonated (-1)
| Glutamate (Glu, E) | Gamma-Carboxyl     | 4.1                | Deprotonated (-1)
| Histidine (His, H) | Imidazole ring     | 6.0 - 6.5          | Neutral / +0.1
| N-Terminal Amino   | Terminal alpha-NH3+| 8.6                | Protonated (+1)
| Cysteine (Cys, C)  | Thiol (-SH)        | 8.5                | Neutral (0)
| Tyrosine (Tyr, Y)  | Phenolic -OH       | 10.1               | Neutral (0)
| Lysine (Lys, K)    | Epsilon-NH3+       | 10.5               | Protonated (+1)
| Arginine (Arg, R)  | Guanidinium        | 12.5               | Protonated (+1)
+--------------------+--------------------+--------------------+--------------+
```

**Speaker Talking Points:**  
* The net charge is the algebraic sum of all positive and negative groups.
* The algorithm uses the **Bisection Method** to iterate across pH [0..14] to find Q = 0.

---

## Slide 5: The Sickle Cell Shift: Charge Alteration

```text
Topic: Glu6Val Alters the Isoelectric Point

  Wild-Type Beta-Globin (HbA):
    Position 6: Glutamic Acid (Glu, E) --> Negative Charge (-1 at pH 7)
    Theoretical pI: **6.87**

  Sickle-Cell Variant (HbS):
    Position 6: Valine (Val, V)        --> Neutral Hydrophobic (0 charge)
    Theoretical pI: **7.10**
```

**Speaker Talking Points:**  
* Replacing one carboxyl group eliminates a negative charge, shifting the pI upwards!
* In 1949, Linus Pauling used moving-boundary electrophoresis at pH 8.6 to separate
  HbS from HbA, inaugurating the era of **Molecular Medicine**.

---

## Slide 6: Molar Extinction Coefficient (Epsilon_280)

```text
Topic: Quantifying Protein Concentration by UV Light

  Beer-Lambert Law: A = Epsilon * c * l

  Pace & Edelhoch Method (at 280 nm in 6M Guanidine-HCl):
    Epsilon_280 = (Count(Trp) * 5,500) + (Count(Tyr) * 1,490) + (Count(Cystine) * 125)
```

**Speaker Talking Points:**  
* Tryptophan and Tyrosine are the primary chromophores absorbing at 280 nm.
* Knowing $\epsilon_{280}$ allows you to calculate exact protein concentration in a spectrophotometer!

---

## Slide 7: In Vitro Stability and Hydropathy Profiling

```text
Topic: Guruprasad's Instability Index & Kyte-Doolittle

1. Guruprasad Instability Index (II):
   * Statistical weightings of dipeptide combinations:
     - II < 40  --> Predicted STABLE in test tube.
     - II > 40  --> Predicted UNSTABLE (half-life < 5 hours in vitro).
   * Human HBB: II ≈ 33.6 (Stable!).

2. Hydropathy Profiling (Kyte & Doolittle, 1982):
   * Assigns numerical hydropathy scores: Isoleucine (+4.5) to Arginine (-4.5).
   * Sliding window 9: Maps hydrophobic core vs surface-exposed loops.
   * Sliding window 19-21: Identifies 20-residue Transmembrane Helices!
```

**Speaker Talking Points:**  
* Hydropathy peaks spanning >+1.6 over 20 residues reliably predict membrane anchors.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 23

* Primary sequence determines mass, net charge, extinction, and stability.
* Theoretical pI is solved via bisection of the Henderson-Hasselbalch equation.
* Sickle-cell HbS (Glu6Val) increases pI from 6.87 to 7.10 via loss of an acid group.
* Extinction coefficient $\epsilon_{280}$ derives from Trp, Tyr, and Cystine counts.
* Kyte-Doolittle hydropathy plots identify transmembrane domains and surface loops.
* Next Lecture: Motifs, Patterns (PROSITE syntax), Pfam Domains, and InterPro.
```

