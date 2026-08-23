# Final Report

i. Which insights did you gain from your EDA? 
ii. How did you determine which columns to drop or keep? If your EDA informed this process, explain which insights you used to determine which columns were not needed. 
iii. Which hyperparameter tuning strategy did you use? Grid-search or random-search? Why? 
iv. How did your model's performance change after discovering optimal hyperparameters? 
v. What was your final F1 Score? And what is your interpretation of the precision metric vs the recall metric?


## i. Which insights did you gain from your EDA?
Our EDA showed that fraud is heavily concentrated in TRANSFER and CASH_OUT transactions, while other transaction types rarely contain fraud. We also observed that fraudulent transactions often involve large balance changes, especially full drains of the origin or destination accounts. Correlation analysis revealed strong relationships between old and new balances, supporting the creation of balance-difference features. The dataset is highly imbalanced, with fraud representing a very small fraction of all transactions. These insights guided both preprocessing decisions and model selection.

## ii. How did you determine which columns to drop or keep?
We dropped `nameOrig` and `nameDest` because they are high-cardinality identifiers with no predictive value. We also removed `isFlaggedFraud` because it rarely triggers and does not meaningfully contribute to fraud detection. EDA confirmed that balance-related features and transaction types were strongly associated with fraud patterns, so we kept those and engineered additional features (`balanceDiffOrg`, `balanceDiffDest`) based on observed behavior. All remaining columns showed either direct relevance or measurable correlation with fraud outcomes.

## iii. Which hyperparameter tuning strategy did you use? Grid-search or random-search? Why?
We used GridSearchCV because the parameter space for Random Forest was small and well-defined. Grid search allowed us to systematically evaluate combinations of depth, number of trees, and split criteria without requiring a large search budget. Since Random Forest is relatively stable and not highly sensitive to extreme hyperparameter ranges, a structured grid was sufficient. This approach ensured reproducible results and clear comparisons across parameter sets.

## iv. How did your model's performance change after discovering optimal hyperparameters?
After tuning, the Random Forest model showed improvements in both precision and recall for the fraud class. The optimized model reduced false positives while maintaining strong fraud detection capability. ROC-AUC increased, indicating better separation between fraud and non-fraud transactions. Overall, tuning produced a more balanced and reliable model suitable for real-world fraud detection.

## v. What was your final F1 Score? And what is your interpretation of the precision metric vs the recall metric?
The final F1 score for the fraud class was 0.90. Precision (0.91) indicates that most transactions flagged as fraud were truly fraudulent, minimizing unnecessary investigations. Recall (0.88) shows that the model successfully identified the majority of fraud cases. In fraud detection, precision is critical because false positives are costly, but recall must remain high enough to avoid missing actual fraud. The final model achieves a strong balance between both metrics.
