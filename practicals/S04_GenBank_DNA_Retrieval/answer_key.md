# Instructor Answer Key & Evaluation Manual: Practical 04 (GenBank DNA Retrieval)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S04 (Syllabus Practical P4)  
**Curriculum Topic:** Retrieving DNA Sequence from GenBank and Analyzing Data Formats  

---

## 1. Expected Outputs & Reference Solutions

### Table 4.1: GenBank Flat File Structural Anatomy (`NM_000518.5`) (Completed)
| Section / Token | Extracted Value / Coordinates | Biological / Informatics Significance |
|---|---|---|
| `LOCUS` | `NM_000518  626 bp  mRNA  linear  PRI 14-OCT-2023` | Identifier, length, single-stranded mRNA, primate division |
| `DEFINITION` | `Homo sapiens hemoglobin subunit beta (HBB), mRNA.` | Official descriptive biological title |
| `ACCESSION` vs `VERSION` | Accession: `NM_000518`<br>Version: `NM_000518.5` | Base accession is permanent; `.5` indicates 5th official release update |
| `SOURCE` / `ORGANISM` | `Homo sapiens` (Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Mammalia; Primates; Hominidae; Homo) | Organism source and formal NCBI taxonomic classification lineage |
| `FEATURES` : `gene` | `1..626` (`/gene="HBB"`, `/db_xref="GeneID:3043"`, `/db_xref="HGNC:HGNC:4827"`) | Total transcript span represented by the gene model |
| `FEATURES` : `CDS` | `51..494` | Coding sequence boundary (start of start codon to end of stop codon) |
| `FEATURES` : `/codon_start` | `1` | Translation begins with the first base of the specified CDS span |
| `FEATURES` : `/protein_id` | `NP_000509.1` | Curated RefSeq protein counterpart accession |
| 5' UTR Span | `1..50` (50 bp) | Leader sequence upstream of the initiating AUG codon |
| 3' UTR Span | `495..626` (132 bp) | Trailer sequence downstream of the termination UAA codon |
| Poly-A Signal Sequence | Coordinates: `600..605`<br>Motif: `aataaa` | Cleavage and polyadenylation signal recognized by CPSF complex |
| `ORIGIN` End Token | `//` | Standard GenBank flat file termination token |

### Table 4.2: Comparison of Biological Sequence Formats (Completed)
| Feature / Characteristic | GenBank (`.gb`) | FASTA (`.fasta`) | EMBL (`.embl`) | GCG (`.gcg`) |
|---|---|---|---|---|
| Header Identifier Token | `LOCUS` | `>` | `ID` | Line ending with `..` |
| Feature Table Support (Yes/No) | Yes (`FEATURES`) | No | Yes (`FT`) | No (or basic header comments) |
| Literature Citations Included (Yes/No) | Yes (`REFERENCE`) | No | Yes (`RX`, `RA`, `RT`, `RL`) | No |
| Output File Size for `NM_000518` | ~5,500 – 6,000 bytes | ~700 bytes | ~5,800 – 6,200 bytes | ~900 bytes |
| Primary Use Case | NCBI comprehensive sequence curation | Fast sequence search & alignment | European archiving (ENA) | Legacy Wisconsin Package analysis |

---

## 2. Sample Converted File Layouts

### Converted EMBL Format (`hbb_converted.embl`)
```
ID   NM_000518; SV 5; linear; mRNA; STD; HUM; 626 BP.
XX
AC   NM_000518;
XX
DE   Homo sapiens hemoglobin subunit beta (HBB), mRNA.
XX
KW   .
XX
OS   Homo sapiens (human)
OC   Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Euteleostomi;
OC   Mammalia; Eutheria; Euarchontoglires; Primates; Haplorrhini;
OC   Catarrhini; Hominidae; Homo.
XX
FH   Key             Location/Qualifiers
FH
FT   gene            1..626
FT                   /gene="HBB"
FT   CDS             51..494
FT                   /gene="HBB"
FT                   /codon_start=1
FT                   /protein_id="NP_000509.1"
FT                   /translation="MVHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFES
FT                   FGDLSTPDAVMGNPKVKAHGKKVLGAFSDGLAHLDNLKGTFATLSELHCDKLHVDPEN
FT                   FRLLGNVLVCVLAHHFGKEFTPPVQAAYQKVVAGVANALAHKYH"
XX
SQ   Sequence 626 BP; 141 A; 216 C; 155 G; 114 T; 0 other;
     acatttgctt ctgacacaac tgtgttcact agcaacctca aacagacacc atggtgcatc        60
     ctgactcctg aggagaagtc tgccgttact gccctgtggg gcaaggtgaa cgtggatgaa       120
//
```

---

## 3. Model Answers to Discussion Questions

### Q1. Coding Sequence Mathematics
- **Model Answer:**
  - Coding range: `51..494`.
  - Total nucleotide length = $494 - 51 + 1 = 444$ nucleotides.
  - Number of codons = $444 / 3 = 148$ triplets.
  - The final codon is the termination stop codon (UAA, bases 492..494), which does not specify an amino acid during translation termination.
  - Number of encoded amino acids = $148 - 1 = 147$ amino acids.
  - This perfectly matches the 147 residue length of `NP_000509.1`.

### Q2. Accession vs. Version Numbering
- **Model Answer:** If a single nucleotide base is corrected in the sequence, the **accession number** (`NM_000518`) remains permanently unchanged because it identifies the biological locus and transcript entity. However, the **version number** is incremented from `NM_000518.5` to `NM_000518.6`. This mechanism is crucial for scientific reproducibility: an investigator can cite the exact version used in an analysis, allowing future researchers to distinguish between original observations and potential sequence revisions.

### Q3. The `/codon_start` Qualifier
- **Model Answer:** The `/codon_start=1` qualifier indicates that the reading frame is aligned such that the first nucleotide of the annotated CDS span corresponds to the first position of the first codon. If a cDNA clone is 5'-truncated and begins in the middle of a codon, the annotator specifies `/codon_start=2` or `/codon_start=3`. An automated translation algorithm reading `/codon_start=3` skips the first 2 nucleotides of the CDS coordinate block and begins translating triplets starting from the 3rd nucleotide.

### Q4. GenBank vs. EMBL Flat File Syntax
- **Model Answer:**
  - **GenBank:** Uses indented free-text keywords (`FEATURES`, `gene`, `CDS`) where column 1 contains section names, column 6 starts feature keys, and column 22 starts location coordinates or slashed qualifiers (`/qualifier="value"`).
  - **EMBL:** Uses strict two-character column codes at the beginning of every line (`ID` for identification, `AC` for accession, `FT` for feature table, `SQ` for sequence header, `XX` for spacer lines). In EMBL feature tables, each line begins with `FT` followed by column-aligned feature keys and locations.

### Q5. Machine-Readable ASN.1
- **Model Answer:** GenBank flat files were designed in the 1980s as human-readable report documents. Parsing them with regular expressions is prone to severe errors because qualifiers can span arbitrary lines, indentation can shift between software versions, and descriptive strings may contain reserved punctuation characters (slashes, quotation marks). By contrast, ASN.1 (Abstract Syntax Notation One) and XML are formal hierarchical data description languages with strict schemas. Parsers can deserialize ASN.1 trees into typed object models without textual ambiguity or regex failures.

---

## 4. Solution to Extension / Challenge Task

### Biopython Exon Extraction Script
```python
from Bio import SeqIO

gb_path = "../../data/genbank/hbb_human.gb"
record = SeqIO.read(gb_path, "genbank")

print(f"Record: {record.id}, Total Length: {len(record.seq)} bp")
total_exon_len = 0
exon_count = 0

for feat in record.features:
  if feat.type == "exon":
    exon_count += 1
    start = int(feat.location.start)  # 0-based
    end = int(feat.location.end)  # 1-based open
    span_len = end - start
    total_exon_len += span_len
    print(
        f"Exon {exon_count}: Coordinates [{start + 1}..{end}], Length:"
        f" {span_len} bp"
    )

print(f"Total Exon Length Sum: {total_exon_len} bp")
assert total_exon_len == len(
    record.seq
), "Error: Exon length does not match mRNA length!"
print("Verification: Exon length sum matches transcript length perfectly.")
```

### Expected Output
```
Record: NM_000518.5, Total Length: 626 bp
Exon 1: Coordinates [1..142], Length: 142 bp
Exon 2: Coordinates [143..365], Length: 223 bp
Exon 3: Coordinates [366..626], Length: 261 bp
Total Exon Length Sum: 626 bp
Verification: Exon length sum matches transcript length perfectly.
```

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & GenBank Dissection** | 2.0 | Deduct 0.5 if student fails to locate CDS or poly-A signal coordinates. |
| **Format Conversion Execution** | 4.0 | Deduct 1.0 per missing format file (FASTA, EMBL, GCG). |
| **Observation Tables (Table 4.1 & 4.2)** | 2.0 | Deduct 0.5 for incorrect format size or wrong UTR spans. |
| **Discussion Questions & CDS Calculation** | 2.0 | Award 0.4 marks per question (CDS math must clearly show deduction of stop codon). |
| **Total** | **10.0** | |
