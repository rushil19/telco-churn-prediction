# Telecom Customer Churn Prediction

Data Science Assignment 1 (Portfolio), Option A. Predicts which telecom customers are likely to churn, comparing a tuned Logistic Regression and a tuned Random Forest against a baseline.

## Contents
| File | Purpose |
|---|---|
| `Churn_Analysis.ipynb` | Full workflow: cleaning and validation, EDA, feature engineering, tuning, model comparison, results and evaluation, model export (outputs included) |
| `data/Telco-Customer-Churn.csv` | Dataset (see `DATASET_SOURCE.md`) |
| `models/best_churn_model.joblib` | Final model: full scikit-learn pipeline (preprocessing + tuned Logistic Regression) |
| `models/random_forest_model.joblib` | The other tuned model (Random Forest), for comparison |
| `models/model_metadata.json` | Chosen model, hyperparameters, input columns, library versions, test results |
| `figures/` | Charts used in the report (Figures 1-12) |
| `evaluation_data/` | Tables behind the Results section (metrics, confusion counts, importance, thresholds, fairness) |
| `demo/demo_customer_test_case.csv` | Held-out customer used for the demo |
| `DATASET_SOURCE.md` | Where the data came from and what was changed |
| `requirements.txt` | Python packages (versions used for the reported results) |

## How to run
1. Install Python 3.10+ and run `pip install -r requirements.txt`
2. Run `jupyter notebook` and open `Churn_Analysis.ipynb`
3. Choose *Run All* (about 3-5 minutes; the Random Forest grid search is the slow step). If the CSV is missing locally, the notebook downloads it automatically.

Reported numbers come from one run with the versions in `requirements.txt`. Other scikit-learn versions can shift tree-based results in the third decimal.

## Use the saved model
Load it with the same scikit-learn version listed in `models/model_metadata.json`.
```python
import joblib, pandas as pd
model = joblib.load("models/best_churn_model.joblib")
# new_customer: a one-row DataFrame with the 24 input columns listed in models/model_metadata.json
# (see the last section of the notebook for a full example)
print(model.predict_proba(new_customer)[:, 1])
```

## Team
- Punya Arora
- Rushil Chawla
- Sree Renga Harinee
- Ruth Schnarch
