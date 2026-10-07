# Customer Churn Analysis & Risk Prediction

An end-to-end customer churn analysis project using **Python, machine learning, and Power BI** to understand churn patterns, predict customer churn risk, and identify customers who may need retention attention.

## Project Overview

Customer churn is a major business problem: understanding which customers are more likely to leave can help companies prioritize retention efforts.

This project answers three main questions:

* **What customer characteristics are associated with higher churn?**
* **How accurately can churn be predicted?**
* **Which customers have the highest predicted churn risk?**

The analysis combines exploratory data analysis with two classification models and a Power BI dashboard for interactive exploration.

> **Important:** The dataset is observational, so the patterns identified in the analysis represent associations rather than causal relationships.

---

## Key Findings

The analysis identified several clear churn patterns:

* Overall churn rate is **26.5%** across **7,043 customers**.
* **Month-to-month customers** have a churn rate of **42.7%**, compared with **11.3%** for one-year contracts and **2.8%** for two-year contracts.
* Customers with **0–12 months of tenure** have the highest churn rate at **47.4%**, while customers with **61–72 months** have a churn rate of **6.6%**.
* Tenure, total charges, monthly charges, contract type, internet service, and payment method are among the strongest signals identified by the Random Forest model.
* A **40% churn-probability threshold** was used to classify customers as high risk.
* This threshold identifies **3,235 high-risk customers**, whose average predicted churn probability is **68.6%**.

The Power BI dashboard allows these patterns to be explored interactively and provides a customer-level view of predicted churn risk.

---

## Machine Learning

### Data Preparation

The dataset was prepared before modeling by:

* Inspecting data types, missing values, and duplicates
* Converting `TotalCharges` to a numeric variable and handling invalid/blank values
* Removing `customerID` from the model features
* Creating a binary `ChurnFlag` target
* Encoding categorical variables
* Scaling numeric variables where required
* Using a **stratified train/test split** to preserve the churn distribution
* Building preprocessing and modeling steps using Scikit-learn pipelines

The target variable is imbalanced, with approximately **73.5% non-churned customers and 26.5% churned customers**.

### Models

Two classification models were trained and compared:

* **Logistic Regression**
* **Random Forest**

Model evaluation was performed on a held-out test set.

### Model Performance

| Metric   | Result |
| -------- | -----: |
| Accuracy |  76.7% |
| Recall   |  71.9% |
| F1 Score |  62.1% |
| ROC-AUC  |  84.2% |

Because missing a potential churner can be more costly than contacting a customer who ultimately stays, threshold analysis was also performed. The final dashboard uses a **40% predicted-probability threshold** to identify high-risk customers.

---

## Power BI Dashboard

The dashboard is divided into three pages.

### 1. Churn Overview

Provides a high-level view of:

* Total customers
* Actual churn rate
* High-risk customers
* Average churn probability
* Churn rate by contract type
* Churn rate by tenure group
* Churn rate by internet service
* Churn rate by payment method
* Held-out model performance

### 2. Churn Drivers

Explores the features most associated with churn using:

* Random Forest feature importance
* Logistic Regression coefficients
* Average monthly charges for churned vs. retained customers
* Average tenure for churned vs. retained customers

### 3. Customer Risk

Provides a customer-level risk view with:

* Predicted churn probability
* Contract type
* Tenure
* Internet service
* Payment method
* Monthly charges

Customers with a predicted churn probability of **40% or higher** are classified as high risk.

The probability column uses conditional formatting to make lower-, medium-, and higher-risk customers easier to identify.

---

## Project Structure

```text
telco-churn-analysis/
│
├── data/
│   └── telco_churn.csv
│
├── notebooks/
│   └── churn_analysis.ipynb
│
├── outputs/
│   ├── churn_eval_test_set.csv
│   ├── churn_scoring_all_customers.csv
│   ├── rf_feature_importance.csv
│   └── lr_coefficients.csv
│
├── powerbi/
│   └── telco_churn_dashboard.pbix
│
├── screenshots/
│   └── dashboard.png
│
└── README.md
```

---

## Technologies

**Python**

* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

**Business Intelligence**

* Microsoft Power BI
* DAX
* Power Query

---

## Workflow

```text
Raw Data
   ↓
Data Cleaning & Validation
   ↓
Exploratory Data Analysis
   ↓
Feature Preparation
   ↓
Train / Test Split
   ↓
Logistic Regression + Random Forest
   ↓
Model Evaluation
   ↓
Threshold Analysis
   ↓
Score All Customers
   ↓
Power BI Dashboard
```

---

## Outputs

The Python workflow produces separate outputs for different purposes:

* `churn_eval_test_set.csv` — predictions on the held-out test set for honest model evaluation
* `churn_scoring_all_customers.csv` — churn probabilities and risk classifications for the full customer population
* `rf_feature_importance.csv` — Random Forest feature importance
* `lr_coefficients.csv` — Logistic Regression coefficients

Keeping model evaluation separate from full-customer scoring prevents the dashboard's customer risk analysis from being confused with held-out model evaluation.

---

## Limitations

This project is intended as an analytical and predictive exercise rather than a production retention system.

The main limitations are:

* The dataset is observational, so the analysis does not establish causality.
* Model predictions indicate estimated risk, not certainty that a customer will churn.
* The 40% threshold is a business-oriented decision threshold and can be adjusted depending on the cost of false positives and false negatives.
* Retention actions would require additional business information, such as customer value, intervention cost, and historical retention outcomes.

---

## Conclusion

This project combines **data cleaning, exploratory analysis, predictive modeling, threshold analysis, and business intelligence** into one workflow.

The final result is not only a churn prediction model, but also an interactive dashboard that connects overall churn patterns to individual customer risk.
