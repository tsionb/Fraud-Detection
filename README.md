# Fraud-Detection

## Project Overview
This project aims to improve fraud detection for e-commerce and bank transactions using machine learning. Task 1 focuses on data preparation, exploratory analysis, and feature engineering.

## Task 1: Data Analysis & Preprocessing
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

