# Information About the Datasets Used

The project trains on three churn datasets that are harmonised into a unified feature schema at runtime.

---

## Dataset 1 — IBM Telco Customer Churn

| | |
|---|---|
| **Source** | Kaggle |
| **URL** | https://www.kaggle.com/datasets/blastchar/telco-customer-churn |
| **Rows** | 7,043 |
| **Target file** | `data/telco_churn.csv` |

---

## Dataset 2 — Orange Telecom Churn

| | |
|---|---|
| **Source** | Kaggle |
| **URL** | https://www.kaggle.com/datasets/mnassrib/telecom-churn-datasets |
| **Rows** | 3,333 (80/20 split files merged) |
| **Target files** | `data/orange_churn_train.csv` + `data/orange_churn_test.csv` |

---

## Dataset 3 — Iranian Churn Dataset

| | |
|---|---|
| **Source** | UCI ML Repository (ID: 563) |
| **UCI URL** | https://archive.ics.uci.edu/dataset/563/iranian+churn+dataset |
| **Kaggle mirror** | https://www.kaggle.com/datasets/royjafari/customer-churn |
| **Rows** | 3,150 |
| **Target file** | `data/iranian_churn.csv` |

---

## Folder Layout

```
data/
├── telco_churn.csv
├── orange_churn_train.csv
├── orange_churn_test.csv
└── iranian_churn.csv
```
---

## Unified Feature Schema

All three datasets are mapped to these 10 numeric features:

| Feature | Description |
|---|---|
| `tenure` | Months the customer has been with the company |
| `monthly_charges` | Average monthly payment (USD or normalised) |
| `total_charges` | Cumulative charges to date |
| `num_services` | Count of add-on services subscribed |
| `has_internet` | 1 = has internet / data plan |
| `has_phone` | 1 = has voice / phone plan |
| `is_monthly_contract` | 1 = month-to-month / pay-as-you-go contract |
| `cust_service_calls` | Number of calls to customer support |
| `has_complaints` | 1 = customer has lodged a formal complaint |
| `is_senior` | 1 = senior citizen / age-group ≥ 50 |
| **`churn`** | **TARGET — 1 = churned, 0 = stayed** |
