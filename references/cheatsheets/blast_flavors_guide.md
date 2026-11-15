# Quick Reference: BLAST Flavours & Statistical Parameters

The Basic Local Alignment Search Tool (BLAST) finds regions of local similarity between biological sequences.

---

## 1. The Five Core BLAST Flavours

| Program | Query Type | Database Type | Comparison Level | Primary Use Case |
|---|---|---|---|---|
| **blastn** | Nucleotide | Nucleotide | DNA vs DNA | Finding identical or closely related genes, PCR primers, mapping clones |
| **blastp** | Protein | Protein | Amino Acid vs Amino Acid | Detecting distant homologous proteins, function transfer, domain identification |
| **blastx** | Nucleotide | Protein | 6-Frame Translated DNA vs Protein | Identifying novel protein-coding genes in genomic or cDNA contigs |
| **tblastn** | Protein | Nucleotide | Protein vs 6-Frame Translated Database | Finding unannotated coding regions across newly sequenced genomes |
| **tblastx** | Nucleotide | Nucleotide | 6-Frame DNA vs 6-Frame Database | Finding distant relationships between two unannotated DNA sequences |

---

## 2. Reading BLAST Statistical Metrics

### E-value (Expect Value)
The number of distinct alignments with a score equal to or greater than $S$ that one expects to see by chance in a database of size $N$:
$$E = K \cdot m \cdot n \cdot e^{-\lambda S}$$
- $m$: query length
- $n$: effective database size
- $K, \lambda$: Karlin–Altschul statistical scaling parameters
- **Rule of Thumb:**
  - $E \le 10^{-10}$: Definitive homology.
  - $10^{-10} < E \le 10^{-4}$: Probable homology (inspect coverage, domain match, and active site conservation).
  - $E > 0.05$: Statistically indistinguishable from random chance.

### Bit Score ($S'$)
A normalized score independent of database size and scoring system:
$$S' = \frac{\lambda S - \ln K}{\ln 2}$$
Bit scores allow comparisons across different searches and different database releases.

---

## 3. Substitution Matrix Selection

| Matrix | Best For | Typical Sequence Divergence | Equivalent PAM |
|---|---|---|---|
| **BLOSUM80** | Very close relatives, short queries | 80% identity or higher | ~PAM120 |
| **BLOSUM62** | **Default standard**, general protein search | 60%–70% identity | ~PAM250 |
| **BLOSUM45** | Distantly related proteins, deep homology | 30%–45% identity | ~PAM350 |

---

## 4. Searching Artifacts & Masking
- **Low-Complexity Regions:** Segments with biased amino acid composition (e.g., poly-proline, collagen Gly-X-Y repeats). Handled by **SEG** (protein) or **DUST** (nucleotide) filtering.
- **RepeatMasker:** Removes interspersed transposable elements (LINEs, SINEs, Alu) prior to genome searching.
