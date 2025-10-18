# Research Papers

Curated references grounding TrustX-Defect in defect prediction, explainable AI, and reliability analysis. Use this directory as the single source for literature cited across reports, presentations, and notebooks.

## Catalog
| File | Authors (Year) | Venue | Topic focus | Key contribution to TrustX-Defect |
| ---- | -------------- | ----- | ----------- | ---------------------------------- |
| 10499820.pdf | Kumar et al. (2016) | IEEE | Software defect prediction at scale | Presents industrial defect prediction best practices that informed our baseline metrics and evaluation criteria. |
| 2306.08655v1.pdf | Boudiaf et al. (2023) | arXiv | Reliability-aware explainable machine learning | Introduces calibration-aware explanation methods; referenced when designing GLR and epsilon-sanity checks. |
| A_Methodology_for_Reliability_Analysis_of_Explainable_Machine_Learning_Application_to_Endocrinology_Diseases.pdf | Paulovich et al. (2022) | Expert Systems with Applications | Reliability audits in healthcare XAI | Demonstrates a rigorous protocol for validating explanations that we adapted to software metrics. |
| Applied Soft Computing.pdf | Malhotra (2015) | Applied Soft Computing | Survey of soft computing techniques for defect detection | Provides comparative baselines and feature ideas for ensemble models. |
| Software Defects Identification_ Results Using Machine Learning and Explainable Artificial Intelligence Techniques.pdf | Dar et al. (2021) | IEEE Access | ML plus XAI for defect identification | Aligns closely with our combined predictive and interpretability pipeline. |
| Understanding Software Defect Prediction Through eXplainable Neural Additive Models.pdf | Aggarwal et al. (2022) | ICSE | Interpretable neural architectures | Inspired the use of additive and SHAP-based perspectives on feature contributions. |

## Suggested workflow
1. **Triage new papers**  
   - Read abstracts quickly, then decide whether to download into this directory.  
   - Rename files using `FirstAuthorYear_TitleSnippet.pdf` for easy identification.
2. **Annotate and summarise**  
   - Maintain a `notes.md` or use PDF annotations to capture experiment setups, datasets, and metrics.  
   - Store replication code snippets or equations in the same file for quick reference.
3. **Cross-link with documentation**  
   - Reference PDFs explicitly in reports stored under `Documentation/` and update bibliography sections with consistent citation keys.  
   - Mention relevant datasets in `dataset/README.md` when a paper discusses them.

## Rapid relevance matrix
| Focus area | High-impact references | Notes for implementation |
| ---------- | ---------------------- | ------------------------ |
| Baseline metrics and evaluation | 10499820.pdf, Applied Soft Computing.pdf | Defines accuracy, recall, and AUC targets for defect prediction benchmarks. |
| Reliability and calibration | 2306.08655v1.pdf, A_Methodology_for_Reliability_Analysis...pdf | Provides formulas for Brier score, ECE, and reliability diagrams integrated into proposed notebooks. |
| Explanation robustness | 2306.08655v1.pdf, A_Methodology_for_Reliability_Analysis...pdf | Guides GLR computation and epsilon-sanity sanity checks. |
| Model interpretability | Understanding Software Defect Prediction...pdf, Software Defects Identification...pdf | Supplies design patterns for SHAP analysis and interpretable neural models. |

## Citation management
- Maintain a `references.bib` file under `Documentation/` that mirrors the PDFs here; update it whenever a new citation is added.
- Use consistent citation keys (e.g., `Aggarwal2022ENAM`) across LaTeX, Markdown, and slides to avoid duplication.
- Record DOI and URL metadata in the BibTeX entry for quick access when drafting.
- When a citation is used in a notebook, add a Markdown cell in the notebook citing the key and linking back to this directory.

## Reading log template
Create a running summary in `reading_log.md` with the following fields for each paper:
```
## Aggarwal2022ENAM
- Status: Completed (2024-07-18)
- Summary: Highlights additive neural models that separate global and local effects.
- Datasets referenced: PROMISE (PC1, PC3), NASA CM1.
- Action items: Prototype a neural additive variant for proposed pipeline comparison.
```
This log helps track open action items and informs which results should be reproduced in notebooks.

## Literature tracking tips
- Create a Zotero or Mendeley library that mirrors this directory structure; export BibTeX entries when writing LaTeX reports.
- Tag papers by theme (`calibration`, `xai`, `defect prediction`) either within your reference manager or by adding suffixes to filenames.
- Record key quantitative results in a shared spreadsheet to enable direct comparisons with your experiments.

## Keeping the folder tidy
- Remove duplicate downloads once the canonical file name is chosen.
- Store supplementary material (code archives, appendices) in subfolders named after the citation key.
- If file sizes become large, compress rarely used PDFs and note the archive location here.
- Maintain a `TO_READ.txt` list for papers not yet reviewed; move entries to the reading log once processed.

## Access and licensing
- Verify each paper's usage rights before sharing externally. Conference or journal PDFs should include citation notices.
- For open-access articles (e.g., arXiv), keep track of version numbers (v1, v2) to ensure experiments align with the referenced revision.
- Store institution-specific access details (library proxy links, VPN requirements) in a separate secure note if needed.

## Linking to implementation
- Note any datasets introduced in a paper and confirm whether they exist in `dataset/`. Create a task if acquisition is pending.
- Capture pseudo-code or algorithmic steps in `notes.md` alongside parameter ranges to accelerate re-implementation.
- When a paper motivates a new experiment, open an issue or TODO in the relevant notebook and reference the citation key.
