# Practical 04: Retrieving DNA Sequences from GenBank and Analyzing Biological Data Formats

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S04 (Syllabus Practical P4)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO2 — Retrieve nucleotide records, dissect the GenBank flat file structure, interpret the Feature Table (`join`, `complement`), and interconvert biological file formats.

---

## 1. Aim & Objectives

### Aim
To retrieve nucleotide records from NCBI GenBank, dissect every structural component and feature tag of the GenBank flat file format, analyze the NCBI ASN.1 data model representation, and perform sequence format conversions between FASTA, GenBank, EMBL, and GCG formats.

### Objectives
1. Retrieve the human beta-globin (*HBB*) mRNA transcript record (`NM_000518.5`) from the NCBI Nucleotide database.
2. Systematically dissect and annotate the GenBank flat file sections: `LOCUS`, `DEFINITION`, `ACCESSION`, `VERSION`, `DBLINK`, `KEYWORDS`, `SOURCE`, `ORGANISM`, `REFERENCE`, `FEATURES`, and `ORIGIN`.
3. Interpret the **Feature Table (FT)** syntax: qualifiers, `gene`, `exon`, `CDS`, `regulatory`, `misc_feature`, translation tables, and location operators (`join`, `complement`).
4. View and contrast alternative machine-readable formats: NCBI ASN.1 text and XML.
5. Perform sequence format conversion using the EMBOSS utility `seqret` (or Biopython `SeqIO`) to convert GenBank flat files into FASTA, EMBL, and legacy GCG format.

---

## 2. Background & Scientific Principle

### GenBank and the INSDC Exchange
The **GenBank** sequence database is the NIH genetic sequence database, an annotated collection of all publicly available DNA sequences. Together with the European Nucleotide Archive (ENA) at EMBL-EBI and the DNA Data Bank of Japan (DDBJ), GenBank forms the **International Nucleotide Sequence Database Collaboration (INSDC)**. These three organizations exchange new and updated data daily, ensuring that sequence accessions are globally synchronized.

### The GenBank Flat File Architecture
Although modern databases store records as relational objects or structured ASN.1/XML hierarchies, the **GenBank Flat File (GBFF)** remains the primary human-readable format for sequence inspection. A standard flat file is divided into three major structural blocks:

1. **Header Block (Descriptive Metadata):**
   - `LOCUS` : Locus name, sequence length, molecule type (mRNA, DNA, ss-RNA), topology (linear or circular), GenBank division (e.g., `PRI` for primate), and date of last modification.
   - `DEFINITION` : Concise description of the biological sequence.
   - `ACCESSION` : The permanent unique identifier for the sequence (does not change).
   - `VERSION` : The accession number followed by a dot and version number (e.g., `NM_000518.5`). If even a single nucleotide is corrected, the version number increments, while the base accession remains constant.
   - `DBLINK` : Cross-references to BioProject, BioSample, and other repositories.
   - `KEYWORDS` : Controlled keywords (frequently unannotated in RefSeq records).
   - `SOURCE` & `ORGANISM` : Common organism name and formal NCBI taxonomic lineage tree.
   - `REFERENCE` : Scientific literature citations documenting the sequence discovery and characterization.

2. **Feature Table Block (`FEATURES`):**
   Contains biological annotation mapped to specific sequence coordinate spans.
   - **Feature Keys:** The category of biological entity (e.g., `source`, `gene`, `exon`, `CDS`, `regulatory`).
   - **Location Syntax:**
     - `1..626` : Contiguous span from nucleotide 1 to 626.
     - `join(51..142, 273..495)` : Spliced segments concatenated together in the mature transcript.
     - `complement(100..500)` : Transcribed from the opposite (minus) DNA strand.
     - `<1..>600` : Partial sequence extending beyond the sequenced clone boundaries.
   - **Qualifiers:** Slashed tags providing descriptive attributes (e.g., `/gene="HBB"`, `/protein_id="NP_000509.1"`, `/translation="..."`).

3. **Sequence Data Block (`ORIGIN`):**
   - Begins with the token `ORIGIN`.
   - Sequence lines are indexed in blocks of 10 nucleotides, 60 bases per line, preceded by a line number base count.
   - Terminates with the end-of-record delimiter: two forward slashes (`//`).

### Format vs. Content: The Machine vs. Human Dilemma
A biological sequence consists fundamentally of a string of nucleotide or amino acid characters. However, computational processing requires explicit metadata. Multiple formats evolved historically:
- **FASTA:** Minimalist header (`>`) followed by raw sequence. Lacks coordinate-level annotation.
- **GenBank / EMBL:** Rich, comprehensive feature annotation tables.
- **GCG (Genetics Computer Group):** Historical Wisconsin Package format featuring checksums and base counts.
- **ASN.1 / XML:** Strictly validated, hierarchical, machine-parseable data exchange models.

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & Local Software
- NCBI Nucleotide: [https://www.ncbi.nlm.nih.gov/nucleotide/](https://www.ncbi.nlm.nih.gov/nucleotide/)
- EMBOSS Software Suite: `seqret` command-line utility (or Biopython script).
- Text editor: VS Code, nano, or gedit.

### Input Datasets & Accessions
- Target Accession: Human *HBB* mRNA (`NM_000518.5`, 626 bp).
- Local Pre-retrieved Flat File: `../../data/genbank/hbb_human.gb`.
- Local FASTA Records: `../../data/sequences/hbb_human_mrna.fasta`, `../../data/sequences/hbb_human_cds.fasta`.

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Retrieving `NM_000518.5` from NCBI Nucleotide
1. Open [https://www.ncbi.nlm.nih.gov/nucleotide/](https://www.ncbi.nlm.nih.gov/nucleotide/).
2. In the search box, enter `NM_000518.5` and click **Search**.
3. The GenBank flat file view loads directly.
4. Locate the display format selector at the top left (default is **GenBank**):
   - Click the **FASTA** link to observe how the view strips all metadata except the `>` definition line.
   - Return to the **GenBank** view.
5. In the top right corner, click **Send to:**
   - Choose Destination: **File**
   - Format: **GenBank (full)**
   - Click **Create File**. A file named `sequence.gb` will download.

### Phase 2: Dissecting the GenBank Flat File Anatomy
Open the downloaded `sequence.gb` (or local file `../../data/genbank/hbb_human.gb`) in a text editor and locate each of the following sections:

1. **The `LOCUS` Line:**
   - Identify the Locus name, molecule length (626 bp), molecule type (`mRNA`), division (`PRI`), and release date.
2. **Accession and Version Tracking:**
   - Locate the `ACCESSION` line (`NM_000518`).
   - Locate the `VERSION` line (`NM_000518.5`).
3. **Organism and Source Hierarchy:**
   - Identify `/organism="Homo sapiens"` and the complete taxonomic classification.
4. **Dissecting the Feature Table (`FEATURES`):**
   - Find the `gene` feature: Record the coordinate span (`1..626`) and HGNC symbol (`HBB`).
   - Find the `exon` features: Record the coordinate boundaries for Exon 1, Exon 2, and Exon 3.
   - Find the `CDS` (Coding Sequence) feature:
     - Record the exact coding coordinates: `51..494`.
     - Record the `/codon_start=1` qualifier.
     - Note the `/protein_id="NP_000509.1"`.
     - Note the conceptual translation string (`MVHLTPEEKS...`).
   - Identify the 5' Untranslated Region (5' UTR: coordinates `1..50`) and the 3' Untranslated Region (3' UTR: coordinates `495..626`).
   - Locate the polyadenylation signal (`regulatory` feature, `misc_feature`, or `/regulatory_class="polyA_signal_sequence"` around bases `600..605`: `aataaa`).

### Phase 3: Viewing ASN.1 and XML Representations
1. On the NCBI Nucleotide web page for `NM_000518.5`, locate the format dropdown or click on the **More formats** option.
2. Select **ASN.1 (text)** or navigate to the URL parameter `&report=asn1`.
3. Observe how the same biological data is structured as nested structured trees (`Seq-entry`, `Bioseq`, `Seq-id`, `Seq-inst`).
4. Note how machine parsers can navigate ASN.1 without regex ambiguity.

### Phase 4: Format Conversion using EMBOSS `seqret`
EMBOSS `seqret` is the standard bioinformatics utility for reading sequence files in one format and writing them to another.
1. In your Linux terminal, verify that EMBOSS is available:
   ```bash
   seqret -version || python3 -c "import Bio; print('Biopython available')"
   ```
2. Convert the GenBank flat file to standard FASTA format:
   ```bash
   seqret -sequence ../../data/genbank/hbb_human.gb -outseq hbb_converted.fasta -osformat2 fasta
   ```
3. Convert the GenBank flat file to European Molecular Biology Laboratory (EMBL) flat file format:
   ```bash
   seqret -sequence ../../data/genbank/hbb_human.gb -outseq hbb_converted.embl -osformat2 embl
   ```
4. Convert to legacy GCG format:
   ```bash
   seqret -sequence ../../data/genbank/hbb_human.gb -outseq hbb_converted.gcg -osformat2 gcg
   ```
5. *(Fallback if EMBOSS is not installed):* Use the provided Python script:
   ```bash
   python3 -c "
   from Bio import SeqIO
   record = SeqIO.read('../../data/genbank/hbb_human.gb', 'genbank')
   SeqIO.write(record, 'hbb_converted.fasta', 'fasta')
   SeqIO.write(record, 'hbb_converted.embl', 'embl')
   print('Format conversion completed successfully via Biopython.')
   "
   ```
6. Inspect the converted files using `head -n 25`:
   - Notice the two-letter line codes in EMBL (`ID`, `AC`, `DE`, `KW`, `OS`, `FT`, `SQ`).
   - Compare them against the GenBank flat file.

---

## 5. Offline Fallback Note

If internet access to NCBI Nucleotide is unavailable:
- Use the complete pre-packaged GenBank record in `../../data/genbank/hbb_human.gb`.
- All format conversion commands (`seqret` or Biopython) run locally on the workstation filesystem using `../../data/genbank/hbb_human.gb`.

---

## 6. Observations Table

### Table 4.1: GenBank Flat File Structural Anatomy (`NM_000518.5`)
| Section / Token | Extracted Value / Coordinates | Biological / Informatics Significance |
|---|---|---|
| `LOCUS` | | Name, length, molecule type, division |
| `DEFINITION` | | Human-readable title description |
| `ACCESSION` vs `VERSION` | Accession: <br>Version: | Distinguishes immutable record ID from version |
| `SOURCE` / `ORGANISM` | | Common name and full taxonomic lineage |
| `FEATURES` : `gene` | | Full gene span on the transcript |
| `FEATURES` : `CDS` | | Coding sequence coordinates |
| `FEATURES` : `/codon_start` | | Reading frame offset (1, 2, or 3) |
| `FEATURES` : `/protein_id` | | Derived RefSeq protein identifier |
| 5' UTR Span | | Non-coding leader sequence |
| 3' UTR Span | | Non-coding trailer sequence |
| Poly-A Signal Sequence | | Consensus hexanucleotide motif |
| `ORIGIN` End-of-Record Token | | Delimiter signaling termination of flat file |

### Table 4.2: Comparison of Biological Sequence Formats
| Feature / Characteristic | GenBank (`.gb`) | FASTA (`.fasta`) | EMBL (`.embl`) | GCG (`.gcg`) |
|---|---|---|---|---|
| Header Identifier Token | `LOCUS` | `>` | `ID` | Line with `..` |
| Feature Table Support (Yes/No) | | | | |
| Literature Reference Inclusion (Yes/No) | | | | |
| File Size for `NM_000518` (bytes) | | | | |
| Primary Use Case | Full curation | Alignment/Search | European archiving | Legacy GCG suite |

---

## 7. Interpretation & Discussion Questions

1. **Coding Sequence Mathematics:** The CDS is annotated as `51..494`. Calculate the total length of the coding region in nucleotides. How many amino acids does this encode (accounting for the termination stop codon)? Does this match the 147 aa length of `NP_000509.1`? Show your calculation.
2. **Accession vs. Version Numbering:** Suppose an sequencing update corrects a single base call in the 3' UTR of `NM_000518.5`. What will happen to the accession number, and what will happen to the version number? Why is this convention essential for biomedical reproducibility?
3. **The `/codon_start` Qualifier:** What does the qualifier `/codon_start=1` indicate? If a fragmented cDNA sequence in GenBank has `/codon_start=3`, how must an automated translation algorithm adjust its reading frame?
4. **GenBank vs. EMBL Flat File Syntax:** Contrast the syntax used by GenBank and EMBL to denote feature tables. How does GenBank indicate qualifiers versus EMBL's two-character column codes?
5. **Machine-Readable ASN.1:** Why is it computationally error-prone to write automated web scrapers that parse GenBank flat files with regular expressions, compared to parsing structured ASN.1 or XML schemas?

---

## 8. Extension / Challenge Task (For Advanced Students)

Write a short Python script (using Biopython `SeqIO`) that:
1. Parses `../../data/genbank/hbb_human.gb`.
2. Automatically loops through all `record.features`.
3. Detects every feature of type `exon` and prints its start coordinate, end coordinate, and total length.
4. Verifies whether the sum of the exon lengths equals the total sequence length of the mRNA (626 bp).
