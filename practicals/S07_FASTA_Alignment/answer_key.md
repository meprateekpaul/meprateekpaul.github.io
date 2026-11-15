# Instructor Answer Key & Evaluation Manual: Practical 07 (FASTA Alignment)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S07 (Syllabus Practical P9)  
**Curriculum Topic:** Sequence Alignment and Similarity Searching Using FASTA & SSEARCH  

---

## 1. Expected Outputs & Reference Solutions

### Table 7.1: FASTA Search Results for Human HBB (`NP_000509.1`) against UniProtKB/Swiss-Prot (Completed)
*(Values representative of FASTA36 run at EMBL-EBI with BLOSUM50, gap open -10, gap ext -2, $ktup=2$).*

| Subject Protein (Accession & Description) | Alignment Length | % Identity | $init1$ Score | $initn$ Score | $opt$ Score | Expect Value ($E$) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| `P68871` (HBB_HUMAN, Hemoglobin beta) | 147 | 100.0% | 1022 | 1022 | 1022 | $1.8 \times 10^{-72}$ |
| `P02042` (HBD_HUMAN, Hemoglobin delta) | 147 | 95.2% | 968 | 968 | 968 | $2.1 \times 10^{-68}$ |
| `P69891` (HBG1_HUMAN, Hemoglobin gamma-1) | 147 | 73.5% | 745 | 745 | 745 | $4.5 \times 10^{-52}$ |
| `P69905` (HBA_HUMAN, Hemoglobin alpha) | 144 | 43.1% | 342 | 412 | 448 | $8.2 \times 10^{-28}$ |
| `P02144` (MYG_HUMAN, Myoglobin) | 144 | 28.5% | 158 | 234 | 268 | $2.4 \times 10^{-14}$ |

### Table 7.2: Methodological Comparison (Completed)
| Metric / Parameter | FASTA ($ktup=2$) | FASTA ($ktup=1$) | SSEARCH (Smith-Waterman) | NCBI BLASTP |
|---|---|---|---|---|
| Execution Speed (Relative) | Fast (~10–15 sec) | Moderate (~40–60 sec) | Slow (~2–5 min) | Very Fast (~2–5 sec) |
| Myoglobin Identity (%) | 28.5% | 28.5% | 28.5% | 28.5% |
| Myoglobin $E$-value | $\sim 2.4 \times 10^{-14}$ | $\sim 8.1 \times 10^{-16}$ | $\sim 4.2 \times 10^{-16}$ | $\sim 1.5 \times 10^{-18}$ |
| Neuroglobin Detected? (Yes/No) | Borderline ($E \sim 0.02$) | Yes ($E \sim 10^{-4}$) | Yes ($E \sim 10^{-5}$) | Yes ($E \sim 4.2 \times 10^{-8}$) |
| Algorithmic Basis | Hashing ($ktup=2$) + Diagonals + Band DP | Hashing ($ktup=1$) + Diagonals + Band DP | Exhaustive Dynamic Programming | Seeding ($W=3$) + Word Neighborhood + Extension |

---

## 2. Sample FASTA Output Wireframe

```
The best scores are:                                      opt  bits  E(569516)
P68871|HBB_HUMAN Hemoglobin subunit beta OS=Homo sapiens 1022 272.4  1.8e-72
P02042|HBD_HUMAN Hemoglobin subunit delta OS=Homo sapien  968 258.4  2.1e-68
P69891|HBG1_HUMAN Hemoglobin subunit gamma-1 OS=Homo sap  745 200.1  4.5e-52
P69905|HBA_HUMAN Hemoglobin subunit alpha OS=Homo sapien  448 122.5  8.2e-28
P02144|MYG_HUMAN Myoglobin OS=Homo sapiens OX=9606 GN=MB  268  75.6  2.4e-14

>>>P02144|MYG_HUMAN, 154 aa vs NP_000509.1, 147 aa
 init1: 158 initn: 234 opt: 268  Z-score: 382.4  bits: 75.6 E(569516): 2.4e-14
Smith-Waterman score: 268; 28.5% identity (52.8% similar) in 144 aa overlap (5-146:8-149)
```

---

## 3. Model Answers to Discussion Questions

### Q1. The Four FASTA Scores
- **Model Answer:**
  - **$init1$:** The raw score of the single highest-scoring diagonal segment without any gaps, evaluated using the substitution matrix.
  - **$initn$:** The score obtained by joining multiple compatible sub-alignments across different diagonals using gap penalties.
  - **$opt$:** The optimized score computed by running restricted dynamic programming (Smith-Waterman) in a narrow band around the $init1$ diagonal.
  - **$Z$-score / $E$-value:** The normalized statistical score adjusted for library sequence length, and the resulting number of false positives expected by chance.
  - **Why $opt \ge initn \ge init1$:** Because $init1$ is an un-gapped segment; $initn$ allows joining multiple segments (which can only add positive scores if they overcome the joining penalty); and $opt$ allows insertions, deletions, and flexible boundary optimization within the band, discovering the mathematically highest score possible in that region.

### Q2. The $ktup$ Parameter
- **Model Answer:** In protein FASTA, $ktup=2$ requires two adjacent matching amino acids to register a hash hit, whereas $ktup=1$ hashes individual single residues.
  - **Sensitivity:** When $ktup=1$, any single amino acid match can seed a diagonal. For divergent proteins (like HBB vs. Neuroglobin) where mutations have disrupted contiguous dipeptide matches, $ktup=1$ allows the algorithm to detect weak similarity that $ktup=2$ misses completely.
  - **Trade-off:** The number of single-residue matches is orders of magnitude higher than dipeptide matches. This triggers extensive diagonal sorting and band dynamic programming for many random sequences, increasing execution time by 300% to 500%.

### Q3. Diagonal Joining with Gap Penalties
- **Model Answer:** In Stage 3, shifting from one diagonal to another represents an **insertion or deletion (indel)** event. The distance between the diagonals corresponds to the length of the gap:
  $$\text{Gap Length} = |\text{Diagonal}_1 - \text{Diagonal}_2|$$
  The algorithm joins two diagonals only if the sum of their segment scores minus the joining gap penalty ($P_{\text{join}} = g_{\text{open}} + k \cdot g_{\text{ext}}$) is greater than either segment score alone.

### Q4. FASTA vs. BLAST Word Construction
- **Model Answer:**
  - **FASTA:** Relies entirely on **exact string matching** of length $ktup$. The substitution matrix is not involved during Stage 1 hashing; it is used only in Stage 2 to score the diagonals.
  - **BLAST:** Generates a list of **fuzzy neighborhood words** by evaluating all possible words using the substitution matrix (BLOSUM62) and including any word that scores $\ge T$.
  - Therefore, **BLAST's seeding is inherently matrix-driven**, while FASTA's initial seeding is purely string-hashing, with matrix scoring applied downstream.

### Q5. Why SSEARCH is the Golden Benchmark
- **Model Answer:** Heuristic search algorithms (BLAST and FASTA) make approximations (dropping diagonals, requiring word seeds) that can occasionally miss the true optimal alignment or truncate alignment boundaries. **SSEARCH** implements the exact, exhaustive Smith-Waterman dynamic programming algorithm without any heuristics. It is guaranteed by mathematical proof to find the global maximum local alignment score for any given scoring matrix. Consequently, SSEARCH serves as the definitive reference standard to benchmark the sensitivity and specificity of heuristic methods.

---

## 4. Solution to Extension / Challenge Task

- **Extreme Value Distribution in FASTA:** Random local alignment scores follow a Gumbel Extreme Value Distribution, which has a positive skew (long right tail).
- **Length Normalization Regression:** In database searches, longer sequences naturally produce higher raw alignment scores simply because they offer more random alignment opportunities. William Pearson introduced a linear regression where raw scores are plotted against $\ln(\text{length})$. The regression slope determines the expected score for any sequence length. The **Z-score** represents the number of standard deviations an observed score lies above the regression line, successfully eliminating length-dependent false-positive bias.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & EBI FASTA Setup** | 2.0 | Deduct 0.5 if student used wrong database or failed to locate ktup setting. |
| **FASTA Execution & Table 7.1** | 4.0 | Deduct 0.5 per missing score column ($init1$, $initn$, $opt$, $E$-value). |
| **Comparative Table 7.2** | 2.0 | Deduct 0.5 if comparison with SSEARCH and BLAST is incomplete. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question for thorough and accurate answers. |
| **Total** | **10.0** | |
