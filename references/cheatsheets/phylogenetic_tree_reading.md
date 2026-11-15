# Quick Reference: Phylogenetic Tree Reading & Interpretation

A phylogenetic tree is a graphical hypothesis of evolutionary relationships between taxa, genes, or species.

---

## 1. Anatomy of a Tree

```text
               Internal Node (Speciation or Duplication)
                   ┌────────── Human HBB (Terminal Node / Taxon / Leaf)
         Root ─────┤
                   │    ┌───── Human HBD
                   └────┤
                        └───── Human HBA1
```

- **Root:** The common ancestor of all operational taxonomic units (OTUs) in the tree.
- **Node:** A point of divergence representing a shared ancestral lineage.
- **Branch:** Line connecting two nodes. In phylograms, branch length is proportional to estimated evolutionary distance (substitutions per site). In cladograms, branch length is arbitrary.
- **Clade (Monophyletic Group):** An ancestor and *all* of its descendants.

---

## 2. Orthology vs. Paralogy

| Concept | Event | Example in Globin Family | Functional Implication |
|---|---|---|---|
| **Orthologues** | Speciation event | Human HBB vs. Mouse HBB | Typically retain identical biological function across species |
| **Paralogues** | Gene duplication event | Human HBA1 vs. Human HBB vs. Human MB | Free to diverge, undergo subfunctionalization or neofunctionalization |
| **Xenologues** | Horizontal gene transfer | Bacterial gene acquired by fungal genome | Phylogeny conflicts with organismal species tree |

---

## 3. Tree Building Methods

| Method | Type | Principle | Advantages / Limitations |
|---|---|---|---|
| **UPGMA** | Distance-based | Assumes a strict molecular clock (ultrametric tree) | Fast, works by hand on 4 taxa; distorted when evolutionary rates vary |
| **Neighbor-Joining (NJ)** | Distance-based | Finds minimum total branch length, allows variable rates | Fast, accurate for moderate sequence divergence; does not assume molecular clock |
| **Maximum Parsimony (MP)** | Character-based | Chooses tree requiring fewest evolutionary changes | Intuitive, but prone to long-branch attraction artifacts |
| **Maximum Likelihood (ML)** | Probabilistic | Finds tree maximizing probability of observed alignment given a substitution model | Most statistically rigorous, computationally intensive |

---

## 4. Reading Bootstrap Values
- **Bootstrap Support (e.g. 95%):** Out of 100 or 1,000 resampled pseudo-replicate alignment matrices, the clade was recovered in 95% of the resulting trees.
- **Interpretation:**
  - $\ge 85\%$: Strong statistical support for the clade.
  - $70\% - 84\%$: Moderate support.
  - $< 70\%$: Unresolved branching order / low confidence.
  - *Caution:* A high bootstrap value does **not** prove a tree is objectively true if the underlying evolutionary model or alignment is flawed.
