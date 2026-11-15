# Question Bank: Unit 8 — Predictive Methods using Nucleotide Sequence

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Syllabus Topic:** Introduction, Marking repetitive DNA, Database search, Codon bias detection, Detecting functional site in DNA  
**Primary Learning Outcome:** LO6 (Predict sequence features from nucleotide data: repeats, ORFs, codon bias, promoters, splice sites, CpG islands)  

---

## Section A: Multiple Choice Questions (15 MCQs)

### Q01
Why must eukaryotic genomic DNA sequences be processed through repeat-masking software (such as RepeatMasker) prior to executing automated gene prediction or database searches?  
a) Repetitive elements accelerate the speed of the computer processor to dangerous temperatures  
b) Interspersed transposable elements (e.g., SINEs and LINEs) and tandem repeats match thousands of unrelated genomic locations, generating massive computational noise and false-positive gene calls  
c) Repeats cause DNA polymerase to stop functioning during in vitro PCR  
d) RepeatMasker converts all purines into pyrimidines  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Interspersed transposable elements (e.g., SINEs and LINEs) and tandem repeats match thousands of unrelated genomic locations, generating massive computational noise and false-positive gene calls  
* **Rationale:** Nearly 50% of the human genome consists of repetitive elements (e.g., ~1 million Alu elements). Searching unmasked genomic DNA produces overwhelming numbers of non-homologous alignments against unrelated loci that share the same transposable element.

### Q02
How many possible reading frames must be inspected computationally when searching for Open Reading Frames (ORFs) in a newly sequenced double-stranded genomic DNA contig?  
a) 1  
b) 3  
c) 6  
d) 12  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** c) 6  
* **Rationale:** Double-stranded DNA possesses three forward reading frames (+1, +2, +3, offset by 0, 1, or 2 nucleotides) on the positive strand, and three reverse reading frames (-1, -2, -3) transcribed in the opposite $5' \rightarrow 3'$ direction on the reverse-complement strand.

### Q03
What defines an Open Reading Frame (ORF) in computational nucleotide sequence analysis?  
a) Any sequence of DNA that contains more than 50% GC content  
b) A contiguous stretch of codons beginning with an initiation codon (typically ATG), devoid of in-frame termination codons (TAA, TAG, TGA), and ending with an in-frame stop codon  
c) A DNA sequence that binds specifically to RNA polymerase II  
d) The non-coding region located between the promoter and the transcription start site  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) A contiguous stretch of codons beginning with an initiation codon (typically ATG), devoid of in-frame termination codons (TAA, TAG, TGA), and ending with an in-frame stop codon  
* **Rationale:** By definition, an ORF is an open translation window: starting with a start triplet (ATG in DNA), continuing uninterrupted in triplets, and terminated by one of the three canonical stop triplets (TAA, TAG, or TGA).

### Q04
Why is simple ORF-finding software (such as NCBI ORFfinder) highly effective for predicting genes in prokaryotic genomes (e.g., *E. coli*), but largely ineffective on un-spliced human genomic contigs?  
a) Bacteria use a completely different 4-letter genetic code than humans  
b) Bacterial genomes have high coding density with long, uninterrupted protein-coding ORFs, whereas eukaryotic protein-coding genes are interrupted by extensive non-coding introns that break ORFs into short exons  
c) Eukaryotes do not use ATG as a start codon  
d) Bacterial genes do not contain termination codons  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Bacterial genomes have high coding density with long, uninterrupted protein-coding ORFs, whereas eukaryotic protein-coding genes are interrupted by extensive non-coding introns that break ORFs into short exons  
* **Rationale:** Over 85% of a bacterial genome consists of continuous, uninterrupted protein-coding sequence. In humans, exons average only ~150 bp (~50 amino acids), which cannot be distinguished from random background non-coding stop-free intervals without splice-site modeling.

### Q05
What biological phenomenon is measured by the Codon Adaptation Index (CAI)?  
a) The rate of spontaneous point mutations per generation  
b) The degree to which synonymous codon usage in a target gene matches the preferred codon usage bias of highly expressed reference genes in that organism  
c) The percentage of codons that encode hydrophobic amino acids  
d) The number of codons present in the 5' untranslated region  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The degree to which synonymous codon usage in a target gene matches the preferred codon usage bias of highly expressed reference genes in that organism  
* **Rationale:** CAI (Sharp & Li, 1987) quantifies synonymous codon usage bias. It calculates the geometric mean of relative synonymous codon adaptiveness values against a reference set of highly expressed genes (e.g., ribosomal proteins), correlating directly with translational efficiency and mRNA expression levels.

### Q06
What is the Effective Number of Codons ($N_c$), and what does an $N_c$ value of 20 signify for a gene?  
a) The gene is exactly 20 nucleotides long  
b) Extreme codon usage bias, where only a single synonymous codon is exclusively used for each of the 20 amino acids  
c) Completely random and uniform codon usage across all 61 sense codons  
d) The protein contains exactly 20 alpha-helices  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Extreme codon usage bias, where only a single synonymous codon is exclusively used for each of the 20 amino acids  
* **Rationale:** The Effective Number of Codons ($N_c$, Wright 1990) ranges from 20 (extreme bias: only one codon used per amino acid) to 61 (no bias: all synonymous codons used with equal probability).

### Q07
Which consensus sequence motif in prokaryotic mRNA serves as the ribosome binding site, positioned approximately 6 to 10 nucleotides upstream of the start codon?  
a) Pribnow box (TATAAT)  
b) Shine–Dalgarno sequence (AGGAGGU)  
c) Kozak consensus (CCACCAUGG)  
d) Polyadenylation signal (AATAAA)  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Shine–Dalgarno sequence (AGGAGGU)  
* **Rationale:** The Shine–Dalgarno sequence (purine-rich consensus $5'\text{-AGGAGGU-}3'$) base-pairs directly with the complementary pyrimidine-rich sequence at the $3'$ end of the 16S ribosomal RNA in prokaryotes to position the 30S ribosomal subunit at the initiator AUG.

### Q08
In eukaryotic mRNAs, which sequence context surrounding the initiator AUG codon is recognized by the scanning 40S ribosomal subunit to optimize translation initiation (the Kozak consensus)?  
a) `TTGACA`  
b) `(gcc)gccRccAUGG` (where `R` is a purine, typically `A` at position -3 and `G` at +4)  
c) `TATAAA`  
d) `GT...AG`  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) `(gcc)gccRccAUGG` (where `R` is a purine, typically `A` at position -3 and `G` at +4)  
* **Rationale:** Marilyn Kozak established that eukaryotic translation initiation is strongly enhanced by the consensus $(gcc)gccRccAUGG$. A purine (ideally A) at position $-3$ and a guanine at position $+4$ (relative to the A of AUG at $+1$) are the most critical regulatory nucleotides.

### Q09
What are the almost universally invariant dinucleotides found at the 5' splice donor site and the 3' splice acceptor site of canonical eukaryotic nuclear pre-mRNA introns?  
a) `AT` at 5' donor and `GC` at 3' acceptor  
b) `GT` (or `GU` in RNA) at the 5' donor, and `AG` at the 3' acceptor  
c) `CA` at 5' donor and `TG` at 3' acceptor  
d) `GG` at 5' donor and `CC` at 3' acceptor  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) `GT` (or `GU` in RNA) at the 5' donor, and `AG` at the 3' acceptor  
* **Rationale:** The Chambon rule states that eukaryotic introns begin with an invariant $5'\text{-GT-}3'$ (donor splice junction) and terminate with an invariant $5'\text{-AG-}3'$ (acceptor splice junction). Rare non-canonical exceptions (e.g., GC-AG or AT-AC U12-type introns) account for $<1\%$ of junctions.

### Q10
What are the standard bioinformatics criteria established by Gardiner-Garden and Frommer to define a genomic "CpG island"?  
a) A window of at least 200 bp with GC content $\ge 50\%$ and an Observed/Expected CpG ratio $\ge 0.60$  
b) Any sequence containing exactly 100 consecutive cytosine residues  
c) A genomic region enriched in adenine and thymine with length $>1000\text{ bp}$  
d) A tandem repeat of `CG` dinucleotides exceeding 5,000 base pairs  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) A window of at least 200 bp with GC content $\ge 50\%$ and an Observed/Expected CpG ratio $\ge 0.60$  
* **Rationale:** Gardiner-Garden and Frommer (1987) formally defined CpG islands as DNA segments of length $\ge 200\text{ bp}$, with calculated GC content $\ge 50\%$, and a ratio of observed-to-expected CpG dinucleotides $\ge 0.60$. They typically mark unmethylated promoters of mammalian genes.

### Q11
Why are CpG dinucleotides severely underrepresented (depleted) across the bulk vertebrate genome, occurring at only ~20% of their expected statistical frequency?  
a) DNA polymerase cannot incorporate cytosine next to guanine  
b) Cytosines in CpG dinucleotides are frequently methylated to 5-methylcytosine, which undergoes spontaneous hydrolytic deamination to thymine, creating permanent $C \rightarrow T$ transition mutations if unrepaired  
c) Ribosomes degrade CpG dinucleotides during transcription  
d) CpG dinucleotides prevent histones from binding  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Cytosines in CpG dinucleotides are frequently methylated to 5-methylcytosine, which undergoes spontaneous hydrolytic deamination to thymine, creating permanent $C \rightarrow T$ transition mutations if unrepaired  
* **Rationale:** Unmethylated cytosine deaminates to uracil, which is easily recognized and excised by Uracil-DNA Glycosylase. However, methylated cytosine (5mC) deaminates directly into thymine, generating a $T:G$ mismatch that often escapes repair, permanently converting CpGs into TpGs over evolutionary time.

### Q12
What is the primary canonical hexamer polyadenylation signal sequence located ~10 to 30 nucleotides upstream of the cleavage and poly(A) addition site in mammalian pre-mRNAs?  
a) `TATAAA`  
b) `AATAAA`  
c) `TTGACA`  
d) `CCTGAC`  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) `AATAAA`  
* **Rationale:** The canonical polyadenylation signal in mammalian pre-mRNAs is $5'\text{-AAUAAA-}3'$ ($5'\text{-AATAAA-}3'$ in genomic DNA). It is bound by the Cleavage and Polyadenylation Specificity Factor (CPSF) to direct 3' end cleavage and polyadenylation.

### Q13
How do *ab initio* gene prediction algorithms (such as Genscan and Glimmer) predict gene structures without relying on homology matches in sequence databases?  
a) By downloading finished mRNA flat files from NCBI  
b) By utilizing probabilistic Hidden Markov Models (HMMs) parameterized on statistical properties of exons, introns, splice signals, branch sites, and hexamer coding frequencies  
c) By translating the entire chromosome into protein and testing enzyme activity in silico  
d) By asking the user to manually highlight the start and stop codons  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) By utilizing probabilistic Hidden Markov Models (HMMs) parameterized on statistical properties of exons, introns, splice signals, branch sites, and hexamer coding frequencies  
* **Rationale:** *Ab initio* programs use Generalized Hidden Markov Models (GHMMs). They integrate multiple statistical signals (donor/acceptor weight matrices, promoter consensus) and content sensors (5th-order Markov models of coding hexamers vs non-coding introns) to compute the most probable exon-intron path via the Viterbi algorithm.

### Q14
What is an "isochore" in eukaryotic genome organization?  
a) A microscopic chromosome banding artifact visible only under UV light  
b) A large genomic chromosomal region (>300 kb) characterized by a remarkably uniform GC content composition, categorized into distinct GC-poor (L1, L2) and GC-rich (H1, H2, H3) families  
c) A viral transposon that integrates specifically into telomeres  
d) A specialized dynamic programming scoring matrix used for promoters  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) A large genomic chromosomal region (>300 kb) characterized by a remarkably uniform GC content composition, categorized into distinct GC-poor (L1, L2) and GC-rich (H1, H2, H3) families  
* **Rationale:** Giorgio Bernardi discovered that vertebrate genomes are mosaics of long segments ($>300\text{ kb}$) called isochores, each possessing homogeneous base composition. Gene density, SINE distribution, and recombination rates vary systematically between GC-poor (L) and GC-rich (H) isochores.

### Q15
What type of genetic repetitive element is classified as a "microsatellite" (or Short Tandem Repeat - STR)?  
a) A 300 bp retrotransposon belonging to the Alu family  
b) A tandem repeat of a simple short motif of 1 to 6 base pairs (e.g., $(CA)_n$ or $(GATA)_n$) repeated multiple times  
c) A 6 kb full-length retrovirus with long terminal repeats  
d) A duplicated ribosomal RNA gene cluster spanning 40 kb  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) A tandem repeat of a simple short motif of 1 to 6 base pairs (e.g., $(CA)_n$ or $(GATA)_n$) repeated multiple times  
* **Rationale:** Microsatellites (Short Tandem Repeats / STRs) consist of tandemly repeated 1–6 bp motifs (e.g., $(CA)_{15}$). They are highly polymorphic due to replication slippage, making them ideal genetic markers for forensics and linkage mapping. Minisatellites have 10–100 bp repeat units.

---

## Section B: Short Answer Questions (6 SAQs)

### SAQ 01: Six-Frame Translation Mechanics (3 Marks)
**Question:** Explain why a double-stranded DNA sequence has exactly six reading frames. If a forward strand begins with `5'-ATG-CCA-T...-3'`, what are the first two triplets of reading frame +1, +2, and +3?  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Why Six Frames:** The genetic code reads nucleotides in non-overlapping triplets (codons). On a single strand, translation can initiate at nucleotide 1 (frame +1), nucleotide 2 (frame +2), or nucleotide 3 (frame +3). Initiating at nucleotide 4 simply repeats the codon phase of frame +1. Because DNA is an anti-parallel double helix with functional genes encoded on either strand, the complementary strand similarly possesses three frames (-1, -2, -3) oriented in its $5' \rightarrow 3'$ direction, yielding $3 + 3 = 6$ potential reading frames.
* **Triplet Offsets for `5'-ATG-CCA-T...-3'`:**  
  - **Frame +1** (starts at base 1 `A`): `ATG`, `CCA`  
  - **Frame +2** (starts at base 2 `T`): `TGC`, `CAT`  
  - **Frame +3** (starts at base 3 `G`): `GCC`, `AT...`

**Marking Scheme:**  
* 1.5 Marks: Clear biological explanation of 3 frames per strand due to triplet codons and anti-parallel orientation of double-stranded DNA.  
* 1.5 Marks: 0.5 marks for correct triplet derivation in frame +1, +2, and +3.

---

### SAQ 02: Mathematical Formula for CpG Observed/Expected Ratio (4 Marks)
**Question:** State the mathematical formula used to calculate the Observed-to-Expected CpG ratio in a DNA sequence window of length $L$. Given a 1,000 bp DNA segment containing 300 Cytosines, 300 Guanines, and 54 CpG dinucleotides, calculate the Observed/Expected CpG ratio and determine whether it meets the Gardiner-Garden & Frommer threshold for a CpG island.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Formula:**  
  $$\text{Obs/Exp CpG} = \frac{\text{Count}(\text{CpG})}{\text{Expected}(\text{CpG})} = \frac{\text{Count}(\text{CpG})}{\frac{\text{Count}(C) \times \text{Count}(G)}{L}} = \frac{\text{Count}(\text{CpG}) \times L}{\text{Count}(C) \times \text{Count}(G)}$$
* **Calculation:**  
  - $L = 1000\text{ bp}$  
  - $\text{Count}(C) = 300$  
  - $\text{Count}(G) = 300$  
  - $\text{Count}(\text{CpG}) = 54$  
  $$\text{Expected}(\text{CpG}) = \frac{300 \times 300}{1000} = \frac{90000}{1000} = 90$$  
  $$\text{Obs/Exp CpG} = \frac{54}{90} = \mathbf{0.60}$$  
* **GC Content Check:**  
  $$\%GC = \frac{300 + 300}{1000} \times 100\% = 60.0\%$$
* **Evaluation:**  
  - Length $1000\text{ bp} \ge 200\text{ bp}$ (Pass)  
  - $\%GC = 60.0\% \ge 50\%$ (Pass)  
  - $\text{Obs/Exp CpG} = 0.60 \ge 0.60$ (Pass)  
  **Conclusion:** The sequence strictly meets all criteria and is classified as a bona fide **CpG Island**.

**Marking Scheme:**  
* 1.5 Marks: Correct mathematical formula with all terms defined.  
* 1.5 Marks: Flawless stepwise calculation yielding Expected CpG = 90 and Obs/Exp ratio = 0.60.  
* 1 Mark: Accurate check against Gardiner-Garden thresholds (Length, %GC, Obs/Exp) and positive conclusion.

---

### SAQ 03: Prokaryotic vs Eukaryotic Gene Architecture (3 Marks)
**Question:** Compare prokaryotic and eukaryotic gene architecture across three structural features: transcript operon organization, presence of introns, and ribosome recruitment signals.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  

| Feature | Prokaryotic Gene Architecture | Eukaryotic Gene Architecture |
| :--- | :--- | :--- |
| **Operon Organization** | Frequently polycistronic (multiple continuous protein-coding ORFs transcribed on a single mRNA under one promoter). | Strictly monocistronic (one gene transcribed into a single precursor transcript under its own dedicated promoter). |
| **Exon-Intron Structure** | Colinear and uninterrupted; completely devoid of spliceosomal introns. | Split genes; coding exons are interrupted by extensive non-coding introns removed by splicing. |
| **Ribosome Recruitment** | Shine–Dalgarno consensus motif ($5'\text{-AGGAGGU-}3'$) upstream of start codon pairing with 16S rRNA. | 5' 7-methylguanosine cap recruitment; ribosome scans $5' \rightarrow 3'$ to find initiator codon in Kozak context. |

**Marking Scheme:**  
* 1 Mark per row accurately contrasted.

---

### SAQ 04: Transposable Elements: SINEs vs LINEs (3 Marks)
**Question:** Differentiate between Short Interspersed Nuclear Elements (SINEs) and Long Interspersed Nuclear Elements (LINEs) in the human genome, citing typical length, mechanism of retrotransposition, and one concrete biological example of each.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **SINEs (Short Interspersed Nuclear Elements):**  
  - Length: Short, typically $100\text{--}400\text{ bp}$.  
  - Autonomy: Non-autonomous; lack any protein-coding capacity and hijack the reverse transcriptase/endonuclease machinery of LINEs to transpose.  
  - Example: *Alu* elements (primate-specific, ~300 bp, ~1.2 million copies in the human genome).
* **LINEs (Long Interspersed Nuclear Elements):**  
  - Length: Long, typically $6\text{--}8\text{ kb}$ when full-length.  
  - Autonomy: Autonomous retrotransposons; encode their own open reading frames (ORF1 RNA-binding protein and ORF2 reverse transcriptase/endonuclease).  
  - Example: *LINE-1* (*L1* family, ~500,000 copies, occupying ~17% of the human genome).

**Marking Scheme:**  
* 1.5 Marks: Accurate contrast of length and autonomous vs non-autonomous retrotransposition mechanics.  
* 1.5 Marks: 0.75 marks for each concrete example (*Alu* and *L1*) with genomic context.

---

### SAQ 05: Anatomy of a Splicing Junction (4 Marks)
**Question:** Diagram a typical eukaryotic pre-mRNA intron flanked by its two exons. Label the 5' splice donor site, 3' splice acceptor site, branch point adenosine, and polypyrimidine tract, indicating the consensus nucleotides for each.  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
```text
5' EXON 1 ---|--- INTRON ---------------------------------------------|--- EXON 2 3'
             |                                                        |
         [5' Donor]           [Branch Point]    [Polypyrimidine]  [3' Acceptor]
          MAG|GURAGU              CURAY               YYYYYYYYYY      NCAG|G
             |                                                        |
        (Invariant GT)         (Adenosine 'A')      (T/C tract)   (Invariant AG)
```
* **Structural Elements:**
  1. **5' Splice Donor Junction:** Located at the Exon 1 / Intron boundary. Consensus sequence: $5'\text{-MAG}\mid\text{GURAGU-}3'$ with invariant **GT** (or GU) at intron positions +1 and +2.
  2. **Branch Point Site:** Located 20 to 50 nucleotides upstream of the 3' end of the intron. Consensus sequence: $5'\text{-CURAY-}3'$, where the invariant **Adenosine (A)** acts as the nucleophile that attacks the 5' splice site to form the lariat.
  3. **Polypyrimidine Tract:** A stretch of 10–20 pyrimidines (**Y** = C or T/U) positioned between the branch point and 3' splice site; recognized by U2AF65.
  4. **3' Splice Acceptor Junction:** Located at the Intron / Exon 2 boundary. Consensus sequence: $5'\text{-NCAG}\mid\text{G-}3'$ with invariant **AG** at intron positions -2 and -1.

**Marking Scheme:**  
* 1 Mark: Clear schematic diagram showing linear order of all 4 splicing features.  
* 3 Marks: Accurate consensus sequence and functional description for donor site (invariant GT), branch point (invariant A), polypyrimidine tract, and acceptor site (invariant AG).

---

### SAQ 06: Ab Initio vs Evidence-Based Gene Prediction (3 Marks)
**Question:** Compare *ab initio* gene prediction with evidence-based (similarity-based) gene prediction. What are the advantages and weaknesses of each approach?  
* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Analyze  

**Model Answer:**  
* **Ab Initio Gene Prediction (e.g., Genscan, Glimmer):**  
  - *Mechanism:* Relies purely on mathematical and probabilistic properties of the query DNA sequence itself (HMM models of hexamer frequencies, codon bias, splice site matrices).  
  - *Advantage:* Capable of discovering completely novel genes, lineage-specific transcripts, and genes expressed at low levels without existing experimental cDNA data.  
  - *Weakness:* Prone to high false-positive rates, chimeric gene predictions, and inaccurate exon boundary calls.
* **Evidence-Based Prediction (e.g., BLAST, spliced alignment of RNA-seq/ESTs):**  
  - *Mechanism:* Uses dynamic programming (e.g., Spidey, GMAP) to align experimentally sequenced transcripts (ESTs, cDNAs, RNA-seq reads) or homologous proteins onto the genomic contig.  
  - *Advantage:* Highly accurate; directly confirms transcription and resolves exact biological splice junctions with empirical physical proof.  
  - *Weakness:* Completely blind to genes not present in databases (unexpressed genes, tissue-specific genes, or novel taxa lacking cDNA libraries).

**Marking Scheme:**  
* 1.5 Marks: Detailed operational contrast of intrinsic HMM modeling vs empirical alignment evidence.  
* 1.5 Marks: Clear evaluation of complementary strengths (novel gene discovery vs experimental boundary accuracy) and weaknesses.

---

## Section C: Long Answer / Problem Questions (2 LAQs)

### LAQ 01: Comprehensive Gene Finding Pipeline and ORF Dissection (10 Marks)
**Question:**  
A microbiology team sequences a 900 bp uncharacterized genomic fragment from a newly discovered thermophilic archaeon. To locate potential protein-coding genes:

a) Define the computational rules implemented by ORF prediction algorithms (such as EMBOSS `getorf` or NCBI ORFfinder) to scan the six reading frames. Specify the default codon table, start and stop triplets, and minimum length thresholds used to filter spurious background ORFs. (3 Marks)  
b) Examine the hypothetical single-strand sequence snippet below:  
   `5'- GGC CTA ATG GCA CTG TGG ATG CGA CTC CTC TGA GCA TAA -3'`  
   Translate this sequence in Reading Frame +1. Identify all start and stop codons, demarcate the open reading frame, and write out the resulting single-letter amino acid peptide sequence. (3 Marks)  
c) If an insertion of a single nucleotide occurs after base 9 (`5'-GGCCTAATG [T] GCA...-3'`), trace the catastrophic consequences on downstream translation. Name this mutation and explain how automated gene prediction algorithms detect frameshifts versus authentic evolutionary indels. (2 Marks)  
d) Contrast prokaryotic gene finding algorithms (e.g., Glimmer) with eukaryotic gene finders (e.g., Genscan). Explain why prokaryotic gene prediction achieves $>99\%$ accuracy, while eukaryotic gene prediction remains one of bioinformatics' greatest challenges. (2 Marks)  

* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Apply / Analyze  

**Model Solution:**  
**a) ORF Prediction Computational Rules (3 Marks):**  
1. **Six-Frame Translation:** The algorithm generates all three forward translation phases (+1, +2, +3) and the three reverse-complement phases (-1, -2, -3).
2. **Genetic Code & Codon Triplet Lookup:** By default, it applies NCBI Genetic Code Table 11 (Bacterial, Archaeal, and Plant Plastid), where standard start codons are `ATG`, `GTG`, and `TTG` (all translating to formyl-Met at initiation), and stop codons are `TAA`, `TAG`, and `TGA`.
3. **Boundary Identification:** An ORF is identified as a span of codons starting at a start codon and terminating at the first in-frame stop codon.
4. **Length Threshold Filtering:** Because random non-coding DNA with 50% GC content produces a stop codon roughly once every $64/3 \approx 21$ triplets by chance, ORF finders enforce a minimum length threshold (typically $\ge 100\text{ codons} / 300\text{ bp}$). Random background stop-free windows exceeding 100 codons are statistically rare ($P < 0.01$), effectively filtering non-coding noise.

**b) Reading Frame +1 Translation and ORF Demarcation (3 Marks):**  
Given sequence:  
`5'- GGC CTA ATG GCA CTG TGG ATG CGA CTC CTC TGA GCA TAA -3'`  
* **Triplet Partitioning in Frame +1:**  
  1. `GGC` = Gly (G)  
  2. `CTA` = Leu (L)  
  3. `ATG` = **Start Codon / Met (M)** [Base 7..9]  
  4. `GCA` = Ala (A)  
  5. `CTG` = Leu (L)  
  6. `TGG` = Trp (W)  
  7. `ATG` = Met (M) [Internal sense methionine]  
  8. `CGA` = Arg (R)  
  9. `CTC` = Leu (L)  
  10. `CTC` = Leu (L)  
  11. `TGA` = **Stop Codon (***) [Base 31..33]  
  12. `GCA` = Ala (A)  
  13. `TAA` = Stop Codon (***)
* **Demarcated ORF:**  
  Spans from base 7 to base 33 (inclusive of stop codon): `ATG GCA CTG TGG ATG CGA CTC CTC TGA`  
* **Translated Polypeptide:**  
  `M - A - L - W - M - R - L - L` (Length = 8 amino acids).

**c) Frameshift Mutation and Algorithmic Detection (2 Marks):**  
* **Consequences of Single Base Insertion (`+T` at position 10):**  
  Original: `ATG | GCA | CTG | TGG | ATG | CGA | CTC | CTC | TGA`  
  Mutated:  `ATG | TGC | ACT | GTG | GAT | GCG | ACT | CCT | CTG | AGC | ATA | A...`  
  - The reading frame shifts from Frame +1 into Frame +2.
  - The amino acid sequence changes completely: `M - C - T - V - D - A - T - P - L - S - I...`
  - The original in-frame stop codon `TGA` is disrupted (`CTG`), causing abnormal translation run-on until a novel downstream out-of-frame stop codon is encountered.
* **Detection by Gene Finders:** Algorithms like Glimmer or GeneMark compute hexamer coding potential (interpolated Markov models). When a frameshift occurs, the coding score suddenly collapses from a high coding probability to background non-coding noise. In pseudo-gene detection pipelines, spliced alignments against homologous proteins reveal an unexpected gap of 1 or 2 nucleotides, flagging a sequencing error or pseudogenic frameshift.

**d) Accuracy Disparity: Prokaryotic vs Eukaryotic Gene Finding (2 Marks):**  
* **Why Prokaryotic Accuracy Exceeds 99%:**  
  1. Uninterrupted coding sequences (no introns).  
  2. Extremely high coding density (~85–90% of genome is protein-coding).  
  3. Clear boundary signals: prominent Shine-Dalgarno motifs and short intergenic distances. Finding long ORFs ($>300\text{ bp}$) almost always corresponds to authentic genes.
* **Why Eukaryotic Gene Finding is Extremely Difficult:**  
  1. Split gene architecture: small coding exons (~150 bp) separated by vast introns (often $>10,000\text{ bp}$).  
  2. Low coding density (<1.5% of human DNA codes for proteins).  
  3. Degenerate biological signals: splice sites (`GT...AG`) occur millions of times randomly across non-coding introns without being functional splice junctions.  
  4. Extensive alternative splicing produces multiple distinct transcript isoforms from a single genomic locus, which static Markov models struggle to predict without direct RNA-seq empirical evidence.

**Marking Scheme Breakdown:**  
* 3 Marks: Comprehensive ORF rules detailing 6 frames, Table 11 start/stop codons, and statistical basis of the 100-codon length filter.  
* 3 Marks: Flawless codon partitioning, start/stop identification, ORF coordinate demarcation (bases 7–33), and peptide translation (`MALWMRLL`).  
* 2 Marks: Precise explanation of frameshift consequence on downstream reading frame/stops, and Markov coding score collapse detection.  
* 2 Marks: In-depth contrast explaining $>99\%$ bacterial accuracy (high density, no introns, long ORFs) vs eukaryotic complexity (tiny exons, huge introns, alternative splicing, low coding density).

---

### LAQ 02: Codon Usage Bias, CAI Formulation, and Heterologous Expression Optimization (10 Marks)
**Question:**  
A biotechnology firm is expressing human beta-globin (*HBB*) in an *Escherichia coli* microbial fermentation system. The recombinant yield is unexpectedly low due to translational stalling caused by codon usage incompatibility.

a) Define synonymous codon usage bias. Explain the biochemical mechanisms that cause synonymous mutations—which do not change the amino acid sequence—to drastically alter protein expression levels in heterologous hosts. (3 Marks)  
b) Write out the mathematical formula for the **Codon Adaptation Index (CAI)** developed by Sharp and Li. Define the relative synonymous codon adaptiveness parameter ($w_{ij}$) and explain how the reference set of highly expressed genes is established. (4 Marks)  
c) Examine the following codon frequency data for Leucine in *E. coli*:  

```text
Codon    Observed Frequency in Highly Expressed E. coli Genes
CUA      0.002 (extremely rare)
CUC      0.010
CUG      0.840 (optimal preferred codon)
CUU      0.011
UUA      0.027
UUG      0.110
```

   1. Calculate the relative adaptiveness ($w$) for the optimal codon `CUG` and the rare codon `CUA`.  
   2. Explain why a human cDNA containing multiple `CUA` codons stalls *E. coli* ribosomes.  
   3. Describe how computational "codon optimization" software designs a synthetic gene to maximize expression in *E. coli* without changing a single amino acid. (3 Marks)  

* **Learning Outcome:** LO6  
* **Bloom's Taxonomy Level:** Analyze / Apply  

**Model Solution:**  
**a) Synonymous Codon Usage Bias and Biochemical Mechanisms (3 Marks):**  
* **Definition:** Most amino acids are encoded by multiple synonymous codons (e.g., Leucine has 6 codons, Glycine has 4). Synonymous codon bias refers to the non-random, unequal frequency with which an organism utilizes specific synonymous codons over others in its protein-coding genes.
* **Biochemical Impact on Heterologous Expression:**  
  1. **tRNA Pool Depletion & Ribosomal Stalling:** Intracellular concentrations of isoaccepting tRNAs directly mirror the host organism's codon usage. In *E. coli*, tRNAs recognizing rare codons (like `CUA` or `AGG`/`AGA` for Arg) are present in trace amounts. When an overexpressed human mRNA presents rare codons, ribosomes stall waiting for cognate aminoacyl-tRNAs.
  2. **Premature Translation Termination:** Stalled ribosomes frequently dissociate, leading to truncated, non-functional protein fragments.
  3. **mRNA Secondary Structure at Translation Initiation:** Synonymous mutations at the $5'$ end of the transcript can form stable hairpin loops spanning the Shine-Dalgarno sequence or start codon, physically blocking 30S ribosomal subunit binding.

**b) Mathematical Formulation of the Codon Adaptation Index (CAI) (4 Marks):**  
* **The CAI Equation:**  
  For a gene consisting of $L$ sense codons (excluding Met and Trp, which have single codons, and stop codons), CAI is the geometric mean of the relative adaptiveness ($w_k$) of each codon:  
  $$\text{CAI} = \left( \prod_{k=1}^L w_k \right)^{1/L} = \exp \left( \frac{1}{L} \sum_{k=1}^L \ln w_k \right)$$
* **Relative Adaptiveness ($w_{ij}$):**  
  For codon $j$ encoding amino acid $i$:  
  $$w_{ij} = \frac{x_{ij}}{x_{i,\max}}$$  
  Where:
  - $x_{ij}$: Frequency of codon $j$ observed in a reference set of highly expressed genes.
  - $x_{i,\max}$: Frequency of the most frequently used (optimal) codon for amino acid $i$ in that reference set.
  - By definition, the optimal codon receives $w = 1.0$, while suboptimal codons receive $0 \le w < 1.0$.
* **Reference Set Establishment:** The reference set consists of 20 to 50 genes known to have massive constitutive cellular abundance (typically ribosomal protein genes, translation elongation factors like EF-Tu, and outer membrane proteins).

**c) Calculations and Codon Optimization Strategy (3 Marks):**  
1. **Relative Adaptiveness Calculations:**  
   - For `CUG` (optimal codon, $x_{\max} = 0.840$):  
     $$w_{\text{CUG}} = \frac{0.840}{0.840} = \mathbf{1.000}$$  
   - For `CUA` (rare codon, $x = 0.002$):  
     $$w_{\text{CUA}} = \frac{0.002}{0.840} \approx \mathbf{0.00238}$$
2. **Why `CUA` Stalls Ribosomes:** The relative adaptiveness of `CUA` is less than $0.003$. *E. coli* contains minimal copies of the $tRNA^{\text{Leu}}$ cognate to `CUA` (encoded by the rare *leuX* gene). Successive `CUA` triplets starve the ribosomal A-site, triggering ribosome stalling, frameshifting, or transfer-messenger RNA (tmRNA) mediated peptide tagging and degradation.
3. **Computational Codon Optimization Pipeline:**  
   Software (such as EMBOSS `backtranseq` or commercial gene synthesis tools):
   - Scans the human polypeptide sequence.
   - Replaces rare codons with high-adaptiveness host codons (e.g., converting all `CUA` and `UUA` Leucines to `CUG`, and `AGG`/`AGA` Arginines to `CGC`/`CGU`), raising the overall CAI toward $1.0$.
   - Simultaneously scans the optimized nucleotide sequence to remove premature polyadenylation signals, internal Shine-Dalgarno motifs, restriction sites, and stable $5'$ RNA hairpins ($\Delta G > -10\text{ kcal/mol}$), maximizing translation initiation and elongation yield.

**Marking Scheme Breakdown:**  
* 3 Marks: Accurate definition of synonymous bias and 3 distinct biochemical impacts (tRNA depletion, ribosomal stalling, 5' RNA hairpin blockage).  
* 4 Marks: Flawless mathematical formula for CAI (geometric mean) and $w_{ij} = x_{ij}/x_{i,\max}$ with complete definitions; clear description of reference gene sets.  
* 3 Marks: Correct mathematical calculations ($w_{\text{CUG}}=1.0$, $w_{\text{CUA}}=0.0024$), explanation of ribosomal starvation, and multi-parameter computational optimization pipeline.
