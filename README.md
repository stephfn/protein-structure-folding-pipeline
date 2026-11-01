# 🧬 Structural Bioinformatics Analysis of the p53 DNA-Binding Domain

[![Render with nbviewer](https://img.shields.io/badge/render-nbviewer-orange?logo=jupyter)](https://nbviewer.org/github/stephfn/protein-structure-folding-pipeline/blob/main/01_sequence_to_3d_structure.ipynb)
[![Python](https://img.shields.io/badge/Python-3-blue.svg)](https://www.python.org/)
[![Biopython](https://img.shields.io/badge/Biopython-green.svg)](https://biopython.org/)

> **Viewing note:** GitHub's notebook preview does not execute interactive JavaScript visualizations. The notebook can be run locally in JupyterLab to explore the interactive 3D molecular structure. Static figures are provided below.

## 📌 Project Overview

This project uses Python and Biopython to investigate the structural and biophysical properties of the human p53 DNA-binding domain using an experimentally determined structure from the Protein Data Bank (PDB ID: `1TUP`).

The workflow retrieves and parses protein structural data, extracts amino acid sequences, calculates pairwise residue distances, evaluates nonlocal spatial contacts, and generates sequence-based biophysical profiles.

The analysis focuses on chain A, containing 196 extracted amino acids. Rather than predicting a protein structure from sequence, the project characterizes an existing experimental structure and explores relationships between amino acid sequence properties and three-dimensional spatial organization.

## 🔬 Analysis Modules and Visualizations

### 1. PDB Structure Retrieval and 3D Visualization

- Retrieves the experimentally determined p53–DNA complex using Biopython's `PDBList`.
- Parses structural coordinates and extracts protein sequences from the available chains.
- Uses `py3Dmol` to provide an interactive molecular visualization.
- Selects chain A for subsequent structural calculations.

### 2. Residue–Residue Distance Matrix

The workflow extracts Cα atomic coordinates from 196 residues in chain A and calculates pairwise Euclidean distances.

The resulting 196 × 196 distance matrix illustrates spatial relationships between residues within the p53 DNA-binding domain.

The zero-distance diagonal represents residues compared with themselves. Off-diagonal regions with relatively short distances may indicate contacts between residues that are separated along the primary sequence.

The visualization is a continuous distance map rather than a binary contact map.

![p53 Residue Distance Matrix](p53_distance_matrix.png)

### 3. Sequence-Based Biophysical Profiling

Biopython's `ProteinAnalysis` is used to calculate properties of the extracted chain A amino acid sequence.

**Results:**

- Sequence length: 196 amino acids
- Estimated molecular weight: 22.00 kDa
- Theoretical isoelectric point: 8.34

A nine-residue sliding window applies the Kyte–Doolittle hydrophobicity scale to examine variation in hydrophobic character along the sequence.

Positive hydrophobicity scores indicate relatively hydrophobic regions, while negative scores indicate more hydrophilic regions. These values do not independently determine whether residues are buried or solvent-exposed.

![p53 Hydrophobicity Profile](p53_hydrophobicity_profile.png)

### 4. Nonlocal Spatial Contact Analysis

An 8 Å Cα distance threshold is applied to identify spatially neighboring residues.

To reduce the influence of immediate sequence neighbors, residue pairs separated by three or fewer sequence positions are excluded.

**Results:**

- Mean nonlocal contacts per residue: **5.09**
- Highest observed nonlocal contact count: **13**
- Position with the highest count: **42** in the extracted sequence

The analysis highlights variation in nonlocal contact density across the domain. These contact counts provide a measure of spatial organization under the selected thresholds but do not independently establish solvent accessibility, flexibility, or biological function.

![p53 Nonlocal Contact Profile](p53_coordination_profile.png)

### 5. Sequence-Based Secondary-Structure Propensity

Biopython's `ProteinAnalysis.secondary_structure_fraction()` estimates secondary-structure propensity from amino acid composition.

| Sequence-based category | Estimated percentage |
|---|---:|
| Beta-sheet propensity | 32.1% |
| Alpha-helix propensity | 21.9% |
| Turn propensity | 32.1% |
| Remaining fraction | 13.8% |

These values are sequence-derived estimates, not secondary-structure assignments obtained from the experimental PDB coordinates.

The remaining fraction is calculated arithmetically and should not be interpreted as an experimentally measured disordered or coil region.

![p53 Secondary-Structure Propensity](p53_secondary_structure_composition.png)

## 🛠️ Repository Structure

```text
protein-structure-folding-pipeline/
├── 01_sequence_to_3d_structure.ipynb
├── pdb1tup.ent
├── p53_distance_matrix.png
├── p53_hydrophobicity_profile.png
├── p53_coordination_profile.png
├── p53_secondary_structure_composition.png
├── .gitignore
└── README.md
```

## 💻 Tools and Libraries

- Python
- Biopython
- NumPy
- Pandas
- Matplotlib
- Seaborn
- py3Dmol
- JupyterLab

## ▶️ Reproducing the Analysis

1. Clone the repository.
2. Install the Python libraries listed above.
3. Open `01_sequence_to_3d_structure.ipynb` in JupyterLab.
4. Run the notebook cells sequentially.

The notebook retrieves PDB entry `1TUP` from the Protein Data Bank, so an internet connection may be required during structure retrieval. A copy of the PDB file is also included in the repository.

The notebook generates the four static visualizations shown in this README.

## 🧬 Biological Context and Interpretation

The p53 tumor suppressor plays an important role in cellular responses to DNA damage and other forms of stress. Its DNA-binding domain contributes to recognition of regulatory DNA sequences.

PDB entry `1TUP` provides experimentally determined structural information about p53 in complex with DNA.

This project demonstrates how computational methods can characterize a protein domain using both sequence information and experimentally derived atomic coordinates.

The distance matrix and nonlocal contact analysis examine spatial organization, while hydrophobicity and secondary-structure propensity calculations provide complementary sequence-based descriptors.

These approaches are useful for exploratory structural bioinformatics, but they answer different questions and should not be treated as interchangeable measurements.

## ⚠️ Limitations

- The analysis focuses on one extracted p53 chain from a single experimental PDB structure rather than full-length p53.
- Distance and contact calculations use Cα coordinates rather than all-atom interactions.
- Contact counts depend on the 8 Å cutoff and the exclusion of nearby sequence positions.
- Hydrophobicity does not directly establish solvent accessibility.
- Secondary-structure propensity is estimated from amino acid composition rather than assigned from PDB coordinates.
- No new protein fold is predicted, and no protein variants are experimentally evaluated.

## 🔭 Future Improvements

Potential extensions include structure-based secondary-structure assignment using DSSP, solvent-accessible surface area calculations, comparison of wild-type and mutant p53 structures, and investigation of residue contacts across the p53–DNA interface.

## Conclusion

This project demonstrates a reproducible Python workflow for retrieving and analyzing experimentally determined protein structural data.

By combining sequence-based biophysical characterization with Cα distance calculations and nonlocal contact analysis, the notebook provides an exploratory view of the p53 DNA-binding domain while distinguishing measured structural coordinates from sequence-derived estimates.

The project establishes a foundation for further work in structural bioinformatics and computational protein analysis.
