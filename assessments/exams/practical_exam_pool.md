# Practical Examination Pool & Viva Voce Question Bank

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Total Marks:** 50 Marks (Scaled to 10% Continuous Assessment)  
**Examination Duration:** 2 Hours (In-lab terminal and browser tasks)  
**Examination Architecture:**
* **Part A:** One Information Retrieval & Data Handling Task drawn by lottery (15 Marks)
* **Part B:** One Computational Analysis / Alignment / Structure Task drawn by lottery (20 Marks)
* **Part C:** Oral Viva Voce Examination based on the Viva Question Bank (15 Marks)

---

## Section 1: Examination Administration & Rules

1. Each student draws a random token corresponding to **One Task from Part A** (Tasks 01–07) and **One Task from Part B** (Tasks 08–15).
2. Students must document their complete terminal command history, exact database queries, software parameters, tabular results, and biological conclusions on the official Practical Exam Answer Sheet.
3. If public web servers experience downtime, students must utilize the local offline mirror files stored in `data/` and `data/expected/`.
4. The oral Viva Voce is conducted individually by the instructor during or immediately following task completion.

---

## Section 2: Pool of 15 Randomized Practical Lab Tasks

### Part A Tasks: Information Retrieval & Data Handling (15 Marks Each)

#### Task 01: Targeted Entrez Gene & Literature Retrieval
* **Aim:** Execute an advanced Entrez search to retrieve curated mRNA and literature records for the human cystic fibrosis transmembrane conductance regulator (*CFTR*) gene.
* **Procedure:**
  1. Formulate an Entrez Nucleotide query to retrieve only reviewed RefSeq mRNA records (`NM_...`) for human *CFTR*, excluding genomic contigs.
  2. Record the exact query string, result count, and primary RefSeq accession number.
  3. Formulate an Entrez PubMed query combining the MeSH term for cystic fibrosis with field-tagged search for therapeutic drugs (e.g., ivacaftor or lumacaftor) published between 2020 and 2023. Record the first 3 PMIDs.
* **Deliverables:** Documented query strings, RefSeq accession, and PMID table with brief abstracts.

#### Task 02: GenBank Flat File Feature Anatomy & CDS Extraction
* **Aim:** Dissect the complete GenBank flat file of human beta-globin (*HBB*, RefSeq: `NM_000518.5`) and extract its coding sequence.
* **Procedure:**
  1. Retrieve the full GenBank flat file for `NM_000518.5`.
  2. Identify and record: Locus name, molecule type, length, GenBank division, publication citation (authors, title, journal), and gene map location.
  3. In the `FEATURES` table, locate the `CDS` coordinates and `/codon_start`. Calculate the exact base pair length of the coding sequence and the expected amino acid length.
  4. Copy the raw nucleotide sequence of the CDS and translate it into amino acids; verify against `/protein_id="NP_000509.1"`.
* **Deliverables:** Annotated table of flat-file sections and verified peptide translation.

#### Task 03: Primary vs Secondary Protein Database Comparison
* **Aim:** Compare the representation of human insulin (*INS*) between a primary translation database (NCBI Protein) and a curated secondary database (UniProtKB/Swiss-Prot).
* **Procedure:**
  1. Retrieve the NCBI Protein record for human insulin (`NP_000198.1`).
  2. Retrieve the UniProtKB/Swiss-Prot record for human insulin (`P01308`).
  3. Construct a comparative table evaluating: record ownership, level of curation, sequence length, post-translational processing annotations (signal peptide, B-chain, C-peptide, A-chain), and cross-references to 3D PDB structures.
* **Deliverables:** Comparison table and detailed explanation of why RefSeq/Swiss-Prot curation is essential for biomedical research.

#### Task 04: Sequence File Format Conversion using EMBOSS seqret
* **Aim:** Perform automated universal file format conversions and integrity checks on biological sequence records.
* **Procedure:**
  1. Download or locate a multi-record GenBank file (`sequences.gb`) containing globin transcripts.
  2. Using EMBOSS `seqret`, execute terminal commands to convert the GenBank file into:
     - FASTA format (`output.fasta`)
     - EMBL format (`output.embl`)
     - GCG format (`output.gcg`)
  3. Inspect the GCG file and extract the mathematical `Check:` checksum integer. Explain how the checksum guarantees transmission integrity.
* **Deliverables:** Command log, converted files, and technical description of header structures.

#### Task 05: NCBI Entrez History & E-Utilities Command Pipeline
* **Aim:** Execute automated batch sequence retrieval using NCBI EDirect / E-utilities command-line tools.
* **Procedure:**
  1. In the terminal, execute `esearch -db nuccore -query "HBB[GENE] AND human[ORGN] AND biomol_mrna[PROP]"` piped to `efilter` and `efetch`.
  2. Download the record in FASTA format directly using `efetch -format fasta`.
  3. Download the record in GenBank flat-file text using `efetch -format gb`.
  4. Explain the roles of the server parameters `WebEnv` and `QueryKey` in maintaining session history without client data re-transmission.
* **Deliverables:** Executable command-line log and retrieved sequence files.

#### Task 06: Linux Shell Data Wrangling on Genomic FASTQ/FASTA Files
* **Aim:** Perform high-throughput sequence file manipulation using Linux terminal utilities.
* **Procedure:**
  1. Given a multi-FASTA file in the terminal:
     - Count the exact number of sequence records using `grep -c "^>"`.
     - Extract all sequence header lines and save them to `headers.txt`.
     - Calculate the total residue count of all sequences combined using `grep -v "^>" | tr -d '\n' | wc -c`.
  2. Extract a specific sequence record by its accession ID using `awk` or `sed`.
* **Deliverables:** Command log showing pipes (`|`), redirection (`>`), and correct numerical sequence counts.

#### Task 07: Unmasking and Analyzing Eukaryotic Interspersed Repeats
* **Aim:** Identify and mask repetitive DNA elements in a human genomic contig using RepeatMasker.
* **Procedure:**
  1. Retrieve a 10 kb unmasked human genomic segment containing an exon of the *HBB* gene cluster.
  2. Run RepeatMasker (or inspect saved RepeatMasker tabular output).
  3. Identify all detected transposable elements, classifying them into SINEs (*Alu*), LINEs (*L1*), and simple tandem repeats.
  4. Calculate the total percentage of the 10 kb contig occupied by repetitive DNA.
* **Deliverables:** RepeatMasker summary table and annotated masked FASTA output.

---

### Part B Tasks: Computational Analysis, Alignment & Modeling (20 Marks Each)

#### Task 08: BLAST Parameter Optimization & Heuristic Tuning
* **Aim:** Evaluate the sensitivity of `blastp` searches by altering substitution matrices, word sizes, and filtering parameters.
* **Procedure:**
  1. Query human myoglobin (`P02144`) against the `nr` database using default parameters (`BLOSUM62`, Word size $W=3$, threshold $T=11$).
  2. Repeat the search using `BLOSUM45` (for distant homologues) and `PAM30` (for closely related proteins).
  3. Repeat the search with and without the `SEG` low-complexity filter.
  4. Tabulate the bit scores and $E$-values for the top bacterial or plant globin hit across the three conditions.
* **Deliverables:** Comparative BLAST table and written explanation of how matrix choice dictates evolutionary reach.

#### Task 09: Heuristic Comparison: BLAST vs FASTA
* **Aim:** Execute a head-to-head performance and sensitivity comparison between NCBI BLAST and EBI FASTA.
* **Procedure:**
  1. Using the human insulin sequence (`P01308`), perform a `blastp` search at NCBI.
  2. Perform a `fasta36` search at EMBL-EBI using the same query against UniProtKB.
  3. Compare the top 5 hits: inspect alignment boundaries, gap placement, bit scores, and $E$-values.
  4. Explain the difference between BLAST's neighborhood word extension and FASTA's $ktup$ diagonal hashing.
* **Deliverables:** Comparative hit table and algorithmic critique.

#### Task 10: Multiple Sequence Alignment & Conservation Mapping in Jalview
* **Aim:** Build and annotate a publication-quality multiple sequence alignment of the vertebrate globin family.
* **Procedure:**
  1. Import the globin protein dataset (human HBB, HBA, HBG, MB, CYGB, NGB, and orthologues) into **Clustal Omega** or **MUSCLE**.
  2. Open the alignment in **Jalview**. Color by Clustalx and set a conservation threshold of 80%.
  3. Locate the proximal histidine (F8) and distal histidine (E7). Mark these columns.
  4. Generate and export a Sequence Logo for the 10-residue window surrounding the proximal histidine.
* **Deliverables:** Rendered Jalview graphic with marked active site columns and Sequence Logo plot.

#### Task 11: Molecular Phylogenetic Reconstruction in MEGA
* **Aim:** Reconstruct and statistically evaluate a molecular phylogenetic tree from a multiple sequence alignment.
* **Procedure:**
  1. Load the vertebrate globin alignment into **MEGA 11**.
  2. Reconstruct a phylogenetic tree using **Neighbor-Joining (NJ)** under the JTT substitution model with pairwise deletion.
  3. Execute **Bootstrap Testing** with 500 replicates.
  4. Root the tree using human neuroglobin (*NGB*) or myoglobin (*MB*) as the outgroup.
  5. Label which internal nodes represent gene duplications (paralogues) and which represent speciation events (orthologues).
* **Deliverables:** Rooted phylogenetic tree diagram with bootstrap values and evolutionary node labels.

#### Task 12: In Silico DNA Characterisation: ORFs, Codon Bias & CpG Islands
* **Aim:** Perform a complete structural and composition analysis of an uncharacterized nucleotide contig.
* **Procedure:**
  1. Given a 2,000 bp uncharacterized bacterial/viral sequence:
     - Run NCBI ORFfinder (min length 150 bp); record all detected ORFs across 6 frames.
     - Calculate overall GC content and GC3 (third codon position GC%).
     - Compute the Codon Adaptation Index (CAI) or Effective Number of Codons ($N_c$) using EMBOSS `cusp` / `chips`.
  2. Scan the sequence for CpG islands (length $\ge 200\text{ bp}$, $\%GC \ge 50\%$, Obs/Exp CpG $\ge 0.60$).
* **Deliverables:** ORF coordinate map, codon usage table, and CpG island evaluation report.

#### Task 13: Protein Physicochemical Profiling with Expasy ProtParam
* **Aim:** Determine the complete physicochemical profile of human haemoglobin beta and predict its solubility.
* **Procedure:**
  1. Submit the human HBB protein sequence (`P68871`) to Expasy **ProtParam**.
  2. Record: Molecular weight, theoretical pI, amino acid composition, atomic formula, extinction coefficient, estimated half-life, instability index, aliphatic index, and GRAVY score.
  3. Generate a Kyte–Doolittle hydropathy plot via **ProtScale** (window size 9).
  4. Compare the HBB profile with a known transmembrane receptor (e.g., human rhodopsin `P08100`), contrasting their GRAVY scores and hydropathy peaks.
* **Deliverables:** Detailed property sheet and comparative hydropathy plot analysis.

#### Task 14: Secondary Structure Prediction and Q3 Benchmark
* **Aim:** Predict secondary structure using GOR IV and benchmark its accuracy against experimental crystal structure ground truth.
* **Procedure:**
  1. Submit the human HBB sequence to the **GOR IV** server (NPS@). Record the predicted percentages of Helix ($H$), Sheet ($E$), and Coil ($C$).
  2. Retrieve the true DSSP secondary structure string from PDB `1A3N`.
  3. Align the GOR IV prediction string against the DSSP string for a 30-residue segment.
  4. Count the number of identical secondary structure assignments and compute the three-state accuracy metric:  
     $$Q_3 = \frac{\text{Correct Predictions}}{\text{Total Residues}} \times 100\%$$
* **Deliverables:** Aligned prediction strings, confusion matrix count, and calculated $Q_3$ percentage.

#### Task 15: 3D Macromolecular Visualisation & Active Site Measurement in VMD
* **Aim:** Parse an experimental PDB structure, measure active site geometric bond distances, and render a publication graphic.
* **Procedure:**
  1. Download PDB `1A3N` (deoxyhemoglobin) and open it in **VMD** (or **PyMOL** / **Mol***).
  2. Create representation 1: NewCartoon representation of Chain A, colored by secondary structure.
  3. Create representation 2: Licorice/Sticks representation of the Heme group (`resname HEM`) and proximal Histidine 92 (`resid 92`), colored by atom name (CPK).
  4. Using the distance measurement tool, measure the bond distance between the `NE2` nitrogen atom of His92 and the central `FE` iron atom. Confirm that it measures between $2.1\text{ \AA}$ and $2.4\text{ \AA}$.
* **Deliverables:** High-resolution rendered 3D image with labeled bond measurement and structural caption.

---

## Section 3: Viva Voce Question Bank (30 Questions)

### Group 1: Internet & Biological Databases (Units 1–4)

**V01:** What is the fundamental difference between a Primary Database (like GenBank) and a Secondary Database (like RefSeq or Swiss-Prot)?  
* *Model Answer:* Primary databases archive original experimental data submitted by researchers without editorial modification (redundant, submitter-owned). Secondary databases derive curated, non-redundant, peer-reviewed reference records from primary data.

**V02:** What is the International Nucleotide Sequence Database Collaboration (INSDC), and how frequently do its nodes exchange data?  
* *Model Answer:* The INSDC comprises NCBI GenBank (USA), EMBL-EBI ENA (Europe), and DDBJ (Japan). They exchange new, revised, and retracted records automatically on a **daily** basis to ensure global data synchronization.

**V03:** Explain the anatomical structure of an NCBI RefSeq accession number. What do `NM_` and `NP_` represent?  
* *Model Answer:* RefSeq accessions feature two letters, an underscore, an integer, and a version suffix (`Prefix_Digits.Version`). `NM_` represents curated mRNA transcripts; `NP_` represents curated translated protein products.

**V04:** What is the Medical Subject Headings (MeSH) vocabulary, and what is "MeSH explosion" in PubMed?  
* *Model Answer:* MeSH is a curated, hierarchical indexing thesaurus. "Explosion" means searching a broad MeSH descriptor automatically retrieves all citations indexed under its narrower descendant branch terms.

**V05:** In the NCBI data model, what is a `Bioseq` and how does it differ from a `Bioseq-set`?  
* *Model Answer:* A `Bioseq` is the atomic data object storing an individual sequence and its metadata. A `Bioseq-set` is a container holding collections of sequences (such as a `nuc-prot` set bundling an mRNA with its translated protein).

**V06:** What does the delimiter `//` signify in a GenBank flat file?  
* *Model Answer:* `//` marks the formal end of a record, allowing computer parsers to distinguish entry boundaries in multi-record files.

---

### Group 2: Sequence Alignment & Database Searching (Unit 5)

**V07:** What is the biological distinction between homologous genes that are "orthologues" versus "paralogues"?  
* *Model Answer:* Orthologues diverged due to a **speciation event** and typically perform the same function in different species. Paralogues diverged due to an intragenomic **gene duplication event** and often evolve specialized or diverged functions.

**V08:** What is the primary difference in initialization and recurrence between Needleman–Wunsch and Smith–Waterman dynamic programming?  
* *Model Answer:* Needleman–Wunsch (global) initializes borders with cumulative gap penalties and forces end-to-end alignment. Smith–Waterman (local) initializes with zeros and includes a zero lower bound ($F = \max\{0, \dots\}$), resetting negative scores to find the highest-scoring local sub-alignment.

**V09:** Why is an affine gap penalty model ($W_g + (k-1)W_s$) biologically superior to a linear gap penalty model ($k \cdot d$)?  
* *Model Answer:* Opening an insertion/deletion requires a rare mutational event (high penalty $W_g$), whereas extending an existing gap by additional residues often happens in that same single event (low penalty $W_s$).

**V10:** How do the numbering scales of PAM and BLOSUM substitution matrices differ when aligning distant homologues?  
* *Model Answer:* In PAM matrices, larger numbers denote greater evolutionary divergence (e.g., PAM250 for distant homologues). In BLOSUM matrices, smaller numbers denote greater divergence (e.g., BLOSUM45 for distant homologues; BLOSUM80 for close homologues).

**V11:** In Karlin–Altschul statistics, what does the $E$-value represent, and what threshold typically denotes biological significance?  
* *Model Answer:* The $E$-value is the number of chance alignments with score $\ge S$ expected in a database of size $N$. $E$-values $<10^{-3}$ or $<10^{-5}$ typically indicate statistically significant homology.

**V12:** What happens to the bit score and the $E$-value if the database size doubles?  
* *Model Answer:* The bit score remains **constant** (it is a normalized score independent of search space). The $E$-value **doubles** ($E \propto n$).

**V13:** What are the three heuristic steps in a standard BLASTp search?  
* *Model Answer:* 1. Seeding: generating words of length $W$ ($W=3$) scoring $\ge T$. 2. Ungapped extension: extending seeds until score drops by $X$. 3. Gapped extension: triggering banded dynamic programming to join HSPs.

**V14:** What biological problem do low-complexity regions cause in BLAST, and what tool masks them?  
* *Model Answer:* Biased, repetitive amino acid runs align with high scores by chance, generating spurious low $E$-values. The **SEG** program filters them by replacing biased residues with 'X's.

---

### Group 3: Multiple Sequence Alignment & Molecular Phylogenetics (Units 6–7)

**V15:** Why is exact multidimensional dynamic programming impossible for aligning 50 protein sequences?  
* *Model Answer:* It has a time and memory complexity of $O(L^N)$, which is NP-complete and computationally intractable for $N=50$.

**V16:** What is the "once a gap, always a gap" limitation in progressive alignment?  
* *Model Answer:* Progressive aligners make greedy decisions: gaps introduced in early pairwise alignments are frozen and cannot be repositioned when more sequences are merged later.

**V17:** How does Clustal Omega achieve scalability for over 100,000 sequences?  
* *Model Answer:* It uses the $mBed$ seed embedding algorithm to generate guide trees in $O(N \log N)$ time rather than calculating all $O(N^2)$ pairwise alignments, and uses HHalign HMM profile alignments.

**V18:** How does MUSCLE correct early progressive alignment errors?  
* *Model Answer:* It uses **iterative refinement**: it systematically cuts guide tree edges, divides the alignment into two sub-profiles, and realigns them via profile-profile dynamic programming, retaining improvements in Log-Expectation score.

**V19:** What does a bootstrap value of 95% at an internal phylogenetic node mean?  
* *Model Answer:* It means that across 95% of resampled pseudo-replicate alignments generated with replacement, the descendant taxa clustered together as an exclusive clade, indicating strong statistical confidence.

**V20:** Why does UPGMA produce an incorrect tree topology when sequences violate the molecular clock?  
* *Model Answer:* UPGMA assumes equal substitution rates (ultrametricity). If one lineage evolves significantly faster, UPGMA incorrectly groups slow-evolving lineages together. Neighbor-Joining avoids this using rate-correction matrices ($Q$-matrices).

---

### Group 4: Predictive Sequence Methods (Units 8–9)

**V21:** Why does double-stranded DNA have exactly six potential reading frames?  
* *Model Answer:* Codons are triplets, yielding three reading phases (+1, +2, +3) per strand. Because DNA is an anti-parallel double helix with genes on either strand, the reverse-complement strand has three additional frames (-1, -2, -3).

**V22:** What are the canonical dinucleotides at the 5' donor and 3' acceptor splice junctions of eukaryotic introns?  
* *Model Answer:* Invariant **GT** (or GU in RNA) at the 5' donor site, and invariant **AG** at the 3' acceptor site.

**V23:** What are the criteria defining a genomic CpG island?  
* *Model Answer:* A sequence window of length $\ge 200\text{ bp}$, with GC content $\ge 50\%$, and an Observed-to-Expected CpG ratio $\ge 0.60$.

**V24:** Why are CpG dinucleotides depleted across the bulk vertebrate genome?  
* *Model Answer:* Cytosines in CpGs are methylated to 5-methylcytosine, which spontaneously deaminates into thymine ($C \rightarrow T$ transitions) that frequently escape DNA repair.

**V25:** What does an Instability Index value $<40$ vs $>40$ indicate in ProtParam?  
* *Model Answer:* Guruprasad's instability index classifies values $<40$ as stable in vitro, and $>40$ as unstable in vitro.

**V26:** What does a positive GRAVY score indicate about a protein's physical property?  
* *Model Answer:* A positive GRAVY score indicates the protein is **hydrophobic** (characteristic of integral membrane proteins), whereas a negative score indicates hydrophilicity (soluble globular proteins).

**V27:** What does the $Q_3$ metric measure in secondary structure prediction?  
* *Model Answer:* $Q_3$ is the percentage of all sequence residues whose predicted secondary structure state (Helix, Sheet, or Coil) correctly matches experimental DSSP ground truth: $Q_3 = \frac{N_H + N_E + N_C}{N_{\text{total}}} \times 100\%$.

---

### Group 5: Structure Databases & Comparative Genomics (Units 10–11)

**V28:** What is the difference between an `ATOM` record and a `HETATM` record in a PDB file?  
* *Model Answer:* `ATOM` records coordinates of standard polymeric biomolecules (amino acids and nucleotides). `HETATM` records non-polymer hetero groups (water, ions, ligands, heme prosthetic groups).

**V29:** In X-ray crystallography, what does an $R$-value of 0.18 and a resolution of 1.5 Angstroms indicate?  
* *Model Answer:* Resolution of $1.5\text{ \AA}$ indicates a high-resolution structure where individual atoms and water molecules are clearly resolved. An $R$-value of $0.18$ ($18\%$) indicates excellent agreement between the atomic model and observed experimental X-ray diffraction amplitudes.

**V30:** What computational lines of evidence identify a horizontally transferred Pathogenicity Island (PAI) in a bacterial genome?  
* *Model Answer:* 1. Anomalous GC content deviating from host genome average. 2. Atypical codon usage bias. 3. Flanking direct repeats and integration adjacent to a tRNA gene. 4. Presence of mobility genes (integrase/transposase) and virulence factors.

---

## Section 4: Analytical Practical Exam Grading Rubric (50 Marks)

| Assessment Component | Maximum Marks | Evaluation Criteria |
| :--- | :---: | :--- |
| **Part A: Retrieval & Data Handling Task** | **15 Marks** | Accurate command/query execution (5); correct identification of accessions, coordinates, or file sections (5); biological interpretation and error-free output data (5). |
| **Part B: Computational Analysis / Structure Task** | **20 Marks** | Correct tool selection and parameter setup (5); accurate execution of alignment, phylogeny, prediction, or 3D rendering (8); mathematical correctness of calculations ($Q_3$, distance, $E$-value) (4); high-quality graphical presentation (3). |
| **Part C: Oral Viva Voce Examination** | **15 Marks** | Rapid, confident response to 3 selected viva questions (5 marks per question). Demonstrates deep conceptual understanding of algorithms, databases, and biological mechanisms. |
| **Total Practical Grade** | **50 Marks** | **Scaled to 10% Continuous Internal Assessment** |
