---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 14 Slides: Heuristic Algorithms: BLAST and FASTA"
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
# Lecture 14 — Heuristic Algorithms: BLAST and FASTA
### Concepts of Bioinformatics (CBBI-501)
**Unit 05:** Sequence Alignment and Database Searching  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Scaling Crisis in Database Searching

```text
Topic: Why Exact Dynamic Programming Cannot Keep Up

[Visual: Graph comparing Search Time vs Database Size:
  Smith-Waterman: O(m * n) --> Linear with database size, but constant factor is HUGE!
  Searching 1 query against NCBI nr (10^11 bases) requires ~10^14 DP operations.
  On a single CPU, Smith-Waterman would take days per search!]
```

**Speaker Talking Points:**  
* Modern biological repositories contain billions of sequences.
* We cannot afford full Dynamic Programming for every routine database query.
* Solution: **Heuristic Algorithms** that trade a tiny loss in theoretical sensitivity
  for a 500x to 1000x gain in execution speed.

---

## Slide 2: The Heuristic Philosophy: Seed and Extend

```text
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
```

**Speaker Talking Points:**  
* Both FASTA and BLAST are implementations of this fundamental heuristic philosophy.

---

## Slide 3: The FASTA Algorithm (Lipman & Pearson, 1985)

```text
Topic: The Predecessor to BLAST

[Visual: 4-Stage Architecture Diagram of FASTA:
  Stage 1: Hashing / k-tuples (ktup) -> Identify matching diagonals
  Stage 2: Score top 10 diagonals with matrix without gaps (init1 score)
  Stage 3: Join collinear diagonals with gap penalty (initn score)
  Stage 4: Banded Smith-Waterman around best diagonal (opt score)]
```

**Speaker Talking Points:**  
* FASTA uses a lookup table of short words called **k-tuples** (`ktup`):
  - `ktup = 2` for proteins.
  - `ktup = 6` for nucleic acids.
* Fast hash lookups pinpoint common diagonals; then localized DP refines the alignment.

---

## Slide 4: The BLAST Algorithm (Altschul et al., 1990)

```text
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
```

**Speaker Talking Points:**  
* BLAST was published in 1990 and remains one of the most cited papers in all of science.

---

## Slide 5: The Neighborhood Word Concept

```text
Topic: Why BLAST is More Sensitive than FASTA

  Query Word: `PQG` (Pro-Gln-Gly)
  Exact Match: `PQG` scores +16 (BLOSUM62)

  Neighborhood Words (Threshold T >= 13):
  * `PEG` (Pro-Glu-Gly) --> Score: 7 + 2 + 6 = 15  (QUALIFIES!)
  * `PRG` (Pro-Arg-Gly) --> Score: 7 + 1 + 6 = 14  (QUALIFIES!)
  * `PKG` (Pro-Lys-Gly) --> Score: 7 + 1 + 6 = 14  (QUALIFIES!)
  * `PAG` (Pro-Ala-Gly) --> Score: 7 - 1 + 6 = 12  (REJECTED: < 13)
```

**Speaker Talking Points:**  
* FASTA requires exact word matches. BLAST accepts *similar* words whose substitution
  score meets threshold $T$. This enables BLAST to detect distant homologs!

---

## Slide 6: Two-Hit Seed Extension & Gapped BLAST (1997)

```text
Topic: Innovations in BLAST 2.0

[Visual: Two-hit trigger diagram:
  Two non-overlapping neighborhood words hitting the SAME diagonal
  within a window of distance A (typically 40 residues) -> Trigger extension!]
```

**Speaker Talking Points:**  
* In 1997, Altschul introduced two major optimizations:
  1. **Two-Hit Seed Method:** Reduces time spent extending spurious single words by 75%.
  2. **Gapped BLAST:** Allows indels by triggering banded dynamic programming
     around high-scoring HSP pairs.

---

## Slide 7: The Five Classic Flavors of BLAST

```text
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
```

**Speaker Talking Points:**  
* Always search protein space whenever possible: protein alignments are far more
  sensitive than nucleotide alignments!

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 14

* Heuristics trade a fraction of sensitivity for 1000x computational speed.
* FASTA uses k-tuple hashing and diagonal joining.
* BLAST compiles neighborhood words (score >= T), finds seeds, and extends HSPs
  until score drops by X.
* Choose `blastp` for proteins, `blastx` for uncharacterized cDNAs, and `tblastn`
  for discovering unannotated genes.
* Next Lecture: BLAST Artifacts (Low-Complexity Masking) and PSSMs (PSI-BLAST).
```

