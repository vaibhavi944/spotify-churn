# 🎵 Spotify User Lifecycle Predictor
[![Python 3.13](https://img.shields.io/badge/python-3.13-blue.svg)](https://www.python.org/downloads/)
[![ML: XGBoost](https://img.shields.io/badge/ML-XGBoost-green.svg)](https://xgboost.readthedocs.io/)
[![SQL: DuckDB](https://img.shields.io/badge/SQL-DuckDB-orange.svg)](https://duckdb.org/)

A high-performance **User Lifecycle Prediction System** engineered to identify behavioral "leading indicators" of attrition. This project integrates advanced temporal feature engineering via **SQL Window Functions** and an optimized **XGBoost** pipeline to predict 30-day user churn with actionable precision.

---

## 🏗️ System Architecture
The project is structured as a modular three-stage pipeline, transitioning from raw event logs to predictive business intelligence.

1.  **Detective Phase ([`01_retention_analysis`](notebooks/01_retention_analysis.ipynb))**:
    *   Cohort analysis to map the user journey.
    *   **Finding**: Identified the **D7 Critical Inflection Point**—a massive engagement drop at the 7-day mark, defining the "golden window" for retention.
2.  **Engineering Phase ([`02_sql_feature_engineering`](notebooks/02_sql_feature_engineering.ipynb))**:
    *   Utilizes **DuckDB** to execute complex SQL window functions on local CSV data.
    *   **Key Features**: `rolling_7d_intensity_avg`, `negative_feedback_density` (skips/minutes), and `intensity_percentile`.
3.  **Predictive Phase ([`03_xgboost_predictor`](notebooks/03_xgboost_predictor.ipynb))**:
    *   Automated ML pipeline including One-Hot Encoding and feature name sanitization.
    *   **Model**: Optimized Gradient Boosted Trees (XGBoost) with a focus on feature attribution (Gain).

---

## 📊 Key Findings & Business Intelligence
### 1. The Power of Feature Engineering
Raw data wasn't enough. Our SQL-engineered features (temporal averages and intensity percentiles) proved to be the **strongest predictors** of churn, outperforming static demographic data.

### 2. Model Performance
*   **Overall Accuracy**: `80%`
*   **Churn Precision**: `0.41` (High signal for identifying risk groups)
*   **Top 3 Churn Predictors (by Gain)**:
    1.  **Subscription Type (Premium)**: Identifying high-value LTV risk.
    2.  **Support Load Score**: Direct link between technical friction and attrition.
    3.  **Regional Signals (France)**: Localized behavioral patterns detected.

### 3. Visual Insights
*   **Retention Curves**: Clearly visualize the probability of a user staying based on their age in the system.
*   **Behavioral KDE Plots**: Distinct "fingerprints" discovered for churned users (higher skip rates vs. lower active minutes).

---

## 🛠️ Technical Stack
| Category | Tools |
| :--- | :--- |
| **Data Engine** | DuckDB (SQL), Pandas, NumPy |
| **Machine Learning** | XGBoost, Scikit-Learn |
| **Visualization** | Seaborn, Matplotlib |
| **Cloud (Design Pattern)** | Boto3 (AWS S3 Ingestion template included) |

---

## ⚙️ Setup & Execution
1.  **Clone the Repository**:
    ```bash
    git clone https://github.com/your-username/spotify-churn.git
    cd spotify-churn
    ```
2.  **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the Pipeline**:
    Open the notebooks in `notebooks/` sequentially (01 -> 02 -> 03) to reproduce the analysis and model.

---

## 📂 Project Structure
```text
├── data/
│   ├── spotify_churn_dataset.csv          # Raw behavioral logs
│   └── engineered_lifecycle_features.csv  # SQL-transformed features
├── notebooks/
│   ├── 01_retention_analysis.ipynb        # Cohort & EDA
│   ├── 02_sql_feature_engineering.ipynb   # DuckDB Window Functions
│   └── 03_xgboost_predictor.ipynb         # ML Training & Audit
├── README.md                              # Project Documentation
└── requirements.txt                       # Dependency Manifest
```

---
*Developed as a demonstration of high-dimensional feature engineering and lifecycle modeling.*
