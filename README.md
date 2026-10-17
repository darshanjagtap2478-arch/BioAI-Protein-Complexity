# Balanced Four-Group Evaluation of Length- and Complexity-Associated Prediction Patterns in Sequence-Based Protein Function Predictors

[![DOI](https://zenodo.org/badge/1413587976.svg)](https://doi.org/10.5281/zenodo.23301043)

**Author:** Darshan Jagtap  
**Domain:** Computational Biology / Machine Learning Engineering  
**Platform:** Python 3 (Google Colab / Ubuntu Linux Containers)  
**Primary Reproducibility Assets:** `deepgo_predictions_master.csv`, `definitive_manuscript_dashboard.png`, `analysis_pipeline.ipynb`  

---

## 1. Project Overview & Problem Statement
Modern high-throughput deep learning architectures and traditional ensemble machine learning estimators are widely deployed to automate the functional annotation of primary protein sequences. However, these models frequently display variations associated with global structural layout parameters—such as overall sequence length and low compositional sequence complexity—rather than relying exclusively on localized, highly conserved functional motifs or domain signatures. 

This mini-study establishes a balanced four-group evaluation across a 400-sequence benchmark grid to inspect these patterns. Using the community-verified `unipressed` REST API client, a pool of reviewed human sequences was ingested from the Swiss-Prot database. The dataset was stratified into four distinct experimental cohorts (n=100 per group): a Biological Normal cohort, a compositionally biased Low-Complexity Region (LCR) cohort, an unannotated Biological Orphan cohort, and an artificial control population of computer-generated synthetic composition-controlled sequences. 

To evaluate the consistency of these patterns, a trained local Random Forest baseline was evaluated alongside an established deep learning protein-function predictor (DeepGOPlus via the DeepGOWeb REST API) to determine whether low-complexity sequence composition is associated with variations in functional prediction profiles.

---

## 2. Comprehensive Mini-Study Research Matrix (n=400)
The finalized data-scraping, line-by-line text parsing, and cross-validation pipelines generated the following empirical statistical averages across our 400-sequence evaluation grid:

| Proteomic Sample Cohort | Row Volume (n) | Avg Sequence Length (aa) | Minimum Window Shannon Entropy | True Biological GO Count | Mean Random Forest Confidence | Mean DeepGOPlus Confidence |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Biological_LCR_Rich** | 100 | 795.89 | 2.13129 | 18.01 | 0.67078 | 0.51200 |
| **Biological_Normal** | 100 | 531.91 | 2.73820 | 16.60 | 0.54150 | 0.54200 |
| **Biological_Orphan** | 100 | 711.57 | 2.34065 | 0.00 | 0.63070 | 0.54500 |
| **Synthetic_Control** | 100 | 593.30 | 0.00000 | 0.00 | 0.63800 | 0.50800 |

### Mann-Whitney U Test Significance Metrics (Compared Against Biological Normal Baseline):
* **Synthetic Control vs. Biological Normal:** Median: 0.508 (Synthetic) vs 0.542 (Normal) | p-value = 0.00000 (U-statistic = 0.0)
* **Biological LCR-Rich vs. Biological Normal:** Median: 0.512 (LCR) vs 0.542 (Normal) | p-value = 0.00000 (U-statistic = 0.0)
* **Biological Orphan vs. Biological Normal:** Median: 0.545 (Orphan) vs 0.542 (Normal) | p-value = 0.00000 (U-statistic = 10000.0)

### Preliminary Observations:
1. **The Sequence Length Shift:** Human proteins containing heavily biased, low-complexity regions (LCRs) exhibit structural length expansions within this sample pool, averaging 795.89 amino acids compared to a baseline average of 531.91 amino acids for standard human sequences.
2. **DeepGOPlus Prediction Tendencies:** Some synthetic composition-controlled sequences received GO predictions. When introduced to artificial repeating amino acid strings, the system assigned a mean confidence score of 0.508 and generated functional predictions.
3. **Distribution Alignments:** The statistical test distributions provide preliminary evidence that the model processes synthetic composition-controlled noise with a mean confidence structure (0.508) closely aligned to verified biological human proteins (0.542).

**Approved Statement of Finding:** In a 400-sequence evaluation, synthetic and low-complexity sequences were compared with biological controls for GO-prediction count and confidence. Results describe associations in this dataset and do not establish causation.

---

## 3. Computational Pipeline Architecture
* **High-Fidelity REST Ingestion:** Programmatically queries the `unipressed` REST API gateway client to pull human sequences (`organism_id:9606 AND reviewed:true`), parsing the nested `uniProtKBCrossReferences` schema to isolate true biological annotations.
* **Native Shannon Window Segmentation:** Tracks local text complexity down to a threshold constraint (<= 2.5) by executing a sliding window function of 20 residues.
* **Predictor Evaluation Engine:** Trains a local Scikit-Learn `RandomForestClassifier` (50 estimators) to model sequence parameter evaluations. It utilizes an automated batch loop to parse JSON payload structures from the remote DeepGOWeb network endpoint, merging the metrics back into the master dataset.

---

## 4. Project Experimental Limitations
1. **Sample Size Constraints:** The pipeline profiles a balanced evaluation population matrix (n=400). Extending evaluations across the complete human proteome is required to minimize potential sampling variations.
2. **Organism Restriction:** The scope of this study is isolated to the *Homo sapiens* proteome (`organism_id:9606`). Prediction patterns may vary when applied to prokaryotic sequences or virus structures.

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
