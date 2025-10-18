# Proposed Approach Implementations

This directory houses the production-ready notebooks that embody TrustX-Defect’s enhancements over the baseline models. Each notebook extends its counterpart in `current_approach_implementations/` with:
1. Advanced preprocessing (feature engineering, class balancing, outlier handling).
2. Automated or Bayesian hyper-parameter optimisation.
3. Calibration techniques (temperature scaling, isotonic regression) and reliability diagnostics.
4. Explanation robustness checks (GLR, epsilon-sanity) and curated SHAP visualisations.
5. Reporting hooks that export plots and metrics for inclusion in `Documentation/`.

## Notebook catalog
- **xai_ada.ipynb** (Adaptive Boosting ++)  
  - Introduces class weight calibration and probability temperature scaling.  
  - Logs SHAP stability across folds to detect overfitting.  
  - Useful for lightweight deployments needing interpretability with improved reliability.

- **xai_cat.ipynb** (CatBoost ++)  
  - Taps into CatBoost’s categorical encoders while enforcing monotonic constraints where applicable.  
  - Produces SHAP summary, dependence, and waterfall plots for multi-level interpretation.  
  - Includes reliability diagrams per dataset split.

- **xai_et.ipynb** (ExtraTrees ++)  
  - Adds temperature scaling and expected calibration error (ECE) reporting.  
  - Explores ensemble size versus calibration trade-offs.  
  - Generates comparative SHAP rankings vs. baseline to highlight improvements.

- **xai_gb.ipynb** (Gradient Boosting ++)  
  - Employs Bayesian optimisation for learning rate, tree depth, and subsample tuning.  
  - Tracks reliability metrics (Brier score, ECE) before and after calibration.  
  - Integrates SHAP interaction values to surface feature synergies.

- **xai_lgbm.ipynb** (LightGBM ++)  
  - Flagship notebook with iterative feature selection, focal loss experiments, and reliability pipelines.  
  - Executes epsilon-sanity checks to confirm explanation sensitivity.  
  - Exports aggregated reports (CSV summaries, PNG plots) spanning all folds.

- **xai_mlp.ipynb** (MLP ++)  
  - Implements cross-validated early stopping with stratified folds and variance reduction via ensembling.  
  - Uses SHAP DeepExplainer and integrated gradients for cross-method validation.  
  - Provides calibration via temperature scaling and histogram binning.

- **xai_rf.ipynb** (Random Forest ++)  
  - Adds threshold optimisation (Youden’s J, cost-sensitive thresholds).  
  - Compares multiple calibration strategies and logs the best-performing approach.  
  - Generates SHAP bar charts annotated with reliability insights.

- **xai_xgb.ipynb** (XGBoost ++)  
  - Incorporates learning rate scheduling, early stopping patience, and class imbalance handling.  
  - Computes fold-wise ECE, Brier score, and reliability diagrams; exports consolidated metrics.  
  - Evaluates explanation robustness by perturbing top SHAP features.

## Usage workflow
1. **Baseline confirmation:** Run the corresponding notebook in `current_approach_implementations/` to establish a reference.  
2. **Configure dataset:** Update the dataset path (default: `../dataset/CM1.csv`) and target column if necessary.  
3. **Execute enhancements:** Run the “proposed” notebook end-to-end; ensure calibration and explanation cells complete successfully.  
4. **Collect artefacts:** Save generated plots (calibration curves, SHAP summaries) and metric tables to `Documentation/` with descriptive filenames.  
5. **Compare results:** Log key metrics (AUC, Brier, ECE, explanation robustness) alongside baseline values to quantify improvements.  
6. **Iterate:** Adjust hyper-parameter search spaces or calibration techniques as new datasets are introduced; document changes in notebook headers.

## Reliability and explanation checklist
- Verify calibration plots show improvements over baselines; note any datasets where calibration diverges.  
- Inspect GLR histograms and epsilon-sanity hit rates to ensure explanations remain trustworthy.  
- Cross-check SHAP global feature rankings with domain expectations; flag anomalies for further investigation.  
- For neural models, compare DeepExplainer outputs with integrated gradients to spot inconsistencies.

## Reproducibility practices
- Fix random seeds for data splits, optimisation routines, and model training (NumPy, scikit-learn, PyTorch, LightGBM, XGBoost).  
- Record hyper-parameter configurations (best-found values, search ranges) in a Markdown summary cell.  
- Persist calibration parameters (e.g., temperature values) when exporting models for deployment.  
- Use consistent evaluation bins (e.g., 10 equally populated bins) when computing ECE to standardise comparisons.

## Extending the proposed pipeline
- When introducing new trust metrics (e.g., conformal prediction intervals), prototype in `src/approaches/` then integrate here.  
- For multi-dataset evaluations, consider scripting batch execution (Papermill, nbconvert) and store aggregated results under `Documentation/metrics/`.  
- If a new model type is added, document its rationale, calibration plan, and explanation method in the notebook introduction.  
- Update `Documentation/README.md` with any new plots or tables derived from these notebooks.

## Troubleshooting
- **Calibration fails to improve:** Revisit class balancing, adjust calibration method (temperature vs. isotonic), or revisit hyper-parameter ranges.  
- **SHAP computation times out:** Sample a subset of data for explanation or leverage approximate/gradient-based alternatives.  
- **Epsilon-sanity results unexpected:** Confirm perturbations target the correct top features and that the loss function matches model training.  
- **Notebook execution slow:** Reduce cross-validation folds temporarily (note the change) or cache intermediate results using joblib/Parquet.
