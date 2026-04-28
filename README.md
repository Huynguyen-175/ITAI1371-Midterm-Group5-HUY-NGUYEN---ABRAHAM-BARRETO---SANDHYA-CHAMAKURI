# 🚗 Used Car Price Prediction

### ITAI 1371 — Intro to Machine Learning | Mid-Term Project | Spring 2026

[![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)](https://python.org)
[![Scikit-learn](https://img.shields.io/badge/scikit--learn-1.3+-F7931E?style=flat-square)](https://scikit-learn.org)
[![XGBoost](https://img.shields.io/badge/XGBoost-1.7+-red?style=flat-square)](https://xgboost.readthedocs.io)
[![Pandas](https://img.shields.io/badge/Pandas-2.0+-150458?style=flat-square&logo=pandas)](https://pandas.pydata.org)
[![Platform](https://img.shields.io/badge/Platform-Google%20Colab-F9AB00?style=flat-square&logo=googlecolab)](https://colab.research.google.com)

---

## 📌 Project Overview

This project builds a **supervised regression model** that predicts the asking price of used cars from their attributes. Accurate price prediction has direct commercial value — it helps buyers avoid overpaying and helps sellers price competitively.

The project covers the **full machine learning pipeline**:

- ✅ Real-world data cleaning and string parsing
- ✅ Missing value imputation and duplicate removal
- ✅ Feature engineering and encoding
- ✅ Z-score standardization
- ✅ Training and comparison of three regression models
- ✅ Evaluation using MAE, RMSE, and R²

---

## 👥 Team Members

| Name | Contributions |
|------|--------------|
| **Huy Nguyen** | Data prep, feature engineering, modeling, integration |
| **Abraham Barreto** | EDA, model evaluation, visualization |
| **Sandhya Chamakuri** | Data cleaning, encoding, documentation |

---

## 📊 Dataset

**Source:** [Used Car Listings — Kaggle](https://www.kaggle.com/datasets/used-car-listings)
Scraped from an Indian online automobile marketplace.

| Property | Value |
|----------|-------|
| Raw records | 9,582 rows |
| Raw features | 11 columns |
| Target variable | `AskPrice` (listed price in Indian Rupees) |
| Cleaned training set | 5,973 rows |
| Features after prep | 26 (after encoding & engineering) |

### Feature Overview

| Column | Type | Description |
|--------|------|-------------|
| `Brand` | Categorical | Car manufacturer (e.g., Maruti Suzuki, Toyota, BMW) |
| `model` | Categorical | Vehicle model — *dropped (high cardinality)* |
| `Year` | Numeric | Year manufactured — *dropped (collinear with Age)* |
| `Age` | Numeric | Age in years — key predictor |
| `kmDriven` | Numeric* | Total km driven (raw string, requires parsing) |
| `Transmission` | Categorical | Manual or Automatic |
| `Owner` | Categorical | First or second owner |
| `FuelType` | Categorical | Petrol, Diesel, or Hybrid/CNG |
| `PostedDate` | String | Listing month-year — *dropped (not a car attribute)* |
| `AskPrice` | Numeric* | **Target variable** — listed price in Rupees (raw string) |

> *`kmDriven` and `AskPrice` are raw strings in the source file and require parsing before use.*

---

## 🔧 Data Preparation

### Cleaning Steps

- **Parse raw strings** — Convert `kmDriven` (e.g., `'98,000 km'`) and `AskPrice` (e.g., `'Rs 1,95,000'`) from formatted strings to numeric floats
- **Handle missing values** — Impute 47 null values in `kmDriven` using the median calculated on training data only
- **Remove duplicates** — Drop 724 exact duplicate rows from the raw dataset
- **Feature engineering** — Drop `Year` (collinear with `Age`), `AdditionInfo`, `PostedDate` (low signal), and `model` (too many categories)
- **Brand filtering** — Retain only the top 16 brands by frequency; rare brands are removed to reduce noise
- **Encoding** — One-hot encode `Brand`, `Transmission`, `Owner`, and `FuelType` → integer 0/1 columns
- **Standardization** — Z-score scale `Age`, `kmDriven`, and `AskPrice` (mean=0, std=1) using a scaler fitted on training data only
- **Train/Test split** — Hold out 30% of data as an untouched test set before any cleaning or scaling

---

## 🧠 Models

Three regression models were trained and compared:

| Model | Strengths | Primary Metrics |
|-------|-----------|-----------------|
| **Linear Regression** | Interpretable baseline; coefficient ranking of features | R², MAE |
| **Random Forest** | Non-linear patterns; robust to outliers; feature importance | MAE, RMSE |
| **XGBoost** | Highest accuracy on tabular data; handles missing values | RMSE, R² |

All models are evaluated on the held-out test set using **MAE**, **RMSE**, and **R²**.

---

## 🚀 How to Run

### Option 1: Google Colab (Recommended)

1. Open the notebook in Google Colab
2. Run all cells top to bottom (`Runtime → Run All`)
3. No additional setup required

### Option 2: Local Setup

```bash
# Clone the repository
git clone https://github.com/Huynguyen-175/ITAI1371-Midterm-Group5-HUY-NGUYEN---ABRAHAM-BARRETO---SANDHYA-CHAMAKURI.git
cd ITAI1371-Midterm-Group5

# Install dependencies
pip install pandas numpy scikit-learn xgboost matplotlib seaborn jupyter

# Launch Jupyter
jupyter notebook
```

---

## 📦 Dependencies
python        >= 3.10
pandas        >= 2.0
numpy         >= 1.24
scikit-learn  >= 1.3
xgboost       >= 1.7
matplotlib    >= 3.7
seaborn       >= 0.12

---

## 📁 Repository Structure
ITAI1371-Midterm-Group5/
│
├── notebook.ipynb          # Main Jupyter notebook
├── README.md               # This file
├── data/
│   └── used_cars_raw.csv   # Raw dataset from Kaggle
└── outputs/
├── eda_plots.png
├── model_comparison.png
└── feature_importance.png

---

## 🎓 Course Information

| | |
|--|--|
| **Course** | ITAI 1371 — Intro to Machine Learning |
| **Project** | Mid-Term Group Project |
| **Semester** | Spring 2026 |
| **Group** | Group 5 |

