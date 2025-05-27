# 🌞 Solar Panel Efficiency Prediction 🌞

Welcome to the **Solar Panel Efficiency Prediction** project! This repository contains code to predict solar panel efficiency using machine learning, based on the provided `train.csv` and `test.csv` datasets. The goal is to generate a submission file (`submission.csv`) with predictions for 12,000 test samples, evaluated using the metric:  
**Score = 100 * (1 - sqrt(MSE))** 🚀

---

## 📚 Project Overview

This project leverages **XGBoost** for regression, combined with robust data preprocessing and feature engineering to maximize prediction accuracy. The dataset includes:

- **Numerical features** (e.g., *irradiance*, *temperature*)
- **Categorical features** (e.g., *string_id*, *error_code*)

It tackles real-world challenges like missing values and invalid entries (e.g., `'unknown'`, `'error'`).

---

## 🎯 Objectives

- Predict solar panel **efficiency** for the test set.
- Generate a submission file with **12,000 rows** with columns: `id`, `efficiency`.
- Achieve a **high score** based on the evaluation metric.

---

## 🛠️ Approach

This project follows a streamlined pipeline combining:

1. **Data Cleaning**
2. **Feature Engineering**
3. **Model Training with XGBoost**

---

## 🧹 Data Preprocessing

- Convert numeric columns to proper types (handle `'unknown'`, `'error'` as NaN).
- Impute missing numerical values with **median**.
- Replace missing categorical values with **'Unknown'**.
- Cap `cloud_coverage` at **100**.
- Ensure `soiling_ratio` is between **0 and 1**.

---

## ⚙️ Feature Engineering

| Feature Name        | Description |
|---------------------|-------------|
| `power_output`      | `voltage * current`: Captures electrical output 🔌 |
| `temp_diff`         | `module_temperature - temperature`: Models thermal effects 🌡️ |
| `degradation_rate`  | `panel_age / (maintenance_count + 1)`: Accounts for wear 🕰️ |
| `has_error`         | Binary: `1` if `error_code != 'E00'`, else `0` 🚨 |
| `soiling_impact`    | `1 - soiling_ratio`: Efficiency loss from dust 💨 |
| `effective_irradiance` | `irradiance * (1 - cloud_coverage / 100)`: Adjusts solar input ☁️ |

---

## 🤖 Model Training

- Use **XGBoost** for its robustness with tabular data and native support for missing values.
- Build a **pipeline** with:
  - `SimpleImputer (median)`
  - `StandardScaler`
  - `OneHotEncoder`
- Perform **GridSearchCV** over:
  - `n_estimators`
  - `max_depth`
  - `learning_rate`
- Use **5-fold cross-validation**
- Evaluate using a **custom metric**:  
  `Score = 100 * (1 - sqrt(MSE))`

---

## 🛠️ Tools Used

- **Python Libraries**
  - `pandas` – Data manipulation 📊
  - `numpy` – Numerical operations 🔢
  - `scikit-learn` – Preprocessing, pipelines, evaluation 🧰
  - `xgboost` – ML model 🌲

---

## 🎉 Conclusion

This project delivers a **robust, scalable solution** for predicting solar panel efficiency. By combining domain-driven features, powerful modeling, and solid preprocessing, it offers reliable results that can support:

- **Real-world solar energy optimization**
- **Sustainable clean energy initiatives**

