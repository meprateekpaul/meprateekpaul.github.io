---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 11 Slides: Needleman-Wunsch Global Alignment"
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
# Lecture 11 — Needleman-Wunsch Global Alignment
### Concepts of Bioinformatics (CBBI-501)
**Unit 05:** Sequence Alignment and Database Searching  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Alignment Combinatorial Explosion

```text
Topic: Why Brute Force Search is Impossible

[Visual: Graph of number of possible alignments vs sequence length
         n = 100 sequences -> 10^75 possible alignments (more than atoms in universe!)]

Formula:
  Number of alignments for length n ≈ (4^n) / sqrt(pi * n)
```

**Speaker Talking Points:**  
* We cannot simply test every possible way to place dashes and letters.
* For two typical proteins of length 300, the search space is astronomical.
* We require an algorithm that guarantees finding the mathematically optimal
  alignment in polynomial time.

---

## Slide 2: Dynamic Programming Foundations

```text
Topic: Richard Bellman's Principle of Optimality (1957)

[Visual: Breaking a big path problem into overlapping sub-paths:
  Optimal path to (i, j) MUST be composed of an optimal path to one of its
  predecessors: (i-1, j-1), (i-1, j), or (i, j-1)]
```

**Speaker Talking Points:**  
* Dynamic Programming (DP) solves complex problems by breaking them into overlapping
  sub-problems, solving each sub-problem once, and memoizing (storing) the solutions.
* In 1970, Saul Needleman and Christian Wunsch applied DP to molecular biology,
  creating the **Needleman-Wunsch Global Alignment Algorithm**.

---

## Slide 3: The Needleman-Wunsch Algorithm: Three Phases

```text
Topic: The Lifecycle of Global DP Alignment

  Phase 1: Initialization
  * Construct a matrix F of dimensions (m + 1) x (n + 1).
  * Fill the 0th row and 0th column with cumulative gap penalties (-i * d, -j * d).

  Phase 2: Matrix Fill (Recurrence)
  * Calculate each cell F(i, j) by taking the MAXIMUM of three incoming routes.
  * Store pointer arrow(s) showing which route produced the maximum.

  Phase 3: Traceback
  * Start at the bottom-right cell F(m, n).
  * Follow arrows back to the origin F(0, 0) to reconstruct the optimal alignment.
```

**Speaker Talking Points:**  
* Every cell represents the optimal alignment score of prefix X[1..i] and Y[1..j].

---

## Slide 4: The Core Recurrence Relation

```text
Topic: The Engine of Matrix Fill

                     +------------------+
                     | F(i-1, j-1)      |  F(i-1, j) [Up]
                     | [Diagonal]       |  Gap in Y: -d
                     +--------+---------+-------+
                              |                 |
                              | +s(x_i, y_j)    |
                              v                 v
  F(i, j-1) [Left]  -----> +--------------------+
  Gap in X: -d             |      F(i, j)       |
                           +--------------------+

  F(i, j) = MAX of:
    1. F(i-1, j-1) + s(x_i, y_j)   [Diagonal: match/mismatch]
    2. F(i-1, j)   - d             [Vertical: gap in sequence Y]
    3. F(i, j-1)   - d             [Horizontal: gap in sequence X]
```

**Speaker Talking Points:**  
* s(x_i, y_j) is the substitution score (from a matrix or identity rule).
* d is the linear gap penalty.

---

## Slide 5: Initialization Mechanics

```text
Topic: Why Edges Have Negative Multiples of d

              j=0       j=1 (y_1)   j=2 (y_2)   j=3 (y_3)
              [-]
  i=0 [-]      0          -d         -2d         -3d
  i=1 (x_1)   -d
  i=2 (x_2)  -2d
  i=3 (x_3)  -3d
```

**Speaker Talking Points:**  
* Global alignment requires aligning EVERY residue from end to end.
* Aligning x_1..x_i against an empty sequence requires opening i gaps: score = -i * d.
* This forms the immutable boundary condition of the global alignment problem.

---

## Slide 6: The Traceback Mechanism

```text
Topic: Reconstructing the Character Strings

+--------------------+-------------------------+------------------------------+
| Pointer Direction  | Character Assignment    | Alignment Action             |
+--------------------+-------------------------+------------------------------+
| Diagonal (\nwarrow)| Align x_i with y_j      | Conserved residue or mutate  |
| Up (\uparrow)      | Align x_i with gap '-'  | Deletion in Y / Insert in X  |
| Left (\leftarrow)  | Align gap '-' with y_j  | Insertion in Y / Delete in X |
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* Traceback MUST start at the terminal cell F(m, n) and end at F(0, 0).
* If a cell has two arrows, a "tie" exists: both paths yield identical optimal scores.

---

## Slide 7: Algorithmic Complexity: Time & Space

```text
Topic: Computational Performance

+--------------------+-------------------------+------------------------------+
| Resource           | Standard Needleman-W    | Hirschberg Optimization      |
+--------------------+-------------------------+------------------------------+
| Time Complexity    | O(m * n)                | O(m * n)                     |
| Space (Memory)     | O(m * n)                | O(min(m, n))                 |
+--------------------+-------------------------+------------------------------+
```

**Speaker Talking Points:**  
* Filling an (m x n) table requires computing 3 additions and a max per cell: O(mn).
* For two 10,000-bp sequences, m * n = 10^8 cells (~400 MB of RAM).
* Hirschberg's divide-and-conquer algorithm reduces memory to linear space O(n).

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 11

* Needleman-Wunsch solves global end-to-end alignment using Dynamic Programming.
* Matrix fill uses recurrence: Max(Diagonal + score, Up - gap, Left - gap).
* Boundary conditions are cumulative negative gap penalties.
* Traceback guarantees finding the mathematically optimal alignment.
* Next Lecture: Smith-Waterman Local Alignment — Finding conserved domains and
  the zero-floor threshold!
```

