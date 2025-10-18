# Current Approach Implementations

Reproducible notebooks implementing the baseline models covered in the literature review. Each notebook follows a shared scaffold:
1. Load and inspect datasets from `../dataset/`.
2. Preprocess via numeric casting, missing value imputation, and scaling.
3. Train using stratified k-fold cross-validation with fixed random seeds for reproducibility.
4. Evaluate using ROC-AUC, accuracy, precision/recall, Brier score, and calibration plots.
5. Generate SHAP explanations (global bar charts, local beeswarm) for interpretability.

## Notebook catalog
- **xai_ada.ipynb** (Adaptive Boosting)  
  - Base learners: decision stumps with learning rate tuning.  
  - Emphasis on comparing AdaBoost feature importances with SHAP values.  
  - Useful as a fast baseline on imbalanced datasets.

- **xai_cat.ipynb** (CatBoost)  
  - Leverages CatBoost’s ordered boosting to handle categorical fields and reduces target leakage.  
  - Includes SHAP value extraction via CatBoost’s native API for alignment with model internals.  
  - Captures calibration curves pre/post isotonic calibration.

- **xai_et.ipynb** (ExtraTrees)  
  - Focuses on variance reduction by averaging randomized trees.  
  - Reports feature importance variance across folds to highlight stability concerns.  
  - Provides quick sanity checks for ensemble baselines.

- **xai_gd.ipynb** (Gradient Boosting, scikit-learn)  
  - Classical gradient boosting implementation with shallow trees.  
  - Explores learning rate versus number of estimators trade-offs.  
  - Benchmarks training times compared to more modern libraries.

- **xai_lgbm.ipynb** (LightGBM)  
  - Uses histogram-based tree growth and gradient-based one-side sampling.  
  - Tuned for faster training on high-dimensional PROMISE datasets.  
  - Integrates SHAP TreeExplainer for detailed feature attribution.

- **xai_mlp.ipynb** (Multi-Layer Perceptron)  
  - Implements the neural architecture detailed in the project report (two hidden layers, dropout).  
  - Utilises early stopping and learning-rate scheduling per fold.  
  - Generates SHAP values via DeepExplainer for neural interpretation.

- **xai_rf.ipynb** (Random Forest)  
  - Classic bagging ensemble emphasising robustness to noisy features.  
  - Includes OOB (out-of-bag) error tracking and SHAP-based feature rankings.  
  - Serves as a stable baseline for ensemble comparisons.

- **xai_xgb.ipynb** (XGBoost)  
  - Highly configurable gradient boosting with regularisation (lambda, alpha).  
  - Supports class weight adjustments to cope with defect imbalance.  
  - Compares native gain/cover importances with SHAP values to ensure alignment.

## Recommended workflow
1. **Synchronise datasets**: Ensure prerequisite CSVs exist in `dataset/`. Convert ARFF files beforehand.  
2. **Run baseline notebooks**: Execute each notebook end-to-end to replicate reported metrics; save generated plots to `Documentation/`.  
3. **Record results**: Log metrics (AUC, Brier, ECE) in a shared spreadsheet or Markdown table.  
4. **Compare with proposed pipeline**: Use outputs as the reference point when evaluating `proposed_approach_implementations/`.  
5. **Document deviations**: If metrics differ from published values, annotate the notebook with data version, parameter changes, or environment notes.

## Testing and reproducibility
- Set seeds via `numpy.random.seed`, `random.seed`, and framework-specific calls (`torch.manual_seed`) where applicable.  
- Employ consistent fold splits by storing the `StratifiedKFold` configuration (number of splits, shuffle flag, seed).  
- Use the same preprocessing pipeline across models to allow apples-to-apples comparisons.  
- Export SHAP plots and calibration diagrams with filenames reflecting the dataset, model, and fold for traceability.

## Extending the baselines
- When introducing a new model variant, clone the closest existing notebook and document the divergence in the header.  
- Keep hyper-parameter grids concise; extensive sweeps belong in exploratory notebooks (`src/approaches/`).  
- If a notebook introduces reusable utility functions, extract them to a shared module (e.g., `src/utils/metrics.py`) and import accordingly.  
- Cross-reference the motivating literature entry in `Research_Papers/README.md` and note any expected behaviour changes.

## Troubleshooting checklist
- **Inconsistent metrics**: Verify dataset preprocessing, class balancing, and random seed alignment.  
- **SHAP computation errors**: Ensure the model type is supported by the selected SHAP explainer (TreeExplainer vs. DeepExplainer).  
- **Calibration plots missing**: Confirm that probability outputs are being captured (e.g., `predict_proba`).  
- **Long training times**: Reduce estimator counts temporarily or sample fewer folds for quick smoke tests, documenting any shortcuts taken.
