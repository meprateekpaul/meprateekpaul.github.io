# Quiz 2: Dedicated Test on Dynamic Programming Hand Alignment

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit Covered:** Unit 5 (Sequence Alignment — Optimal Dynamic Programming)  
**Time Allowed:** 15 Minutes  
**Maximum Marks:** 10 Marks  
**Nature of Examination:** Closed Book, Individual Assessment (Calculator permitted)  

---

## Part I: Student Test Paper

### Instructions to Candidates
1. You are required to compute the optimal global and local alignments between two 6-residue peptide sequences by hand.
2. Show all matrix cell values and directional traceback pointers clearly.
3. Use the scoring parameters specified for each problem.

---

### Problem: Dynamic Programming on a 6-Residue Toy Matrix (10 Marks)

You are provided with two peptide fragments derived from the globin family:  
* **Sequence 1 ($X$, Row sequence):** `H - E - A - G - A - W`  (Length $M = 6$)  
* **Sequence 2 ($Y$, Column sequence):** `H - E - A - W - A - W`  (Length $N = 6$)

#### Scoring Scheme:
* **Identical Match:** $+2$  
* **Mismatch / Substitution:** $-1$  
* **Linear Gap Penalty ($d$):** $-2$ per gap character

---

### Task A: Needleman–Wunsch Global Alignment (6 Marks)

1. **Matrix Initialization & Fill:** Initialize row 0 and column 0, and compute the populated $7 \times 7$ dynamic programming matrix $F(i,j)$ using the global recurrence relation:  
   $$F(i,j) = \max \begin{cases} 
   F(i-1, j-1) + s(x_i, y_j) & \text{(Diagonal)} \\ 
   F(i-1, j) - d & \text{(Up: deletion)} \\ 
   F(i, j-1) - d & \text{(Left: insertion)} 
   \end{cases}$$  
   Draw traceback arrows in each cell indicating the optimal predecessor(s). `[4 Marks]`

```text
       -       H       E       A       W       A       W
   +-------+-------+-------+-------+-------+-------+-------+
 - |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+
 H |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+
 E |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+
 A |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+
 G |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+
 A |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+
 W |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+
```

2. **Traceback & Optimal Global Alignment:**  
   Trace back from bottom-right cell $(6,6)$ to origin $(0,0)$. Write out the final aligned sequences and report the optimal global alignment score: `[2 Marks]`

   * **Optimal Global Alignment:**  
     `Seq X:  ____________________________________`  
     `Seq Y:  ____________________________________`  
   * **Final Global Alignment Score:** `__________`

---

### Task B: Smith–Waterman Local Alignment Concept & Traceback (4 Marks)

1. State the Smith–Waterman local alignment dynamic programming recurrence relation, explaining how the zero lower bound alters matrix initialization and cell evaluation. `[2 Marks]`

2. In the matrix for Sequence $X$ (`HEAGAW`) vs Sequence $Y$ (`HEAWAW`), consider the local alignment of the shared N-terminal tripeptide `H-E-A` vs `H-E-A` at coordinate $(3,3)$:  
   - What is the numerical score in cell $(3,3)$? `[1 Mark]`  
   - Where does the local traceback terminate, and what is the resulting local alignment? `[1 Mark]`

---
---

## Part II: Instructor Answer Key & Marking Scheme

### Task A: Needleman–Wunsch Global Alignment (6 Marks)

#### 1. Fully Populated Matrix with Traceback Arrows (4 Marks)

* **Residue Pair Matches:**  
  - Matches ($+2$): $(H,H)$, $(E,E)$, $(A,A)$, $(W,W)$.  
  - Mismatches ($-1$): $(G,W)$, $(A,W)$, etc.  
  - Gap penalty: $-2$.

* **Stepwise Evaluation:**  
  - Row 0 / Col 0: Initialized with $0, -2, -4, -6, -8, -10, -12$.  
  - Cell $(1,1)$ [$H,H$]: $\max\{0+2, -2-2, -2-2\} = \mathbf{+2}$ ($\nwse$).  
  - Cell $(2,2)$ [$E,E$]: $\max\{2+2, -4-2, -4-2\} = \mathbf{+4}$ ($\nwse$).  
  - Cell $(3,3)$ [$A,A$]: $\max\{4+2, -6-2, -6-2\} = \mathbf{+6}$ ($\nwse$).  
  - Cell $(4,4)$ [$G,W$]: Mismatch ($-1$). $\max\{6-1, 4-2, 4-2\} = \mathbf{+5}$ ($\nwse$).  
  - Cell $(5,5)$ [$A,A$]: Match ($+2$). $\max\{5+2, 3-2, 3-2\} = \mathbf{+7}$ ($\nwse$).  
  - Cell $(6,6)$ [$W,W$]: Match ($+2$). $\max\{7+2, 5-2, 5-2\} = \mathbf{+9}$ ($\nwse$).

* **Fully Populated Matrix:**  

```text
         -       H        E        A        W        A        W
   +--------+--------+--------+--------+--------+--------+--------+
 - |    0   |   -2   |   -4   |   -6   |   -8   |  -10   |  -12   |
   +--------+--------+--------+--------+--------+--------+--------+
 H |   -2   |   +2 ↖ |    0 ← |   -2 ← |   -4 ← |   -6 ← |   -8 ← |
   +--------+--------+--------+--------+--------+--------+--------+
 E |   -4   |    0 ↑ |   +4 ↖ |   +2 ← |    0 ← |   -2 ← |   -4 ← |
   +--------+--------+--------+--------+--------+--------+--------+
 A |   -6   |   -2 ↑ |   +2 ↑ |   +6 ↖ |   +4 ← |   +2 ← |    0 ← |
   +--------+--------+--------+--------+--------+--------+--------+
 G |   -8   |   -4 ↑ |    0 ↑ |   +4 ↑ |   +5 ↖ |   +3 ← |   +1 ← |
   +--------+--------+--------+--------+--------+--------+--------+
 A |  -10   |   -6 ↑ |   -2 ↑ |   +2 ↑ |   +3 ↑ |   +7 ↖ |   +5 ← |
   +--------+--------+--------+--------+--------+--------+--------+
 W |  -12   |   -8 ↑ |   -4 ↑ |    0 ↑ |   +4 ↖ |   +5 ↑ |   +9 ↖ |
   +--------+--------+--------+--------+--------+--------+--------+
```

* **Marking Breakdown for Matrix:**  
  * **1.0 Mark:** Correct initialization of Row 0 and Column 0 with cumulative $-2$ steps.  
  * **2.0 Marks:** Correct calculation of internal matrix cell values. (Deduct 0.5 for every 2 arithmetic errors).  
  * **1.0 Mark:** Clear and correct traceback directional pointers ($\nwse, \leftarrow, \uparrow$).

#### 2. Traceback Path, Score & Alignment (2 Marks)

* **Traceback Walk:**  
  - Start at bottom-right cell $(6,6)$ with score $+9$. Pointer is diagonal $\nwse$ to $(5,5)$. (`W` / `W`)  
  - At $(5,5)$ with score $+7$. Pointer is diagonal $\nwse$ to $(4,4)$. (`A` / `A`)  
  - At $(4,4)$ with score $+5$. Pointer is diagonal $\nwse$ to $(3,3)$. (`G` / `W` mismatch)  
  - At $(3,3)$ with score $+6$. Pointer is diagonal $\nwse$ to $(2,2)$. (`A` / `A`)  
  - At $(2,2)$ with score $+4$. Pointer is diagonal $\nwse$ to $(1,1)$. (`E` / `E`)  
  - At $(1,1)$ with score $+2$. Pointer is diagonal $\nwse$ to $(0,0)$. (`H` / `H`)  
  - Traceback terminates at $(0,0)$.

* **Final Global Alignment:**  
  ```text
  Seq X:  H - E - A - G - A - W
          |   |   |   :   |   |
  Seq Y:  H - E - A - W - A - W
  ```
* **Score Verification:** $2 + 2 + 2 + (-1) + 2 + 2 = \mathbf{+9}$.  
* **Marking Breakdown:**  
  * **1.0 Mark:** Correct alignment representation with aligned letters.  
  * **1.0 Mark:** Exactly $+9$ reported as final global score.

---

### Task B: Smith–Waterman Local Alignment (4 Marks)

1. **Recurrence Relation & Zero Bound (2 Marks):**  
   $$F(i,j) = \max \begin{cases} 
   0 & \text{(Zero lower bound / termination)} \\ 
   F(i-1, j-1) + s(x_i, y_j) & \text{(Diagonal: match/mismatch)} \\ 
   F(i-1, j) - d & \text{(Up: gap in } Y\text{)} \\ 
   F(i, j-1) - d & \text{(Left: gap in } X\text{)} 
   \end{cases}$$  
   *Explanation:* Row 0 and Column 0 are initialized entirely with **zeros** ($F(i,0) = 0, F(0,j) = 0$). The zero bound prevents negative score accumulation; if local sequence similarity drops below zero, the alignment ends, allowing a new high-scoring local alignment to begin anywhere downstream. `[2 Marks]`

2. **Local Optimal Hit & Termination (2 Marks):**  
   - **Score at Cell $(3,3)$:** Cell $(3,3)$ aligns `H-E-A` vs `H-E-A` without mismatches:  
     $$\text{Score} = (+2) + (+2) + (+2) = \mathbf{+6} \quad \text{`[1 Mark]`}$$  
   - **Termination & Optimal Local Alignment:**  
     Traceback starts at the maximal matrix cell (cell 6,6 with $+9$ if full sequence aligns, or cell 3,3 for the N-terminal tripeptide `HEA`). Traceback proceeds diagonally backwards and **terminates as soon as a cell with score 0 is encountered** (cell 0,0).  
     *Optimal Local Alignment:*  
     ```text
     Seq X:  H - E - A
             |   |   |
     Seq Y:  H - E - A
     Score:  +6
     ```  
     `[1 Mark]`
