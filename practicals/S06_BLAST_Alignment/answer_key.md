# Instructor Answer Key & Evaluation Manual: Practical 06 (BLAST Alignment)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S06 (Syllabus Practical P8)  
**Curriculum Topic:** Sequence Alignment and Similarity Searching Using BLAST  

---

## 1. Expected Outputs & Reference Solutions

### Table 6.1: Tabular BLASTP Hits for Human HBB (`NP_000509.1`) vs. Human RefSeq (Completed)
*(Values verified against `../../data/expected/blast_hbb_vs_refseq.tsv`).*

| Subject Accession | Protein Name / Paralog Description | Query Cover (%) | % Identity | Positives (%) | Bit Score ($S'$) | Expect Value ($E$) |
|---|---|:---:|:---:|:---:|:---:|:---:|
| `NP_000509.1` | Hemoglobin subunit beta | 100% | 100.00% | 100% | `298.0` | `1.2e-105` |
| `NP_000510.1` | Hemoglobin subunit delta | 100% | 95.24% | 97.96% | `279.0` | `3.4e-98` |
| `NP_000550.2` | Hemoglobin subunit gamma-1 | 100% | 73.47% | 85.03% | `212.0` | `2.1e-72` |
| `NP_000549.1` | Hemoglobin subunit gamma-2 | 100% | 72.79% | 84.35% | `210.0` | `8.5e-72` |
| `NP_000508.1` | Hemoglobin subunit alpha | 97% | 43.06% | 59.72% | `121.0` | `4.8e-37` |
| `NP_005359.1` | Myoglobin | 97% | 28.47% | 48.61% | `73.6` | `1.5e-18` |
| `NP_067080.1` | Neuroglobin | 95% | 24.11% | 44.68% | `47.8` | `4.2e-08` |

### Table 6.2: Matrix Sensitivity Comparison for Distant Paralogues (Completed)
| Target Homologue | Metric | Default (BLOSUM62) | Divergent (BLOSUM45) | Ancient (PAM250) |
|---|---|:---:|:---:|:---:|
| **Myoglobin** (`NP_005359.1`) | Bit Score ($S'$) | `73.6` | `78.2` | `75.1` |
| | Expect Value ($E$) | `1.5e-18` | `3.2e-20` | `8.1e-19` |
| **Neuroglobin** (`NP_067080.1`) | Bit Score ($S'$) | `47.8` | `54.3` | `51.2` |
| | Expect Value ($E$) | `4.2e-08` | `1.1e-10` | `6.8e-09` |

---

## 2. Sample Alignment Wireframe (HBB vs. Myoglobin)

```
Query  NP_000509.1   hemoglobin subunit beta [Homo sapiens]
Length=147
Subject NP_005359.1  myoglobin [Homo sapiens]
Length=154

 Score = 73.6 bits (180),  Expect = 1.5e-18, Method: Compositional matrix adjust.
 Identities = 41/144 (28%), Positives = 70/144 (49%), Gaps = 3/144 (2%)

Query  5    TPEEKSAVTALWGKVN--VDEVGGEALGRLLVVYPWTQRFFESFGDLSTPDAVMGNPKVK  62
            + E +  V   W K+   + ++G E L RLL+V PWTQR+FE FG+L +   V  + K K
Sbjct  8    SEGEWQLVLHVWAKVEADVAGHGQDILIRLFKSHPETQRFEE-FGNLSSPSLVFTS-KSK  65

Query  63   AHGKKVLGAFSDGLAHLDNLKGTFATLSELHCDKLHVDPENFRLLGNVLVCVLAHHFGKE  122
            AHG +V+ A   GL HLD LKGT A LSELH +KL VD ENF+ L   ++ VL  + G +
Sbjct  66   AHGVEVVVALEAGLQHLDGLKGTIANLSELHAEKLSVDLENFKRLAQAIIVVLRDYLGSD  125

Query  123  FTPPVQAAYQKVVAGVANALAHKY  146
            FTP  QA +QK +  V  A++ K+
Sbjct  126  FTPATQAMFQKALQDVPAAVSDKF  149
```

---

## 3. Model Answers to Discussion Questions

### Q1. Bit Score vs. Raw Score
- **Model Answer:** A raw alignment score $S$ is simply the sum of individual match/mismatch substitution scores and gap penalties. Because different scoring matrices use completely different scales, log-odds bases, and target frequencies (e.g., half-bit units vs. third-bit units), a raw score of 120 under BLOSUM62 is mathematically incomparable to a raw score of 120 under PAM250. The **bit score** ($S' = \frac{\lambda S - \ln K}{\ln 2}$) normalizes the raw score using Karlin-Altschul parameters ($\lambda$ and $K$). Bit score represents the information content of the alignment measured in standard binary information units (bits), enabling direct, statistically sound comparisons across different scoring schemes.

### Q2. Database Size Dependence of $E$-value
- **Model Answer:** The Expect value equation is $E = m \cdot N \cdot 2^{-S'}$, where $N$ is the total number of amino acids in the database.
  - If the database size $N$ doubles, the number of random alignments expected to achieve that score doubles; therefore, the **$E$-value increases linearly by a factor of 2** (e.g., from $1.5 \times 10^{-18}$ to $3.0 \times 10^{-18}$).
  - In contrast, the **bit score ($S'$) remains completely unchanged** because bit score depends solely on the sequence quality of the query-subject match, independent of the external search space size.

### Q3. The "Twilight Zone" of Sequence Identity
- **Model Answer:** Although the pairwise sequence identity is only 28.5%, we are absolutely confident of true homology based on:
  1. **Extreme Statistical Significance ($E$-value):** An $E$-value of $1.5 \times 10^{-18}$ means that the probability of finding such an alignment by random chance in the database is less than 1 in $10^{17}$.
  2. **High Conservative Positives:** Over 48.6% of aligned residues represent conservative physico-chemical substitutions (positive scores in BLOSUM62).
  3. **Preservation of Key Functional Residues:** Crucial invariant functional residues (e.g., the proximal His-93 and distal His-64 coordinating the heme iron, and the conserved hydrophobic core packing residues) are perfectly preserved.

### Q4. BLOSUM Matrix Numbering vs. PAM Numbering
- **Model Answer:**
  - **BLOSUM (Blocks Substitution Matrix):** The number indicates the **minimum percentage identity threshold** used to cluster sequence blocks. Higher numbers represent more closely related sequences (BLOSUM80 = 80% clustering threshold, for near relatives). Lower numbers represent more divergent sequences (BLOSUM45 clusters sequences sharing $\ge 45\%$ identity, capturing distant evolutionary divergence).
  - **PAM (Point Accepted Mutation):** The number indicates the **evolutionary distance** measured as accepted point mutations per 100 amino acids. Higher numbers represent greater evolutionary divergence (PAM250 represents sequences that have undergone 250 mutations per 100 residues, appropriate for distant homologues; PAM30 is for closely related sequences).
  - Hence, **BLOSUM45** and **PAM250** are both tuned for remote homologs, while **BLOSUM80** and **PAM30** are tuned for close relatives.

### Q5. Heuristic Seeding Trade-offs
- **Model Answer:** If the word size $W$ is reduced from $W=3$ to $W=2$, the algorithm searches for smaller 2-amino-acid seeds.
  - **Sensitivity:** Increases significantly, because more seed hits will cross threshold $T$, allowing the detection of highly divergent distant homologs that lack a 3-residue matching word.
  - **Run Time:** Increases dramatically (combinatorial explosion), because the number of matching 2-word hits in a large database increases exponentially, forcing the extension engine to evaluate thousands of false-positive random extensions. Defaulting to $W=3$ (or $W=6$ in fast mode) provides the optimal balance of high-speed search and biologically robust sensitivity.

---

## 4. Solution to Extension / Challenge Task

1. **blastn Search Result:** Querying *HBB* mRNA (`NM_000518.5`) against mammalian nucleotide databases finds beta-globin orthologues across primates, rodents, and other mammals, plus human delta-globin and gamma-globin. However, **blastn fails to detect Myoglobin or Neuroglobin entirely** ($E > 10$ or no hits returned).
2. **Scientific Explanation:**
   - At the DNA level, nucleotide sequences undergo synonymous (silent) third-base wobble substitutions that rapidly saturate over evolutionary time (>400 million years since the myoglobin/hemoglobin gene duplication).
   - The genetic code is degenerate (64 codons for 20 amino acids). Two homologous codons can encode the exact same or chemically similar amino acid while differing in two out of three base positions.
   - Consequently, nucleotide sequence identity falls to background random noise (~25%), while protein sequence conservation is maintained by negative purifying selection on structural stability and biochemical function. Hence, protein BLAST (blastp) is vastly superior for deep evolutionary searches.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & Parameter Configuration** | 2.0 | Deduct 0.5 if organism restriction or refseq database was misconfigured. |
| **blastp Execution & Table 6.1** | 4.0 | Deduct 0.5 per missing or erroneous metric (score, E-value, identity). |
| **Matrix Comparison Table 6.2** | 2.0 | Deduct 0.5 if BLOSUM45 or PAM250 data is missing. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question for rigorous answers (E-value math, twilight zone). |
| **Total** | **10.0** | |
