# Practical 09: Computational Analysis of DNA Sequences (ORFs, EMBOSS Suite, and Repeat Detection)

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S09 (Syllabus Practical P7)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO6 — Predict sequence features, detect Open Reading Frames (ORFs) across 6 frames, quantify base composition and codon usage bias, and identify repetitive genomic elements.

---

## 1. Aim & Objectives

### Aim
To perform comprehensive sequence feature characterization on nucleotide records using NCBI ORFfinder, the EMBOSS bioinformatics analysis suite (`geecee`, `cusp`, `transeq`, `cpgplot`), and RepeatMasker, evaluating base composition, codon usage bias, six-frame translations, and genomic repeat architectures.

### Objectives
1. Analyze the six reading frames (3 forward: $+1, +2, +3$; 3 reverse: $-1, -2, -3$) of double-stranded DNA.
2. Predict Open Reading Frames in the human beta-globin mRNA (`NM_000518.5`) using NCBI ORFfinder, identifying the authentic biological coding sequence (`51..494`) among spurious alternative ORFs.
3. Quantify overall base composition and localized GC percentage using EMBOSS `geecee`.
4. Generate a codon usage frequency and bias table for *HBB* using EMBOSS `cusp` and interpret synonymous codon selection.
5. Identify CpG islands (unmethylated regulatory clusters in promoters) using EMBOSS `cpgplot`.
6. Contrast eukaryotic monocistronic gene organization against the overlapping gene architecture of Bacteriophage $\Phi$X174 (`phix174.fasta`).
7. Understand repetitive DNA masking using RepeatMasker to detect SINEs (Alu), LINEs, and simple tandem repeats.

---

## 2. Background & Scientific Principle

### The Six Reading Frames of DNA
Because DNA is a double-stranded antiparallel helix and the genetic code is read in non-overlapping triplets (codons), any unannotated nucleotide sequence possesses **six possible reading frames**:
- **Forward Frames:** Reading the top strand ($5' \rightarrow 3'$) beginning at nucleotide 1 (Frame $+1$), nucleotide 2 (Frame $+2$), or nucleotide 3 (Frame $+3$).
- **Reverse Frames:** Reading the reverse complement strand ($5' \rightarrow 3'$) beginning at nucleotide 1 (Frame $-1$), nucleotide 2 (Frame $-2$), or nucleotide 3 (Frame $-3$).

An **Open Reading Frame (ORF)** is a continuous stretch of codons beginning with an initiation codon (typically `ATG` encoding Met in the standard genetic code) and ending with a canonical in-frame stop codon (`TAA`, `TAG`, or `TGA`), with no intervening stop codons. In long random DNA sequences with 50% GC content, a stop codon occurs on average every $64/3 \approx 21$ codons. Therefore, any un-interrupted ORF encoding $>100$ amino acids has a high probability of representing a genuine protein-coding gene.

### Codon Usage Bias
Although the genetic code is degenerate (18 of the 20 standard amino acids are encoded by two to six synonymous codons), organisms and individual highly expressed genes do not utilize synonymous codons with equal frequency. This phenomenon is termed **codon usage bias**.
- In highly expressed human genes like *HBB*, codons matching the most abundant cellular tRNA species (often GC-ending codons such as `GTG` for Val, `CTG` for Leu, `GAG` for Glu) are strongly enriched to maximize translation elongation speed and ribosomal fidelity.
- Measuring codon bias is crucial in synthetic biology and recombinant protein expression: expressing a human gene in *E. coli* frequently requires "codon optimization" to replace human-preferred codons with bacterial-preferred codons.

### Repetitive DNA and the Necessity of Masking
In eukaryotic genomes, repetitive elements constitute a vast fraction of nuclear DNA (over 50% of the human genome):
- **Interspersed Repeats:** Retrotransposons including Short Interspersed Nuclear Elements (SINEs, e.g., ~1 million *Alu* copies), Long Interspersed Nuclear Elements (LINEs, e.g., LINE-1), and LTR retroviruses.
- **Tandem Repeats:** Satellite DNA, minisatellites, and microsatellites (Short Tandem Repeats, STRs).
When performing sequence similarity searches (BLAST) or *de novo* genome assemblies, unmasked repetitive elements produce astronomical numbers of spurious, biologically meaningless matches. Programs like **RepeatMasker** screen sequence queries against libraries of known repetitive motifs (RepBase) and "mask" them (replacing repeat nucleotides with `N`s or lower-case letters) prior to downstream analysis.

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & Software
- NCBI ORFfinder: [https://www.ncbi.nlm.nih.gov/orffinder/](https://www.ncbi.nlm.nih.gov/orffinder/)
- EMBOSS Online Services / Local EMBOSS Suite (`geecee`, `cusp`, `transeq`, `cpgplot`): [https://www.ebi.ac.uk/Tools/emboss/](https://www.ebi.ac.uk/Tools/emboss/)
- RepeatMasker Web Server: [https://www.repeatmasker.org/cgi-bin/WEBRepeatMasker](https://www.repeatmasker.org/cgi-bin/WEBRepeatMasker)

### Input Datasets
- Human *HBB* mRNA: `../../data/sequences/hbb_human_mrna.fasta` (`NM_000518.5`, 626 bp).
- Bacteriophage $\Phi$X174 Genome: `../../data/genomes/phix174.fasta` (`NC_001422.1`, 5386 bp).
- Human *HBB* CDS: `../../data/sequences/hbb_human_cds.fasta`.

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Predicting Open Reading Frames with NCBI ORFfinder
1. Open [https://www.ncbi.nlm.nih.gov/orffinder/](https://www.ncbi.nlm.nih.gov/orffinder/).
2. Paste the sequence from `../../data/sequences/hbb_human_mrna.fasta`.
3. Configure search parameters:
   - Minimal ORF length: Set to **75 nt** (25 aa).
   - Genetic code: **1. Standard**.
   - ORF start codon to use: Select **"ATG only"** (canonical).
4. Click **Submit**.
5. Examine the graphical six-frame display:
   - Note the three positive frames ($+1, +2, +3$) and three negative frames ($-1, -2, -3$).
   - Identify the largest predicted ORF (colored cyan/blue):
     - Frame: `+3` (or `+1` depending on coordinates)
     - Coordinates: `51..494`
     - Length: `444 nt` (147 aa)
   - Inspect the smaller background ORFs (e.g., in reverse frames or alternate frames). Notice how short they are ($<100$ bp) due to frequent random stop codons.
6. Click on the largest ORF to view its translated amino acid sequence (`MVHLTPEEKS...`). Confirm that it is 100% identical to RefSeq `NP_000509.1`.

### Phase 2: Base Composition and GC Content Analysis with EMBOSS `geecee`
1. Open the EMBOSS `geecee` web tool (or run in terminal):
   ```bash
   geecee -sequence ../../data/sequences/hbb_human_mrna.fasta -outfile hbb_gc.txt
   ```
2. Inspect the output file:
   - Record the total sequence length (626 bp).
   - Record the total count of G and C nucleotides.
   - Record the calculated percentage GC content.
3. Compare this against the coding region (`../../data/sequences/hbb_human_cds.fasta`):
   ```bash
   geecee -sequence ../../data/sequences/hbb_human_cds.fasta -outfile hbb_cds_gc.txt
   ```
   Note whether the coding sequence is more GC-rich than the overall transcript.

### Phase 3: Codon Usage Bias Analysis with EMBOSS `cusp`
1. Run EMBOSS `cusp` to calculate the codon usage table of human *HBB* CDS:
   ```bash
   cusp -sequence ../../data/sequences/hbb_human_cds.fasta -outfile hbb_codon_usage.cusp
   ```
2. Open `hbb_codon_usage.cusp` in a text editor:
   - Locate the codons encoding **Valine (Val / V)**: `GTT`, `GTC`, `GTA`, `GTG`.
     - Record the count and fraction for each.
     - Observe that `GTG` is the predominantly utilized codon.
   - Locate the codons encoding **Leucine (Leu / L)**: `TTA`, `TTG`, `CTT`, `CTC`, `CTA`, `CTG`.
     - Observe that `CTG` is heavily favored.
   - Locate the codons encoding **Glutamic acid (Glu / E)**: `GAA` vs. `GAG`.
     - Observe the preference for `GAG`.

### Phase 4: Overlapping Genes in Bacteriophage $\Phi$X174
1. Open NCBI ORFfinder in a new tab.
2. Paste the circular genome of Bacteriophage $\Phi$X174 from `../../data/genomes/phix174.fasta`.
3. Set minimal length to **150 nt** and click **Submit**.
4. Examine the output:
   - Locate Gene B embedded entirely inside the coding region of Gene A, but translated in an alternate reading frame ($+1$ vs $+2$).
   - Locate Gene E embedded inside Gene D.
   - Explain how viral genomes maximize coding capacity under extreme physical capsid volume constraints.

### Phase 5: Repetitive Element Detection with RepeatMasker
1. Navigate to the RepeatMasker web server: `https://www.repeatmasker.org/cgi-bin/WEBRepeatMasker`.
2. Input a 2 kb genomic locus flanking human *HBB* (or paste the genomic sequence from `NC_000011.10:5224000-5228000`).
3. Select DNA source: **Human**.
4. Select Speed/Sensitivity: **Default**.
5. Submit and inspect the repeat summary table:
   - Identify SINEs (AluSx, AluJb) and LINEs (L1).
   - Observe how RepeatMasker masks repeats by converting retrotransposon bases into lowercase or `N` characters.

---

## 5. Offline Fallback Note

If web servers are inaccessible:
- The EMBOSS suite commands (`geecee`, `cusp`, `transeq`) execute entirely offline in the local terminal environment using files in `../../data/sequences/`.
- Alternatively, use Python scripts with Biopython to calculate GC content and codon frequency tables as documented in the instructor answer key.

---

## 6. Observations Table

### Table 9.1: ORFfinder Prediction Summary for Human *HBB* mRNA (`NM_000518.5`)
| ORF Rank | Reading Frame ($+1$ to $-3$) | Start Coordinate | Stop Coordinate | Length (nt) | Length (aa) | Matches Curated Protein? (Yes/No) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| **ORF 1 (Primary)** | | 51 | 494 | 444 | 147 | Yes (`NP_000509.1`) |
| **ORF 2** | | | | | | |
| **ORF 3** | | | | | | |
| **ORF 4** | | | | | | |

### Table 9.2: EMBOSS `geecee` and `cusp` Codon Usage Profile for *HBB* CDS
| Amino Acid | Codon | Total Count in HBB | Frequency per 1000 | Fraction (Relative Synonymous Usage) |
|---|:---:|:---:|:---:|:---:|
| **Valine (Val)** | `GTG` | | | |
| | `GTC` | | | |
| | `GTT` | | | |
| | `GTA` | | | |
| **Glutamic Acid (Glu)** | `GAG` | | | |
| | `GAA` | | | |
| **Leucine (Leu)** | `CTG` | | | |
| | `CTC` | | | |
| Overall % GC (mRNA) | — | — | — | |
| Overall % GC (CDS) | — | — | — | |

---

## 7. Interpretation & Discussion Questions

1. **Biological Significance of 5' and 3' UTRs:** The predicted functional ORF spans coordinates `51..494` in a 626 bp mRNA. What are the biological functions of the 50 bp 5' UTR and the 132 bp 3' UTR that do not code for amino acids?
2. **Kozak Consensus Context:** What sequence motif surrounds the authentic initiation codon at base 51 (`accatgG`)? Explain the role of the eukaryotic Kozak consensus sequence in ribosome scanning.
3. **Translational Selection and Codon Bias:** Why does the highly expressed beta-globin gene overwhelmingly favor `CTG` over `CTA` for leucine, and `GTG` over `GTA` for valine? How does this correlate with cellular tRNA abundance?
4. **Overlapping Reading Frames in Viruses:** In Bacteriophage $\Phi$X174, Gene B is translated within the same physical DNA sequence as Gene A, but in a different reading frame. How does a single nucleotide mutation in this overlapping region impact both viral proteins simultaneously?
5. **RepeatMasker in NGS Pipelines:** Why is running RepeatMasker a mandatory first step before assembling mammalian whole-genome sequencing reads or executing genome-wide BLAST searches? What happens if repetitive elements are left unmasked?

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Write a Python script using Biopython to compute the **Relative Synonymous Codon Usage (RSCU)** for all four Valine codons in `hbb_human_cds.fasta`.
2. Recall that:
   $$\text{RSCU} = \frac{X_{ij}}{\frac{1}{n_i} \sum_{j=1}^{n_i} X_{ij}}$$
   where $X_{ij}$ is the observed count of the $j$-th codon for the $i$-th amino acid, and $n_i$ is the degeneracy (number of synonymous codons, $n_i=4$ for Val).
3. Confirm that an RSCU value $>1.0$ indicates positive codon preference, while $<1.0$ indicates codon avoidance.
