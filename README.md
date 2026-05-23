# Customer Churn Prediction Dashboard

An interactive machine-learning dashboard that predicts customer churn using **XGBoost** trained on three real-world datasets. Built with Streamlit and an imbalanced-learning pipeline (SMOTE).

**Streamlit App** : 🔗[URL](https://customer-churn-prediction00.streamlit.app)

---

## Features

| Section | Description |
|---|---|
| **Overview & EDA** | KPI cards, churn distribution, tenure/charge box-plots, correlation matrix, per-feature churn rates |
| **Model Performance** | Confusion matrix, ROC curve (with AUC), feature importance chart, full classification report |
| **Single Prediction** | Interactive form → churn probability gauge with risk level indicator |
| **Batch Prediction** | Upload CSV → scored table with risk bands → download results |

---

## Tech Stack

| Layer | Library |
|---|---|
| Model | XGBoost 2.x (`XGBClassifier`) |
| Preprocessing | scikit-learn `StandardScaler` |
| Imbalance handling | imbalanced-learn `SMOTE` |
| Dashboard | Streamlit |
| Visualisation | Plotly |
| Data | Pandas, NumPy |

---

## Datasets

Three publicly sourced datasets are harmonised into a single 10-feature schema:

| # | Dataset | Source | Rows |
|---|---|---|---|
| 1 | IBM Telco Customer Churn | [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) | 7,043 |
| 2 | Orange Telecom Churn | [Kaggle](https://www.kaggle.com/datasets/mnassrib/telecom-churn-datasets) | 3,333 |
| 3 | Iranian Churn Dataset | [UCI ML Repository](https://archive.ics.uci.edu/dataset/563/iranian+churn+dataset) | 3,150 |

See **DATASET.md** for more information.

---

## Project Structure

```
.
├── app.py                  # Streamlit dashboard (4 pages)
├── train_model.py          # Training pipeline
├── data_loader.py          # Multi-dataset loading & feature harmonisation
├── requirements.txt        # Dependencies
├── README.md
├── DATASET.md              # Dataset download instructions
├── data/                   # Place downloaded CSVs here
│   ├── telco_churn.csv
│   ├── orange_churn_train.csv
│   ├── orange_churn_test.csv
│   └── iranian_churn.csv
└── models/                 # Auto-created by train_model.py
    ├── xgb_model.pkl
    ├── scaler.pkl
    ├── metrics.json
    ├── feature_importance.csv
    └── feature_cols.json
```

## How It Works

### Data Harmonisation
Each dataset has different columns. `data_loader.py` maps each one to a shared 10-feature schema:

```
tenure, monthly_charges, total_charges, num_services,
has_internet, has_phone, is_monthly_contract,
cust_service_calls, has_complaints, is_senior
```

Where a feature is unavailable in a dataset (e.g. `has_internet` for Orange, which is voice-only), it is set to a constant — XGBoost learns to ignore zero-variance columns for those rows.

### Pipeline

```
raw data  →  StandardScaler  →  SMOTE  →  XGBoost
```

- **StandardScaler** normalises features to zero mean / unit variance so that high-magnitude features like `total_charges` don't dominate.
- **SMOTE** generates synthetic samples for the minority churn class in the training set only, keeping the test set untouched.
- **XGBoost** is a gradient-boosted tree ensemble with early stopping, regularisation, and row/column subsampling to prevent overfitting.

### Why multiple datasets?
Training on a single dataset would bias the model toward one provider's demographics and pricing. Combining three datasets from different markets broadens the decision boundary and improves generalisability.

---

## License

This project uses publicly available datasets. See each dataset's source page for its respective license.
