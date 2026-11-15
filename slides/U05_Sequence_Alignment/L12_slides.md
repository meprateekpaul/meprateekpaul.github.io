---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 12 Slides: Smith-Waterman Local Alignment"
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
# Lecture 12 — Smith-Waterman Local Alignment
### Concepts of Bioinformatics (CBBI-501)
**Unit 05:** Sequence Alignment and Database Searching  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Failure of Global Alignment in Modular Biology

```text
Topic: Why End-to-End Alignment Breaks Down

[Visual: Multidomain protein diagram:
  Protein 1: [Signal Peptide]--[SH2 Domain]--[Kinase Domain]--[Tail]
  Protein 2: [Transmembrane]-----------------[Kinase Domain]--[C-term]
  Global Alignment tries to force non-homologous flanking regions to align!
  Result: Hundreds of negative gap penalties overwhelm the conserved Kinase score!]
```

**Speaker Talking Points:**  
* Proteins are modular: domains are shuffled, duplicated, and recombined.
* Global alignment (Needleman-Wunsch) assumes sequences are homologous end-to-end.
* When comparing multidomain proteins or raw genomic DNA, we need an algorithm
  that ignores non-homologous flanks and isolates strictly conserved internal motifs.

---

## Slide 2: The Smith-Waterman Paradigm (1981)

```text
Topic: Temple Smith & Michael Waterman's Breakthrough

  The Two Fundamental Innovations of Smith-Waterman:
  1. The "Zero Floor": Alignment scores are never allowed to become negative.
     If an alignment accumulates negative score, it is terminated and restarted at 0.
  2. Flexible Start and End: The optimal local alignment can start anywhere
     and terminate anywhere within the two sequences.
```

**Speaker Talking Points:**  
* Published in 1981 in the *Journal of Molecular Biology*.
* Guaranteed to find the mathematically optimal local alignment between two sequences.

---

## Slide 3: The Local Recurrence Relation

```text
Topic: The Four-Way Maximum Function

  F(i, j) = MAX of:
    1.  0                          <-- THE ZERO FLOOR (Reset condition)
    2.  F(i-1, j-1) + s(x_i, y_j)  [Diagonal: match/mismatch]
    3.  F(i-1, j)   - d            [Vertical: gap in sequence Y]
    4.  F(i, j-1)   - d            [Horizontal: gap in sequence X]
```

**Speaker Talking Points:**  
* The addition of '0' as a choice prevents poor alignments from propagating.
* If all three incoming routes produce negative numbers, the cell is assigned 0.
* A cell of value 0 has NO traceback pointer (it represents an alignment boundary).

---

## Slide 4: Boundary Conditions and Initialization

```text
Topic: Edges are All ZEROS

              j=0       j=1 (y_1)   j=2 (y_2)   j=3 (y_3)
              [-]
  i=0 [-]      0           0           0           0
  i=1 (x_1)    0
  i=2 (x_2)    0
  i=3 (x_3)    0
```

**Speaker Talking Points:**  
* Compare with Needleman-Wunsch: no negative gap penalties on the boundary!
* An alignment can begin at any interior residue (i, j) without paying a penalty
  for preceding unaligned characters.

---

## Slide 5: The Local Traceback Protocol

```text
Topic: How to Reconstruct the Alignment

  Rule 1: START at the MAXIMUM score anywhere in the entire matrix F!
          (Do NOT start at bottom-right cell F(m, n) unless it happens to be max!)

  Rule 2: Follow pointer arrows backwards (Diagonal, Up, Left).

  Rule 3: STOP IMMEDIATELY when you reach a cell with value ZERO (0)!
```

**Speaker Talking Points:**  
* The starting cell determines the C-terminal end of the local alignment.
* Reaching 0 marks the N-terminal boundary where the local match begins.

---

## Slide 6: Gap Penalty Models: Linear vs Affine

```text
Topic: Gotoh's Affine Gap Penalty Model (1982)

  Linear Gap Penalty:
    W(k) = k * d                      [Every gap position penalized equally: -d]

  Affine Gap Penalty:
    W(k) = d + (k - 1) * e            [d = Gap Opening; e = Gap Extension]
    Rule: d >> e                      (Opening penalty is MUCH larger than extension!)

  Example (d = 11, e = 1):
    1 gap:   11 + (0 * 1) = 11
    2 gaps:  11 + (1 * 1) = 12  (Only +1 for the second gap!)
    3 gaps:  11 + (2 * 1) = 13
```

**Speaker Talking Points:**  
* Biological rationale: Opening an indel requires an enzymatic break (rare event).
  Extending an existing indel by extra bases is much more frequent during slippage.

---

## Slide 7: Global vs Local Alignment Decision Tree

```text
Topic: Which Algorithm to Choose?

+--------------------+-------------------------+------------------------------+
| Criterion          | Needleman-Wunsch (Global)| Smith-Waterman (Local)       |
+--------------------+-------------------------+------------------------------+
| Best For           | Closely related proteins| Distant homologs, domains,   |
|                    | of similar length       | chimeric or genomic reads    |
| Edge Initialisation| -i * d, -j * d          | All zeros                    |
| Recurrence Choices | 3 routes (Diag, Up, Left)| 4 routes (0, Diag, Up, Left) |
| Traceback Start    | Bottom-right F(m, n)    | Highest value in matrix      |
| Traceback End      | Top-left F(0, 0)        | First cell with value 0      |
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* If you suspect homologous domains embedded in non-homologous sequence: use Local!

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 12

* Smith-Waterman isolates optimal local sub-alignments using the 0-floor threshold.
* Traceback starts at the global maximum score and terminates at zero.
* Affine gap penalties (d + (k-1)e) reflect the biophysical reality of indels.
* Next Lecture: Scoring Matrices (PAM & BLOSUM) and Statistical Significance (E-values).
```

