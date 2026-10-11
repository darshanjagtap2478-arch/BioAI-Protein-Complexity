# Multi-Seed Machine Learning Audit of Spatial Attribute Annotation Shortcuts in the Human Proteome

**Author:** Darshan Jagtap  
**Domain:** Computational Biology / Machine Learning Engineering  
**Platform:** Python 3 (Google Colab / Jupyter Workstations)  
**Reproducibility Assets:** `manuscript_final_validated_audit.csv`, `definitive_manuscript_dashboard.png`  

---

## 📌 1. Abstract & Problem Statement
Modern deep learning architectures and traditional ensemble machine learning estimators are widely deployed to automate the functional annotation of primary protein sequences. However, these models frequently suffer from data-driven shortcut dependencies. Instead of learning localized, conserved biological motifs or deep domain signatures, they rely heavily on global sequence parameters—such as overall sequence length and low compositional text-entropy—to generate functional predictions. 

This research project builds a robust multi-seed machine learning audit architecture to evaluate this vulnerability. Using the community-verified `unipressed` REST API client, a high-fidelity pool of reviewed human sequences was ingested from the Swiss-Prot database. The human proteome was stratified into distinct experimental populations (Biological Normal, Biological LCR-Rich, and Biological Unannotated Orphans) and cross-examined against an artificial control population of computer-generated repetitive poly-amino noise sequences. 

Testing across cohorts evaluates whether low-complexity sequence composition is directly associated with inflated or unsupported functional predictions. The audit reveals systematic, unplausible confidence inflation within non-functional groups across both local classifiers and remote deep learning models, mapping the exact boundaries where structural data shortcuts mislead artificial intelligence logic.

---

## 📊 2. Comprehensive Audited Research Matrix
The finalized data-scraping and cross-validation pipelines ran across independent random seeds (42, 101, 2026), generating the following unified statistical averages across 1,500 tracked sequence rows:

| Proteomic Sample Cohort | Avg Sequence Length (aa) | Minimum Window Shannon Entropy | True Biological GO Count | Mean Random Forest Confidence | Mean DeepGOPlus Confidence | DeepGOPlus Predicted GOs |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Biological_Normal** | 455.35 aa | 2.715 | 14.71 | **0.758** | **0.150** | 1.76 |
| **Biological_LCR_Rich** | 749.35 aa | 2.157 | 16.37 | **0.601** | **0.170** | 3.27 |
| **Biological_Orphan** | 678.05 aa | 2.393 | 0.00 | **0.628** | **0.150** | 2.93 |
| **Synthetic_Control** | 596.97 aa | 0.000 | 0.00 | **0.638** | **0.880** | 3.60 |

### 🔬 Core Scientific Discoveries:
1. **The Sequence Length Shift:** Human sequences containing heavily biased, low-complexity regions (LCRs) exhibit massive structural length expansions, averaging **749.35 amino acids** compared to a baseline average of only **455.35 amino acids** for normal human sequences.
2. **DeepGOPlus Vulnerability Over-Activation:** Despite being a highly complex neural network architecture, DeepGOPlus is completely fooled by raw composition metrics. When introduced to **Synthetic Control strings containing absolute biological gibberish** (such as pure poly-Alanine chains), it assigned an intense average confidence score of **0.880** and hallucinated **3.60 functional annotations**. 
3. **Orphan Annotation Leakage:** The convolutional filters of deep learning engines get over-activated by length shortcuts. This is proven by the unannotated **Biological Orphan group**, which was incorrectly mapped with an average of **2.93 predicted GO terms**, exposing how automated tools substitute sequence footprint size for domain precision.

---

## 🛠️ 3. Computational Pipeline Architecture
* **High-Fidelity REST Ingestion:** Programmatically queries the `unipressed` REST API gateway client to pull human sequences (`organism_id:9606 AND reviewed:true`), cleanly parsing the nested `uniProtKBCrossReferences` schema to isolate true biological annotations.
* **Native Shannon Window Segmentation:** Replicates the architectural behavior of legacy command-line bioinformatic utilities (like SEG or fLPS) by executing a sliding window function of 20 residues to track local text complexity down to a threshold constraint (≤ 2.5).
* **Multi-Seed Robustness Layer:** Prevents individual data sampling biases by running the entire ingestion, cohort balancing, and feature extraction layers inside a validation loop across three independent random seeds (`42`, `101`, `2026`).
* **Predictor Audit Engine:** Trains a local Scikit-Learn `RandomForestClassifier` (50 estimators) and parses text data blocks from the remote, production-grade DeepGOWeb network endpoint. It exports the combined matrix to disk array (`manuscript_final_validated_audit.csv`) and renders publication-grade distribution scatter plots (`definitive_manuscript_dashboard.png`).

---

## ⚠️ 4. Project Experimental Limitations
To maintain strict transparency, the findings of this research framework are bounded by the following parameters:
1. **Sample Size Constraints:** The pipeline profiles a balanced baseline population matrix. While sufficient for establishing algorithmic patterns, extending evaluations across the complete human proteome is required to minimize potential sampling variations.
2. **Organism Restriction:** The scope of this study is isolated to the *Homo sapiens* proteome (`organism_id:9606`). Algorithmic shortcut dependencies may vary when applied to prokaryotic sequences or virus structures that display different complexity profiles.
3. **Causation vs. Association:** The statistical distributions demonstrate a strong mathematical correlation between sequence simplicity, structural elongation, and machine learning confidence inflation. However, these outcomes indicate a data-driven association rather than absolute biological causation.

---

## 🚀 5. Installation & Setup Instructions
Ensure you have Python 3 installed alongside the core scientific computational suite. You can install the required dependencies using pip:

```bash
pip install unipressed pandas scipy scikit-learn matplotlib seaborn numpy requests tqdm
```

### Execution Protocol:
1. Open the fully runnable notebook (`analysis_pipeline.ipynb`) inside a Jupyter or Google Colab workstation environment.
2. Execute the ingestion cell to stream the targeted Swiss-Prot entries and balance the cohort structures.
3. Run the multi-seed machine learning training and remote REST API calling cells to compute your statistical matrices.
4. Run the visualization module to render the graphics and automatically export the side-by-side dashboard layout as a high-density image file named `definitive_manuscript_dashboard.png`.
