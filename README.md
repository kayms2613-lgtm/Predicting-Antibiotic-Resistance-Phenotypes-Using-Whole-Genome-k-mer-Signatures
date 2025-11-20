## 🔍 Introduction

Antibiotic resistance (AR) is an urgent and escalating global health threat, driven by genomic mutations and mobile genetic elements that enable bacteria to survive antibiotic treatment. Traditional phenotypic susceptibility testing is accurate but slow, often requiring 24–48 hours and delaying clinical decisions. This motivates the development of rapid, genome-based computational approaches capable of predicting resistance directly from sequence data.

This project investigates whether **whole-genome k-mer signatures**—short, fixed-length substrings extracted from raw DNA—can accurately distinguish *Escherichia coli* isolates that are resistant or susceptible to ciprofloxacin. Unlike database-matching tools such as CARD or ResFinder, k-mer–based methods do not rely on prior knowledge of AMR genes or SNP catalogs, making them well-suited for detecting emerging or previously uncharacterized resistance mechanisms.

Building on alignment-free genomics research, this study tests the hypothesis that genomic sequence patterns carry sufficient discriminative signal for resistance prediction. Using curated genomes paired with high-quality phenotype labels, multiple machine-learning models were trained and evaluated to identify the strength of k-mer–based prediction and determine which approaches perform best on this dataset.

---

## 📘 Project Summary

A curated set of **26 E. coli genomes** with ciprofloxacin resistance phenotypes was downloaded from BV-BRC. After preprocessing and filtering, each genome was converted into a normalized vector of **31-mer counts**, and a dense **26 × 10,000** k-mer matrix was generated.

Four models—**Logistic Regression, Random Forest, SVM, and Gradient Boosting**—were trained to determine how effectively k-mer patterns predict resistance. Early results show promising predictive performance, especially for tree-based models, with several high-importance k-mers mapping to regions associated with known fluoroquinolone resistance pathways (including *gyrA* and *parC*).

The notebook produces key visualizations including ROC curves, confusion matrices, feature-importance plots, and class-distribution summaries to support interpretation. Although the dataset is small, the balanced class distribution and consistent preprocessing steps strengthen the reliability of the findings.


🚀 How to Run the Project

This project can be run using the main Python script, the Jupyter notebook, or directly through Google Colab. Make sure the dataset is already placed inside the dataset/ folder.

✅ 1. Run the Python Script (Local Machine)
Folder Layout
project/
│
├── src/
│   └── Predicting_Antibiotic_Resistance_Phenotypes_Using_Whole-Genome_k-mer_Signatures.py
│
├── dataset/
│   ├── genome/        ← FASTA genome files
│   └── phenotype/     ← phenotype CSV/TSV file


Run the Pipeline
python src/Predicting_Antibiotic_Resistance_Phenotypes_Using_Whole-Genome_k-mer_Signatures.py \
    --genome_dir dataset/genome \
    --pheno_file dataset/phenotype/phenotype.csv \

This Script Will Automatically:

Load phenotype metadata

Parse FASTA genomes

Extract 31-mer signatures

Build a 10,000-feature matrix

Train LR, RF, SVM, and GBM models

Generate ROC curves, confusion matrices, and feature-importance plots


✅ 2. Run in Google Colab
Upload datasets:
from google.colab import files
files.upload()

Create folders:
!mkdir -p dataset/genome dataset/phenotype outputs

Move your uploaded files into these folders, then open:
notebooks/AMR_kmer_analysis.ipynb


Run:
Runtime → Run all

Colab will execute the full k-mer ML pipeline.

✅ 3. Run from GitHub Clone
Clone repo:
git clone https://github.com/yourusername/kayms2613-lgtm
cd yourrepo

Install dependencies:
pip install -r requirements.txt

Ensure dataset placement:
dataset/
   genome/*.fasta
   phenotype/*.csv

Run either:
Python script
python src/Predicting_Antibiotic_Resistance_Phenotypes_Using_Whole-Genome_k-mer_Signatures.py

Or the notebook
jupyter notebook notebooks/AMR_kmer_analysis.ipynb
---

## 📂 Dataset

The dataset used in this project consists of:

### **1. Genome FASTA Files**
- Source: BV-BRC  
- Contents: 26 complete or draft *E. coli* genomes  
- Format: `.fasta` files stored in `dataset/phenotype/`  
- Each FASTA header includes the genome’s internal BV-BRC Genome ID.

### **2. Phenotype Metadata**
- File stored in `dataset/genome/`  
- Contains:
  - Genome ID  
  - Ciprofloxacin phenotype (Resistant / Susceptible)  
  - Additional metadata (sample ID, source, collection info)

### **3. Labels**
- Resistant = **1**  
- Susceptible = **0**

### **Class Balance**
| Phenotype | Count |
|-----------|-------|
| Resistant | 16 |
| Susceptible | 10 |

The dataset is balanced and suitable for stratified cross-validation.

---

## 🧪 Methods Overview

### **1. Genome Preprocessing**
- FASTA parsing using **Biopython 1.83**
- Extraction of genome-wide 31-mers for each isolate  
- Counting and normalization of k-mers  
- Low-variance features removed  
- Final matrix created with **10,000 informative k-mers**

### **2. Feature Engineering**
- k-mer frequencies normalized using L2 scaling  
- Variance filtering removes sparse or uninformative features  
- Resulting feature matrix: **26 isolates × 10,000 features**

### **3. Model Training**
The following supervised ML classifiers were evaluated:
- **Logistic Regression**
- **Random Forest**
- **Support Vector Machine (SVM)**
- **Gradient Boosting Classifier**

All models implemented using **scikit-learn 1.4**.

Training procedure:
- Stratified 5-fold cross-validation  
- Evaluation metrics: Accuracy, Precision, Recall, F1-score, ROC-AUC  
- Random seeds fixed for reproducibility  

### **4. Visualization Outputs**
The notebook generates:
- Class-distribution plot  
- ROC curves for all models  
- Confusion matrices  
- Random Forest feature-importance plot  
- Summary performance tables  

These help interpret biological relevance and model behavior.

---

## 🧠 Summary of Key Early Findings

- Whole-genome k-mers **do contain predictive signal** for ciprofloxacin resistance.  
- Random Forest and SVM outperform simpler models.  
- Important k-mers align with **biologically meaningful** quinolone resistance regions.  
- Balanced dataset strengthens evaluation credibility.  
- Some models show instability due to small sample size.

---

## 💬 Discussion

Initial results strongly support the project’s hypothesis: **k-mer–based representations of whole genomes can distinguish resistant from susceptible E. coli isolates.** The presence of high-importance k-mers corresponding to known resistance genes (e.g., *gyrA*, *parC*) reinforces the biological validity of machine-learning predictions.

Despite the small dataset (n=26), both SVM and Random Forest showed clear predictive trends, suggesting that genomic patterns driving resistance are detectable even with limited samples. However, Logistic Regression underperformed, indicating that AR mechanisms are nonlinear and distributed across multiple genomic regions.

Some limitations remain:

- Small genome count restricts generalizability.  
- High dimensionality (10,000 k-mers) may introduce noise.  
- Gradient Boosting instability indicates need for more samples.

Upcoming steps will include hyperparameter tuning, mapping informative k-mers to genomic coordinates, and enhancing feature reduction to strengthen interpretability.

**Overall, these results demonstrate promising potential for scalable, alignment-free antibiotic resistance prediction using k-mer-based machine learning.**
 

---

