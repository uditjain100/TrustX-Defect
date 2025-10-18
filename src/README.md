# Source Code

This directory provides all executable notebooks and shared utilities for TrustX-Defect. The layout mirrors the project lifecycle: experimentation, baseline reproduction, and production-ready enhancements. Run notebooks from the project root (`../`) so relative paths to `dataset/` and `Documentation/` resolve correctly.

## Directory layout
- **approaches/**  
  Exploratory notebooks used for ideation, ablation studies, and cross-domain validation. See `approaches/README.md` for notebook-by-notebook guidance, experiment logging templates, and environment notes.

- **current_approach_implementations/**  
  Baseline implementations that reproduce metrics cited in the dissertation. Each notebook shares a common scaffold (load, preprocess, train with cross-validation, evaluate, explain) and acts as the reference point for subsequent improvements.

- **proposed_approach_implementations/**  
  Production-ready notebooks encapsulating TrustX-Defect enhancements: calibration pipelines, reliability diagnostics, explanation robustness checks, and automated reporting. Refer to `proposed_approach_implementations/README.md` for detailed per-model capabilities.

- **utils/** (optional, create as needed)  
  Central location for reusable Python modules (metrics, plotting helpers, calibration wrappers). Extract shared logic from notebooks here to reduce duplication.

## Workflow across directories
1. **Explore**  
   Prototype hypotheses in `approaches/` (feature selection, new metrics, cross-domain transfer). Document setup, findings, and follow-up tasks in Markdown cells.
2. **Baseline**  
   Run `current_approach_implementations/` notebooks to establish benchmark metrics per dataset. Capture outputs (tables, plots) for comparison.
3. **Enhance**  
   Apply advanced preprocessing, calibration, and explanation tooling in `proposed_approach_implementations/`. Log improvements versus baselines.
4. **Report**  
   Export artefacts (calibration diagrams, SHAP summaries, metric CSVs) to `Documentation/` for inclusion in papers, presentations, and progress updates.

## Execution checklist
- Install required packages: `numpy`, `pandas`, `scikit-learn`, `torch`, `lightgbm`, `xgboost`, `catboost`, `shap`, `matplotlib`, `seaborn`, `scipy`, `joblib`. Document extra dependencies directly in notebooks.
- Ensure datasets reside in `../dataset/`; convert ARFF files to CSV before running if necessary.
- Set consistent random seeds (`numpy.random.seed`, `random.seed`, `torch.manual_seed`, library-specific seed setters) to improve reproducibility.
- Restart kernels and run notebooks top to bottom before committing to avoid stale outputs or hidden state.
- Save derived artefacts with descriptive filenames (e.g., `calibration_pc3_lgbm_fold1.png`) under `Documentation/`.

## Notebook conventions
- First cell: high-level summary (objective, dataset, date, maintainer) and references to relevant literature entries in `Research_Papers/README.md`.
- Configuration cell: centralise paths, target column names, hyper-parameters, and seed values for easy modifications.
- Logging cell: append key metrics to a shared CSV (e.g., `../Documentation/metrics/baseline_results.csv`) or embed Markdown tables summarising results.
- Comment complex code snippets sparingly to explain non-obvious logic (custom calibration, explanation sanity checks).
- Tag TODOs with `TODO:` and, if actionable, cross-link to issues or tasks.

## Automation and batch runs
- Use Papermill or `jupyter nbconvert --execute` to batch-execute notebooks across datasets or parameter sweeps. Store scripts under `scripts/` if repeat runs are required.
- For nightly builds or CI, limit to smoke tests (smaller estimator counts or fewer folds) and document any shortcuts in output logs.
- Archive aggregated metrics in `Documentation/metrics/` with timestamped filenames (e.g., `metrics_2024-09-15.csv`).

## Testing and quality assurance
- Validate new utilities (under `utils/`) with lightweight unit tests (`pytest`) where feasible. Place tests in `tests/` (create if absent) and ensure they run without notebook context.
- Perform manual spot checks on SHAP plots and calibration curves after major changes to confirm expected behaviour.
- When results deviate from baselines, note the change in the notebook and update `Documentation/README.md` if the reported figures change.

## Dependency management
- Maintain a `requirements.txt` or `environment.yml` at the project root; update it when new packages are introduced.
- For GPU-specific dependencies (e.g., CUDA-enabled PyTorch), supply installation notes in the notebook header.
- Avoid pinning patch versions unless necessary; prefer minimum versions that satisfy functionality.

## Data provenance
- Document dataset versions and preprocessing steps in the notebook summary. If a dataset is modified (resampled, filtered), save the transformed copy with a suffix (e.g., `_processed`) under `dataset/processed/` and record details in `dataset/README.md`.
- Ensure all generated intermediate files are either committed intentionally or excluded via `.gitignore`.

## Collaboration tips
- Use consistent notebook metadata (title, authors, dataset) for easy navigation.  
- Coordinate merges by working on separate notebooks or branches to avoid conflict-heavy `.ipynb` diffs.  
- When handing off work, include a short status block (completed steps, pending actions, blockers) at the top of the notebook or in a companion comment.  
- Consider exporting critical notebooks to HTML/PDF for quick sharing with stakeholders who do not run code.

## Quick FAQ
- **Where do I add a new model experiment?** Start in `approaches/`; once stable, promote to `current_approach_implementations/` (baseline) or `proposed_approach_implementations/` (enhanced).  
- **How do I share results?** Export figures/tables to `Documentation/` and reference them in progress reports or slide decks.  
- **What if I need a new utility?** Implement it in `utils/` (or create the folder) and import it in notebooks. Add usage notes to this README or the relevant subdirectory README.  
- **How do I ensure reproducibility?** Set seeds, log hyper-parameters, and keep notebook outputs in sync with the code by always running cells sequentially after changes.
