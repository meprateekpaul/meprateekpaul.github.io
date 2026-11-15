# Pre-Screened Gene Families for Mini-Project Allocation

**Course Code:** CBBI-501 (Concepts of Bioinformatics)  
**Programme:** B.Tech. Bioinformatics, Semester II  

The following 12 gene families have been pre-screened to ensure high sequence quality across diverse taxonomic clades, well-annotated active site motifs in PROSITE/Pfam, and high-resolution experimental 3D structures in the RCSB PDB. Each group must choose (or be assigned) one family.

---

### 1. The Globin Superfamily (Oxygen Binding & Transport)
* **Biological Context:** Heme-containing metalloproteins responsible for reversible oxygen transport and storage; classic model for gene duplication, allostery, and molecular evolution.
* **Core Human Reference:** *HBB* (Hemoglobin subunit beta, UniProt: `P68871`, RefSeq: `NP_000509.1`).
* **Secondary / Paralogous Members:** *HBA1* ($\alpha$-globin), *MB* (myoglobin), *CYGB* (cytoglobin), *NGB* (neuroglobin).
* **Reference 3D Structure:** PDB `1A3N` (deoxyhemoglobin, $1.80\text{ \AA}$) or `1WLA` (myoglobin).
* **Key Evolutionary Challenge:** Identify the ancestral gene duplication giving rise to myoglobin and hemoglobin, and trace the invariant proximal (F8) and distal (E7) histidine residues.

---

### 2. The Insulin / IGF Superfamily (Endocrine Metabolic Regulators)
* **Biological Context:** Ancient peptide hormones controlling carbohydrate metabolism, cell growth, and lifespan from nematodes to mammals.
* **Core Human Reference:** *INS* (Preproinsulin, UniProt: `P01308`, RefSeq: `NP_000198.1`).
* **Secondary / Paralogous Members:** *IGF1* (Insulin-like growth factor 1), *IGF2*, *RLN1* (Relaxin).
* **Reference 3D Structure:** PDB `4INS` (mature insulin hexamer) or `1GZR` (IGF-1).
* **Key Evolutionary Challenge:** Map the differential conservation of the functional A and B chains vs the hypervariable intervening C-peptide, and trace the 3 invariant disulfide bridges.

---

### 3. Serpins (Serine Protease Inhibitors)
* **Biological Context:** Structurally conserved suicide substrate inhibitors that undergo massive conformational rearrangements to inhibit target proteases (coagulation, inflammation).
* **Core Human Reference:** *SERPINA1* ($\alpha_1$-antitrypsin, UniProt: `P01009`, RefSeq: `NP_000286.3`).
* **Secondary / Paralogous Members:** *SERPINC1* (Antithrombin-III), *SERPINE1* (PAI-1), *SERPINB9*.
* **Reference 3D Structure:** PDB `1QLP` (native active conformation) or `1EZX`.
* **Key Evolutionary Challenge:** Locate the hypervariable Reactive Center Loop (RCL) that dictates protease specificity and evaluate the "stressed-to-relaxed" (S-to-R) transition mechanism.

---

### 4. Cytochrome P450 Monooxygenases (Drug & Xenobiotic Metabolism)
* **Biological Context:** Vast heme-thiolate enzyme superfamily responsible for Phase I oxidative metabolism of pharmaceuticals, steroids, and environmental toxins.
* **Core Human Reference:** *CYP3A4* (UniProt: `P08684`, RefSeq: `NP_000768.1`) or *CYP2D6* (`P10635`).
* **Secondary / Paralogous Members:** *CYP1A2*, *CYP2C9*, *CYP2E1*.
* **Reference 3D Structure:** PDB `1TQN` (CYP3A4, $2.05\text{ \AA}$) or `2F9Q` (CYP2D6).
* **Key Evolutionary Challenge:** Locate the universally conserved signature motif `F-x-x-G-x-R-x-C-x-G` containing the cysteine thiolate axial ligand coordinated to the heme iron.

---

### 5. Rhodopsins / Class A GPCRs (Visual & Sensory Transduction)
* **Biological Context:** 7-transmembrane G-protein coupled receptors responsible for light perception (rhodopsin) and hormonal transmembrane signaling.
* **Core Human Reference:** *RHO* (Rhodopsin, UniProt: `P08100`, RefSeq: `NP_000530.1`).
* **Secondary / Paralogous Members:** *OPN1MW* (Green opsin), *OPN1SW* (Blue opsin), *ADRB2* ($\beta_2$-adrenergic receptor).
* **Reference 3D Structure:** PDB `1F88` (bovine rhodopsin, $2.80\text{ \AA}$) or `2X72`.
* **Key Evolutionary Challenge:** Map the 7 hydrophobic transmembrane alpha-helices, the conserved `D/ERY` signaling motif in TM3, and the retinal-binding Lys296 Schiff base in TM7.

---

### 6. Ras Small GTPases (Intracellular Signaling Switches)
* **Biological Context:** Binary molecular switches cycling between GDP-bound (inactive) and GTP-bound (active) states, relaying growth factor signals; heavily mutated in oncology.
* **Core Human Reference:** *KRAS* (K-Ras GTPase, UniProt: `P01116`, RefSeq: `NP_004976.2`).
* **Secondary / Paralogous Members:** *HRAS*, *NRAS*, *RHOA*, *RAB5A*.
* **Reference 3D Structure:** PDB `4OBE` (K-Ras G12D) or `121P` (H-Ras, $1.54\text{ \AA}$).
* **Key Evolutionary Challenge:** Identify the conserved Switch I and Switch II loops, the G-box nucleotide-binding motifs (`G-x(4)-G-K-S/T`), and oncogenic mutation positions (Gly12, Gln61).

---

### 7. Cyclin-Dependent Kinases (Cell Cycle Regulation)
* **Biological Context:** Serine/threonine protein kinases that orchestrate eukaryotic cell cycle progression upon binding regulatory cyclin subunits.
* **Core Human Reference:** *CDK2* (Cyclin-dependent kinase 2, UniProt: `P24941`, RefSeq: `NP_001789.2`).
* **Secondary / Paralogous Members:** *CDK1*, *CDK4*, *CDK6*, *MAPK1* (ERK2).
* **Reference 3D Structure:** PDB `1HCL` (CDK2 monomer, $1.90\text{ \AA}$) or `1FIN` (CDK2-Cyclin A complex).
* **Key Evolutionary Challenge:** Align the canonical kinase catalytic core, locating the ATP-binding Lys33, the catalytic Asp145 in the `DFG` motif, and the activation loop Thr160 phosphorylation site.

---

### 8. C2H2 Zinc Finger Transcription Factors (DNA Binding)
* **Biological Context:** Classical sequence-specific DNA-binding modules coordinating a structural zinc ion; involved in transcriptional development and chromatin remodeling.
* **Core Human Reference:** *EGR1* (Early growth response protein 1 / Zif268, UniProt: `P18146`, RefSeq: `NP_001955.1`).
* **Secondary / Paralogous Members:** *SP1*, *WT1*, *YY1*.
* **Reference 3D Structure:** PDB `1ZAA` (Zif268 bound to DNA, $1.60\text{ \AA}$) or `2DRP`.
* **Key Evolutionary Challenge:** Delineate the tandem repeat units containing the invariant consensus `C-x(2,4)-C-x(12)-H-x(3)-H` and map base-specifying residues (-1, +2, +3, +6 of the recognition helix).

---

### 9. Chemokines (Leukocyte Chemotaxis & Immune Trafficking)
* **Biological Context:** Small chemotactic cytokines (8–10 kDa) directing immune cell recruitment during inflammation and infection; classified into CC, CXC, CX3C, and C subfamilies.
* **Core Human Reference:** *CXCL8* (Interleukin-8, UniProt: `P10145`, RefSeq: `NP_000575.1`).
* **Secondary / Paralogous Members:** *CCL2* (MCP-1), *CCL5* (RANTES), *CXCL12* (SDF-1).
* **Reference 3D Structure:** PDB `1IL8` (IL-8 dimer, $2.00\text{ \AA}$) or `1DOM`.
* **Key Evolutionary Challenge:** Contrast the cysteinyl motif patterns of CXC (one intervening residue) versus CC (adjacent cysteines), and trace their distinct receptor-binding loop conformations.

---

### 10. Aquaporins (Membrane Water & Glycerol Channels)
* **Biological Context:** Integral membrane channel tetramers facilitating selective, bidirectional water or neutral solute transport across cell membranes.
* **Core Human Reference:** *AQP1* (Aquaporin-1, UniProt: `P29972`, RefSeq: `NP_000376.1`).
* **Secondary / Paralogous Members:** *AQP4* (brain water channel), *AQP9* (aquaglyceroporin).
* **Reference 3D Structure:** PDB `1J4N` (AQP1, $2.20\text{ \AA}$) or `1FQY`.
* **Key Evolutionary Challenge:** Trace the dual internal `N-P-A` (Asn-Pro-Ala) motifs that form the central constriction pore and the aromatic/arginine (ar/R) selectivity filter.

---

### 11. Heat Shock Protein 70 (Hsp70 Chaperone Family)
* **Biological Context:** Ubiquitous ATP-dependent molecular chaperones preventing protein aggregation, assisting de novo folding, and driving translocation across membranes.
* **Core Human Reference:** *HSPA1A* (Hsp70-1A, UniProt: `P0DMV8` / `P08107`, RefSeq: `NP_005336.3`).
* **Secondary / Paralogous Members:** *HSPA5* (BiP / GRP78), *HSPA8* (Hsc70), *DnaK* (bacterial orthologue).
* **Reference 3D Structure:** PDB `1HJO` (ATPase domain) or `2KHO` (intact full-length DnaK chaperone).
* **Key Evolutionary Challenge:** Contrast the highly conserved 44 kDa N-terminal nucleotide-binding domain (NBD) with the more divergent 28 kDa C-terminal substrate-binding domain (SBD).

---

### 12. Tubulins (Cytoskeletal Microtubule Subunits)
* **Biological Context:** Globular heterodimeric proteins ($\alpha$- and $\beta$-tubulin) that polymerize into hollow cylindrical microtubules essential for mitosis, intracellular transport, and ciliary motility.
* **Core Human Reference:** *TUBA1A* ($\alpha$-tubulin 1A, UniProt: `Q71U36`, RefSeq: `NP_006000.2`).
* **Secondary / Paralogous Members:** *TUBB* ($\beta$-tubulin), *TUBG1* ($\gamma$-tubulin centrosomal nucleator).
* **Reference 3D Structure:** PDB `1JFF` (bovine tubulin dimer, $3.50\text{ \AA}$) or `5JCO` (cryo-EM, $3.30\text{ \AA}$).
* **Key Evolutionary Challenge:** Identify the ancestral gene duplication separating $\alpha$- and $\beta$-tubulin and locate the invariant GTP-binding pocket at the intradimer interface.
