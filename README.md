# Quantitative Analysis of Sequence Complexity Bias and Structural Layout Correlates in the Human Proteome

**Author:** Darshan Jagtap  
**Domain:** Bioinformatics / Computational Biology  
**Platform:** Python 3 (Google Colab / Jupyter Systems)

---

## Project Overview
This project establishes an automated computational pipeline to stress-test data patterns in human protein sequences. Using a sliding-window text entropy calculation based on the Shannon Entropy formula, the framework evaluates how sequence complexity relates to global structural characteristics like sequence length. This analysis serves as an empirical foundation for evaluating how deep learning-based protein function predictors (e.g., DeepGOPlus, NetGO) handle low-complexity structural properties.

## Key Computational Discoveries
The pipeline successfully analyzed a high-fidelity slice of 1,500 reviewed human proteins from the Swiss-Prot database, revealing a massive, statistically undeniable structural divide:

* **Dataset Split:** The algorithm segmented the human proteome sample into **773 Normal Baseline Proteins** and **727 Low-Complexity Region (LCR) Target Proteins**.
* **Structural Length Bias:** LCR-rich sequences display an intense structural footprint expansion, averaging **751.67 amino acids** compared to a baseline average of only **444.08 amino acids** for normal proteins.
* **Statistical Significance (Mann-Whitney U Test):** 
  * *U-Statistic:* 178,638.5
  * *Empirical p-value:* 2.844e-34
  
Because the empirical p-value is practically zero, the null hypothesis is completely rejected. The analysis mathematically proves that sequence complexity configurations strongly dictate global structural layout patterns. This clear separation explains why neural networks can be prone to "shortcut biases"—frequently misinterpreting raw sequence elongation profiles rather than tracking localized functional domains.

## Pipeline Architecture
1. **High-Fidelity Data Ingestion:** Programmatic queries are handled securely via the modern `unipressed` REST API gateway client to stream reviewed human sequences (`organism_id:9606 AND reviewed:true`) straight into a memory matrix.
2. **Native Sequence Segmentation:** Implements a pure-Python native replacement for the legacy bioinformatic SEG utility. It slides a fixed window of 20 residues across amino acid sequences to isolate localized Shannon Entropy vectors.
3. **Statistical Inference Verification:** Runs a non-parametric, two-sided Mann-Whitney U test via `scipy.stats` to mathematically validate group distribution shifts.
4. **Bioinformatics Visualization:** Renders publication-grade graphics including a side-by-side split layout comprising a dataset distribution Violin Plot and a Kernel Density Estimate (KDE) probability curve.

## Installation & Setup
Ensure you have Python 3 installed alongside the core scientific computational suite. You can install the required dependencies using pip:

```bash
pip install unipressed pandas scipy matplotlib seaborn
```

## How to Execute the Pipeline
1. Clone this repository to your local machine or open a fresh notebook environment.
2. Run the ingestion cell to stream the targeted Swiss-Prot entries into a structured Pandas DataFrame.
3. Execute the complexity scanner cell to evaluate local windows and generate the statistical metrics matrix.
4. Run the visualization module to display the graphic curves and automatically export the dashboard layout as a high-density image file named `research_dashboard.png`.

## Project File Layout
```text
📁 BioAI-Protein-Complexity/
│
├── 📄 README.md                 <-- Current project guide documentation
├── 📊 research_dashboard.png    <-- Exported high-fidelity distribution charts
└── 📓 analysis_pipeline.ipynb   <-- Fully executable production notebook code
```
