# Instructor Answer Key & Evaluation Manual: Practical 08 (Multiple Sequence Alignment)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S08 (Syllabus Practical P10)  
**Curriculum Topic:** Multiple Sequence Alignment Using ClustalW/Clustal Omega and Jalview  

---

## 1. Expected Outputs & Reference Solutions

### Table 8.1: Invariant and Critical Functional Residues in the Globin Family MSA (Completed)
*(Positions reference the standard Clustal Omega alignment of `globin_family_proteins.fasta` / `globin_family.aln`).*

| Functional Landmark | HBB Residue & Position | Aligned Column No. in MSA | Residue in HBA1 | Residue in MB | Residue in NGB | Clustal Consensus Token (`*`, `:`, `.`, space) | Biological Role |
|---|:---:|:---:|:---:|:---:|:---:|:---:|---|
| **Distal Histidine (His-E7)** | His-64 | ~Column 68 | `His` (H) | `His` (H) | `His` (H) | `*` (or `:`) | Stabilizes bound $O_2$ ligand via hydrogen bond |
| **Proximal Histidine (His-F8)** | His-93 | ~Column 105 | `His` (H) | `His` (H) | `His` (H) | `*` (Invariant) | Covalently coordinates the $Fe^{2+}$ heme iron |
| **Invariant Phenylalanine (CD1)** | Phe-43 | ~Column 45 | `Phe` (F) | `Phe` (F) | `Phe` (F) | `*` (Invariant) | Wedges the porphyrin ring into hydrophobic pocket |
| **Sickle Cell Site (E6V)** | Glu-7 | Column 7 | `Ala` (A) | `Glu` (E) | `Met` (M) | ` ` (Space / Divergent) | Surface residue; non-conserved across paralogues |

### Table 8.2: Clustal Consensus Symbol Interpretation (Completed)
| Symbol | Mathematical / Property Definition | Count in Globin Family Alignment (Approx.) | Biological Significance |
|:---:|---|:---:|---|
| `*` (Asterisk) | 100% identical residue across all sequences | ~18 – 24 columns | Essential core architecture or invariant active-site ligands |
| `:` (Colon) | Strongly similar physico-chemical group ($>0.5$ in PAM250) | ~25 – 35 columns | Conservative substitutions (e.g., Leu/Ile/Val, Arg/Lys) |
| `.` (Period) | Weakly similar physico-chemical group ($\le 0.5$ in PAM250) | ~15 – 22 columns | Semi-conservative substitutions (e.g., Ser/Ala, Asn/Gln) |
| ` ` (Space) | No conservation / divergent properties | ~80 – 100 columns | Tolerant surface loops, termini, evolutionary drift |

---

## 2. Sample MSA Fragment Wireframe (`globin_family.aln`)

```
CLUSTAL O(1.2.4) multiple sequence alignment

NP_000508.1_HBA1      -MVLSPADKTNVKAAWGKVGAHAGEYGAEALERMFLSFPTTKTYFPHF-DLS-----HGS  53
NP_000509.1_HBB       -MVHLTPEEKSAVTALWGKVN--VDEVGGEALGRLLVVYPWTQRFFESFGDLSTPDAVMG  57
NP_000510.1_HBD       -MVHLTPEEKTAVNALWGKVN--VDAVGGEALGRLLVVYPWTQRFFESFGDLSSPDAVMG  57
NP_000550.2_HBG1      -MGHFTEEDKATITSLWGKVN--VEDAGGETLGRLLVVYPWTQRFFDSFGNLSSASAIMG  57
NP_005359.1_MB        --MGLSDGEWQLVLNVWGKVEADIPGHGQEVLIRLFKGHPETLEKFDKFKHLKSEDEMKA  58
NP_067080.1_NGB       -MERPEPELIRQSWRAVSRSPLEHGTVLFARLFALEPDLLPLFQYNCRQFSSPEDCLSSP  59
NP_599030.1_CYGB      MEKVPGEMEIERPERGAESKEAELVERYFETLVAHEP---RLLSYFPKDFSRFEDSLSAP  57
                                     . *       .    .  *             :            

NP_000508.1_HBA1      AQVKGHGKKVADALTNAVAHVDDMPNALSALSDLHAHKLRVDPVNFKLLSHCLLVTLAAH  113
NP_000509.1_HBB       NPKVKAHGKKVLGAFSDGLAHLDNLKGTFATLSELHCDKLHVDPENFRLLGNVLVCVLAHH  117
NP_000510.1_HBD       NPKVKAHGKKVLGAFSDGLAHLDNLKGTFSQLSELHCDKLHVDPENFRLLGNVLVCVLARH  117
NP_000550.2_HBG1      NPKVKAHGKKVLTSLGDAIKHLDDLKGTFAQLSELHCDKLHVDPENFKLLGNVLVTVLAIH  117
NP_005359.1_MB        SEDLKKHGATVLTALGGILKKKGHHEAEIKPLAQSHATKHKIPVKYLEFISECIIQVLQSK  118
NP_067080.1_NGB       -EHFRVHGRSVLVALAAFLKKSDPLEAQHRLLSHCHSRRLHVDPEHFKLLGDCLLVILAQH  118
NP_599030.1_CYGB      -TRFGEHGRSVLVALGGFLKRHDPQEAQLKILTRCHSKRLHVDPENFRLLGDCLIVVLAQH  116
                             *  . .          .       :   :   :  *     ::.  ::  *   
                                  ^^                 ^^
                            Distal His (E7)       Proximal His (F8)
```

---

## 3. Model Answers to Discussion Questions

### Q1. The "Once a Gap, Always a Gap" Flaw
- **Model Answer:** In the progressive alignment algorithm, sequences are aligned hierarchically according to a guide tree. Once an alignment between two sequences (or profiles) is locked, gaps inserted into either sequence are treated as fixed characters in all subsequent alignment stages ("frozen gaps"). If an initial misplacement of a gap occurs due to non-optimal local penalties or divergent sequence noise, the algorithm has no backtracking or iterative mechanism to reopen, shift, or eliminate that gap. Modern algorithms like **MUSCLE** and **MAFFT** solve this by implementing **iterative refinement**: they repeatedly partition the completed alignment into two sub-profiles, recalculate profile-profile alignments, and realign, allowing misplaced gaps to be dynamically corrected.

### Q2. Proximal vs. Distal Histidine Invariance
- **Model Answer:**
  - **Proximal Histidine (His-F8):** Forms a direct, indispensable covalent coordination bond with the fifth coordination site of the iron atom ($Fe^{2+}$) in the heme porphyrin ring. Mutation of His-F8 obliterates heme binding, destroys globin fold integrity, and causes severe globin precipitation (Heinz bodies). Hence, it is subject to absolute purifying selection across all globins.
  - **Distal Histidine (His-E7):** Does not bind the iron directly; instead, it resides on the opposite face of the heme pocket, forming a hydrogen bond with the bound diatomic oxygen ligand ($O_2$) and sterically discriminating against toxic carbon monoxide ($CO$). While highly conserved in vertebrates, certain invertebrates and non-symbiotic plant globins employ alternative residues (e.g., Gln, Leu) that can sterically shield the pocket or stabilize oxygen through different hydrogen-bonding architectures.

### Q3. Reading the Guide Tree (Orthologues vs. Paralogues)
- **Model Answer:**
  - **Paralogues:** Genes related via **gene duplication events within an ancestral genome**. Human HBB, HBA1, and Myoglobin arose from ancient gene duplications of an ancestral globin gene hundreds of millions of years ago, allowing them to evolve specialized divergent functions (tetrameric cooperativity in blood vs. high-affinity monomeric oxygen storage in muscle).
  - **Orthologues:** Genes related via **speciation events from a common ancestral organism**. Human HBB and chimpanzee HBB arose when the hominid lineage speciated; they perform the identical physiological function in both descendant species.

### Q4. Coloring Schemes in Jalview
- **Model Answer:** Coloring by hydrophobicity highlights the fundamental thermodynamic driving force of globular protein folding: the sequestration of non-polar side chains away from water into an interior **hydrophobic core**, while charged and polar residues remain exposed to solvent on the exterior surface. In alpha-helices (such as the 8 helices A through H of the globin fold), one observes an **amphipathic periodicity** where hydrophobic residues recur every 3 to 4 residues (corresponding to the 3.6 residues per helical turn), perfectly outlining the face of the helix packed against the heme core versus the solvent-exposed surface.

### Q5. Impact of Adding Divergent Sequences
- **Model Answer:** As more divergent sequences (e.g., plant leghemoglobin, bacterial flavohemoglobins) are added to the MSA, the number of fully invariant columns (`*`) **decreases significantly**. Because an asterisk requires 100% identity across every single sequence in the alignment, every additional evolutionary lineage introduces lineage-specific mutational drift. Only the absolute core catalytic and biophysical keystones (such as the proximal histidine His-F8 and the CD1 phenylalanine wedging the heme) remain completely invariant across billions of years of divergence.

---

## 4. Solution to Extension / Challenge Task

1. **Alignment of 9 Vertebrate HBB Orthologues:**
   - Aligned sequences: Human, Chimpanzee, Gorilla, Macaque, Mouse, Rat, Cattle, Chicken, Zebrafish (`hbb_vertebrate_orthologues.fasta`).
2. **Identical Columns Count:**
   - Across all 9 species, ~75–85 columns out of 147 (~55%) are 100% identical.
   - Among primates (Human, Chimp, Gorilla, Macaque), identity is $>98\%$.
3. **Most Divergent Vertebrate:**
   - **Zebrafish (*Danio rerio*)** is the most divergent, exhibiting ~45% to 50% sequence divergence from human HBB.
   - **Evolutionary Explanation:** Teleost fish diverged from the tetrapod common ancestor approximately 450 million years ago, compared to mammals diverging from birds ~310 million years ago, and rodents diverging from primates ~80 million years ago. The greater elapsed time allowed a vastly higher number of neutral and adaptive substitutions to accumulate in the teleost globin lineage.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & Clustal Execution** | 2.0 | Deduct 0.5 if student failed to align the 7 globin paralogues. |
| **Landmark Identification (Table 8.1)** | 4.0 | Deduct 1.0 if His-E7 or His-F8 are misidentified or column numbers omitted. |
| **Consensus & Jalview Analysis (Table 8.2)** | 2.0 | Deduct 0.5 if Clustal consensus symbol definitions are inaccurate. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question for scientifically rigorous explanations. |
| **Total** | **10.0** | |
