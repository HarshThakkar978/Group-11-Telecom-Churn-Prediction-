# Dataset source

**Dataset:** Telco Customer Churn

**Created by:** IBM, as a sample dataset for customer retention analysis

**Where we got it:** Kaggle, uploaded by BlastChar
https://www.kaggle.com/datasets/blastchar/telco-customer-churn

**Accessed:** October 2026

**File:** `WA_Fn-UseC_-Telco-Customer-Churn.csv`, 7,043 rows and 21 columns. Each row is one customer. The column `Churn` says whether the customer left within the last month, and 26.5% of customers did.

The file is used exactly as downloaded. We did not edit the CSV itself, and all the changes below happen inside the notebook.

## Preprocessing

1. `TotalCharges` is stored as text in the original file. We converted it to a number. 11 customers had a blank value, and all of them have a tenure of 0, meaning they had just joined and not been billed yet. We filled these with 0 and did not drop any rows.
2. `SeniorCitizen` was 0 and 1, so we changed it to No and Yes to match the other columns.
3. In the service columns, "No internet service" and "No phone service" were merged into "No". The `InternetService` and `PhoneService` columns still show which customers have no internet or phone.
4. `Churn` was changed to 1 for yes and 0 for no.
5. `customerID` is not used as an input.
6. We checked for duplicates and outliers and found none, so no rows were removed.

## Features we added

- `num_addons`: how many of the 6 add-on services the customer has
- `tenure_group`: tenure grouped into 0 to 1, 1 to 2, 2 to 4 and 4 to 6 years
- `auto_pay`: Yes if the customer pays by automatic bank transfer or credit card

## Splitting

The data was split 60/20/20 into training, validation and test sets with a fixed random seed of 42, stratified by churn so all three sets have the same churn rate. Scaling and encoding are learned from the training data only.
