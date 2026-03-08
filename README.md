# ESG Risk Prediction for Credit Assessment

## Overview

This project develops a **machine learning model to predict a company's ESG (Environmental, Social, Governance) risk score** to support credit risk evaluation.

The goal is to build a **real-time inference model** that estimates ESG risk using only features available at the point of credit assessment. This ensures the model avoids **data leakage** and remains applicable in practical lending scenarios.

The model predicts a **continuous ESG risk score**, which can be used by financial institutions to incorporate sustainability risk into credit decisions.

---

## Problem Statement

Financial institutions increasingly incorporate ESG considerations into credit risk analysis. However, many ESG datasets include **derived metrics or historical indicators** that are not available for new applicants.

This project focuses on building a predictive model that:

* Estimates **ESG risk score**
* Uses **only real-time available features**
* Avoids **data leakage**
* Provides **explainable predictions**

---

## Dataset

The dataset contains ESG-related metrics for publicly listed companies which exclusively features companies from the influential S&P 500 index.

### Key Characteristics

* **Total companies:** 583
* **US companies:** 482
* **Highly skewed geographic distribution**
* Includes ESG pillar scores and company attributes

### Example Columns

| Column                 | Description                     |
| ---------------------- | ------------------------------- |
| sector                 | Company sector                  |
| industry               | Company industry                |
| full_time_employees    | Number of employees             |
| environment_risk_score | Environmental pillar risk score |
| governance_risk_score  | Governance pillar risk score    |
| social_risk_score      | Social pillar risk score        |
| esg_risk_level         | ESG risk category               |
| is_US                  | Engineered geographic indicator |

### Removed Columns (to prevent leakage)

The following features were removed because they would not be available during real-time credit evaluation:

* `symbol`
* `name`
* `address`
* `description`
* `location`
* `esg_risk_percentile`
* `total_esg_risk_score`
* `controversy_level`
* `controversy_score`

---

## Key Challenges

### 1. Data Imbalance (Geographic Bias)

The dataset was heavily skewed toward US companies:

* **482 / 583 companies were US-based**

This raised concerns about **geographic bias**, which was partially addressed by engineering an `is_US` feature.

---

### 2. Missing Data Analysis

Missingness patterns were evaluated using:

* **MCAR** – Missing Completely At Random
* **MAR** – Missing At Random
* **MNAR** – Missing Not At Random

Based on this analysis:

* Numerical features were **imputed using median values**
* Categorical features were **filled with "Unknown"**

---

### 3. Data Leakage Prevention

Several columns were derived from the target variable or historical controversies.

Including them would produce **unrealistically high model performance** and invalidate real-time deployment.

These features were removed to ensure **true predictive capability**.

---

## Feature Engineering

Final model features:

```
sector
industry
full_time_employees
environment_risk_score
governance_risk_score
social_risk_score
is_US
```

Categorical variables were **one-hot encoded** before training.

---

## Model Training

Multiple regression models were trained:

* **Random Forest Regressor**
* **XGBoost Regressor**

These models were chosen for their ability to capture **non-linear relationships** and handle structured tabular data effectively.

---

## Model Evaluation

Since this is a **regression problem**, model performance was evaluated using:

### R² (Coefficient of Determination)

Measures how well the model explains variance in ESG risk scores.

### RMSE (Root Mean Squared Error)

Measures the average magnitude of prediction errors.

Both metrics were used to ensure **accurate and stable predictions**.

---

## Model Explainability

To ensure transparency and interpretability, the project incorporates **SHAP (SHapley Additive exPlanations)**.

This allows stakeholders to understand:

* Which features influence ESG risk predictions
* The contribution of each variable to the model output

Example insight:

> Governance risk score and environmental risk score were among the strongest contributors to predicted ESG risk.

---

## Project Workflow

```
Data Collection
      ↓
Data Cleaning
      ↓
Missing Data Analysis (MCAR / MAR / MNAR)
      ↓
Feature Engineering
      ↓
Data Leakage Prevention
      ↓
Model Training (Random Forest, XGBoost)
      ↓
Evaluation (R², RMSE)
      ↓
Model Explainability (SHAP)
      ↓
Real-Time Deployment Preparation
```

---

## Real-Time Deployment Considerations

The model was designed to support **real-time ESG inference** during credit evaluation.

Key considerations:

* Use only features available at application time
* Prevent derived ESG metrics from leaking target information
* Keep the feature set lightweight for fast inference

The trained model can be exported and integrated into a backend service for automated ESG risk evaluation.

---

## Tech Stack

* **Python**
* **Pandas**
* **Scikit-learn**
* **XGBoost**
* **SHAP**
* **Jupyter / Google Colab**

---

## Future Improvements

* Expand dataset beyond US-dominated samples
* Incorporate **time-series ESG trends**
* Add **federated learning for privacy-preserving ESG modeling**
* Deploy model via **REST API for production credit systems**

---

## Author

**Adeseto Akinwe**
**www.linkedin.com/in/adeseto-akinwe**

Machine Learning | Optimization | ESG Risk Modeling