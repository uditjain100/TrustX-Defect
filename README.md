# TrustX-Defect

## Table of Contents

1. [Project Motivation](#project-motivation)
2. [Features](#features)
3. [Dataset Structure & Requirements](#dataset-structure--requirements)
4. [Algorithmic Pipeline](#algorithmic-pipeline)
5. [Model Architecture](#model-architecture)
6. [Reliability Analysis](#reliability-analysis)
7. [Explanation Techniques](#explanation-techniques)
8. [Usage Instructions](#usage-instructions)
9. [Extending to New Datasets](#extending-to-new-datasets)
10. [Troubleshooting](#troubleshooting)
11. [References](#references)
12. [License & Contact](#license--contact)

---

## Project Motivation

Software defect prediction is critical for improving software quality and reducing maintenance costs. However, traditional machine learning models often lack transparency, making it difficult to trust their predictions. **TrustX-Defect** addresses this by combining robust predictive modeling with explainable AI (XAI) techniques, enabling users to understand, trust, and validate defect predictions.

https://www.openml.org/search?type=data&status=active&id=1054

## Features

- Predicts software defects from tabular datasets (CSV, ARFF)
- Automated preprocessing: missing value imputation, feature scaling
- Model training with cross-validation (stratified k-fold)
- Reliability analysis: calibration curves, Brier score, threshold optimization
- SHAP-based global and local explanations
- Gradient-based sanity checks (GLR, epsilon-sanity)
- Visual reporting: reliability diagrams, SHAP plots, feature importance
- Modular design for easy extension to new datasets

## Dataset Structure & Requirements

Datasets must be placed in the `dataset` directory. Supported formats:

- **CSV**: Recommended. Columns should be numeric features and a binary target (e.g., `defects`, `bug`, `class`).
- **ARFF**: Convert to CSV before use.

Example directory:

```
dataset/
├── swdefect.csv   # Main defect dataset
├── CM1.csv        # NASA defect dataset
├── diabetes.csv   # Example medical dataset
├── mc1.arff       # ARFF format (convert to CSV)
```

**Target column:**
Accepted names: `defects`, `bug`, `Defects`, `Bug`, `defective`, `target`, `class`, `Class`. If not found, update the code to specify your target column.

## Algorithmic Pipeline

1. **Data Loading:** Reads CSV, identifies target column, converts features to numeric, imputes missing values.
2. **Preprocessing:** Standardizes features using `StandardScaler`.
3. **Model Training:** Trains a multi-layer perceptron (MLP) using PyTorch with stratified k-fold cross-validation.
4. **Evaluation:** Computes AUC, accuracy, Brier score, and optimal threshold (Youden's J statistic).
5. **Reliability Analysis:** Plots calibration curve, computes Brier score, and visualizes reliability.
6. **Explanation:** Uses SHAP DeepExplainer for feature attributions, generates beeswarm and bar plots.
7. **Sanity Checks:** Computes GLR (Spearman ρ) and epsilon-sanity hit rate for explanation robustness.
8. **Reporting:** Outputs metrics, plots, and feature rankings.

## Model Architecture

- **MLP (Multi-Layer Perceptron):**
  - Input: All numeric features
  - Hidden layers: 2 (default 32 units each, ReLU activation, dropout)
  - Output: Single neuron (binary classification)
  - Loss: Binary cross-entropy with logits
  - Optimizer: Adam
  - Early stopping: Monitors validation AUC

## Reliability Analysis

Reliability quantifies how well predicted probabilities reflect true outcome frequencies.

- **Calibration Curve:**
  - Plots predicted probability vs. observed fraction of positives (reliability diagram)
  - Ideal: points lie on the diagonal
- **Brier Score:**
  - Mean squared error between predicted probabilities and actual outcomes
  - Lower is better (range: 0 to 1)
- **Threshold Optimization:**
  - Uses Youden's J statistic to select optimal decision threshold

Example:

```python
from sklearn.calibration import calibration_curve
from sklearn.metrics import brier_score_loss

# y_true: true labels, y_prob: predicted probabilities
p_true, p_pred = calibration_curve(y_true, y_prob, n_bins=10, strategy="quantile")
brier = brier_score_loss(y_true, y_prob)
print("Brier Score:", brier)
```

## Explanation Techniques

- **SHAP Beeswarm Plot:**
  - Shows per-sample feature impact (positive/negative contribution)
- **SHAP Bar Plot:**
  - Ranks features by mean absolute SHAP value (global importance)
- **GLR (Spearman ρ):**
  - Measures correlation between SHAP and gradient attributions for each sample
  - High ρ indicates agreement between methods
- **Epsilon-Sanity Check:**
  - Perturbs top features and checks if loss increases as expected
  - Reports hit@1 rate (fraction of samples where SHAP top feature matches loss sensitivity)

## Results & Interpretation

After running the notebook/script, you will obtain:

- **Model Metrics:**
  - AUC (Area Under ROC Curve)
  - Accuracy (at 0.5 and optimal threshold)
  - Brier score (uncalibrated reliability)
- **Reliability Diagrams:**
  - Calibration curve for each fold
- **Explanations:**
  - SHAP beeswarm and bar plots
  - Feature importance ranking
- **Sanity Checks:**
  - GLR histogram (distribution of Spearman ρ)
  - Epsilon-sanity hit rate

**Interpretation:**

- High AUC/accuracy: good predictive performance
- Low Brier score: reliable probability estimates
- Well-calibrated curve: trustworthy predictions
- SHAP plots: identify key defect predictors
- High GLR/epsilon-sanity: robust explanations

## Usage Instructions

### 1. Environment Setup

Install required packages:

```bash
pip install numpy pandas scikit-learn torch shap matplotlib
```

### 2. Jupyter Notebook

Open `defect_xai_analysis.ipynb` and set the dataset path:

```python
csv_path = "../dataset/swdefect.csv"
```

Run the notebook cells in order:

- Data exploration and EDA
- Model training and evaluation
- Reliability analysis
- SHAP explanation and sanity checks

### 3. Python Script

Run the script (if available):

```bash
python defect_xai_analysis.py
```

### 4. Output

Results are displayed in notebook cells and saved as plots (if implemented).

## Extending to New Datasets

1. Add your dataset to the `dataset` folder.
2. Update the `csv_path` variable in the notebook/script.
3. Run the analysis. Ensure the target column is correctly identified.
4. If your target column is not recognized, edit the code to specify its name.

## Troubleshooting

- **Missing target column:**
  - Check column names in your CSV; update code if needed.
- **Non-numeric features:**
  - Convert categorical features to numeric before analysis.
- **Imbalanced classes:**
  - Review class distribution; consider resampling if needed.
- **Package errors:**
  - Ensure all required packages are installed and up to date.
- **CUDA/CPU issues:**
  - Default device is CPU; update code for GPU if available.

## References

- [SHAP documentation](https://shap.readthedocs.io/en/latest/)
- [scikit-learn calibration](https://scikit-learn.org/stable/modules/calibration.html)
- [PyTorch documentation](https://pytorch.org/)
- [NASA defect datasets](https://promise.site.uottawa.ca/SERepository/datasets-page.html)
- [Explainable AI resources](https://arxiv.org/abs/2306.08655)

## License & Contact

MIT License

---

**Contact:**
For questions, bug reports, or contributions, please open an issue or pull request on GitHub. For academic use, please cite the repository or contact the maintainer.
