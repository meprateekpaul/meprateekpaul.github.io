# Quiz 1: Units 1–3 — Fundamentals, Information Retrieval & The NCBI Data Model

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Units Covered:** Unit 1 (Bioinformatics & Internet), Unit 2 (Information Retrieval / Entrez), Unit 3 (The NCBI Data Model)  
**Time Allowed:** 15 Minutes  
**Maximum Marks:** 10 Marks  
**Nature of Examination:** Closed Book, Individual Assessment  

---

## Part I: Student Test Paper

### Instructions to Candidates
1. Answer all questions in the space provided.
2. Ensure queries and syntax conform strictly to NCBI Entrez conventions (capitalized Booleans, valid brackets).
3. Manage your time carefully (approx. 1.5 minutes per mark).

---

### Question 1: Multiple Choice / Direct Concept Checks (4 Marks)

**(a)** Which protocol and port combination is universally employed to establish an encrypted, TLS-authenticated connection to retrieve PubMed records via a web browser? `[1 Mark]`  
[  ] A) FTP on Port 21  
[  ] B) HTTP on Port 80  
[  ] C) HTTPS on Port 443  
[  ] D) SMTP on Port 25  

**(b)** Which organization is the European node of the International Nucleotide Sequence Database Collaboration (INSDC)? `[1 Mark]`  
[  ] A) NCBI  
[  ] B) DDBJ  
[  ] C) EMBL-EBI (ENA)  
[  ] D) SIB (Swiss Institute of Bioinformatics)  

**(c)** Which NCBI RefSeq accession prefix designates an experimentally verified, curated human messenger RNA (mRNA) transcript? `[1 Mark]`  
[  ] A) `NP_`  
[  ] B) `NM_`  
[  ] C) `NC_`  
[  ] D) `XM_`  

**(d)** In the NCBI abstract data model, what is the fundamental atomic data object that stores an individual biological sequence and its sequence coordinates? `[1 Mark]`  
[  ] A) `Bioseq-set`  
[  ] B) `Seq-annot`  
[  ] C) `Bioseq`  
[  ] D) `Seq-descr`  

---

### Question 2: Targeted Entrez Query Formulation (3 Marks)

You need to formulate a targeted search in the NCBI Nucleotide database to retrieve **only** the curated RefSeq messenger RNA (mRNA) sequence for the human beta-globin gene (*HBB*), while strictly avoiding genomic DNA contigs and homologues from other species.

Write the exact, single-line Entrez query string utilizing appropriate field tags (`[GENE]`, `[ORGN]`, `[PROP]`) and Boolean operators:

**Your Query:**  
`________________________________________________________________________________________________________________________`

---

### Question 3: NCBI Data Model Mapping (3 Marks)

Examine the following simplified GenBank flat-file snippet:

```text
LOCUS       NM_000518               628 bp    mRNA    linear   PRI 01-FEB-2024
DEFINITION  Homo sapiens hemoglobin subunit beta (HBB), mRNA.
SOURCE      Homo sapiens (human)
FEATURES             Location/Qualifiers
     CDS             51..494
                     /gene="HBB"
                     /protein_id="NP_000509.1"
```

Map each element from the left column to its corresponding abstract data object in the NCBI Data Model from the right column (write the letter A, B, C, or D next to each number):

1. The text string `"Homo sapiens hemoglobin subunit beta (HBB), mRNA."`  [ _____ ]  
2. The coordinate span `51..494` defining the coding sequence interval  [ _____ ]  
3. The overall container packaging the 628 bp RNA molecule and its properties  [ _____ ]  

* **Options:**  
  * **A:** `Bioseq`  
  * **B:** `Seq-descr` (Sequence Descriptor)  
  * **C:** `Seq-loc` (Sequence Location)  
  * **D:** `Bioseq-set`  

---
---

## Part II: Instructor Answer Key & Marking Scheme

### Question 1: Multiple Choice Answers (4 Marks)
* **(a)** **C) HTTPS on Port 443** `[1 Mark]`  
  *Rationale:* HTTPS uses Transport Layer Security (TLS) encryption over port 443. Port 21 is FTP, 80 is unencrypted HTTP, and 25 is SMTP.
* **(b)** **C) EMBL-EBI (ENA)** `[1 Mark]`  
  *Rationale:* The tripartite INSDC consists of NCBI GenBank (USA), ENA at EMBL-EBI (Europe), and DDBJ (Japan). SIB maintains Swiss-Prot/Expasy.
* **(c)** **B) `NM_`** `[1 Mark]`  
  *Rationale:* `NM_` = curated mRNA; `NP_` = curated protein; `NC_` = genomic chromosome; `XM_` = automated model mRNA prediction.
* **(d)** **C) `Bioseq`** `[1 Mark]`  
  *Rationale:* `Bioseq` is the atomic unit storing a single sequence. `Bioseq-set` is a collection, `Seq-annot` holds annotations, and `Seq-descr` provides metadata.

---

### Question 2: Targeted Entrez Query Formulation (3 Marks)

* **Model Answer:**  
  `HBB[GENE] AND "Homo sapiens"[ORGN] AND biomol_mrna[PROP] AND srcdb_refseq[PROP]`  
  *(Acceptable alternative: `(HBB[GENE] AND human[ORGN]) AND RefSeq[Filter] AND biomol_mrna[PROP]`)*

* **Marking Scheme Breakdown:**  
  * **1.0 Mark:** Correct restriction of gene symbol `HBB[GENE]` and organism `"Homo sapiens"[ORGN]` (or `human[ORGN]`).  
  * **1.0 Mark:** Correct restriction to mature mRNA via `biomol_mrna[PROP]` (or `mrna[Filter]`).  
  * **1.0 Mark:** Correct filtering to curated RefSeq standard via `srcdb_refseq[PROP]` (or `RefSeq[Filter]`). Deduct 0.5 marks if Boolean `AND` is written in lowercase `and`.

---

### Question 3: NCBI Data Model Mapping (3 Marks)

* **Model Answer & Mappings:**  
  1. The text string `"Homo sapiens hemoglobin subunit beta (HBB), mRNA."` $\rightarrow$ **B (`Seq-descr`)** `[1 Mark]`  
     *(Represents a global title/definition descriptor for the sequence).*
  2. The coordinate span `51..494` defining the coding sequence interval $\rightarrow$ **C (`Seq-loc`)** `[1 Mark]`  
     *(Represents the sequence location interval attribute `int` of a `Seq-feat` feature).*
  3. The overall container packaging the 628 bp RNA molecule and its properties $\rightarrow$ **A (`Bioseq`)** `[1 Mark]`  
     *(Represents the core atomic sequence object containing `id`, `descr`, `inst`, and `annot`).*

* **Marking Scheme Breakdown:**  
  * Exactly 1.0 Mark per correct letter match. No partial credit within an individual sub-item.
