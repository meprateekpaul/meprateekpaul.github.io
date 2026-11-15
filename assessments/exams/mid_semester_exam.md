# Mid-Semester Examination: Concepts of Bioinformatics

**Course Code:** CBBI-501  
**Course Title:** Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Duration:** 2 Hours (120 Minutes)  
**Maximum Marks:** 50 Marks  
**Coverage:** Units 1 to 5 (Bioinformatics & Internet, Entrez Retrieval, NCBI Data Model, GenBank, Sequence Alignment & Similarity Searching)  
**Instructions to Candidates:**
1. This paper contains THREE sections: Section A (10 Marks), Section B (20 Marks), and Section C (20 Marks).
2. Answer ALL questions in Section A.
3. Answer any FOUR out of five questions in Section B.
4. Answer BOTH questions in Section C.
5. Non-programmable scientific calculators are permitted.

---

## Part I: Question Paper

### Section A: Objective & Direct Concept Checks (10 Marks)
*(Answer ALL ten questions. Each question carries 1 Mark).*

1. Name the three international database repositories that constitute the International Nucleotide Sequence Database Collaboration (INSDC). `[1 Mark]`
2. What network port is standardly assigned for encrypted HTTPS communication with biological web portals? `[1 Mark]`
3. In NCBI Entrez search syntax, write the specific field tag used to restrict a search term strictly to an organism's taxonomic name. `[1 Mark]`
4. What is the standard RefSeq accession prefix for a curated, non-redundant human protein record? `[1 Mark]`
5. In the NCBI data model, which atomic data object stores an individual sequence and its core instance data? `[1 Mark]`
6. Identify the three-letter GenBank division code assigned to human and chimpanzee nucleotide sequence records. `[1 Mark]`
7. In a GenBank feature table, what does the `<` symbol in the coordinate expression `<1..450` signify? `[1 Mark]`
8. Differentiate between homologous genes categorized as **orthologues** versus those categorized as **paralogues**. `[1 Mark]`
9. Which substitution matrix is the default standard for NCBI `blastp` searches? `[1 Mark]`
10. In Karlin–Altschul statistics, what happens to the $E$-value of an identical alignment match if the database size ($n$) doubles? `[1 Mark]`

---

### Section B: Short Notes & Analytical Concepts (20 Marks)
*(Answer any FOUR out of the following five questions. Each question carries 5 Marks).*

11. **Client–Server Model vs Programmatic Bulk Retrieval (5 Marks):**  
    Contrast retrieving biological data via an interactive graphical web browser with automated retrieval via FTP or RESTful APIs (E-utilities) across three criteria: computational reproducibility, pipeline automation, and server bandwidth efficiency.

12. **Targeted Entrez Query Formulation (5 Marks):**  
    Formulate an exact NCBI Entrez search query to retrieve only curated RefSeq messenger RNA (mRNA) transcripts for the human insulin gene (*INS*), published between 2018 and 2023. Deconstruct each field tag and Boolean operator used.

13. **The NCBI Data Model Hierarchy (5 Marks):**  
    Explain the hierarchical relationship between `Bioseq-set`, `Bioseq`, `Seq-descr`, `Seq-annot`, `Seq-feat`, and `Seq-loc`. Why is a formal object data model superior to flat files for automated computer parsing?

14. **GenBank Feature Table Dissection (5 Marks):**  
    Examine the feature table entry: `CDS join(complement(500..850), complement(100..250))`. Explain the biological meaning of `join` and `complement`, identify the number of exons, and state the transcription direction.

15. **BLAST Heuristics & Search Artifacts (5 Marks):**  
    Explain the three heuristic phases of BLAST: seeding (words and neighborhood threshold $T$), un-gapped extension, and gapped extension. What biological problem do low-complexity regions cause during database searching, and how does SEG filtering resolve it?

---

### Section C: Numerical & Dynamic Programming Problems (20 Marks)
*(Answer BOTH questions. Each question carries 10 Marks).*

16. **Needleman–Wunsch Global Alignment Hand Calculation (10 Marks):**  
    You are given two short peptide sequences:  
    * **Sequence $X$ (Row):** `V - A - L - E`  
    * **Sequence $Y$ (Column):** `I - A - L - E`  

    **Scoring Parameters:**  
    * Identical Match: $+3$  
    * Conservative Substitution (Valine `V` vs Isoleucine `I`): $+1$  
    * All other mismatches: $-1$  
    * Linear gap penalty ($d$): $-2$ per gap character  

    a) Initialize row 0 and column 0 of the $5 \times 5$ dynamic programming matrix. State the initialization formula. `[2 Marks]`  
    b) Compute the populated dynamic programming matrix step by step. Explicitly show the three-way calculation ($\max\{\text{diagonal}, \text{up}, \text{left}\}$) for cell $(1,1)$, cell $(1,2)$, and cell $(4,4)$. `[4 Marks]`  
    c) Draw the complete, populated matrix with directional traceback arrows. `[2 Marks]`  
    d) Trace back from cell $(4,4)$ to cell $(0,0)$. Write out the optimal global alignment, state the final alignment score, and explain why Needleman–Wunsch forces end-to-end alignment. `[2 Marks]`

17. **Karlin–Altschul Statistics & BLAST Output Interpretation (10 Marks):**  
    A researcher queries a 300-amino-acid human beta-globin polypeptide against the non-redundant protein database (`nr`, total size $N = 2 \times 10^8$ amino acids). The top hit returns:  
    * Raw alignment score $S = 180$  
    * Query coverage = $98\%$  
    * Percentage identity = $55.2\%$  
    * Statistical parameters: $\lambda = 0.267$, $K = 0.041$.

    a) Write out the Karlin–Altschul formula for Expectation value ($E$) and normalized bit score ($S'$). `[2 Marks]`  
    b) Calculate the normalized bit score ($S'$) in bits for this alignment. Show your calculation. `[3 Marks]`  
    c) Calculate the theoretical $E$-value for this match. Explain what this numerical $E$-value means biologically. `[3 Marks]`  
    d) If the researcher performs the same query against a small custom database containing only 200,000 amino acids ($N = 2 \times 10^5$), calculate the new $E$-value for the exact same alignment score. Explain why bit score remains constant while $E$-value changes. `[2 Marks]`

---
---

## Part II: Instructor Model Answers & Scoring Key

### Section A: Objective Model Answers (10 Marks)
1. **INSDC Members:** NCBI GenBank (USA), EMBL-EBI ENA (Europe), and DDBJ (Japan). `[1 Mark]`
2. **HTTPS Port:** Port 443. `[1 Mark]`
3. **Organism Field Tag:** `[ORGN]` (or `[Organism]`). `[1 Mark]`
4. **RefSeq Curated Protein Prefix:** `NP_`. `[1 Mark]`
5. **Atomic Sequence Object:** `Bioseq`. `[1 Mark]`
6. **GenBank Primate Division:** `PRI`. `[1 Mark]`
7. **Meaning of `<`:** Partial sequence at 5' end (incomplete start codon / cloned fragment truncated upstream). `[1 Mark]`
8. **Orthologues vs Paralogues:** Orthologues diverged via a speciation event; paralogues diverged via an intragenomic gene duplication event. `[1 Mark]`
9. **Default BLASTp Matrix:** `BLOSUM62`. `[1 Mark]`
10. **Effect of Doubling Database Size:** The bit score remains unchanged; the $E$-value **doubles** ($E \propto n$). `[1 Mark]`

---

### Section B: Short Notes Scoring Key (20 Marks)

#### 11. Client–Server vs Automated Programmatic Bulk Retrieval (5 Marks)
* **Reproducibility (1.5 Marks):** Browser searches involve manual point-and-click steps that are prone to human variation and impossible to record in version control. Scripted API/FTP calls record exact URLs, parameters, and timestamps, ensuring 100% scientific reproducibility.
* **Pipeline Automation (1.5 Marks):** Browser interfaces cannot process 10,000 accessions sequentially. Command-line APIs (e.g., EDirect or Python `Bio.Entrez`) and FTP allow unattended batch execution chained into high-performance compute clusters.
* **Bandwidth & Server Efficiency (2.0 Marks):** Web browsers download megabytes of unnecessary HTML, CSS, JavaScript, and graphical headers. Programmatic API and FTP transfers stream raw compressed text directly, minimizing network traffic and server CPU rendering overhead.

#### 12. Targeted Entrez Query Formulation (5 Marks)
* **Query String (2.5 Marks):**  
  `INS[GENE] AND "Homo sapiens"[ORGN] AND biomol_mrna[PROP] AND srcdb_refseq[PROP] AND 2018/01/01:2023/12/31[PDAT]`
* **Deconstruction of Terms (2.5 Marks):**  
  - `INS[GENE]`: Limits search to official gene symbol *INS*, excluding papers where insulin is merely discussed. (0.5)  
  - `"Homo sapiens"[ORGN]`: Restricts species scope to human. (0.5)  
  - `biomol_mrna[PROP]`: Restricts molecule type to mature mRNA, excluding genomic contigs. (0.5)  
  - `srcdb_refseq[PROP]`: Filters to curated RefSeq standard, excluding redundant primary GenBank clones. (0.5)  
  - `[PDAT]` range: Restricts publication dates strictly between Jan 1, 2018 and Dec 31, 2023. (0.5)

#### 13. The NCBI Data Model Hierarchy (5 Marks)
* **Hierarchical Structure (3.0 Marks):**  
  - `Bioseq-set`: Top-level container bundling collections (e.g., `nuc-prot` bundling nucleotide and translated proteins).  
  - `Bioseq`: Atomic sequence unit containing `id` (`Seq-id`), molecule type/length (`inst`), and descriptors (`descr`).  
  - `Seq-descr`: Global metadata descriptors (organism, title, publications) applying across the entire sequence.  
  - `Seq-annot`: Container holding tables of annotations.  
  - `Seq-feat`: Localized feature (e.g., `gene`, `CDS`, `variation`) anchored to specific coordinates via a `Seq-loc`.
* **Object Model vs Flat Files (2.0 Marks):** Flat files suffer from brittle text parsing (whitespace shifts, wrapped lines, missing delimiter errors). An abstract data model defines explicit data types and schemas (ASN.1/XML), allowing compiled software parsers to automatically validate records and extract sub-objects without regex errors.

#### 14. GenBank Feature Table Dissection (5 Marks)
* **`complement` Operator (1.5 Marks):** Indicates that the gene is encoded on the reverse-complement (minus) strand. Transcription and translation proceed in the $5' \rightarrow 3'$ direction of the opposite strand (from coordinate 850 down to 500, then 250 down to 100).
* **`join` Operator & Exons (1.5 Marks):** Indicates a spliced eukaryotic transcript consisting of **2 exons**. Exon 1 spans $500..850$ ($351\text{ bp}$) and Exon 2 spans $100..250$ ($151\text{ bp}$) on the negative strand.
* **Intervening Intron (2.0 Marks):** The non-coding intron between the two exons spans genomic coordinates $251..499$ ($499 - 251 + 1 = 249\text{ bp}$). Splicing excises this segment, joining the two coding segments into a mature $502\text{ bp}$ CDS.

#### 15. BLAST Heuristics & Search Artifacts (5 Marks)
* **Three Heuristic Phases (3.0 Marks):**  
  1. *Seeding:* Splits query into words of length $W$ ($W=3$ for blastp). Generates neighborhood words that score $\ge T$ using BLOSUM62. Scans database for exact seed matches via a hash table.  
  2. *Ungapped Extension:* Extends alignment in both directions without gaps until running score drops by $X$ below maximum score.  
  3. *Gapped Extension:* Triggers banded Smith–Waterman dynamic programming to join proximal HSPs into a final gapped alignment.
* **Low-Complexity Artifact & SEG Filtering (2.0 Marks):** Biased, repetitive segments (e.g., poly-proline tracts) align with high scores against unrelated proteins purely due to amino acid frequencies, generating spurious false-positive $E$-values. The SEG algorithm measures local Shannon entropy and masks low-complexity regions with 'X's, preventing spurious seed initiation.

---

### Section C: Numerical & Dynamic Programming Model Solutions (20 Marks)

#### 16. Needleman–Wunsch Global Alignment (10 Marks)
* **a) Initialization (2 Marks):**  
  $F(i,0) = -i \cdot d = -2 \cdot i \implies 0, -2, -4, -6, -8$  
  $F(0,j) = -j \cdot d = -2 \cdot j \implies 0, -2, -4, -6, -8$  
  *Formula:* $F(i,0) = -i \cdot d; \quad F(0,j) = -j \cdot d$.

* **b) Step-by-Step Matrix Cell Calculations (4 Marks):**  
  - **Cell (1,1) [$V, I$]:** Substitution $s(V,I) = +1$ (conservative).  
    $\text{Diag} = F(0,0) + 1 = 0 + 1 = \mathbf{+1}$.  
    $\text{Up} = F(0,1) - 2 = -2 - 2 = -4$; $\text{Left} = F(1,0) - 2 = -2 - 2 = -4$.  
    $F(1,1) = \max\{+1, -4, -4\} = \mathbf{+1}$ ($\nwse$).  
  - **Cell (1,2) [$V, A$]:** Mismatch $s(V,A) = -1$.  
    $\text{Diag} = F(0,1) - 1 = -2 - 1 = -3$.  
    $\text{Up} = F(0,2) - 2 = -4 - 2 = -6$; $\text{Left} = F(1,1) - 2 = 1 - 2 = \mathbf{-1}$.  
    $F(1,2) = \max\{-3, -6, -1\} = \mathbf{-1}$ ($\leftarrow$).  
  - **Cell (4,4) [$E, E$]:** Match $s(E,E) = +3$.  
    $F(3,3) = +7$ ($A,A$ and $L,L$ matches).  
    $\text{Diag} = F(3,3) + 3 = 7 + 3 = \mathbf{+10}$.  
    $\text{Up} = F(3,4) - 2 = 5 - 2 = 3$; $\text{Left} = F(4,3) - 2 = 5 - 2 = 3$.  
    $F(4,4) = \max\{+10, 3, 3\} = \mathbf{+10}$ ($\nwse$).

* **c) Populated Dynamic Programming Matrix (2 Marks):**  

```text
         -        I        A        L        E
   +--------+--------+--------+--------+--------+
 - |    0   |   -2   |   -4   |   -6   |   -8   |
   +--------+--------+--------+--------+--------+
 V |   -2   |   +1 ↖ |   -1 ← |   -3 ← |   -5 ← |
   +--------+--------+--------+--------+--------+
 A |   -4   |   -1 ↑ |   +4 ↖ |   +2 ← |    0 ← |
   +--------+--------+--------+--------+--------+
 L |   -6   |   -3 ↑ |   +2 ↑ |   +7 ↖ |   +5 ← |
   +--------+--------+--------+--------+--------+
 E |   -8   |   -5 ↑ |    0 ↑ |   +5 ↑ |  +10 ↖ |
   +--------+--------+--------+--------+--------+
```

* **d) Traceback, Optimal Alignment & Justification (2 Marks):**  
  - Traceback: $(4,4) \rightarrow (3,3) \rightarrow (2,2) \rightarrow (1,1) \rightarrow (0,0)$ along main diagonal.  
  - **Optimal Alignment:**  
    ```text
    Seq X:  V - A - L - E
            :   |   |   |
    Seq Y:  I - A - L - E
    Score:  +10
    ```  
  - *Justification:* Needleman–Wunsch initializes borders with gap penalties and forces traceback from the ultimate corner $(M,N)$ back to $(0,0)$, guaranteeing an end-to-end global alignment.

---

#### 17. Karlin–Altschul Statistics & BLAST Output Interpretation (10 Marks)
* **a) Mathematical Formulas (2 Marks):**  
  - Bit score: $S' = \frac{\lambda S - \ln K}{\ln 2}$  
  - $E$-value: $E = K \cdot m \cdot n \cdot e^{-\lambda S} = m \cdot n \cdot 2^{-S'}$

* **b) Bit Score Calculation (3 Marks):**  
  - Raw score $S = 180$, $\lambda = 0.267$, $K = 0.041$.  
  - $\lambda S = 0.267 \times 180 = \mathbf{48.06}$  
  - $\ln K = \ln(0.041) \approx \mathbf{-3.194}$  
  - $\lambda S - \ln K = 48.06 - (-3.194) = 48.06 + 3.194 = \mathbf{51.254}$  
  - $\ln 2 \approx 0.69315$  
  $$S' = \frac{51.254}{0.69315} \approx \mathbf{73.94\text{ bits}} \quad (\approx 74\text{ bits})$$

* **c) $E$-value Calculation and Biological Meaning (3 Marks):**  
  - Search space: $m = 300$, $n = 2 \times 10^8 \implies m \cdot n = 6 \times 10^{10}$.  
  - Using bit score: $2^{-73.94} \approx 5.66 \times 10^{-23}$.  
  - Alternatively: $E = K \cdot m \cdot n \cdot e^{-\lambda S} = 0.041 \times (6 \times 10^{10}) \times e^{-48.06}$  
    $e^{-48.06} \approx 1.34 \times 10^{-21}$  
    $$E = 2.46 \times 10^9 \times 1.34 \times 10^{-21} \approx \mathbf{3.3 \times 10^{-12}}$$  
  - *Biological Meaning:* In a database of 200 million residues, the expected number of random, non-homologous alignments achieving a score $\ge 180$ purely by chance is $3.3 \times 10^{-12}$ (effectively zero). This conclusively proves that the match is an authentic evolutionary homologue.

* **d) Database Rescaling & Invariance (2 Marks):**  
  - New database size: $n_{\text{new}} = 2 \times 10^5$ residues (a 1,000-fold reduction).  
  - Because $E \propto n$, the new $E$-value scales directly:  
    $$E_{\text{new}} = \frac{E_{\text{old}}}{1000} = \frac{3.3 \times 10^{-12}}{1000} = \mathbf{3.3 \times 10^{-15}}$$  
  - *Why Bit Score is Invariant:* Bit score ($S'$) is a normalized representation of raw alignment quality independent of database size ($S'$ depends strictly on score $S$ and matrix parameters $\lambda, K$). In contrast, $E$-value measures statistical significance relative to the total number of chance opportunities in the search space ($m \cdot n$).
