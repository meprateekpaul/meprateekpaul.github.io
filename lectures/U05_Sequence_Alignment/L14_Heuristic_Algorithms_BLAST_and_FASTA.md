# Lecture 14 — Heuristic Algorithms: BLAST and FASTA

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 5:** Sequence Alignment and Database Searching  
**Syllabus Topic:** Database similarity searching, FASTA, BLAST  
**Primary Learning Outcome:** LO3, LO4 — Run BLAST and FASTA searches, explain heuristic seed-and-extend mechanics, and select appropriate BLAST flavors.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Scaling Crisis in Database Searching
================================================================================
Topic: Why Exact Dynamic Programming Cannot Keep Up

[Visual: Graph comparing Search Time vs Database Size:
  Smith-Waterman: O(m * n) --> Linear with database size, but constant factor is HUGE!
  Searching 1 query against NCBI nr (10^11 bases) requires ~10^14 DP operations.
  On a single CPU, Smith-Waterman would take days per search!]

Speaker Bullets:
* Modern biological repositories contain billions of sequences.
* We cannot afford full Dynamic Programming for every routine database query.
* Solution: **Heuristic Algorithms** that trade a tiny loss in theoretical sensitivity
  for a 500x to 1000x gain in execution speed.
```

```
================================================================================
SLIDE 2: The Heuristic Philosophy: Seed and Extend
================================================================================
Topic: Exploiting the Biology of Homology

  Core Observation:
  Authentic biological homologs almost NEVER consist of completely uniform,
  low-level divergence spread evenly across the sequence.
  Instead, they contain short, highly conserved core islands ("seeds" or "words")
  flanked by more variable loop regions!

  Strategy:
  1. Rapidly find small, high-confidence exact or near-exact "seeds".
  2. Filter out 99.9% of the database that contains no matching seeds.
  3. Spend computational time extending alignments ONLY around verified seeds!

Speaker Bullets:
* Both FASTA and BLAST are implementations of this fundamental heuristic philosophy.
```

```
================================================================================
SLIDE 3: The FASTA Algorithm (Lipman & Pearson, 1985)
================================================================================
Topic: The Predecessor to BLAST

[Visual: 4-Stage Architecture Diagram of FASTA:
  Stage 1: Hashing / k-tuples (ktup) -> Identify matching diagonals
  Stage 2: Score top 10 diagonals with matrix without gaps (init1 score)
  Stage 3: Join collinear diagonals with gap penalty (initn score)
  Stage 4: Banded Smith-Waterman around best diagonal (opt score)]

Speaker Bullets:
* FASTA uses a lookup table of short words called **k-tuples** (`ktup`):
  - `ktup = 2` for proteins.
  - `ktup = 6` for nucleic acids.
* Fast hash lookups pinpoint common diagonals; then localized DP refines the alignment.
```

```
================================================================================
SLIDE 4: The BLAST Algorithm (Altschul et al., 1990)
================================================================================
Topic: Basic Local Alignment Search Tool

  BLAST's 3-Step Execution Pipeline:
  1. Compile Query Words & Neighborhood:
     * Break query into words of length W (W = 3 for protein).
     * Find all neighborhood words scoring >= T using BLOSUM62.
  2. Scan Database:
     * High-speed DFA (Deterministic Finite Automaton) scans database for hits.
  3. Extend Seeds:
     * Extend seed in both directions until score drops by X (Dropoff threshold).
     * Yields High-scoring Segment Pairs (HSPs).

Speaker Bullets:
* BLAST was published in 1990 and remains one of the most cited papers in all of science.
```

```
================================================================================
SLIDE 5: The Neighborhood Word Concept
================================================================================
Topic: Why BLAST is More Sensitive than FASTA

  Query Word: `PQG` (Pro-Gln-Gly)
  Exact Match: `PQG` scores +16 (BLOSUM62)

  Neighborhood Words (Threshold T >= 13):
  * `PEG` (Pro-Glu-Gly) --> Score: 7 + 2 + 6 = 15  (QUALIFIES!)
  * `PRG` (Pro-Arg-Gly) --> Score: 7 + 1 + 6 = 14  (QUALIFIES!)
  * `PKG` (Pro-Lys-Gly) --> Score: 7 + 1 + 6 = 14  (QUALIFIES!)
  * `PAG` (Pro-Ala-Gly) --> Score: 7 - 1 + 6 = 12  (REJECTED: < 13)

Speaker Bullets:
* FASTA requires exact word matches. BLAST accepts *similar* words whose substitution
  score meets threshold $T$. This enables BLAST to detect distant homologs!
```

```
================================================================================
SLIDE 6: Two-Hit Seed Extension & Gapped BLAST (1997)
================================================================================
Topic: Innovations in BLAST 2.0

[Visual: Two-hit trigger diagram:
  Two non-overlapping neighborhood words hitting the SAME diagonal
  within a window of distance A (typically 40 residues) -> Trigger extension!]

Speaker Bullets:
* In 1997, Altschul introduced two major optimizations:
  1. **Two-Hit Seed Method:** Reduces time spent extending spurious single words by 75%.
  2. **Gapped BLAST:** Allows indels by triggering banded dynamic programming
     around high-scoring HSP pairs.
```

```
================================================================================
SLIDE 7: The Five Classic Flavors of BLAST
================================================================================
Topic: Matching the Tool to Your Research Question

+----------+---------------+-------------------+------------------------------+
| Program  | Query Type    | Database Type     | Translation Frame & Use Case |
+----------+---------------+-------------------+------------------------------+
| `blastn` | Nucleotide    | Nucleotide        | None; identify identical DNA |
| `blastp` | Protein       | Protein           | None; protein homology/motif |
| `blastx` | Nucleotide    | Protein           | Query translated in 6 frames |
| `tblastn`| Protein       | Nucleotide        | Database in 6 frames         |
| `tblastx`| Nucleotide    | Nucleotide        | Both in 6 frames (36 combos!)|
+----------+---------------+-------------------+------------------------------+

Speaker Bullets:
* Always search protein space whenever possible: protein alignments are far more
  sensitive than nucleotide alignments!
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 14

* Heuristics trade a fraction of sensitivity for 1000x computational speed.
* FASTA uses k-tuple hashing and diagonal joining.
* BLAST compiles neighborhood words (score >= T), finds seeds, and extends HSPs
  until score drops by X.
* Choose `blastp` for proteins, `blastx` for uncharacterized cDNAs, and `tblastn`
  for discovering unannotated genes.
* Next Lecture: BLAST Artifacts (Low-Complexity Masking) and PSSMs (PSI-BLAST).
```

---

## Detailed Comprehensive Technical Notes

### 1. The Computational Scaling Problem

Exact dynamic programming algorithms (Smith-Waterman and Needleman-Wunsch) possess a computational time complexity of $\mathcal{O}(m \cdot n)$, where $m$ is the query sequence length and $n$ is the database size.

Consider a routine query:
- Query: Human beta-globin ($m = 147$ amino acids).
- Database: NCBI Non-Redundant Protein Database (`nr`), which exceeds $n \approx 1.5 \times 10^{11}$ residues.
- Number of dynamic programming cell updates required:
  $$m \cdot n = 147 \times (1.5 \times 10^{11}) \approx \mathbf{2.2 \times 10^{13}\text{ cell calculations}}$$
Even on modern multi-core server nodes computing $10^9$ DP matrix updates per second, a single search would consume over 6 hours of dedicated compute time. Because the NCBI web server processes hundreds of thousands of queries daily, exact dynamic programming is computationally infeasible for general database searching.

---

### 2. The FASTA Algorithm (Lipman & Pearson, 1985)

The first widely adopted heuristic sequence comparison tool was **FASTA** (FAST-All), developed by William Pearson and David Lipman.

#### The Four Stages of FASTA:
1. **Hashing and Diagonal Identification (Lookup Table):**  
   The query sequence is converted into a hash table of short words of fixed length $k$, called **k-tuples** (`ktup`):
   - For proteins: `ktup = 1` or `2` (default is 2).
   - For DNA: `ktup = 4` to `6` (default is 6).
   The algorithm rapidly scans the database using the hash index to locate matching words, calculating the offset (diagonal coordinate):
   $$\text{diagonal} = i - j$$
   where $i$ is the coordinate in sequence 1 and $j$ is the coordinate in sequence 2. Identical words on the same diagonal indicate regions of potential alignment.
2. **Rescoring the Best Diagonals (`init1`):**  
   The top 10 diagonal regions containing the highest density of matching k-tuples are rescored using an amino acid substitution matrix (such as BLOSUM50 or PAM250) **without allowing gaps**. Sub-segments that score poorly are trimmed to produce the `init1` score.
3. **Joining Diagonals with Gap Penalties (`initn`):**  
   The algorithm checks whether multiple high-scoring ungapped diagonal segments can be joined together in collinear order (increasing coordinates). If joining them—after subtracting an intervening gap penalty—yields a higher combined score, they are merged to produce the `initn` score.
4. **Band-Limited Smith-Waterman Optimization (`opt`):**  
   Around the highest-scoring diagonal region, FASTA constructs a narrow, band-limited corridor (typically 32 residues wide) and executes full Smith-Waterman dynamic programming within that band to generate the final `opt` score.

---

### 3. The BLAST Algorithm (Altschul et al., 1990)

The **Basic Local Alignment Search Tool (BLAST)** revolutionized computational biology by introducing a probabilistic word-neighborhood approach that eliminated the need for exact word matches.

#### The Three Core Steps of BLAST:

```
  Step 1: Word Generation & Neighborhood List
          Query: ... V H L T P E E K S ...
          Query 3-mer: "HLT"
          Find all 3-mers in 20^3 space scoring >= T against "HLT" (BLOSUM62)
          Neighborhood list: { HLT (16), HMT (13), HIT (13), HVT (13) ... }
             |
             v
  Step 2: Database Scanning (DFA Engine)
          Scan target database using a Deterministic Finite Automaton (Aho-Corasick tree)
          Instantaneously detect occurrences of any neighborhood word in the database
             |
             v
  Step 3: Two-Hit Trigger & Extension (HSP Generation)
          When two neighborhood hits occur on the same diagonal within distance A (40 aa),
          trigger bidirectional extension!
          Extend without gaps until score drops by X below the peak score achieved.
          Yields High-scoring Segment Pair (HSP).
```

#### Key BLAST Parameters:
- **Word Size ($W$):** The length of the sliding seed window. For proteins, $W = 3$; for nucleotides, $W = 11$ (or $28$ in Megablast).
- **Threshold Score ($T$):** The minimum BLOSUM62 score required for a 3-mer to enter the neighborhood word list. Lowering $T$ increases the size of the neighborhood, increasing sensitivity at the expense of search speed.
- **Dropoff Score ($X$):** The stopping condition during seed extension. As an HSP extends through divergent residues, the running score fluctuates. If the score falls by more than $X$ below the highest running score achieved so far ($\text{Score} < \text{MaxScore} - X$), extension terminates immediately.

---

### 4. The Five Classic BLAST Flavors

```
  Program Name   Query Type     Database Type  Internal Translation Mechanics
  -------------------------------------------------------------------------------------------------
  blastn         Nucleotide     Nucleotide     No translation. Compares nucleotide words directly.
                                               Used for mapping PCR primers, checking vector tags,
                                               and cross-checking identical species genomic DNA.
  blastp         Protein        Protein        No translation. Compares amino acid words using 
                                               BLOSUM62. The gold standard for identifying homologs.
  blastx         Nucleotide     Protein        Translates the nucleotide query conceptually in all 
                                               6 reading frames (+1, +2, +3, -1, -2, -3) and compares
                                               each against the protein database. Ideal for newly 
                                               sequenced cDNAs or identifying protein-coding genes.
  tblastn        Protein        Nucleotide     Translates the entire nucleotide database conceptually 
                                               in all 6 reading frames and compares the protein query 
                                               against each translated frame. Used to discover novel 
                                               unannotated genes in newly assembled raw contigs.
  tblastx        Nucleotide     Nucleotide     Translates the nucleotide query in all 6 frames AND 
                                               translates the nucleotide database in all 6 frames 
                                               (36 simultaneous comparisons!). Extremely compute-
                                               intensive; used to detect distant evolutionary 
                                               relationships between diverged RNA/DNA genomes.
```

---

## Worked Example: Calculating a BLAST Neighborhood Word List

### Problem:
Given the tripeptide query word **`VHL`** (the first three residues of the human beta-globin mature peptide), calculate its exact match score and determine which of the following candidate variants qualify for the BLASTP neighborhood list using the **BLOSUM62** scoring matrix with a threshold threshold **$T = 13$**:
1. Candidate 1: `V H L` (Exact Match)
2. Candidate 2: `V H M` (Val - His - Met)
3. Candidate 3: `I H L` (Ile - His - Leu)
4. Candidate 4: `V H I` (Val - His - Ile)
5. Candidate 5: `V R L` (Val - Arg - Leu)
6. Candidate 6: `A H L` (Ala - His - Leu)

### BLOSUM62 Values Required:
- $s(V, V) = +4, \quad s(V, I) = +3, \quad s(V, A) = 0$
- $s(H, H) = +8, \quad s(H, R) = 0$
- $s(L, L) = +4, \quad s(L, M) = +2, \quad s(L, I) = +2$

---

### Step-by-Step Scoring Calculations:

1. **Candidate 1: `V H L` (Exact Match)**
   $$\text{Score} = s(V, V) + s(H, H) + s(L, L) = 4 + 8 + 4 = \mathbf{16}$$
   - Evaluation: $16 \ge 13 \implies$ **QUALIFIES (Enters Neighborhood List)**

2. **Candidate 2: `V H M`**
   $$\text{Score} = s(V, V) + s(H, H) + s(L, M) = 4 + 8 + 2 = \mathbf{14}$$
   - Evaluation: $14 \ge 13 \implies$ **QUALIFIES (Enters Neighborhood List)**

3. **Candidate 3: `I H L`**
   $$\text{Score} = s(V, I) + s(H, H) + s(L, L) = 3 + 8 + 4 = \mathbf{15}$$
   - Evaluation: $15 \ge 13 \implies$ **QUALIFIES (Enters Neighborhood List)**

4. **Candidate 4: `V H I`**
   $$\text{Score} = s(V, V) + s(H, H) + s(L, I) = 4 + 8 + 2 = \mathbf{14}$$
   - Evaluation: $14 \ge 13 \implies$ **QUALIFIES (Enters Neighborhood List)**

5. **Candidate 5: `V R L`**
   $$\text{Score} = s(V, V) + s(H, R) + s(L, L) = 4 + 0 + 4 = \mathbf{8}$$
   - Evaluation: $8 < 13 \implies$ **REJECTED (Score below threshold $T$)**

6. **Candidate 6: `A H L`**
   $$\text{Score} = s(V, A) + s(H, H) + s(L, L) = 0 + 8 + 4 = \mathbf{12}$$
   - Evaluation: $12 < 13 \implies$ **REJECTED (Score below threshold $T$)**

### Summary:
The neighborhood for `VHL` at $T=13$ contains `VHL`, `IHL`, `VHM`, and `VHI`. When BLAST scans the database, encountering any one of these four words triggers a potential seed hit on that diagonal!

---

## Formative In-Class Checks

### Question 1
**Prompt:** A researcher isolates an unannotated genomic DNA contig from a newly discovered deep-sea archaebacterium and suspects it contains an uncharacterized DNA polymerase. They have the purified protein sequence of a known bacterial DNA polymerase. Which BLAST program should they run against their unannotated DNA contig? Explain why.

**Model Answer:**
The researcher should run **`tblastn`**.
- The query is a known **protein sequence**, while the database/target is an **unannotated genomic nucleotide contig**.
- `tblastn` translates the nucleotide contig into all six reading frames (+1, +2, +3, -1, -2, -3) and searches the protein query against all six translations.
- This allows the software to identify the homologous polymerase gene directly from raw DNA, even if the open reading frame has not yet been annotated or contains non-standard prokaryotic start codons.

---

### Question 2
**Prompt:** In BLASTP, what is the consequence of decreasing the neighborhood word threshold parameter from $T = 13$ to $T = 9$? Describe the effect on both computational runtime and search sensitivity.

**Model Answer:**
- **Search Sensitivity:** Sensitivity will **increase significantly**. A lower threshold of $T=9$ allows many more divergent, weakly conserved tripeptides into the neighborhood list, enabling BLAST to detect more distant evolutionary homologs.
- **Computational Runtime:** Runtime will **increase dramatically (search will become much slower)**. Lowering $T$ causes an exponential expansion in the number of neighborhood words, producing millions of spurious seed matches in the database that force the algorithm to spend excessive time executing costly bidirectional seed extensions.

---

### Question 3
**Prompt:** Explain the architectural difference between FASTA's word-matching mechanism and BLAST's word-matching mechanism. Why does this make BLAST more sensitive for protein searching?

**Model Answer:**
- **FASTA** relies on **exact k-tuple identity matches** (e.g., a 2-mer in the query must match an identical 2-mer in the database character-for-character) to identify diagonals.
- **BLAST** uses a **probabilistic scoring neighborhood**: it pre-computes all words in the entire amino acid dictionary that achieve a substitution score $\ge T$ against the query word using BLOSUM62.
- **Why BLAST is more sensitive:** Authentic homologous proteins frequently diverge via conservative substitutions (e.g. `Val` to `Ile` or `Asp` to `Glu`) without sharing any exact multi-residue identities. FASTA completely misses these regions in its initial hash pass, whereas BLAST captures them through its substitution-weighted neighborhood list.
