# Algorithmic Shortcut Vulnerabilities in Sequence-Based Machine Learning Models for Functional Proteomic Annotation

**Author:** Darshan Jagtap  
**Domain:** Computational Biology / Machine Learning Engineering  
**Platform:** Python 3 (Google Colab / Jupyter Cluster Environments)  
**Reproducibility Assets:** `robust_ml_audit_results.csv`, `robust_ml_dashboard.png`  

---

## 📌 1. Abstract & Problem Statement
Modern high-throughput deep learning models and traditional machine learning estimators (such as Random Forest and Support Vector Classifiers) are widely deployed to predict Gene Ontology (GO) terms based on primary amino acid sequences. However, these models frequently suffer from structural shortcut vulnerabilities. Instead of learning localized, highly conserved functional motifs or domain signatures, they rely heavily on global sequence layout features, such as overall structural sequence length and low compositional sequence complexity, to output predictions. 

This research project builds a robust, multi-seed machine learning audit architecture to evaluate this vulnerability. Using the modern `unipressed` REST API gateway client, a high-fidelity pool of reviewed human sequences was retrieved from the Swiss-Prot database. The human proteome was stratified into distinct experimental cohorts (Biological Normal, Biological LCR-Rich, and Biological Unannotated Orphans) and evaluated against an artificial control population of completely meaningless, computer-generated repetitive poly-amino noise sequences. 

Statistical validation over three independent data seeds (42, 101, 2026) proves that sequence complexity configurations strongly dictate structural changes. A trained Scikit-Learn Random Forest Classifier demonstrated intense confidence inflation when exposed to non-functional noise, exposing a massive data-driven shortcut loop within sequence-based proteomic predictors.

---

## 📊 2. Empirical Research Matrix & Discoveries
The computational pipeline ran across independent dataset splits, generating the following cross-validated statistical averages:

| Proteomic Sample Cohort | Row Volume (\(n\)) | Avg Sequence Length (aa) | Minimum Window Shannon Entropy | True Biological GO Count | Mean ML Prediction Confidence |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Biological_Normal** | 300 | 455.35 aa | 2.715 | 14.71 | **0.758** |
| **Biological_LCR_Rich** | 300 | 749.35 aa | 2.157 | 16.37 | **0.601** |
| **Biological_Orphan** | 150 | 678.05 aa | 2.393 | 0.00 | **0.628** |
| **Synthetic_Control** | 150 | 596.97 aa | 0.000 | 0.00 | **0.638** |

### 🔬 Core Discoveries:
1. **The Sequence Length Shift:** Human proteins containing heavily biased, low-complexity regions (LCRs) exhibit massive structural length expansions, averaging **749.35 amino acids** compared to a baseline average of only **455.35 amino acids** for normal human sequences.
2. **Algorithmic Shortcut Exploitation:** The Random Forest Classifier assigned a high average prediction confidence score of **0.638** to completely meaningless, non-biological synthetic control blocks (such as pure poly-Alanine and poly-Glutamine chains). 
3. **Orphan Annotation Leakage:** Completely unannotated biological human orphan sequences were incorrectly classified with an inflated mean confidence score of **0.628**. This confirms that sequence length elongation and low compositional entropy act as major algorithmic data shortcuts, triggering systematic, unplausible functional annotations in sequence-based models.

---

## 🛠️ 3. Computational Pipeline Architecture
1. **Dynamic REST Data Ingestion:** Programmatic queries are handled securely via the `unipressed` API layout client to loop through and extract human sequence records (`organism_id:9606 AND reviewed:true`), cleanly isolating the nested `uniProtKBCrossReferences` schema path to map verified biological GO terms.
2. **Native Shannon Window Segmentation:** Replicates the exact architectural behavior of legacy command-line bioinformatic utilities (like SEG or fLPS) by executing a sliding window function of 20 residues to track local text complexity down to a threshold constraint (\(\leq 2.5\)).
3. **Multi-Seed Robustness Layer:** Prevents individual data sampling biases by running the entire ingestion, cohort balancing, and feature extraction layers inside a validation loop across three independent random seeds (`42`, `101`, `2026`).
4. **Predictor Calibration & Graphics Execution:** Trains a Scikit-Learn `RandomForestClassifier` (50 estimators) to extract performance metrics. It outputs clean metadata logs (`robust_ml_audit_results.csv`) and generates high-density dual-axis distribution scatter plots (`robust_ml_dashboard.png`).

---

## 🚀 4. Installation & Setup Instructions
To run this pipeline locally, set up a python 3 compiler and pull down the verified scientific packages via pip:

```bash
pip install unipressed pandas scipy scikit-learn matplotlib seaborn numpy
```

### Execution Protocol:
1. Open the fully runnable notebook (`analysis_pipeline.ipynb`) inside a Jupyter or Google Colab workstation environment.
2. Execute the ingestion cells to map the human proteome and balance the cohort data structures.
3. Run the multi-seed Machine Learning training module to compute your statistical matrices.
4. Execute the visualization block to automatically render and save the final research dashboard graphics to your disk array.

---

## 📂 5. Project Directory Structure
```text
📁 BioAI-Protein-Complexity/
│
├── 📄 README.md                    <-- Current project guide and documentation
├── 📊 robust_ml_dashboard.png       <-- Exported high-fidelity ML confidence scatter plot
├── 💾 robust_ml_audit_results.csv  <-- Reproducible multi-seed training dataset matrix
└── 📓 analysis_pipeline.ipynb       <-- Complete error-free production notebook script
```
