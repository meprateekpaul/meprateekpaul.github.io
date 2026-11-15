# Lecture 02 — Internet Protocols and Resources

**Course:** CBBI-501: Concepts of Bioinformatics  
**Programme:** B.Tech. Bioinformatics, Semester II  
**Unit 1:** Bioinformatics and Internet  
**Syllabus Topic:** Internet Basics, FTP, www, connecting to Internet, Electronic mail, internet resources  
**Primary Learning Outcome:** LO1 — Describe what kinds of biological data exist, where each is stored, and how the major databases link to one another.

---

## Slide Deck Outline (8 Slides)

```
================================================================================
SLIDE 1: Biological Data Over the Wire
================================================================================
Topic: Moving Petabytes Across Global Networks

[Visual: Network diagram connecting User Workstation -> ISP -> Transatlantic Fiber
         -> NCBI (Bethesda, USA) / EMBL-EBI (Hinxton, UK) / DDBJ (Mishima, Japan)]

Speaker Bullets:
* Modern bioinformatics is intrinsically distributed: no individual laptop can store
  all biological data. We retrieve data across the Internet continuously.
* Understanding the underlying network stack ensures we build robust, scalable,
  and reproducible computational pipelines.
* Today's focus: TCP/IP, URLs, HTTP vs FTP, REST APIs, and the global database hubs.
```

```
================================================================================
SLIDE 2: The Client-Server Architecture in Bioinformatics
================================================================================
Topic: Request-Response Mechanics

  +-----------------------+                    +-------------------------+
  |    Client (Browser    |   HTTP GET Request |      Web/API Server     |
  |     or Python / curl) | -----------------> |    (e.g., NCBI Apache)  |
  |                       | <----------------- |                         |
  | Renders HTML or JSON  |   HTTP 200 OK      +-------------------------+
  +-----------------------+     + Payload                   |
                                                            | SQL / Index Query
                                                            v
                                               +-------------------------+
                                               |    Back-end Database    |
                                               | (GenBank / PubMed / DB) |
                                               +-------------------------+

Speaker Bullets:
* In bioinformatics, the "Client" is rarely just a web browser; it is often a Python
  script, an R session, or a command-line utility (`curl`, `wget`, `efetch`).
* The server processes the request, interfaces with back-end indexing engines,
  and streams the requested payload (FASTA, XML, JSON, or flat file).
```

```
================================================================================
SLIDE 3: Anatomy of a Biological URL
================================================================================
Topic: Deconstructing Web Locators

  https://eutils.ncbi.nlm.nih.gov:443/entrez/eutils/efetch.fcgi?db=nuccore&id=NM_000518.5&rettype=fasta
  \___/   \_____________________/ \__/ \______________________/ \_____________________________________/
    |                |              |              |                               |
 Protocol        Hostname          Port           Path                        Query String

Speaker Bullets:
* Protocol (`https`): Secure HyperText Transfer Protocol (encrypted via TLS).
* Hostname: Fully Qualified Domain Name (FQDN) resolved via DNS to an IP address.
* Port (`443` default for HTTPS; `80` for HTTP).
* Path: Directs the request to the specific CGI/REST endpoint script on the server.
* Query String (`?key=value&...`): Parameters passed to the application.
```

```
================================================================================
SLIDE 4: HTTP/HTTPS vs FTP/SFTP
================================================================================
Topic: Contrasting the Two Pillars of Biological Data Transfer

+-------------------------+-------------------------+-------------------------+
| Feature                 | HTTP / HTTPS            | FTP / SFTP              |
+-------------------------+-------------------------+-------------------------+
| Primary Use Case        | Interactive queries,    | Bulk, multi-gigabyte or |
|                         | web pages, REST APIs    | terabyte downloads      |
| Connection State        | Stateless (per request) | Stateful (session-based)|
| Ports                   | 80 (HTTP) / 443 (HTTPS) | 21 (Control), 20 (Data) |
| Programmatic Interface  | REST, E-utilities, JSON | Scripts, `rsync`, `wget`|
| Overhead                | Headers per request     | Low transport overhead  |
+-------------------------+-------------------------+-------------------------+

Speaker Bullets:
* When you need one record (`NM_000518.5`), use HTTPS via web or REST API.
* When you need all human RefSeq mRNAs (millions of records), HTTPS web queries
  will time out or be rate-limited; use FTP bulk dumps.
```

```
================================================================================
SLIDE 5: Bulk Data Acquisition via FTP
================================================================================
Topic: Navigating NCBI and EBI FTP Directory Hierarchies

[Visual: Directory tree of ftp.ncbi.nlm.nih.gov]
  ftp.ncbi.nlm.nih.gov/
  |-- blast/
  |   `-- db/                    <-- Pre-formatted BLAST databases (nr, nt)
  |-- genomes/
  |   `-- refseq/
  |       `-- vertebrate_mammalian/
  |           `-- Homo_sapiens/  <-- Complete human reference genome builds
  `-- sra/                       <-- Sequence Read Archive raw short reads

Speaker Bullets:
* NCBI FTP (`ftp.ncbi.nlm.nih.gov`) and EBI FTP (`ftp.ebi.ac.uk`) host public data archives.
* Files are compressed with gzip (`.gz`) or tar (`.tar.gz`) to conserve bandwidth.
* Best practice: Use `wget -c` (continue broken downloads) or `rsync` for synchronization.
```

```
================================================================================
SLIDE 6: The INSDC: Global Tripartite Synchronization
================================================================================
Topic: International Nucleotide Sequence Database Collaboration

                    +-------------------------------+
                    |             INSDC             |
                    | (Daily Exchange of New Data)  |
                    +---------------+---------------+
                                    |
          +-------------------------+-------------------------+
          |                         |                         |
          v                         v                         v
+-------------------+     +-------------------+     +-------------------+
|   NCBI: GenBank   |     |    EMBL-EBI: ENA  |     |    DDBJ (Japan)   |
|  (Bethesda, USA)  |     |   (Hinxton, UK)   |     |  (Mishima, Japan) |
+-------------------+     +-------------------+     +-------------------+

Speaker Bullets:
* Established in 1988 to prevent fragmented sequence silos.
* A sequence submitted to DDBJ in Japan is synchronized overnight to NCBI and EBI.
* Shared accession numbering space ensures universal, unique identification.
```

```
================================================================================
SLIDE 7: Major Global Bioinformatics Resource Hubs
================================================================================
Topic: Where to Go for Which Data

1. NCBI (National Center for Biotechnology Information — USA)
   * Entrez, GenBank, RefSeq, PubMed, BLAST, ClinVar, GEO, SRA.
2. EMBL-EBI (European Bioinformatics Institute — UK)
   * Ensembl (genomes), UniProt (with SIB/PIR), ENA, ChEMBL, ArrayExpress.
3. Expasy (Swiss Institute of Bioinformatics — Switzerland)
   * Protein resources: Swiss-Prot curation, ProtParam, Swiss-Model.
4. RCSB PDB / wwPDB (Worldwide Protein Data Bank)
   * Atomic 3D macromolecular structures (X-ray, NMR, Cryo-EM).
5. DDBJ (DNA Data Bank of Japan)
   * Asian hub of INSDC; specialized genomic tools.

Speaker Bullets:
* Notice how functional roles are distributed: GenBank is archival; RefSeq is curated;
  UniProt focuses on proteins; PDB governs 3D structures.
```

```
================================================================================
SLIDE 8: Programmatic Access vs Interactive Browsers
================================================================================
Topic: The Transition to Computational Automation

Interactive Web Browser:
  [Search Box] -> [Click Filter] -> [Download Page]
  * Ideal for exploratory, one-off lookups of single genes (e.g. HBB).
  * Incapable of scaling to 20,000 human genes.

Programmatic Access (CLI / Scripting):
  `esearch -db gene -query "Homo sapiens[ORGN] AND HBB[GENE]" | efetch -format fasta`
  * Fully automatable, reproducible, batch-compatible.
  * Essential skill for modern bioinformatics engineers.
```

---

## Detailed Comprehensive Technical Notes

### 1. Network Architecture for the Bioinformatician

Biological computation is distributed across global networks. When a researcher queries an accession number or initiates a BLAST alignment, their local machine interacts with remote high-performance computing clusters over the Internet protocol suite ($\text{TCP/IP}$).

The process follows a standardized four-layer abstraction model:

```
  Layer                  Protocol Examples          Function in Bioinformatics
  ---------------------------------------------------------------------------------------------------
  4. Application         HTTP, HTTPS, FTP, SSH      Defines biological payloads (FASTA, XML, JSON)
  3. Transport           TCP, UDP                   Ensures reliable, ordered byte delivery (TCP)
  2. Internet (Network)  IP (IPv4, IPv6)            Routes packet fragments across global routers
  1. Link (Physical)     Ethernet, Wi-Fi, Fiber     Physical transmission of electrical/optical signals
```

#### Transmission Control Protocol (TCP) vs User Datagram Protocol (UDP)
Biological data cannot tolerate transmission errors or dropped packets; a single dropped nucleotide frame-shifts an entire coding sequence. Therefore, biological protocols rely exclusively on **TCP**, a connection-oriented transport protocol providing:
1. **Three-Way Handshake:** Connection establishment via `SYN` $\to$ `SYN-ACK` $\to$ `ACK`.
2. **Packet Sequencing and Checksums:** Packets arriving out of order are reassembled based on sequence numbers; corrupted packets fail checksum verification and are automatically retransmitted.
3. **Congestion and Flow Control:** Sliding window algorithms adapt transmission rates to prevent network buffer overflow.

In contrast, **UDP** is connectionless and does not guarantee packet delivery or order, making it suitable for live video streaming, but wholly unsuited for genomic data transfer.

#### Domain Name System (DNS) Resolution
Human researchers query servers using symbolic Fully Qualified Domain Names (e.g., `eutils.ncbi.nlm.nih.gov`). The client machine queries local and hierarchical DNS root servers to translate this symbolic name into a 32-bit (IPv4) or 128-bit (IPv6) numerical IP address (e.g., `130.14.29.110`), allowing packets to be routed across internet switches.

---

### 2. Dissecting the Anatomy of a Biological URL

A **Uniform Resource Locator (URL)** provides a standardized syntax to locate and retrieve biological resources. Consider an NCBI Entrez E-utilities request:

$$\text{\texttt{https://eutils.ncbi.nlm.nih.gov:443/entrez/eutils/efetch.fcgi?db=nuccore\&id=NM\_000518.5\&rettype=fasta\&retmode=text}}$$

Deconstruction of components:
1. **Scheme / Protocol (`https`):**  
   Hypertext Transfer Protocol Secure. Indicates that communication is encrypted via Transport Layer Security (TLS), preventing packet interception or man-in-the-middle tampering.
2. **Host / Domain Name (`eutils.ncbi.nlm.nih.gov`):**  
   The target server cluster hosting the NCBI web API.
3. **Port Number (`:443`):**  
   The logical communication endpoint. Port `443` is standard for HTTPS; port `80` is standard for unencrypted HTTP.
4. **Path (`/entrez/eutils/efetch.fcgi`):**  
   The hierarchical file path on the server pointing to the executable server-side script (`efetch.fcgi` compiled C++ Common Gateway Interface binary).
5. **Query String (`?db=nuccore&id=NM_000518.5&rettype=fasta&retmode=text`):**  
   Begins with a question mark (`?`) and separates key-value parameter pairs with ampersands (`&`):
   - `db=nuccore`: Instructs the server to query the Nucleotide database.
   - `id=NM_000518.5`: Specifies the exact accession and version of human *HBB*.
   - `rettype=fasta`: Requests the FASTA sequence format.
   - `retmode=text`: Requests plain MIME text output rather than HTML or XML.

---

### 3. Protocol Deep Dive: HTTP/HTTPS vs FTP/SFTP

| Operational Metric | HTTP / HTTPS | FTP / SFTP |
|---|---|---|
| **Underlying State** | Stateless (each request/response is independent) | Stateful (connection maintained across directory changes) |
| **Connection Channels** | Single multiplexed channel (Port 80/443) | Dual channel: Control (Port 21) and Data (Port 20) |
| **Bandwidth Optimization** | Chunked transfer, Gzip compression on payload | Direct binary socket streaming; minimal protocol framing |
| **Typical File Scale** | Kilobytes to several Megabytes | Tens of Gigabytes to Terabytes |
| **Bioinformatics Role** | RESTful web APIs, interactive searches, dynamic JSON | Bulk genomic database distributions, raw read archives |

#### Why FTP Persists in Bioinformatics
While web browsers have largely phased out native FTP support, FTP (and secure SFTP / `rsync`) remains indispensable in computational biology. GenBank, Ensembl, and UCSC release complete database dumps containing hundreds of gigabytes of compressed flat files and indices. Downloading 50 GB via an HTTPS browser download frequently suffers connection timeouts, memory exhaustion, and failure to resume interrupted streams.

FTP utility programs (such as `wget`, `curl`, and `lftp`) support:
- **Resumable Transfers:** The `-c` or `--continue` flag inspects the local byte size and issues a `REST` (restart) command to resume downloading from the exact byte where a connection dropped.
- **Recursive Directory Mirroring:** Automated traversal of directory trees to mirror entire organismal clades.

---

### 4. The International Nucleotide Sequence Database Collaboration (INSDC)

The INSDC represents a historic international treaty among three foundational repositories:
1. **GenBank (NCBI):** National Center for Biotechnology Information, National Library of Medicine, NIH, Bethesda, Maryland, USA.
2. **European Nucleotide Archive (ENA / EMBL-EBI):** European Molecular Biology Laboratory - European Bioinformatics Institute, Wellcome Genome Campus, Hinxton, Cambridge, UK.
3. **DNA Data Bank of Japan (DDBJ):** National Institute of Genetics, Mishima, Shizuoka, Japan.

```
       NCBI GenBank                    EMBL-EBI ENA                     DDBJ
       (USA - NIH)                    (Europe - EMBL)                 (Japan - NIG)
            |                                |                              |
            \________________________________+______________________________/
                                             |
                          Overnight Tripartite Exchange
                   (Uniform Accession Space & Raw Submissions)
```

#### The Tripartite Operating Principles:
- **Unified Accession Space:** Accession number prefixes are strictly allocated to prevent collision. An accession assigned by DDBJ is unique worldwide.
- **Daily Synchronization:** New submissions, revisions, and metadata updates submitted to any one of the three nodes are packaged and mirrored to the other two nodes on a daily cycle.
- **Permanent Archival Mandate:** The INSDC is an archival record. Sequences are never deleted; if an author discovers an error, the record is updated with an incremented version number (e.g., `.1` to `.2`), but the original version remains retrievable in the historical record.

---

### 5. Primary Resource Hubs and Their Structural Specializations

| Hub | Host Institution & Location | Flagship Databases & Tools |
|---|---|---|
| **NCBI** | National Institutes of Health (NIH), Bethesda, MD, USA | **Entrez**, GenBank, RefSeq, PubMed, BLAST, ClinVar, SRA, Gene, GEO, MMDB |
| **EMBL-EBI** | European Molecular Biology Laboratory, Hinxton, UK | **Ensembl** (vertebrate genomes), **ENA**, UniProt (joint), InterPro, ChEMBL, PDBe |
| **Expasy / SIB** | Swiss Institute of Bioinformatics, Geneva, Switzerland | **Swiss-Prot** (expert protein curation), ProtParam, Swiss-Model, ENZYME |
| **wwPDB** | Consortium: RCSB (USA), PDBe (Europe), PDBj (Japan) | **Protein Data Bank (PDB)**: atomic coordinates of macromolecules |
| **DDBJ** | National Institute of Genetics (NIG), Mishima, Japan | **DDBJ**, Japanese genomic projects, DDBJ Read Archive (DRA) |

---

## Worked Example: Programmatic API Query vs Direct FTP

### Task: Retrieve the human *HBB* mRNA sequence via two distinct network modalities.

#### Modality A: RESTful HTTP Query via NCBI E-utilities
Using standard command-line HTTP clients (`curl` or `wget`):

```bash
# Issue an HTTPS GET request to the NCBI E-utilities efetch endpoint
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=NM_000518.5&rettype=fasta&retmode=text" -o hbb_mrna.fasta

# Inspect the downloaded FASTA stream
head -n 5 hbb_mrna.fasta
```

Expected output:
```
>NM_000518.5 Homo sapiens hemoglobin subunit beta (HBB), mRNA
ACATTTGCTTCTGACACAACTGTGTTCACTAGCAACCTCAAACAGACACCATGGTGCACCTGACTCCTGA
GGAGAAGTCTGCCGTTACTGCCCTGTGGGGCAAGGTGAACGTGGATGAAGTTGGTGGTGAGGCCCTGGGC
AGGTTGGTATCAAGGTTACAAGACAGGTTTAAGGAGACCAATAGAAACTGGGCATGTGGAGACAGAGAAG
ACTCTTGGGTTTCTGATAGGCACTGACTCTCTCTGCCTATTGGTCTATTTTCCCACCCTTAGGCTGCTGG
```

#### Modality B: Locating and Navigating NCBI FTP for Bulk Data
To download the complete human reference transcriptome (containing thousands of genes including *HBB*), we do not run 20,000 curl commands; we fetch the bulk archive from the RefSeq FTP release directory:

```bash
# Connect to NCBI FTP and fetch the compressed human RNA release catalog
wget -c "https://ftp.ncbi.nlm.nih.gov/genomes/refseq/vertebrate_mammalian/Homo_sapiens/latest_assembly_versions/GCF_000001405.40_GRCh38.p14/GCF_000001405.40_GRCh38.p14_rna.fna.gz"

# Decompress and search for NM_000518.5 using zgrep
zgrep -A 2 "NM_000518.5" GCF_000001405.40_GRCh38.p14_rna.fna.gz | head -n 3
```

---

## Formative In-Class Checks

### Question 1
**Prompt:** A bioinformatics student writes a shell script containing a `while` loop that calls `curl` against NCBI Entrez 50,000 consecutive times in 2 minutes. What will happen at both the transport/network level and the application level? How should this task be properly executed?

**Model Answer:**
- **What will happen:**
  1. *Application Level (NCBI Policy Violation):* NCBI strictly enforces automated query guidelines: without an API key, users are limited to a maximum of 3 requests per second; with an API key, the limit is 10 requests per second. Exceeding this threshold triggers an automated HTTP `429 Too Many Requests` status code, followed by a temporary or permanent IP address block by NCBI firewalls.
  2. *Transport/Network Level:* Spawning 50,000 distinct `curl` processes creates 50,000 separate TCP 3-way handshakes and TLS cryptographic handshakes, wasting local socket ports (ephemeral port exhaustion) and placing heavy connection-establishment overhead on the server.
- **Proper Execution:**
  1. Batch the queries: NCBI `efetch` accepts up to 500 comma-separated identifiers per single HTTP GET/POST request (e.g., `id=ID1,ID2,ID3...`), reducing 50,000 requests down to 100 requests.
  2. Throttle execution by introducing a sleep delay (`time.sleep(0.34)` in Python) to respect the 3 req/sec rate limit, and supply an NCBI API key (`&api_key=...`).
  3. For massive datasets, completely bypass web APIs and download the pre-computed bulk archive directly via FTP or use the Entrez Direct (`edirect`) pipeline.

---

### Question 2
**Prompt:** You are given the task of identifying which global database hub you would visit to perform each of the following four bioinformatics tasks. Name the exact resource and institution:
1. Obtain the curated 3D atomic coordinates of deoxygenated human hemoglobin.
2. Search for all peer-reviewed biomedical literature describing the discovery of the *HbS* mutation.
3. Compare the complete genomic synteny of the beta-globin locus between human and chimpanzee.
4. Calculate the theoretical isoelectric point (pI) of the human beta-globin polypeptide.

**Model Answer:**
1. **RCSB PDB (Worldwide Protein Data Bank - wwPDB):** To download structure coordinate files (PDB ID: `1A3N` or `4HHB`).
2. **PubMed (NCBI / NLM):** The biomedical literature database index using Entrez or MeSH terms.
3. **Ensembl (EMBL-EBI / Sanger):** The vertebrate comparative genomics browser specializing in synteny, gene orthology, and chromosomal alignments.
4. **Expasy (Swiss Institute of Bioinformatics - SIB):** Using the **ProtParam** tool to compute sequence-based physicochemical parameters.

---

### Question 3
**Prompt:** Explain why the INSDC maintains an "archival" policy where sequence records are never deleted or modified in place, but instead increment version numbers. What would happen to published scientific literature if GenBank allowed silent in-place editing of sequences?

**Model Answer:**
The INSDC enforces strict archival immutability to ensure **scientific reproducibility**. When a scientific paper is published in a journal citing GenBank accession `AF123456.1`, that scientific claim is inextricably tied to the exact sequence bases present on that date. 

If GenBank allowed silent in-place modifications:
1. Re-running published computational experiments years later could produce divergent results, different alignment scores, or altered translation frames without warning.
2. Citations in published literature would point to moving targets, destroying the traceability and auditing of scientific evidence.
By incrementing version suffixes (`.1` -> `.2`), the INSDC preserves the exact historical record of `AF123456.1` permanently, while allowing researchers to retrieve the updated, corrected sequence under `AF123456.2`.
