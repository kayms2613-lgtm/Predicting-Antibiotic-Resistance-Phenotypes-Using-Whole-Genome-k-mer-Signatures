AI Usage & Reproducibility Statement

This project used AI tools (specifically ChatGPT) only for writing support, organization, and clarification of concepts, not for data analysis or scientific computation.

How AI Was Used

To help draft and revise written sections such as the introduction, methods descriptions, results summaries, and README content.

To refine explanations of machine-learning workflows, k-mer processing steps, and project structure.

To format tables, summaries, and documentation for clearer presentation.

To propose workflow improvements and help troubleshoot non-biological coding issues (e.g., file structure, formatting, documentation).

What AI Was Not Used For

No AI tool processed, analyzed, or interpreted genomic data.

No AI model generated k-mers, trained machine-learning classifiers, or evaluated results.

All computational steps—including parsing genomes, building feature matrices, training models, calculating metrics, and generating visualizations—were executed entirely through Python code written and validated by the project team.

Manual Verification

All AI-assisted text was:

Manually reviewed for accuracy and technical correctness.

Checked against Python outputs, datasets, and BV-BRC metadata.

Revised or corrected wherever inconsistencies were identified.

Reproducibility Practices

To ensure full reproducibility:

All Python scripts and notebooks used for data processing and modeling are included in the repository.

Package versions (Python 3.10, Biopython 1.83, NumPy 1.26, pandas 2.2, scikit-learn 1.4, matplotlib 3.8, seaborn 0.13) are documented in requirements.txt.

Random seeds were fixed for all model-training steps.

All datasets used in the project are publicly available from BV-BRC and stored locally in the dataset/ directory for reproducibility.

Outputs such as ROC curves, confusion matrices, and feature-importance plots are saved in the outputs/ directory.

Ethical Considerations

All data used were publicly available bacterial genomes with no human-identifiable information.

AI assistance was restricted to communication clarity and documentation, not the scientific validity of the results.
