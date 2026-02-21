# Loan Default Prediction – Application Repository

## Project Overview
This repository contains the deployment-ready application layer for a Loan Default Prediction System.
It uses a pre-trained machine learning model to predict the probability of loan default for new, unseen customers.

The machine learning model has already been:
- Trained
- Validated
- Finalized
- Serialized

 ⚠️No model training or feature engineering is performed in this repository.⚠️

## Model Summary
- Final Model: Stacking Ensemble
  - Base Models: Random Forest, XGBoost
  - Meta Model: Logistic Regression
- Imbalance Handling: SMOTE + ENN (training phase only)
- Feature Selection: 76 selected features
- Output: Probability of default + risk category
- Supports unseen customer data



## IMPORTANT RULES

### What NOT to do
- Do NOT retrain the model
- Do NOT modify or replace `.pkl` files
- Do NOT add training notebooks to this repository
- Do NOT change preprocessing or feature selection

### What you SHOULD do
- Load model files only from `/models`
- Build web UI / API / database layer
- Use the provided prediction pipeline
- Handle new customer inputs safely

The `/models` directory must be treated as READ-ONLY.


## Prediction Pipeline
For every new prediction request:

Raw customer input  
→ align columns using `raw_feature_columns.pkl`  
→ `preprocess_pipeline.pkl` (scaling + encoding)  
→ `selected_feature_indices.pkl` (76 features)  
→ `final_stacking_model.pkl`  
→ Probability of default  
→ Risk category (Low / Medium / High)

## Input Format Example
{
"loan_amnt": 15000,
"term": "36 months",
"int_rate": 13.5,
"installment": 510,
"grade": "B",
"sub_grade": "B2",
"home_ownership": "RENT",
"annual_inc": 60000,
"verification_status": "Verified",
"purpose": "credit_card",
"dti": 18.5,
"fico_range_low": 690,
"fico_range_high": 694
}

- Missing fields are handled safely
- Unseen categorical values are supported

---

## Output
The system should return:
- Probability of Default (0–1)
- Risk Category (Low / Medium / High)
- Optional explanation using SHAP

Example:
Probability of Default: 0.72  
Risk Category: High Risk


## Explainability (Optional)
- Use SHAP on the XGBoost base model
- Explain top contributing features
- Prediction: Stacking Ensemble
- Explanation: XGBoost + SHAP



## Database Recommendation
- Recommended: PostgreSQL
- Demo / local testing: SQLite

Store:
- Raw input data
- Prediction output
- Risk category
- Timestamp

## Installation
Create virtual environment:
python -m venv venv
Activate:
- Windows: `venv\Scripts\activate`
- Linux / Mac: `source venv/bin/activate`

## Install dependencies:

pip install -r requirements.txt

## Testing
Before building UI:
- Load `.pkl` files
- Test prediction using dummy input
- Ensure pipeline runs without errors


## Related Repository
Machine learning training notebooks and experimentation are maintained in a separate repository.
This repository is strictly for application development and deployment.


## Final Note
Model training is complete.
Application development starts here.