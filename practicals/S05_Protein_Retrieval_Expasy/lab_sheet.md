# Practical 05: Retrieving Protein Sequences from GenPept/NCBI and UniProtKB/Expasy

**Course Code:** CBBI-501 / CBBI-502  
**Course Title:** Concepts of Bioinformatics  
**Target Audience:** B.Tech. Bioinformatics, Semester II  
**Practical Session:** S05 (Syllabus Practical P5)  
**Duration:** 2 Hours (120 Minutes)  
**Learning Outcome (LO):** LO2 — Retrieve protein sequence records, contrast primary translation archives against manually curated knowledgebases, and parse UniProtKB flat files.

---

## 1. Aim & Objectives

### Aim
To retrieve protein sequence records from the NCBI Protein database (historically known as GenPept) and the UniProtKB/Expasy Swiss-Prot database, critically analyze the differences between automated conceptual translations and expert manual curation, and decipher protein sequence numbering conventions.

### Objectives
1. Retrieve human hemoglobin subunit beta from NCBI Protein (`NP_000509.1`) and UniProtKB (`P68871` / `HBB_HUMAN`).
2. Dissect the UniProtKB Swiss-Prot entry structure: Entry Name, Accession, Status (Reviewed/Curated), Function, Subcellular Location, Subunit Structure, Post-Translational Modifications (PTMs), Mutagenesis, and Pathology/Variants.
3. Contrast the two-tier structure of UniProtKB: the manually reviewed **Swiss-Prot** section versus the unreviewed computationally translated **TrEMBL** section.
4. Resolve the historical amino acid numbering discrepancy of the sickle cell mutation: classical clinical biochemical nomenclature (Glu6Val / E6V) versus formal initiator methionine sequence coordinates (Glu7Val / p.Glu7Val).
5. Compare the depth of functional annotation between NCBI Protein flat files and UniProtKB entries.

---

## 2. Background & Scientific Principle

### The Evolution of Protein Repositories
In the early days of molecular biology, protein sequences were deduced either through laborious Edman degradation chemical sequencing or by translating nucleotide submissions.
- **GenPept (NCBI Protein):** Originally established by NCBI to collect automated conceptual translations of coding regions (CDS features) present in GenBank nucleotide records. While RefSeq provides curated records (`NP_` accessions), NCBI Protein records primarily preserve the translation coordinates and nucleotide-linked feature metadata.
- **Expasy (Expert Protein Analysis System):** Launched in 1993 by the Swiss Institute of Bioinformatics (SIB) in Geneva, Expasy was the first life sciences website in the world. It hosted the **Swiss-Prot** database, founded by Amos Bairoch in 1986.
- **UniProt (Universal Protein Resource):** In 2002, the SIB, the European Bioinformatics Institute (EMBL-EBI), and the Protein Information Resource (PIR) united to create UniProt.

### Swiss-Prot vs. TrEMBL: Two Tiers of Curation
UniProtKB is partitioned into two distinct repositories:
1. **UniProtKB/Swiss-Prot (Reviewed):**
   - High-quality, manually annotated, non-redundant database.
   - Expert biocurators read peer-reviewed literature and manually extract protein functions, enzyme kinetics ($K_m$, $V_{max}$), 3D structural domains, binding sites, quaternary oligomeric states, post-translational modifications (PTMs like phosphorylation, acetylation, ubiquitination), and disease-causing natural variants.
   - Entries are assigned an immutable Accession (e.g., `P68871`) and an informative Entry Name (e.g., `HBB_HUMAN`).
2. **UniProtKB/TrEMBL (Unreviewed):**
   - **Tr**anslated **EMBL**.
   - Contains automated computer-generated translations of all EMBL-Bank/GenBank/DDBJ coding sequences not yet reviewed by human curators.
   - Massive in scale (>200 million records), but prone to fragment sequences, automated annotation transfer errors, and lacking experimental literature curation.

### The Sickle Cell Numbering Dilemma (E6V vs. E7V)
A critical lesson in biological database informatics is understanding sequence coordinate conventions:
- When Linus Pauling and Vernon Ingram (1956) chemically sequenced the beta-globin polypeptide from red blood cells using peptide fingerprinting, the mature circulating protein had already undergone post-translational **initiator methionine cleavage** by cellular methionine aminopeptidase. Thus, Val-His-Leu-Thr-Pro-**Glu** was labeled residues 1 to 6, giving the celebrated designation **Glu6Val (E6V)**.
- In genomic databases (GenBank `NP_000509.1` and HGVS nomenclature), the sequence begins with the translation-initiating Methionine (`Met-Val-His-Leu-Thr-Pro-Glu...`), placing the mutated glutamic acid at **residue position 7 (p.Glu7Val)**.
- UniProtKB explicitly cross-references both the precursor coordinate (position 7) and the mature processed chain coordinate (position 6), preventing clinical diagnostic confusion.

---

## 3. Required Software, Tools, and Input Datasets

### Web Portals & URLs
- NCBI Protein Database: [https://www.ncbi.nlm.nih.gov/protein/](https://www.ncbi.nlm.nih.gov/protein/)
- UniProt Knowledgebase: [https://www.uniprot.org/](https://www.uniprot.org/)
- Expasy SIB Resource Portal: [https://www.expasy.org/](https://www.expasy.org/)

### Target Accessions
- NCBI RefSeq Protein: `NP_000509.1`
- UniProtKB Swiss-Prot Entry: `P68871` (Entry Name: `HBB_HUMAN`)
- Local Sequence Files: `../../data/sequences/hbb_human_protein.fasta`, `../../data/sequences/hbs_human_protein.fasta`.

---

## 4. Detailed Step-by-Step Procedure

### Phase 1: Retrieving `NP_000509.1` from NCBI Protein
1. Navigate to [https://www.ncbi.nlm.nih.gov/protein/](https://www.ncbi.nlm.nih.gov/protein/).
2. In the query box, enter `NP_000509.1` and click **Search**.
3. Inspect the GenPept flat file view:
   - Note the `LOCUS` line: `NP_000509  147 aa  linear  PRI`.
   - Locate the `DBSOURCE` line indicating derivation from `REFSEQ: accession NM_000518.5`.
   - Scroll through the `FEATURES` section: note `Site` features indicating heme binding sites (e.g., His93 proximal, His64 distal) and $\alpha_1\beta_1$ / $\alpha_1\beta_2$ dimer interface contacts.
4. Click **FASTA** to view the raw single-letter sequence.

### Phase 2: Retrieving `P68871` from UniProtKB
1. Open [https://www.uniprot.org/](https://www.uniprot.org/).
2. In the search box, enter `P68871` and press **Enter**.
3. Confirm that the top hit shows:
   - Entry: `P68871`
   - Entry Name: `HBB_HUMAN`
   - Protein: `Hemoglobin subunit beta`
   - Gene: `HBB`
   - Organism: `Homo sapiens (Human)`
   - Status: Golden icon labeled **Reviewed (Swiss-Prot)** with high annotation score (5/5).
4. Click on `P68871` to enter the complete Swiss-Prot curation entry.

### Phase 3: Exploring Swiss-Prot Annotation Categories
Navigate the left sidebar navigation anchors on the `P68871` page:
1. **Function:**
   - Read the molecular function description (involved in oxygen transport from lung to tissues).
   - Note cofactor binding: Heme b (iron protoporphyrin IX).
2. **Subunit Structure:**
   - Note the quaternary structure: Heterotetramer consisting of two alpha chains and two beta chains ($\alpha_2\beta_2$).
3. **Subcellular Location:**
   - Note cellular compartment: Cytoplasm and red blood cell cytosol.
4. **PTM / Processing:**
   - Locate the feature table for **Molecule processing**:
     - Initiator methionine: Position `1` (Removed by methionine aminopeptidase).
     - Beta-globin mature chain: Positions `2..147` (Length: 146 amino acids).
   - Note post-translational modifications (e.g., Glycation of Val-2 in diabetic hemoglobin HbA1c; S-nitrosylation of Cys-94).
5. **Pathology & Variants:**
   - Scroll to the **Natural variants** table.
   - Search for variant `VAR_003881` or position `7`: `E -> V` (in Hb S).
   - Notice the curated description of Sickle Cell Anemia, erythrocyte sickling under low oxygen tension, and associated malaria resistance (*Plasmodium falciparum*).
6. **Cross-References:**
   - Inspect cross-references to 3D structure databases (PDB entries `1A3N`, `4HHB`, `2HBS`).

### Phase 4: Downloading and Inspecting UniProt Flat File Format
1. At the top right of the UniProt page, click the **Download** button.
2. Select **Text (flat file)** format.
3. Open the downloaded file in a text editor (or view in browser):
   - Notice the line headers:
     - `ID` : Identification line (`HBB_HUMAN Reviewed; 147 AA.`)
     - `AC` : Primary accession (`P68871;`)
     - `DE` : Description / Protein names
     - `GN` : Gene names (`Name=HBB;`)
     - `OS` / `OC` : Organism Species and Classification
     - `CC` : Free-text Comments (`-!- FUNCTION:`, `-!- SUBUNIT:`, `-!- DISEASE:`)
     - `FT` : Feature Table (`CHAIN`, `MOD_RES`, `VARIANT`, `BINDING`)
     - `SQ` : Sequence header followed by checksum and 10-residue sequence blocks.

---

## 5. Offline Fallback Note

If internet connectivity to NCBI Protein or UniProt is degraded:
- Open local files `../../data/sequences/hbb_human_protein.fasta` and `../../data/sequences/hbs_human_protein.fasta`.
- Review the comprehensive UniProt flat file excerpts and comparison matrices provided in the instructor answer key.

---

## 6. Observations Table

### Table 5.1: Comparative Annotation Matrix (NCBI Protein vs. UniProtKB Swiss-Prot)
| Feature / Annotation Field | NCBI RefSeq (`NP_000509.1`) | UniProtKB Swiss-Prot (`P68871`) |
|---|---|---|
| Primary Database Category | Automated / RefSeq Curated | Expert Manual Literature Curation |
| Primary Identifier / Accession | | |
| Review / Curation Status | | |
| Sequence Length (aa) | | |
| Mature Chain Coordinates | | |
| Functional Mechanism & Subunit Stoichiometry | | |
| Post-Translational Modifications (PTMs) | | |
| Natural Variants & Phenotypes Curated | | |
| Cross-References to PDB Structures | | |
| Cross-References to Medical Genetics (OMIM/ClinVar) | | |

### Table 5.2: Natural Variant Comparison (Sickle Cell Mutation)
| Attribute | Clinical Historical Standard | UniProtKB Curated Coordinate | NCBI RefSeq Coordinate |
|---|---|---|---|
| Mutation Notation | Glu6Val (E6V) | | |
| Wild-type Residue | Glutamic acid (Glu / E) | | |
| Mutant Residue | Valine (Val / V) | | |
| Position Number | 6 | | |
| Biological Explanation for Numbering Difference | | | |

---

## 7. Interpretation & Discussion Questions

1. **Swiss-Prot vs. TrEMBL Growth Rates:** Why is UniProtKB/TrEMBL growing exponentially at orders of magnitude faster than UniProtKB/Swiss-Prot? What are the key bottlenecks limiting Swiss-Prot manual curation?
2. **Initiator Methionine Cleavage:** Explain why the mature circulating human beta-globin protein in erythrocytes contains 146 amino acids, while the genomic CDS translation (`NP_000509.1`) reports 147 residues. Which enzyme performs this post-translational cleavage?
3. **HbA1c Clinical Biomarker:** In the UniProt entry `P68871`, locate the PTM annotation for glycated hemoglobin (HbA1c). Which specific residue is glycated, and why is HbA1c measured in clinical diabetes monitoring?
4. **Primary Accession Stability:** If two distinct Swiss-Prot entries are merged because modern experimental evidence proves they are the same protein, how does UniProt handle their accession numbers? What is the difference between a primary accession and a secondary accession?
5. **Database Cross-Referencing:** How does UniProtKB integrate functional proteomics with 3D structural biology? Name three structural databases cross-referenced in `P68871`.

---

## 8. Extension / Challenge Task (For Advanced Students)

1. Use the UniProt search bar with advanced query syntax:
   ```
   gene:HBB AND reviewed:true
   ```
2. Identify how many mammalian orthologues of beta-globin have been manually reviewed in Swiss-Prot.
3. Compare the human HBB entry (`P68871`) against the mouse (*Mus musculus*) beta-globin entry (`P02088` or `P02089`).
4. Identify whether mouse hemoglobin undergoes the same initiator methionine cleavage.
