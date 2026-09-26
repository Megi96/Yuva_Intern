# AI Internship — Weekly Task Submissions

This repository collects the weekly deliverables completed during the internship: notebooks, reports, and supporting files for each assigned task.

## Repository Structure

```
.
├── week2-data-preprocessing/
│   ├── week2_data_preprocessing_feature_engineering.ipynb
│   ├── Week2_Data_Preprocessing_Report.docx
│   └── README.md            # task-specific notes (this file, or a per-week copy)
├── requirements.txt
└── README.md                 # you are here
```

> As new weeks are added, create one folder per week (e.g. `week3-.../`) following the same pattern: a notebook or script as the primary deliverable, a `.docx` report summarizing it, and any supporting assets.

## Week 2 — Data Preprocessing & Feature Engineering

**Objective.** Build and document a reproducible pipeline that turns a raw, messy dataset into a clean, model-ready feature matrix, and empirically validate that the feature engineering actually improves predictive performance.

**Files:**
- `week2_data_preprocessing_feature_engineering.ipynb` — fully executed Jupyter notebook containing all code, inline documentation, and pre-rendered visualizations. Opens ready-to-read; re-running top to bottom reproduces identical results (see [Reproducibility](#reproducibility) below).
- `Week2_Data_Preprocessing_Report.docx` — companion Word report summarizing the methodology, findings, and validation results for readers who prefer a document over a notebook.

**What the pipeline covers:**
1. Data loading (simulated, realistic telecom customer-churn dataset, N = 2,000)
2. Exploratory data analysis (missingness, distributions, outliers)
3. A leakage-free train/test split — performed *before* any statistic is fit
4. Missing-value imputation (median / mode / explicit "Unknown" category)
5. Outlier detection and treatment (IQR-based winsorization)
6. Categorical encoding (one-hot for nominal, preserved ordering for ordinal)
7. Feature scaling (`StandardScaler`, fit on train only)
8. Feature engineering — six new features, each with a stated rationale
9. Multicollinearity check (VIF) and redundant-feature pruning
10. Baseline-vs-engineered model comparison (ROC-AUC) to quantify actual impact

**Key result:** engineered features lifted held-out ROC-AUC from ~0.678 to ~0.680 over the cleaned baseline, after dropping two features flagged as redundant by VIF analysis.

## Requirements

```
python >= 3.9
numpy
pandas
matplotlib
seaborn
scikit-learn
```

Install with:
```bash
pip install -r requirements.txt
```

## Reproducibility

Every notebook in this repository fixes `RANDOM_STATE = 42` and uses it consistently for data simulation, train/test splitting (with stratification where applicable), and any model fitting. No internet access or external files are required — datasets are generated in-notebook — so running `Kernel → Restart & Run All` on any machine with the listed dependencies reproduces identical numbers, tables, and plots.

## How to Run

1. Clone the repository.
2. Install dependencies: `pip install -r requirements.txt`.
3. Open the desired week's notebook in Jupyter (`jupyter notebook week2-data-preprocessing/week2_data_preprocessing_feature_engineering.ipynb`) or VS Code.
4. Run all cells top to bottom.

## Notes

- Each `.docx` report is generated from, and mirrors, its corresponding notebook — the notebook is the source of truth for code and exact output values.
- Datasets are simulated rather than pulled from a fixed external source, so they remain available and reproducible even if a public dataset changes or goes offline.
