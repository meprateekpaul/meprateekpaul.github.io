---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 08 Slides: GenBank Flat File Anatomy"
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
# Lecture 08 — GenBank Flat File Anatomy
### Concepts of Bioinformatics (CBBI-501)
**Unit 04:** GenBank Sequence Database  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: The Human-Readable Face of NCBI Data

```text
Topic: Deconstructing the GenBank Flat File

[Visual: Schematic highlighting the 3 primary zones of a Flat File:
  Zone 1: Header (Metadata, Taxonomy, Publications)
  Zone 2: Feature Table (Coordinates, Exons, CDS, Qualifiers)
  Zone 3: Sequence Origin (Raw bases and end-of-record // delimiter)]
```

**Speaker Talking Points:**  
* While computers parse ASN.1 or JSON, human bioinformaticians routinely read the
  standard **GenBank Flat File**.
* Every bioinformatics professional must be able to read a flat file without a mouse:
  extracting lengths, species, exons, coding sequences, and translations directly.
* Today's dissection: Human *HBB* (`NM_000518.5`).

---

## Slide 2: Zone 1 — The LOCUS Header Line

```text
Topic: Deconstructing the Very First Line

  LOCUS       NM_000518               626 bp    mRNA    linear   PRI 05-MAY-2024
  \___/       \________/              \____/    \__/    \____/   \_/ \_________/
  Tag         Locus Name              Length    Mol     Shape    Div Date
```

**Speaker Talking Points:**  
* Locus Name (`NM_000518`): Typically matches the accession in modern RefSeq records.
* Length (`626 bp`): Exact base count of the physical molecule.
* Molecule Type (`mRNA`): Primary biomolecule classification.
* Topology (`linear`): vs `circular` for plasmids or mtDNA.
* Division (`PRI`): Primate taxonomic group.
* Date (`05-MAY-2024`): Date of last database modification.

---

## Slide 3: Zone 1 — Metadata and Provenance Lines

```text
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
```

**Speaker Talking Points:**  
* Notice `ACCESSION` (stable root) vs `VERSION` (appended integer `.5`).
* `ORGANISM` provides the full taxonomic classification tree from NCBI Taxonomy.

---

## Slide 4: Zone 1 — The REFERENCE Section

```text
Topic: Scientific Attribution and Primary Citations

  REFERENCE   1  (bases 1 to 626)
    AUTHORS   Ingram VM.
    TITLE     Gene mutations in human haemoglobin: the chemical difference
              between normal and sickle cell haemoglobin
    JOURNAL   Nature 180 (4581), 326-328 (1957)
     PUBMED   13464827
```

**Speaker Talking Points:**  
* Records cite published literature backing the experimental sequence.
* Bases covered by the citation are explicitly stated: `(bases 1 to 626)`.
* Provides direct Entrez link to PubMed (`PUBMED 13464827`).

---

## Slide 5: Zone 2 — The FEATURES Table Syntax

```text
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
```

**Speaker Talking Points:**  
* Strict columnar formatting: parsers fail if qualifiers do not start at column 21.

---

## Slide 6: Zone 2 — Dissecting the CDS Feature

```text
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
```

**Speaker Talking Points:**  
* Coordinates `51..494` define the exact open reading frame.
* `/codon_start=1`: Translation begins with the first base of the range (base 51).
* `/transl_table=1`: Standard Genetic Code.
* `/protein_id="NP_000509.1"`: Authoritative RefSeq protein accession.

---

## Slide 7: Location Syntax: join, complement, and Fuzzy Bounds

```text
Topic: Mathematical Operators in the Feature Table

+-------------------------+---------------------------------------------------+
| Syntax                  | Biological Interpretation                         |
+-------------------------+---------------------------------------------------+
| `51..494`               | Continuous range from base 51 to 494 inclusive    |
| `join(1..142, 273..495)`| Spliced exons: concatenate intervals 1-142 & 273-495|
| `complement(51..494)`   | Transcribed from the reverse-complement (-) strand|
| `complement(join(..))`  | Spliced gene located on the negative strand       |
| `<1..450`               | Truncated / partial at the 5' end (extends left)  |
| `100..>500`             | Truncated / partial at the 3' end (extends right) |
+-------------------------+---------------------------------------------------+
```

**Speaker Talking Points:**  
* In genomic records, the eukaryotic gene structure is captured by `join()`.
* The `complement()` operator reverses the string and applies Watson-Crick pairing.

---

## Slide 8: Zone 3 — The ORIGIN Sequence and Record Delimiter

```text
Topic: The Raw Nucleotide Block

  ORIGIN      
          1 acatttgctt ctgacacaac tgtgttcact agcaacctca aacagacacc atggtgcacc
         61 tgactcctga ggagaagtct gccgttactg ccctgtgggg caaggtgaac gtggatgaag
        121 ttggtggtga ggccctgggc aggttggtat caaggttaca agacaggttt aaggagacca
  //
```

**Speaker Talking Points:**  
* Number margin indicates 1-based coordinate of the first base on that line.
* Bases are formatted in lowercase blocks of 10 separated by single spaces.
* Exactly 60 bases per line.
* The double forward slash `//` at column 1 signifies the absolute **End of Record**.

