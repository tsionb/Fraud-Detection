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
