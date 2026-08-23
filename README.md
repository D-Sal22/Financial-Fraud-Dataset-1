## Project Overview
This project builds a fraud‑detection model using a synthetic financial transactions dataset. It includes three main components: exploratory data analysis (EDA), preprocessing, and modeling.

##  Project Summary
This project builds a fraud‑detection model using a synthetic financial transactions dataset. The workflow includes exploratory data analysis to identify fraud‑related patterns, preprocessing to clean and engineer features, and modeling using a Random Forest classifier and Logistic Regression comparison. The final model achieves strong fraud‑focused performance with high precision and recall, making it effective at identifying fraudulent activity while minimizing false positives. All notebooks are organized to run sequentially once the dataset is placed in the `data/` folder.


## Data Setup Instructions

This repository does not include the original dataset due to file size limits on GitHub.

Before running any notebooks, please download the dataset provided in Canvas and place it in the following directory:
After placing the file in the `data/` folder, the notebooks will load it automatically using:

`python
df = pd.read_csv("../data/fraud_data_raw.csv") `

## Appendix
## Dataset Column Definitions

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
