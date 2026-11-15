# Lecture 05 — ASN.1 and Bioseq Architecture

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 3:** The NCBI Data Model  
**Syllabus Topic:** Introduction, Seq-id, Sequence, collection of sequence, annotation of sequence, Describing sequence  
**Primary Learning Outcome:** LO1, LO2 — Describe what kinds of biological data exist, where each is stored, and parse the underlying data model.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Why a Formal Data Model?
================================================================================
Topic: Moving Beyond Flat Text Files

[Visual: A messy FASTA file with an unstructured header line 
         vs A strictly typed, hierarchical data structure (ASN.1)]

Speaker Bullets:
* Early bioinformatics relied on ad-hoc flat files where authors invented their own
  header conventions: ">my_seq from human liver maybe beta-globin".
* Computers cannot reliably validate, index, or parse unstructured strings.
* In 1989, NCBI designed a mathematically rigorous, object-oriented specification
  known as the **NCBI Data Model** implemented in **ASN.1 (Abstract Syntax Notation One)**.
```

```
================================================================================
SLIDE 2: What is ASN.1?
================================================================================
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

Speaker Bullets:
* ASN.1 is an international standard for describing structured data independent
  of computer architecture, programming language, or operating system.
* It defines both human-readable text syntax and compact binary encoding (BER).
```

```
================================================================================
SLIDE 3: The Atomic Unit: The Bioseq
================================================================================
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

Speaker Bullets:
* A `Bioseq` is the core atomic sequence object in NCBI.
* It combines identification (`Seq-id`), raw sequence physical attributes (`Seq-inst`),
  and metadata descriptions (`Seq-descr`).
```

```
================================================================================
SLIDE 4: Seq-id: Resolving Identity Without Ambiguity
================================================================================
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

Speaker Bullets:
* Because sequences originate from diverse repositories, `Seq-id` is an ASN.1 `CHOICE`.
* A single Bioseq can possess multiple `Seq-id` labels simultaneously (e.g. a RefSeq ID,
  a GenBank accession, and a historical GI).
```

```
================================================================================
SLIDE 5: Seq-inst: The Physical Sequence Instance
================================================================================
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

Speaker Bullets:
* `Seq-inst` defines the physical reality of the macromolecule.
* The sequence bytes can be stored in human ASCII (IUPAC) or packed 2-bit/4-bit binary.
```

```
================================================================================
SLIDE 6: Bioseq-set: Representing Collections of Sequences
================================================================================
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

Speaker Bullets:
* Sequences rarely exist in biological isolation.
* A `Bioseq-set` groups sequences:
  - `nuc-prot`: mRNA and its translated protein product.
  - `pop-set`: Population surveys (e.g. 100 human HBB alleles).
  - `phy-set`: Phylogenetic sets (e.g. 15 mammalian globin orthologues).
```

```
================================================================================
SLIDE 7: ASN.1 vs XML vs JSON
================================================================================
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

Speaker Bullets:
* ASN.1 was designed before XML and JSON existed; it remains the internal storage
  engine of NCBI.
* NCBI tools automatically translate the underlying ASN.1 objects into XML or JSON
  for modern web pipelines without altering the underlying data model semantics.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 05

* A data model decouples biological information from arbitrary presentation formats.
* The `Bioseq` is the atomic unit, comprising `Seq-id`, `Seq-inst`, and `Seq-descr`.
* `Bioseq-set` groups related molecules (e.g., `nuc-prot` bundles mRNA and protein).
* The GenBank flat file you read on screen is merely a rendered view generated
  from an underlying ASN.1 Bioseq tree!
* Next Lecture: Annotations, Features (`Seq-feat`), and Coordinate Syntax (`Seq-loc`).
```

---

## Detailed Comprehensive Technical Notes

### 1. The Engineering Rationale for Formal Data Specifications

In computer science, a **data model** is an abstract formalization that defines how data elements are structured, typed, related, and validated. Before 1990, computational biology relied on ad-hoc flat text formats:
- The **FASTA format** defined only a single-line descriptor prefixed by `>` followed by raw ASCII bases, offering zero mechanisms to encode coordinates, splice junctions, or organismal metadata.
- Early **GenBank and EMBL flat files** were designed for human visual inspection in printed catalogs; they contained informal whitespace indentations and unstructured text fields that caused frequent parser crashes whenever a human curator altered formatting.

To establish a scalable computing foundation, the National Center for Biotechnology Information (NCBI) established three architectural requirements:
1. **Separation of Presentation from Content:** The underlying biological data must exist as pure, typed data structures independent of how a web browser or terminal renders them.
2. **Strict Semantic Typing:** Every coordinate must be an integer; every molecule type must be an enumerated constant; every identifier must belong to a known namespace.
3. **Lossless Machine Translation:** The model must support automatic conversion into binary formats for disk efficiency and into text/XML formats for network distribution without losing metadata.

NCBI selected **Abstract Syntax Notation One (ASN.1)**, an International Organization for Standardization (ISO 8824/8825) standard widely utilized in telecommunications.

---

### 2. ASN.1 Structural Primitives in Biology

ASN.1 distinguishes between **primitive types** (indivisible atomic data) and **constructed types** (aggregations):

```
  Constructed Type   Semantic Rule                        Biological Analog
  -------------------------------------------------------------------------------------------------
  SEQUENCE           Ordered collection of named fields   Bioseq (has id, then inst, then descr)
  SET                Unordered collection of fields       Set of publications or descriptors
  CHOICE             Tagged union: exactly one of a list  Seq-id (can be GenBank OR RefSeq OR PDB)
  SEQUENCE OF        Ordered list of a repeating type     List of exon intervals in an mRNA
  SET OF             Unordered collection of a type       Set of homologous proteins in a cluster
```

The `CHOICE` construct is fundamental in bioinformatics: it allows software to accept multiple distinct forms of data under a single type constraint. For instance, a sequence coordinate might be an absolute integer position, a fuzzy boundary, or an open interval; `CHOICE` accommodates all three without ambiguous type conversions.

---

### 3. The `Bioseq` Architecture: Core Components

The fundamental building block of the NCBI data model is the **`Bioseq` (Biological Sequence)**. A `Bioseq` represents a single, continuous or segmented physical strand of nucleic acid or polypeptide.

```
                                    +-----------------------------+
                                    |           Bioseq            |
                                    +--------------+--------------+
                                                   |
                     +-----------------------------+-----------------------------+
                     |                             |                             |
                     v                             v                             v
           +-------------------+         +-------------------+         +-------------------+
           |    Seq-id (SET)   |         | Seq-inst (RECORD) |         | Seq-descr (LIST)  |
           +-------------------+         +-------------------+         +-------------------+
           | Unique identifiers|         | Physical properties|        | Global context    |
           | * RefSeq NM_...   |         | * Representation  |         | * Organism name   |
           | * GenBank acc     |         | * Molecule (DNA)  |         | * Title           |
           | * Gene ID         |         | * Length (626 bp) |         | * Literature pubs |
           |                   |         | * Raw sequence    |         | * Genetic code    |
           +-------------------+         +-------------------+         +-------------------+
```

#### A. `Seq-id` (Sequence Identifier)
A `Bioseq` maintains a `SET OF Seq-id`. This reflects biological reality: the same physical molecule may be tracked by an internal database key (`local`), an archival GenBank accession (`genbank`), a curated reference accession (`refseq`), or a structural registry (`pdb`).

#### B. `Seq-inst` (Sequence Instance)
`Seq-inst` describes the physical properties of the biological polymer:
- `repr` (Representation):
  - `raw`: Continuous, uninterrupted string of known sequence letters.
  - `seg` (Segmented): Composed of an ordered sequence of other `Bioseq` objects (e.g., an assembled chromosome built from BAC clones).
  - `const` (Constructed): Built by splicing coordinates from underlying sequences.
  - `virtual`: A sequence of known length but undetermined bases (e.g., an unsequenced physical gap).
- `mol`: The chemical nature of the polymer: `dna`, `rna`, `aa` (amino acid).
- `topology`: `linear` (eukaryotic nuclear DNA, typical proteins) vs `circular` (plasmids, mitochondrial genomes, bacterial chromosomes).
- `strand`: `ss` (single-stranded) vs `ds` (double-stranded).
- `length`: Exact integer count of monomers.
- `seq-data`: The underlying sequence storage, which can be encoded in ASCII IUPAC letters or memory-compressed 2-bit binary for genomic nucleotides ($A=00_2, C=01_2, G=10_2, T=11_2$).

---

### 4. `Bioseq-set`: Modeling Biological Collections

Sequences do not function in isolation. When an mRNA is transcribed and translated, the resulting mRNA and protein are two distinct chemical polymers linked by the genetic code. 

NCBI models this using the **`Bioseq-set`**:

```asn1
Bioseq-set ::= SEQUENCE {
    id        Dbtag OPTIONAL,
    coll      Dbtag OPTIONAL,
    level     INTEGER OPTIONAL,
    class     ENUMERATED {
        not-set (0),
        nuc-prot (1),      -- Nucleotide + translated protein
        segset (2),        -- Segmented sequence collection
        pop-set (4),       -- Population study (same locus, multiple individuals)
        phy-set (5),       -- Phylogenetic study (homologs across species)
        eco-set (6),       -- Ecological survey / metagenome
        gen-set (7),       -- Complete genomic set
        parts (9)          -- Parts of a segmented sequence
    },
    descr     Seq-descr OPTIONAL,
    seq-set   SET OF Bioseq-set-element
}
```

The **`nuc-prot` (Nucleotide-Protein)** set is the architecture behind every standard GenBank transcript entry. It bundles:
1. The **Nucleotide Bioseq** (`NM_000518.5`: 626 bp mRNA).
2. The **Protein Bioseq** (`NP_000509.1`: 147 aa beta-globin polypeptide).
3. The **CDS Feature (`Seq-feat`)** that mathematically defines the translation interval (`51..494`) and maps triplet codons to amino acids.

---

## Worked Example: Dissecting an ASN.1 Fragment for Human *HBB*

Below is an authentic snippet of the NCBI ASN.1 specification representing the human *HBB* `nuc-prot` set:

```asn1
Bioseq-set ::= {
  class nuc-prot,
  descr {
    source {
      genome genomic,
      org {
        taxname "Homo sapiens",
        common "human",
        lineage "Eukaryota; Metazoa; Chordata; Craniata; Vertebrata;
                 Euteleostomi; Mammalia; Eutheria; Euarchontoglires;
                 Primates; Haplorrhini; Catarrhini; Hominidae; Homo"
      }
    },
    title "Homo sapiens hemoglobin subunit beta (HBB), mRNA"
  },
  seq-set {
    -- 1. THE NUCLEOTIDE BIOSEQ
    seq {
      id {
        other {
          accession "NM_000518",
          version 5
        }
      },
      inst {
        repr raw,
        mol rna,
        length 626,
        topology linear,
        strand ss,
        seq-data ncbi2na '...binary bytes...'H
      }
    },
    -- 2. THE PROTEIN BIOSEQ
    seq {
      id {
        other {
          accession "NP_000509",
          version 1
        }
      },
      inst {
        repr raw,
        mol aa,
        length 147,
        topology linear,
        seq-data iupacaa "MVHLTPEEKSAVTALWGKVNVDEVGGEALGRLLVVYPWTQRFFESFGDLST..."
      }
    }
  }
}
```

### Key Architectural Takeaways from the Snippet:
1. The organism description (`Homo sapiens` taxonomic lineage) is written **once** in the parent `Bioseq-set.descr` block and is automatically inherited by both the nucleotide and protein child Bioseqs.
2. The nucleotide sequence (`NM_000518.5`) and protein sequence (`NP_000509.1`) are modeled as peer `Bioseq` objects packaged within the same collection.
3. The nucleotide sequence is encoded in binary (`ncbi2na`), while the protein sequence is stored in IUPAC amino acid characters (`iupacaa`).

---

## Formative In-Class Checks

### Question 1
**Prompt:** Why is an ASN.1 data model superior to a traditional FASTA text file for storing and distributing genomic sequence records across international database networks? Cite three concrete technical capabilities of the data model.

**Model Answer:**
An ASN.1 data model is superior because:
1. **Semantic Typing and Validation:** In ASN.1, every field has an enforced data type (e.g., `length` must be an integer, `mol` must be an enumerated class `dna|rna|aa`). FASTA stores only untyped raw text where coordinates and metadata are buried in an unstructured header string that parsers cannot rigorously validate.
2. **Explicit Biological Linkages (`Bioseq-set`):** The data model can bundle related biological entities together (such as a nucleotide mRNA Bioseq and its translated protein Bioseq in a `nuc-prot` set). In FASTA, the mRNA and protein must be saved in separate, disconnected files with no programmatic link between them.
3. **Machine-Efficient Binary Serialisation:** ASN.1 records can be compiled into compact binary formats (such as BER - Basic Encoding Rules) using 2-bit compressed nucleotides, drastically reducing disk storage, memory footprints, and network transmission times compared to ASCII text.

---

### Question 2
**Prompt:** In the NCBI data model, explain the relationship between a `Bioseq` and a `Bioseq-set`. Which one represents human *HBB* in NCBI Nucleotide?

**Model Answer:**
- A **`Bioseq`** is the atomic, indivisible container representing a single, physical polymer of DNA, RNA, or protein, characterized by an identifier (`Seq-id`), physical attributes (`Seq-inst`), and metadata (`Seq-descr`).
- A **`Bioseq-set`** is a higher-order container that groups multiple `Bioseq` objects together based on a shared biological relationship (e.g., population surveys, phylogenetic sets, or genomic assemblies).
- In the NCBI Nucleotide database, the curated record for human *HBB* is modeled as a **`nuc-prot` `Bioseq-set`**. It bundles the 626 bp mRNA `Bioseq` (`NM_000518.5`) together with its 147 aa translated protein `Bioseq` (`NP_000509.1`), connected by a coding region feature (`Seq-feat`).

---

### Question 3
**Prompt:** What is the function of the `CHOICE` construct in ASN.1? Give an example of how `CHOICE` is utilized in defining a sequence identifier (`Seq-id`).

**Model Answer:**
In ASN.1, a **`CHOICE`** represents a tagged union: a data structure that allows exactly one type out of a predefined list of alternatives to be selected. 

In defining sequence identifiers, `Seq-id` is specified as a `CHOICE`:
```asn1
Seq-id ::= CHOICE {
    local       Object-id,
    genbank     Textseq-id,
    refseq      Textseq-id,
    pdb         PDB-seq-id,
    ...
}
```
This enables NCBI software to handle sequences originating from different sources uniformly. A program can accept any valid `Seq-id` object, inspect its active tag (e.g., whether it is a RefSeq accession, a GenBank accession, or a PDB chain ID), and branch its parsing logic accordingly without type errors.
