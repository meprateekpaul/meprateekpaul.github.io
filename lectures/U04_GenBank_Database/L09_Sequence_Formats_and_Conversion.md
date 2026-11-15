# Lecture 09 — Sequence Formats and Conversion

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 4:** GenBank Sequence Database  
**Syllabus Topic:** Format vs Content: Computer vs. Human, Databases, Genbank Flat file, GCG  
**Primary Learning Outcome:** LO2 — Retrieve nucleotide, protein, structure, and literature records, and convert between sequence formats (FASTA, GenBank, EMBL, GCG).

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Format vs Content: The Bioinformatic Dichotomy
================================================================================
Topic: Separating Biological Information from File Framing

[Visual: A single biological sequence (Human HBB) wrapped in 4 different jackets:
  FASTA jacket | GenBank jacket | EMBL jacket | GCG jacket]

Speaker Bullets:
* "Content" is the objective biological truth: the sequence of nucleotides or amino acids,
  their biological source, and their physical features.
* "Format" is merely the syntactic container or file grammar chosen by software engineers
  to store, transmit, or render that content.
* A bioinformatician must never confuse the limitation of a file format with the reality
  of biological data.
```

```
================================================================================
SLIDE 2: Computer-Readable vs Human-Readable Formats
================================================================================
Topic: The Engineering Trade-off

+--------------------+-------------------------+------------------------------+
| Criterion          | Human-Readable Formats  | Machine-Optimized Formats    |
+--------------------+-------------------------+------------------------------+
| Examples           | GenBank Flat File, EMBL | ASN.1 BER, 2-bit, BAM, JSON  |
| Visual Inspection  | Easy via text editor    | Impossible without parser    |
| File Size          | Large (ASCII text)      | Minimal (compressed binary)  |
| Parsing Speed      | Slow (complex regex)    | Instantaneous memory mapping |
| Metadata Richness  | High (descriptive text) | Variable (strictly typed)    |
+--------------------+-------------------------+------------------------------+

Speaker Bullets:
* Humans want labels, indentation, and spaces; computers want fixed-width byte streams
  and binary structs.
* We use human-readable formats for inspection and machine-readable formats for pipelines.
```

```
================================================================================
SLIDE 3: The Universal Workhorse: FASTA Format
================================================================================
Topic: The Minimalist Standard (Lipman & Pearson, 1985)

  >NM_000518.5 Homo sapiens hemoglobin subunit beta (HBB), mRNA
  ACATTTGCTTCTGACACAACTGTGTTCACTAGCAACCTCAAACAGACACCATGGTGCACCTGACTCCTGA
  GGAGAAGTCTGCCGTTACTGCCCTGTGGGGCAAGGTGAACGTGGATGAAGTTGGTGGTGAGGCCCTGGGC
  AGGTTGGTATCAAGGTTACAAGACAGGTTTAAGGAGACCAATAGAAACTGGGCATGTGGAGACAGAGAAG

Speaker Bullets:
* Line 1: Definition line ("defline") prefixed by a greater-than symbol (`>`).
* Followed immediately by raw, unformatted IUPAC nucleotide or amino acid characters.
* Multi-FASTA files simply concatenate multiple sequence records sequentially.
* Weakness: Zero ability to store feature coordinates (exons, CDS) or publication metadata.
```

```
================================================================================
SLIDE 4: The European Standard: EMBL Flat File Syntax
================================================================================
Topic: Two-Letter Line Designators

  ID   NM_000518; SV 5; linear; mRNA; STD; HUM; 626 BP.
  XX
  AC   NM_000518;
  XX
  DE   Homo sapiens hemoglobin subunit beta (HBB), mRNA.
  XX
  OS   Homo sapiens (human)
  OC   Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Mammalia...
  XX
  FH   Key             Location/Qualifiers
  FT   CDS             51..494
  XX
  SQ   Sequence 626 BP; 141 A; 173 C; 160 G; 152 T; 0 other;
       acatttgctt ctgacacaac tgtgttcact agcaacctca aacagacacc atggtgcacc   60
  //

Speaker Bullets:
* Maintained by EMBL-EBI / ENA.
* Replaces verbose GenBank keywords with strict 2-letter tokens (`ID`, `AC`, `DE`, `FT`, `SQ`).
* Separator line: `XX`. End of record: `//`.
```

```
================================================================================
SLIDE 5: The Historical Giant: GCG / Wisconsin Package
================================================================================
Topic: The Legacy Format Named in Your Syllabus

  !!NA_SEQUENCE 1.0
  Human beta-globin mRNA from GenBank NM_000518
  NM_000518  Length: 626  05-MAY-2024  Type: N  Check: 4521  ..

         1  ACATTTGCTT CTGACACAAC TGTGTTCACT AGCAACCTCA AACAGACACC
        51  ATGGTGCACC TGACTCCTGA GGAGAAGTCT GCCGTTACTG CCCTGTGGGG

Speaker Bullets:
* Created by the Genetics Computer Group (Univ. of Wisconsin) in 1982.
* Features:
  - Header line ending with two consecutive dots (`..`) separating metadata from sequence.
  - Mandatory checksum (`Check: 4521`) to detect file corruption on floppy disks/tapes.
* While the Wisconsin Package was discontinued, legacy tools still expect this syntax.
```

```
================================================================================
SLIDE 6: Automated Format Conversion: EMBOSS `seqret`
================================================================================
Topic: The Swiss Army Knife of Sequence Formats

[Visual: EMBOSS seqret Engine:
  Input (GenBank / EMBL / GCG / SwissProt)
           |
           v [EMBOSS Internal Data Model]
           |
  Output (FASTA / Clustal / Phylip / GCG / ASN.1)]

Command:
  `seqret -sequence hbb.gbk -outseq hbb.fasta -osformat fasta`

Speaker Bullets:
* The European Molecular Biology Open Software Suite (**EMBOSS**) contains `seqret`.
* Never write custom text-replacement scripts to convert formats; use standard,
  RFC-compliant bioinformatic engines (`seqret` or Biopython `Bio.SeqIO`).
```

```
================================================================================
SLIDE 7: Depositing Sequences: From Bench to GenBank
================================================================================
Topic: How Biological Data Reaches the Archive

1. BankIt:
   * Web-based form wizard at NCBI.
   * Best for single sequences, simple mRNAs, or small-scale PCR surveys (<100 records).

2. Sequin / table2asn:
   * High-throughput command-line submission utility.
   * Takes raw FASTA files + 5-column feature annotation tables (`.tbl`).
   * Compiles and validates complete ASN.1 submission packages for whole genomes.

Speaker Bullets:
* When your laboratory sequences a new gene, you use `table2asn` to generate
  the official submission package before publishing your paper.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 09

* Format is the syntactic vehicle; Content is the biological substance.
* FASTA is minimal and universal; GenBank and EMBL are feature-rich and hierarchical.
* GCG format represents a historically important milestone featuring the `..` divider
  and mathematical checksums.
* EMBOSS `seqret` and Biopython handle seamless format conversion across all types.
* Next Unit: Sequence Alignment — Biological basis, Homology vs Similarity, and Dot Plots.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Philosophical Dichotomy: Format vs Content

In computational biology, novice researchers often confuse the syntax of a file with its biological semantics. A nucleotide sequence consisting of 626 base pairs encoding human beta-globin represents **content**. 

That exact same biological content can be stored in over 20 distinct **formats**:
- As a **FASTA file**: minimal, stripped of all feature annotations, containing only a header line and raw ASCII bases.
- As a **GenBank Flat File**: verbose, human-readable, containing taxonomic trees, literature citations, and a columnar feature table.
- As an **EMBL Flat File**: European two-letter tokenized syntax.
- As an **ASN.1 object**: strictly typed, object-oriented, machine-parsable tree.
- As an **XML / JSON document**: web-standard hierarchical markup.
- As a **GCG / Wisconsin Package file**: legacy format with mathematical checksums and two-dot separators.

Software developers must design systems that operate on the underlying **biological data model** rather than hard-coding assumptions tied to a specific file format's layout.

---

### 2. Major Bioinformatic Sequence Formats

```
  Format Name            Origin / Agency        Structural Identifier                 Primary Strength
  -------------------------------------------------------------------------------------------------
  FASTA                  Lipman & Pearson (1985)`>` at Column 1                       Universal, lightweight
  GenBank Flat File      NCBI (USA)             `LOCUS` at Col 1; `//` at end         Rich metadata, features
  EMBL Flat File         EMBL-EBI (Europe)      2-letter line tokens (`ID`, `AC`, `//`)Tokenized, clean parsing
  GCG / Wisconsin        Univ. of Wisconsin     Two dots `..` on header; `Check:`     Checksum verification
  ASN.1                  NCBI / ISO             Nested braces `{ ... }`               Strictly typed data model
  PDB / mmCIF            wwPDB Consortium       `ATOM`, `HETATM` fixed columns        3D Cartesian coordinates
```

---

### 3. Detailed Anatomy of Formats

#### A. The FASTA Format
Created for the FASTP/FASTA software package by David Lipman and William Pearson in 1985, FASTA is the undisputed universal standard for biological sequence exchange.

```fasta
>NM_000518.5 Homo sapiens hemoglobin subunit beta (HBB), mRNA
ACATTTGCTTCTGACACAACTGTGTTCACTAGCAACCTCAAACAGACACCATGGTGCACCTGACTCCTGA
GGAGAAGTCTGCCGTTACTGCCCTGTGGGGCAAGGTGAACGTGGATGAAGTTGGTGGTGAGGCCCTGGGC
```
- **The Defline:** The first line must begin with a greater-than symbol (`>`). The text immediately following `>` up to the first whitespace character is treated by parsers as the **unique sequence identifier**. Everything after the first whitespace is treated as an optional descriptive title.
- **Sequence Body:** Subsequent lines contain sequence characters in single-letter IUPAC notation. Whitespace, numbers, and carriage returns are ignored by compliant parsers.
- **Multi-FASTA:** Multiple records are concatenated sequentially. When a parser encounters a new line starting with `>`, it terminates the previous sequence and initializes a new record.

#### B. The EMBL Flat File Format
Developed by the European Molecular Biology Laboratory, the EMBL format uses standardized two-letter line type prefixes followed by three spaces:

```embl
ID   NM_000518; SV 5; linear; mRNA; STD; HUM; 626 BP.
XX
AC   NM_000518;
XX
DE   Homo sapiens hemoglobin subunit beta (HBB), mRNA.
XX
OS   Homo sapiens (human)
OC   Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Mammalia; Eutheria;
OC   Euarchontoglires; Primates; Haplorrhini; Catarrhini; Hominidae; Homo.
XX
FH   Key             Location/Qualifiers
FH
FT   source          1..626
FT                   /organism="Homo sapiens"
FT                   /chromosome="11"
FT   CDS             51..494
FT                   /gene="HBB"
FT                   /product="hemoglobin subunit beta"
FT                   /protein_id="NP_000509.1"
XX
SQ   Sequence 626 BP; 141 A; 173 C; 160 G; 152 T; 0 other;
     acatttgctt ctgacacaac tgtgttcact agcaacctca aacagacacc atggtgcacc       60
     tgactcctga ggagaagtct gccgttactg ccctgtgggg caaggtgaac gtggatgaag      120
//
```
- `ID`: Identification line (accession, version, topology, molecule, division, length).
- `AC`: Accession number(s).
- `DE`: Description.
- `OS` / `OC`: Organism Species and Organism Classification.
- `FH` / `FT`: Feature Header and Feature Table lines.
- `SQ`: Sequence Header followed by nucleotide base counts.
- `XX`: Blank spacer line separating logical sections.
- `//`: Universal terminator.

#### C. The GCG (Genetics Computer Group) / Wisconsin Package Format
The Genetics Computer Group at the University of Wisconsin developed the Wisconsin Package in 1982. For fifteen years, GCG was the dominant academic and commercial sequence analysis suite.

```gcg
!!NA_SEQUENCE 1.0
Human beta-globin mRNA sequence from GenBank NM_000518
NM_000518  Length: 626  05-MAY-2024  Type: N  Check: 4521  ..

       1  ACATTTGCTT CTGACACAAC TGTGTTCACT AGCAACCTCA AACAGACACC
      51  ATGGTGCACC TGACTCCTGA GGAGAAGTCT GCCGTTACTG CCCTGTGGGG
     101  CAAGGTGAAC GTGGATGAAG TTGGTGGTGA GGCCCTGGGC AGGTTGGTAT
```

**Key Architectural Features of GCG Format:**
1. **Magic Header:** Starts with `!!NA_SEQUENCE 1.0` (for nucleic acids) or `!!AA_SEQUENCE 1.0` (for amino acids).
2. **The Two-Dot Separator (`..`):** GCG parsers scan text lines looking for two consecutive period characters (`..`). Everything preceding the two dots is treated as documentation; the sequence begins immediately on the line following `..`.
3. **The GCG Checksum:** To detect bit flips, truncated magnetic tapes, and corrupted downloads, GCG computed a deterministic mathematical integer checksum on the sequence letters (`Check: 4521`). If a file was altered by a single byte, the recalculated checksum failed, and GCG programs refused to run.

---

### 4. Format Conversion Engines: EMBOSS and Biopython

Manually editing file formats or writing custom Python string replacements (`split()`, `replace()`) is prone to errors. Standardized conversion utilities should always be used.

#### A. EMBOSS `seqret`
The European Molecular Biology Open Software Suite (**EMBOSS**) includes the definitive command-line format conversion utility: **`seqret`**.

```bash
# Convert a GenBank flat file to standard FASTA
seqret -sequence hbb.gbk -outseq hbb.fasta -osformat fasta

# Convert a GenBank flat file to European EMBL format
seqret -sequence hbb.gbk -outseq hbb.embl -osformat embl

# Convert FASTA to legacy GCG format
seqret -sequence hbb.fasta -outseq hbb.gcg -osformat gcg
```

#### B. Programmatic Conversion via Biopython (`Bio.SeqIO`)
In modern Python workflows, `Bio.SeqIO` provides a unified input/output interface:

```python
from Bio import SeqIO

# Read a GenBank flat file and write as FASTA in a single line
count = SeqIO.convert("hbb.gbk", "genbank", "hbb.fasta", "fasta")
print(f"Converted {count} records successfully.")

# Inspect features before conversion
for record in SeqIO.parse("hbb.gbk", "genbank"):
    print(f"ID: {record.id}")
    print(f"Features present: {len(record.features)}")
    for feat in record.features:
        if feat.type == "CDS":
            print(f"CDS Location: {feat.location}")
            print(f"Translated Protein: {feat.qualifiers['translation'][0][:30]}...")
```

---

### 5. Sequence Submission Pipelines: From Bench to GenBank

When an experimentalist sequences a novel gene or complete genome, they must deposit the data into the INSDC to receive an accession number prior to journal publication.

```
                  +----------------------------------------------+
                  |         Raw Experimental Sequence Data       |
                  |     (Sanger electropherograms, NGS contigs)   |
                  +----------------------+-----------------------+
                                         |
         +-------------------------------+-------------------------------+
         | (Small-scale: <100 genes)                                     | (Large-scale / Genomes)
         v                                                               v
  +-----------------------+                                     +-----------------------+
  |    NCBI BankIt Web    |                                     |    NCBI table2asn     |
  | (Interactive wizard)  |                                     |  (Command-line tool)  |
  +-----------+-----------+                                     +-----------+-----------+
              |                                                             |
              |                                                 Takes:      |
              |                                                 * FASTA (.fsa)
              |                                                 * 5-col table (.tbl)
              |                                                 * Template (.sbt)
              \______________________________+______________________________/
                                             |
                                             v
                              +-----------------------------+
                              | ASN.1 Submission (.sqn file)|
                              | Validated by NCBI curators  |
                              | Assigned Accession Number   |
                              +-----------------------------+
```

1. **BankIt:** A web-based interactive questionnaire suitable for researchers submitting a few ribosomal RNA (16S rRNA) sequences, viral isolates, or individual cDNA fragments.
2. **`table2asn` (formerly `tbl2asn` / `Sequin`):** A high-performance command-line utility used by sequencing centers and bioinformaticians. It accepts:
   - A FASTA file containing raw genomic scaffolds (`genome.fsa`).
   - A 5-column tab-delimited feature table (`genome.tbl`) specifying gene and CDS coordinates.
   - A submitter information template (`template.sbt`).
   `table2asn` compiles these files into a binary ASN.1 submission file (`genome.sqn`) while performing hundreds of validation checks (flagging internal stop codons, invalid splice sites, and misaligned reading frames).

---

## Worked Example: Calculating a GCG Checksum by Hand

### The Algorithm:
The historical GCG checksum calculates a 16-bit integer hash by iterating across the uppercase sequence characters. For each character $i$, its ASCII integer value is multiplied by $( (i \pmod{57}) + 1 )$, summed into an accumulator, and reduced modulo 10,000:

$$\text{Check} = \left( \sum_{i=1}^{L} \text{ASCII}(c_i) \times ((i \pmod{57}) + 1) \right) \pmod{10000}$$

### Worked Toy Sequence: `HBB` peptide fragment `VHLT`
Let us calculate the checksum for the 4-amino acid string `VHLT`:

```
  Index (i)   Residue   ASCII Value   Weight = ((i % 57) + 1)   Product
  ------------------------------------------------------------------------
  1           V         86            (1 % 57) + 1 = 2          86 * 2 = 172
  2           H         72            (2 % 57) + 1 = 3          72 * 3 = 216
  3           L         76            (3 % 57) + 1 = 4          76 * 4 = 304
  4           T         84            (4 % 57) + 1 = 5          84 * 5 = 420
  ------------------------------------------------------------------------
  Sum:                                                          1,112
  Modulo 10,000:                                                1,112
```

The header line in a GCG file for this peptide will read:
```gcg
VHLT  Length: 4  Type: P  Check: 1112  ..
```
If a researcher accidentally typed `I` instead of `L` (ASCII 73 instead of 76), the sum would change to 1,100, triggering an immediate `CHECKSUM MISMATCH ERROR` when loaded into GCG.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A student converts a rich GenBank flat file (`NM_000518.gbk`) into a FASTA file (`hbb.fasta`). Later, they realize they need to reconstruct the original GenBank flat file from the FASTA file. Can this conversion be performed losslessly? Explain why or why not.

**Model Answer:**
**No, this conversion is strictly LOSSY and CANNOT be reversed.**
- The GenBank flat file contains extensive hierarchical metadata: organism taxonomy, bibliographic citations (PubMed IDs), exon-intron coordinate boundaries, CDS definitions, genetic code tables, and variation records (dbSNP links).
- The FASTA format retains **only** the defline header string and the raw nucleotide letters. 
- Converting GenBank $\to$ FASTA discards all feature tables and metadata. Converting FASTA back to GenBank produces an empty skeleton containing raw bases with zero biological annotations.

---

### Question 2
**Prompt:** In the legacy GCG sequence format, what is the syntactic significance of the two consecutive period characters (`..`), and what catastrophic error occurs if a text editor accidentally deletes them?

**Model Answer:**
- **Syntactic Significance:** In GCG format, the two consecutive periods (`..`) serve as the **formal boundary divider** separating the free-text documentation header from the sequence data block.
- **What occurs if deleted:** GCG parsing engines scan the file line by line searching specifically for `..`. If this divider is missing, the parser fails to find the sequence start delimiter, assumes the entire file is unformatted header commentary, and throws a fatal error: *"No sequence found"* or *"Header termination syntax missing"*.

---

### Question 3
**Prompt:** Write the command to convert an EMBL-format file `sample.embl` into a standard FASTA file named `sample.fa` using the EMBOSS `seqret` tool.

**Model Answer:**
```bash
seqret -sequence sample.embl -outseq sample.fa -osformat fasta
```
*(Alternative syntax: `seqret sample.embl fasta::sample.fa`)*
