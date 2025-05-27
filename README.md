🌞 Solar Panel Efficiency Prediction 🌞
Welcome to the Solar Panel Efficiency Prediction project! This repository contains code to predict solar panel efficiency using machine learning, based on the provided train.csv and test.csv datasets. The goal is to generate a submission file (submission.csv) with predictions for 12,000 test samples, evaluated using the metric: Score = 100 * (1 - sqrt(MSE)). 🚀
📚 Project Overview
The project leverages XGBoost for regression, combined with robust data preprocessing and feature engineering to maximize prediction accuracy. The dataset includes numerical features (e.g., irradiance, temperature) and categorical features (e.g., string_id, error_code), with challenges like missing values and invalid entries (e.g., 'unknown', 'error'). 🧠
🎯 Objectives

Predict solar panel efficiency for the test set.
Generate a submission file with 12,000 rows and columns id, efficiency.
Achieve a high score based on the evaluation metric.

🛠️ Approach
The approach combines data cleaning, feature engineering, and a tuned machine learning model:

Data Preprocessing 🧹

Convert numerical columns to numeric types, handling invalid values (e.g., 'unknown' in pressure, 'error' in humidity) by converting to NaN.
Impute missing numerical values with the median.
Replace missing categorical values (error_code, installation_type) with 'Unknown'.
Cap cloud_coverage at 100 and ensure soiling_ratio is between 0 and 1.

Feature Engineering ⚙️

power_output = voltage * current: Captures electrical output. 🔌
temp_diff = module_temperature - temperature: Models thermal effects. 🌡️
degradation_rate = panel_age / (maintenance_count + 1): Accounts for panel wear. 🕰️
has_error: Binary indicator (1 if error_code != 'E00', else 0). 🚨
soiling_impact = 1 - soiling_ratio: Represents efficiency loss due to dust. 💨
effective_irradiance = irradiance * (1 - cloud_coverage / 100): Adjusts for cloud cover. ☁️

Model Training 🤖

Use XGBoost for its robustness with tabular data and handling of missing values.
Apply a preprocessing pipeline with SimpleImputer (median), StandardScaler, and OneHotEncoder.
Perform hyperparameter tuning with grid search over n_estimators, max_depth, and learning_rate.
Evaluate using 5-fold cross-validation and the custom metric.


Submission 📄

Generate predictions for the test set.
Save as submission.csv with 12,000 rows (id, efficiency).



🧩 Feature Engineering Details
The engineered features capture domain-specific relationships:

Power Output: Approximates electrical output, critical for efficiency. ⚡
Temperature Difference: Higher module temperatures reduce efficiency. 🔥
Degradation Rate: Models long-term wear relative to maintenance frequency. 🛠️
Error Indicator: Simplifies error codes into a binary feature. ✅
Soiling Impact: Quantifies efficiency retention after dust accumulation. 🧼
Effective Irradiance: Adjusts solar input for cloud cover, a key efficiency driver. 🌞

🛠️ Tools Used

Python Libraries 📦
pandas: Data manipulation and loading.
numpy: Numerical operations.
scikit-learn: Preprocessing, pipeline, and evaluation.
xgboost: Regression model.

🌟 Future Improvements

Feature Selection: Use XGBoost feature importance to drop low-impact features. 📉
Ensembling: Combine XGBoost with LightGBM for better predictions. 🤝
Outlier Handling: Apply robust scaling or anomaly detection. 🛡️
Neural Networks: Experiment with deep learning for complex patterns. 🧠

📬 Contact
For issues or suggestions, open a GitHub issue or contact the repository owner. Happy predicting! 🎉
🎉 Conclusion
This project successfully delivers a robust solution for predicting solar panel efficiency, achieving high accuracy through careful data preprocessing, domain-driven feature engineering, and a tuned XGBoost model. By addressing challenges like missing values and invalid entries, the model provides reliable predictions for real-world solar energy applications. The approach not only meets the competition requirements but also lays a foundation for further enhancements, such as ensembling or advanced outlier handling, to push performance even higher. This work contributes to optimizing solar energy systems, supporting a sustainable future powered by clean energy. 🌍
