---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 09 Slides: Sequence Formats and Conversion"
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
# Lecture 09 — Sequence Formats and Conversion
### Concepts of Bioinformatics (CBBI-501)
**Unit 04:** GenBank Sequence Database  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Format vs Content: The Bioinformatic Dichotomy

```text
Topic: Separating Biological Information from File Framing

[Visual: A single biological sequence (Human HBB) wrapped in 4 different jackets:
  FASTA jacket | GenBank jacket | EMBL jacket | GCG jacket]
```

**Speaker Talking Points:**  
* "Content" is the objective biological truth: the sequence of nucleotides or amino acids,
  their biological source, and their physical features.
* "Format" is merely the syntactic container or file grammar chosen by software engineers
  to store, transmit, or render that content.
* A bioinformatician must never confuse the limitation of a file format with the reality
  of biological data.

---

## Slide 2: Computer-Readable vs Human-Readable Formats

```text
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
```

**Speaker Talking Points:**  
* Humans want labels, indentation, and spaces; computers want fixed-width byte streams
  and binary structs.
* We use human-readable formats for inspection and machine-readable formats for pipelines.

---

## Slide 3: The Universal Workhorse: FASTA Format

```text
Topic: The Minimalist Standard (Lipman & Pearson, 1985)

  >NM_000518.5 Homo sapiens hemoglobin subunit beta (HBB), mRNA
  ACATTTGCTTCTGACACAACTGTGTTCACTAGCAACCTCAAACAGACACCATGGTGCACCTGACTCCTGA
  GGAGAAGTCTGCCGTTACTGCCCTGTGGGGCAAGGTGAACGTGGATGAAGTTGGTGGTGAGGCCCTGGGC
  AGGTTGGTATCAAGGTTACAAGACAGGTTTAAGGAGACCAATAGAAACTGGGCATGTGGAGACAGAGAAG
```

**Speaker Talking Points:**  
* Line 1: Definition line ("defline") prefixed by a greater-than symbol (`>`).
* Followed immediately by raw, unformatted IUPAC nucleotide or amino acid characters.
* Multi-FASTA files simply concatenate multiple sequence records sequentially.
* Weakness: Zero ability to store feature coordinates (exons, CDS) or publication metadata.

---

## Slide 4: The European Standard: EMBL Flat File Syntax

```text
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
```

**Speaker Talking Points:**  
* Maintained by EMBL-EBI / ENA.
* Replaces verbose GenBank keywords with strict 2-letter tokens (`ID`, `AC`, `DE`, `FT`, `SQ`).
* Separator line: `XX`. End of record: `//`.

---

## Slide 5: The Historical Giant: GCG / Wisconsin Package

```text
Topic: The Legacy Format Named in Your Syllabus

  !!NA_SEQUENCE 1.0
  Human beta-globin mRNA from GenBank NM_000518
  NM_000518  Length: 626  05-MAY-2024  Type: N  Check: 4521  ..

         1  ACATTTGCTT CTGACACAAC TGTGTTCACT AGCAACCTCA AACAGACACC
        51  ATGGTGCACC TGACTCCTGA GGAGAAGTCT GCCGTTACTG CCCTGTGGGG
```

**Speaker Talking Points:**  
* Created by the Genetics Computer Group (Univ. of Wisconsin) in 1982.
* Features:
  - Header line ending with two consecutive dots (`..`) separating metadata from sequence.
  - Mandatory checksum (`Check: 4521`) to detect file corruption on floppy disks/tapes.
* While the Wisconsin Package was discontinued, legacy tools still expect this syntax.

---

## Slide 6: Automated Format Conversion: EMBOSS `seqret`

```text
Topic: The Swiss Army Knife of Sequence Formats

[Visual: EMBOSS seqret Engine:
  Input (GenBank / EMBL / GCG / SwissProt)
           |
           v [EMBOSS Internal Data Model]
           |
  Output (FASTA / Clustal / Phylip / GCG / ASN.1)]

Command:
  `seqret -sequence hbb.gbk -outseq hbb.fasta -osformat fasta`
```

**Speaker Talking Points:**  
* The European Molecular Biology Open Software Suite (**EMBOSS**) contains `seqret`.
* Never write custom text-replacement scripts to convert formats; use standard,
  RFC-compliant bioinformatic engines (`seqret` or Biopython `Bio.SeqIO`).

---

## Slide 7: Depositing Sequences: From Bench to GenBank

```text
Topic: How Biological Data Reaches the Archive

1. BankIt:
   * Web-based form wizard at NCBI.
   * Best for single sequences, simple mRNAs, or small-scale PCR surveys (<100 records).

2. Sequin / table2asn:
   * High-throughput command-line submission utility.
   * Takes raw FASTA files + 5-column feature annotation tables (`.tbl`).
   * Compiles and validates complete ASN.1 submission packages for whole genomes.
```

**Speaker Talking Points:**  
* When your laboratory sequences a new gene, you use `table2asn` to generate
  the official submission package before publishing your paper.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 09

* Format is the syntactic vehicle; Content is the biological substance.
* FASTA is minimal and universal; GenBank and EMBL are feature-rich and hierarchical.
* GCG format represents a historically important milestone featuring the `..` divider
  and mathematical checksums.
* EMBOSS `seqret` and Biopython handle seamless format conversion across all types.
* Next Unit: Sequence Alignment — Biological basis, Homology vs Similarity, and Dot Plots.
```

