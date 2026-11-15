---
marp: true
theme: default
paginate: true
header: "CBBI-501 · Lecture 02 Slides: Internet Protocols and Resources"
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
# Lecture 02 — Internet Protocols and Resources
### Concepts of Bioinformatics (CBBI-501)
**Unit 01:** Bioinformatics and Internet  
**Format:** 8-Slide Canonical University Presentation Deck  
[View Interactive Web Presentation](https://meprateekpaul.github.io/conceptsbio.html#lectures)

---

## Slide 1: Biological Data Over the Wire

```text
Topic: Moving Petabytes Across Global Networks

[Visual: Network diagram connecting User Workstation -> ISP -> Transatlantic Fiber
         -> NCBI (Bethesda, USA) / EMBL-EBI (Hinxton, UK) / DDBJ (Mishima, Japan)]
```

**Speaker Talking Points:**  
* Modern bioinformatics is intrinsically distributed: no individual laptop can store
  all biological data. We retrieve data across the Internet continuously.
* Understanding the underlying network stack ensures we build robust, scalable,
  and reproducible computational pipelines.
* Today's focus: TCP/IP, URLs, HTTP vs FTP, REST APIs, and the global database hubs.

---

## Slide 2: The Client-Server Architecture in Bioinformatics

```text
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
```

**Speaker Talking Points:**  
* In bioinformatics, the "Client" is rarely just a web browser; it is often a Python
  script, an R session, or a command-line utility (`curl`, `wget`, `efetch`).
* The server processes the request, interfaces with back-end indexing engines,
  and streams the requested payload (FASTA, XML, JSON, or flat file).

---

## Slide 3: Anatomy of a Biological URL

```text
Topic: Deconstructing Web Locators

  https://eutils.ncbi.nlm.nih.gov:443/entrez/eutils/efetch.fcgi?db=nuccore&id=NM_000518.5&rettype=fasta
  \___/   \_____________________/ \__/ \______________________/ \_____________________________________/
    |                |              |              |                               |
 Protocol        Hostname          Port           Path                        Query String
```

**Speaker Talking Points:**  
* Protocol (`https`): Secure HyperText Transfer Protocol (encrypted via TLS).
* Hostname: Fully Qualified Domain Name (FQDN) resolved via DNS to an IP address.
* Port (`443` default for HTTPS; `80` for HTTP).
* Path: Directs the request to the specific CGI/REST endpoint script on the server.
* Query String (`?key=value&...`): Parameters passed to the application.

---

## Slide 4: HTTP/HTTPS vs FTP/SFTP

```text
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
```

**Speaker Talking Points:**  
* When you need one record (`NM_000518.5`), use HTTPS via web or REST API.
* When you need all human RefSeq mRNAs (millions of records), HTTPS web queries
  will time out or be rate-limited; use FTP bulk dumps.

---

## Slide 5: Bulk Data Acquisition via FTP

```text
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
```

**Speaker Talking Points:**  
* NCBI FTP (`ftp.ncbi.nlm.nih.gov`) and EBI FTP (`ftp.ebi.ac.uk`) host public data archives.
* Files are compressed with gzip (`.gz`) or tar (`.tar.gz`) to conserve bandwidth.
* Best practice: Use `wget -c` (continue broken downloads) or `rsync` for synchronization.

---

## Slide 6: The INSDC: Global Tripartite Synchronization

```text
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
```

**Speaker Talking Points:**  
* Established in 1988 to prevent fragmented sequence silos.
* A sequence submitted to DDBJ in Japan is synchronized overnight to NCBI and EBI.
* Shared accession numbering space ensures universal, unique identification.

---

## Slide 7: Major Global Bioinformatics Resource Hubs

```text
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
```

**Speaker Talking Points:**  
* Notice how functional roles are distributed: GenBank is archival; RefSeq is curated;
  UniProt focuses on proteins; PDB governs 3D structures.

---

## Slide 8: Programmatic Access vs Interactive Browsers

```text
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

