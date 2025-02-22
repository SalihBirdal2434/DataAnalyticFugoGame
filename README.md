# Predicting 90-Day Total Revenue Using 15-Day Ingame Data

This project involves using user data from a mobile game to predict each user's total revenue generated in their first 90 days. The dataset contains user metadata and their ingame behavior during the first 15 days, as well as a target variable indicating each user's total 90-day revenue. The goal is to train a model on the training set and generate predictions on the test set, minimizing **Root Mean Square Error (RMSE)**.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset Description](#dataset-description)
3. [Files Provided](#files-provided)
4. [Getting Started](#getting-started)
5. [Approach Outline](#approach-outline)
6. [Submission Format](#submission-format)
7. [Future Work](#future-work)

---

## Project Overview
This project aims to predict **day-90 total revenue** of each user based on their **first 15-day** metadata and ingame behavior. By applying machine learning or statistical models to the training data, we can generate robust revenue predictions on the test set.

---

## Dataset Description
Below is a brief explanation of the key columns in the dataset:

- **ID**: Unique ID for every installation (User ID).
- **first_open_date**: Date of the first time the user opened the game.
- **first_open_timestamp**: Timestamp of the first launch of the game (in UTC, Unix time in microseconds).
- **local_first_open_timestamp**: First open timestamp in the user's local timezone.
- **country**: Country of the user.
- **platform**: Platform of the user (Android or iOS).
- **device_category**: Category of the device (mobile or tablet).
- **device_brand**: Brand of the device.
- **device_model**: Model of the device.
- **has_ios_att_permission**: Whether the iOS user has given ATT permission (true/false). For Android users, this is false.
- **ad_network**: Ad network the user came from (null for organic users).
- **first_prediction**: An initial predicted value of the user in USD.
- **RetentionD{i}**: Boolean indicating whether the user launched the game on day `i`.
- **LevelAdvancedCountD{i}**: Number of levels completed by the user on day `i`.
- **Level_{i}_Duration**: Time it took the user to complete level `i` (null if not completed).
- **AdRevenueD{i}**: Amount of ad revenue the user generated on day `i` (USD).
- **IAPRevenueD{i}**: Amount of in-app purchase revenue the user generated on day `i` (USD).
- **TARGET**: Total amount of revenue the user generated in the first 90 days. **This is the target variable** you need to predict.

---

## Files Provided
The dataset is split into multiple files:

### Training
1. **users_train.csv**: Contains user metadata for each user, including columns like `ID`, `country`, `platform`, etc.
2. **user_features_train.csv**: Contains ingame behavior for the first 15 days (e.g., `RetentionD{i}`, `LevelAdvancedCountD{i}`, `AdRevenueD{i}`, `IAPRevenueD{i}`, etc.).
3. **targets_train.csv**: Contains the target variable (`TARGET`) for each user in the training set.

All training files share a common `ID` column to match data.

### Test
1. **users_test.csv**: Contains user metadata (same structure as `users_train.csv` but without target).
2. **user_features_test.csv**: Contains 15-day ingame behavior (same structure as `user_features_train.csv`, again no target).

### Sample Submission
- **sample_submission.csv**: Example of the required submission format.



## Getting Started
1. **Clone or Download** this repository.
2. **Install** necessary libraries/packages (e.g., pandas, numpy, scikit-learn, lightgbm, xgboost, etc.).
3. **Load** the CSV files into your environment (e.g., Python). Merge them on the `ID` column for training.
4. **Explore** and **clean** the data:
   - Handle missing values.
   - Convert data types.
   - Handle outliers if necessary.

---

## Approach Outline
1. **Data Merging**: Merge `users_train.csv`, `user_features_train.csv`, and `targets_train.csv` by `ID` for the training phase.
2. **Feature Engineering** (optional):
   - Aggregate daily metrics (e.g., sum of AdRevenueD{i} over 15 days) or compute day-to-day differences.
   - Encode categorical variables (e.g., country, device_brand).
   - Extract time-based features (e.g., day of week from `first_open_date`).
3. **Model Selection**:
   - Choose a regression model suitable for the data (Linear Regression, Random Forest, XGBoost, LightGBM, etc.).
   - Train on the 15-day data to predict the `TARGET` variable.
4. **Hyperparameter Tuning**: Optimize hyperparameters using cross-validation or a validation set.
5. **Prediction on Test Set**:
   - Prepare test data by merging `users_test.csv` and `user_features_test.csv` on `ID`.
   - Perform the same transformations (encoding, feature engineering) as in training.
   - Use the trained model to predict the day-90 revenue for each user in the test set.
6. **RMSE Evaluation**:
   - Compare predictions with actual values (on a hold-out set if available) and measure RMSE.

---

## Submission Format
- Your final submission should contain **two columns**:
  1. `ID`: Same as test dataset `ID`.
  2. `TARGET`: The predicted total revenue for day 90.

Below is an example (from `sample_submission.csv`):
```csv
ID,TARGET
123456,50.25
123457,10.75
123458,0
...
```

> **Note**: Ensure the `ID` values match exactly with `users_test.csv` and `user_features_test.csv`.

---

## Future Work
- **Feature Engineering**: Incorporate advanced features like retention rates, or daily revenue trends.
- **Ensemble Methods**: Combine multiple models for potentially better performance.
- **Time-Series Modeling**: If day-by-day data is available for more than 15 days, consider a time-series approach.
- **Automated Hyperparameter Optimization**: Tools like Optuna or Hyperopt can be used to systematically find best hyperparameters.

---


