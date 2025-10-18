# Exploratory Approaches

Notebooks in this folder capture early experiments that shaped TrustX-Defect. They bridge the gap between raw ideation and the refined pipelines in `current_approach_implementations` and `proposed_approach_implementations`. Use them to prototype new ideas, run ablation studies, or validate explanation techniques before promoting changes downstream.

## Notebook catalog
- **xai_bruteforce.ipynb**  
  - Performs brute-force feature selection to estimate signal strength for individual metrics and combinations.  
  - Compares gradient, permutation, and SHAP attributions to probe explanation stability.  
  - Ideal when diagnosing noisy features or evaluating new candidate metrics.

- **xai_diabetes.ipynb**  
  - Ports the defect prediction pipeline to the Pima Indians diabetes dataset to stress-test generalisation beyond software engineering.  
  - Highlights domain-transfer adjustments (continuous clinical features vs. discrete code metrics).  
  - Useful for checking robustness under different class imbalance profiles.

- **xai_swdefect_cur.ipynb**  
  - Recreates the “current” baseline workflow extracted from literature for NASA PROMISE datasets.  
  - Acts as a regression harness when modifying preprocessing or hyper-parameters.  
  - Minimal reliability instrumentation makes it a clean comparator for upgraded pipelines.

- **xai_swdefect_pro.ipynb**  
  - Prototype for the enhanced TrustX-Defect approach with calibration diagnostics, GLR analysis, and SHAP reporting.  
  - Tracks feature engineering and reliability visualisations prior to graduation into production notebooks.  
  - Best place to evaluate new trust metrics (e.g., expected calibration error, epsilon-sanity hit rates).

## Recommended workflow
1. **Ideate:** Start with `xai_bruteforce.ipynb` to identify influential features and assess explanation agreement.  
2. **Transfer:** Validate the approach on `xai_diabetes.ipynb` to ensure components generalise outside software datasets.  
3. **Baseline check:** Run `xai_swdefect_cur.ipynb` to benchmark against legacy performance levels.  
4. **Prototype upgrades:** Iterate within `xai_swdefect_pro.ipynb`, layering calibration and explanation robustness checks.  
5. **Promote:** Once stable, port reusable code to the implementation directories and document findings in `Documentation/`.

## Contributor guidelines
- Keep experiments lightweight; reserve large hyper-parameter searches for the implementation notebooks.  
- Annotate major observations in Markdown cells (dataset version, metrics, anomalies) to aid reproducibility.  
- When creating reusable utilities (e.g., plotting helpers), extract them into shared modules under `src/` instead of duplicating code.  
- Reference related literature using citation keys from `Research_Papers/README.md` so insights map back to sources.
- Track parameter changes (e.g., learning rate, tree depth) in a small `experiments.csv` or a notebook header to avoid duplicate trials.  
- If a notebook depends on a feature branch or custom dataset, document the prerequisite branch name or file path in the opening cell.

## Data and environment assumptions
- Datasets are loaded from `../dataset/`; adjust relative paths only if executing from a different working directory.  
- Required Python packages mirror the main project stack (`numpy`, `pandas`, `scikit-learn`, `torch`, `shap`, `matplotlib`). Document any additional dependencies introduced here.  
- Export plots or tables intended for reports into `Documentation/`; delete temporary artefacts before committing to keep the repository tidy.

## Experiment logging template
When running exploratory trials, capture details in a shared log (Markdown or CSV) using the following structure:
```
Notebook: xai_swdefect_pro.ipynb
Date: 2024-09-12
Dataset: pc3.arff (converted to CSV)
Key settings: learning_rate=0.05, max_depth=5, calibration=temperature
Metrics: AUC=0.87, Brier=0.142, ECE=0.031
Observations: Epsilon-sanity hit rate improved to 0.74 after feature scaling tweaks.
Next actions: Replicate on pc4 and update proposed pipeline notebook.
```
This format ensures insights transfer smoothly into production notebooks.

## Known limitations
- Notebooks may lack rigorous error handling; unexpected data formats can cause cell failures. Validate inputs before running long pipelines.  
- Random seeds might differ between runs, affecting reproducibility. Set explicit seeds (`numpy.random.seed`, `torch.manual_seed`) when comparing variants.  
- Some plots rely on interactive backends (e.g., `%matplotlib inline`); ensure Jupyter settings are configured accordingly if running headless.
