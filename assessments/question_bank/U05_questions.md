# Question Bank: Unit 5 — Sequence Alignment and Database Searching

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Syllabus Topic:** Evolutionary Basis of Sequence Alignment, Optimal alignment method, Substitution Score and Gap Penalty, Statistical Significance of Alignment Database similarity searching, FASTA, BLAST, Database searching Artifacts, Position Specific Scoring Matrices  
**Primary Learning Outcomes:** LO3, LO4 (Dynamic programming hand calculations, matrices, gap penalties, Karlin-Altschul statistics, BLAST/FASTA heuristics, PSSMs)  

---

## Section A: Multiple Choice Questions (15 MCQs)

### Q01
Two homologous genes that diverged as a result of a speciation event (e.g., human beta-globin and chimpanzee beta-globin) are defined as:  
a) Paralogues  
b) Orthologues  
c) Xenologues  
d) Analogues  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Orthologues  
* **Rationale:** Orthologues are genes in different species that evolved from a common ancestral gene via speciation and typically retain the same biological function. Paralogues arise via gene duplication within a genome (e.g., alpha- and beta-globin).

### Q02
In a dot-plot comparison between two sequences, what biological feature is indicated by a diagonal line shifted parallel to the main diagonal?  
a) An inversion of a sequence segment  
b) An insertion or deletion (indel) that altered the relative register of identical sequence segments  
c) A complete loss of sequence homology  
d) A ribosomal frameshift mutation  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) An insertion or deletion (indel) that altered the relative register of identical sequence segments  
* **Rationale:** In dot plots, a continuous diagonal indicates matched segments. If a diagonal is offset from the main central diagonal, it reveals that an insertion or deletion occurred upstream, displacing the matching region along one axis.

### Q03
What is the fundamental mathematical difference between the Needleman–Wunsch algorithm and the Smith–Waterman algorithm?  
a) Needleman-Wunsch is heuristic, whereas Smith-Waterman is exact dynamic programming  
b) Needleman-Wunsch initializes the first row and column with cumulative gap penalties and finds an end-to-end global alignment, whereas Smith-Waterman initializes with zeros and resets negative scores to zero to find optimal local alignments  
c) Needleman-Wunsch aligns only nucleotides, while Smith-Waterman aligns only proteins  
d) Needleman-Wunsch does not permit gap penalties  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Needleman-Wunsch initializes the first row and column with cumulative gap penalties and finds an end-to-end global alignment, whereas Smith-Waterman initializes with zeros and resets negative scores to zero to find optimal local alignments  
* **Rationale:** Global alignment (Needleman-Wunsch) forces the alignment across the entire length of both sequences ($F(i,0) = -i \cdot d$). Local alignment (Smith-Waterman) includes a zero lower bound ($F(i,j) = \max\{0, \dots\}$), allowing alignments to begin and end anywhere with maximum local score.

### Q04
Why is an affine gap penalty model ($W(k) = W_g + (k-1) \cdot W_s$) biologically more realistic than a simple linear gap penalty model ($W(k) = k \cdot d$)?  
a) Because a single mutational event (e.g., strand slippage or unequal crossing over) frequently inserts or deletes multiple contiguous residues at once  
b) Because biological cells do not allow gap extensions  
c) Because linear gap penalties violate the laws of thermodynamics  
d) Because affine gap penalties run faster on computer graphics cards  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) Because a single mutational event (e.g., strand slippage or unequal crossing over) frequently inserts or deletes multiple contiguous residues at once  
* **Rationale:** Biologically, opening a gap requires a distinct mutational event (high penalty $W_g$), whereas extending an existing gap by additional residues often happens in that same single event (low penalty $W_s$).

### Q05
How is the Henikoff BLOSUM substitution matrix family numbered, and which matrix is optimal for aligning sequences with roughly 62% identity?  
a) Higher numbers denote greater evolutionary divergence; BLOSUM30 is for 62% identity  
b) Lower numbers denote closer relationships; BLOSUM80 is for 62% identity  
c) The number denotes the clustering identity threshold of sequences; BLOSUM62 is derived from blocks clustered at 62% identity  
d) The number represents the percentage of gaps permitted in the alignment  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Remember/Understand  
* **Correct Answer:** c) The number denotes the clustering identity threshold of sequences; BLOSUM62 is derived from blocks clustered at 62% identity  
* **Rationale:** In BLOSUM matrices, sequences sharing $\ge X\%$ identity are clustered into single consensus representatives. BLOSUM62 clusters at 62% identity and is the standard default for general-purpose protein alignments. Higher numbers (BLOSUM80) suit closely related sequences; lower numbers (BLOSUM45) suit distant homologues.

### Q06
In contrast to BLOSUM, how are Margaret Dayhoff's PAM (Point Accepted Mutation) matrices scaled?  
a) PAM1 corresponds to 1% amino acid divergence; higher PAM numbers (e.g., PAM250) model greater evolutionary divergence calculated by matrix multiplication ($PAM1^{250}$)  
b) PAM250 corresponds to very closely related sequences, while PAM1 is for distant homologues  
c) PAM numbers represent the physical length of the query protein  
d) PAM matrices are derived exclusively from ribosomal RNA alignments  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) PAM1 corresponds to 1% amino acid divergence; higher PAM numbers (e.g., PAM250) model greater evolutionary divergence calculated by matrix multiplication ($PAM1^{250}$)  
* **Rationale:** One PAM unit corresponds to 1 accepted mutation per 100 residues. Extrapolation to distant divergence is achieved by raising the PAM1 transition probability matrix to powers ($PAM250 = PAM1^{250}$). Thus, larger PAM numbers = greater divergence.

### Q07
In Karlin-Altschul statistics for sequence alignment, what does the Expectation value ($E$-value) represent?  
a) The probability that the two aligned proteins have identical 3D structures  
b) The expected number of distinct alignments with a score equal to or greater than $S$ that would occur purely by random chance in a database of size $N$  
c) The percentage sequence identity divided by query length  
d) The time in milliseconds required for BLAST to execute  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The expected number of distinct alignments with a score equal to or greater than $S$ that would occur purely by random chance in a database of size $N$  
* **Rationale:** The $E$-value describes the random background noise: $E = K \cdot m \cdot n \cdot e^{-\lambda S}$. An $E$-value of $0.05$ means that in a database of size $n$, one would expect to see a hit with this score purely by chance only $0.05$ times (1 in 20).

### Q08
If the size of a sequence database ($n$) doubles, what happens to the bit score ($S'$) and the $E$-value of an identical alignment match?  
a) The bit score doubles; the $E$-value remains unchanged  
b) The bit score remains unchanged; the $E$-value doubles  
c) Both the bit score and the $E$-value double  
d) Both the bit score and the $E$-value are halved  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** b) The bit score remains unchanged; the $E$-value doubles  
* **Rationale:** The bit score $S' = (\lambda S - \ln K)/\ln 2$ is normalized and depends exclusively on the alignment score, independent of database size. The $E$-value is directly proportional to search space size ($E \propto m \cdot n$); doubling $n$ doubles the expected number of random false-positive hits.

### Q09
Which BLAST program should be selected to compare a newly sequenced, uncharacterized cDNA nucleotide query against the NCBI non-redundant Protein database (nr)?  
a) blastn  
b) blastp  
c) blastx  
d) tblastn  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** c) blastx  
* **Rationale:** `blastx` dynamically translates a nucleotide query in all six reading frames (+1, +2, +3, -1, -2, -3) and compares the resulting peptide translations against a protein database. `blastn` is DNA vs DNA; `blastp` is Protein vs Protein; `tblastn` compares a protein query against a translated nucleotide database.

### Q10
How does the FASTA heuristic algorithm initially identify candidate matching regions in a database before executing full alignments?  
a) By building a neural network autoencoder of all sequences  
b) By finding shared short exact words of length $k$ ($ktup$) using a lookup table and identifying high-density diagonal bands in a virtual dot plot  
c) By calculating global Needleman-Wunsch alignments against every record in the database  
d) By computing the molecular weight of the query  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) By finding shared short exact words of length $k$ ($ktup$) using a lookup table and identifying high-density diagonal bands in a virtual dot plot  
* **Rationale:** FASTA indexes the query into short $k$-tuples ($ktup=1$ or 2 for proteins; 4–6 for DNA) using a lookup table. It rapidly identifies diagonals with high concentrations of matching words without gaps (`init1`), joins consistent diagonals (`initn`), and rescores the optimal band using Smith-Waterman (`opt`).

### Q11
What is a "High-scoring Segment Pair" (HSP) in BLAST terminology?  
a) A pair of primers used to amplify the query sequence  
b) A local pairwise alignment between query and database subject that contains no insertions or deletions and whose alignment score cannot be improved by extension or trimming  
c) Two proteins that have identical quaternary crystal structures  
d) The highest scoring pair of exons in an mRNA  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) A pair of primers used to amplify the query sequence  
* **Rationale:** In BLAST, an HSP is an un-gapped alignment segment between two sequences whose score cannot be improved by extending or shortening the segment boundaries. Modern gapped BLAST combines multiple proximal HSPs.

### Q12
What biological artifact in protein sequences commonly generates spurious, artificially low $E$-values and misleading BLAST hits if not masked by programs like SEG?  
a) Disulfide bridges between cysteines  
b) Low-complexity regions (e.g., poly-proline tracts or simple amino acid repeats)  
c) Alpha-helical dipoles  
d) Stop codons at the carboxyl terminus  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Low-complexity regions (e.g., poly-proline tracts or simple amino acid repeats)  
* **Rationale:** Low-complexity regions contain biased, repetitive amino acid compositions (e.g., proline-rich or glutamine tracts). They align with high scores against other unrelated proteins possessing similar compositional bias purely due to residue frequencies, not common ancestry. The SEG filter masks these regions with 'X's.

### Q13
What is the primary operational advantage of Position-Specific Iterative BLAST (PSI-BLAST) over standard blastp?  
a) PSI-BLAST runs ten times faster than blastp  
b) PSI-BLAST constructs a position-specific scoring matrix (PSSM) from an alignment of initial hits, greatly increasing sensitivity to detect distant evolutionary homologues  
c) PSI-BLAST automatically solves the 3D crystal structure of the hit  
d) PSI-BLAST does not require a database  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) PSI-BLAST constructs a position-specific scoring matrix (PSSM) from an alignment of initial hits, greatly increasing sensitivity to detect distant evolutionary homologues  
* **Rationale:** Standard blastp uses a static, uniform matrix (BLOSUM62) across all positions. PSI-BLAST builds a dynamic profile (PSSM) where highly conserved functional positions receive severe mismatch penalties, while variable positions tolerate substitutions, uncovering distant homologues in the "twilight zone" of sequence similarity.

### Q14
What is the danger known as "profile drift" during iterative PSI-BLAST searches?  
a) The database file runs out of disk storage  
b) A non-homologous or false-positive sequence passes the inclusion threshold and is incorporated into the PSSM, corrupting the profile and pulling in thousands of unrelated sequences in subsequent iterations  
c) The query sequence degrades into random nucleotide noise  
d) The computer CPU clock speed drifts over time  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) A non-homologous or false-positive sequence passes the inclusion threshold and is incorporated into the PSSM, corrupting the profile and pulling in thousands of unrelated sequences in subsequent iterations  
* **Rationale:** Profile drift occurs when an erroneous false-positive hit (e.g., with a marginal $E$-value or shared coiled-coil motif) is included in the PSSM. In the next iteration, the PSSM shifts towards this false sequence family, compounding errors exponentially until the search retrieves irrelevant hits.

### Q15
When filtering low-complexity regions during BLAST searches, what is the difference between "hard masking" and "soft masking"?  
a) Hard masking converts low-complexity residues to 'N's or 'X's for both initial word seeding and final extension, whereas soft masking masks residues only during word seeding while allowing real residues to participate in alignment extension  
b) Hard masking deletes the query file from the server  
c) Soft masking is applied only to plant sequences  
d) Hard masking uses BLOSUM45 while soft masking uses PAM250  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) Hard masking converts low-complexity residues to 'N's or 'X's for both initial word seeding and final extension, whereas soft masking masks residues only during word seeding while allowing real residues to participate in alignment extension  
* **Rationale:** Hard masking permanently replaces biased residues with 'X' (or 'N'), completely preventing alignments from passing through those regions. Soft masking (displayed in lowercase) prevents spurious word matches from initiating seeds in low-complexity regions, but allows authentic high-scoring alignments to extend through them.

---

## Section B: Short Answer Questions (6 SAQs)

### SAQ 01: Dynamic Programming Recurrence Relations (4 Marks)
**Question:** Write the exact mathematical dynamic programming recurrence relation for both:  
1. Needleman–Wunsch global alignment, and  
2. Smith–Waterman local alignment.  
Define each term in the equations and explain the significance of the zero in Smith–Waterman.  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
1. **Needleman–Wunsch (Global Alignment):**  
   $$F(i,j) = \max \begin{cases} 
   F(i-1, j-1) + s(x_i, y_j) & \text{(diagonal: match/mismatch)} \\ 
   F(i-1, j) - d & \text{(vertical: deletion/gap in sequence } Y\text{)} \\ 
   F(i, j-1) - d & \text{(horizontal: insertion/gap in sequence } X\text{)} 
   \end{cases}$$
2. **Smith–Waterman (Local Alignment):**  
   $$F(i,j) = \max \begin{cases} 
   0 & \text{(zero lower bound)} \\ 
   F(i-1, j-1) + s(x_i, y_j) \\ 
   F(i-1, j) - d \\ 
   F(i, j-1) - d 
   \end{cases}$$
* **Terms:** $F(i,j)$ is the score at cell $(i,j)$; $s(x_i, y_j)$ is the substitution score from matrix (e.g., BLOSUM62); $d$ is the gap penalty.  
* **Significance of Zero:** The zero ensures that negative cumulative scores do not propagate. If local similarity drops below zero, the alignment terminates, allowing a new local high-scoring alignment to start afresh at any downstream position.

**Marking Scheme:**  
* 1.5 Marks: Correct mathematical equation and 3 cases for Needleman-Wunsch.  
* 1.5 Marks: Correct mathematical equation and 4 cases (including 0) for Smith-Waterman.  
* 1 Mark: Precise explanation of the biological/mathematical function of the zero boundary condition.

---

### SAQ 02: PAM vs BLOSUM Matrices (4 Marks)
**Question:** Compare and contrast the PAM and BLOSUM families of substitution matrices across four criteria: underlying biological dataset, method of deriving distant matrices, numbering convention, and intended use-cases.  
* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Analyze  

**Model Answer:**  

| Feature | PAM Matrices (Dayhoff) | BLOSUM Matrices (Henikoff) |
| :--- | :--- | :--- |
| **Dataset Source** | Small set of closely related global protein alignments ($\ge 85\%$ identity). | BLOCKS database: local, un-gapped multiple alignments of conserved protein domains. |
| **Derivation of Distant Scores**| Extrapolated mathematically by taking powers of the PAM1 transition probability matrix ($PAM250 = PAM1^{250}$). | Calculated directly from observed sequence blocks clustered at varying percentage identity thresholds. |
| **Numbering Meaning** | Higher number = greater evolutionary distance ($PAM1 \rightarrow PAM250$). | Lower number = greater evolutionary distance ($BLOSUM80 \rightarrow BLOSUM45$). |
| **Recommended Equivalents** | PAM250 is roughly equivalent to BLOSUM45; PAM120 is roughly equivalent to BLOSUM80. |

**Marking Scheme:**  
* 1 Mark per table row: Accurate contrast of dataset source, mathematical derivation method, numbering scale direction, and equivalent pairings.

---

### SAQ 03: Karlin-Altschul Statistics: Bit Score vs E-value (3 Marks)
**Question:** Explain the mathematical and practical differences between a raw alignment score ($S$), a normalized bit score ($S'$), and an Expectation value ($E$-value). Why is the bit score comparable across different searches, while the raw score is not?  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand / Analyze  

**Model Answer:**  
* **Raw Score ($S$):** The direct sum of match scores, substitution matrix values, and gap penalties. It is entirely dependent on the specific scoring system used (e.g., match $+1$ vs $+5$, or BLOSUM62 vs PAM250) and cannot be compared between different matrix choices.
* **Bit Score ($S'$):** Normalizes the raw score using statistical scaling parameters $\lambda$ and $K$:  
  $$S' = \frac{\lambda S - \ln K}{\ln 2}$$  
  Because $\lambda$ and $K$ correct for the arbitrary scale and background residue frequencies of the scoring matrix, $S'$ is expressed in standard information units (bits). A bit score of 80 has the exact same statistical significance whether obtained with BLOSUM62 or PAM250.
* **$E$-value:** Incorporates search space size ($m \times n$): $E = m \cdot n \cdot 2^{-S'}$. It indicates the number of random false-positives expected purely by chance.

**Marking Scheme:**  
* 1 Mark: Accurate definition of raw score and its matrix dependence.  
* 1 Mark: Exact formula and explanation of bit score normalization independent of matrix units.  
* 1 Mark: Clear formulation of $E$-value scaling with search space ($m \cdot n$).

---

### SAQ 04: BLAST Heuristic: Words, Neighborhoods, and Seeds (4 Marks)
**Question:** Outline the three core heuristic steps used by standard protein BLAST (`blastp`) to identify sequence matches rapidly without evaluating the full dynamic programming matrix.  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
1. **Word Generation (Seeding):** The query protein is split into overlapping words of fixed length $W$ (default $W=3$ for blastp). For each query 3-mer, BLAST generates a list of all possible "neighborhood words" that score at least $T$ (threshold) when aligned against the query word using BLOSUM62.
2. **Database Scanning (Seed Matching):** BLAST uses a deterministic finite automaton (DFA) or hash table to scan the target database rapidly, flagging exact occurrences of any high-scoring neighborhood words.
3. **Extension (Ungapped and Gapped):**  
   - When a seed match is found (or two proximal matches on the same diagonal in the two-hit method), BLAST extends the alignment in both directions without gaps until the running score drops by $X$ below the maximum score attained.
   - If the un-gapped score exceeds a trigger threshold, a banded Smith–Waterman dynamic programming alignment is executed to produce the final gapped High-scoring Segment Pair (HSP).

**Marking Scheme:**  
* 1.5 Marks: Detailed explanation of word length $W$, neighborhood generation, and threshold $T$.  
* 1 Mark: Accurate explanation of high-speed database scanning using hash table/DFA.  
* 1.5 Marks: Detailed explanation of un-gapped extension with score drop-off $X$ and trigger of banded dynamic programming.

---

### SAQ 05: Interpreting the Five BLAST Flavours (3 Marks)
**Question:** Complete the following table by identifying the query type, database type, and internal translation mechanism for the five standard BLAST programs:  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  

| Program | Query Type | Database Type | Translation Mechanism |
| :--- | :--- | :--- | :--- |
| **blastn** | Nucleotide | Nucleotide | None (direct base-to-base comparison) |
| **blastp** | Protein | Protein | None (amino acid comparison) |
| **blastx** | Nucleotide | Protein | Query is translated dynamically in all 6 reading frames |
| **tblastn** | Protein | Nucleotide | Database sequences are translated dynamically in all 6 frames |
| **tblastx** | Nucleotide | Nucleotide | Both query and database are translated in 6 frames (36 comparisons) |

**Marking Scheme:**  
* 3 Marks: 0.6 marks for each correctly populated row.

---

### SAQ 06: Searching Artifacts and Low-Complexity Masking (3 Marks)
**Question:** What are low-complexity regions in proteins? Explain how they generate artifactual hits in database searches and describe how filtering with the SEG program remedies this problem.  
* **Learning Outcome:** LO4  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Definition:** Low-complexity regions are peptide segments dominated by a single amino acid or simple periodic repeats (e.g., poly-glutamine runs, collagen Gly-Pro-Pro repeats, or proline/serine-rich transcriptional activation domains).
* **Search Artifact:** When queried against large databases, low-complexity regions match unrelated proteins that happen to possess similar amino acid compositions. Because BLOSUM matrices assign positive scores to frequent matches (e.g., Pro-Pro = $+7$), these non-homologous alignments accumulate massive raw scores and statistically significant $E$-values ($E < 10^{-10}$), masking true biological homologues.
* **Remedy by SEG:** The SEG algorithm calculates the local Shannon information entropy of sequence windows. Regions with entropy below a defined threshold are masked (replaced with 'X' characters), preventing spurious word matching during the initial search phase.

**Marking Scheme:**  
* 1 Mark: Clear biological definition and examples of low-complexity regions.  
* 1 Mark: Accurate explanation of compositional bias creating false-positive high scores.  
* 1 Mark: Accurate description of SEG entropy calculation and masking mechanism.

---

## Section C: Long Answer / Problem Questions (2 LAQs)

### LAQ 01: Step-by-Step Dynamic Programming Global Alignment (10 Marks)
**Question:**  
You are given two short toy peptide sequences:  
* Sequence $X$ (Row / Query): `V - A - L`  
* Sequence $Y$ (Column / Target): `I - A - L`

Using the **Needleman–Wunsch global alignment algorithm**, align Sequence $X$ and Sequence $Y$ under the following linear scoring parameters:  
* **Match score:** $+3$ (identical residues)  
* **Conservative substitution:** $+1$ (between Valine `V` and Isoleucine `I`)  
* **Non-conservative mismatch:** $-1$ (all other mismatches)  
* **Linear gap penalty ($d$):** $-2$ for each inserted gap

a) Initialize the dynamic programming matrix $F$ of dimensions $4 \times 4$ (including the zero/gap row and column). State the formal initialization formula for global alignment. (2 Marks)  
b) Fill in all remaining cells of the dynamic programming matrix step by step. Explicitly show the three-way calculation ($\max\{\text{diagonal}, \text{up}, \text{left}\}$) for cell $(1,1)$, cell $(1,2)$, and cell $(3,3)$. (4 Marks)  
c) Draw the complete, populated scoring matrix, marking traceback arrows in every cell. (2 Marks)  
d) Trace back from cell $(3,3)$ to cell $(0,0)$ to derive the optimal global alignment. State the final alignment score and write out the resulting aligned sequences with gap characters where appropriate. (2 Marks)  

* **Learning Outcome:** LO3  
* **Bloom's Taxonomy Level:** Apply / Analyze  

**Model Solution:**  
**a) Matrix Initialization (2 Marks):**  
In Needleman–Wunsch, the first row and column are initialized with cumulative gap penalties:  
$F(0,0) = 0$  
$F(i, 0) = -i \cdot d = -2 \cdot i \implies F(1,0) = -2, F(2,0) = -4, F(3,0) = -6$  
$F(0, j) = -j \cdot d = -2 \cdot j \implies F(0,1) = -2, F(0,2) = -4, F(0,3) = -6$

**b) Step-by-Step Matrix Cell Calculations (4 Marks):**  
* **Cell (1,1) [Residue $X_1=\text{V}$, $Y_1=\text{I}$]:**  
  - Substitution score $s(\text{V}, \text{I}) = +1$ (conservative substitution)  
  - Diagonal: $F(0,0) + s(\text{V},\text{I}) = 0 + 1 = \mathbf{+1}$  
  - Up: $F(0,1) - d = -2 - 2 = -4$  
  - Left: $F(1,0) - d = -2 - 2 = -4$  
  - $F(1,1) = \max\{+1, -4, -4\} = \mathbf{+1}$ (Pointer: $\nwse$ Diagonal)

* **Cell (1,2) [Residue $X_1=\text{V}$, $Y_2=\text{A}$]:**  
  - Substitution score $s(\text{V}, \text{A}) = -1$ (non-conservative mismatch)  
  - Diagonal: $F(0,1) + s(\text{V},\text{A}) = -2 + (-1) = -3$  
  - Up: $F(0,2) - d = -4 - 2 = -6$  
  - Left: $F(1,1) - d = 1 - 2 = \mathbf{-1}$  
  - $F(1,2) = \max\{-3, -6, -1\} = \mathbf{-1}$ (Pointer: $\leftarrow$ Left)

* *[Evaluating Remaining Row 1 and Row 2 Cells]:*  
  - Cell (1,3) [$V, L$]: $\max\{F(0,2)+s(V,L), F(0,3)-2, F(1,2)-2\} = \max\{-4+1, -6-2, -1-2\} = \max\{-3, -8, -3\} = \mathbf{-3}$ (from Diag and Left)  
  - Cell (2,1) [$A, I$]: $\max\{F(1,0)+s(A,I), F(1,1)-2, F(2,0)-2\} = \max\{-2-1, 1-2, -4-2\} = \max\{-3, -1, -6\} = \mathbf{-1}$ (Pointer: $\uparrow$ Up)  
  - Cell (2,2) [$A, A$]: Match $s(A,A) = +3$. $\max\{F(1,1)+3, F(1,2)-2, F(2,1)-2\} = \max\{1+3, -1-2, -1-2\} = \mathbf{+4}$ (Pointer: $\nwse$ Diagonal)  
  - Cell (2,3) [$A, L$]: $\max\{F(1,2)+s(A,L), F(1,3)-2, F(2,2)-2\} = \max\{-1-1, -3-2, 4-2\} = \max\{-2, -5, +2\} = \mathbf{+2}$ (Pointer: $\leftarrow$ Left)  
  - Cell (3,1) [$L, I$]: $\max\{F(2,0)+s(L,I), F(2,1)-2, F(3,0)-2\} = \max\{-4+1, -1-2, -6-2\} = \max\{-3, -3, -8\} = \mathbf{-3}$  
  - Cell (3,2) [$L, A$]: $\max\{F(2,1)+s(L,A), F(2,2)-2, F(3,1)-2\} = \max\{-1-1, 4-2, -3-2\} = \max\{-2, +2, -5\} = \mathbf{+2}$ (Pointer: $\uparrow$ Up)

* **Cell (3,3) [Residue $X_3=\text{L}$, $Y_3=\text{L}$]:**  
  - Substitution score $s(\text{L}, \text{L}) = +3$ (identical match)  
  - Diagonal: $F(2,2) + s(\text{L},\text{L}) = +4 + 3 = \mathbf{+7}$  
  - Up: $F(2,3) - d = 2 - 2 = 0$  
  - Left: $F(3,2) - d = 2 - 2 = 0$  
  - $F(3,3) = \max\{+7, 0, 0\} = \mathbf{+7}$ (Pointer: $\nwse$ Diagonal)

**c) Complete Populated Dynamic Programming Matrix (2 Marks):**  

```text
         -        I        A        L
   +--------+--------+--------+--------+
 - |    0   |   -2   |   -4   |   -6   |
   +--------+--------+--------+--------+
 V |   -2   |   +1 ↖ |   -1 ← |   -3 ↖←|
   +--------+--------+--------+--------+
 A |   -4   |   -1 ↑ |   +4 ↖ |   +2 ← |
   +--------+--------+--------+--------+
 L |   -6   |   -3 ↖↑|   +2 ↑ |   +7 ↖ |
   +--------+--------+--------+--------+
```

**d) Traceback and Optimal Global Alignment (2 Marks):**  
* **Traceback:**  
  1. Start at bottom-right cell $(3,3)$ with score $+7$. Pointer points $\nwse$ diagonally to cell $(2,2)$.  
     Aligned pair: `L` / `L`.  
  2. At cell $(2,2)$ with score $+4$. Pointer points $\nwse$ diagonally to cell $(1,1)$.  
     Aligned pair: `A` / `A`.  
  3. At cell $(1,1)$ with score $+1$. Pointer points $\nwse$ diagonally to cell $(0,0)$.  
     Aligned pair: `V` / `I`.  
  4. Traceback terminates at origin $(0,0)$.
* **Final Result:**  
  - **Optimal Alignment:**  
    ```text
    Seq X:  V - A - L
            :   |   |
    Seq Y:  I - A - L
    ```
  - **Alignment Score:** $+7$ (Check: $s(\text{V},\text{I}) + s(\text{A},\text{A}) + s(\text{L},\text{L}) = 1 + 3 + 3 = +7$).

**Marking Scheme Breakdown:**  
* 2 Marks: Complete, accurate row 0 and column 0 initialization with $-2, -4, -6$.  
* 4 Marks: Explicit three-way evaluation shown for $(1,1)$, $(1,2)$, and $(3,3)$ with correct intermediate arithmetic.  
* 2 Marks: Complete $4 \times 4$ matrix drawn with correct cell values and directional traceback pointers.  
* 2 Marks: Flawless traceback path, optimal alignment diagram, and verified total score $+7$.

---

### LAQ 02: BLAST Statistical Mechanics, Heuristics, and Output Interpretation (10 Marks)
**Question:**  
A researcher investigates an uncharacterized marine actinomycete sequence. Running `blastp` against the NCBI RefSeq database (size $N = 2 \times 10^{8}$ residues) with a 250-amino-acid query yields the following hit table:

```text
Description                         Max Score  Total Score  Query Cover  E-value  Per. Ident  Accession
Hemoglobin subunit beta-like [Bac]     145        145          94%       2e-34     42.5%      WP_01124567.1
Hypothetical proline-rich protein      142        142          45%       5e-04     68.2%      WP_09876543.1
Putative flavohemoprotein [Actino]     120        120          88%       4e-27     38.1%      WP_04455667.1
```

a) Write out the Karlin–Altschul equation relating the raw alignment score ($S$), statistical parameters ($K, \lambda$), query length ($m$), database size ($n$), and the Expectation value ($E$). Calculate what the $E$-value of the first hit would become if the database size expanded 10-fold. (3 Marks)  
b) Analyze the second hit (`Hypothetical proline-rich protein`). Although it displays a high percentage identity (68.2%) and a high score (142), its $E$-value ($5 \times 10^{-4}$) is thirty orders of magnitude worse than the first hit ($2 \times 10^{-34}$). Explain the mathematical and biological reasons for this discrepancy. (3 Marks)  
c) Deconstruct the heuristic trade-off between sensitivity and speed in BLAST: explain how altering the word size ($W$) and neighborhood threshold ($T$) influences the ability to detect remote homologues versus search execution time. (2 Marks)  
d) What subsequent computational analysis (such as PSI-BLAST or HMM profile searching) should the researcher execute to confirm whether the actinomycete query is a true structural homologue of the globin fold? Describe the workflow. (2 Marks)  

* **Learning Outcome:** LO3, LO4  
* **Bloom's Taxonomy Level:** Analyze / Synthesize  

**Model Solution:**  
**a) Karlin–Altschul Equation and Database Size Scaling (3 Marks):**  
* **The Karlin–Altschul Equation:**  
  $$E = K \cdot m \cdot n \cdot e^{-\lambda S}$$  
  Where:
  - $E$: Expected number of random chance alignments with score $\ge S$.
  - $m$: Effective query sequence length in residues.
  - $n$: Effective database size in total residues.
  - $K$: Natural scale parameter for search space.
  - $\lambda$: Extreme Value Distribution (Gumbel) scale factor.
  - $S$: Raw alignment score.
* **Database Expansion Calculation:**  
  Notice that $E$ is strictly linear with respect to database size $n$ ($E \propto n$). If the database expands by a factor of 10 ($n_{\text{new}} = 10 \cdot n_{\text{old}}$), the expected number of random hits increases tenfold:  
  $$E_{\text{new}} = 10 \times E_{\text{old}} = 10 \times (2 \times 10^{-34}) = \mathbf{2 \times 10^{-33}}$$

**b) Discrepancy Analysis of the Proline-Rich Hit (3 Marks):**  
* **Query Coverage Factor:** The second hit aligns over only 45% of the query length ($112\text{ aa}$), whereas the first hit spans 94% ($235\text{ aa}$). A score of 142 compressed over a short 112-residue stretch has a fundamentally different statistical significance than a score of 145 spread across a full-length domain.
* **Low-Complexity Compositional Artifact:** Proline-rich proteins exhibit severe compositional bias. Because proline matches proline with a high positive score in BLOSUM62 ($+7$), a short segment of repetitive proline residues accumulates an artificially elevated raw score by chance.
* **Why the $E$-value is Poor ($5 \times 10^{-4}$):** When BLAST computes the statistical significance using compositional score matrix adjustment, it penalizes alignments dominated by biased residue frequencies. Short biased alignments occur with high frequency in random scrambled databases, resulting in an $E$-value close to the non-significant threshold ($10^{-3}$). In contrast, the first hit spans 94% coverage with diverse biological residues, reflecting true structural homology.

**c) Heuristic Parameters: Word Size ($W$) and Threshold ($T$) (2 Marks):**  
* **Word Size ($W$):** Reducing $W$ from 3 to 2 increases sensitivity to detect remote homologues because short conserved dipeptides are more likely to survive evolutionary divergence without mutation. However, the number of seed hits increases exponentially, dramatically slowing search speed. Increasing $W$ to 6 speeds up the search but misses distant relatives.
* **Threshold ($T$):** Lowering $T$ expands the neighborhood of acceptable substitution words (e.g., accepting more conservative amino acid replacements into the seed table). This enhances sensitivity for distant relationships, but increases search time. Raising $T$ restricts seeds to near-identical words, yielding rapid execution suited only for close homologues.

**d) Confirmatory Workflow: PSI-BLAST and Profile HMMs (2 Marks):**  
1. **PSI-BLAST Iteration:** Run the query through PSI-BLAST with an inclusion threshold $h = 0.005$. Construct a position-specific scoring matrix (PSSM) over 3 iterations to capture conserved actinomycete globin signatures (e.g., the proximal and distal histidine residues).
2. **Profile Hidden Markov Models (HMMER):** Search the Pfam database using `hmmscan` to test against the Globin profile HMM (`PF00042`).
3. **Secondary Structure & 3D Fold Prediction:** Predict secondary structure (e.g., PSIPRED) to confirm the classic 8-alpha-helix globin fold (helices A through H), followed by homology modeling (SWISS-MODEL) or AlphaFold structure comparison against known myoglobin/flavohemoglobin crystal structures (e.g., PDB 1A3N, 1CQX).

**Marking Scheme Breakdown:**  
* 3 Marks: Accurate Karlin–Altschul equation with all 5 terms defined (1.5 marks) and flawless 10-fold $E$-value math ($2 \times 10^{-33}$) (1.5 marks).  
* 3 Marks: In-depth dissection of coverage disparity (45% vs 94%) and low-complexity compositional bias causing the 30-order-of-magnitude $E$-value gulf.  
* 2 Marks: Clear analysis of trade-offs when altering word size $W$ and threshold $T$ on sensitivity vs compute time.  
* 2 Marks: Complete confirmatory pipeline detailing PSI-BLAST PSSM iteration, Pfam HMM scanning, and 8-helix globin fold structural verification.
