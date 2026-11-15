# Quick Reference: GenBank Flat File Anatomy

A GenBank record consists of three principal divisions: **Header**, **Feature Table**, and **Sequence Data (ORIGIN)**.

---

## 1. Header Section

| Keyword | Content | Interpretation |
|---|---|---|
| `LOCUS` | `NM_000518 626 bp mRNA linear PRI 12-OCT-2023` | Locus name, length, molecule type, topology, division (`PRI` = primate), date |
| `DEFINITION` | `Homo sapiens hemoglobin subunit beta (HBB), mRNA.` | Concise biological description of the molecule |
| `ACCESSION` | `NM_000518` | Unique, permanent accession identifier assigned by INSDC/RefSeq |
| `VERSION` | `NM_000518.5` | Accession plus specific version number incremented upon any sequence edit |
| `KEYWORDS` | `RefSeq.` | Controlled indexing terms |
| `SOURCE` | `Homo sapiens (human)` | Common and formal taxonomy of the source organism |
| `REFERENCE` | `1 (bases 1 to 626)` | Literature citations documenting the discovery, sequencing, and annotation |

---

## 2. Feature Table (`FEATURES`)

Features describe functional regions. Each has a **Key** (e.g. `source`, `gene`, `CDS`, `exon`), a **Location**, and **Qualifiers** (`/qualifier="value"`).

### Location Syntax
- `51..494`: Continuous interval from base 51 through base 494 (inclusive, 1-based coordinates).
- `join(143..365, 366..626)`: Joined exons forming the spliced transcript.
- `complement(100..500)`: Feature located on the negative (reverse-complementary) strand.
- `<1..450`: Partial at the 5' end (sequence does not contain the complete upstream terminus).

### Key Features
- `source`: Mandatory first feature. Lists `/organism`, `/mol_type`, `/db_xref="taxon:9606"`, `/chromosome`.
- `gene`: Extent of the gene. Qualifiers: `/gene="HBB"`, `/db_xref="GeneID:3043"`.
- `CDS`: Coding Sequence (the region translated into protein).
  - `/codon_start=1`: Reading frame relative to the feature start (1, 2, or 3).
  - `/product="hemoglobin subunit beta"`
  - `/protein_id="NP_000509.1"`
  - `/translation="MVHLTPEEKSAVTAL..."`
- `exon`: Individual exon spans with `/number`.
- `regulatory`: Functional sites (e.g., `/regulatory_class="polyA_signal_sequence"`).

---

## 3. Sequence Section (`ORIGIN`)

```text
ORIGIN      
        1 acatttgctt ctgacacaac tgtgttcact agcaacctca aacagacacc atggtgcacc
       61 tgactcctga ggagaagtct gccgttactg ccctgtgggg caaggtgaac gtggatgaag
//
```
- Always begins with `ORIGIN`.
- Displayed in blocks of 10 bases, 60 bases per numbered line.
- The record terminates with `//` (two forward slashes on their own line).
