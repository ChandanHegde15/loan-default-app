## Loan Default Prediction – Application Repository
Project Overview
This repository contains the deployment-ready application layer for a Loan Risk Assessment System.
The system supports two distinct use cases:
Pre-Loan Eligibility Assessment (new applicants)
Post-Loan Default Risk Monitoring (issued loans / portfolio)
All machine learning models in this repository are:
Trained
Validated
Finalized
Serialized (.pkl)
## ⚠️ No model training, feature engineering, or re-fitting is performed in this repository⚠️
This repository is strictly for inference, integration, and deployment.

## Model Summary
1️⃣ Pre-Loan Eligibility Model
Model: Logistic Regression
Purpose: Real-time screening of new loan applicants
Input: Applicant-time features only
Output:
Eligibility probability
Risk band (Low / Medium / High)
Preprocessing: Embedded inside the model pipeline
## File location:
models_preloan/eligibility_lr.pkl

## 2️⃣ Post-Loan Default Monitoring Model
Final Model: Stacking Ensemble
Base Models: Random Forest, XGBoost
Meta Model: Logistic Regression
Purpose: Portfolio-level default risk monitoring
Imbalance Handling: SMOTE + ENN (training phase only)
Feature Selection: 76 selected features
Output:
Probability of default
Risk category (Low / Medium / High)
Files:

models/
├── final_stacking_model.pkl
├── preprocess_pipeline.pkl
├── selected_feature_indices.pkl
├── raw_feature_columns.pkl

## Model Summary
- Final Model for Pre-loan Default Monitoring : Linear Regression
- Final Model for post loan default monitoring: Stacking Ensemble
  - Base Models: Random Forest, XGBoost
  - Meta Model: Logistic Regression
- Imbalance Handling: SMOTE + ENN (training phase only)
- Feature Selection: 76 selected features
- Output: Probability of default + risk category
- Supports unseen customer data



## IMPORTANT RULES


### What you SHOULD do
- Load model files only from `/models`


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