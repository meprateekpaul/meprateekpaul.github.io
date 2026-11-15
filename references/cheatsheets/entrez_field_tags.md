# Quick Reference: NCBI Entrez Field Tags & Search Syntax

Entrez uses qualified search terms enclosed in square brackets `[TAG]` combined with Boolean operators (`AND`, `OR`, `NOT`). Operators must be capitalized.

---

## 1. Universal & Commonly Used Field Tags

| Tag | Field Name | Description & Example |
|---|---|---|
| `[GENE]` | Gene Name | Official gene symbol: `HBB[GENE]`, `INS[GENE]`, `TP53[GENE]` |
| `[ORGN]` | Organism | Scientific or common name: `Homo sapiens[ORGN]`, `vertebrates[ORGN]` |
| `[ACCN]` | Accession | Database accession number: `NM_000518[ACCN]`, `P68871[ACCN]` |
| `[TITL]` | Title Word | Words in title: `sickle cell[TITL]`, `crystal structure[TITL]` |
| `[AUTH]` | Author Name | Standard format (Last FM): `Lawn RM[AUTH]`, `Altschul SF[AUTH]` |
| `[JOUR]` | Journal Name | Standard ISO journal abbreviation: `J Mol Biol[JOUR]`, `Cell[JOUR]` |
| `[PDAT]` | Publication Date | Single date or range (YYYY/MM/DD): `1978[PDAT]`, `2015:2025[PDAT]` |
| `[PROP]` | Properties | Pre-computed filters: `biomol mrna[PROP]`, `srcdb refseq[PROP]` |
| `[SLEN]` | Sequence Length | Exact length or range: `400:700[SLEN]` |
| `[MMLS]` | Molecule Type | Molecule type: `biomol dna[MMLS]`, `biomol rna[MMLS]` |
| `[MESH]` | MeSH Terms | Medical Subject Headings (PubMed): `Anemia, Sickle Cell[MESH]` |

---

## 2. RefSeq Accession Prefixes

| Prefix | Molecule Type | Status |
|---|---|---|
| `NM_` | mRNA (Transcript) | Curated protein-coding nucleotide record (e.g. `NM_000518`) |
| `NP_` | Protein | Curated translation of NM_ record (e.g. `NP_000509`) |
| `NR_` | Non-coding RNA | Curated non-coding RNA (lncRNA, microRNA, rRNA) |
| `NC_` | Genomic | Complete chromosome or organelle genome (e.g. `NC_001422`) |
| `NG_` | Genomic | Curated genomic gene region / locus |
| `XM_` / `XP_` | mRNA / Protein | Automated computational model (uncorated, predicted) |

---

## 3. High-Precision Query Examples

- **Find curated human beta-globin mRNA only:**  
  `HBB[GENE] AND Homo sapiens[ORGN] AND biomol mrna[PROP] AND srcdb refseq[PROP]`
- **Find sickle-cell crystal structures with resolution ≤ 2.5 Å:**  
  `sickle cell[TITL] AND "Homo sapiens"[ORGN] AND 0.0:2.5[RESL]`
- **PubMed search for classic Needleman-Wunsch algorithm:**  
  `Needleman SB[AUTH] AND Wunsch CD[AUTH] AND 1970[PDAT]`
