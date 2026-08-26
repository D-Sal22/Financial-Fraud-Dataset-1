# Final Report

i. Which insights did you gain from your EDA? 

ii. How did you determine which columns to drop or keep? If your EDA informed this process, explain which insights you used to determine which columns were not needed. 

iii. Which hyperparameter tuning strategy did you use? Grid-search or random-search? Why? 

iv. How did your model's performance change after discovering optimal hyperparameters? 

v. What was your final F1 Score? And what is your interpretation of the precision metric vs the recall metric?


## i. Which insights did you gain from your EDA?
The EDA showed that fraud in this dataset was concentrated in TRANSFER and CASH_OUT transactions. I also observed that fraudulent transactions often involve large balance changes, especially full drains of the origin or destination accounts. Correlation analysis revealed strong relationships between old and new balances, supporting the creation of balance-difference features. The dataset is highly imbalanced, with fraud representing a very small fraction of all transactions. These insights guided both preprocessing decisions and model selection.

## ii. How did you determine which columns to drop or keep?
I dropped `nameOrig` and `nameDest` because they are high-cardinality identifiers that were not useful for the scope of this model. I also removed `isFlaggedFraud` because it rarely triggers and does not meaningfully contribute to fraud detection. EDA confirmed that balance-related features and transaction types were strongly associated with fraud patterns, so I kept those and engineered additional features (`balanceDiffOrg`, `balanceDiffDest`) based on observed behavior. 

## iii. Which hyperparameter tuning strategy did you use? Grid-search or random-search? Why?
I used GridSearchCV because the parameter space for Random Forest was small and well-defined. Grid search allowed me to systematically evaluate combinations of tree depth, number of estimators, and minimum samples required to split a node without requiring a large search budget. Because the full training dataset contained several million transactions, the search was performed on a stratified subset of the training data to make tuning computationally manageable while preserving the fraud/non-fraud class distribution.

GridSearchCV selected 200 estimators, no maximum depth restriction, and a minimum samples split of 2. These parameters matched the effective configuration of the baseline Random Forest, so tuning confirmed the baseline configuration rather than materially changing test performance. This structured approach provided reproducible results and a clear comparison across the tested parameter combinations.

## iv. How did your model's performance change after discovering optimal hyperparameters?
The Random Forest substantially outperformed Logistic Regression for fraud-focused classification. GridSearchCV was used to evaluate alternative Random Forest hyperparameters on a stratified subset of the training data. The search selected 200 estimators, no maximum depth restriction, and a minimum samples split of 2, matching the effective configuration of the baseline Random Forest.

As a result, hyperparameter tuning confirmed the baseline Random Forest configuration rather than materially changing test performance. The final model achieved 0.91 precision, 0.88 recall, and a 0.90 F1 score for fraudulent transactions, with a ROC-AUC of approximately 0.9987.

## v. What was your final F1 Score? And what is your interpretation of the precision metric vs the recall metric?
The final F1 score for the fraud class was 0.90. Precision (0.91) indicates that most transactions flagged as fraud were truly fraudulent, minimizing unnecessary investigations. Recall (0.88) shows that the model successfully identified the majority of fraud cases. In fraud detection, precision is critical because false positives are costly, but recall must remain high enough to avoid missing actual fraud. The final model achieved a strong balance between both metrics.
