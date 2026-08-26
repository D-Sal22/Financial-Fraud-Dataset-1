# Financial Fraud Detection

## Project Overview

This project develops a machine learning workflow for identifying fraudulent activity within a synthetic financial transactions dataset. The analysis moves from exploratory data analysis (EDA) and preprocessing through model development, hyperparameter tuning, and evaluation.

The project compares Logistic Regression with a Random Forest classifier, with Random Forest selected as the final model based on its stronger balance of precision and recall for fraudulent transactions.

## Key Results

The final Random Forest model achieved:

- **Precision:** 0.91
- **Recall:** 0.88
- **F1 Score:** 0.90
- **ROC-AUC:** 0.9987

The model correctly identified **1,451 of 1,643 fraudulent transactions** in the test set while producing **141 false-positive alerts**.

GridSearchCV was used to evaluate alternative Random Forest hyperparameters. The search selected 200 estimators, no maximum depth restriction, and a minimum samples split of 2, confirming that the baseline Random Forest configuration was already optimal among the tested combinations.

## Project Workflow

1. **Exploratory Data Analysis (EDA)**  
   Examines transaction distributions, fraud frequency, class imbalance, transaction types, balance behavior, and relationships among numeric features.

2. **Preprocessing & Feature Engineering**  
   Removes high-cardinality and low-information fields, encodes transaction type, and creates balance-difference features informed by the EDA.

3. **Modeling & Evaluation**  
   Compares Logistic Regression and Random Forest, performs Random Forest hyperparameter tuning with GridSearchCV, and evaluates fraud-focused performance using precision, recall, F1 score, confusion matrices, and ROC-AUC.

4. **Final Report**  
   Summarizes the analytical findings, feature-selection decisions, tuning strategy, model performance, and interpretation of fraud-focused metrics.

## Project Files

- [`eda.ipynb`](notebooks/eda.ipynb) — Exploratory data analysis
- [`preprocessing.ipynb`](notebooks/preprocessing.ipynb) — Data cleaning and feature engineering
- [`modeling.ipynb`](notebooks/modeling.ipynb) — Model development, tuning, and evaluation
- [`FINALREPORT.md`](report/FINALREPORT.md) — Final project report

## Tools & Technologies

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Jupyter Notebook
- Git / GitHub


## Data Setup Instructions

This repository does not include the original dataset due to file size limits on GitHub.

Before running the notebooks, create a `data/` folder in the project root and place the raw dataset in that directory as:

`fraud_data_raw.csv`

The EDA and preprocessing notebooks will load the raw dataset using:

```python
df = pd.read_csv("../data/fraud_data_raw.csv")


## Appendix
**Dataset Column Definitions**

Below is a description of each column in the synthetic financial‑fraud dataset:

**step**
A time index representing hours in the simulation.  
Example: step 1 = hour 1, step 2 = hour 2, etc.

**type**
The type of financial transaction.  
Common values include:
- `CASH_IN`
- `CASH_OUT`
- `DEBIT`
- `PAYMENT`
- `TRANSFER`

**amount**
The amount of money transferred in the transaction.

**nameOrig**
The ID of the originating (sender) account.  
This is a random string identifier, not a real name.

**oldbalanceOrg**
The sender’s account balance **before** the transaction.

**newbalanceOrig**
The sender’s account balance **after** the transaction.

**nameDest**
The ID of the destination (receiver) account.  
Also a random identifier.

 **oldbalanceDest**
The receiver’s account balance **before** the transaction.

**newbalanceDest**
The receiver’s account balance **after** the transaction.

**isFraud**
Ground‑truth label indicating whether the transaction was fraudulent.  
- `0` = legitimate  
- `1` = fraud

**isFlaggedFraud**
A naive rule‑based flag that marks transactions as fraud **only if the amount > 200,000**.  
This is intentionally simplistic and usually not useful for 
