---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 13 Slides: Scoring Matrices and Significance"
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
# Lecture 13 — Scoring Matrices and Significance
### Concepts of Bioinformatics (CBBI-501)
**Unit 05:** Sequence Alignment and Database Searching  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Beyond Binary Identity

```text
Topic: Why Amino Acids Are Not Equal

[Visual: Substitution Spectrum:
  Conservative: Leucine <-> Isoleucine (Both branched aliphatic; minimal structural disruption)
  Radical:      Glutamate <-> Valine   (HbS Sickle Cell! Polar charged to hydrophobic)
  Identity match: Tryptophan <-> Tryptophan (Rare, massive indole ring: irreplaceable!)]
```

**Speaker Talking Points:**  
* DNA uses a 4-letter alphabet where transition/transversion matrices suffice.
* Proteins utilize a 20-letter alphabet with complex chemical, steric, and physical constraints.
* A scoring matrix must quantify the evolutionary probability of every possible pair (20 x 20 = 210 pairs).

---

## Slide 2: The Log-Odds Formulation

```text
Topic: Quantifying Biological Evidence over Random Chance

Formula:
  s(i, j) = (1 / lambda) * log_2 [ q_ij / (p_i * p_j) ]

  * q_ij: Target frequency (observed frequency of i aligned with j in authentic homologs)
  * p_i * p_j: Background frequency (probability of i and j aligning by pure random chance)

Interpretation:
  * s(i, j) > 0  --> Observed MORE often than random chance (Evolutionarily accepted)
  * s(i, j) = 0  --> Exactly equal to random expectation
  * s(i, j) < 0  --> Observed LESS often than random chance (Evolutionarily purged)
```

**Speaker Talking Points:**  
* Log-odds scores allow dynamic programming to add scores across columns rather
  than multiplying probabilities.

---

## Slide 3: Dayhoff's PAM Matrices (1978)

```text
Topic: Point Accepted Mutations and Evolutionary Models

[Visual: Extrapolation from PAM1:
  PAM1 (1% divergence) --(Markov Chain M^k)--> PAM250 (~80% sequence divergence)]
```

**Speaker Talking Points:**  
* Margaret Dayhoff analyzed 1,572 mutations across 71 closely related families (>85% identity).
* 1 PAM = 1 accepted point mutation per 100 amino acids.
* To model ancient evolutionary distances, Dayhoff multiplied the transition probability
  matrix by itself $k$ times: PAM250 = $(M_1)^{250}$.
* Note: Higher PAM numbers = greater evolutionary divergence.

---

## Slide 4: The BLOSUM Matrices (Henikoff & Henikoff, 1992)

```text
Topic: Blocks Substitution Matrices

[Visual: Ungapped Multiple Alignment Block -> Cluster sequences at threshold L%
         -> Count observed pairs directly from real ancient conserved blocks]

Key Thresholds:
  * BLOSUM62: Sequences sharing >= 62% identity are clustered. (Default workhorse!)
  * BLOSUM80: Clustered at 80% identity. (Best for closely related sequences)
  * BLOSUM45: Clustered at 45% identity. (Best for distant, ancient homologs)
```

**Speaker Talking Points:**  
* Derived from the BLOCKS database of real, ungapped conserved core structures.
* Inverted numbering relative to PAM: Lower BLOSUM number = greater evolutionary divergence!

---

## Slide 5: PAM vs BLOSUM Matrix Selection Guide

```text
Topic: Matching Matrix to Evolutionary Divergence

+-------------------------+--------------------+------------------------------+
| Evolutionary Target     | PAM Equivalent     | BLOSUM Equivalent            |
+-------------------------+--------------------+------------------------------+
| Closely related (>80% id| PAM30, PAM70       | **BLOSUM80**, BLOSUM90       |
| Medium divergence (60% id| PAM120            | **BLOSUM62** (Universal default)
| Distant homologs (<35% id| PAM250            | **BLOSUM45**                 |
+-------------------------+--------------------+------------------------------+
```

**Speaker Talking Points:**  
* If you search for human vs chimp HBB: use BLOSUM80.
* If you search for human HBB vs bacterial flavohemoglobin: switch to BLOSUM45!

---

## Slide 6: Statistical Significance: The Gumbel Distribution (EVD)

```text
Topic: Karlin-Altschul Statistics

[Visual: Comparison of Normal Bell Curve vs Skewed Gumbel Extreme Value Distribution
         EVD has a long right-hand tail describing maximal scores from random data]

  P(Score S >= x) = 1 - exp( - K * m * n * e^(-lambda * x) )
```

**Speaker Talking Points:**  
* When comparing random sequences, the distribution of the HIGHEST local score
  does not follow a normal bell curve; it follows the Gumbel Extreme Value Distribution.
* Samuel Karlin and Stephen Altschul derived the exact mathematical parameters
  (lambda and K) governing this tail.

---

## Slide 7: Raw Score (S) vs Bit Score (S') vs E-Value

```text
Topic: Decoupling Scores from Scoring System and Search Space

1. Raw Score (S): Dependent on arbitrary matrix units and gap penalties.
2. Bit Score (S'): Normalized score expressed in information-theoretic bits:
   S' = (lambda * S - ln K) / ln 2
   (Comparable across DIFFERENT matrices and databases!)
3. Expectation Value (E):
   E = m * n * 2^(-S')
   (Number of random hits with score >= S expected by chance in a database of size N = m * n)
```

**Speaker Talking Points:**  
* The E-value is the ultimate metric reported in BLAST.
* E < 10^-5: Statistically significant homology. E > 1: Pure random noise.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 13

* Substitution matrices represent log-odds likelihood ratios: q_ij / (p_i * p_j).
* BLOSUM62 is the global default; lower BLOSUM numbers target deeper evolutionary divergence.
* Local alignment scores follow the Gumbel Extreme Value Distribution.
* Bit score is database-independent; E-value scales linearly with database size!
* Next Lecture: Heuristic Alignment Algorithms — How FASTA and BLAST achieve
  1000x speedups over dynamic programming.
```

