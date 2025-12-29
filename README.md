# Fraud-Detection

## Project Overview
This project aims to improve fraud detection for e-commerce and bank transactions using machine learning. Task 1 focuses on data preparation, exploratory analysis, and feature engineering.

# Task 1: Data Analysis & Preprocessing
### Completed Steps:
1. Data Cleaning: Verified data quality, converted data types, handled datetime formats
2. EDA: Analyzed 151,112 transactions with severe class imbalance 
3. Geolocation: Simulated country mapping (original IP file had NaN values)
4. Feature Engineering: Created 11+ features including time patterns, device/IP sharing metrics
5. Class Balancing: Applied SMOTE/RandomOverSampler to training data 
6. Data Saved: Processed datasets ready for modeling in data/processed/

### Key Features Created:
1. Time-based: time_since_signup_hours, hour_of_day, day_of_week
2. Device/IP Patterns: device_usage_count, ip_usage_count, is_shared_device, is_shared_ip
3. Behavioral: is_bulk_signup, is_off_hours, is_chrome, is_seo_source

### Key Findings:
1. Fraud rate: 0.2% (extreme imbalance)
2. Shared devices/IPs show 1.5-2x higher fraud risk
3. Fraud patterns vary by time, browser, and traffic source
4. Bulk signups (>30/hour) correlate with increased fraud


# Task 2: Modeling, Evaluation & Model Selection

## Objective
Build and evaluate machine learning models to detect fraudulent transactions using the engineered features from Task 1. The focus is on handling highly imbalanced data and selecting a model that balances fraud detection performance with business impact.

## Completed Steps:

### 1. Train–Test Split
- Split the processed dataset into training and testing sets
- Used stratification to preserve the fraud ratio in both sets

### 2. Baseline Model: Logistic Regression
- Trained a Logistic Regression model with class weighting
- Used as a simple, interpretable baseline
- Evaluated using AUC-PR, F1-score, precision, and recall

### 3. Advanced Model: Random Forest
- Trained a Random Forest classifier with:
  - Limited tree depth
  - Balanced class weights
- Captured non-linear fraud patterns missed by Logistic Regression

### 4. Model Evaluation
- Evaluated both models on the test set using:
  - Precision-Recall Curve
  - AUC-PR (primary metric due to class imbalance)
  - F1-Score and Recall
- Generated confusion matrices to analyze false positives and false negatives

### 5. Cross-Validation
- Applied Stratified 5-Fold Cross-Validation on the training set
- Measured model stability using:
  - AUC-PR
  - F1-Score
  - Recall
- Confirmed consistent performance across folds

### 6. Model Comparison & Selection
- Compared Logistic Regression and Random Forest using:
  - AUC-PR
  - F1-Score
  - Business trade-offs (missed fraud vs false alarms)
- Selected Random Forest due to higher AUC-PR and better fraud capture

### 7. Model Persistence
- Saved the final selected model for future deployment:
  - `models/random_forest_fraud_model.pkl`

##  Key Evaluation Results

### Random Forest
- Slightly higher AUC-PR than Logistic Regression
- Better ability to detect fraudulent transactions
- Acceptable false-positive rate

### Logistic Regression
- Strong interpretability
- Competitive performance
- Suitable as a baseline or explainability-focused model

##  Key Takeaways
- AUC-PR is the most reliable metric for fraud detection due to extreme class imbalance
- Random Forest outperformed Logistic Regression in detecting rare fraud cases
- Cross-validation confirmed model stability and generalization
- Feature engineering from Task 1 significantly improved model performance


# Task 3: Model Explainability & Interpretation (SHAP)

## Objective
Explain how the selected Random Forest model makes fraud detection decisions. Since fraud detection impacts real users and financial systems, model predictions must be transparent, interpretable, and trustworthy.

##  Completed Steps:

### 1. Model Loading
- Loaded the trained Random Forest model from Task 2
- Used consistent feature set for accurate explanations

### 2. SHAP Explainer Initialization
- Used TreeExplainer optimized for Random Forest
- Computed SHAP values quantifying each feature's contribution

### 3. Global Model Explainability
- Generated SHAP summary plots showing:
  - Feature importance rankings
  - How high/low feature values influence fraud predictions
  - Most influential fraud indicators across all transactions

### 4. Local (Individual) Explainability
- Created force/waterfall plots for specific transactions
- Visualized why individual cases were flagged as fraud or legitimate
- Showed how multiple features combine to affect fraud risk

### 5. Feature Impact Analysis
- Analyzed direction of feature effects (positive vs negative contributions)
- Compared SHAP insights with Task 1 EDA findings

##  Key Explainability Findings

### Transaction Behavior Features
- **Device sharing** is the #1 fraud indicator (`device_usage_count`: 0.0846 SHAP importance)
- **IP sharing** also strongly increases fraud risk
- Shared resources indicate potential fraud rings

### Time-Based Patterns
- **Short time since signup** significantly increases fraud probability
- **Off-hours transactions** show higher risk
- Time patterns align with typical fraudster behavior

### Model Validation
- SHAP explanations align perfectly with exploratory findings from Task 1
- 9 out of 10 top features match between SHAP and built-in importance
- Model learns logical, interpretable fraud patterns

##  Why SHAP Matters in Fraud Detection
- **Improves trust**: Stakeholders understand why transactions are flagged
- **Enables compliance**: Meets explainability requirements in financial systems
- **Supports debugging**: Identifies model weaknesses and improvement opportunities
- **Facilitates auditing**: Provides clear documentation of decision logic

##  Outputs Generated
- `shap_summary_plot.png` - Global feature importance visualization
- `shap_force_true_positive.png` - Correctly identified fraud case explanation
- `shap_force_false_positive.png` - False alarm case explanation  
- `shap_force_false_negative.png` - Missed fraud case explanation
- `shap-explainability.ipynb` - Complete analysis notebook

##  Key Takeaways
- Random Forest is both accurate **and** interpretable for fraud detection
- SHAP provides clear explanations at global and individual levels
- Explainability results validate earlier data analysis and feature engineering
- The model is suitable for real-world deployment where transparency is critical

##  Project Structure
fraud-detection/
├── data/
│ ├── raw/ # Original datasets
│ └── processed/ # Cleaned and feature-engineered data
├── notebooks/
│ ├── eda-fraud-data.ipynb # Task 1: Data analysis
│ ├── modeling.ipynb # Task 2: Model building
│ └── shap-explainability.ipynb # Task 3: Model interpretation
├── models/
│ ├── random_forest_fraud_model.pkl # Saved best model
│ └── shap_force_*.png # SHAP visualization files
├── requirements.txt # Python dependencies
└── README.md 
