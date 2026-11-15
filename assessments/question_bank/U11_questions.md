# Question Bank: Unit 11 — Comparative Genome Analysis

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Syllabus Topic:** Introduction, Application, Genome analysis and annotation  
**Primary Learning Outcome:** LO8 (Explain comparative genomics workflows, synteny, genome annotation, and evolutionary conservation)  

---

## Section A: Multiple Choice Questions (15 MCQs)

### Q01
What is the "C-value paradox" in eukaryotic genomics?  
a) The observation that cytosine is the rarest nucleotide in all living organisms  
b) The total haploid genomic DNA content (C-value) of a eukaryote does not correlate with its morphological or developmental complexity  
c) The speed of DNA replication is identical across all kingdoms of life  
d) The number of chromosomes is always a multiple of four  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The total haploid genomic DNA content (C-value) of a eukaryote does not correlate with its morphological or developmental complexity  
* **Rationale:** The C-value paradox notes that genome size does not track organismal complexity: certain amoebae (*Polychaos dubium*) and lungfish possess genomes over 40 times larger than the human genome, driven primarily by non-coding repeat accumulation rather than increased gene counts.

### Q02
How does typical gene density differ between prokaryotic genomes (e.g., *E. coli*) and complex multicellular eukaryotic genomes (e.g., human)?  
a) Prokaryotes have ~1 gene per 1,000 bp (~1 kb), whereas humans have ~1 gene per 100,000 bp (~100 kb)  
b) Humans have higher gene density than bacteria  
c) Gene density is strictly uniform across all cellular organisms  
d) Bacteria have no genes; they possess only non-coding RNA  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) Prokaryotes have ~1 gene per 1,000 bp (~1 kb), whereas humans have ~1 gene per 100,000 bp (~100 kb)  
* **Rationale:** Bacterial genomes are tightly packed with ~85% coding sequence (~1 gene per kb). In the human genome, ~20,000 genes are scattered across 3.2 billion base pairs, yielding an average density of roughly 1 gene per 100–150 kb.

### Q03
What is the biological definition of **synteny** (or colinearity) in comparative genomics?  
a) The percentage of identical amino acids in a multiple sequence alignment  
b) The conserved order and linkage of homologous genes along chromosomal blocks shared between two or more diverging species  
c) The simultaneous transcription of tRNA and rRNA genes  
d) The alignment of protein structures using RMSD  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) The conserved order and linkage of homologous genes along chromosomal blocks shared between two or more diverging species  
* **Rationale:** Synteny describes the preservation of gene order on chromosomes across species. Large conserved syntenic blocks (e.g., between human chromosome 17 and mouse chromosome 11) reflect chromosomal segments inherited intact from a common ancestor.

### Q04
In genome annotation pipelines, what is the distinction between **Structural Annotation** and **Functional Annotation**?  
a) Structural annotation uses X-ray crystallography, while functional annotation uses NMR  
b) Structural annotation identifies the physical genomic coordinates of genes, exons, introns, and repeats; functional annotation assigns biological roles, GO terms, and metabolic pathways to those predicted features  
c) Structural annotation is applied only to viruses, while functional annotation is for mammals  
d) Structural annotation deletes non-coding DNA from the file  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Structural annotation identifies the physical genomic coordinates of genes, exons, introns, and repeats; functional annotation assigns biological roles, GO terms, and metabolic pathways to those predicted features  
* **Rationale:** Structural annotation maps "where" the features are on the DNA scaffold (coordinates of start/stop codons, splice junctions, ncRNAs). Functional annotation answers "what they do" by attaching descriptive annotations, Enzyme Commission (EC) numbers, and Gene Ontology categories.

### Q05
What computational strategy is standardly used to identify 1-to-1 orthologous gene pairs between two newly sequenced genomes ($G_A$ and $G_B$)?  
a) Random selection of genes with matching names  
b) Reciprocal Best Hits (RBH) via BLAST  
c) Calculating the molecular weight of the translated proteins  
d) Comparing the GC content of the promoters  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** b) Reciprocal Best Hits (RBH) via BLAST  
* **Rationale:** Reciprocal Best Hits (RBH) posits that if gene $A$ in genome $G_A$ finds gene $B$ as its top hit in genome $G_B$, and querying gene $B$ against genome $G_A$ returns gene $A$ as its top hit, they are candidate 1-to-1 orthologues that diverged via speciation.

### Q06
What are the three standardized, structured ontologies provided by the **Gene Ontology (GO)** consortium to describe gene function?  
a) DNA, RNA, and Protein  
b) Molecular Function, Biological Process, and Cellular Component  
c) Genotype, Phenotype, and Karyotype  
d) Bacteria, Archaea, and Eukaryota  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Molecular Function, Biological Process, and Cellular Component  
* **Rationale:** Gene Ontology categorizes gene product attributes into three independent domains: Molecular Function (elemental biochemical activities, e.g., kinase activity), Biological Process (broad cellular/pathway goals, e.g., cell division), and Cellular Component (subcellular localization, e.g., mitochondrial matrix).

### Q07
What sequence signature typically identifies a **Pathogenicity Island (PAI)** when comparing the genome of a virulent bacterial pathogen to a benign, non-pathogenic close relative?  
a) A region with an anomalous GC content, flanked by direct repeats or tRNA genes, encoding virulence factors, and absent in the benign strain  
b) A 100% loss of all ribosomal protein genes  
c) A region consisting purely of adenine homopolymers  
d) A chromosomal segment that lacks double-stranded DNA  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) A region with an anomalous GC content, flanked by direct repeats or tRNA genes, encoding virulence factors, and absent in the benign strain  
* **Rationale:** Pathogenicity islands are mobile genomic islands acquired via horizontal gene transfer. They feature atypical GC content compared to the host genome, are often inserted adjacent to tRNA genes, carry mobility genes (integrases/transposases), and encode toxins or type III secretion systems.

### Q08
How does comparative genomics provide conclusive evidence that human Chromosome 2 originated from an end-to-end telomeric fusion of two ancestral ape chromosomes?  
a) Human chromosome 2 contains vestigial telomeric hexamer repeats (`TTAGGG`) head-to-head in its internal 2q13 band and contains two centromere loci (one active, one inactivated), matching chimpanzee chromosomes 2A and 2B  
b) Human chromosome 2 is identical in length to bacterial plasmids  
c) Human chromosome 2 lacks any protein-coding genes  
d) Chimpanzees lack chromosome 2 completely  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) Human chromosome 2 contains vestigial telomeric hexamer repeats (`TTAGGG`) head-to-head in its internal 2q13 band and contains two centromere loci (one active, one inactivated), matching chimpanzee chromosomes 2A and 2B  
* **Rationale:** Comparative cytogenetics and sequencing reveal that human Chr 2 resulted from a telomere-to-telomere fusion of two ancestral hominid chromosomes (syntenic to chimp 2A and 2B). The junction contains internal inverted telomeric repeats ($5'\text{-TTAGGG-}(CCCTAA)_n\text{-}3'$) and a second inactivated centromere.

### Q09
What is a **Conserved Non-coding Element (CNE)**, and what biological function do CNEs frequently perform?  
a) Defective transposons that have lost the ability to replicate  
b) Genomic non-coding DNA regions that exhibit extreme sequence conservation across divergent species, frequently functioning as critical transcriptional enhancers or developmental gene regulators  
c) Ribosomal RNA operons that do not fold into secondary structures  
d) Intron regions that mutate at 100 times the neutral rate  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Genomic non-coding DNA regions that exhibit extreme sequence conservation across divergent species, frequently functioning as critical transcriptional enhancers or developmental gene regulators  
* **Rationale:** CNEs (or ultra-conserved elements) are non-coding sequences exhibiting higher evolutionary conservation between humans and rodents than protein-coding exons. Experimental assays demonstrate that CNEs act as long-range developmental enhancers governing embryonic patterning genes.

### Q10
What computational signature indicates that a gene was recently acquired by a bacterial genome via **Horizontal Gene Transfer (HGT)** rather than vertical descent?  
a) The gene has identical codon usage bias to the rest of the bacterial genome  
b) The gene displays significantly different GC content and atypical codon usage compared to the host genome average, and is phylogenetically related to distant phyla  
c) The gene encodes a ribosomal protein  
d) The gene contains human introns  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) The gene displays significantly different GC content and atypical codon usage compared to the host genome average, and is phylogenetically related to distant phyla  
* **Rationale:** A horizontally transferred gene initially reflects the mutational signatures (GC content and codon bias) of its donor organism. An unexpected GC% deviation, discordant phylogenetic placement, and proximity to mobile elements are hallmarks of HGT.

### Q11
In genome assembly pipelines, what is the hierarchical progression from raw sequencing reads to finished chromosomal maps?  
a) Scaffolds $\rightarrow$ Contigs $\rightarrow$ Raw Reads $\rightarrow$ Chromosomes  
b) Raw Reads $\rightarrow$ Contigs (continuous overlapping reads) $\rightarrow$ Scaffolds (linked contigs separated by known gaps) $\rightarrow$ Chromosome Assemblies  
c) Chromosomes $\rightarrow$ Plasmids $\rightarrow$ Reads  
d) Transcripts $\rightarrow$ Genes $\rightarrow$ Reads  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Raw Reads $\rightarrow$ Contigs (continuous overlapping reads) $\rightarrow$ Scaffolds (linked contigs separated by known gaps) $\rightarrow$ Chromosome Assemblies  
* **Rationale:** Assembly algorithms first merge overlapping raw reads into gapless contiguous blocks called **contigs**. Paired-end/mate-pair information or long reads then orient and order contigs into **scaffolds** spanning repeat gaps, which are finally anchored to **chromosomes**.

### Q12
What is the primary function of the **KEGG (Kyoto Encyclopedia of Genes and Genomes)** database in comparative genome analysis?  
a) Classifying 3D crystal structures into all-alpha and all-beta folds  
b) Reconstructing higher-level biological systems, metabolic pathways, and cellular networks by mapping annotated gene enzymes to reference pathway wiring diagrams  
c) Generating PCR primers for Sanger sequencing  
d) Storing raw FASTQ sequencing files  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Reconstructing higher-level biological systems, metabolic pathways, and cellular networks by mapping annotated gene enzymes to reference pathway wiring diagrams  
* **Rationale:** KEGG maps genomic enzymatic content to reference metabolic pathways, allowing researchers to reconstruct the full metabolic network of a newly sequenced organism and identify missing enzymes or novel biosynthetic pathways.

### Q13
What is the "minimal bacterial genome", as exemplified by *Mycoplasma genitalium* and synthetic biology experiments (e.g., JCVI-syn3.0)?  
a) The smallest set of essential genes (~450 to 500 genes) required to sustain autonomous cellular life in a nutrient-rich environment  
b) A genome composed exclusively of RNA  
c) A genome containing only one gene  
d) A virus that cannot infect bacteria  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** a) The smallest set of essential genes (~450 to 500 genes) required to sustain autonomous cellular life in a nutrient-rich environment  
* **Rationale:** Comparative genomics of parasitic bacteria (*M. genitalium*, 482 genes) and transposon mutagenesis define the "minimal gene set": the conserved core machinery for replication, transcription, translation, and rudimentary energy generation.

### Q14
Which web-based genome browser, maintained by the European Bioinformatics Institute (EMBL-EBI) and the Wellcome Sanger Institute, provides comprehensive comparative genomic alignments and Ensembl Compara gene trees across vertebrate species?  
a) Ensembl Genome Browser  
b) PDB-101  
c) ProtParam  
d) Expasy PROSITE  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) Ensembl Genome Browser  
* **Rationale:** Ensembl (www.ensembl.org) is the premier vertebrate genome browser, providing automated annotation, whole-genome pairwise and multiple syntenic alignments, and the Ensembl Compara database of orthologues and paralogues.

### Q15
What type of chromosomal rearrangement occurs when a chromosome segment breaks, rotates 180 degrees, and reintegrates back into the chromosome?  
a) Translocation  
b) Inversion  
c) Duplication  
d) Aneuploidy  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) Inversion  
* **Rationale:** An inversion occurs when a chromosomal region is flipped end-to-end. In paracentric inversions, the centromere is excluded; in pericentric inversions, the centromere is included. Inversions alter local gene order without changing overall gene dosage.

---

## Section B: Short Answer Questions (6 SAQs)

### SAQ 01: The C-Value Paradox and Non-Coding DNA (3 Marks)
**Question:** Explain the C-value paradox in genomics. Why does a single-celled protozoan like *Amoeba dubia* possess a genome 200 times larger than *Homo sapiens*, and what biological component accounts for this discrepancy?  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **The Paradox:** The "C-value" is the amount of DNA in a haploid cell nucleus. The paradox is that genome size does NOT correlate with evolutionary complexity: morphological complexity does not scale with DNA quantity (e.g., *Polychaos dubium* has ~670 billion bp vs human 3.2 billion bp).
* **Biological Explanation:**  
  The massive variation in eukaryotic genome size is NOT driven by protein-coding gene counts (both humans and amoebae possess ~20,000–30,000 genes). Instead, it is driven by the differential accumulation, amplification, and purge-rates of **non-coding DNA**:
  1. Proliferation of retrotransposons and mobile repetitive elements (SINEs, LINEs).
  2. Large expansions of satellite and tandem non-coding DNA.
  3. Extensive intron lengths and genomic duplications.

**Marking Scheme:**  
* 1.5 Marks: Clear explanation of the paradox (lack of correlation between nuclear DNA content and organismal complexity).  
* 1.5 Marks: Detailed biological explanation attributing differences to non-coding repetitive DNA, retrotransposons, and introns rather than protein-coding gene counts.

---

### SAQ 02: Reciprocal Best Hits (RBH) Workflow (4 Marks)
**Question:** Describe the algorithmic logic of the Reciprocal Best Hits (RBH) method for identifying 1-to-1 orthologues between two distinct genomes. What is its primary limitation when gene duplication has occurred?  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Algorithmic Procedure:**  
  1. Let Genome 1 contain Gene $A$ and Genome 2 contain Gene $B$.
  2. Run BLASTp using Gene $A$ as query against all proteins in Genome 2. If the top-scoring hit with lowest $E$-value is Gene $B$, proceed.
  3. Run the reciprocal search: use Gene $B$ as query against all proteins in Genome 1.
  4. If and only if the top hit returned in Genome 1 is Gene $A$, the pair $(A, B)$ is declared a **Reciprocal Best Hit (RBH)** and classified as putative 1-to-1 orthologues.
* **Primary Limitation with Duplications:**  
  RBH assumes a simple 1-to-1 speciation relationship. When lineage-specific gene duplications occur (producing paralogues, such as multiple alpha-globin copies), RBH arbitrarily picks only one of the duplicated paralogues based on minor score fluctuations, failing to identify complex 1-to-many or many-to-many orthologous co-orthologue sets.

**Marking Scheme:**  
* 2.5 Marks: Clear stepwise description of forward BLAST, top-hit identification, reciprocal reverse BLAST, and reciprocal top-hit confirmation.  
* 1.5 Marks: Detailed explanation of RBH failure in the presence of paralogous gene duplications (1-to-many / co-orthologues).

---

### SAQ 03: The Three Domains of Gene Ontology (3 Marks)
**Question:** Name the three distinct domains of the Gene Ontology (GO) framework and give an example of how human beta-globin (*HBB*) is annotated in each domain.  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
1. **Molecular Function (Elemental biochemical activity):**  
   - *Definition:* The direct molecular activity of a gene product (e.g., binding, catalysis).  
   - *HBB Example:* `oxygen binding` (GO:0019825) or `iron ion binding` (GO:0005506).
2. **Biological Process (Broad cellular/physiological system):**  
   - *Definition:* A coordinated multi-step biological objective achieved by assemblies of molecular functions.  
   - *HBB Example:* `oxygen transport` (GO:0015671) or `erythrocyte development`.
3. **Cellular Component (Subcellular localization):**  
   - *Definition:* The physical location or macromolecular complex where the gene product executes its activity.  
   - *HBB Example:* `hemoglobin complex` (GO:0005833) or `cytosol` (GO:0005829).

**Marking Scheme:**  
* 1 Mark per domain correctly defined with a biologically accurate *HBB* annotation example.

---

### SAQ 04: Identifying Horizontal Gene Transfer (3 Marks)
**Question:** Explain three distinct computational lines of evidence used to detect a Horizontal Gene Transfer (HGT) event in a bacterial genome.  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
1. **Anomalous GC Content:** The gene's GC percentage deviates significantly ($>2$ standard deviations) from the host genome's mean GC composition, retaining the compositional signature of the foreign donor organism.
2. **Atypical Codon Usage Bias:** The gene exhibits a codon adaptation profile completely discordant with the host's preferred synonymous codon frequencies.
3. **Phylogenetic Discordance:** A phylogenetic tree constructed for the gene shows a topology in sharp contradiction with the known organismal species tree (e.g., an *E. coli* gene clustering robustly within an Archaeal or Cyanobacterial clade).
*(Additional valid factor: Proximity to mobile elements, transposases, or tRNA gene insertion sites).*

**Marking Scheme:**  
* 1 Mark per distinct computational line of evidence (GC anomaly, codon bias discordance, phylogenetic tree conflict).

---

### SAQ 05: Syntenic Dot-Plot Signatures (4 Marks)
**Question:** In a comparative whole-genome synteny dot-plot comparing Chromosome 1 of Species A against Chromosome 1 of Species B:  
a) What does an uninterrupted diagonal line extending from bottom-left to top-right indicate?  
b) What does a diagonal line with an inverted negative slope ($\nwse$ or $\swne$) indicate?  
c) What does a sudden horizontal or vertical displacement in the diagonal line indicate?  
d) What do parallel duplicate diagonal lines indicate?  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
a) **Continuous positive diagonal ($/$)**: Perfectly conserved **colinear synteny**; gene order and orientation are identical between the two chromosomes.  
b) **Inverted negative slope ($\backslash$)**: A **chromosomal inversion**; the segment has flipped 180 degrees in orientation relative to the other genome.  
c) **Displaced diagonal (offset shift)**: An **insertion or deletion (indel)**; a large segment of DNA is present in one genome but absent in the other, shifting the downstream alignment coordinates.  
d) **Parallel duplicate diagonals**: A **segmental gene duplication**; the same chromosomal block is present in two copies in one of the genomes.

**Marking Scheme:**  
* 1 Mark per correctly interpreted syntenic pattern.

---

### SAQ 06: Structural vs Functional Annotation Workflow (3 Marks)
**Question:** Contrast the tools and data inputs used during the structural annotation phase versus the functional annotation phase of a newly sequenced fungal genome.  
* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Analyze  

**Model Answer:**  
* **Structural Annotation Phase:**  
  - *Data Inputs:* Raw genomic scaffold DNA and spliced RNA-seq transcript read alignments.  
  - *Tools Used:* RepeatMasker (repeat masking), ab initio gene finders (Augustus, SNAP, Genscan), and spliced alignment tools (GMAP, STAR).  
  - *Deliverable:* A structural GFF3/GTF feature coordinate file defining exact coordinates of promoters, exons, introns, CDSs, and UTRs.
* **Functional Annotation Phase:**  
  - *Data Inputs:* Translated protein sequences extracted from the structural annotation.  
  - *Tools Used:* BLASTp against RefSeq/UniProt, InterProScan / Pfam (HMM protein domain search), Blast2GO (Gene Ontology assignment), and KAAS / KEGG (metabolic pathway mapping).  
  - *Deliverable:* Functional descriptions, EC enzyme numbers, GO term associations, and metabolic maps.

**Marking Scheme:**  
* 1.5 Marks: Detailed description of structural annotation inputs, tools (Augustus/STAR), and GFF3 coordinate outputs.  
* 1.5 Marks: Detailed description of functional annotation inputs, tools (BLASTp/InterProScan/KEGG), and biological role assignments.

---

## Section C: Long Answer / Problem Questions (2 LAQs)

### LAQ 01: End-to-End Comparative Genomics Pipeline for a Bacterial Outbreak (10 Marks)
**Question:**  
A hospital experiences an acute outbreak of multidrug-resistant *Klebsiella pneumoniae*. High-throughput sequencing of the outbreak strain produces 10 million paired-end Illumina reads.

a) Outline the complete bioinformatics pipeline to assemble, structurally annotate, and functionally annotate the new genome from raw FASTQ reads. (3 Marks)  
b) Describe how you would conduct a comparative genomic analysis comparing the outbreak strain with the reference benign laboratory strain *K. pneumoniae* MGH 78578 to pinpoint the exact genomic modifications responsible for pathogenesis. (3 Marks)  
c) Explain how you would identify and characterize candidate **Pathogenicity Islands (PAIs)** and **Antimicrobial Resistance (AMR)** mobile elements in the outbreak genome:  
   - What sequence properties and signature enzymes would you screen for?  
   - What specialized databases (such as CARD or ResFinder) would you utilize? (2 Marks)  
d) Synteny analysis reveals that an 80 kb virulence plasmid has integrated directly into the host bacterial chromosome adjacent to a `tRNA-Leu` locus. Describe the biological mechanism of this integration and its evolutionary impact on horizontal gene transfer across hospital pathogens. (2 Marks)  

* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Apply / Synthesize  

**Model Solution:**  
**a) End-to-End Assembly and Annotation Pipeline (3 Marks):**  
1. **Quality Control & Trimming:** Evaluate raw FASTQ reads with FastQC; remove low-quality bases ($Q < 30$) and sequencing adapters using Trimmomatic or fastp.
2. **De Novo Genome Assembly:** Assemble paired reads into contigs using a De Bruijn graph assembler (e.g., SPAdes or Unicycler). Order contigs into scaffolds using long-read or paired-end linkages.
3. **Structural Annotation:** Run automated prokaryotic pipeline (e.g., Prokka):
   - Find tRNA genes using Aragorn / tRNAscan-SE.
   - Find rRNA genes with Barrnap.
   - Predict protein-coding CDSs using Prodigal.
4. **Functional Annotation:**
   - Search predicted proteins against UniProt/RefSeq via BLASTp / DIAMOND.
   - Scan protein domains against Pfam/TIGRFAMs using HMMER.
   - Map Gene Ontology (GO) terms and EC numbers. Output standardized GFF3 and GenBank flat files.

**b) Comparative Genomic Analysis vs Reference Strain (3 Marks):**  
1. **Whole-Genome Alignment:** Align the assembled outbreak genome against reference strain MGH 78578 using progressive Mauve or MUMmer (nucmer).
2. **Core vs Pan-Genome Partitioning (Roary pipeline):**  
   - **Core Genome:** Genes shared by both strains (used to build a high-resolution SNP phylogenetic tree to determine outbreak origin).  
   - **Accessory / Strain-Specific Genome:** Genes present exclusively in the outbreak strain and absent from the reference strain.
3. **Variant Calling:** Identify Single Nucleotide Polymorphisms (SNPs) and small indels within the core genome to detect point mutations in target enzymes (e.g., GyrA/ParC mutations conferring fluoroquinolone resistance).

**c) Identifying Pathogenicity Islands and AMR Genes (2 Marks):**  
* **Screening Signatures:**  
  - **GC-Content Anomaly:** Scan the genome with a sliding window to detect segments where GC% deviates from the 57% *Klebsiella* species baseline.  
  - **Mobility Genes:** Search for flanking direct repeats ($15\text{--}30\text{ bp}$) and genes encoding integrases, transposases, or plasmid replication proteins.
* **Specialized AMR Databases:** Query the Comprehensive Antibiotic Resistance Database (CARD) and ResFinder using `rgi` (Resistance Gene Identifier) to identify acquired carbapenemases (e.g., *bla*KPC or *bla*NDM-1) and extended-spectrum beta-lactamases (ESBLs).

**d) Plasmid Integration at tRNA Loci and Evolutionary Impact (2 Marks):**  
* **Site-Specific Recombination Mechanism:**  
  tRNA genes are highly conserved and possess invariant loop sequences. Plasmid-borne integrases (tyrosine recombinases) recognize a specific attachment site (*attP*) on the plasmid and an identical sequence (*attB*) embedded within the host `tRNA-Leu` gene. Integrase mediates site-specific reciprocal crossover, seamlessly integrating the entire 80 kb plasmid into the chromosome flanked by direct repeat attachment sites (*attL* and *attR*).
* **Evolutionary Impact:** Chromosomal integration stabilizes the multi-drug resistance and virulence cassette: it can no longer be lost during plasmid segregation under antibiotic-free conditions. Furthermore, if excised errantly, the element can package flanking host chromosomal genes into conjugative transposons, accelerating horizontal dissemination across diverse clinical enterobacterial species.

**Marking Scheme Breakdown:**  
* 3 Marks: Complete, accurate pipeline from FASTQ QC, SPAdes assembly, Prokka structural prediction, to BLAST/Pfam functional annotation.  
* 3 Marks: Clear comparative workflow using MUMmer/Mauve, Roary core vs accessory genome partitioning, and SNP resistance calling.  
* 2 Marks: Identification of PAIs via GC-skew, integrases, and direct repeats; screening AMR genes against CARD/ResFinder.  
* 2 Marks: Accurate biological explanation of integrase-mediated *attP* $\times$ *attB* site-specific crossover at tRNA loci and evolutionary permanence/dissemination impact.

---

### LAQ 02: Synteny Mapping, Chromosomal Evolution, and Orthologue Clustering (10 Marks)
**Question:**  
Comparative genomics resolves large-scale chromosomal rearrangements across evolutionary divergence.

a) Construct a synthetic whole-genome synteny dot-plot illustrating the following evolutionary rearrangement events between Genome 1 (Horizontal axis) and Genome 2 (Vertical axis):  
   1. A conserved colinear segment (Block A).  
   2. A paracentric chromosomal inversion (Block B).  
   3. A segmental genomic duplication (Block C).  
   4. A reciprocal translocation between two non-homologous chromosomes (Block D). (4 Marks)  
b) Explain how the **Clusters of Orthologous Groups (COG)** and **eggNOG** databases classify orthologous proteins across prokaryotic and eukaryotic lineages. Define the difference between an "in-paralogue" and an "out-paralogue" relative to a reference speciation node. (3 Marks)  
c) Human Chromosome 17 displays profound synteny with Mouse Chromosome 11. However, the order of genes along the chromosome is scrambled into several discrete sub-blocks. Explain the evolutionary mutational mechanisms that scramble gene order while preserving gene linkage on the same chromosome over 80 million years of mammalian divergence. (3 Marks)  

* **Learning Outcome:** LO8  
* **Bloom's Taxonomy Level:** Analyze / Synthesize  

**Model Solution:**  
**a) Syntenic Dot-Plot Representation of Rearrangements (4 Marks):**  

```text
Genome 2
  ^
  |        [Block D: Translocation]               / (Block D1)
  |                                              /  (Block D2)
  |        [Block C: Duplication]       /      /   (Two parallel diagonals)
  |                                    /      /
  |        [Block B: Inversion]          \         (Inverted negative slope)
  |                                       \
  |        [Block A: Colinear]      /              (Uninterrupted positive slope)
  |                                /
  +------------------------------------------------------------> Genome 1
                               Block A  Block B  Block C  Block D
```

* **Detailed Mechanics:**  
  1. **Block A (Colinear):** Continuous diagonal ($/$) with positive slope ($+1$). Gene order is strictly identical in both genomes.
  2. **Block B (Inversion):** Diagonal with negative slope ($\backslash$). The sequence orientation has inverted $180^\circ$ on Genome 2 relative to Genome 1.
  3. **Block C (Segmental Duplication):** Two parallel diagonal lines at the same horizontal coordinate span, showing that one genomic locus in Genome 1 matches two distinct paralogous copies in Genome 2.
  4. **Block D (Reciprocal Translocation):** Segment D appears on an entirely different chromosome or unlinked scaffold in Genome 2, breaking chromosomal synteny.

**b) Orthologue Clustering and In-Paralogues vs Out-Paralogues (3 Marks):**  
* **COG and eggNOG Databases:**  
  - COG (Clusters of Orthologous Groups, NCBI) and eggNOG apply all-against-all BLASTp and Markov Cluster algorithms (MCL) across complete proteomes.  
  - They group proteins into functional clusters based on shared ancestry. Each COG represents an ancient orthologous lineage present in the common ancestor of the analyzed species, assigned standardized functional category letters (e.g., `J` = Translation, `C` = Energy production).
* **In-Paralogues vs Out-Paralogues:**  
  - **In-Paralogues (Symparalogues):** Paralogous genes that arose via gene duplication **AFTER** the speciation event uniting the species being compared. They represent lineage-specific co-orthologues (e.g., two mouse alpha-globin genes that duplicated after the human-mouse split are in-paralogues relative to human alpha-globin).  
  - **Out-Paralogues (Alloparalogues):** Paralogous genes that arose via gene duplication **BEFORE** the speciation event uniting the species (e.g., alpha-globin and beta-globin duplicated before the mammalian radiation; thus, human alpha-globin and mouse beta-globin are out-paralogues).

**c) Evolutionary Scrambling of Human Chr 17 vs Mouse Chr 11 (3 Marks):**  
* **Conserved Linkage (Synteny):** Over 80 million years since the human-mouse common ancestor, natural selection has kept the genes of ancestral Chromosome 17 linked on the same syntenic chromosome (Mouse Chr 11) because whole-chromosome fissions and inter-chromosomal translocations are often deleterious or meiotically disadvantageous.
* **Intra-Chromosomal Rearrangement Mechanisms:**  
  While inter-chromosomal translocations were purged, frequent **intra-chromosomal inversions** (both pericentric and paracentric) and non-allelic homologous recombination (NAHR) mediated by repetitive elements (LINEs/SINEs) occurred.  
  - An inversion breaks a segment, rotates it, and religates it within the same chromosome.  
  - Multiple successive overlapping inversions scramble the linear gene order into fragmented sub-blocks while preserving the physical membership of all genes on that single chromosome.

**Marking Scheme Breakdown:**  
* 4 Marks: Complete, properly labeled synteny dot-plot diagram accurately illustrating colinear (/), inverted (\), duplicated (//), and translocated segments.  
* 3 Marks: Accurate description of COG/eggNOG clustering and rigorous phylogenetic definitions of in-paralogues (post-speciation) vs out-paralogues (pre-speciation).  
* 3 Marks: Detailed evolutionary explanation of conserved linkage (purifying selection against translocations) vs intra-chromosomal inversion shuffling mediated by NAHR over 80 million years.
