# Telecom Customer Churn Prediction

Applied Data Science Portfolio, Assignment 1, Option A.

We predict which telecom customers are likely to leave, using the IBM Telco Customer Churn dataset with 7,043 customers. The final model is a random forest, and the notebook also covers feature importance, a fairness check and a business recommendation on who the company should actually contact.

## Files

| File | What it is |
|---|---|
| `Group_11_Telco_churn_prediction.ipynb` | the full project, from loading the data to saving the model, with outputs already visible |
| `churn_model.joblib` | the trained random forest, saved together with the cutoff and the column list |
| `WA_Fn-UseC_-Telco-Customer-Churn.csv` | the dataset |
| `DATA_SOURCE.md` | where the data came from and what we did to it |
| `requirements.txt` | python packages needed to run the notebook |

## How to run

**Google Colab**

1. Open colab.research.google.com and upload `Group_11_Telco_churn_prediction.ipynb`
2. Click Runtime, then Run all
3. When the upload box appears, choose `WA_Fn-UseC_-Telco-Customer-Churn.csv`

The last cells of the notebook save `churn_model.joblib` and download it.

**On a laptop**

```
pip install -r requirements.txt
jupyter notebook
```

Put the notebook and the CSV in the same folder, open the notebook and run all cells.

## Results

The final model is a random forest with a cutoff of 0.55. Scores on the test set, which was only used once at the end:

| Accuracy | Precision | Recall | F1-score |
|---|---|---|---|
| 0.773 | 0.555 | 0.727 | 0.630 |

It catches 272 of the 374 churners in the test set. A baseline that predicts "stays" for everyone has 73.5% accuracy but catches none, which is why we look at recall and F1 more than accuracy.

## Using the saved model

```python
import joblib

bundle = joblib.load('churn_model.joblib')
model = bundle['model']
cutoff = bundle['cutoff']
```

New customer data has to go through the `prepare_features` function from section 5 of the notebook first. After that:

```python
probability = model.predict_proba(prepared_data)[:, 1]
likely_to_churn = probability >= cutoff
```

Section 14 of the notebook shows this working on two example customers.

## Data

See `DATA_SOURCE.md`.
