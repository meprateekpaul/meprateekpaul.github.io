# Lecture 11 — Needleman-Wunsch Global Alignment

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 5:** Sequence Alignment and Database Searching  
**Syllabus Topic:** Optimal alignment method, Substitution Score and Gap Penalty  
**Primary Learning Outcome:** LO3 — Explain global, local, and heuristic alignment, and compute optimal dynamic programming matrices by hand.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Alignment Combinatorial Explosion
================================================================================
Topic: Why Brute Force Search is Impossible

[Visual: Graph of number of possible alignments vs sequence length
         n = 100 sequences -> 10^75 possible alignments (more than atoms in universe!)]

Formula:
  Number of alignments for length n ≈ (4^n) / sqrt(pi * n)

Speaker Bullets:
* We cannot simply test every possible way to place dashes and letters.
* For two typical proteins of length 300, the search space is astronomical.
* We require an algorithm that guarantees finding the mathematically optimal
  alignment in polynomial time.
```

```
================================================================================
SLIDE 2: Dynamic Programming Foundations
================================================================================
Topic: Richard Bellman's Principle of Optimality (1957)

[Visual: Breaking a big path problem into overlapping sub-paths:
  Optimal path to (i, j) MUST be composed of an optimal path to one of its
  predecessors: (i-1, j-1), (i-1, j), or (i, j-1)]

Speaker Bullets:
* Dynamic Programming (DP) solves complex problems by breaking them into overlapping
  sub-problems, solving each sub-problem once, and memoizing (storing) the solutions.
* In 1970, Saul Needleman and Christian Wunsch applied DP to molecular biology,
  creating the **Needleman-Wunsch Global Alignment Algorithm**.
```

```
================================================================================
SLIDE 3: The Needleman-Wunsch Algorithm: Three Phases
================================================================================
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

Speaker Bullets:
* Every cell represents the optimal alignment score of prefix X[1..i] and Y[1..j].
```

```
================================================================================
SLIDE 4: The Core Recurrence Relation
================================================================================
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

Speaker Bullets:
* s(x_i, y_j) is the substitution score (from a matrix or identity rule).
* d is the linear gap penalty.
```

```
================================================================================
SLIDE 5: Initialization Mechanics
================================================================================
Topic: Why Edges Have Negative Multiples of d

              j=0       j=1 (y_1)   j=2 (y_2)   j=3 (y_3)
              [-]
  i=0 [-]      0          -d         -2d         -3d
  i=1 (x_1)   -d
  i=2 (x_2)  -2d
  i=3 (x_3)  -3d

Speaker Bullets:
* Global alignment requires aligning EVERY residue from end to end.
* Aligning x_1..x_i against an empty sequence requires opening i gaps: score = -i * d.
* This forms the immutable boundary condition of the global alignment problem.
```

```
================================================================================
SLIDE 6: The Traceback Mechanism
================================================================================
Topic: Reconstructing the Character Strings

+--------------------+-------------------------+------------------------------+
| Pointer Direction  | Character Assignment    | Alignment Action             |
+--------------------+-------------------------+------------------------------+
| Diagonal (\nwarrow)| Align x_i with y_j      | Conserved residue or mutate  |
| Up (\uparrow)      | Align x_i with gap '-'  | Deletion in Y / Insert in X  |
| Left (\leftarrow)  | Align gap '-' with y_j  | Insertion in Y / Delete in X |
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* Traceback MUST start at the terminal cell F(m, n) and end at F(0, 0).
* If a cell has two arrows, a "tie" exists: both paths yield identical optimal scores.
```

```
================================================================================
SLIDE 7: Algorithmic Complexity: Time & Space
================================================================================
Topic: Computational Performance

+--------------------+-------------------------+------------------------------+
| Resource           | Standard Needleman-W    | Hirschberg Optimization      |
+--------------------+-------------------------+------------------------------+
| Time Complexity    | O(m * n)                | O(m * n)                     |
| Space (Memory)     | O(m * n)                | O(min(m, n))                 |
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* Filling an (m x n) table requires computing 3 additions and a max per cell: O(mn).
* For two 10,000-bp sequences, m * n = 10^8 cells (~400 MB of RAM).
* Hirschberg's divide-and-conquer algorithm reduces memory to linear space O(n).
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 11

* Needleman-Wunsch solves global end-to-end alignment using Dynamic Programming.
* Matrix fill uses recurrence: Max(Diagonal + score, Up - gap, Left - gap).
* Boundary conditions are cumulative negative gap penalties.
* Traceback guarantees finding the mathematically optimal alignment.
* Next Lecture: Smith-Waterman Local Alignment — Finding conserved domains and
  the zero-floor threshold!
```

---

## Detailed Comprehensive Technical Notes

### 1. The Needleman-Wunsch Algorithmic Formulation

Published in 1970 by Saul B. Needleman and Christian D. Wunsch, this algorithm was the first application of dynamic programming to macromolecular sequence comparison. 

**Problem Statement:**  
Given two sequences $X = x_1 x_2 \dots x_m$ of length $m$ and $Y = y_1 y_2 \dots y_n$ of length $n$ over an alphabet $\Sigma$, find an alignment that maximizes the total alignment score, defined as the sum of substitution scores minus gap penalties:

$$\text{Score} = \sum_{k} s(x_k', y_k')$$

where $x_k', y_k' \in \Sigma \cup \{-\}$ and $(x_k', y_k') \neq (-, -)$.

---

### 2. The Three Algorithmic Stages

#### Stage 1: Matrix Initialization
A dynamic programming table $F$ of size $(m+1) \times (n+1)$ is initialized. The coordinate indices are $i \in \{0, 1, \dots, m\}$ and $j \in \{0, 1, \dots, n\}$:
- Cell $F(0,0) = 0$ (aligning two empty sequences costs nothing).
- The 0th row represents aligning prefix $Y[1..j]$ against $j$ leading gaps:
  $$F(0, j) = -j \cdot d \quad \text{for } j = 1, 2, \dots, n$$
- The 0th column represents aligning prefix $X[1..i]$ against $i$ leading gaps:
  $$F(i, 0) = -i \cdot d \quad \text{for } i = 1, 2, \dots, m$$

#### Stage 2: Matrix Fill (Recurrence Relation)
Cells are computed row by row (or column by column) from top-left to bottom-right. For every cell $F(i, j)$:

$$F(i, j) = \max \begin{cases}
F(i-1, j-1) + s(x_i, y_j) & \text{[Diagonal: align residue } x_i \text{ with residue } y_j\text{]} \\
F(i-1, j) - d & \text{[Up: align residue } x_i \text{ with a gap } \text{'-' in sequence } Y\text{]} \\
F(i, j-1) - d & \text{[Left: align a gap } \text{'-' in sequence } X \text{ with residue } y_j\text{]}
\end{cases}$$

During computation, a **pointer array** (or backtracking matrix) $T(i, j)$ records the direction(s) that achieved the maximum:
- $\nwarrow$ (Diagonal)
- $\uparrow$ (Up)
- $\leftarrow$ (Left)

#### Stage 3: Traceback
1. Traceback begins strictly at the bottom-right terminal cell: **$F(m, n)$**.
2. Follow pointer arrows backwards:
   - If pointer is $\nwarrow$: append $x_i$ to aligned $X$, append $y_j$ to aligned $Y$, decrement $i \gets i-1$, $j \gets j-1$.
   - If pointer is $\uparrow$: append $x_i$ to aligned $X$, append `'-'` to aligned $Y$, decrement $i \gets i-1$.
   - If pointer is $\leftarrow$: append `'-'` to aligned $X$, append $y_j$ to aligned $Y$, decrement $j \gets j-1$.
3. Traceback terminates when cell **$F(0, 0)$** is reached.
4. Reverse the accumulated strings to produce the final optimal global alignment.

---

## Worked Mathematical Example: Step-by-Step Hand Calculation

Let us calculate the complete dynamic programming matrix by hand for two peptide fragments related to the beta-globin chain:
- **Sequence $X$ (Rows):** `V H L T P` ($m = 5$)
- **Sequence $Y$ (Columns):** `V H T P` ($n = 4$)

### Scoring Parameters:
- **Match score:** $s(a, a) = \mathbf{+2}$
- **Mismatch score:** $s(a, b) = \mathbf{-1}$
- **Linear gap penalty:** $d = \mathbf{2}$ (subtracted as $-2$)

---

### Step 1: Matrix Initialization ($6 \times 5$ Table)
The 0th row is filled with multiples of $-2$: $[0, -2, -4, -6, -8]$.  
The 0th column is filled with multiples of $-2$: $[0, -2, -4, -6, -8, -10]$.

```
          [-]     V (j=1)   H (j=2)   T (j=3)   P (j=4)
  [-]      0        -2        -4        -6        -8
  V (i=1) -2
  H (i=2) -4
  L (i=3) -6
  T (i=4) -8
  P (i=5)-10
```

---

### Step 2: Step-by-Step Cell Calculations

#### Row 1 ($x_1 = \text{'V'}$):
- **Cell (1, 1) [$y_1 = \text{'V'}$]:** Match ($+2$)
  - Diag: $F(0,0) + s(V,V) = 0 + 2 = \mathbf{2}$
  - Up: $F(0,1) - 2 = -2 - 2 = -4$
  - Left: $F(1,0) - 2 = -2 - 2 = -4$
  - $\max = \mathbf{2}$ (Pointer: $\nwarrow$)
- **Cell (1, 2) [$y_2 = \text{'H'}$]:** Mismatch ($-1$)
  - Diag: $F(0,1) + s(V,H) = -2 - 1 = -3$
  - Up: $F(0,2) - 2 = -4 - 2 = -6$
  - Left: $F(1,1) - 2 = 2 - 2 = \mathbf{0}$
  - $\max = \mathbf{0}$ (Pointer: $\leftarrow$)
- **Cell (1, 3) [$y_3 = \text{'T'}$]:** Mismatch ($-1$)
  - Diag: $F(0,2) - 1 = -4 - 1 = -5$
  - Up: $F(0,3) - 2 = -6 - 2 = -8$
  - Left: $F(1,2) - 2 = 0 - 2 = \mathbf{-2}$
  - $\max = \mathbf{-2}$ (Pointer: $\leftarrow$)
- **Cell (1, 4) [$y_4 = \text{'P'}$]:** Mismatch ($-1$)
  - Diag: $F(0,3) - 1 = -6 - 1 = -7$
  - Up: $F(0,4) - 2 = -8 - 2 = -10$
  - Left: $F(1,3) - 2 = -2 - 2 = \mathbf{-4}$
  - $\max = \mathbf{-4}$ (Pointer: $\leftarrow$)

#### Row 2 ($x_2 = \text{'H'}$):
- **Cell (2, 1) [$y_1 = \text{'V'}$]:** Mismatch ($-1$)
  - Diag: $F(1,0) - 1 = -2 - 1 = -3$
  - Up: $F(1,1) - 2 = 2 - 2 = \mathbf{0}$
  - Left: $F(2,0) - 2 = -4 - 2 = -6$
  - $\max = \mathbf{0}$ (Pointer: $\uparrow$)
- **Cell (2, 2) [$y_2 = \text{'H'}$]:** Match ($+2$)
  - Diag: $F(1,1) + 2 = 2 + 2 = \mathbf{4}$
  - Up: $F(1,2) - 2 = 0 - 2 = -2$
  - Left: $F(2,1) - 2 = 0 - 2 = -2$
  - $\max = \mathbf{4}$ (Pointer: $\nwarrow$)
- **Cell (2, 3) [$y_3 = \text{'T'}$]:** Mismatch ($-1$)
  - Diag: $F(1,2) - 1 = 0 - 1 = -1$
  - Up: $F(1,3) - 2 = -2 - 2 = -4$
  - Left: $F(2,2) - 2 = 4 - 2 = \mathbf{2}$
  - $\max = \mathbf{2}$ (Pointer: $\leftarrow$)
- **Cell (2, 4) [$y_4 = \text{'P'}$]:** Mismatch ($-1$)
  - Diag: $F(1,3) - 1 = -2 - 1 = -3$
  - Up: $F(1,4) - 2 = -4 - 2 = -6$
  - Left: $F(2,3) - 2 = 2 - 2 = \mathbf{0}$
  - $\max = \mathbf{0}$ (Pointer: $\leftarrow$)

#### Row 3 ($x_3 = \text{'L'}$):
- **Cell (3, 1) [$y_1 = \text{'V'}$]:** Mismatch ($-1$)
  - Diag: $F(2,0) - 1 = -4 - 1 = -5$
  - Up: $F(2,1) - 2 = 0 - 2 = \mathbf{-2}$
  - Left: $F(3,0) - 2 = -6 - 2 = -8$
  - $\max = \mathbf{-2}$ (Pointer: $\uparrow$)
- **Cell (3, 2) [$y_2 = \text{'H'}$]:** Mismatch ($-1$)
  - Diag: $F(2,1) - 1 = 0 - 1 = -1$
  - Up: $F(2,2) - 2 = 4 - 2 = \mathbf{2}$
  - Left: $F(3,1) - 2 = -2 - 2 = -4$
  - $\max = \mathbf{2}$ (Pointer: $\uparrow$)
- **Cell (3, 3) [$y_3 = \text{'T'}$]:** Mismatch ($-1$)
  - Diag: $F(2,2) - 1 = 4 - 1 = \mathbf{3}$
  - Up: $F(2,3) - 2 = 2 - 2 = 0$
  - Left: $F(3,2) - 2 = 2 - 2 = 0$
  - $\max = \mathbf{3}$ (Pointer: $\nwarrow$)
- **Cell (3, 4) [$y_4 = \text{'P'}$]:** Mismatch ($-1$)
  - Diag: $F(2,3) - 1 = 2 - 1 = \mathbf{1}$
  - Up: $F(2,4) - 2 = 0 - 2 = -2$
  - Left: $F(3,3) - 2 = 3 - 2 = \mathbf{1}$
  - $\max = \mathbf{1}$ (Tie: $\nwarrow$ and $\leftarrow$)

#### Row 4 ($x_4 = \text{'T'}$):
- **Cell (4, 1) [$y_1 = \text{'V'}$]:** Mismatch ($-1$)
  - Diag: $F(3,0) - 1 = -6 - 1 = -7$
  - Up: $F(3,1) - 2 = -2 - 2 = \mathbf{-4}$
  - Left: $F(4,0) - 2 = -8 - 2 = -10$
  - $\max = \mathbf{-4}$ (Pointer: $\uparrow$)
- **Cell (4, 2) [$y_2 = \text{'H'}$]:** Mismatch ($-1$)
  - Diag: $F(3,1) - 1 = -2 - 1 = -3$
  - Up: $F(3,2) - 2 = 2 - 2 = \mathbf{0}$
  - Left: $F(4,1) - 2 = -4 - 2 = -6$
  - $\max = \mathbf{0}$ (Pointer: $\uparrow$)
- **Cell (4, 3) [$y_3 = \text{'T'}$]:** Match ($+2$)
  - Diag: $F(3,2) + 2 = 2 + 2 = \mathbf{4}$
  - Up: $F(3,3) - 2 = 3 - 2 = 1$
  - Left: $F(4,2) - 2 = 0 - 2 = -2$
  - $\max = \mathbf{4}$ (Pointer: $\nwarrow$)
- **Cell (4, 4) [$y_4 = \text{'P'}$]:** Mismatch ($-1$)
  - Diag: $F(3,3) - 1 = 3 - 1 = \mathbf{2}$
  - Up: $F(3,4) - 2 = 1 - 2 = -1$
  - Left: $F(4,3) - 2 = 4 - 2 = \mathbf{2}$
  - $\max = \mathbf{2}$ (Tie: $\nwarrow$ and $\leftarrow$)

#### Row 5 ($x_5 = \text{'P'}$):
- **Cell (5, 1) [$y_1 = \text{'V'}$]:** Mismatch ($-1$)
  - Diag: $F(4,0) - 1 = -8 - 1 = -9$
  - Up: $F(4,1) - 2 = -4 - 2 = \mathbf{-6}$
  - Left: $F(5,0) - 2 = -10 - 2 = -12$
  - $\max = \mathbf{-6}$ (Pointer: $\uparrow$)
- **Cell (5, 2) [$y_2 = \text{'H'}$]:** Mismatch ($-1$)
  - Diag: $F(4,1) - 1 = -4 - 1 = -5$
  - Up: $F(4,2) - 2 = 0 - 2 = \mathbf{-2}$
  - Left: $F(5,1) - 2 = -6 - 2 = -8$
  - $\max = \mathbf{-2}$ (Pointer: $\uparrow$)
- **Cell (5, 3) [$y_3 = \text{'T'}$]:** Mismatch ($-1$)
  - Diag: $F(4,2) - 1 = 0 - 1 = -1$
  - Up: $F(4,3) - 2 = 4 - 2 = \mathbf{2}$
  - Left: $F(5,2) - 2 = -2 - 2 = -4$
  - $\max = \mathbf{2}$ (Pointer: $\uparrow$)
- **Cell (5, 4) [$y_4 = \text{'P'}$]:** Match ($+2$)
  - Diag: $F(4,3) + 2 = 4 + 2 = \mathbf{6}$
  - Up: $F(4,4) - 2 = 2 - 2 = 0$
  - Left: $F(5,3) - 2 = 2 - 2 = 0$
  - $\max = \mathbf{6}$ (Pointer: $\nwarrow$)

---

### Step 3: Complete Filled DP Matrix

```
              [-]       V (j=1)     H (j=2)     T (j=3)     P (j=4)
  [-]          0          -2          -4          -6          -8
  V (i=1)     -2         [2]\nw        0<-        -2<-        -4<-
  H (i=2)     -4          0^         [4]\nw        2<-         0<-
  L (i=3)     -6         -2^         [2]^         3\nw        1\nw,<-
  T (i=4)     -8         -4^          0^         [4]\nw        2\nw,<-
  P (i=5)    -10         -6^         -2^          2^         [6]\nw
```

*(Brackets indicate the cells traversed during optimal traceback).*

---

### Step 4: Traceback & Alignment Reconstruction

1. Start at terminal cell **$F(5, 4) = 6$**:
   - Pointer is **$\nwarrow$ (Diagonal)** from $F(4, 3)$.
   - Align $x_5$ (`P`) with $y_4$ (`P`).
   - Move to $F(4, 3)$.
2. At cell **$F(4, 3) = 4$**:
   - Pointer is **$\nwarrow$ (Diagonal)** from $F(3, 2)$.
   - Align $x_4$ (`T`) with $y_3$ (`T`).
   - Move to $F(3, 2)$.
3. At cell **$F(3, 2) = 2$**:
   - Pointer is **$\uparrow$ (Up)** from $F(2, 2)$.
   - Align $x_3$ (`L`) with a gap **`'-'`** in Sequence $Y$.
   - Move to $F(2, 2)$.
4. At cell **$F(2, 2) = 4$**:
   - Pointer is **$\nwarrow$ (Diagonal)** from $F(1, 1)$.
   - Align $x_2$ (`H`) with $y_2$ (`H`).
   - Move to $F(1, 1)$.
5. At cell **$F(1, 1) = 2$**:
   - Pointer is **$\nwarrow$ (Diagonal)** from $F(0, 0)$.
   - Align $x_1$ (`V`) with $y_1$ (`V`).
   - Move to $F(0, 0)$ $\implies$ **TERMINATE**.

### Final Optimal Global Alignment:

```
  Sequence X:   V   H   L   T   P
  Sequence Y:   V   H   -   T   P
```

### Verification of Score:
$$\text{Score} = s(V,V) + s(H,H) + \text{gap} + s(T,T) + s(P,P)$$
$$\text{Score} = (+2) + (+2) + (-2) + (+2) + (+2) = \mathbf{+6}$$
The calculated score matches the terminal matrix cell value $F(5, 4) = 6$!

---

## Formative In-Class Checks

### Question 1
**Prompt:** During a Needleman-Wunsch calculation with match $= +3$, mismatch $= -1$, and gap $d = 2$, compute the value of cell $F(1, 1)$ if residue $x_1 = \text{'A'}$ and $y_1 = \text{'C'}$. Show the comparison of the three incoming routes.

**Model Answer:**
- $F(0, 0) = 0$, $F(0, 1) = -2$, $F(1, 0) = -2$.
- $x_1 \neq y_1 \implies$ Mismatch score $s(A, C) = -1$.
- Evaluate three incoming paths:
  1. Diagonal: $F(0, 0) + s(A, C) = 0 + (-1) = \mathbf{-1}$
  2. Up (Vertical): $F(0, 1) - d = -2 - 2 = \mathbf{-4}$
  3. Left (Horizontal): $F(1, 0) - d = -2 - 2 = \mathbf{-4}$
- Taking the maximum:
  $$F(1, 1) = \max(-1, -4, -4) = \mathbf{-1}$$
The cell value is **$-1$**, with a diagonal pointer ($\nwarrow$).

---

### Question 2
**Prompt:** Why must a global alignment algorithm initialize the top row and left column with cumulative negative gap penalties ($-j \cdot d$ and $-i \cdot d$), whereas a local alignment algorithm initializes them with zeros?

**Model Answer:**
- In **global alignment (Needleman-Wunsch)**, the objective is end-to-end alignment spanning the full length of both sequences. If sequence $X$ has length $m$ and sequence $Y$ is empty, aligning them requires introducing $m$ consecutive gaps, each penalized by $d$, yielding a cumulative penalty of $-m \cdot d$.
- In **local alignment (Smith-Waterman)**, the objective is to locate the most conserved internal sub-segment regardless of surrounding non-homologous flanking sequences. Penalizing leading gaps would unfairly depress the score of conserved motifs located deep within long proteins; therefore, local alignment initializes edges with zeros, allowing an alignment to begin anywhere at zero penalty.

---

### Question 3
**Prompt:** If cell $F(i, j)$ in a dynamic programming matrix receives identical maximal scores from both the Diagonal pointer ($\nwarrow$) and the Left pointer ($\leftarrow$), what does this tie imply biologically and computationally?

**Model Answer:**
- **Computationally:** It indicates that the dynamic programming optimization landscape contains **multiple co-optimal solutions** (alternative alignments that achieve the identical optimal mathematical score).
- **Biologically:** It implies an evolutionary ambiguity: the observed sequence divergence could be explained equally well by either a point mutation (substitution) or an insertion/deletion event at that position. A complete alignment tool should report both alternative traceback paths to the investigator.
