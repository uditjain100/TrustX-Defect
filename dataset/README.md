# Dataset

Raw benchmark datasets used to evaluate TrustX-Defect. Place additional CSV/ARFF files here before running notebooks.

## Included files
- **CM1.csv** - NASA CM1 software module metrics with binary defect labels (already converted to CSV).
- **diabetes.csv** - Medical dataset used as an auxiliary case study for validating generalisation.
- **mc1.arff**, **mc2.arff**, **mw1.arff**, **pc1.arff**, **pc2.arff**, **pc3.arff**, **pc4.arff** - NASA PROMISE datasets retained in their original ARFF format; convert to CSV (`python -m arff2csv`) before ingestion.

## Usage guidelines
- Verify that every file contains a binary target column (e.g., `defects`, `bug`, `class`). Update notebook configuration if a target name differs.
- Use consistent preprocessing (scaling, imputation) when adding new datasets to keep cross-study comparisons fair.
- Prefer storing large or proprietary datasets via `.gitignore` to avoid accidental commits; keep this folder focused on shareable benchmarks.

## Directory quick view
```
dataset/
├── CM1.csv
├── diabetes.csv
├── mc1.arff
├── mc2.arff
├── mw1.arff
├── pc1.arff
├── pc2.arff
├── pc3.arff
└── pc4.arff
```

## Dataset catalog
| File | Domain | Format | Notes |
| ---- | ------ | ------ | ----- |
| CM1.csv | NASA spacecraft flight software metrics | CSV | Label column typically named `defects` |
| diabetes.csv | Medical diagnostics (Pima Indians Diabetes) | CSV | Binary label `class` with 0 or 1 |
| mc1.arff | NASA PROMISE (Mission Control) | ARFF | Convert to CSV before training |
| mc2.arff | NASA PROMISE (Mission Control v2) | ARFF | Shares schema with `mc1` |
| mw1.arff | NASA PROMISE (Maintenance) | ARFF | Contains categorical severity flags |
| pc1.arff | NASA PROMISE (Project Control) | ARFF | Common defect benchmark |
| pc2.arff | NASA PROMISE (Project Control v2) | ARFF | More features than `pc1` |
| pc3.arff | NASA PROMISE (Project Control v3) | ARFF | Useful for temporal generalisation |
| pc4.arff | NASA PROMISE (Project Control v4) | ARFF | High class imbalance |

## ARFF to CSV conversion
- Install the helper library once: `pip install liac-arff`.
- Convert in place:
  ```
  python - <<'PY'
  import arff, csv, pathlib

  src = pathlib.Path("dataset")
  for path in src.glob("*.arff"):
      data = arff.load(open(path))
      out = path.with_suffix(".csv")
      with open(out, "w", newline="") as f:
          writer = csv.writer(f)
          writer.writerow([a[0] for a in data["attributes"]])
          writer.writerows(data["data"])
      print(f"Converted {path.name} -> {out.name}")
  PY
  ```
- Confirm the resulting CSVs retain the expected target column and remove the ARFF files if no longer needed.

## Feature schema expectations
- PROMISE datasets mostly contain numeric software metrics (lines of code, cyclomatic complexity, Halstead measures).
- Categorical attributes may appear (e.g., module name). Encode them numerically or drop them before training.
- Missing values are rare but treat them consistently (median imputation in notebooks).
- Ensure the positive class signifies defective modules (`1`, `true`, or `yes`).

## Preprocessing checklist
- Inspect class balance with pandas:
  ```
  python -c "import pandas as pd; df = pd.read_csv('dataset/CM1.csv'); print(df['defects'].value_counts())"
  ```
- Standardise features before training if models assume comparable scales (scikit-learn pipelines already do this).
- Apply stratified splitting to preserve class ratios across train and validation folds.
- Document any feature engineering steps in `Documentation/` for reproducibility.

## Adding a new dataset
1. Place the raw file under `dataset/`. Prefer CSV for reproducibility.
2. Validate the schema (numeric features and a binary target). Rename the target to an accepted name if necessary.
3. Record provenance in this README (file name, source URL, pre-processing decisions).
4. Update notebooks to load the dataset and capture new experiment results in `Documentation/`.

## Data management tips
- Track large proprietary data outside version control using `.gitignore`.
- Compress archival datasets with `tar.gz` if storage becomes an issue.
- When sharing externally, include a data usage or licensing note aligned with the original source.
