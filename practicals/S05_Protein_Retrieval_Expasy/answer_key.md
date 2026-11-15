# Instructor Answer Key & Evaluation Manual: Practical 05 (Protein Retrieval)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S05 (Syllabus Practical P5)  
**Curriculum Topic:** Retrieving Protein Sequence from GenPept/NCBI and Expasy/UniProtKB  

---

## 1. Expected Outputs & Reference Solutions

### Table 5.1: Comparative Annotation Matrix (Completed)
| Feature / Annotation Field | NCBI RefSeq (`NP_000509.1`) | UniProtKB Swiss-Prot (`P68871`) |
|---|---|---|
| Primary Database Category | NCBI RefSeq (curated from conceptual translation) | UniProtKB/Swiss-Prot (expert manual literature curation) |
| Primary Identifier / Accession | `NP_000509.1` | `P68871` (Entry Name: `HBB_HUMAN`) |
| Review / Curation Status | Curated RefSeq | Reviewed (Swiss-Prot, Annotation Score: 5/5) |
| Total Sequence Length (aa) | 147 aa | 147 aa |
| Mature Chain Coordinates | Not split into precursor/chain in basic FASTA; annotated in Features | Explicitly split: Initiator Met (`1`), Mature chain (`2..147`, 146 aa) |
| Functional Mechanism & Quaternary Structure | Basic summary text derived from Gene entry | In-depth: Heterotetramer ($\alpha_2\beta_2$), cooperativity, allosteric transition (T to R state), 2,3-BPG binding |
| Post-Translational Modifications (PTMs) | Limited site features | Comprehensive: Glycation (Val-2 HbA1c), S-nitrosylation (Cys-94), acetylation |
| Natural Variants & Phenotypes Curated | Cross-links to ClinVar / dbSNP | Hundreds of manually curated natural variants with clinical descriptions (HbS, HbC, HbE, thalassemias) |
| Cross-References to PDB Structures | Links via MMDB / Identical Protein groups | Direct structural links to >100 PDB entries (1A3N, 4HHB, 2HBS, etc.) with resolution and chain mapping |
| Cross-References to Medical Genetics | Links to OMIM, ClinVar, dbSNP | Cross-references to OMIM (`141900`, `603903`), Orphanet, ClinVar, DisGeNET |

### Table 5.2: Natural Variant Comparison (Sickle Cell Mutation) (Completed)
| Attribute | Clinical Historical Standard | UniProtKB Curated Coordinate | NCBI RefSeq Coordinate |
|---|---|---|---|
| Mutation Notation | Glu6Val (E6V) / Hb S | p.Glu7Val (legacy: Glu6Val) | p.Glu7Val (E7V) |
| Wild-type Residue | Glutamic acid (Glu / E) | Glutamic acid (Glu / E) | Glutamic acid (Glu / E) |
| Mutant Residue | Valine (Val / V) | Valine (Val / V) | Valine (Val / V) |
| Position Number | 6 | 7 (precursor) / 6 (mature chain) | 7 (translated CDS coordinate) |
| Biological Explanation for Difference | Circulating mature protein was sequenced after removal of initiator Met. | Precursor coordinates include Met1. Notes explicitly state: mature chain position 6. | Sequence coordinates strictly follow the 5'->3' open reading frame starting at Met1. |

---

## 2. Sample UniProt Flat File Excerpt (`P68871.txt`)

```
ID   HBB_HUMAN               Reviewed;         147 AA.
AC   P68871; P02023; Q13852; Q14481; Q14510;
DT   21-JUL-1986, integrated into UniProtKB/Swiss-Prot.
DE   RecName: Full=Hemoglobin subunit beta;
DE   AltName: Full=Beta-globin;
DE   AltName: Full=Hemoglobin beta chain;
GN   Name=HBB;
OS   Homo sapiens (Human).
OC   Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Euteleostomi;
OC   Mammalia; Eutheria; Euarchontoglires; Primates; Haplorrhini;
OC   Catarrhini; Hominidae; Homo.
CC   -!- FUNCTION: Involved in oxygen transport from the lung to the various
CC       peripheral tissues. {ECO:0000269|PubMed:15395398}.
CC   -!- SUBUNIT: Heterotetramer of two alpha and two beta chains.
CC   -!- DISEASE: Sickle cell anemia (SCA) [MIM:603903]: A severe hemolytic
CC       disease characterized by rigid, sickle-shaped erythrocytes...
FT   INIT_MET        1
FT                   /note="Removed"
FT   CHAIN           2..147
FT                   /note="Hemoglobin subunit beta"
FT                   /id="PRO_0000094770"
FT   VARIANT         7
FT                   /note="E -> V (in Hb S; sickle cell anemia; dbSNP:rs334)"
FT                   /id="VAR_003881"
FT   MOD_RES         2
FT                   /note="N-glycated valine (in Hb A1c)"
SQ   SEQUENCE   147 AA;  15998 MW;  C438BEFF61AFB2FE CRC64;
     MVHLTPEEKS AVTALWGKVN VDEVGGEALG RLLVVYPWTQ RFFESFGDLS TPDAVMGNPK
     VKAHGKKVLG AFSDGLAHLD NLKGTFATLS ELHCDKLHVD PENFRLLGNV LVCVLAHHFG
     KEFTPPVQAA YQKVVAGVAN ALAHKYH
//
```

---

## 3. Model Answers to Discussion Questions

### Q1. Swiss-Prot vs. TrEMBL Growth Rates
- **Model Answer:** UniProtKB/TrEMBL expands automatically at an exponential rate because next-generation high-throughput sequencing projects deposit millions of raw whole genomes, metagenomes, and transcriptomes directly into the INSDC databases (ENA/GenBank/DDBJ), which are computationally translated overnight without manual intervention. By contrast, UniProtKB/Swiss-Prot curation requires professional doctoral-level biocurators who read full-text scientific papers, evaluate contradictory experimental data, extract kinetic/biophysical parameters, and standardize annotations according to controlled vocabularies. Manual reading and curation constitute an intellectual bottleneck that cannot keep pace with automated raw sequence generation.

### Q2. Initiator Methionine Cleavage
- **Model Answer:** In eukaryotes, protein translation is initiated at an AUG start codon encoding Methionine (`Met-1`). In the erythroblast cytosol, the nascent beta-globin polypeptide is recognized by the enzyme **methionine aminopeptidase (MAP)**. Because the residue adjacent to methionine has a small uncharged side chain (Valine at position 2), methionine aminopeptidase cotranslationally cleaves the initiator methionine off the N-terminus. Therefore, mature circulating hemoglobin beta chains circulating in peripheral blood have 146 amino acids beginning with Val-1 (corresponding to position 2 of the genomic precursor).

### Q3. HbA1c Clinical Biomarker
- **Model Answer:** In `P68871`, residue Val-2 (the N-terminal valine of the mature chain) undergoes non-enzymatic condensation with blood glucose, forming a stable Amadori product known as **glycated hemoglobin (HbA1c)**. Because erythrocytes circulate for an average lifespan of 120 days, the percentage of glycated hemoglobin directly reflects the mean blood glucose concentration over the preceding 2 to 3 months, making HbA1c the gold standard clinical diagnostic biomarker for long-term glycemic control in diabetes mellitus.

### Q4. Primary Accession Stability
- **Model Answer:** When two distinct Swiss-Prot records are merged (or an existing record is split), UniProt maintains absolute database backward-compatibility. One accession number is designated as the **Primary Accession** (the current official identifier, e.g., `P68871`), while the superseded accessions (e.g., `P02023`, `Q13852`) are retained in the record as **Secondary Accessions**. Any historical script or published paper querying the secondary accession is automatically redirected by the database engine to the updated primary entry without breaking automated workflows.

### Q5. Database Cross-Referencing
- **Model Answer:** UniProtKB functions as a universal central hub cross-referencing over 150 biological databases. For 3D macromolecular structures, `P68871` cross-references:
  1. **PDB / wwPDB:** Worldwide Protein Data Bank of experimentally determined atomic coordinates (e.g., `1A3N`, `4HHB`, `2HBS`).
  2. **AlphaFold Protein Structure Database:** AI-predicted high-confidence 3D models.
  3. **PDBe-KB:** PDB Knowledge Base collating functional and ligand-binding structural annotations.
  4. **SWISS-MODEL Repository:** Homology models based on known structural templates.

---

## 4. Solution to Extension / Challenge Task

1. **Reviewed Mammalian HBB Query:** Querying `gene:HBB AND taxonomy_id:40674 AND reviewed:true` returns ~20–30 curated mammalian beta-globin entries (Human, Chimpanzee, Gorilla, Mouse, Rat, Bovine, Sheep, etc.).
2. **Mouse HBB Comparison (`P02088` / `HBB1_MOUSE`):**
   - Sequence length: 147 aa.
   - Sequence: `MVHLTDAEKSAVSCLWAKVNPDEVGGEALGRLLVVYPWTQRYFDSFGDLSSASAIMGNPKVKAHGKKVITAFNEGLKHLDNLKGTFASLSELHCDKLHVDPENFRLLGNMIVIVLGHHLGKEFTPCAQAAFQKVVAGVASALAHKYH`.
   - Feature table explicitly records `INIT_MET 1 /note="Removed"` and `CHAIN 2..147 /note="Hemoglobin subunit beta-1"`.
   - Demonstrates that initiator methionine cleavage is universally conserved across mammalian beta-globin orthologues.

---

## 5. Rubric & Marking Scheme

| Metric | Max Marks | Deduction Guidelines |
|---|:---:|---|
| **Pre-lab & Identification** | 2.0 | Deduct 0.5 if student fails to retrieve both NP_000509 and P68871. |
| **Comparative Annotation Table** | 4.0 | Deduct 0.5 per missing or superficial field in Table 5.1. |
| **Numbering Discrepancy (E6V vs E7V)** | 2.0 | Full marks awarded for explaining initiator Met removal by methionine aminopeptidase. |
| **Discussion Questions & Critical Viva** | 2.0 | Award 0.4 marks per question for accurate, comprehensive biological explanations. |
| **Total** | **10.0** | |
