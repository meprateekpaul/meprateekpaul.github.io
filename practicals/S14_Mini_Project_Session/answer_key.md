# Instructor Answer Key & Master Benchmark: Practical 14 (Mini-Project)

**Course Code:** CBBI-501 / CBBI-502  
**Session:** S14 (Mini-Project Master Solution & Evaluation Manual)  
**Standard Exemplar Family:** The Globin Family (*Homo sapiens* & Vertebrates)  

---

## 1. Master Benchmark Dataset (The Globin Family)

This benchmark provides the complete instructor gold standard against which student pipeline executions and final reports are evaluated.

### Table 14.1: Master Dataset — Human Globin Family Paralogues
| Gene Symbol | Full Protein Name | Organism | NCBI Gene ID | RefSeq mRNA | RefSeq Protein | UniProt ID | PDB Code |
|---|---|---|:---:|:---:|:---:|:---:|:---:|
| **HBB** | Hemoglobin subunit beta | *Homo sapiens* | 3043 | NM_000518.5 | NP_000509.1 | P68871 | 1A3N, 4HHB |
| **HBD** | Hemoglobin subunit delta | *Homo sapiens* | 3045 | NM_000519.4 | NP_000510.1 | P02042 | 1HBD |
| **HBG1** | Hemoglobin subunit gamma-1 | *Homo sapiens* | 3047 | NM_000559.3 | NP_000550.2 | P69891 | 1FDH |
| **HBG2** | Hemoglobin subunit gamma-2 | *Homo sapiens* | 3048 | NM_000184.3 | NP_000175.1 | P69892 | 1FDH |
| **HBE1** | Hemoglobin subunit epsilon-1 | *Homo sapiens* | 3046 | NM_005330.4 | NP_005321.1 | P02100 | 1E8W |
| **HBA1** | Hemoglobin subunit alpha-1 | *Homo sapiens* | 3039 | NM_000558.5 | NP_000508.1 | P69905 | 1A3N, 4HHB |
| **HBZ** | Hemoglobin subunit zeta | *Homo sapiens* | 3050 | NM_005332.3 | NP_005323.2 | P02008 | 1B86 |
| **MB** | Myoglobin | *Homo sapiens* | 4151 | NM_005368.3 | NP_005359.1 | P02144 | 1MBO |
| **NGB** | Neuroglobin | *Homo sapiens* | 58157 | NM_021257.4 | NP_067080.1 | Q9NPG2 | 1OJ6 |
| **CYGB** | Cytoglobin | *Homo sapiens* | 114757 | NM_134268.5 | NP_599030.1 | Q8WWM9 | 1V5H |

---

## 2. Expected Alignment Motifs & Invariant Landmark Columns

In the master Clustal Omega alignment of the 10 human globins, the following landmark positions are expected to be identified:

1. **The CD1 Phenylalanine (Phe-43 in HBB):** Invariant across all 10 globins (`*`). Wedges the porphyrin ring into the hydrophobic core.
2. **The Distal Histidine (His-64 / His-E7 in HBB):** Conserved in HBB, HBD, HBG, HBA, MB, NGB, and CYGB. Stabilizes bound oxygen via hydrogen bonding.
3. **The Proximal Histidine (His-93 / His-F8 in HBB):** 100% strictly invariant across all 10 sequences without exception (`*`). Forms the covalent coordination bond with the $Fe^{2+}$ ion.
4. **The FG Corner α1β2 Interface Residues:** Asp-99 and Tyr-145 in HBB, essential for allosteric salt bridges during the T-to-R transition.

---

## 3. Phylogenetic Reconstruction Topology

### Expected Neighbor-Joining Tree Topology
```
           +-------------------------------- NGB (Neuroglobin) - Outgroup
           |
      (D1) +-------------------------------- CYGB (Cytoglobin)
           |
           |                        +------- MB (Myoglobin)
           |                   (D2) |
           +------------------------+  (D3) +--- HBA1 (Alpha-globin)
                                    +---+---|
                                            |   (D4) +--- HBG1 (Gamma-1)
                                            +---+----+--- HBG2 (Gamma-2)
                                                |
                                                |   (D5) +--- HBD (Delta)
                                                +---+----+--- HBB (Beta)
```

### Evolutionary Events to be Identified:
- **Duplication Node D1 (~600–700 Mya):** Divergence of ancestral neural/intracellular globins (NGB, CYGB) from respiratory blood globins.
- **Duplication Node D2 (~500 Mya):** Divergence of monomeric muscle oxygen storage (Myoglobin) from circulating blood hemoglobin subunits.
- **Duplication Node D3 (~450 Mya, Whole Genome Duplication in early gnathostomes):** Duplication giving rise to the distinct $\alpha$-cluster (Chromosome 16) and $\beta$-cluster (Chromosome 11).
- **Duplication Node D4 & D5 (<100 Mya, Mammalian / Primate Specific):** Tandem gene duplications generating fetal ($\gamma$) and adult ($\delta, \beta$) chains, facilitating maternal-fetal oxygen transfer in placental mammals.

---

## 4. Master Comparative Physicochemical Profile (ProtParam)

| Protein | Residues | Molecular Weight ($M_r$) | Theoretical $pI$ | Net Charge at pH 7.0 | Instability Index ($II$) | Aliphatic Index | GRAVY Score |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **HBB** | 147 | 15,998.18 | 6.75 | -0.1 | 33.74 (Stable) | 91.09 | -0.111 |
| **HBD** | 147 | 16,054.26 | 7.91 | +1.9 | 32.88 (Stable) | 91.09 | -0.118 |
| **HBG1** | 147 | 16,140.35 | 6.71 | -0.2 | 31.25 (Stable) | 88.44 | -0.118 |
| **HBA1** | 142 | 15,257.42 | 8.73 | +2.8 | 32.14 (Stable) | 103.38 | +0.106 |
| **MB** | 154 | 17,183.74 | 7.36 | +0.8 | 26.69 (Stable) | 87.08 | -0.386 |
| **NGB** | 151 | 16,933.24 | 5.30 | -5.2 | 41.52 (Borderline) | 90.73 | -0.158 |
| **CYGB** | 190 | 21,399.70 | 6.18 | -2.1 | 48.74 (Unstable) | 80.16 | -0.428 |

---

## 5. Master 3D Structural Coordination Parameters (`1A3N`)

- **Method & Resolution:** X-ray crystallography, 2.00 $\text{\AA}$ resolution.
- **Quaternary Structure:** Heterotetramer ($\alpha_2\beta_2$).
- **Proximal Coordination Distance:** Fe to His-87 NE2 ($\alpha$) = **2.10 $\text{\AA}$**; Fe to His-92 NE2 ($\beta$) = **2.09 $\text{\AA}$**.
- **Distal Open Space Distance:** Fe to His-58 NE2 ($\alpha$) = **4.12 $\text{\AA}$**; Fe to His-63 NE2 ($\beta$) = **3.98 $\text{\AA}$**.
- **Heme Pocket Hydrophobic Packing Residues:** Phe-42, Phe-43, Leu-88, Val-62, Leu-91.

---

## 6. Comprehensive Grading Rubric & Penalty Guide (100 Marks)

| Category | Component | Full Marks | Deductions / Penalties |
|---|---|:---:|---|
| **In-Lab Execution (20%)** | 6 Milestone Sign-offs | 20 | Deduct 3 marks per missed or unverified milestone during lab session. |
| **Data & Search (15%)** | Curated Accession Table | 8 | Deduct 1 mark per missing or erroneous accession/Gene ID. |
| | BLAST & FASTA Comparison | 7 | Deduct 2 marks if scoring matrix impact (BLOSUM62 vs BLOSUM45) is omitted. |
| **Alignment & Trees (20%)** | MSA Curation & Jalview | 10 | Deduct 3 marks if invariant functional residues (His-F8, CD1) are not mapped. |
| | Phylogenetic Tree | 10 | Deduct 4 marks if tree is unrooted or duplication vs speciation nodes are confused. |
| **Physicochemical (15%)** | ProtParam Profile Matrix | 8 | Deduct 2 marks for incorrect pI or missing GRAVY interpretations. |
| | Secondary Structure & $Q_3$ | 7 | Deduct 2 marks for computational math errors in $Q_3$ accuracy. |
| **3D Structure (15%)** | Quaternary Render (Fig A) | 7 | Deduct 2 marks for poor perspective, clipping, or missing chain color coding. |
| | Pocket Geometry Render (Fig B) | 8 | Deduct 3 marks if iron coordination distances are not explicitly labeled. |
| **Synthesis & Polish (15%)** | Biological Discussion | 10 | Deduct 3 marks for superficial answers lacking mechanistic evolutionary depth. |
| | Formatting & Length Rules | 5 | **Strict Penalty:** Deduct 5 marks immediately if report exceeds 4 pages! |
| **Total** | | **100** | Scaled to 10% of course grade. |
