
# Home Credit Default Risk - Kaggle Challenge

This project is a solution to the [Home Credit Default Risk](https://www.kaggle.com/competitions/home-credit-default-risk) competition hosted on Kaggle. The goal is to predict the probability that an applicant will default on a loan based on a variety of financial, demographic, and behavioral features.

---

## Project Overview

Home Credit seeks to expand credit opportunities to unbanked individuals. Accurate credit scoring helps them responsibly provide loans while managing risk. This project builds a predictive model that ranks applicants based on their default likelihood.

---

## Dataset Used

The dataset contains both a main application file and multiple auxiliary tables:

- `application_train.csv` / `application_test.csv`
- `bureau.csv` / `bureau_balance.csv`
- `previous_application.csv`
- `POS_CASH_balance.csv`
- `installments_payments.csv`
- `credit_card_balance.csv`

---

## Preprocessing & Feature Engineering

- Merged and aggregated auxiliary tables into the main training set.
- Dropped columns with more than **60% missing values**.
- Imputed remaining missing values:
  - **Numerical** → median
  - **Categorical** → mode
- Applied **label encoding** to binary features and **one-hot encoding** to low-cardinality categorical features.
- Engineered ratio features:
  - `CREDIT_INCOME_RATIO = AMT_CREDIT / AMT_INCOME_TOTAL`
  - `ANNUITY_INCOME_RATIO = AMT_ANNUITY / AMT_INCOME_TOTAL`
  - `ANNUITY_CREDIT_RATIO = AMT_ANNUITY / AMT_CREDIT`
  - `EMPLOYED_PERCENT = DAYS_EMPLOYED / DAYS_BIRTH`

Final dataset contained **168 features** after preprocessing.

---

## Modeling Approach

- Models used:
  - Logistic Regression (baseline)
  - LightGBM (final model)
- Feature selection using **Random Forest feature importance** (top 50 features)
- Hyperparameter tuning via **Optuna**
- **5-fold stratified cross-validation** with out-of-fold (OOF) AUC evaluation
- Final model trained using best parameters from Optuna.

---

## Results

| Model                    | Public AUC | Private AUC |
|-------------------------|------------|-------------|
| Logistic Regression     | ~0.703     | ~0.705      |
| LightGBM (all features) | ~0.765     | 0.76718     |
| LightGBM (top 50)       | 0.76426    | **0.76966** ✅ |

---


## 📽️ Presentation Slides

You can find a detailed summary in the [📊 PowerPoint presentation](https://github.com/vigneshrb250/Home-Credit-Default-Analysis/blob/main/Home%20Credit%20Default%20Risk%20Analysis.pptx).

---

## Folder Structure

```
├── data/                        # Raw and processed datasets
├── notebooks/                  # Jupyter Notebooks (EDA, modeling, tuning)
├── submission/                 # CSVs submitted to Kaggle
├── Home_Credit_Default_Risk_Analysis.pptx  # Presentation slides
└── README.md                   # This file
```

---

## How to Run

1. Clone the repo:
```bash
git clone https://github.com/vigneshrb250/Home-Credit-Default-Analysis.git
cd Home-Credit-Default-Analysis
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the notebook `EAI Assignment.ipynb` end-to-end for training and submission generation.

---

## Author

**Vignesh Ramaswamy Balasundaram**  
[LinkedIn](https://www.linkedin.com/in/vigneshrb250/) | [GitHub](https://github.com/vigneshrb250)

---

## Final Notes

- This solution focuses on clarity, interpretability, and strong validation practices.
- Additional performance could be achieved by ensembling or using external data.

⭐ If you found this helpful, consider starring the repo!
