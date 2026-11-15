# Lecture 13 — Scoring Matrices and Significance

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 5:** Sequence Alignment and Database Searching  
**Syllabus Topic:** Substitution Score and Gap Penalty, Statistical Significance of Alignment  
**Primary Learning Outcome:** LO3, LO4 — Calculate log-odds scores, select PAM/BLOSUM matrices, and calculate bit scores and E-values.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Beyond Binary Identity
================================================================================
Topic: Why Amino Acids Are Not Equal

[Visual: Substitution Spectrum:
  Conservative: Leucine <-> Isoleucine (Both branched aliphatic; minimal structural disruption)
  Radical:      Glutamate <-> Valine   (HbS Sickle Cell! Polar charged to hydrophobic)
  Identity match: Tryptophan <-> Tryptophan (Rare, massive indole ring: irreplaceable!)]

Speaker Bullets:
* DNA uses a 4-letter alphabet where transition/transversion matrices suffice.
* Proteins utilize a 20-letter alphabet with complex chemical, steric, and physical constraints.
* A scoring matrix must quantify the evolutionary probability of every possible pair (20 x 20 = 210 pairs).
```

```
================================================================================
SLIDE 2: The Log-Odds Formulation
================================================================================
Topic: Quantifying Biological Evidence over Random Chance

Formula:
  s(i, j) = (1 / lambda) * log_2 [ q_ij / (p_i * p_j) ]

  * q_ij: Target frequency (observed frequency of i aligned with j in authentic homologs)
  * p_i * p_j: Background frequency (probability of i and j aligning by pure random chance)

Interpretation:
  * s(i, j) > 0  --> Observed MORE often than random chance (Evolutionarily accepted)
  * s(i, j) = 0  --> Exactly equal to random expectation
  * s(i, j) < 0  --> Observed LESS often than random chance (Evolutionarily purged)

Speaker Bullets:
* Log-odds scores allow dynamic programming to add scores across columns rather
  than multiplying probabilities.
```

```
================================================================================
SLIDE 3: Dayhoff's PAM Matrices (1978)
================================================================================
Topic: Point Accepted Mutations and Evolutionary Models

[Visual: Extrapolation from PAM1:
  PAM1 (1% divergence) --(Markov Chain M^k)--> PAM250 (~80% sequence divergence)]

Speaker Bullets:
* Margaret Dayhoff analyzed 1,572 mutations across 71 closely related families (>85% identity).
* 1 PAM = 1 accepted point mutation per 100 amino acids.
* To model ancient evolutionary distances, Dayhoff multiplied the transition probability
  matrix by itself $k$ times: PAM250 = $(M_1)^{250}$.
* Note: Higher PAM numbers = greater evolutionary divergence.
```

```
================================================================================
SLIDE 4: The BLOSUM Matrices (Henikoff & Henikoff, 1992)
================================================================================
Topic: Blocks Substitution Matrices

[Visual: Ungapped Multiple Alignment Block -> Cluster sequences at threshold L%
         -> Count observed pairs directly from real ancient conserved blocks]

Key Thresholds:
  * BLOSUM62: Sequences sharing >= 62% identity are clustered. (Default workhorse!)
  * BLOSUM80: Clustered at 80% identity. (Best for closely related sequences)
  * BLOSUM45: Clustered at 45% identity. (Best for distant, ancient homologs)

Speaker Bullets:
* Derived from the BLOCKS database of real, ungapped conserved core structures.
* Inverted numbering relative to PAM: Lower BLOSUM number = greater evolutionary divergence!
```

```
================================================================================
SLIDE 5: PAM vs BLOSUM Matrix Selection Guide
================================================================================
Topic: Matching Matrix to Evolutionary Divergence

+-------------------------+--------------------+------------------------------+
| Evolutionary Target     | PAM Equivalent     | BLOSUM Equivalent            |
+-------------------------+--------------------+------------------------------+
| Closely related (>80% id| PAM30, PAM70       | **BLOSUM80**, BLOSUM90       |
| Medium divergence (60% id| PAM120            | **BLOSUM62** (Universal default)
| Distant homologs (<35% id| PAM250            | **BLOSUM45**                 |
+-------------------------+--------------------+------------------------------+

Speaker Bullets:
* If you search for human vs chimp HBB: use BLOSUM80.
* If you search for human HBB vs bacterial flavohemoglobin: switch to BLOSUM45!
```

```
================================================================================
SLIDE 6: Statistical Significance: The Gumbel Distribution (EVD)
================================================================================
Topic: Karlin-Altschul Statistics

[Visual: Comparison of Normal Bell Curve vs Skewed Gumbel Extreme Value Distribution
         EVD has a long right-hand tail describing maximal scores from random data]

  P(Score S >= x) = 1 - exp( - K * m * n * e^(-lambda * x) )

Speaker Bullets:
* When comparing random sequences, the distribution of the HIGHEST local score
  does not follow a normal bell curve; it follows the Gumbel Extreme Value Distribution.
* Samuel Karlin and Stephen Altschul derived the exact mathematical parameters
  (lambda and K) governing this tail.
```

```
================================================================================
SLIDE 7: Raw Score (S) vs Bit Score (S') vs E-Value
================================================================================
Topic: Decoupling Scores from Scoring System and Search Space

1. Raw Score (S): Dependent on arbitrary matrix units and gap penalties.
2. Bit Score (S'): Normalized score expressed in information-theoretic bits:
   S' = (lambda * S - ln K) / ln 2
   (Comparable across DIFFERENT matrices and databases!)
3. Expectation Value (E):
   E = m * n * 2^(-S')
   (Number of random hits with score >= S expected by chance in a database of size N = m * n)

Speaker Bullets:
* The E-value is the ultimate metric reported in BLAST.
* E < 10^-5: Statistically significant homology. E > 1: Pure random noise.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 13

* Substitution matrices represent log-odds likelihood ratios: q_ij / (p_i * p_j).
* BLOSUM62 is the global default; lower BLOSUM numbers target deeper evolutionary divergence.
* Local alignment scores follow the Gumbel Extreme Value Distribution.
* Bit score is database-independent; E-value scales linearly with database size!
* Next Lecture: Heuristic Alignment Algorithms — How FASTA and BLAST achieve
  1000x speedups over dynamic programming.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Biophysical Rationale of Scoring Matrices

In an alignment of nucleic acid sequences, four bases yield 16 possible pairwise alignments, which can be modeled with simple match/mismatch scores or transition/transversion weights ($2 \times 2$ symmetry). In proteins, 20 amino acids yield $20 \times 20 = 400$ possible pairings ($210$ unique pairs accounting for symmetry).

Empirical observation of protein evolution reveals that amino acid substitutions are governed by three biophysical constraints:
1. **Physicochemical Similarity:** Substitutions that preserve charge, hydrophobicity, steric volume, and hydrogen-bonding capacity (e.g., Aspartate $\leftrightarrow$ Glutamate, or Isoleucine $\leftrightarrow$ Leucine $\leftrightarrow$ Valine) are frequently accepted by natural selection.
2. **Genetic Code Architecture:** The standard genetic code is structured such that single-nucleotide transitions frequently yield chemically conservative substitutions.
3. **Structural and Catalytic Uniqueness:** Certain amino acids possess unique stereochemical properties that cannot be replaced without catastrophic structural failure:
   - **Tryptophan ($W$):** Largest aromatic residue; fits into rigid hydrophobic cores.
   - **Cysteine ($C$):** Forms covalent disulfide bonds ($-S-S-$) stabilizing extracellular folds.
   - **Proline ($P$):** Cyclic rigid imino acid that breaks $\alpha$-helices and forces sharp polypeptide turns.
   - **Glycine ($G$):** Possesses no side chain ($-H$); provides conformational flexibility in tight turns.

---

### 2. The Log-Odds Mathematical Formulation

Every modern amino acid scoring matrix is formalized as a **Log-Odds Matrix** (Dayhoff, 1978). Let:
- $q_{ij}$: The **target frequency**—the joint probability that amino acids $i$ and $j$ share a common ancestral origin in authentic homologous alignments.
- $p_i, p_j$: The **background frequencies**—the individual probabilities of encountering amino acids $i$ and $j$ in public protein databases by chance.

The likelihood ratio comparing the homology hypothesis ($H_1$) to the random chance hypothesis ($H_0$) is:

$$\text{Likelihood Ratio} = \frac{P(\text{Data} \mid H_1)}{P(\text{Data} \mid H_0)} = \frac{q_{ij}}{p_i p_j}$$

To make scores additive across independent alignment columns, we take the logarithm:

$$s(i, j) = \frac{1}{\lambda} \log_2 \left( \frac{q_{ij}}{p_i p_j} \right)$$

where $\lambda$ is a statistical scaling factor that scales the matrix values to integers (half-bits or third-bits) for computational efficiency.

```
  Log-Odds Score Sign      Biological Meaning
  -------------------------------------------------------------------------------------------------
  Positive: s(i, j) > 0     Pair occurs significantly MORE frequently than random expectation;
                            indicates evolutionary conservation or conservative substitution.
  Zero:     s(i, j) = 0     Pair occurs at EXACTLY random expectation; evolutionarily neutral.
  Negative: s(i, j) < 0     Pair occurs significantly LESS frequently than random expectation;
                            indicates deleterious substitution purged by purifying selection.
```

---

### 3. PAM vs BLOSUM: Contrasting Paradigms

```
  Property               Dayhoff PAM Matrices                   Henikoff BLOSUM Matrices
  -------------------------------------------------------------------------------------------------
  Full Name              Point Accepted Mutation                BLOcks SUbstitution Matrix
  Origin Year & Author   1978 (Margaret Dayhoff)                1992 (Steven & Jorja Henikoff)
  Training Dataset       71 closely related families            BLOCKS Database (~2,000 blocks
                         (>85% identity; 1,572 mutations)       of ungapped multiple alignments)
  Derivation Method      Observed PAM1 transition matrix,       Direct counting of observed pairs
                         extrapolated via Markov chains: M^k    from clustered blocks
  Evolutionary Target    Higher number = greater divergence     Lower number = greater divergence
                         (PAM250 is distant; PAM30 is close)    (BLOSUM45 is distant; BLOSUM80 is close)
  Default Workhorse      PAM250 (historically)                  **BLOSUM62** (universally accepted)
```

#### Why Tryptophan Has a High Diagonal Score:
In BLOSUM62, an identity match for Tryptophan ($W-W$) scores **$+11$**, whereas an identity match for Leucine ($L-L$) scores only **$+4$**. 
- Leucine is abundant ($p_L \approx 9.6\%$ of all residues). Random alignments produce $L-L$ pairings frequently ($p_L \cdot p_L \approx 0.0092$).
- Tryptophan is the rarest amino acid ($p_W \approx 1.1\%$). The probability of two random proteins aligning a Tryptophan by chance is $p_W \cdot p_W \approx 0.00012$.
- When a $W-W$ alignment is observed, the likelihood ratio $\frac{q_{WW}}{p_W p_W}$ is astronomical, providing massive evidence of homology.

---

### 4. Statistical Significance: Karlin-Altschul Statistics

When a bioinformatician searches a database of 100 million residues, how do we distinguish whether a score of $S = 45$ represents genuine evolutionary kinship or merely the best random match among millions of candidates?

Samuel Karlin and Stephen Altschul (1990) proved that under the conditions of local alignment (independent letters, negative average score), the distribution of the maximal local score $S$ follows a **Gumbel Extreme Value Distribution (Type I EVD)**:

$$P(S \ge x) = 1 - \exp\left( -K \cdot m \cdot n \cdot e^{-\lambda x} \right)$$

where:
- $m$: Length of the query sequence.
- $n$: Length of the database (total residues).
- $K$: A natural scaling constant reflecting the search space entropy and scoring matrix background.
- $\lambda$: The unique positive root of the Karlin-Altschul equation: $\sum_{i,j} p_i p_j e^{\lambda s(i,j)} = 1$.

#### Normalized Bit Score ($S'$):
Because raw score $S$ depends on the arbitrary scaling factor $\lambda$ of the scoring matrix, Altschul normalized the score into **bits**:

$$S' = \frac{\lambda S - \ln K}{\ln 2}$$

The Bit Score is matrix-independent: a bit score of 50 bits obtained using BLOSUM62 represents the exact same statistical significance as 50 bits obtained using PAM250.

#### The Expectation Value ($E$):
The **E-value** is the expected number of false-positive alignments with a score $\ge S$ that would occur purely by chance when searching a random database of size $N = m \cdot n$:

$$E = K \cdot m \cdot n \cdot e^{-\lambda S} = m \cdot n \cdot 2^{-S'}$$

```
  E-Value Threshold Range    Biological Interpretation
  -------------------------------------------------------------------------------------------------
  E < 10^-50                 Virtually identical sequences; absolute biological certainty
  10^-50 <= E < 10^-10       Extremely strong homology (e.g. human HBB vs mouse Hbb)
  10^-10 <= E < 10^-4        Statistically significant homology; reliable domain kinship
  10^-4 <= E < 10^-1         The "Twilight Zone": potential distant homology or random match;
                             requires structural validation or secondary structure support
  E >= 1                     Pure random noise; expected to occur by chance in any search
```

---

## Worked Mathematical Example: Calculating Bit Score and E-Value

### Problem:
A researcher queries the human beta-globin protein sequence ($m = 147$ amino acids) using BLASTP against a non-redundant database of $n = 1.0 \times 10^8$ amino acids.  
The search identifies an alignment with a raw score of **$S = 75$**.  
The Karlin-Altschul scoring parameters for BLOSUM62 with gap penalties (11, 1) are:
- $\lambda = 0.267$
- $K = 0.041$

Calculate:
1. The normalized **Bit Score ($S'$)**.
2. The **Expectation Value ($E$)**.
3. Determine whether this hit represents statistically significant homology.

---

### Step 1: Calculate the Bit Score ($S'$)

Using the bit score formula:
$$S' = \frac{\lambda S - \ln K}{\ln 2}$$

First, compute the components:
$$\lambda \cdot S = 0.267 \times 75 = 20.025$$
$$\ln K = \ln(0.041) \approx -3.1942$$
$$\ln 2 \approx 0.69315$$

Substitute into the equation:
$$S' = \frac{20.025 - (-3.1942)}{0.69315} = \frac{20.025 + 3.1942}{0.69315} = \frac{23.2192}{0.69315} \approx \mathbf{33.50\text{ bits}}$$

---

### Step 2: Calculate the Expectation Value ($E$)

Using the E-value formula:
$$E = K \cdot m \cdot n \cdot e^{-\lambda S}$$

Compute the search space ($m \cdot n$):
$$m \cdot n = 147 \times 1.0 \times 10^8 = 1.47 \times 10^{10}$$

Compute the exponential decay term:
$$e^{-\lambda S} = e^{-20.025} \approx 2.010 \times 10^{-9}$$

Multiply all terms:
$$E = 0.041 \times (1.47 \times 10^{10}) \times (2.010 \times 10^{-9})$$
$$E = 0.041 \times 29.547 \approx \mathbf{1.21}$$

---

### Step 3: Biological Interpretation
- The raw score of 75 yields an **E-value of 1.21**.
- An E-value of $1.21$ means that in a database of this size, **we expect to find approximately 1.21 alignments with this score purely by random chance**.
- **Conclusion:** This hit is **NOT statistically significant**; it falls into the realm of background noise and cannot be claimed as an authentic homolog.

*(Note: To achieve significant homology with $E \le 10^{-5}$ in this database, the Bit Score would need to exceed $\approx 51\text{ bits}$, corresponding to a raw score of $S \ge 120$).*

---

## Formative In-Class Checks

### Question 1
**Prompt:** A student uses BLASTP to search for homologs of a novel kinase against the Swiss-Prot database ($n \approx 1.8 \times 10^8$ aa) and obtains an alignment with an E-value of $0.002$. The next day, the student re-runs the exact same query with the same scoring parameters against the much larger NCBI non-redundant (`nr`) database ($n \approx 5.0 \times 10^{10}$ aa).  
1. Will the raw score $S$ change?  
2. Will the Bit score $S'$ change?  
3. What will happen to the E-value?

**Model Answer:**
1. **Raw Score ($S$):** Will **NOT change**. The raw score depends solely on the pairwise alignment of the query against that specific hit sequence.
2. **Bit Score ($S'$):** Will **NOT change**. The bit score is normalized using $\lambda$ and $K$, remaining strictly independent of database size.
3. **E-Value:** The E-value will **increase dramatically** (become much worse/less significant). Because $E = m \cdot n \cdot 2^{-S'}$, the E-value scales linearly with database size $n$. Searching a database that is $\approx 277$ times larger will increase the E-value from $0.002$ to $\approx 0.55$, rendering the match statistically insignificant.

---

### Question 2
**Prompt:** Explain why the default matrix in NCBI BLASTP is BLOSUM62 rather than BLOSUM45 or BLOSUM80. Under what specific biological research scenario should a researcher manually switch the matrix to BLOSUM45?

**Model Answer:**
- **Why BLOSUM62 is default:** Extensive empirical benchmarking by Henikoff & Henikoff demonstrated that BLOSUM62 provides the best overall balance of sensitivity and selectivity across medium evolutionary distances (detecting sequences sharing between 30% and 70% identity), making it the optimal general-purpose workhorse.
- **When to switch to BLOSUM45:** A researcher should manually switch to **BLOSUM45** when searching for **ancient, highly diverged homologs** (such as identifying evolutionary homologs between mammalian beta-globin and bacterial or fungal flavohemoglobins sharing $<30\%$ sequence identity), where conservative substitutions accumulated over billions of years need to be recognized.

---

### Question 3
**Prompt:** Why do extreme value scores of local sequence alignments follow the Gumbel Extreme Value Distribution (EVD) rather than a Gaussian (normal) distribution?

**Model Answer:**
When searching a biological database, software does not report the *average* score of all random alignments; it reports the **maximum score** among millions of independent pairwise comparisons. By the Fisher-Tippett-Gnedenko theorem of extreme value theory, the maximum of a large collection of independent and identically distributed random variables does not converge to a Gaussian normal bell curve, but converges to an **Extreme Value Distribution (Gumbel distribution)**, which is fundamentally asymmetric with a characteristic heavy right-hand tail.
