---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 05 Slides: ASN.1 and Bioseq Architecture"
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
# Lecture 05 — ASN.1 and Bioseq Architecture
### Concepts of Bioinformatics (CBBI-501)
**Unit 03:** The NCBI Data Model  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Why a Formal Data Model?

```text
Topic: Moving Beyond Flat Text Files

[Visual: A messy FASTA file with an unstructured header line 
         vs A strictly typed, hierarchical data structure (ASN.1)]
```

**Speaker Talking Points:**  
* Early bioinformatics relied on ad-hoc flat files where authors invented their own
  header conventions: ">my_seq from human liver maybe beta-globin".
* Computers cannot reliably validate, index, or parse unstructured strings.
* In 1989, NCBI designed a mathematically rigorous, object-oriented specification
  known as the **NCBI Data Model** implemented in **ASN.1 (Abstract Syntax Notation One)**.

---

## Slide 2: What is ASN.1?

```text
Topic: Abstract Syntax Notation One (ISO 8824 / 8825)

+--------------------+--------------------+-----------------------------------+
| Primitive Type     | Biological Analog  | Example in ASN.1                  |
+--------------------+--------------------+-----------------------------------+
| `INTEGER`          | Coordinate / Count | `length 626`                      |
| `VisibleString`    | Accession / Text   | `accession "NM_000518"`           |
| `BOOLEAN`          | Flag / Feature     | `partial FALSE`                   |
| `ENUMERATED`       | Molecule Class     | `mol dna, rna, aa`                |
| `SEQUENCE`         | Ordered Record     | `Bioseq ::= { id {...}, inst ...}`|
| `CHOICE`           | Tagged Union       | `Seq-id ::= CHOICE { genbank ...}`|
+--------------------+--------------------+-----------------------------------+
```

**Speaker Talking Points:**  
* ASN.1 is an international standard for describing structured data independent
  of computer architecture, programming language, or operating system.
* It defines both human-readable text syntax and compact binary encoding (BER).

---

## Slide 3: The Atomic Unit: The Bioseq

```text
Topic: Anatomy of the Core Sequence Container

                         +-----------------------------+
                         |           Bioseq            |
                         | (The fundamental sequence)  |
                         +--------------+--------------+
                                        |
          +-----------------------------+-----------------------------+
          |                             |                             |
          v                             v                             v
   Seq-id (Set)                  Seq-inst (Instance)           Seq-descr (List)
   Identity tokens               Physical sequence data        Contextual descriptors
   (NM_000518.5, etc.)          (Bases, length, mol type)     (Source, title, pub)
```

**Speaker Talking Points:**  
* A `Bioseq` is the core atomic sequence object in NCBI.
* It combines identification (`Seq-id`), raw sequence physical attributes (`Seq-inst`),
  and metadata descriptions (`Seq-descr`).

---

## Slide 4: Seq-id: Resolving Identity Without Ambiguity

```text
Topic: The Tagged Union of Sequence Identifiers

  Seq-id ::= CHOICE {
    local       Object-id,           -- Internal database key
    gibbs       INTEGER,             -- Historical Gibbs sampler ID
    gi          INTEGER,             -- GenInfo Identifier (historical)
    genbank     Textseq-id,          -- Traditional GenBank accession.version
    refseq      Textseq-id,          -- Curated NCBI RefSeq token
    pdb         PDB-seq-id,          -- PDB structure chain identifier
    swissprot   Textseq-id           -- UniProtKB/Swiss-Prot identifier
  }
```

**Speaker Talking Points:**  
* Because sequences originate from diverse repositories, `Seq-id` is an ASN.1 `CHOICE`.
* A single Bioseq can possess multiple `Seq-id` labels simultaneously (e.g. a RefSeq ID,
  a GenBank accession, and a historical GI).

---

## Slide 5: Seq-inst: The Physical Sequence Instance

```text
Topic: Describing the Molecular Substance

+--------------------+--------------------------------------------------------+
| Seq-inst Attribute | Biological Meaning & Values                            |
+--------------------+--------------------------------------------------------+
| `repr`             | Representation: `raw` (continuous), `seg` (segmented), |
|                    | `const` (constructed contig), `virtual` (unsequenced)  |
| `mol`              | Molecule Type: `dna`, `rna`, `aa` (amino acid)         |
| `topology`         | Conformation: `linear` (eukaryotic), `circular` (plasmid)|
| `strand`           | Strandedness: `ss` (single), `ds` (double-stranded)    |
| `length`           | Exact integer count of monomers (e.g. 626 for HBB mRNA)|
| `seq-data`         | Actual byte-encoded sequence string                    |
+--------------------+--------------------------------------------------------+
```

**Speaker Talking Points:**  
* `Seq-inst` defines the physical reality of the macromolecule.
* The sequence bytes can be stored in human ASCII (IUPAC) or packed 2-bit/4-bit binary.

---

## Slide 6: Bioseq-set: Representing Collections of Sequences

```text
Topic: Packaging Biological Relationships

                    +-----------------------------------+
                    |            Bioseq-set             |
                    +-----------------+-----------------+
                                      |
         +----------------------------+----------------------------+
         |                                                         |
         v                                                         v
  Class: `nuc-prot`                                         Class: `pop-set`
  (Nucleotide-Protein Set)                                  (Population Set)
  * Parent mRNA Bioseq (NM_000518)                          * 50 HBB alleles sequenced
  * Child Protein Bioseq (NP_000509)                          across global human cohorts
  * CDS Seq-feat binding them together                      * Shared organism & locus
```

**Speaker Talking Points:**  
* Sequences rarely exist in biological isolation.
* A `Bioseq-set` groups sequences:
  - `nuc-prot`: mRNA and its translated protein product.
  - `pop-set`: Population surveys (e.g. 100 human HBB alleles).
  - `phy-set`: Phylogenetic sets (e.g. 15 mammalian globin orthologues).

---

## Slide 7: ASN.1 vs XML vs JSON

```text
Topic: Modern Serializations of the Data Model

  ASN.1 (Native NCBI):
    Bioseq ::= { id { refseq { accession "NM_000518", version 5 } }, ... }

  XML (NCBI INSDSeq / TinySeq):
    <INSDSeq>
      <INSDSeq_accession-version>NM_000518.5</INSDSeq_accession-version>
      <INSDSeq_length>626</INSDSeq_length>
    </INSDSeq>

  JSON (Modern Web APIs):
    { "accession": "NM_000518", "version": 5, "length": 626 }
```

**Speaker Talking Points:**  
* ASN.1 was designed before XML and JSON existed; it remains the internal storage
  engine of NCBI.
* NCBI tools automatically translate the underlying ASN.1 objects into XML or JSON
  for modern web pipelines without altering the underlying data model semantics.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 05

* A data model decouples biological information from arbitrary presentation formats.
* The `Bioseq` is the atomic unit, comprising `Seq-id`, `Seq-inst`, and `Seq-descr`.
* `Bioseq-set` groups related molecules (e.g., `nuc-prot` bundles mRNA and protein).
* The GenBank flat file you read on screen is merely a rendered view generated
  from an underlying ASN.1 Bioseq tree!
* Next Lecture: Annotations, Features (`Seq-feat`), and Coordinate Syntax (`Seq-loc`).
```

