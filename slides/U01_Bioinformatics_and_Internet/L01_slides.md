---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 01 Slides: Introduction to Bioinformatics"
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
# Lecture 01 — Introduction to Bioinformatics
### Concepts of Bioinformatics (CBBI-501)
**Unit 01:** Bioinformatics and Internet  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Title & Foundations

```text
Course: CBBI-501 — Concepts of Bioinformatics (Semester II)
Lecture 01: What is Bioinformatics & The Genomic Data Revolution

[Visual: Schematic of Central Dogma (DNA -> RNA -> Protein -> Phenotype)
         bridged to Computer Science (Bits -> Text -> Matrices -> 3D Models)]
```

**Speaker Talking Points:**  
* Welcome to the core computational foundation of your B.Tech. degree.
* Bioinformatics is not merely "using computers in biology"; it is the mathematical,
  statistical, and algorithmic science that decodes biological information.
* Molecular biology has transitioned from a purely descriptive, wet-lab discipline
  into an information science driven by massive, high-throughput digital data.

---

## Slide 2: The Biological Information Explosion

```text
Topic: Exponential Data Growth vs Moore's Law

[Visual: ASCII Curve showing GenBank base-pair doubling every ~18 months
         outpacing computer processing cost reductions post-NGS (2007)]

  Base Pairs
    ^
    |                                                * (2020s: Petabytes)
    |                                            *
    |                                        *
    |                                    * (Next-Gen Sequencing Boom)
    |                            *
    |                    *
    |            *  (Sanger Era)
    +--------------------------------------------------------> Time (Years)
```

**Speaker Talking Points:**  
* In 1965, Margaret Dayhoff published the first *Atlas of Protein Sequence and Structure*
  containing 65 protein sequences on physical paper.
* Today, the International Nucleotide Sequence Database Collaboration (INSDC)
  holds trillions of bases spanning hundreds of thousands of species.
* The bottleneck in modern biology is no longer data acquisition—it is data analysis,
  interpretation, storage, and contextual retrieval.

---

## Slide 3: The Central Dogma as a Digital Information Conduit

```text
Topic: Digital Nature of the Genome and Proteome

[Visual: 
 DNA:    5'- ... A T G G T G C A C C T G A C T C C T G A G G A G ... -3' (Digital: Alphabet of 4)
             |   | | | | | | | | | | | | | | | | | | | | | |
 mRNA:   5'- ... A U G G U G C A C C U G A C U C C U G A G G A G ... -3' (Digital: Codons)
             |   \___/ \___/ \___/ \___/ \___/ \___/ \___/
 Protein: N- ...   M     V     H     L     T     P     E     E  ... -C  (Digital: Alphabet of 20)
             |
 Structure: 3D coordinates (x, y, z) in space (Analog / Physical Chemistry)]
```

**Speaker Talking Points:**  
* DNA is fundamentally a digital discrete storage medium: strings over Sigma_DNA = {A, C, G, T}.
* Translation maps 64 triplet codons to 20 amino acids (degenerate, deterministic code).
* Proteins fold into intricate 3D shapes driven by thermodynamics: bioinformatics connects
  the 1D digital sequence string directly to 3D physical structure and function.

---

## Slide 4: The Four Foundational Questions of Bioinformatics

```text
Topic: What computational biology actually calculates

+-------------------------+---------------------------------------------------+
| Core Question           | Computational Approach & Tools                    |
+-------------------------+---------------------------------------------------+
| 1. What is this sequence?| Database searching, exact & heuristic matching    |
|                         | (BLAST, FASTA, Entrez)                            |
| 2. What is it related   | Pairwise & multiple sequence alignment, phylogeny |
|    to? (Evolution)      | (Needleman-Wunsch, Smith-Waterman, Clustal, NJ)   |
| 3. What is its 3D shape?| Structure prediction, modeling, coordinates       |
|    (Biophysics)         | (PDB, GOR, AlphaFold, Homology modeling)          |
| 4. What does it do?     | Functional annotation, motif finding, expression  |
|    (Phenotype)          | (PROSITE, Pfam, Gene Ontology, RNA-seq)           |
+-------------------------+---------------------------------------------------+
```

**Speaker Talking Points:**  
* Every tool you will learn this semester addresses one or more of these four queries.
* We do not treat tools as black boxes; we dissect their underlying scoring functions,
  dynamic programming tables, and statistical guarantees.

---

## Slide 5: The Thread of the Semester: Human Hemoglobin Beta (HBB)

```text
Topic: One Molecule, Complete Bioinformatics Arc

[Visual: Diagram connecting HBB through the 11 units:
 NCBI Gene -> GenBank NM_000518 -> NP_000509 -> BLAST against globins -> 
 Phylogenetic Tree -> ProtParam pI/MW -> PDB 1A3N / 4HHB -> 11p15.4 Synteny]
```

**Speaker Talking Points:**  
* Rather than using disconnected toy examples, we will track human beta-globin (*HBB*)
  across every single unit and practical.
* Accessions to memorize:
  - mRNA: `NM_000518.5`
  - Protein: `NP_000509.1` (UniProt: `P68871`)
  - 3D Structure: PDB `1A3N` (deoxyhemoglobin), `4HHB`
* Secondary comparative references: Insulin (*INS*) and Tumor Suppressor *TP53*.

---

## Slide 6: A Single Nucleotide Polymorphism: HbS and Glu6Val

```text
Topic: The Molecular Paradigm of Sickle Cell Anemia

  Wild-type Beta-Globin (HbA):
    Codon 6:  G A G  -->  Glutamic Acid (Glu / E) [Negatively charged, polar, hydrophilic]
    Surface:  Soluble, repels adjacent tetramers in red blood cell cytoplasm.

  Sickle-cell Variant (HbS):
    Codon 6:  G T G  -->  Valine (Val / V)        [Non-polar, branched aliphatic, hydrophobic]
    Surface:  Creates a sticky hydrophobic patch (Phe85/Leu88 docking pocket on partner beta-chain).
    Result:   Polymerization into long insoluble fibers under deoxy conditions -> erythrocyte sickling.
```

**Speaker Talking Points:**  
* A change of a single bit of information (A -> T) in a 444-nucleotide coding region
  alters one residue out of 147, transforming a life-sustaining molecule into a lethal pathology.
* Bioinformatics gives us the computational microscope to detect, predict, and model
  such consequences before entering the wet lab.

---

## Slide 7: Course Architecture & The 11 Units

```text
Topic: Road Map of CBBI-501

[Visual: 4 Pillars of the Curriculum:
 1. Data & Retrieval (Units 1-4)    --> Internet, Entrez, ASN.1, GenBank
 2. Alignment & Evolution (Units 5-7)--> DP, BLAST, MSA, Phylogenetics
 3. Predictive Biology (Units 8-9)  --> DNA features, Codon bias, Protein properties
 4. Structure & Genomes (Units 10-11)--> PDB, 3D Modeling, Synteny & Genomics]
```

**Speaker Talking Points:**  
* Units 1-4 establish the data landscape: where data lives and how it is structured.
* Units 5-7 cover core algorithms: Needleman-Wunsch, Smith-Waterman, BLAST heuristics, and trees.
* Units 8-9 focus on prediction from sequence alone: ORFs, CpG islands, hydropathy, secondary structure.
* Units 10-11 culminate in macromolecular 3D structures and whole-genome comparative synteny.

---

## Slide 8: Summary & Looking Ahead

```text
Topic: Takeaways from Lecture 01

* Biological systems are digital information processors.
* Bioinformatics sits at the intersection of Molecular Biology, Computer Science,
  and Applied Mathematics.
* Our course thread (*HBB*) demonstrates how sequence dictates structure, and structure
  governs physiological function.
* Next Lecture: How does biological data travel over the wire? Internet protocols,
  FTP servers, client-server models, and the INSDC exchange.
```

