---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 06 Slides: Annotations, Features, and Descriptors"
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
# Lecture 06 — Annotations, Features, and Descriptors
### Concepts of Bioinformatics (CBBI-501)
**Unit 03:** The NCBI Data Model  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Describing vs Annotating Sequences

```text
Topic: The Dual Layer of Biological Metadata

[Visual: A raw DNA tape 5'-...-3'
  Layer 1 (Global): Who sequenced it, what species, which paper -> Descriptors (Seq-descr)
  Layer 2 (Local): Where is the promoter, exon 1, codon 6 -> Features (Seq-feat)]
```

**Speaker Talking Points:**  
* In the NCBI data model, there is a strict conceptual distinction between:
  1. Describing a sequence (global properties applying to the entire molecule).
  2. Annotating a sequence (local biological landmarks tied to specific coordinates).
* Confusing these two layers leads to data corruption; the data model enforces
  their separation via `Seq-descr` and `Seq-annot` / `Seq-feat`.

---

## Slide 2: Seq-descr: Global Sequence Descriptors

```text
Topic: Metadata That Applies Globally to a Bioseq

+--------------------+--------------------------------------------------------+
| Descriptor Type    | Biological Scope & Content                             |
+--------------------+--------------------------------------------------------+
| `title`            | Formal descriptive title of the record                 |
| `source`           | `BioSource`: Organism taxonomy, tissue, organelle      |
| `pub`              | Citations to published papers validating the sequence  |
| `molinfo`          | Biomolecule classification (mRNA, genomic), status     |
| `comment`          | Free-text curation remarks or historical notes         |
| `user`             | Structured user data (e.g. NCBI RefSeq tracking flags) |
+--------------------+--------------------------------------------------------+
```

**Speaker Talking Points:**  
* `Seq-descr` is a list of descriptors attached to a `Bioseq` or `Bioseq-set`.
* Descriptors do NOT possess coordinate boundaries; they apply universally.

---

## Slide 3: Scope and Inheritance in Descriptor Trees

```text
Topic: Hierarchical Metadata Propagation

                   +----------------------------------+
                   |     Bioseq-set: class nuc-prot   |
                   |  descr: BioSource = Homo sapiens |
                   +----------------+-----------------+
                                    |
            +-----------------------+-----------------------+
            |                                               |
            v                                               v
  +-------------------+                           +-------------------+
  |   mRNA Bioseq     |                           |   Protein Bioseq  |
  |  (NM_000518.5)    |                           |   (NP_000509.1)   |
  +-------------------+                           +-------------------+
  (Inherits organism                              (Inherits organism
   Homo sapiens)                                   Homo sapiens)
```

**Speaker Talking Points:**  
* Descriptors placed at the root of a `Bioseq-set` cascade downward.
* You do not need to re-type the organism taxonomy for every translated protein;
  the child Bioseq inherits the parent descriptor automatically!

---

## Slide 4: Seq-annot and Seq-feat: Localized Biological Features

```text
Topic: Anchoring Information to Coordinate Intervals

                         +-----------------------------+
                         |          Seq-feat           |
                         |     (Sequence Feature)      |
                         +--------------+--------------+
                                        |
          +-----------------------------+-----------------------------+
          |                             |                             |
          v                             v                             v
     data (CHOICE)                 location (Seq-loc)             qualifiers
   What kind of feature?         Where is it on the tape?       Extra metadata
   (gene, cdregion, rna, var)    (coordinates 51..494)          (/gene="HBB")
```

**Speaker Talking Points:**  
* A `Seq-feat` is an explicit, localized biological annotation.
* It must always specify:
  1. `data`: The feature type (e.g., coding region, gene, SNP, binding site).
  2. `location`: The exact mathematical interval on the sequence.

---

## Slide 5: Seq-loc: Spatial Coordinate Syntax in 1D Space

```text
Topic: Defining Intervals on Nucleic Acids and Proteins

+--------------------+--------------------------------------------------------+
| Seq-loc Variant    | Coordinate Representation & Biological Example         |
+--------------------+--------------------------------------------------------+
| `Seq-point`        | Single integer position: coordinate 51 (Cleavage site) |
| `Seq-interval`     | Continuous span: `from 50, to 493` (0-based inside)    |
| `mix`              | Spliced / discontinuous intervals: exons 1, 2, and 3   |
| Fuzzy boundaries   | Partial coordinates: `<` (partial 5'), `>` (partial 3')|
| Strand tag         | `plus` (+), `minus` (- / reverse complement), `both`   |
+--------------------+--------------------------------------------------------+
```

**Speaker Talking Points:**  
* `Seq-loc` handles complex eukaryotic gene structures:
  `join(51..142, 273..495)` is modeled as a `mix` of distinct `Seq-interval` objects.

---

## Slide 6: The Anatomy of a Coding Region: cdregion

```text
Topic: The Feature that Translates DNA to Protein

  Seq-feat ::= {
    data cdregion {
      frame 1,                       -- Reading frame offset (1, 2, or 3)
      code { id 1 },                 -- Genetic code table (Table 1: Standard)
      code-break { ... }             -- Non-standard codon re-assignments
    },
    location int {
      from 50, to 493,               -- 0-based coordinates for 51..494
      id other { accession "NM_000518", version 5 }
    },
    product {
      whole other { accession "NP_000509", version 1 }
    }
  }
```

**Speaker Talking Points:**  
* The `cdregion` feature contains the exact mathematical translation rule.
* `product` points directly to the `Seq-id` of the translated polypeptide Bioseq!

---

## Slide 7: Mapping ASN.1 to the GenBank Flat File View

```text
Topic: How the Data Model Renders What You See

  NCBI Data Model Object                 Rendered GenBank Flat File Line
  -------------------------------------------------------------------------
  Bioseq.inst.length & mol        -->    LOCUS       626 bp    mRNA
  Bioseq-set.descr.title          -->    DEFINITION  Homo sapiens HBB...
  Bioseq.id                       -->    ACCESSION   NM_000518
  Bioseq.id (version)             -->    VERSION     NM_000518.5
  Seq-descr.source (BioSource)    -->    SOURCE      Homo sapiens
  Seq-feat (gene)                 -->    FEATURES    gene    1..626
  Seq-feat (cdregion)             -->    FEATURES    CDS     51..494
  Bioseq.inst.seq-data            -->    ORIGIN      1 acatttgctt...
```

**Speaker Talking Points:**  
* Every single line of a GenBank flat file is generated by a specific branch
  of the ASN.1 object hierarchy.

---

## Slide 8: Summary & Key Takeaways

```text
Topic: Core Concepts from Lecture 06

* `Seq-descr` captures global molecule context (organism, title, publications).
* `Seq-feat` anchors localized functional annotations to precise coordinates via `Seq-loc`.
* Spliced exons and reverse strands are handled natively by `mix` and `strand` attributes.
* A GenBank flat file is not an original document; it is a human-friendly projection
  of the NCBI ASN.1 object tree.
* Next Unit: The GenBank Sequence Database — Primary vs Secondary databases,
  line-by-line flat file anatomy, and format conversion.
```

