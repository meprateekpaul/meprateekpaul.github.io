# Practical 06: Sequence Similarity Searching Using BLAST (Basic Local Alignment Search Tool)

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S06 (Syllabus Practical P8)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcomes (LO):** LO3 (Substitution matrices and gap penalties), LO4 (Heuristic alignment, BLAST flavours, E-value and bit score interpretation).

---

## 1. Aim & Objectives

### Aim
To perform sequence similarity searching across primary biological databases using the Basic Local Alignment Search Tool (BLAST), master the selection of BLAST algorithm variants (blastn, blastp, blastx), evaluate the statistical significance of High-scoring Segment Pairs (HSPs), and analyze the impact of substitution matrices and search parameters on alignment sensitivity.

### Objectives
1. Understand the seed-and-extend heuristic methodology of BLAST and contrast it with optimal dynamic programming (Smith-Waterman).
2. Select and execute appropriate BLAST search programs (blastp, blastn, blastx) for given biological queries.
3. Query the NCBI Reference Protein database with the human beta-globin protein sequence (`NP_000509.1`).
4. Read, filter, and interpret tabular and graphical BLAST output: Percentage Identity, Query Coverage, Raw Score ($S$), Bit Score ($S'$), and Expect Value ($E$-value).
5. Systematically evaluate the mathematical impact of altering substitution matrices (BLOSUM62 vs. BLOSUM45 vs. PAM250), word sizes ($W=3$ vs. $W=6$), and filtering parameters on the identification of distant paralogues (e.g., Myoglobin, Neuroglobin).

---

## 2. Background & Scientific Principle

### The Need for Heuristic Sequence Searching
Exact local alignment algorithms (Smith-Waterman) guarantee mathematically optimal alignments. However, Smith-Waterman has a computational time complexity of $\mathcal{O}(m \cdot n)$ per comparison, where $m$ is the query length and $n$ is the database size. Searching a modern database containing hundreds of millions of sequences using Smith-Waterman is computationally prohibitive.

To solve this, Altschul and colleagues (1990, 1997) developed **BLAST**, a heuristic algorithm that sacrifices guaranteed optimality for a 50- to 100-fold increase in execution speed.

### The BLAST Algorithmic Strategy (Seed and Extend)
BLAST executes in three distinct heuristic stages:
1. **Word Generation (Seeding):**
   - For a protein query, all overlapping words of fixed length $W$ (default $W=3$) are extracted.
   - Using a substitution matrix (default BLOSUM62), a list of neighborhood words that score at or above a threshold score $T$ is compiled.
2. **Hit Detection:**
   - The database is scanned for exact matches to the query word list.
   - Modern two-hit BLAST requires two independent word hits on the same diagonal within a distance $A$ before initiating extension.
3. **Ungapped and Gapped Extension:**
   - The seed hit is extended bidirectionally along the diagonal. Extension continues until the cumulative alignment score drops by an amount $X$ below the maximum score achieved so far.
   - Successful extensions produce a **High-scoring Segment Pair (HSP)**.

### Statistical Significance: Raw Score, Bit Score, and E-value
The raw alignment score $S$ depends on the specific scoring matrix and gap penalties used. To allow comparisons across different matrices and database sizes, BLAST calculates:

1. **Bit Score ($S'$):**
   $$S' = \frac{\lambda S - \ln K}{\ln 2}$$
   where $\lambda$ (lambda) and $K$ are statistical parameters derived from the extreme value distribution (Karlin-Altschul statistics) reflecting the scoring system and background sequence composition. Bit score is normalized and independent of database size.

2. **Expect Value ($E$-value):**
   The number of distinct alignments with a score $\ge S$ expected to occur purely by chance when searching a random database of size $N$:
   $$E = K \cdot m \cdot N \cdot e^{-\lambda S} = m \cdot N \cdot 2^{-S'}$$
   where $m$ is the effective query length and $N$ is the effective database length.
   - An $E$-value of $10^{-50}$ indicates an infinitesimal probability of occurring by chance (certain homology).
   - An $E$-value around $1$ to $10$ indicates alignments consistent with random noise.
   - **Crucial Rule:** As database size $N$ expands, the $E$-value for the exact same alignment increases linearly, while the bit score remains constant.

### The Five Core BLAST Flavors
| Program | Query Sequence | Database Searched | Translation | Primary Application |
|---|---|---|---|---|
| **blastn** | Nucleotide | Nucleotide | None | Finding identical/closely related genes, mapping primers |
| **blastp** | Protein | Protein | None | Identifying homologous protein families, domain sharing |
| **blastx** | Nucleotide | Protein | Query translated in 6 frames | Identifying protein-coding genes in novel unannotated DNA |
| **tblastn** | Protein | Nucleotide | Database translated in 6 frames | Finding unannotated homologous genes in raw genome assemblies |
| **tblastx** | Nucleotide | Nucleotide | Both translated in 6 frames | Detecting remote relationships between highly divergent DNA sequences |

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & URLs
- NCBI BLAST Gateway: [https://blast.ncbi.nlm.nih.gov/Blast.cgi](https://blast.ncbi.nlm.nih.gov/Blast.cgi)
- NCBI blastp: [https://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE=Proteins](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE=Proteins)
- NCBI blastn: [https://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE=Nucleotides](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE=Nucleotides)

### Input Datasets & Accessions
- Query Protein: Human hemoglobin subunit beta (`NP_000509.1`, 147 aa)
  - Local path: `../../data/sequences/hbb_human_protein.fasta`
- Query Nucleotide: Human *HBB* mRNA (`NM_000518.5`, 626 bp)
  - Local path: `../../data/sequences/hbb_human_mrna.fasta`
- Pre-computed Reference Output: `../../data/expected/blast_hbb_vs_refseq.tsv`

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Running Standard blastp
1. Navigate to the NCBI BLAST page and click **Protein BLAST (blastp)**.
2. In the "Enter Query Sequence" box, paste the accession `NP_000509.1` (or paste the FASTA sequence from `../../data/sequences/hbb_human_protein.fasta`).
3. Under "Choose Search Set":
   - Database: Select **Reference proteins (refseq_protein)**.
   - Organism: Restrict search to `Homo sapiens (taxid:9606)`.
4. Under "Algorithm parameters" (expand at the bottom):
   - Confirm Target Sequences = `100`
   - Confirm Expect threshold = `0.05`
   - Confirm Word size = `6`
   - Confirm Matrix = `BLOSUM62`
   - Confirm Gap Costs = `Existence: 11, Extension: 1`
   - Confirm Filter = Low complexity regions (default: unmasked or conditional)
5. Click the large blue **BLAST** button.

### Phase 2: Inspecting and Interpreting blastp Output
1. When the results page loads, inspect the **Graphic Summary**:
   - Observe how hits align along the 147-amino-acid query bar.
   - Notice the color coding indicating bit scores ($S' \ge 200$ red, $80-200$ magenta, etc.).
2. Scroll to the **Descriptions** table:
   - Identify the top hit: `NP_000509.1 hemoglobin subunit beta [Homo sapiens]`.
   - Note: Max Score = `298`, Total Score = `298`, Query Cover = `100%`, E-value = `1.2e-105`, Per. Ident = `100.00%`.
3. Locate subsequent globin family paralogues:
   - Hemoglobin delta (`NP_000510.1`): ~95% identity.
   - Hemoglobin gamma-1 and gamma-2 (`NP_000550.2`, `NP_000549.1`): ~73% identity.
   - Hemoglobin alpha (`NP_000508.1`): ~43% identity.
   - Myoglobin (`NP_005359.1`): ~28% identity, E-value ~ $10^{-18}$.
   - Neuroglobin (`NP_067080.1`): ~24% identity, E-value ~ $10^{-8}$.
4. Click on the Myoglobin hit to inspect the **Alignments** view:
   - Notice the alignment layout: Identities, Positives (conservative substitutions scoring $>0$ in BLOSUM62), and Gaps.

### Phase 3: Evaluating the Effect of Scoring Matrices
1. Click **Edit Search** at the top of the results page.
2. Expand **Algorithm parameters**:
   - Change the Matrix from **BLOSUM62** to **BLOSUM45** (designed for more divergent sequences).
   - Keep all other settings identical.
   - Click **BLAST**.
3. Record the E-values and bit scores for Myoglobin (`NP_005359.1`) and Neuroglobin (`NP_067080.1`). Notice how the statistical significance of distant relatives increases with a matrix tuned for lower sequence identity.
4. Repeat the experiment using **PAM250**. Record the resulting hit rankings and scores.

### Phase 4: Cross-Flavour Search (blastx)
1. Navigate back to BLAST home and select **blastx** (translated nucleotide query vs. protein database).
2. Paste the human *HBB* mRNA sequence (`NM_000518.5`).
3. Set Database = **Reference proteins (refseq_protein)**, Organism = `Homo sapiens (taxid:9606)`.
4. Click **BLAST**.
5. Examine the result:
   - Identify which of the 6 reading frames generated the top hit (Frame `+1`, `+2`, or `+3`).
   - Confirm that the translation in the correct frame corresponds exactly to `NP_000509.1`.

---

## 5. Offline Fallback Note

If the NCBI BLAST server is unreachable or offline:
- Open the local pre-computed tabular output file `../../data/expected/blast_hbb_vs_refseq.tsv` in a text editor or spreadsheet viewer.
- The file contains exact tab-delimited values for query ID, subject ID, % identity, alignment length, mismatches, gap opens, query start/end, subject start/end, E-value, bit score, and subject title for human HBB against the RefSeq database.

---

## 6. Observations Table

### Table 6.1: Tabular BLASTP Hits for Human HBB (`NP_000509.1`) vs. Human RefSeq
| Subject Accession | Protein Name / Paralog Description | Query Cover (%) | % Identity | Positives (%) | Bit Score ($S'$) | Expect Value ($E$) |
|---|---|:---:|:---:|:---:|:---:|:---:|
| `NP_000509.1` | Hemoglobin subunit beta | 100% | 100.00% | 100% | | |
| `NP_000510.1` | Hemoglobin subunit delta | 100% | 95.24% | | | |
| `NP_000550.2` | Hemoglobin subunit gamma-1 | 100% | 73.47% | | | |
| `NP_000508.1` | Hemoglobin subunit alpha | 97% | 43.06% | | | |
| `NP_005359.1` | Myoglobin | 97% | 28.47% | | | |
| `NP_067080.1` | Neuroglobin | 95% | 24.11% | | | |

### Table 6.2: Matrix Sensitivity Comparison for Distant Paralogues
| Target Homologue | Metric | Default (BLOSUM62) | Divergent (BLOSUM45) | Ancient (PAM250) |
|---|---|:---:|:---:|:---:|
| **Myoglobin** (`NP_005359.1`) | Bit Score ($S'$) | | | |
| | Expect Value ($E$) | | | |
| **Neuroglobin** (`NP_067080.1`) | Bit Score ($S'$) | | | |
| | Expect Value ($E$) | | | |

---

## 7. Interpretation & Discussion Questions

1. **Bit Score vs. Raw Score:** Why is it scientifically invalid to compare raw alignment scores ($S$) obtained using BLOSUM62 against raw scores obtained using PAM250? How does the bit score ($S'$) solve this problem?
2. **Database Size Dependence of $E$-value:** If the NCBI RefSeq database doubles in size over the next five years, what will happen to the $E$-value of an identical alignment between HBB and Myoglobin (assuming identical query, scoring matrix, and alignment score)? What will happen to the bit score?
3. **The "Twilight Zone" of Sequence Identity:** In Table 6.1, Myoglobin shares only 28.5% sequence identity with HBB, placing it directly in the sequence alignment "twilight zone" (20%–35% identity). Why can we be absolutely confident that Myoglobin is truly homologous to HBB despite this low identity? (Cite two specific metrics).
4. **BLOSUM Matrix Numbering vs. PAM Numbering:** Explain the opposite numbering conventions of BLOSUM and PAM matrices: Why is BLOSUM45 used for *distant* relatives while PAM250 is used for *distant* relatives?
5. **Heuristic Seeding Trade-offs:** What happens to BLAST sensitivity and execution run time if the protein word size $W$ is decreased from $W=3$ to $W=2$? Why does NCBI blastp default to $W=3$ (or $W=6$ in accelerated mode)?

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Run **blastn** querying the human *HBB* mRNA sequence (`NM_000518.5`) against the nucleotide collection (`nt/nr`) with the organism set to `Mammalia`.
2. Observe which globin family members are detected.
3. Compare the blastn hit list against the blastp hit list. Why does blastp detect remote homologues (like myoglobin and neuroglobin) that blastn fails to find entirely? Explain this in terms of the genetic code redundancy and nucleotide divergence saturation.
