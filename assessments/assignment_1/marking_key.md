# Marking Key & Exhaustive Reference Guide: Assignment 1

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Assignment:** Characterise an Unknown Protein Sequence  
**Total Marks:** 100 Marks (Scaled to 5% Course Weight)  

---

## 1. Grading Rubric and Sectional Mark Allocations

| Section | Target Dimension | Max Marks | Core Assessment Criteria |
| :---: | :--- | :---: | :--- |
| **1** | Sequence Identification & Evidence | **25** | Correct protein name, gene, organism (10); complete hit table with E-value, bit score, coverage, identity (10); rigorous Karlin–Altschul statistical reasoning (5). |
| **2** | Pairwise Alignment & Conservation | **20** | Proper Swiss-Prot accession retrieval (5); EMBOSS needle/water execution with reported parameters (5); accurate identity/similarity/gap percentages (5); critical discussion of discrepancies/signal peptides (5). |
| **3** | Physicochemical Characterisation | **20** | Complete, accurate ProtParam metrics (MW, pI, charges, extinction coeff, instability, GRAVY) (10); ProtScale hydropathy plot (5); biological interpretation of solubility/membrane state (5). |
| **4** | Motifs & Secondary Structure | **20** | PROSITE / InterPro motif identification with coordinates (8); catalytic/disulfide/active site mapping (6); GOR/PSIPRED percentages and fold class categorization (6). |
| **5** | 3D Structure & Visualisation | **15** | Valid PDB ID, method, resolution (5); high-resolution rendered 3D image with labeled catalytic/active residues (6); accurate structural caption (4). |
| **Total** | | **100** | Scaled to 5.0 Marks Continuous Evaluation |

---

## 2. Master Key for the 10 Unknown Sequences

### Sequence 01: `unknown_seq_01`
* **Organism:** *Equus caballus* (Horse)  
* **Gene Symbol:** *MB*  
* **Protein Name:** Myoglobin  
* **Length:** 153 amino acids  
* **Primary UniProt Accession:** `P68082` (or `P02144` Horse / Human orthologue)  
* **Biological Function:** Monomeric cytoplasmic hemoprotein that stores molecular oxygen in muscle tissue and facilitates oxygen diffusion to mitochondria.  
* **Key Active Sites & Domains:**
  - Globin domain (Pfam: `PF00042`)
  - Proximal Histidine (His93 / F8) coordinating heme $Fe^{2+}$
  - Distal Histidine (His64 / E7) stabilizing bound $O_2$
  - Protoporphyrin IX (heme) binding pocket
* **Expected BLAST Top Hit:** `NP_001157486.1` / `P68082.2` myoglobin [*Equus caballus*], 100% identity, $E \approx 2 \times 10^{-105}$, bit score $>290$.  
* **Physicochemical Properties:** MW $\approx 16.95\text{ kDa}$, theoretical pI $\approx 6.8\text{--}7.2$, GRAVY $\approx -0.38$ (globular soluble protein), Instability Index $\approx 28$ (stable).  
* **Secondary Structure & Fold:** All-alpha class; ~75% alpha-helix (8 classic helices A through H), ~0% beta-sheet, ~25% coil.  
* **Representative PDB Structure:** `1WLA` (X-ray, $1.40\text{ \AA}$) or `1AZI` ($1.55\text{ \AA}$).

---

### Sequence 02: `unknown_seq_02`
* **Organism:** *Gallus gallus* (Chicken / Hen egg-white)  
* **Gene Symbol:** *LYZ*  
* **Protein Name:** Lysozyme C (1,4-beta-N-acetylmuramidase C)  
* **Length:** 129 amino acids (mature form)  
* **Primary UniProt Accession:** `P00698`  
* **Biological Function:** Innate antimicrobial defense enzyme that hydrolyzes $\beta(1\rightarrow 4)$ glycosidic bonds between N-acetylmuramic acid (NAM) and N-acetylglucosamine (NAG) in bacterial peptidoglycan cell walls.  
* **Key Active Sites & Domains:**
  - Glycosyl hydrolase family 22 (Pfam: `PF00959`)
  - Catalytic Dyad: **Glu35** (general acid proton donor) and **Asp52** (nucleophile stabilizing oxocarbenium transition state)
  - 4 invariant Disulfide Bridges: Cys6-Cys127, Cys30-Cys115, Cys64-Cys80, Cys76-Cys94
* **Expected BLAST Top Hit:** `P00698.1` Lysozyme C [*Gallus gallus*], 100% identity, $E \approx 4 \times 10^{-89}$, bit score $>250$.  
* **Physicochemical Properties:** MW $\approx 14.31\text{ kDa}$, theoretical pI $\approx 9.3\text{--}9.6$ (strongly basic enzyme), GRAVY $\approx -0.47$, Instability Index $\approx 38$ (stable).  
* **Secondary Structure & Fold:** Alpha + Beta ($\alpha+\beta$) class; ~35% alpha-helix, ~12% beta-sheet, ~53% loop/coil.  
* **Representative PDB Structure:** `1LYZ` (X-ray, $2.0\text{ \AA}$), `2LYZ`, or `6LYZ` ($1.30\text{ \AA}$).

---

### Sequence 03: `unknown_seq_03`
* **Organism:** *Bos taurus* (Bovine / Cattle)  
* **Gene Symbol:** *RNASE1*  
* **Protein Name:** Ribonuclease pancreatic (Ribonuclease A / RNase A)  
* **Length:** 124 amino acids (mature chain)  
* **Primary UniProt Accession:** `P61823`  
* **Biological Function:** Endoribonuclease that cleaves single-stranded RNA at the $3'$ end of pyrimidine nucleotides (CpX and UpX bonds) via a 2',3'-cyclic phosphate intermediate.  
* **Key Active Sites & Domains:**
  - Pancreatic ribonuclease family (Pfam: `PF00074`)
  - Catalytic Triad: **His12** (general base), **Lys41** (transition state stabilization), and **His119** (general acid)
  - 4 Disulfide Bonds: Cys26-Cys84, Cys40-Cys95, Cys58-Cys110, Cys65-Cys72
* **Expected BLAST Top Hit:** `P61823.1` Ribonuclease pancreatic [*Bos taurus*], 100% identity, $E \approx 3 \times 10^{-84}$, bit score $>240$.  
* **Physicochemical Properties:** MW $\approx 13.68\text{ kDa}$, theoretical pI $\approx 8.6\text{--}8.9$ (basic), GRAVY $\approx -0.60$ (soluble), Instability Index $\approx 35$ (stable).  
* **Secondary Structure & Fold:** Alpha + Beta ($\alpha+\beta$) class; ~22% alpha-helix, ~38% beta-sheet, ~40% coil. Kidney-shaped cleft.  
* **Representative PDB Structure:** `1RCA` ($1.45\text{ \AA}$) or `7RSA` ($1.26\text{ \AA}$).

---

### Sequence 04: `unknown_seq_04`
* **Organism:** *Homo sapiens* (Human)  
* **Gene Symbol:** *INS*  
* **Protein Name:** Preproinsulin  
* **Length:** 110 amino acids  
* **Primary UniProt Accession:** `P01308`  
* **Biological Function:** Peptide hormone central to regulating glucose homeostasis; processed into mature active insulin (A and B chains linked by disulfides) following removal of signal peptide and C-peptide.  
* **Key Active Sites & Domains:**
  - Signal peptide: Residues 1–24
  - Insulin B chain: Residues 25–54
  - C-peptide: Residues 57–87 (cleaved out by prohormone convertases PC1/3 and PC2)
  - Insulin A chain: Residues 90–110
  - 3 Disulfide Bonds: Cys31-Cys96 (inter-chain), Cys43-Cys109 (inter-chain), Cys95-Cys100 (intra-A chain)
* **Expected BLAST Top Hit:** `NP_000198.1` / `AAA59172.1` insulin preproprotein [*Homo sapiens*], 100% identity, $E \approx 2 \times 10^{-72}$, bit score $>210$.  
* **Physicochemical Properties:** MW $\approx 11.98\text{ kDa}$, theoretical pI $\approx 5.5\text{--}5.8$, GRAVY $\approx -0.19$, Instability Index $\approx 46$ (preproprotein is transiently processed).  
* **Secondary Structure & Fold:** Alpha-dominant hormone fold; ~35% alpha-helix, ~0% beta-sheet, ~65% loops/coils.  
* **Representative PDB Structure:** `4INS` (mature insulin, $1.50\text{ \AA}$) or `1TRZ` ($1.60\text{ \AA}$).

---

### Sequence 05: `unknown_seq_05`
* **Organism:** *Equus caballus* (Horse)  
* **Gene Symbol:** *CYCS*  
* **Protein Name:** Cytochrome c  
* **Length:** 105 amino acids  
* **Primary UniProt Accession:** `P00004`  
* **Biological Function:** Essential electron transport hemoprotein localized to the mitochondrial intermembrane space; transfers single electrons between Complex III (cytochrome $c$ reductase) and Complex IV (cytochrome $c$ oxidase); key trigger of intrinsic apoptosis upon cytosolic release.  
* **Key Active Sites & Domains:**
  - Cytochrome c family heme-binding signature: `C-x(2)-C-H` (Cys14-Ala15-Gln16-Cys17-His18)
  - Heme c covalent thioether linkages: Cys14 and Cys17
  - Axial Iron Ligands: **His18** and **Met80**
* **Expected BLAST Top Hit:** `P00004.2` Cytochrome c [*Equus caballus*], 100% identity, $E \approx 3 \times 10^{-70}$, bit score $>200$.  
* **Physicochemical Properties:** MW $\approx 11.75\text{ kDa}$, theoretical pI $\approx 9.5\text{--}9.8$ (highly basic), GRAVY $\approx -0.56$ (soluble), Instability Index $\approx 22$ (exceptionally stable).  
* **Secondary Structure & Fold:** All-alpha class; ~40% alpha-helix, ~0% beta-sheet, ~60% turns/loops encapsulating the covalently attached heme.  
* **Representative PDB Structure:** `1HRC` (X-ray, $1.90\text{ \AA}$) or `2CYP`.

---

### Sequence 06: `unknown_seq_06`
* **Organism:** *Homo sapiens* (Human)  
* **Gene Symbol:** *TP53*  
* **Protein Name:** Cellular tumor antigen p53 (Tumor suppressor p53)  
* **Length:** 393 amino acids  
* **Primary UniProt Accession:** `P04637`  
* **Biological Function:** "Guardian of the genome"; sequence-specific transcription factor that responds to cellular stress and DNA damage by arresting cell cycle at G1/S or activating apoptotic pathways. Mutated in $>50\%$ of human cancers.  
* **Key Active Sites & Domains:**
  - N-terminal transactivation domain: Residues 1–61
  - Proline-rich regulatory domain: Residues 63–97
  - DNA-binding core domain (Pfam: `PF00870`): Residues 102–292
  - $Zn^{2+}$ coordination center: Cys176, His179, Cys238, Cys242
  - Oncogenic mutation hotspots: Arg175, Gly245, Arg248, Arg249, Arg273, Arg282
  - C-terminal tetramerization domain: Residues 325–356
* **Expected BLAST Top Hit:** `NP_000537.3` / `P04637.4` cellular tumor antigen p53 [*Homo sapiens*], 100% identity, $E \approx 0.0$, bit score $>780$.  
* **Physicochemical Properties:** MW $\approx 43.65\text{ kDa}$, theoretical pI $\approx 6.3$, GRAVY $\approx -0.66$ (hydrophilic, intrinsically disordered terminal domains), Instability Index $\approx 62$ (highly regulated, rapid turnover).  
* **Secondary Structure & Fold:** Core DNA-binding domain is $\beta$-sandwich with loop-sheet-helix motif (PDB `1TUP`); N- and C-termini are intrinsically disordered.  
* **Representative PDB Structure:** `1TUP` (p53 core domain bound to DNA, $2.20\text{ \AA}$) or `1OLG` (tetramerization domain).

---

### Sequence 07: `unknown_seq_07`
* **Organism:** *Homo sapiens* (Human) / *Mus musculus* / *Eukaryota*  
* **Gene Symbol:** *UBB* / *UBC* / *RPS27A*  
* **Protein Name:** Ubiquitin  
* **Length:** 76 amino acids  
* **Primary UniProt Accession:** `P0CG48` (Human) / `P62988`  
* **Biological Function:** Highly conserved eukaryotic regulatory polypeptide covalently tagged to target proteins via isopeptide bonds to direct 26S proteasomal degradation, endocytosis, or DNA repair signaling.  
* **Key Active Sites & Domains:**
  - Ubiquitin fold ($\beta$-grasp fold, Pfam: `PF00240`)
  - C-terminal diglycine motif: **Gly75-Gly76** (covalently attaches to lysine $\epsilon$-amino groups of target substrates)
  - Critical lysine polyubiquitination sites: **Lys48** (canonical proteasomal degradation signal) and **Lys63** (DNA repair and trafficking signal)
  - Hydrophobic patch: Leu8, Ile44, Val70 (mediates proteasome receptor recognition)
* **Expected BLAST Top Hit:** `NP_001268650.1` / `P0CG48.1` ubiquitin [*Homo sapiens*], 100% identity, $E \approx 4 \times 10^{-52}$, bit score $>160$.  
* **Physicochemical Properties:** MW $\approx 8.56\text{ kDa}$, theoretical pI $\approx 6.56$, GRAVY $\approx -0.15$, Instability Index $\approx 31$ (highly stable).  
* **Secondary Structure & Fold:** $\beta$-grasp fold (Mixed $\alpha+\beta$); 5-stranded mixed $\beta$-sheet wrapping around a central $\alpha$-helix.  
* **Representative PDB Structure:** `1UBQ` (X-ray, $1.80\text{ \AA}$) or `1D3Z` (NMR).

---

### Sequence 08: `unknown_seq_08`
* **Organism:** *Bos taurus* (Bovine / Cattle)  
* **Gene Symbol:** *CTRL* / *CTRA*  
* **Protein Name:** Chymotrypsinogen A  
* **Length:** 245 amino acids  
* **Primary UniProt Accession:** `P00766`  
* **Biological Function:** Digestive serine protease zymogen secreted by pancreas; activated in duodenum by trypsin cleavage (releasing active $\alpha$-chymotrypsin) to hydrolyze dietary protein peptide bonds adjacent to bulky hydrophobic aromatic residues (Phe, Tyr, Trp).  
* **Key Active Sites & Domains:**
  - Trypsin/Chymotrypsin serine protease domain (Pfam: `PF00089`)
  - Catalytic Triad: **His57**, **Asp102**, and **Ser195**
  - Oxyanion Hole: Backbone amides of Gly193 and Ser195
  - Primary specificity pocket ($S_1$ pocket): Hydrophobic cleft lined by Ser189, Met192, Gly216, and Gly226
  - 5 Disulfide Bridges: Cys1-Cys122, Cys42-Cys58, Cys136-Cys201, Cys168-Cys182, Cys191-Cys220
* **Expected BLAST Top Hit:** `P00766.2` Chymotrypsinogen A [*Bos taurus*], 100% identity, $E \approx 2 \times 10^{-176}$, bit score $>480$.  
* **Physicochemical Properties:** MW $\approx 25.66\text{ kDa}$, theoretical pI $\approx 8.7\text{--}9.1$, GRAVY $\approx -0.05$, Instability Index $\approx 29$ (stable).  
* **Secondary Structure & Fold:** All-beta fold class; dual Greek-key $\beta$-barrel domains (~5% alpha-helix, ~45% beta-sheet, ~50% coil).  
* **Representative PDB Structure:** `2CGA` ($1.80\text{ \AA}$) or active `4CHA` ($1.68\text{ \AA}$).

---

### Sequence 09: `unknown_seq_09`
* **Organism:** *Aequorea victoria* (Jellyfish)  
* **Gene Symbol:** *GFP*  
* **Protein Name:** Green fluorescent protein  
* **Length:** 238 amino acids  
* **Primary UniProt Accession:** `P42212`  
* **Biological Function:** Bioluminescent energy transfer partner to aequorin; absorbs blue light ($395\text{ nm}$) and emits green light ($509\text{ nm}$). Extensively used as a molecular fluorescent reporter and fusion tag in cell biology.  
* **Key Active Sites & Domains:**
  - Green fluorescent protein domain (Pfam: `PF01353`)
  - Autocatalytic Fluorophore: Formed spontaneously in the presence of $O_2$ by post-translational cyclization and oxidation of the tripeptide **Ser65 - Tyr66 - Gly67** into 4-(p-hydroxybenzylidene)-imidazolidin-5-one
* **Expected BLAST Top Hit:** `P42212.1` Green fluorescent protein [*Aequorea victoria*], 100% identity, $E \approx 2 \times 10^{-174}$, bit score $>470$.  
* **Physicochemical Properties:** MW $\approx 26.89\text{ kDa}$, theoretical pI $\approx 5.67$, GRAVY $\approx -0.40$ (soluble), Instability Index $\approx 37$ (stable).  
* **Secondary Structure & Fold:** All-beta class; canonical 11-stranded $\beta$-can / $\beta$-barrel fold ($11\times \beta$-strands surrounding a central axial alpha-helix containing the fluorophore).  
* **Representative PDB Structure:** `1EMA` ($1.90\text{ \AA}$) or `1GFL` ($1.90\text{ \AA}$).

---

### Sequence 10: `unknown_seq_10`
* **Organism:** *Homo sapiens* (Human)  
* **Gene Symbol:** *AQP1*  
* **Protein Name:** Aquaporin-1 (Water channel protein)  
* **Length:** 269 amino acids  
* **Primary UniProt Accession:** `P29972`  
* **Biological Function:** Integral membrane tetrameric water channel; mediates rapid, passive, bidirectional osmotic water transport across cell membranes (erythrocytes and renal proximal tubules) while strictly excluding protons ($H_3O^+$) and small ions. Peter Agre, Nobel Prize 2003.  
* **Key Active Sites & Domains:**
  - Major Intrinsic Protein (MIP) / Aquaporin family (Pfam: `PF00230`)
  - Six Transmembrane Alpha-Helices ($TM1\text{--}TM6$)
  - Dual conserved **NPA motifs**:
    - Loop B: Asn76 - Pro77 - Ala78
    - Loop E: Asn192 - Pro193 - Ala194
    *(The two NPA motifs dip into the membrane center from opposite sides, forming the selective water pore and reorienting water dipoles to prevent proton jumping).*
  - Aromatic/Arginine (ar/R) selectivity filter: Phe56, His180, Cys189, Arg195 (mercury sensitivity site at Cys189)
* **Expected BLAST Top Hit:** `NP_000376.1` / `P29972.1` aquaporin-1 [*Homo sapiens*], 100% identity, $E \approx 0.0$, bit score $>530$.  
* **Physicochemical Properties:** MW $\approx 28.52\text{ kDa}$, theoretical pI $\approx 8.78$, GRAVY $\approx \mathbf{+0.55}$ (**strongly hydrophobic integral membrane protein**), Instability Index $\approx 34$.  
* **Secondary Structure & Fold:** Membrane all-alpha class; ~55% alpha-helix (6 full TM helices + 2 half-helices), ~0% beta-sheet, ~45% loops/coils.  
* **Representative PDB Structure:** `1J4N` (X-ray, $2.20\text{ \AA}$) or `1FQY` ($3.8\text{ \AA}$).
