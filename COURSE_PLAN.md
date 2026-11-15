# Concepts of Bioinformatics — Course Plan

> **Academic Framework:** Inspired by and formulated from the B.Tech. Bioinformatics undergraduate curriculum of [Sam Higginbottom University of Agriculture, Technology and Sciences (SHUATS)](https://shuats.edu.in/), Prayagraj, Uttar Pradesh, India
> **Department:** Department of Computational Biology & Bioinformatics, Jacob Institute of Biotechnology & Bioengineering (JSBB)
> **Programme:** B.Tech. Bioinformatics, Semester II (outline w.e.f. July 2017)
> **Code:** CBBI-501 in the B.Tech. outline; the syllabus PDF prints the same course as CBBI-502
> **Credits:** 3 (L-T-P 2-0-1) — two lectures and one 2-hour practical per week
> **Syllabus source:** `../BTech_Bioinformatics_CBBI_Syllabus.md` and [SHUATS Official Portal](https://shuats.edu.in/)
>
> Everything under "Syllabus" is from the university documents. Lecture counts, the weekly schedule, the modern tool substitutions, the assessment split and the folder layout are proposals in this plan and can be changed.

---

## Contents

1. [Course at a glance](#1-course-at-a-glance)
2. [Learning outcomes](#2-learning-outcomes)
3. [Design decisions](#3-design-decisions)
4. [Theory plan, unit by unit](#4-theory-plan-unit-by-unit)
5. [Practical plan](#5-practical-plan)
6. [Week-by-week schedule](#6-week-by-week-schedule)
7. [Assessment plan](#7-assessment-plan)
8. [Folder structure](#8-folder-structure)
9. [Material to build](#9-material-to-build)
10. [References](#10-references)
11. [Python notebooks](#11-python-notebooks)

---

## 1. Course at a glance

| Unit | Syllabus topic | Lectures | Practicals |
|---|---|---|---|
| 1 | Bioinformatics and Internet | 2 | P1 |
| 2 | Information Retrieval from Biological Databases | 2 | P2, P3 |
| 3 | The NCBI data model | 2 | — |
| 4 | GenBank Sequence Database | 3 | P4, P5 |
| 5 | Sequence Alignment and Database Searching | 6 | P8, P9 |
| 6 | Multiple Sequence Alignment | 2 | P10 |
| 7 | Phylogenetic Analysis | 3 | (extension of P10) |
| 8 | Predictive Methods using Nucleotide Sequence | 2 | P7 |
| 9 | Predictive Methods using Protein Sequence | 3 | P6, P13 |
| 10 | Structure Databases | 3 | P11, P12 |
| 11 | Comparative Genome Analysis | 2 | — |
| | **Total** | **30** | **13** |

Assumes a 15-teaching-week semester: 30 lecture hours and 15 practical sessions (13 syllabus practicals, one mini-project session, one practical exam).

**Where the course sits.** Students arrive with Elementary Biology (deficiency course) and Computers and Languages from Semester I. They take Molecular Biology and Linux & Shell Programming alongside this course, so central-dogma detail and the command line are being learned in parallel, not known in advance. This course feeds CBBI-504 (Genomics & Proteomics), CBBI-507 (Computational Analysis of Biomolecules), CBBI-508 (Biological Databases) and CBBI-604 (Phyloinformatics), which revisit alignment, databases and trees at algorithmic depth.

---

## 2. Learning outcomes

By the end of the course a student can:

1. Describe what kinds of biological data exist, where each is stored, and how the major databases link to one another.
2. Retrieve a nucleotide, protein, structure or literature record with a precise Entrez query and explain every section of a GenBank flat file.
3. Explain global, local and heuristic alignment, fill a small dynamic-programming matrix by hand, and choose a substitution matrix and gap penalty with a reason.
4. Run BLAST and FASTA searches and judge hits by E-value, bit score, identity and coverage.
5. Build a multiple sequence alignment and a phylogenetic tree, and read the tree correctly (orthologues, paralogues, support values).
6. Predict basic features from sequence alone: ORFs, codon bias and repeats in DNA; composition, physico-chemical properties, motifs and secondary structure in protein.
7. Read a PDB entry, view a structure, and find structural neighbours.
8. Explain what comparative genome analysis and annotation are used for.

Each lecture and practical below is tagged with the outcome it serves (LO1–LO8).

---

## 3. Design decisions

**One set of molecules all semester.** Use human haemoglobin beta (*HBB*, NM_000518, P68871, PDB 1A3N/4HHB) as the main thread, with insulin (*INS*) and *TP53* as secondary examples, and the globin family for alignment and trees. Students meet HBB as a database record, a FASTA file, a BLAST query, a column in an alignment, a leaf in a tree, a ProtParam result and a 3D structure. The sickle-cell variant (E6V) gives a ready-made reason to care about one residue. This also matches the gene set already used in the Programming for Computational Biology course.

**Concepts first, algorithms later.** CBBI-507 covers alignment algorithms and probabilistic models in depth in Semester IV. Here, dynamic programming is taught on 5–8 residue toy sequences by hand, and heuristics (BLAST, FASTA) are taught as "what the steps are and how to read the output", not derived.

**Syllabus items that have aged.** The syllabus text predates several changes. Teach the concept the syllabus names, on the tool that exists today, and say so in class:

| Syllabus item | Status | What to teach |
|---|---|---|
| Electronic mail, FTP, "connecting to Internet" | Historic framing | Keep to one lecture: client–server model, URLs, HTTP vs FTP/SFTP, NCBI/EBI FTP sites, bulk download |
| GCG format | Wisconsin Package discontinued | Mention as a legacy format; spend the time on FASTA, GenBank, EMBL and format conversion |
| MMDB | Still exists inside NCBI Structure | Teach with iCn3D (replaced Cn3D) and VAST+ |
| ClustalW | Superseded | Run Clustal Omega or MUSCLE at EBI; show ClustalW once so the practical record matches the syllabus |
| FASTA program | Available at EBI | Run at EBI; main point is contrast with BLAST |
| GenPept | Now the NCBI Protein database | Use NCBI Protein and UniProtKB; explain the name |
| VMD | Current, but heavy for first-years | Use VMD as the syllabus says; keep Mol* (RCSB in-browser) as fallback for machines where install fails |
| GOR algorithm | Historically important, low accuracy | Run GOR IV (NPS@ server), then compare against PSIPRED and the DSSP assignment from the real structure |
| "Advanced structure modeling" | Field changed by AlphaFold | One lecture segment on homology modelling vs AlphaFold DB; depth is left to CBBI-602/605 |

**Server dependence.** Every practical relies on public web servers. For each one, keep a saved copy of expected output in `data/expected/` so a lab is not lost when a server is down or the network is slow.

---

## 4. Theory plan, unit by unit

### Unit 1 — Bioinformatics and Internet (2 lectures) · LO1

*Syllabus:* Internet Basics, FTP, www, connecting to Internet, Electronic mail, internet resources.

| L | Content |
|---|---|
| 1 | What bioinformatics is and why it exists: growth of sequence data, the central dogma as an information flow, typical questions (what is this sequence, what is it related to, what does it do). Course map and the HBB thread. |
| 2 | How data reaches you: client–server, URL anatomy, HTTP vs FTP, web interface vs bulk download vs programmatic access. Tour of the main resource hubs: NCBI, EMBL-EBI, Expasy/SIB, RCSB PDB, DDBJ. The INSDC exchange. |

*Check:* given five tasks, name the resource you would open first.

### Unit 2 — Information Retrieval from Biological Databases (2 lectures) · LO1, LO2

*Syllabus:* Integrated information retrieval (Entrez system), retrieving database entries.

| L | Content |
|---|---|
| 3 | Entrez as a linked set of databases: PubMed, Nucleotide, Protein, Gene, Structure, Taxonomy, OMIM. Neighbours and links. Identifiers: accession, version, GI (retired), RefSeq prefixes (NM_, NP_, NC_, XM_). |
| 4 | Query building: field tags (`[ORGN]`, `[GENE]`, `[TITL]`, `[PDAT]`), Boolean operators, filters, history. Why the same search gives different counts in Nucleotide and Gene. PubMed and MeSH. |

*Check:* write a query returning only human HBB RefSeq mRNA; explain each term.

### Unit 3 — The NCBI data model (2 lectures) · LO1, LO2

*Syllabus:* Introduction, Seq-id, Sequence, collection of sequence, annotation of sequence, describing sequence.

| L | Content |
|---|---|
| 5 | Why a data model: one sequence, many views. Seq-id and Bioseq; Bioseq-set (collections: nuc-prot sets, population sets). ASN.1 as the underlying format, shown side by side with the flat file. |
| 6 | Seq-annot and Seq-feat (annotation: genes, CDS, variation), Seq-descr (describing: source organism, publication, molecule type). How the model explains the links seen in Entrez. |

*Check:* label Bioseq, Seq-id, Seq-feat and Seq-descr on a printed HBB record.

### Unit 4 — GenBank Sequence Database (3 lectures) · LO2

*Syllabus:* Introduction to structure, primary and secondary database, format vs content: computer vs human, databases, GenBank flat file, GCG.

| L | Content |
|---|---|
| 7 | Primary vs secondary (curated/derived) databases: GenBank/ENA/DDBJ vs RefSeq, UniProtKB/Swiss-Prot vs TrEMBL, Pfam/PROSITE. Redundancy and why RefSeq exists. GenBank divisions. |
| 8 | The GenBank flat file line by line: LOCUS, DEFINITION, ACCESSION, VERSION, SOURCE, REFERENCE, FEATURES (source, gene, CDS, qualifiers, location syntax incl. `join` and `complement`), ORIGIN. |
| 9 | Format vs content: human-readable vs machine-readable. FASTA, GenBank, EMBL, ASN.1/XML; GCG as legacy. Format conversion (EMBOSS seqret). How sequences get submitted. |

*Check:* from a flat file, extract the CDS coordinates and state the protein length without scrolling to the translation.

### Unit 5 — Sequence Alignment and Database Searching (6 lectures) · LO3, LO4

*Syllabus:* Introduction, evolutionary basis of sequence alignment, optimal alignment method, substitution score and gap penalty, statistical significance of alignment; database similarity searching, FASTA, BLAST, database searching artifacts, position specific scoring matrices.

| L | Content |
|---|---|
| 10 | Why align: similarity vs homology, identity vs similarity, orthologues and paralogues introduced. Dot plots as the first picture of an alignment. |
| 11 | Optimal alignment: Needleman–Wunsch global alignment worked by hand on the board (matrix fill and traceback). |
| 12 | Smith–Waterman local alignment by hand; when to use global vs local. Gap penalties: linear vs affine, and what changing them does. |
| 13 | Substitution scores: where PAM and BLOSUM come from (log-odds idea, no derivation), which matrix for which divergence. Statistical significance: random expectation, bit score, E-value, effect of database size. |
| 14 | Database similarity searching: why heuristics are needed. FASTA (k-tuples, diagonals) and BLAST (words, seeds, extension, HSPs). BLAST flavours: blastn, blastp, blastx, tblastn, tblastx. |
| 15 | Reading BLAST output critically. Searching artifacts: low-complexity regions, repeats, vector contamination, compositional bias, masking. PSSMs and PSI-BLAST: what a profile is and why it finds distant relatives. |

*Check:* in-class hand alignment quiz (Quiz 2); interpret a BLAST hit table with a deliberately misleading low-complexity hit.

### Unit 6 — Multiple Sequence Alignment (2 lectures) · LO5

*Syllabus:* What is MSA, structural or evolutionary alignment, how to align sequences, tools.

| L | Content |
|---|---|
| 16 | What an MSA shows that a pairwise alignment cannot: conserved columns, motifs, indel patterns. Structural vs evolutionary alignment. Why exact MSA is infeasible. |
| 17 | Progressive alignment: pairwise distances → guide tree → profile alignment; "once a gap, always a gap". Tools: ClustalW → Clustal Omega, MUSCLE, MAFFT, T-Coffee. Viewing and judging an MSA (Jalview), conservation and consensus. |

### Unit 7 — Phylogenetic Analysis (3 lectures) · LO5

*Syllabus:* Fundamental of phylogenetic model, tree interpretation — paralogues and orthologues, tree building and tree evaluation, phylogenetic software.

| L | Content |
|---|---|
| 18 | Tree vocabulary: nodes, branches, clades, rooted vs unrooted, outgroup, branch length. Gene trees vs species trees. Reading orthologues and paralogues off the globin tree. |
| 19 | Tree building: distance methods (UPGMA worked by hand on a 4-taxon matrix, neighbour joining in outline); character methods (parsimony, maximum likelihood) as ideas only. |
| 20 | Tree evaluation: bootstrap, what a support value does and does not mean, common misreadings. Software: MEGA, PHYLIP, PhyML, iTOL for display. |

### Unit 8 — Predictive Methods using Nucleotide Sequence (2 lectures) · LO6

*Syllabus:* Introduction, marking repetitive DNA, database search, codon bias detection, detecting functional sites in DNA.

| L | Content |
|---|---|
| 21 | What can be predicted from DNA alone. Repeats and why they are masked first (RepeatMasker, interspersed vs tandem repeats). Finding ORFs; six reading frames; prokaryotic vs eukaryotic gene structure. |
| 22 | Codon usage bias and what it reveals. Functional sites: promoters, splice sites, start/stop context, polyadenylation signals, CpG islands. Similarity-based vs *ab initio* gene finding in outline. |

### Unit 9 — Predictive Methods using Protein Sequence (3 lectures) · LO6

*Syllabus:* Protein identification based on composition, physical properties based on sequence, motif and pattern, secondary structure and folding classes, specialized structure or features, tertiary structures.

| L | Content |
|---|---|
| 23 | Identification from composition and mass. Properties from sequence: molecular weight, pI, extinction coefficient, instability index, GRAVY, hydropathy plots (ProtParam, ProtScale). |
| 24 | Motifs, patterns and domains: PROSITE pattern syntax, profiles, Pfam, InterPro. Specialised features: signal peptides, transmembrane helices, coiled coils. |
| 25 | Secondary structure prediction: Chou–Fasman → GOR → neural-network methods; what Q3 accuracy means. Folding classes (all-α, all-β, α/β, α+β; SCOP/CATH). Tertiary structure prediction in outline. |

### Unit 10 — Structure Databases (3 lectures) · LO7

*Syllabus:* Introduction to structure, PDB, MMDB, structure file format, visualizing structure information, structure viewers, structure similarity searching, advanced structure modeling.

| L | Content |
|---|---|
| 26 | The four levels of protein structure in brief; how structures are determined (X-ray, NMR, cryo-EM) and what resolution and R-factor tell you. The PDB and wwPDB; MMDB at NCBI. |
| 27 | Structure file formats: PDB records (HEADER, SEQRES, ATOM, HETATM, CONECT) and mmCIF. Viewers and representations: wireframe, cartoon, surface; colouring by chain, secondary structure, B-factor. |
| 28 | Structure similarity searching (VAST+, DALI) and why structure is more conserved than sequence. Modelling in outline: homology modelling steps; AlphaFold DB as a prediction resource and how to read pLDDT. |

### Unit 11 — Comparative Genome Analysis (2 lectures) · LO8

*Syllabus:* Introduction, application, genome analysis and annotation.

| L | Content |
|---|---|
| 29 | What a genome project produces: assembly, annotation, genome browsers. Structural vs functional annotation. |
| 30 | Comparing genomes: synteny, gene content, orthologue sets, conserved non-coding regions. Applications: gene function transfer, pathogen vs non-pathogen comparison, evolution. Bridge to CBBI-504. Course wrap-up. |

---

## 5. Practical plan

One 2-hour session each. Order follows the theory, so it differs from the syllabus numbering; the syllabus number is kept in the first column for the practical record.

| Session | Syllabus no. | Practical | Tools | What the student submits | LO |
|---|---|---|---|---|---|
| 1 | P1 | Understanding Linux operating system and commands | Terminal: `pwd ls cd mkdir cp mv rm cat less head tail wc grep`, redirection, pipes | Command log; count sequences in a multi-FASTA with `grep -c ">"` | 1 |
| 2 | P2 | Introduction to NCBI | NCBI home, Gene, Nucleotide, Protein, Taxonomy | Worksheet: tour of the HBB Gene page and its links | 1, 2 |
| 3 | P3 | Using Entrez to search literature databases | PubMed, field tags, MeSH, filters, history | Five queries with result counts and reasoning | 2 |
| 4 | P4 | Retrieving DNA sequence from GenBank and analysing data formats | Nucleotide, FASTA/GenBank/ASN.1 views, EMBOSS seqret | Annotated flat file of NM_000518; converted files | 2 |
| 5 | P5 | Retrieving protein sequence from GenPept (NCBI) and Expasy | NCBI Protein, UniProtKB | Comparison table: NP_000509 vs P68871 record contents | 2 |
| 6 | P8 | Sequence alignment using BLAST | blastn, blastp, blastx at NCBI | Hit table interpretation; effect of changing database and matrix | 3, 4 |
| 7 | P9 | Sequence alignment using FASTA | FASTA at EBI | Same query as session 6; BLAST vs FASTA comparison | 3, 4 |
| 8 | P10 | Multiple sequence alignment using ClustalW | ClustalW and Clustal Omega at EBI, Jalview | Globin family MSA with conserved residues marked; tree from the alignment (links to Unit 7) | 5 |
| 9 | P7 | Analysing DNA sequence | ORFfinder, EMBOSS (`geecee`, `cusp`, `transeq`), RepeatMasker | GC content, ORF map, codon usage table for one gene | 6 |
| 10 | P6 | Analysing protein sequences | ProtParam, ProtScale, PROSITE/InterPro | Property sheet for HBB and for one membrane protein, compared | 6 |
| 11 | P13 | Secondary structure prediction using GOR algorithm | GOR IV (NPS@), PSIPRED | Prediction vs actual secondary structure from the PDB entry; Q3 computed by hand | 6 |
| 12 | P11 | Introduction to the structure database PDB | RCSB PDB, NCBI Structure/MMDB | Entry report for 1A3N: method, resolution, chains, ligands; PDB file records identified | 7 |
| 13 | P12 | Visualisation of protein structure using VMD | VMD (fallback: Mol*) | Three rendered images: cartoon by chain, haem pocket, residue 6 highlighted | 7 |
| 14 | — | Mini-project work session | All of the above | See §7 | all |
| 15 | — | Practical examination and viva | | | |

**Lab sheet format** (same for every practical): aim → background (half a page) → step-by-step procedure with the exact accession numbers → observations table to fill → 3–5 interpretation questions → one extension task for students who finish early.

---

## 6. Week-by-week schedule

| Week | Lecture 1 | Lecture 2 | Practical | Assessment |
|---|---|---|---|---|
| 1 | L1 What is bioinformatics | L2 Internet and resource hubs | S1 Linux | |
| 2 | L3 Entrez system | L4 Query building | S2 NCBI tour | |
| 3 | L5 NCBI data model I | L6 NCBI data model II | S3 Entrez / PubMed | |
| 4 | L7 Primary vs secondary databases | L8 GenBank flat file | S4 GenBank retrieval | Quiz 1 (Units 1–3) |
| 5 | L9 Formats and conversion | L10 Why align; dot plots | S5 Protein retrieval | |
| 6 | L11 Global alignment by hand | L12 Local alignment; gaps | S6 BLAST | |
| 7 | L13 Matrices and significance | L14 FASTA and BLAST | S7 FASTA | Quiz 2 (hand alignment) |
| 8 | L15 Artifacts; PSSMs | L16 What is MSA | S8 MSA | Mid-semester test (Units 1–5) |
| 9 | L17 Progressive alignment, tools | L18 Reading trees | S9 DNA analysis | Assignment 1 issued |
| 10 | L19 Tree building | L20 Tree evaluation, software | S10 Protein analysis | |
| 11 | L21 Repeats and ORFs | L22 Codon bias, functional sites | S11 GOR | Quiz 3 (Units 6–7) |
| 12 | L23 Properties from sequence | L24 Motifs and domains | S12 PDB | Assignment 1 due; mini-project issued |
| 13 | L25 Secondary structure, fold classes | L26 Structure determination, PDB | S13 VMD | |
| 14 | L27 File formats and viewers | L28 Structure similarity, modelling | S14 Mini-project | Quiz 4 (Units 8–10) |
| 15 | L29 Genome annotation | L30 Comparative genomics, wrap-up | S15 Practical exam | Mini-project due |

Practicals trail the matching lecture by about a week in the alignment block so students have seen the concept before using the tool.

---

## 7. Assessment plan

The split below is a proposal; replace the weights with the department's scheme.

| Component | Weight | Notes |
|---|---|---|
| Quizzes (4, best 3 count) | 10% | 15 minutes each, closed book |
| Assignment 1 | 5% | "Characterise an unknown sequence": each student gets a different unlabelled FASTA and reports what it is, with evidence |
| Mid-semester test | 20% | Units 1–5 |
| Practical record and continuous lab evaluation | 15% | Marked each session from the lab sheet |
| Mini-project | 10% | One gene family per group of 2–3: retrieve → BLAST → MSA → tree → properties → structure; 4-page report |
| Practical exam and viva | 10% | One retrieval task and one analysis task drawn at random |
| End-semester exam | 30% | All units, weighted towards Units 5–11 |

**Question bank target:** 15 MCQs, 6 short-answer and 2 long-answer questions per unit, each tagged with its learning outcome, built up as the unit is taught.

---

## 8. Folder structure

```
Concepts_of_Bioinformatics/
├── COURSE_PLAN.md            this file
├── README.md                 one-page overview for students
├── SYLLABUS.md               official syllabus text for this course only
├── lectures/
│   ├── U01_Bioinformatics_and_Internet/
│   ├── U02_Information_Retrieval/
│   ├── ...
│   └── U11_Comparative_Genome_Analysis/     slides + notes per lecture (L01_..., L02_...)
├── practicals/
│   ├── S01_Linux_Commands/                  lab_sheet.md, worksheet, answer key
│   ├── ...
│   └── S13_VMD_Visualisation/
├── notebooks/                 Python notebooks: course (C), practice (P), quiz (Q) per unit — see §11
│   ├── U01_Bioinformatics_and_Internet/     U01_C1_....ipynb, U01_P_....ipynb, U01_Q_....ipynb, solutions/
│   └── ...
├── outputs/                   written by notebooks; git-ignored
├── data/
│   ├── sequences/            HBB, INS, TP53, globin family FASTA/GenBank files
│   ├── structures/           1A3N.pdb, 4HHB.pdb
│   └── expected/             saved server outputs for each practical
├── assessments/
│   ├── quizzes/
│   ├── assignment_1/         per-student unknown sequences + key
│   ├── mini_project/         brief and rubric
│   ├── question_bank/        one file per unit
│   └── exams/
└── references/               reading list, tool links, cheat sheets
```

---

## 9. Material to build

Checklist, in the order it is needed.

- [ ] `SYLLABUS.md` and `README.md`
- [ ] `data/sequences/`: HBB mRNA and protein (human), HBA1, HBG1, MB, NGB, CYGB and HBB orthologues from 6–8 vertebrates for the MSA and tree
- [ ] `data/structures/`: 1A3N, 4HHB, 2HBS (sickle haemoglobin)
- [ ] Lecture slides and notes for Units 1–5 (L1–L15) before week 1
- [ ] Lab sheets S1–S8, each tested end to end on a lab machine, with saved expected output
- [ ] Quiz 1, Quiz 2, mid-semester paper
- [ ] Lecture slides and notes for Units 6–11 (L16–L30) before week 8
- [ ] Lab sheets S9–S13 with expected output
- [ ] Assignment 1 sequence set (one per student) and marking key
- [ ] Mini-project brief, list of gene families, rubric
- [ ] Quiz 3, Quiz 4, practical exam task pool, end-semester paper
- [ ] Question bank, one file per unit
- [ ] Python notebooks: 15 course, 11 practice, 11 quiz, with solutions and keys (list, build order and tracker in §11)
- [ ] One-page cheat sheets: Entrez field tags, GenBank flat-file anatomy, BLAST flavours, reading a tree

Before week 1: confirm lab machines have a Linux terminal (or WSL), a modern browser, Jalview and VMD installed, and that NCBI, EBI, Expasy and RCSB are reachable from the lab network.

---

## 10. References

The syllabus PDF lists no textbooks. Suggested:

**Core text**
- Baxevanis A.D., Ouellette B.F.F. (eds.) *Bioinformatics: A Practical Guide to the Analysis of Genes and Proteins.* Wiley. The syllabus unit titles follow this book's chapter titles closely, so it is the natural primary text; use the latest edition available (Baxevanis, Bader & Wishart, 4th ed., 2020) and note that the NCBI data model and GCG chapters are in the older editions (check the 2nd edition, 2001).

**Supporting**
- Mount D.W. *Bioinformatics: Sequence and Genome Analysis.* Cold Spring Harbor Laboratory Press.
- Lesk A.M. *Introduction to Bioinformatics.* Oxford University Press.
- Pevsner J. *Bioinformatics and Functional Genomics.* Wiley.
- Xiong J. *Essential Bioinformatics.* Cambridge University Press.

**Online**
- NCBI Handbook and NCBI Help Manual (Entrez, GenBank, BLAST)
- EMBL-EBI Training on-demand courses
- RCSB PDB-101
- Expasy resource portal

---

## 11. Python notebooks

Each unit gets Jupyter notebooks of three types: **course** (`C`, teaches with worked examples), **practice** (`P`, exercises with self-checks) and **quiz** (`Q`, short self-test with a score). How to write them — templates, naming, the quiz checker, the checklist — is in [`../NOTEBOOK_GUIDE.md`](../NOTEBOOK_GUIDE.md). This section lists what to build for this course.

**Level.** These are Semester II students who have not yet had a Python course. Course notebooks are run-and-modify; practice tasks are one to five lines with the pattern shown just above; nothing asks for a function written from nothing. Notebook U01_C1 is the only Python introduction they get here, so keep later notebooks within what it covers plus what each one introduces itself.

**Running examples.** Human *HBB* (NM_000518, P68871, PDB 1A3N), *INS*, *TP53* and the globin family, the same as the lectures and practicals.

**How they fit the week.** The course notebook is shown in the second lecture of the unit or the first 20 minutes of the practical; the web-tool practical follows; the practice notebook is homework; the quiz notebook is done before the next unit starts. Quiz notebooks are for self-testing and do not replace the four graded quizzes in §7.

### Notebooks to build

All paths are under `notebooks/U<nn>_<Unit>/`. One `P` and one `Q` per unit unless stated.

| Unit | Course notebook(s) | What the student does in it | Practice (`P`) focus | Quiz (`Q`) focus | With |
|---|---|---|---|---|---|
| 1 | `U01_C1_Sequences_as_Text` | Jupyter basics; a DNA sequence as a string: length, slicing, counting bases, reading a FASTA file from `data/` | Count, slice and compare three short sequences | What bioinformatics resources hold what; reading code output | L1–L2, S1 |
| 2 | `U02_C1_Entrez_Search_from_Python` | `Bio.Entrez` esearch/efetch for HBB; the same query as on the website; field tags; saved-copy fallback | Build five queries and record counts | Entrez field tags, identifiers, RefSeq prefixes | L3–L4, S2–S3 |
| 3 | `U03_C1_Inside_a_Sequence_Record` | Load a GenBank record with `SeqIO`; map id, description, annotations and features onto Seq-id, Seq-descr and Seq-feat | Pull organism, molecule type and references out of two records | NCBI data model terms matched to parts of a record | L5–L6 |
| 4 | `U04_C1_GenBank_Flat_File` · `U04_C2_Formats_and_Conversion` | Walk the features table; extract the CDS and translate it; convert GenBank ↔ FASTA ↔ EMBL | Extract CDS coordinates and protein length for *INS* and *TP53* | Flat-file sections, location syntax, primary vs secondary databases | L7–L9, S4–S5 |
| 5 | `U05_C1_Dot_Plots_and_Global_Alignment` · `U05_C2_Local_Alignment_and_Scoring` · `U05_C3_Reading_BLAST_Results` | Draw a dot plot; fill a Needleman–Wunsch matrix step by step on 6-residue sequences; `PairwiseAligner` with BLOSUM/PAM and gap penalties; load a saved BLAST table and filter by E-value, identity, coverage | Hand-fill one matrix then confirm in code; effect of matrix and gap choice on HbA vs HbS and HBB vs MB | Global vs local, matrix choice, E-value and bit score, spotting a low-complexity artifact | L10–L15, S6–S7 |
| 6 | `U06_C1_Multiple_Alignment_and_Conservation` | Read the globin alignment with `AlignIO`; per-column conservation; consensus; plot conservation along the protein | Find the most conserved columns and relate them to haem-binding residues | MSA concepts, progressive alignment, reading an alignment | L16–L17, S8 |
| 7 | `U07_C1_Distances_and_Trees` | Distance matrix from the alignment; UPGMA on four taxa step by step; build and draw UPGMA and NJ trees with `Bio.Phylo` | Build a tree for a second gene family; identify the paralogue pair | Tree vocabulary, orthologue vs paralogue, bootstrap meaning | L18–L20, S8 |
| 8 | `U08_C1_ORFs_GC_and_Codon_Usage` | Six-frame translation; ORF finding with a length threshold; GC content in windows; codon usage table | ORF map and codon usage for one supplied gene | Reading frames, functional sites, codon bias | L21–L22, S9 |
| 9 | `U09_C1_Protein_Properties_and_Motifs` · `U09_C2_Secondary_Structure_Prediction_Scoring` | `ProtParam`: weight, pI, GRAVY; hydropathy plot of HBB vs a membrane protein; PROSITE patterns as regular expressions; compare saved GOR and PSIPRED strings with the real structure and compute Q3 | Property sheet for three proteins; find one PROSITE motif | Properties from sequence, motif syntax, Q3, fold classes | L23–L25, S10–S11 |
| 10 | `U10_C1_Reading_a_PDB_File` | Parse 1A3N with `Bio.PDB`: chains, residues, atoms, hetero groups; distance between two residues; residues near the haem | Same analysis on 2HBS; locate residue 6 | PDB records, resolution, viewers, structure vs sequence conservation | L26–L28, S12–S13 |
| 11 | `U11_C1_Comparing_Two_Genomes` | Two small viral genomes from `data/`: size, GC, gene count, shared genes from a saved BLAST table | Repeat for a second pair | Annotation and comparative genomics terms | L29–L30 |

**Count:** 15 course, 11 practice, 11 quiz notebooks, plus 11 practice solutions and 11 quiz keys.

### Extra data these notebooks need

Add to `data/` (and to the checklist in §9): the globin alignment and a second gene-family alignment (FASTA/Clustal), saved BLAST result tables for HBB (tabular format), saved GOR and PSIPRED prediction strings with the DSSP string for HBB, saved Entrez responses for the offline fallback, and two small viral genomes in GenBank format.

### Build order

1. `U01_C1` first, and test it on a real student or a colleague who does not code: everything later depends on it being enough.
2. Units 2–5 before week 1 of teaching, since they cover the first half of the semester.
3. For each unit: course notebook → practice solution → practice student copy → quiz key → quiz student copy.
4. Units 6–11 before week 8.

### Progress tracker

| Unit | C | P | P solutions | Q | Q key |
|---|---|---|---|---|---|
| 1 | ☑ | ☑ | ☑ | ☑ | ☑ |
| 2 | ☑ | ☑ | ☑ | ☑ | ☑ |
| 3 | ☑ | ☑ | ☑ | ☑ | ☑ |
| 4 | ☑ ☑ | ☑ | ☑ | ☑ | ☑ |
| 5 | ☑ ☑ ☑ | ☑ | ☑ | ☑ | ☑ |
| 6 | ☑ | ☑ | ☑ | ☑ | ☑ |
| 7 | ☑ | ☑ | ☑ | ☑ | ☑ |
| 8 | ☑ | ☑ | ☑ | ☑ | ☑ |
| 9 | ☑ ☑ | ☑ | ☑ | ☑ | ☑ |
| 10 | ☑ | ☑ | ☑ | ☑ | ☑ |
| 11 | ☑ | ☑ | ☑ | ☑ | ☑ |
