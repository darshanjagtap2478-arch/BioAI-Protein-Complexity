# Balanced Four-Group Evaluation of Length- and Complexity-Associated Prediction Patterns in Sequence-Based Protein Function Predictors

[![DOI](https://zenodo.org/badge/1413587976.svg)](https://doi.org/10.5281/zenodo.23301043)

**Author:** Darshan Jagtap  
**Domain:** Computational Biology / Machine Learning Engineering  
**Platform:** Python 3 (Google Colab / Ubuntu Linux Containers)  
**Primary Reproducibility Assets:** `results/deepgo_predictions_master.csv`, `results/figures/definitive_manuscript_dashboard.png`, `analysis_pipeline.ipynb`  

---

## 1. Project Overview & Problem Statement
Modern high-throughput deep learning architectures and traditional ensemble machine learning estimators are widely deployed to automate the functional annotation of primary protein sequences. However, these models frequently display variations associated with global structural layout parameters—such as overall sequence length and low compositional sequence complexity—rather than relying exclusively on localized, highly conserved functional motifs or domain signatures. 

This mini-study establishes a balanced four-group evaluation across a 400-sequence benchmark grid to inspect these patterns. Using the community-verified `unipressed` REST API client and verified biological distribution simulations, a pool of sequences was established. The dataset was stratified into four distinct experimental cohorts (n=100 per group): a Biological Normal cohort, a compositionally biased Low-Complexity Region (LCR) cohort, an unannotated Biological Orphan cohort, and an artificial control population of computer-generated synthetic composition-controlled sequences. 

To evaluate the consistency of these patterns, a trained local Random Forest baseline was evaluated alongside an established deep learning protein-function predictor (DeepGOPlus via the DeepGOWeb REST API) to determine whether low-complexity sequence composition is associated with variations in functional prediction profiles.

---

## 2. Comprehensive Mini-Study Research Matrix (n=400)
The finalized data-scraping, line-by-line text parsing, and cross-validation pipelines generated the following empirical statistical averages across our 400-sequence evaluation grid:

| Proteomic Sample Cohort | Row Volume (n) | Avg Sequence Length (aa) | Minimum Window Shannon Entropy | True Biological GO Count | Mean Random Forest Confidence | Mean DeepGOPlus Confidence |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Biological_LCR_Rich** | 100 | 515.19 | 0.09543 | 1.50 | 0.63768 | 0.51205 |
| **Biological_Normal** | 100 | 499.52 | 2.81865 | 1.72 | 0.52101 | 0.54043 |
| **Biological_Orphan** | 100 | 516.35 | 1.78713 | 0.22 | 0.56461 | 0.53437 |
| **Synthetic_Control** | 100 | 631.81 | 0.00000 | 0.00 | 0.64020 | 0.50855 |

### Preliminary Observations:
1. **The Sequence Length Expansion:** Artificial control sequences built to match structural footprints showcase length shifts, averaging 631.81 amino acids compared to a baseline average of 499.52 amino acids for standard biological sequences.
2. **DeepGOPlus Prediction Tendencies:** Synthetic composition-controlled sequences received functional GO predictions. When introduced to repeating amino acid strings containing natural composition variance, the system assigned a mean confidence score of 0.50855 and generated functional predictions.
3. **Distribution Alignments:** The statistical metrics provide preliminary evidence that the model processes synthetic composition-controlled noise with a mean confidence structure (0.50855) closely aligned to verified biological proteins (0.54043).

**Approved Statement of Finding:** In a 400-sequence evaluation, synthetic and low-complexity sequences were compared with biological controls for GO-prediction count and confidence. Results describe associations in this dataset and do not establish causation.

---

## 3. Computational Pipeline Architecture
* **High-Fidelity Profiling:** Programmatically queries biological REST API endpoints and distribution frameworks to track true functional category cross-references.
* **Native Shannon Window Segmentation:** Tracks local text complexity down to a threshold constraint (<= 2.5) by executing a sliding window function of 20 residues.
* **Predictor Evaluation Engine:** Trains a local Scikit-Learn `RandomForestClassifier` to model sequence parameter evaluations. It utilizes an automated batch loop to parse JSON payload structures from the remote DeepGOWeb network endpoint, merging the metrics back into the master dataset.

---

## 4. Project Experimental Limitations
1. **Sample Size Constraints:** The pipeline profiles a balanced evaluation population matrix (n=400). Extending evaluations across the complete human proteome is required to minimize potential sampling variations.
2. **Organism Restriction:** The scope of this study is isolated to human-centric protein distributions. Prediction patterns may vary when applied to prokaryotic sequences or virus structures.

---

## 5. Required Computational Repository Topology
```text
📁 BioAI-Protein-Complexity/
│
├── 📄 README.md                        <-- Current project guide and documentation
├── 📓 analysis_pipeline.ipynb           <-- Complete production notebook script
│
└── 📁 results/
    ├── 📄 deepgo_predictions_master.csv <-- Combined 400 sequence records data ledger
    └── 📁 figures/
        └── 📊 definitive_manuscript_dashboard.png <-- Exported comparative scatter plot (n=400)
```
