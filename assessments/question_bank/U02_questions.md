# Question Bank: Unit 2 — Information Retrieval from Biological Databases

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Syllabus Topic:** Integrated information Retrieval (Entrez System), Retrieving database entries  
**Primary Learning Outcomes:** LO1, LO2 (Formulate precise Entrez queries, understand identifiers and reciprocal database links)  

---

## Section A: Multiple Choice Questions (15 MCQs)

### Q01
In the NCBI Entrez search syntax, which field tag restricts the search term specifically to the scientific or common name of the organism?  
a) `[GENE]`  
b) `[ORGN]`  
c) `[TITL]`  
d) `[PROP]`  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** b) `[ORGN]`  
* **Rationale:** The `[ORGN]` tag (Organism) confines search evaluation to the NCBI Taxonomy index field. `[GENE]` searches gene symbols, `[TITL]` searches words in the record title/definition, and `[PROP]` filters by record properties.

### Q02
What is the standard RefSeq accession prefix format for a curated, peer-reviewed human messenger RNA (mRNA) transcript?  
a) `NP_`  
b) `NC_`  
c) `NM_`  
d) `XM_`  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** c) `NM_`  
* **Rationale:** In NCBI RefSeq nomenclature, `NM_` denotes curated mRNA transcripts, `NP_` denotes curated protein products, `NC_` represents complete genomic chromosomes, and `XM_` indicates model/predicted mRNA transcripts derived from computational genome annotation pipelines.

### Q03
Which of the following Boolean queries will retrieve records containing *either* the term `haemoglobin` or `hemoglobin`, but *strictly limited* to human entries?  
a) `haemoglobin OR hemoglobin AND human[ORGN]`  
b) `(haemoglobin OR hemoglobin) AND human[ORGN]`  
c) `haemoglobin AND hemoglobin OR human[ORGN]`  
d) `haemoglobin NOT hemoglobin AND human[ORGN]`  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** b) `(haemoglobin OR hemoglobin) AND human[ORGN]`  
* **Rationale:** Boolean operators at NCBI are evaluated strictly from left to right unless parentheses are used to enforce precedence. Parentheses ensure the union (`OR`) of spelling variants is resolved first before performing the intersection (`AND`) with the human organism constraint.

### Q04
Why has NCBI formally retired the GI (GenInfo Identifier) number in favour of the `Accession.Version` tracking system?  
a) GI numbers became too computationally intensive to store in 64-bit integers  
b) A single accession string with a dot-version (e.g., `NM_000518.5`) provides an intuitive, globally stable identifier that explicitly tracks sequence revisions  
c) GI numbers could only be assigned to bacterial sequences  
d) The European Bioinformatics Institute legally forbade the use of integer IDs  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) A single accession string with a dot-version (e.g., `NM_000518.5`) provides an intuitive, globally stable identifier that explicitly tracks sequence revisions  
* **Rationale:** The GI system assigned an entirely new arbitrary integer whenever a sequence was edited by a single base, breaking traceability. The `Accession.Version` system maintains the permanent accession base while incrementing the version suffix (`.1`, `.2`, etc.) to denote sequence modifications.

### Q05
In Entrez, what mechanism allows a user viewing a record in NCBI Gene to jump directly to its corresponding PubMed references, Protein products, or 3D Structures with a single click?  
a) Dynamic programming matrix traceback  
b) Entrez reciprocal links (Links / LinkOut)  
c) BLAST seed extension  
d) Domain Name System resolution  
* **Learning Outcome:** LO1  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Entrez reciprocal links (Links / LinkOut)  
* **Rationale:** Entrez maintains pre-computed relational link tables between cross-indexed databases (e.g., Gene $\leftrightarrow$ Nucleotide $\leftrightarrow$ Protein $\leftrightarrow$ PubMed $\leftrightarrow$ Structure). LinkOut connects NCBI records to external institutional publishers and specialized biological databases.

### Q06
What does the Medical Subject Headings (MeSH) vocabulary provide in PubMed that a simple free-text keyword search cannot?  
a) Automatic translation of PubMed articles into six languages  
b) A controlled, hierarchical indexing thesaurus that captures conceptual synonyms and subheadings regardless of author-specific phrasing  
c) Free open-access PDF downloads for all indexed commercial articles  
d) Direct calculation of the protein crystallization temperature  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) A controlled, hierarchical indexing thesaurus that captures conceptual synonyms and subheadings regardless of author-specific phrasing  
* **Rationale:** MeSH is a curated hierarchical thesaurus. Searching with a MeSH term automatically captures synonymous terminology, related clinical subheadings, and descendant terms in the hierarchy (explosion), overcoming the limitations of idiosyncratic author keywords.

### Q07
A student executes an Entrez query and receives query keys `#1` and `#2` in their Search History. How can they find records present in `#1` that are completely absent from `#2`?  
a) `#1 OR #2`  
b) `#1 AND #2`  
c) `#1 NOT #2`  
d) `#2 NOT #1`  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** c) `#1 NOT #2`  
* **Rationale:** The `NOT` operator executes a set difference operation. Querying `#1 NOT #2` subtracts all records present in query result `#2` from the result set of `#1`.

### Q08
Which NCBI RefSeq accession prefix indicates an uncurated, computationally predicted protein sequence derived from an automated eukaryotic genome annotation pipeline?  
a) `NP_`  
b) `YP_`  
c) `XP_`  
d) `AP_`  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** c) `XP_`  
* **Rationale:** RefSeq accessions starting with 'X' (`XM_`, `XP_`, `XR_`) represent model predictions generated by NCBI's automated Eukaryotic Genome Annotation Pipeline (GNOMON). Curated protein accessions begin with `NP_` or `YP_` (mitochondrial/viral).

### Q09
What is the function of the Entrez field tag `[PROP]`?  
a) Restricts searches to proprietary commercial patents  
b) Filters entries by database record properties such as molecule type, gene location, or curation status (e.g., `biomol_mrna[PROP]`)  
c) Identifies the molecular weight and proportion of basic amino acids  
d) Validates the mathematical properties of a scoring matrix  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Filters entries by database record properties such as molecule type, gene location, or curation status (e.g., `biomol_mrna[PROP]`)  
* **Rationale:** The `[PROP]` (Property) tag filters records based on metadata classifications indexed by NCBI, such as `biomol_mrna`, `srcdb_refseq`, `gene_in_chromosome`, or `complete`.

### Q10
Why does searching for "HBB" in NCBI Gene yield roughly one entry for *Homo sapiens*, whereas searching for "HBB" in NCBI Nucleotide yields thousands of results?  
a) Because the Gene database is broken and has deleted historical records  
b) Because NCBI Gene is a non-redundant gene-centric catalog (one entry per locus), while Nucleotide indexes all submitted mRNAs, ESTs, genomic contigs, and clinical clones  
c) Because human haemoglobin has thousands of distinct chromosomes  
d) Because the Nucleotide database automatically mutates the query string  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Analyze  
* **Correct Answer:** b) Because NCBI Gene is a non-redundant gene-centric catalog (one entry per locus), while Nucleotide indexes all submitted mRNAs, ESTs, genomic contigs, and clinical clones  
* **Rationale:** NCBI Gene organizes data locus-by-locus, providing a single consolidated record for human gene ID 3043 (*HBB*). Nucleotide is a sequence-centric repository containing every individual experimental cDNA, clone, sequencing read, and transcript isoform ever deposited.

### Q11
Which Entrez field tag would you append to restrict an author search specifically to publications where "Baxevanis AD" is an author?  
a) `Baxevanis AD[TITL]`  
b) `Baxevanis AD[AUTH]`  
c) `Baxevanis AD[JOUR]`  
d) `Baxevanis AD[AFFL]`  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** b) `Baxevanis AD[AUTH]`  
* **Rationale:** The `[AUTH]` (Author) tag restricts term matching to author name fields in PubMed and primary sequence records. `[TITL]` searches article titles, `[JOUR]` searches journal names, and `[AFFL]` searches author institutional affiliations.

### Q12
In Entrez query syntax, what happens if Boolean operators such as `and`, `or`, and `not` are typed in lowercase letters?  
a) The Entrez parser will crash and return an HTTP 500 error  
b) Entrez treats them as literal free-text search words rather than Boolean set operators  
c) Entrez automatically converts them to uppercase and executes the Boolean operation  
d) Entrez executes a fuzzy local alignment of the keywords  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Remember/Understand  
* **Correct Answer:** b) Entrez treats them as literal free-text search words rather than Boolean set operators  
* **Rationale:** Entrez requires Boolean operators (`AND`, `OR`, `NOT`) to be capitalized. When entered in lowercase (`and`, `or`, `not`), the search engine treats them as ordinary query text tokens, leading to unintended and noisy search results.

### Q13
Which Entrez tool or service enables automated, script-based batch retrieval of sequence records using command-line scripts or programming languages like Python and R?  
a) Entrez Direct (EDirect) / Entrez Programming Utilities (E-utilities)  
b) NCBI BLAST web form  
c) Gene Expression Omnibus (GEO) interactive viewer  
d) PubMed MeSH Browser  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Remember  
* **Correct Answer:** a) Entrez Direct (EDirect) / Entrez Programming Utilities (E-utilities)  
* **Rationale:** E-utilities (and the EDirect command-line suite) provide seven server-side programs (`esearch`, `efetch`, `epost`, `elink`, `esummary`, `einfo`, `egquery`) designed for automated, scriptable data retrieval over standard HTTP protocols.

### Q14
A researcher wishes to retrieve human *TP53* records published exclusively between January 1, 2020, and December 31, 2022. Which field tag format is correct?  
a) `2020:2022[VOL]`  
b) `2020/01/01:2022/12/31[PDAT]`  
c) `01-01-2020 TO 31-12-2022[DATE]`  
d) `[YEAR] 2020-2022`  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Apply  
* **Correct Answer:** b) `2020/01/01:2022/12/31[PDAT]`  
* **Rationale:** Date ranges in Entrez are specified using the `YYYY/MM/DD:YYYY/MM/DD` syntax followed by the Publication Date tag `[PDAT]`. Colon (`:`) defines an inclusive range.

### Q15
What does the Entrez indexing engine construct behind the scenes to make text retrieval across billions of records virtually instantaneous?  
a) A single unindexed text file searched sequentially using `grep`  
b) Inverted indexes (term lists mapping individual tokens to posting lists of Unique Identifiers / UIDs)  
c) High-dimensional neural embeddings of every flat file  
d) A dynamic programming matrix for each query word  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Understand  
* **Correct Answer:** b) Inverted indexes (term lists mapping individual tokens to posting lists of Unique Identifiers / UIDs)  
* **Rationale:** Entrez builds inverted indexes: dictionaries of standardized terms (tokens) extracted from specific fields, each pointing to an ordered list of record UIDs (posting list). Boolean operations are executed as ultra-fast set unions and intersections of these UID lists.

---

## Section B: Short Answer Questions (6 SAQs)

### SAQ 01: Formulation of a Targeted Entrez Query (4 Marks)
**Question:** Write an exact NCBI Entrez search query to retrieve only curated, reviewed mRNA transcripts for the human insulin gene (*INS*). Explain the specific function of every field tag and filter used in your query.  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Apply  

**Model Answer:**  
* **Target Query:**  
  `INS[GENE] AND "Homo sapiens"[ORGN] AND biomol_mrna[PROP] AND srcdb_refseq[PROP]`  
  *(Alternative valid query: `(INS[GENE] AND human[ORGN]) AND RefSeq[Filter] AND biomol_mrna[PROP]`)*
* **Explanation of Components:**
  1. `INS[GENE]`: Limits search to the official gene symbol *INS*, excluding papers or records where "insulin" appears only in the title or text abstract.
  2. `"Homo sapiens"[ORGN]`: Restricts the taxonomic scope strictly to human, preventing retrieval of porcine, bovine, or rodent homologues.
  3. `biomol_mrna[PROP]`: Filters the molecule type to mature messenger RNA, eliminating genomic DNA contigs and unprocessed pre-mRNAs.
  4. `srcdb_refseq[PROP]`: Restricts the database source to NCBI RefSeq, eliminating thousands of redundant, uncurated primary GenBank clones and ESTs.

**Marking Scheme:**  
* 2 Marks: Flawless query syntax including correct brackets, capitalization of `AND`, and quotes where needed.  
* 2 Marks: 0.5 marks for accurate justification of each of the four components (`[GENE]`, `[ORGN]`, `biomol_mrna`, `srcdb_refseq`).

---

### SAQ 02: Deconstructing RefSeq Accession Prefixes (4 Marks)
**Question:** Explain the structural meaning of NCBI Reference Sequence (RefSeq) accession numbers. Describe what each of the following prefixes designates: `NM_`, `NP_`, `NC_`, and `XM_`.  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
NCBI RefSeq accessions provide a curated, non-redundant sequence standard. Unlike primary GenBank accessions (which have arbitrary letter prefixes), RefSeq accessions always feature a two-letter prefix, followed by an underscore (`_`), and a six- to nine-digit integer, terminated by a dot-version suffix:
1. `NM_` (e.g., `NM_000518.5`): Curated, experimentally verified mature messenger RNA (mRNA) transcript.
2. `NP_` (e.g., `NP_000509.1`): Curated, experimentally supported protein product translated from an `NM_` transcript.
3. `NC_` (e.g., `NC_000011.10`): Complete, curated genomic sequence representing a full chromosome or organelle genome.
4. `XM_` (e.g., `XM_011540123.1`): Model mRNA transcript predicted entirely by automated computational genome annotation algorithms (uncorrobated by full-length cDNA).

**Marking Scheme:**  
* 1 Mark: Clear explanation of RefSeq format architecture (two letters, underscore, digits, version).  
* 3 Marks: 0.75 marks for each correctly identified prefix (`NM_`, `NP_`, `NC_`, `XM_`).

---

### SAQ 03: Entrez History and Query Translation (3 Marks)
**Question:** Describe the role of the Entrez "Search History" feature and explain how query translation operates when a user searches a broad term like "sickle cell anemia".  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Entrez History:** Tracks all sequential queries executed during a session, storing results on the NCBI server under numbered query keys (`#1`, `#2`, etc.). It allows users to combine complex search sets using Boolean logic (e.g., `#1 AND #3 NOT #2`) without re-running previous computational queries.
* **Query Translation:** When an un-tagged term like "sickle cell anemia" is entered, the Entrez translation engine checks internal translation tables:
  1. It maps the phrase to official Medical Subject Headings (MeSH): `"anemia, sickle cell"[MeSH Terms]`.
  2. It generates text word variations across titles and abstracts: `("sickle"[All Fields] AND "cell"[All Fields] AND "anemia"[All Fields])`.
  3. It unites them: `("anemia, sickle cell"[MeSH Terms] OR ("sickle"[All Fields] AND "cell"[All Fields] AND "anemia"[All Fields]))`.

**Marking Scheme:**  
* 1.5 Marks: Clear explanation of Search History session caching and query key referencing (`#n`).  
* 1.5 Marks: Detailed explanation of automatic query translation mapping text to MeSH terms and Boolean term expansion.

---

### SAQ 04: MeSH Hierarchy and Explosion (3 Marks)
**Question:** What are MeSH (Medical Subject Headings)? Explain the concept of "MeSH explosion" and state how it enhances literature retrieval in PubMed.  
* **Learning Outcome:** LO2  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Definition:** MeSH is a controlled, hierarchically organized biomedical vocabulary curated by the US National Library of Medicine (NLM) used to index PubMed articles. Articles are assigned 10–15 MeSH descriptors by expert indexers reflecting primary conceptual content.
* **MeSH Explosion:** In the MeSH tree, terms are arranged from broad categories to narrow specific concepts. "Explosion" means that when a user searches a higher-level MeSH descriptor (e.g., *Hemic and Lymphatic Diseases*), PubMed automatically retrieves all citations indexed with that term PLUS all citations indexed under its narrower descendant terms (e.g., *Anemia*, *Sickle Cell Anemia*, *Thalassemia*).
* **Benefit:** It prevents missing relevant papers whose authors used specific clinical subtypes rather than broad disease category names.

**Marking Scheme:**  
* 1 Mark: Accurate definition of MeSH as a controlled hierarchical indexing thesaurus.  
* 1 Mark: Precise explanation of "explosion" (retrieving broader term + all descendant branch terms).  
* 1 Mark: Statement of clinical/search benefit (high recall without manual synonym compilation).

---

### SAQ 05: Inverted Index Architecture in Entrez (4 Marks)
**Question:** Explain how an inverted index functions in biological text retrieval systems. Why is searching an inverted index thousands of times faster than searching flat files sequentially?  
* **Learning Outcome:** LO1  
* **Bloom's Taxonomy Level:** Understand / Analyze  

**Model Answer:**  
* **Structure of an Inverted Index:**  
  An inverted index consists of two primary components:
  1. **Vocabulary / Dictionary:** A sorted, standardized list of all unique words (tokens) occurring across all records in the database.
  2. **Posting Lists:** Associated with each word is an ordered array of record identifiers (UIDs) in which that word appears, often with field and positional metadata.
* **Search Execution:**  
  When an Entrez query such as `HBB[GENE] AND human[ORGN]` is evaluated:
  - The engine performs a binary search on the dictionary for `HBB` (under the Gene field) to grab its posting list: `{UID: 3043, 11025, ...}`.
  - It retrieves the posting list for `human` (under Organism).
  - It intersects the two sorted integer arrays in linear time $O(L_1 + L_2)$.
* **Performance Superiority:** Sequential flat-file scanning (`grep`) requires reading gigabytes or terabytes of text from disk ($O(N)$ text scanning). An inverted index bypasses the full text entirely, performing instant in-memory pointer/integer comparisons.

**Marking Scheme:**  
* 1.5 Marks: Detailed structural definition of dictionary/tokens and posting lists of UIDs.  
* 1.5 Marks: Clear explanation of how Boolean AND/OR is executed as fast set intersections/unions of UID lists.  
* 1 Mark: Direct contrast showing why sequential disk search is $O(N)$ while indexed search is $O(\log V + K)$.

---

### SAQ 06: Links and LinkOut in Entrez (3 Marks)
**Question:** Distinguish between Entrez "Links" (internal database neighbours) and "LinkOut" (external provider links). Provide one biological use-case for each.  
* **Learning Outcome:** LO1  
* **Bloom's Taxonomy Level:** Understand  

**Model Answer:**  
* **Entrez Links (Internal):** Pre-calculated relational cross-references connecting records within the NCBI Entrez ecosystem.  
  * *Biological Use-Case:* While inspecting the human *HBB* record in NCBI Gene, clicking the "Protein" link immediately displays all hemoglobin beta polypeptide isoforms (`NP_000509.1`), and clicking "Structure" opens the crystal structure (e.g., PDB 1A3N) in MMDB.
* **LinkOut (External):** Direct hyperlinks from an NCBI record to external third-party institutional repositories, publisher websites, or specialized biological databases.  
  * *Biological Use-Case:* Clicking a LinkOut link on a PubMed article navigates directly to the publisher's site (e.g., Nature or Oxford University Press) to access the full-text PDF, or linking from an NCBI Gene page to the HGNC (HUGO Gene Nomenclature Committee) or OMIM database for clinical phenotyping.

**Marking Scheme:**  
* 1.5 Marks: Clear differentiation between internal NCBI inter-database links vs external third-party LinkOut.  
* 1.5 Marks: Concrete biological example for internal Links (0.75 marks) and LinkOut (0.75 marks).

---

## Section C: Long Answer / Problem Questions (2 LAQs)

### LAQ 01: Entrez Database Architecture, Query Optimization, and Execution Mechanics (10 Marks)
**Question:**  
You are tasked with building a reliable computational pipeline to monitor all newly published clinical research papers investigating drug resistance mutations in *Mycobacterium tuberculosis*.

a) Formulate an advanced Entrez PubMed query that captures articles discussing drug resistance (rifampicin or isoniazid) in *Mycobacterium tuberculosis*, published in indexed MEDLINE journals between 2021 and 2023, while strictly excluding animal model studies (mice or rats). (3 Marks)  
b) Diagram and explain the internal step-by-step query parsing, Boolean set operations, and posting list manipulations executed by the Entrez search engine for your query. (4 Marks)  
c) Describe how you would implement this query in Python using `Bio.Entrez` (`esearch` and `efetch`), explaining how `WebEnv` and `query_key` parameters manage stateful batch retrieval without overloading NCBI servers. (3 Marks)  

* **Learning Outcome:** LO1, LO2  
* **Bloom's Taxonomy Level:** Apply / Analyze  

**Model Solution:**  
**a) Advanced PubMed Query Formulation (3 Marks):**  
`("Mycobacterium tuberculosis"[ORGN] OR "Mycobacterium tuberculosis"[MeSH Terms]) AND ("rifampicin" OR "isoniazid" OR "drug resistance"[MeSH Terms]) AND (2021/01/01:2023/12/31[PDAT]) AND medline[SB] NOT ("mice"[MeSH Terms] OR "rats"[MeSH Terms] OR "Mus musculus"[ORGN])`

*Breakdown of criteria:*
- Organism: Targeted to *M. tuberculosis* via `[ORGN]` and `[MeSH Terms]`.
- Drug resistance: Captures specific first-line antibiotics and the broad MeSH resistance descriptor.
- Date range: Restricts publication dates from Jan 1, 2021 to Dec 31, 2023 via `[PDAT]`.
- Journal subset: `medline[SB]` ensures peer-reviewed MEDLINE indexing.
- Exclusion: `NOT` eliminates rodent model studies using MeSH and taxonomy tags.

**b) Query Parsing, Set Logic, and Inverted Index Mechanics (4 Marks):**  
1. **Lexical Analysis and Tokenization:** The Entrez query parser scans the string, recognizes parentheses as nesting delimiters, and isolates field-tagged tokens.
2. **Posting List Lookup:**  
   The engine searches its inverted index B-trees and loads posting lists of PubMed UIDs (PMIDs):
   - $L_{	ext{MTB}} = 	ext{UIDs for } 	ext{M. tuberculosis}$
   - $L_{	ext{Rif}} = 	ext{UIDs for rifampicin}$; $L_{	ext{Iso}} = 	ext{UIDs for isoniazid}$; $L_{	ext{Res}} = 	ext{UIDs for drug resistance}$
   - $L_{	ext{Date}} = 	ext{UIDs for 2021–2023}$; $L_{	ext{Med}} = 	ext{UIDs for MEDLINE subset}$
   - $L_{	ext{Animal}} = 	ext{UIDs for mice/rats}$
3. **Boolean Evaluation (Set Operations):**
   - Union 1 (Drugs): $S_{	ext{Drug}} = L_{	ext{Rif}} \cup L_{	ext{Iso}} \cup L_{	ext{Res}}$
   - Intersection (Target): $S_{	ext{Target}} = L_{	ext{MTB}} \cap S_{	ext{Drug}} \cap L_{	ext{Date}} \cap L_{	ext{Med}}$
   - Difference (Exclusion): $S_{	ext{Final}} = S_{	ext{Target}} \setminus L_{	ext{Animal}}$
4. **Result Assembly:** Because posting lists are maintained in pre-sorted order by PMID, union and intersection operate in $O(N)$ linear time. The final sorted array of PMIDs is saved to the user's Entrez session.

**c) Python `Bio.Entrez` Implementation and Server Etiquette (3 Marks):**  
```python
from Bio import Entrez
import time

Entrez.email = "student@university.edu"
query = ('("Mycobacterium tuberculosis"[ORGN]) AND '
         '("rifampicin" OR "isoniazid") AND '
         '(2021/01/01:2023/12/31[PDAT]) NOT ("mice"[MeSH])')

# Step 1: ESearch with usehistory to store results on NCBI server
handle = Entrez.esearch(db="pubmed", term=query, usehistory="y")
record = Entrez.read(handle)
handle.close()

webenv = record["WebEnv"]
query_key = record["QueryKey"]
count = int(record["Count"])
print(f"Total PMIDs found: {count}")

# Step 2: Batch EFetch using WebEnv and QueryKey in chunks of 500
batch_size = 500
for start in range(0, count, batch_size):
    fetch_handle = Entrez.efetch(db="pubmed", retstart=start, retmax=batch_size,
                                 webenv=webenv, query_key=query_key,
                                 rettype="medline", retmode="text")
    data = fetch_handle.read()
    fetch_handle.close()
    with open("tb_papers.txt", "a") as f:
        f.write(data)
    time.sleep(0.34)  # Adhere to NCBI guideline: max 3 requests/second
```
* **Role of `WebEnv` and `query_key`:** Instead of downloading thousands of PMIDs to the local computer and transmitting them back to NCBI during `efetch`, `usehistory="y"` creates an environment on the NCBI server (`WebEnv`) and an integer pointer (`query_key`). Subsequent fetch calls simply pass these pointers, minimizing internet bandwidth and server memory load.

**Marking Scheme Breakdown:**  
* 3 Marks: Complete, correctly formatted Entrez query satisfying all biological, temporal, and exclusion criteria.  
* 4 Marks: Step-by-step description of tokenizer, B-tree inverted index lookup, posting list unions ($\cup$), intersections ($\cap$), and set difference ($\setminus$).  
* 3 Marks: Functional Python Biopython code snippet (1.5 marks) with accurate technical explanation of `WebEnv`, `query_key`, and rate-limiting etiquette (1.5 marks).

---

### LAQ 02: Biological Identifier Systems: History, Structure, Evolution, and Cross-Referencing (10 Marks)
**Question:**  
Biological databases rely on unique, unambiguous accession and identifier systems to track scientific discoveries over decades.

a) Contrast the historical GenInfo Identifier (GI) system with the modern `Accession.Version` tracking standard. Explain why NCBI phased out GI numbers in 2016. (3 Marks)  
b) Analyze the structural taxonomy of NCBI RefSeq accession prefixes across genomic (`NC_`, `NG_`, `NT_`), transcriptomic (`NM_`, `XM_`, `NR_`), and proteomic (`NP_`, `XP_`, `YP_`) sequences. Create a comprehensive reference table. (4 Marks)  
c) Trace how an experimental discovery—such as the human sickle-cell anaemia mutation (*HBB* Glu6Val)—is cross-referenced across NCBI Gene, Nucleotide, Protein, ClinVar, dbSNP, and OMIM. Explain how Entrez reciprocal links facilitate this multi-omics integration. (3 Marks)  

* **Learning Outcome:** LO1, LO2  
* **Bloom's Taxonomy Level:** Analyze / Synthesize  

**Model Solution:**  
**a) GI Numbers vs Accession.Version and the 2016 Deprecation (3 Marks):**  
* **GenInfo Identifier (GI):** Introduced by NCBI in the 1990s as a simple sequential integer (e.g., `GI: 4504349`) assigned to every sequence deposited. Crucially, GI numbers had no intrinsic structure or human-readable meaning. If a submitter corrected even a single sequencing error, the sequence received a completely new, unrelated GI number, breaking historic links and software indexing.
* **Accession.Version Standard:** Employs an alphanumeric base identifier (e.g., `NM_000518`) that remains permanently tied to that biological locus or cDNA clone. A dot-version integer suffix (`.1`, `.2`, `.5`) is incremented whenever the underlying sequence data is modified. Updates to annotations that leave the sequence unchanged do not alter the version.
* **Why GI Phased Out:** The parallel maintenance of both systems caused massive index bloating. GI integers were nearing 32-bit limits, international consortia (ENA, DDBJ) did not use GIs, and `Accession.Version` provides semantic clarity, version stability, and full backwards compatibility.

**b) Taxonomic Structure of NCBI RefSeq Accession Prefixes (4 Marks):**  

| Category | Prefix | Molecule & Biological Significance | Curation Status |
| :--- | :--- | :--- | :--- |
| **Genomic** | `NC_` | Complete chromosome or organellar genome (e.g., `NC_000011.10`) | Curated reference |
| **Genomic** | `NG_` | Incomplete genomic region; curated genomic gene locus / ref assembly | Curated reference |
| **Genomic** | `NT_` | Genomic contig / scaffold assembly | Automated assembly |
| **RNA** | `NM_` | Protein-coding messenger RNA (mRNA) transcript (e.g., `NM_000518.5`) | Curated / Reviewed |
| **RNA** | `XM_` | Computational model mRNA predicted by GNOMON algorithm | Automated prediction |
| **RNA** | `NR_` | Non-coding RNA (ncRNA, lncRNA, microRNA, rRNA, tRNA) | Curated |
| **Protein** | `NP_` | Protein product derived from curated `NM_` transcript | Curated / Reviewed |
| **Protein** | `XP_` | Model protein translated from automated `XM_` transcript | Automated prediction |
| **Protein** | `YP_` | Organellar (mitochondrial/plastid) or viral protein | Curated |

**c) Multi-Omics Cross-Referencing for *HBB* Glu6Val (3 Marks):**  
A single biomedical entity is represented across specialized Entrez nodes linked via reciprocal foreign keys:
1. **NCBI Gene (Gene ID 3043):** Acts as the central hub, synthesizing chromosomal coordinates (11p15.4), gene structure, official HUGO symbol (*HBB*), and phenotypic summaries.
2. **NCBI Nucleotide (`NM_000518.5`):** Curated mRNA sequence displaying the coding sequence (CDS: 51..494) and the specific codon 6 ($GAG ightarrow GTG$).
3. **NCBI Protein (`NP_000509.1`):** Polypeptide sequence displaying the 147-amino-acid chain with Val replacing Glu at position 7 (or residue 6 of the mature chain following initiator Met cleavage).
4. **dbSNP (`rs334`):** Catalogs the specific genomic variant $A > T$ transversion at GRCh38 coordinate chr11:5227002.
5. **ClinVar (`VCV000013640`):** Evaluates clinical significance: classified as "Pathogenic", causing Sickle Cell Anemia in autosomal recessive inheritance.
6. **OMIM (`*141900` / `#603903`):** Provides detailed clinical genetics literature, inheritance patterns, pathophysiology, and historical medical findings.
* **Role of Entrez Linking:** Entrez maintains relational tables of foreign-key associations. When viewing any one of these records, the sidebar "Related Information" panel allows an investigator to traverse effortlessly between genomic sequence, clinical phenotype, protein structure, and therapeutic literature.

**Marking Scheme Breakdown:**  
* 3 Marks: Rigorous contrast between arbitrary sequential integer GIs and semantic `Accession.Version` tracking; clear justification of 2016 phase-out.  
* 4 Marks: Complete, error-free reference table correctly detailing genomic (`NC_`, `NG_`, `NT_`), transcriptomic (`NM_`, `XM_`, `NR_`), and proteomic (`NP_`, `XP_`, `YP_`) prefixes.  
* 3 Marks: Detailed multi-omics integration tracking *HBB* Glu6Val through Gene, Nucleotide, Protein, dbSNP (`rs334`), ClinVar, and OMIM, explaining foreign-key traversal.
