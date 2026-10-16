# Dataset Source Documentation

## Dataset
**Telco Customer Churn** (Option A: Predicting Customer Churn for a Telecom Provider)

| Item | Detail |
|---|---|
| Source | Kaggle, dataset "Telco Customer Churn" by BlastChar (IBM sample data for a fictional telecom company): https://www.kaggle.com/datasets/blastchar/telco-customer-churn |
| Date accessed | 13 October 2026 |
| File in this repo | `data/Telco-Customer-Churn.csv` |
| Size | 7,043 rows (customers), 21 columns |
| Target variable | `Churn` (Yes/No), about 26.5% Yes |
| Licence / use | Publicly available sample data, used for educational purposes only |
| Personal data | None. `customerID` is a synthetic identifier. No attempt was made to identify individuals. |

The notebook reads the local file. If the file is missing (for example in a fresh Google Colab session) it downloads the same dataset from IBM's public GitHub copy: https://raw.githubusercontent.com/IBM/telco-customer-churn-on-icp4d/master/data/Telco-Customer-Churn.csv

## Columns
- **Demographics:** gender, SeniorCitizen, Partner, Dependents
- **Account:** tenure, Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges
- **Services:** PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies
- **Target:** Churn

## Preprocessing applied before analysis
1. `TotalCharges` converted from text to numeric. 11 blank entries (all customers with tenure = 0, i.e. not yet billed) were set to 0.
2. `SeniorCitizen` converted from 0/1 to No/Yes.
3. "No internet service" and "No phone service" merged into "No" in the seven add-on service columns.
4. `Churn` encoded as 1 (Yes) / 0 (No).
5. `customerID` dropped (identifier only).
6. Checked for duplicate customers and outliers (IQR rule): none found, nothing removed. Consistency checks passed (no phone-less customers with multiple lines, no internet add-ons without internet, `TotalCharges` within about 8% of tenure x monthly charges for 90% of customers). 22 customers share an identical profile with another customer; they are different people, so they were kept.
7. Five engineered features added: `tenure_group`, `num_services`, `has_protection_services`, `auto_pay`, `charge_per_service`.
8. Stratified 80/20 train/test split (random_state = 42). Scaling and one-hot encoding fitted on training data only, inside a scikit-learn Pipeline. The test set is kept for the final evaluation only, not for tuning or model choice.

All steps are reproduced in `Churn_Analysis.ipynb`. The raw CSV in `data/` is left as downloaded; all cleaning happens in the notebook.

## Caveats
- The data is an IBM sample for a **fictional** company, so results illustrate the method and do not describe a real telecom market.
- Row count, columns and churn rate (7,043 / 21 / 26.5%) match the Kaggle description.
- Library versions used for every reported number are recorded in `models/model_metadata.json`.
