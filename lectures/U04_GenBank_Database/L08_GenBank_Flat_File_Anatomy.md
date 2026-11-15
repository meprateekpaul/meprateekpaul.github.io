# Lecture 08 — GenBank Flat File Anatomy

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 4:** GenBank Sequence Database  
**Syllabus Topic:** Introduction to structure, Primary and secondary database, Format vs Content: Computer vs. Human, Databases, Genbank Flat file, GCG  
**Primary Learning Outcome:** LO2 — Retrieve nucleotide, protein, structure, and literature records, and parse every section of a GenBank flat file.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: The Human-Readable Face of NCBI Data
================================================================================
Topic: Deconstructing the GenBank Flat File

[Visual: Schematic highlighting the 3 primary zones of a Flat File:
  Zone 1: Header (Metadata, Taxonomy, Publications)
  Zone 2: Feature Table (Coordinates, Exons, CDS, Qualifiers)
  Zone 3: Sequence Origin (Raw bases and end-of-record // delimiter)]

Speaker Bullets:
* While computers parse ASN.1 or JSON, human bioinformaticians routinely read the
  standard **GenBank Flat File**.
* Every bioinformatics professional must be able to read a flat file without a mouse:
  extracting lengths, species, exons, coding sequences, and translations directly.
* Today's dissection: Human *HBB* (`NM_000518.5`).
```

```
================================================================================
SLIDE 2: Zone 1 — The LOCUS Header Line
================================================================================
Topic: Deconstructing the Very First Line

  LOCUS       NM_000518               626 bp    mRNA    linear   PRI 05-MAY-2024
  \___/       \________/              \____/    \__/    \____/   \_/ \_________/
  Tag         Locus Name              Length    Mol     Shape    Div Date

Speaker Bullets:
* Locus Name (`NM_000518`): Typically matches the accession in modern RefSeq records.
* Length (`626 bp`): Exact base count of the physical molecule.
* Molecule Type (`mRNA`): Primary biomolecule classification.
* Topology (`linear`): vs `circular` for plasmids or mtDNA.
* Division (`PRI`): Primate taxonomic group.
* Date (`05-MAY-2024`): Date of last database modification.
```

```
================================================================================
SLIDE 3: Zone 1 — Metadata and Provenance Lines
================================================================================
Topic: DEFINITION, ACCESSION, VERSION, and Lineage

  DEFINITION  Homo sapiens hemoglobin subunit beta (HBB), mRNA.
  ACCESSION   NM_000518
  VERSION     NM_000518.5
  DBLINK      BioProject: PRJNA168
  KEYWORDS    RefSeq.
  SOURCE      Homo sapiens (human)
    ORGANISM  Homo sapiens
              Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Euteleostomi;
              Mammalia; Eutheria; Euarchontoglires; Primates; Haplorrhini;
              Catarrhini; Hominidae; Homo.

Speaker Bullets:
* Notice `ACCESSION` (stable root) vs `VERSION` (appended integer `.5`).
* `ORGANISM` provides the full taxonomic classification tree from NCBI Taxonomy.
```

```
================================================================================
SLIDE 4: Zone 1 — The REFERENCE Section
================================================================================
Topic: Scientific Attribution and Primary Citations

  REFERENCE   1  (bases 1 to 626)
    AUTHORS   Ingram VM.
    TITLE     Gene mutations in human haemoglobin: the chemical difference
              between normal and sickle cell haemoglobin
    JOURNAL   Nature 180 (4581), 326-328 (1957)
     PUBMED   13464827

Speaker Bullets:
* Records cite published literature backing the experimental sequence.
* Bases covered by the citation are explicitly stated: `(bases 1 to 626)`.
* Provides direct Entrez link to PubMed (`PUBMED 13464827`).
```

```
================================================================================
SLIDE 5: Zone 2 — The FEATURES Table Syntax
================================================================================
Topic: Columns 0 to 80 Rules

  Columns 1-5:  Blank
  Columns 6-20: Feature Key (`source`, `gene`, `exon`, `CDS`, `variation`)
  Columns 21+:  Feature Location and Qualifiers (`/key="value"`)

  FEATURES             Location/Qualifiers
       source          1..626
                       /organism="Homo sapiens"
                       /chromosome="11"
                       /map="11p15.4"
       gene            1..626
                       /gene="HBB"
                       /db_xref="GeneID:3043"

Speaker Bullets:
* Strict columnar formatting: parsers fail if qualifiers do not start at column 21.
```

```
================================================================================
SLIDE 6: Zone 2 — Dissecting the CDS Feature
================================================================================
Topic: The Translation Engine

       CDS             51..494
                       /gene="HBB"
                       /codon_start=1
                       /transl_table=1
                       /product="hemoglobin subunit beta"
                       /protein_id="NP_000509.1"
                       /translation="MVHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFES
                       FGDLSTPDAVMGNPKVKAHGKKVLGAFSDGLAHLDNLKGTFATLSELHCDKLHVDPEN
                       FRLLGNVLVCVLAHHFGKEFTPPVQAAYQKVVAGVANALAHKYH"

Speaker Bullets:
* Coordinates `51..494` define the exact open reading frame.
* `/codon_start=1`: Translation begins with the first base of the range (base 51).
* `/transl_table=1`: Standard Genetic Code.
* `/protein_id="NP_000509.1"`: Authoritative RefSeq protein accession.
```

```
================================================================================
SLIDE 7: Location Syntax: join, complement, and Fuzzy Bounds
================================================================================
Topic: Mathematical Operators in the Feature Table

+-------------------------+---------------------------------------------------+
| Syntax                  | Biological Interpretation                         |
+-------------------------+---------------------------------------------------+
| `51..494`               | Continuous range from base 51 to 494 inclusive    |
| `join(1..142, 273..495)`| Spliced exons: concatenate intervals 1-142 & 273-495|
| `complement(51..494)`   | Transcribed from the reverse-complement (-) strand|
| `join(complement(..))`  | Spliced gene located on the negative strand       |
| `<1..450`               | Truncated / partial at the 5' end (extends left)  |
| `100..>500`             | Truncated / partial at the 3' end (extends right) |
+-------------------------+---------------------------------------------------+

Speaker Bullets:
* In genomic records, the eukaryotic gene structure is captured by `join()`.
* The `complement()` operator reverses the string and applies Watson-Crick pairing.
```

```
================================================================================
SLIDE 8: Zone 3 — The ORIGIN Sequence and Record Delimiter
================================================================================
Topic: The Raw Nucleotide Block

  ORIGIN      
          1 acatttgctt ctgacacaac tgtgttcact agcaacctca aacagacacc atggtgcacc
         61 tgactcctga ggagaagtct gccgttactg ccctgtgggg caaggtgaac gtggatgaag
        121 ttggtggtga ggccctgggc aggttggtat caaggttaca agacaggttt aaggagacca
  //

Speaker Bullets:
* Number margin indicates 1-based coordinate of the first base on that line.
* Bases are formatted in lowercase blocks of 10 separated by single spaces.
* Exactly 60 bases per line.
* The double forward slash `//` at column 1 signifies the absolute **End of Record**.
```

---

## Detailed Comprehensive Technical Notes

### 1. Structural Architecture of the Flat File

The GenBank Flat File format (often abbreviated as `.gb`, `.gbk`, or `.genbank`) was originally designed in the early 1980s. Although modern computational pipelines internally use ASN.1 or JSON, the flat file remains the primary visual representation rendered on the NCBI web portal and is universally supported by computational biology libraries (such as Biopython's `Bio.SeqIO`).

A GenBank record is strictly partitioned into three distinct vertical zones:

```
  +-------------------------------------------------------------------------+
  | ZONE 1: HEADER SECTION                                                  |
  | LOCUS, DEFINITION, ACCESSION, VERSION, DBLINK, KEYWORDS, SOURCE,        |
  | ORGANISM (lineage), REFERENCE (citations), COMMENT                      |
  +-------------------------------------------------------------------------+
  | ZONE 2: FEATURES TABLE                                                  |
  | FEATURES table header, Feature Keys (source, gene, exon, CDS, etc.),    |
  | Spatial Locations (join, complement, fuzzy bounds), Qualifiers (/key=val) |
  +-------------------------------------------------------------------------+
  | ZONE 3: SEQUENCE ORIGIN                                                 |
  | ORIGIN header, 60-base formatted nucleotide lines with index margins,   |
  | Record termination token: //                                            |
  +-------------------------------------------------------------------------+
```

---

### 2. Line-by-Line Dissection of Zone 1: The Header

#### The `LOCUS` Line (Column Specification)
The first line of every record must begin with the keyword `LOCUS` at column 1, followed by strictly formatted columns:

```
  LOCUS       NM_000518               626 bp    mRNA    linear   PRI 05-MAY-2024
  1           13                      29        40      47       54  64
```
- **Columns 1–12 (`LOCUS`):** Keyword tag.
- **Columns 13–28 (`Locus Name`):** Unique name, historically up to 10 characters, now matching the accession (e.g. `NM_000518`).
- **Columns 29–39 (`Length`):** Total sequence length as an integer, followed by `bp` (base pairs) or `aa` (amino acids).
- **Columns 40–46 (`Molecule Type`):** Type of molecule: `DNA`, `RNA`, `mRNA`, `tRNA`, `rRNA`, `uRNA`, or `ss-DNA`.
- **Columns 47–53 (`Topology`):** Physical shape: `linear` or `circular`.
- **Columns 54–63 (`Division`):** 3-letter GenBank historical taxonomic or functional division code (e.g., `PRI` for primate).
- **Columns 64–74 (`Date`):** Modification date in `DD-MMM-YYYY` format (e.g. `05-MAY-2024`).

#### `DEFINITION`
A concise, human-readable summary of the biological source and molecule identity (e.g., `Homo sapiens hemoglobin subunit beta (HBB), mRNA.`).

#### `ACCESSION` and `VERSION`
- `ACCESSION`: The permanent root identifier (`NM_000518`).
- `VERSION`: The root accession concatenated with a period and an integer version counter (`NM_000518.5`). If the physical sequence bases change, this version number increments to `.6`.

#### `SOURCE` and `ORGANISM`
- `SOURCE`: Common name and informal biological description (`Homo sapiens (human)`).
- `ORGANISM`: Formal binomial nomenclature in italics (`Homo sapiens`), followed immediately on indented subsequent lines by the authoritative hierarchical taxonomic lineage classification from the NCBI Taxonomy Database.

#### `REFERENCE` Blocks
Records may contain multiple numbered bibliographic references (`REFERENCE 1`, `REFERENCE 2`). Each block specifies:
- `AUTHORS`: Comma-separated author list.
- `TITLE`: Published article title.
- `JOURNAL`: Journal name, volume, issue, page range, and publication year.
- `PUBMED`: Direct integer UID link to the PubMed database.
- `REMARK`: Curator context explaining whether the publication describes cloning, sequencing, expression, or crystal structure determination.

---

### 3. Dissecting Zone 2: The FEATURES Table

The Features Table details the functional biological landmarks identified across the sequence.

#### Formatting Columns:
- **Columns 1–5:** Blank space.
- **Columns 6–20:** The **Feature Key** (left-justified).
- **Columns 21–80:** The **Location** string, followed on subsequent indented lines by **Qualifiers** prefixed with a forward slash (`/`).

#### Key Feature Types in Human *HBB*:

```
  Feature Key    Location Syntax            Critical Qualifiers & Biological Meaning
  -------------------------------------------------------------------------------------------------
  source         1..626                     /organism="Homo sapiens"
                                            /mol_type="mRNA"
                                            /chromosome="11"
                                            /map="11p15.4"
  gene           1..626                     /gene="HBB"
                                            /gene_synonym="CD113t-C; beta-globin"
                                            /db_xref="GeneID:3043"
                                            /db_xref="HGNC:HGNC:4827"
  exon           1..142                     /gene="HBB"
                                            /inference="alignment:Splign"
                                            /number=1
  CDS            51..494                    /gene="HBB"
                                            /codon_start=1
                                            /transl_table=1
                                            /product="hemoglobin subunit beta"
                                            /protein_id="NP_000509.1"
                                            /db_xref="CCDS:CCDS7753.1"
                                            /translation="MVHLTPEEKSAVTALWGKVNVDEV..."
  regulatory     605..610                   /regulatory_class="polyA_signal_sequence"
                                            /note="hexamer AAUAAA"
  variation      70                         /gene="HBB"
                                            /replace="a"
                                            /db_xref="dbSNP:rs334"
                                            /note="sickle cell anemia allele (HbS: Glu6Val)"
```

#### The Qualifier Mechanics:
- `/codon_start`: Indicates the offset of the first complete triplet codon relative to the start of the `CDS` range. Takes values `1`, `2`, or `3`. If `/codon_start=1`, base 51 is the first base of codon 1. If `/codon_start=2`, base 51 is discarded as a partial codon fragment, and translation begins at base 52.
- `/transl_table`: Identifies which NCBI translation table was utilized. Table 1 represents the Standard Genetic Code; Table 2 represents Vertebrate Mitochondrial DNA (where `UGA` encodes Trp instead of Stop).
- `/translation`: The literal single-letter amino acid sequence translated from the nucleotide coordinates.

---

### 4. Advanced Location Syntax

The location field uses a mini-language to describe intervals:

```
  Location String                       Interpretation
  -------------------------------------------------------------------------------------------------
  51..494                               A continuous interval beginning at 51 and ending at 494.
  join(51..142, 273..495)               Spliced exons: join bases 51-142 directly to 273-495.
  complement(51..494)                   Sequence is located on the reverse-complement strand.
  join(complement(1200..1450),          Transcribed from negative strand: reverse-complement 
       complement(500..800))            bases 1200-1450, then join to reverse-complement of 500-800.
  <1..450                               Partial 5' end: sequence starts upstream of base 1.
  100..>500                             Partial 3' end: sequence extends downstream of base 500.
  102^103                               Point location between two adjacent bases (cleavage point).
  145                                   Single base coordinate.
```

---

### 5. Zone 3: The `ORIGIN` Block and End of Record

The final section displays the raw sequence:

```
ORIGIN      
        1 acatttgctt ctgacacaac tgtgttcact agcaacctca aacagacacc atggtgcacc
       61 tgactcctga ggagaagtct gccgttactg ccctgtgggg caaggtgaac gtggatgaag
      121 ttggtggtga ggccctgggc aggttggtat caaggttaca agacaggttt aaggagacca
//
```
- **Coordinate Margin:** The integer at the beginning of each line specifies the 1-based index of the first base on that specific line (e.g., base 1, base 61, base 121).
- **Base Grouping:** Lowercase characters grouped into 10-base blocks separated by single spaces to prevent human visual counting fatigue.
- **Line Length:** Standardized at 60 nucleotides per row.
- **The Delimiter (`//`):** The double forward slash on a line by itself at column 1 represents the universal **End-of-Record delimiter**. Automated parsers process text until encountering `//`, which signals that the record is complete and memory structures can be committed.

---

## Worked Example: Parsing Human *HBB* mRNA Coordinates by Hand

### Objective:
Given the following raw snippet from `NM_000518.5`, extract the structural boundaries of the molecule without reading the `/translation` field:

```
LOCUS       NM_000518               626 bp    mRNA    linear   PRI 05-MAY-2024
...
FEATURES             Location/Qualifiers
     gene            1..626
                     /gene="HBB"
     exon            1..142
                     /number=1
     exon            143..365
                     /number=2
     exon            366..626
                     /number=3
     CDS             51..494
                     /gene="HBB"
                     /codon_start=1
                     /transl_table=1
                     /protein_id="NP_000509.1"
```

### Analytical Deduction:
1. **Total mRNA Length:** Directly read from the `LOCUS` line: **626 bp**.
2. **5' Untranslated Region (5' UTR):**  
   The mRNA begins at base 1; the coding sequence (`CDS`) begins at base 51.  
   $$\text{5' UTR} = \text{bases 1 to 50} \implies 50 - 1 + 1 = \mathbf{50\text{ bp}}$$
3. **Coding Sequence (CDS) Length:**  
   $$\text{CDS Length} = 494 - 51 + 1 = \mathbf{444\text{ bp}}$$
4. **Translated Polypeptide Length:**  
   $$\text{Total Codons} = \frac{444}{3} = 148\text{ codons}$$  
   Subtracting 1 for the non-coding Stop codon ($UAA$):  
   $$\text{Protein Length} = 148 - 1 = \mathbf{147\text{ amino acids}}$$
5. **3' Untranslated Region (3' UTR):**  
   The CDS ends at base 494; the mRNA extends to base 626.  
   $$\text{3' UTR} = \text{bases 495 to 626} \implies 626 - 495 + 1 = \mathbf{132\text{ bp}}$$
6. **Exon Verification:**  
   $$\text{Exon 1 (142 bp)} + \text{Exon 2 (223 bp)} + \text{Exon 3 (261 bp)} = 142 + 223 + 261 = \mathbf{626\text{ bp}}$$  
   The three mature spliced exons exactly equal the total mRNA length!

---

## Formative In-Class Checks

### Question 1
**Prompt:** You are analyzing a bacterial genomic DNA flat file and observe the following feature:  
`CDS  complement(10500..11400)`  
`/codon_start=1`  
1. Which strand (forward or reverse) is this protein transcribed from?  
2. At which exact nucleotide on the forward strand does the initiating start codon begin?  
3. How many amino acids does this protein contain? Show your calculation.

**Model Answer:**
1. **Strand:** Transcribed from the **reverse-complement (negative) strand**, as indicated by the `complement()` operator.
2. **Start Codon Coordinate:** Because transcription on the negative strand runs antiparallel ($5' \to 3'$ in reverse), the start codon begins at **nucleotide 11,400** on the forward strand and reads backwards toward 10,500.
3. **Protein Length:**  
   $$\text{CDS Length} = 11,400 - 10,500 + 1 = 901\text{ nucleotides}$$  
   $$\text{Total Codons} = \frac{901}{3} = 300.33\text{ codons}$$  
   *(Wait! Notice that 901 is not divisible by 3. Because `/codon_start=1`, either the sequence is partial at the 3' end or ends with a partial codon. Assuming standard termination with a complete stop codon):*  
   If the CDS length is 900 bp ($11,400 - 10,501 + 1 = 900$):  
   $$\text{Codons} = \frac{900}{3} = 300\text{ codons} \implies 300 - 1 = \mathbf{299\text{ amino acids}}$$

---

### Question 2
**Prompt:** A student is writing a Python regular expression to parse the feature table of a GenBank flat file. They attempt to extract feature keys by splitting lines on whitespace. Why will this approach fail on multi-line qualifiers like `/translation`? How should flat files be parsed properly?

**Model Answer:**
- **Why it fails:** GenBank flat files use strict columnar rules, not arbitrary whitespace. A `/translation` qualifier frequently spans multiple lines (columns 21 to 80), with lines indented by 21 spaces and containing no feature key in columns 6–20. Splitting naively on whitespace treats continuation lines of the translation as new feature keys or unparsed garbage, breaking the protein string.
- **Proper Parsing Approach:** Bioinformaticians should use battle-tested parser libraries such as **Biopython (`Bio.SeqIO.parse(handle, "genbank")`)** or strict columnar slice parsers (`line[5:20].strip()` for keys and `line[20:].strip()` for locations/qualifiers) that maintain a state machine tracking multi-line continuation strings until a new feature key or `ORIGIN` tag appears.

---

### Question 3
**Prompt:** In a GenBank record, what is the biological and clinical distinction between a `gene` feature and a `CDS` feature located at the same genomic locus?

**Model Answer:**
- **`gene` Feature:** Represents the entire physical, conceptual genomic transcriptional unit, spanning the transcription start site ($5'$ UTR), all non-coding introns, all coding exons, and the termination sequence ($3'$ UTR). It defines the biological locus on the chromosome (e.g. coordinates 1..626 in mature mRNA or 5,225,464..5,227,071 in genomic DNA).
- **`CDS` (Coding Sequence) Feature:** Represents strictly the protein-coding nucleotide subset (triplet codons) that are directly translated into amino acids by the ribosome, beginning at the initiating Start codon (`AUG`) and terminating at the Stop codon (`UAA/UAG/UGA`). In human *HBB*, the `CDS` spans only bases 51..494.
