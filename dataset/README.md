# Dataset Directory

This folder contains all raw input datasets used by notebooks in `src/`.

## Directory Facts

- **Path:** `/Users/uditjain/Downloads/Final_Year_Project/dataset`
- **Data files:** 9
- **Formats present:** `.xlsx`, `.csv`, `.arff`

## Complete File Inventory

| File | Format | Size | Last Modified | Description |
| --- | --- | --- | --- | --- |
| `CM1.xlsx` | .xlsx | 41.83 KB | 2025-09-19 21:43 | CM1 software defect dataset stored in Excel format. |
| `diabetes.csv` | .csv | 23.31 KB | 2019-09-19 22:44 | Diabetes benchmark dataset used for auxiliary/generalization experiments. |
| `mc1.arff` | .arff | 998.49 KB | 2025-10-11 01:04 | PROMISE/NASA MC1 dataset in ARFF format. |
| `mc2.arff` | .arff | 25.02 KB | 2025-10-11 01:21 | PROMISE/NASA MC2 dataset in ARFF format. |
| `mw1.arff` | .arff | 53.78 KB | 2025-10-11 01:21 | PROMISE/NASA MW1 dataset in ARFF format. |
| `pc1.arff` | .arff | 103.42 KB | 2025-10-11 01:20 | PROMISE/NASA PC1 dataset in ARFF format. |
| `pc2.arff` | .arff | 577.86 KB | 2025-10-11 01:21 | PROMISE/NASA PC2 dataset in ARFF format. |
| `pc3.arff` | .arff | 199.32 KB | 2025-10-11 01:08 | PROMISE/NASA PC3 dataset in ARFF format. |
| `pc4.arff` | .arff | 179.97 KB | 2025-10-11 01:08 | PROMISE/NASA PC4 dataset in ARFF format. |

## Loading Guidance

- Notebooks generally read files from relative path `../dataset/`.
- ARFF files may need conversion to CSV in some notebook flows.
- Keep target columns consistent (`defects`, `bug`, `class`, etc.) when adding new datasets.

## Update Checklist

1. Add/replace dataset file in this directory.
2. Update this README table with metadata and description.
3. Update corresponding notebook configuration in `src/`.
