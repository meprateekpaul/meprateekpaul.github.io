# Lecture 06 — Annotations, Features, and Descriptors

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 3:** The NCBI Data Model  
**Syllabus Topic:** Introduction, Seq-id, Sequence, collection of sequence, annotation of sequence, Describing sequence  
**Primary Learning Outcome:** LO1, LO2 — Describe what kinds of biological data exist, where each is stored, and parse annotations, features, and descriptors.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Describing vs Annotating Sequences
================================================================================
Topic: The Dual Layer of Biological Metadata

[Visual: A raw DNA tape 5'-...-3'
  Layer 1 (Global): Who sequenced it, what species, which paper -> Descriptors (Seq-descr)
  Layer 2 (Local): Where is the promoter, exon 1, codon 6 -> Features (Seq-feat)]

Speaker Bullets:
* In the NCBI data model, there is a strict conceptual distinction between:
  1. Describing a sequence (global properties applying to the entire molecule).
  2. Annotating a sequence (local biological landmarks tied to specific coordinates).
* Confusing these two layers leads to data corruption; the data model enforces
  their separation via `Seq-descr` and `Seq-annot` / `Seq-feat`.
```

```
================================================================================
SLIDE 2: Seq-descr: Global Sequence Descriptors
================================================================================
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

Speaker Bullets:
* `Seq-descr` is a list of descriptors attached to a `Bioseq` or `Bioseq-set`.
* Descriptors do NOT possess coordinate boundaries; they apply universally.
```

```
================================================================================
SLIDE 3: Scope and Inheritance in Descriptor Trees
================================================================================
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

Speaker Bullets:
* Descriptors placed at the root of a `Bioseq-set` cascade downward.
* You do not need to re-type the organism taxonomy for every translated protein;
  the child Bioseq inherits the parent descriptor automatically!
```

```
================================================================================
SLIDE 4: Seq-annot and Seq-feat: Localized Biological Features
================================================================================
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

Speaker Bullets:
* A `Seq-feat` is an explicit, localized biological annotation.
* It must always specify:
  1. `data`: The feature type (e.g., coding region, gene, SNP, binding site).
  2. `location`: The exact mathematical interval on the sequence.
```

```
================================================================================
SLIDE 5: Seq-loc: Spatial Coordinate Syntax in 1D Space
================================================================================
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

Speaker Bullets:
* `Seq-loc` handles complex eukaryotic gene structures:
  `join(51..142, 273..495)` is modeled as a `mix` of distinct `Seq-interval` objects.
```

```
================================================================================
SLIDE 6: The Anatomy of a Coding Region: cdregion
================================================================================
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

Speaker Bullets:
* The `cdregion` feature contains the exact mathematical translation rule.
* `product` points directly to the `Seq-id` of the translated polypeptide Bioseq!
```

```
================================================================================
SLIDE 7: Mapping ASN.1 to the GenBank Flat File View
================================================================================
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

Speaker Bullets:
* Every single line of a GenBank flat file is generated by a specific branch
  of the ASN.1 object hierarchy.
```

```
================================================================================
SLIDE 8: Summary & Key Takeaways
================================================================================
Topic: Core Concepts from Lecture 06

* `Seq-descr` captures global molecule context (organism, title, publications).
* `Seq-feat` anchors localized functional annotations to precise coordinates via `Seq-loc`.
* Spliced exons and reverse strands are handled natively by `mix` and `strand` attributes.
* A GenBank flat file is not an original document; it is a human-friendly projection
  of the NCBI ASN.1 object tree.
* Next Unit: The GenBank Sequence Database — Primary vs Secondary databases,
  line-by-line flat file anatomy, and format conversion.
```

---

## Detailed Comprehensive Technical Notes

### 1. The Conceptual Dichotomy: Describing vs Annotating

A frequent failure in naive computational biology is the conflation of global metadata with localized biological features. In the NCBI Data Model, this boundary is mathematically enforced:

$$\text{Biological Sequence Record} = \text{Identity (Seq-id)} + \text{Physical Polymer (Seq-inst)} + \text{Descriptors (Seq-descr)} + \text{Features (Seq-annot)}$$

```
  Conceptual Layer    ASN.1 Entity      Coordinate Dependent?  Biological Examples
  -------------------------------------------------------------------------------------------------
  Describing          Seq-descr         NO (Global to Bioseq)  Organism taxonomy, tissue type, 
                                                               publication citations, clone library
  Annotating          Seq-annot /       YES (Anchored via      Promoters, TATA boxes, exons, CDS,
                      Seq-feat          Seq-loc intervals)     cleavage sites, missense mutations
```

If an author writes that a sequence was isolated from "human peripheral blood reticulocytes", this statement applies to the entire DNA/RNA molecule. It is modeled as a **`Seq-descr`** (specifically a `BioSource` descriptor). 

Conversely, if an author identifies that bases 51 through 494 encode the beta-globin polypeptide, this statement is strictly bound to a 1D spatial interval. It is modeled as a **`Seq-feat`** anchored by a **`Seq-loc`**.

---

### 2. Deep Dive: `Seq-descr` (Sequence Descriptors)

A `Seq-descr` is defined as a `SET OF Seqdesc`. A single descriptor can contain multiple distinct metadata blocks:

1. **`source` (`BioSource`):**  
   Contains the biological origin of the sample. Sub-fields include:
   - `org`: Taxonomic definition (`taxname "Homo sapiens"`, `taxid 9606`, common name `"human"`, and full phylogenetic lineage string).
   - `subtype`: Organismal modifiers (e.g., `tissue-type "liver"`, `cell-line "HeLa"`, `isolate "Hu-1"`).
   - `genome`: Genomic provenance (`genomic`, `chloroplast`, `mitochondrion`, `plasmid`).
2. **`molinfo` (`MolInfo`):**  
   Encodes the biochemical class and processing state:
   - `biomol`: `genomic`, `pre-RNA`, `mRNA`, `rRNA`, `tRNA`, `peptide`.
   - `tech`: Experimental sequencing technique (`standard`, `est`, `sts`, `survey`, `wgs`).
   - `completeness`: Flags indicating whether the sequence is complete or partial at the $5'$ or $3'$ termini.
3. **`pub` (`Pubdesc`):**  
   Bibliographic citations attributing the sequence to scientific literature, including MEDLINE/PubMed UIDs, article titles, journal names, and author rosters.
4. **`user` (`User-object`):**  
   Structured key-value dictionaries allowing external organizations (such as RefSeq, Ensembl, or UniProt) to attach custom administrative tracking flags without modifying the core ASN.1 specification.

---

### 3. Deep Dive: `Seq-feat` (Sequence Features)

A sequence feature represents a discrete biological entity localized to a specific segment of the macromolecule. The ASN.1 definition is:

```asn1
Seq-feat ::= SEQUENCE {
    id          Feat-id OPTIONAL,
    data        SeqFeatData,             -- The biological nature of the feature
    partial     BOOLEAN OPTIONAL,        -- Is the feature complete or truncated?
    except      BOOLEAN OPTIONAL,        -- Does this feature violate standard rules?
    comment     VisibleString OPTIONAL,  -- Curator remarks
    product     Seq-loc OPTIONAL,        -- The biological product generated (e.g. Protein)
    location    Seq-loc,                 -- Spatial coordinate interval
    qual        SEQUENCE OF Gb-qual OPTIONAL, -- GenBank-style qualifiers (/gene, /allele)
    title       VisibleString OPTIONAL,
    ext         User-object OPTIONAL     -- Structured extensions
}
```

#### Major Variants of `data` (`SeqFeatData`):
- `gene`: Defines the conceptual gene locus, holding the official gene symbol (e.g., `HBB`), locus tag, and map location (`11p15.4`).
- `cdregion` (CDS): The coding sequence. Specifies the reading frame offset (1, 2, or 3), the genetic code table ID (Table 1: Standard, Table 2: Vertebrate Mitochondrial, Table 11: Bacterial), and non-standard translational exceptions (such as selenocysteine incorporation via UGA).
- `rna`: Encodes transcribed RNAs: mature mRNA, tRNA, rRNA, snRNA, or microRNA.
- `variation`: Encodes genomic variants, single nucleotide polymorphisms (SNPs), and insertions/deletions (indels).
- `prot`: For protein Bioseqs, defines protein names, alternate names, and Enzyme Commission (EC) numbers.
- `site`: Biological binding or catalytic sites (e.g., metal-binding sites, phosphorylation targets, active sites).

---

### 4. `Seq-loc`: The Formal Language of Biological Coordinates

Biological coordinates must capture complex phenomena: circular plasmids, reverse strands, spliced multi-exon transcripts, and fuzzy, uncertain boundaries. NCBI formalizes this via **`Seq-loc`**:

```asn1
Seq-loc ::= CHOICE {
    null        NULL,                    -- Represents a physical sequence gap
    empty       Seq-id,                  -- Whole sequence referenced, coordinates omitted
    whole       Seq-id,                  -- Entire sequence
    int         Seq-interval,            -- A continuous interval [from, to]
    equiv       Packed-seqint,           -- Multiple synonymous intervals
    point       Seq-point,               -- A single discrete point
    mix         Seq-loc-mix,             -- Ordered sequence of distinct locations
    packed-pnt  Packed-seqpnt            -- Packed array of individual points
}
```

#### Understanding Coordinate Offsets (0-Based vs 1-Based):
- **Internal ASN.1 Representation:** The NCBI data model computes coordinates using **0-based, half-open indexing** (or 0-based inclusive internally: `from 50, to 493` represents the 444 nucleotides spanning 51 to 494).
- **External Flat File Display:** The GenBank flat file renders coordinates in **1-based inclusive indexing** (`51..494`), which is standard for molecular biologists.

#### Representing Spliced Exons via `mix`:
When a eukaryotic genomic DNA record contains an mRNA transcript assembled from multiple exons separated by introns, `Seq-loc` uses the `mix` choice. In the GenBank flat file, this is rendered using the `join()` operator:

$$\text{GenBank Flat File: } \texttt{CDS join(51..142, 273..495)}$$
$$\text{ASN.1 Engine: } \texttt{Seq-loc.mix = [ Seq-interval(50..141), Seq-interval(272..494) ]}$$

#### Reverse Strand Orientation:
When a gene is encoded on the negative (reverse-complement) strand, the `strand` enumeration inside `Seq-interval` is set to `minus`. The flat file renders this as `complement(join(...))`.

---

## Worked Example: ASN.1 Specification of the *HBB* CDS Feature

Below is the complete, syntactically authentic ASN.1 object representing the Coding Sequence feature of human *HBB* (`NM_000518.5`):

```asn1
Seq-feat ::= {
  data cdregion {
    frame 1,
    code {
      id 1                           -- Standard Genetic Code
    }
  },
  partial FALSE,
  product whole other {
    accession "NP_000509",           -- Links directly to the translated protein!
    version 1
  },
  location int {
    from 50,                         -- 0-based index corresponds to base 51
    to 493,                          -- 0-based index corresponds to base 494
    strand plus,
    id other {
      accession "NM_000518",
      version 5
    }
  },
  qual {
    {
      qual "gene",
      val "HBB"
    },
    {
      qual "product",
      val "hemoglobin subunit beta"
    },
    {
      qual "protein_id",
      val "NP_000509.1"
    },
    {
      qual "db_xref",
      val "CCDS:CCDS7753.1"
    },
    {
      qual "db_xref",
      val "GeneID:3043"
    }
  }
}
```

### Deconstructing the Object:
1. `data cdregion`: Declares this feature as a protein-coding region with reading frame 1 and genetic code 1.
2. `product`: Contains an explicit hard link to the protein `Bioseq` (`NP_000509.1`). This is how Entrez knows which protein belongs to which nucleotide sequence.
3. `location int`: Binds the feature to bases 50 through 493 on the `plus` strand of `NM_000518.5`.
4. `qual`: Contains the auxiliary key-value tags that are rendered beneath the `CDS` line in the GenBank flat file.

---

## Formative In-Class Checks

### Question 1
**Prompt:** A bioinformatics researcher observes that an author's name on a published GenBank record was misspelled. A curator updates the author's name in the `pub` citation block. Does this update cause the sequence version to change from `.1` to `.2`? Explain why based on the NCBI Data Model.

**Model Answer:**
**No, the sequence version will NOT increment.**
In the NCBI Data Model:
- Bibliographic citations are stored in **`Seq-descr`** (specifically within a `Pubdesc` descriptor). 
- The accession version suffix (`.1` $\to$ `.2`) is strictly bound to changes in the physical sequence instance (**`Seq-inst`**) or modifications to the underlying sequence coordinates and length. 
- Updating metadata or fixing typos in descriptors modifies the database timestamp and update date in the record header, but preserves the accession version unchanged, because the physical macromolecular sequence itself did not change by a single base.

---

### Question 2
**Prompt:** In a eukaryotic genomic DNA record, a gene contains three exons located at coordinates 1000..1200, 2500..2800, and 4000..4250. How is this discontinuous coding region modeled in the NCBI Data Model, and what exact location string will appear in the resulting GenBank flat file?

**Model Answer:**
- **In the NCBI Data Model:** This discontinuous location is modeled as a **`Seq-loc`** of type **`mix`** (`Seq-loc-mix`). The `mix` object contains an ordered list of three distinct **`Seq-interval`** objects, each specifying the start and end coordinates (in 0-based notation: 999..1199, 2499..2799, and 3999..4249) and the strand orientation (`plus`).
- **In the GenBank Flat File:** The location parser converts the `mix` structure into a 1-based `join()` string:  
  `CDS    join(1000..1200,2500..2800,4000..4250)`

---

### Question 3
**Prompt:** What is the operational purpose of the `product` field inside a `cdregion` `Seq-feat`? What error would occur in an automated bioinformatics retrieval pipeline if this field were omitted?

**Model Answer:**
- **Operational Purpose:** The `product` field contains an explicit `Seq-id` reference that formally binds the nucleotide coding interval to its translated polypeptide `Bioseq` object (e.g., linking the `CDS` interval in `NM_000518.5` directly to `NP_000509.1`).
- **What error would occur:** If the `product` field were omitted, the relational bridge between the nucleic acid and the protein would be broken. Automated retrieval pipelines (such as Entrez or BLAST) would be unable to traverse the link from mRNA to translated protein without attempting a naive, unverified conceptual translation on the fly, failing to identify post-translational cleavage, non-standard codon re-assignments, or official protein accession numbers.
