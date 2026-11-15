# Practical 07: Sequence Similarity Searching Using the FASTA Suite and SSEARCH

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S07 (Syllabus Practical P9)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcomes (LO):** LO3 (Substitution matrices and gap penalties), LO4 (Heuristic alignment heuristics, FASTA hashing vs. BLAST, ktup sensitivity).

---

## 1. Aim & Objectives

### Aim
To perform sequence similarity searching using the classic FASTA algorithm and the rigorous SSEARCH (full Smith-Waterman) implementation at EMBL-EBI, dissect the four-step FASTA heuristic pipeline (lookup table hashing, diagonal scoring, band joining, and dynamic programming optimization), evaluate the effect of the $ktup$ word-size parameter, and systematically contrast FASTA with BLAST.

### Objectives
1. Understand the mathematical and historical foundations of the FASTA program (Lipman & Pearson, 1985; Pearson & Lipman, 1988).
2. Execute a protein similarity search using FASTA36 at EMBL-EBI querying human beta-globin (`NP_000509.1`).
3. Analyze the four stages of the FASTA algorithm:
   - Stage 1: Fast exact word matching using lookup tables (hashing) with word size $ktup$.
   - Stage 2: Finding diagonals and scoring the top 10 regions ($init1$).
   - Stage 3: Joining compatible sub-alignments across diagonals with a gap penalty ($initn$).
   - Stage 4: Full dynamic programming alignment in a narrow band around the highest diagonal ($opt$).
4. Evaluate the impact of altering the $ktup$ parameter ($ktup=2$ default vs. $ktup=1$ high sensitivity).
5. Compare FASTA results against SSEARCH (optimal local Smith-Waterman) and NCBI BLASTP for the globin family.

---

## 2. Background & Scientific Principle

### Historical Significance of FASTA
Before BLAST was introduced in 1990, the standard tool for searching sequence databases was **FASTA** (Fast All), developed by David J. Lipman and William R. Pearson in 1985 (initially as `FASTP` for proteins). FASTA introduced the concept of rapid heuristic filtering to identify promising sequence regions before investing computational time in dynamic programming.

### The Four-Step FASTA Algorithmic Pipeline
FASTA operates via a distinctive four-step pipeline that differs fundamentally from BLAST's seed-and-extend approach:

```
[Query Sequence] + [Database]
       │
       ▼
[Stage 1: Hashing & Diagonal Search] (Look up all exact matches of length ktup; record offset coordinates)
       │
       ▼
[Stage 2: Rescoring Diagonals -> init1] (Score top diagonals using BLOSUM50; identify highest scoring segment)
       │
       ▼
[Stage 3: Joining Diagonals -> initn] (Join compatible high-scoring diagonals with gap penalties)
       │
       ▼
[Stage 4: Banded Dynamic Programming -> opt] (Run restricted Smith-Waterman in a narrow band around init1)
       │
       ▼
[Statistical Evaluation (Z-score & E-value)]
```

1. **Stage 1: Exact $k$-tuple Matching via Hashing:**
   - The query sequence is indexed into words of length $k$, called **$k$-tuples** ($ktup$).
   - For proteins, default $ktup = 2$ (or $ktup = 1$ for higher sensitivity); for DNA, default $ktup = 6$.
   - An exact lookup hash table stores the position of every $k$-tuple in the query.
   - When scanning a database sequence, matching $k$-tuples are identified instantaneously by hashing.
   - For each match, the diagonal coordinate is computed: $\text{Diagonal} = \text{Query Position} - \text{Subject Position}$.
   - Exact matches falling along the same diagonal represent uninterrupted aligned segments.

2. **Stage 2: Scoring the Top Diagonals ($init1$):**
   - The 10 best diagonal regions containing high densities of $k$-tuple matches are selected.
   - Each region is rescored using an amino acid substitution matrix (historically PAM250 or BLOSUM50).
   - The single highest-scoring segment without gaps is designated the **$init1$ score**.

3. **Stage 3: Joining Diagonals ($initn$):**
   - The algorithm checks whether several high-scoring sub-alignments on different diagonals can be joined together in consistent linear order (representing insertions/deletions).
   - A joining penalty (gap penalty) is subtracted for each jump between diagonals.
   - The resulting score is the **$initn$ score**.
   - If $initn$ is below a significance threshold, the database sequence is discarded from further computation.

4. **Stage 4: Banded Smith-Waterman Optimization ($opt$):**
   - For sequences surviving Stage 3, a full dynamic programming alignment is executed, but restricted strictly to a **narrow band** (width typically 16 or 32 residues) centered around the $init1$ diagonal.
   - This produces the optimized score (**$opt$ score**).

### FASTA vs. BLAST: Fundamental Differences
| Feature | FASTA | BLAST |
|---|---|---|
| Primary Author(s) | Pearson & Lipman (1988) | Altschul et al. (1990, 1997) |
| Word Concept | Exact matches of length $ktup$ ($ktup=1$ or $2$) | Neighborhood words exceeding threshold score $T$ |
| Diagonal Handling | Explicitly tracks and joins diagonals ($init1 \rightarrow initn$) | Two-hit requirement, then extends immediately |
| Gap Treatment | Gaps introduced by joining diagonals ($initn$), then banded DP ($opt$) | Gapped extension initiated directly from seeds |
| Rigorous Benchmark | Accompanied by **SSEARCH** (exact Smith-Waterman) | No exact dynamic programming mode |
| Sensitivity on Remote Homology | High with $ktup=1$; slower than BLAST | Extremely fast; excellent with PSSMs (PSI-BLAST) |

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & URLs
- EMBL-EBI FASTA Search Gateway: [https://www.ebi.ac.uk/Tools/sss/fasta/](https://www.ebi.ac.uk/Tools/sss/fasta/)
- EMBL-EBI SSEARCH Gateway: [https://www.ebi.ac.uk/Tools/sss/fasta/ssearch/](https://www.ebi.ac.uk/Tools/sss/fasta/ssearch/)

### Input Datasets & Accessions
- Query Protein: Human hemoglobin subunit beta (`NP_000509.1`, 147 aa)
  - Local file: `../../data/sequences/hbb_human_protein.fasta`
- Target Database: UniProtKB/Swiss-Prot (or UniProtKB reviewed mammalian subset)
- Local Multi-FASTA: `../../data/sequences/globin_family_proteins.fasta`

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Running FASTA at EMBL-EBI ($ktup=2$)
1. Open your web browser and navigate to the EMBL-EBI FASTA protein service:
   `https://www.ebi.ac.uk/Tools/sss/fasta/`
2. **Step 1 - Enter your input sequence:**
   - Paste the FASTA sequence of human HBB from `../../data/sequences/hbb_human_protein.fasta` (or enter `NP_000509.1`).
3. **Step 2 - Choose database:**
   - Select **Protein Databases** $\rightarrow$ **UniProtKB/Swiss-Prot**.
4. **Step 3 - Set parameters:**
   - Click **More options** to inspect algorithm settings.
   - Program: Confirm **fasta36**.
   - Matrix: Confirm **BLOSUM50** (EBI FASTA default) or **BLOSUM62**.
   - Gap Open: `-10`
   - Gap Extension: `-2`
   - KTUP: Select **2** (default).
5. Click **Submit**.
6. When the search completes, inspect the **Tool Output** page:
   - Identify the top hits: Human HBB (`P68871`), Hemoglobin delta (`P02042`), Hemoglobin gamma (`P69891`, `P69892`), Hemoglobin alpha (`P69905`), and Myoglobin (`P02144`).
   - For each hit, note: Score ($opt$), % Identity, % Similarity, and Expectation ($E$-value).

### Phase 2: Evaluating the Impact of $ktup=1$
1. Return to the FASTA input page (or click **Edit and Resubmit**).
2. Change the **KTUP** parameter from **2** to **1**.
   *(Note: Setting $ktup=1$ instructs FASTA to hash single amino acids, significantly increasing search sensitivity for divergent sequences at the cost of execution speed).*
3. Keep all other parameters identical (UniProtKB/Swiss-Prot database, BLOSUM50 matrix).
4. Click **Submit**.
5. Locate the hits for **Myoglobin** and **Neuroglobin**.
6. Record the change in $opt$ score, bit score, and $E$-value compared to $ktup=2$.

### Phase 3: Running SSEARCH (Full Smith-Waterman)
1. In a new tab, navigate to the EMBL-EBI SSEARCH service:
   `https://www.ebi.ac.uk/Tools/sss/fasta/ssearch/`
   *(SSEARCH executes an exhaustive, non-heuristic Smith-Waterman search across the database).*
2. Paste the same human HBB sequence (`NP_000509.1`).
3. Select **UniProtKB/Swiss-Prot**.
4. Click **Submit**.
5. Compare the resulting scores and alignment boundaries against the heuristic FASTA output.

---

## 5. Offline Fallback Note

If the EMBL-EBI FASTA web server is unreachable or queued:
- Use the pre-computed BLAST and FASTA reference comparisons provided in `../../data/expected/blast_hbb_vs_refseq.tsv`.
- Refer to the detailed expected FASTA36 output scores, Z-scores, and opt values documented in the instructor answer key.

---

## 6. Observations Table

### Table 7.1: FASTA Search Results for Human HBB (`NP_000509.1`) against UniProtKB/Swiss-Prot
| Subject Protein (Accession & Description) | Alignment Length | % Identity | $init1$ Score | $initn$ Score | $opt$ Score | Expect Value ($E$) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| `P68871` (HBB_HUMAN, Hemoglobin beta) | 147 | 100.0% | | | | |
| `P02042` (HBD_HUMAN, Hemoglobin delta) | 147 | 95.2% | | | | |
| `P69891` (HBG1_HUMAN, Hemoglobin gamma-1) | 147 | 73.5% | | | | |
| `P69905` (HBA_HUMAN, Hemoglobin alpha) | 144 | 43.1% | | | | |
| `P02144` (MYG_HUMAN, Myoglobin) | 144 | 28.5% | | | | |

### Table 7.2: Methodological Comparison (FASTA $ktup=2$ vs. $ktup=1$ vs. SSEARCH vs. BLASTP)
| Metric / Parameter | FASTA ($ktup=2$) | FASTA ($ktup=1$) | SSEARCH (Smith-Waterman) | NCBI BLASTP |
|---|---|---|---|---|
| Execution Speed (Relative) | Fast | Moderate | Slow (Exhaustive) | Very Fast |
| Myoglobin Identity (%) | 28.5% | 28.5% | 28.5% | 28.5% |
| Myoglobin $E$-value | | | | |
| Neuroglobin Detected? (Yes/No) | | | | |
| Algorithmic Basis | Hashing ($ktup=2$) + Diagonals + Band DP | Hashing ($ktup=1$) + Diagonals + Band DP | Exhaustive Dynamic Programming | Seeding ($W=3$) + Word Neighborhood + Extension |

---

## 7. Interpretation & Discussion Questions

1. **The Four FASTA Scores:** Explain the specific biological and computational meaning of each of the four scores reported by the FASTA algorithm: $init1$, $initn$, $opt$, and $Z$-score / $E$-value. Why does $opt \ge initn \ge init1$?
2. **The $ktup$ Parameter:** What happens mathematically when $ktup$ is reduced from 2 to 1 in a protein FASTA search? Why does sensitivity for remote homologues increase, and what is the trade-off in computation time?
3. **Diagonal Joining with Gap Penalties:** In Stage 3 of the FASTA pipeline, how does the algorithm decide whether to join two high-scoring sub-alignments on different diagonals? What biological event does a shift from one diagonal to another represent?
4. **FASTA vs. BLAST Word Construction:** Contrast how FASTA identifies initial seed matches using $k$-tuples versus how BLAST identifies seeds using neighborhood words and threshold $T$. Which method is more mathematically dependent on the choice of substitution matrix during the initial seeding phase?
5. **Why SSEARCH is the Golden Benchmark:** Why do bioinformaticians use SSEARCH when evaluating the accuracy of newly developed heuristic alignment algorithms, rather than using BLAST or FASTA as the benchmark?

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Examine the FASTA statistical estimation method: William Pearson showed that raw scores in sequence database searches follow an Extreme Value Distribution (Gumbel distribution).
2. Look at the FASTA output summary showing the histogram of normalized Z-scores.
3. Explain why FASTA performs a linear regression of score against the logarithm of database sequence length to eliminate length-dependent score bias.
