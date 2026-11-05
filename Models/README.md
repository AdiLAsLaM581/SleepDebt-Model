# Week 3 — Supervised Machine Learning Models

## Project Summary

This project uses a bedtime screen-time and sleep-debt dataset to predict sleep debt categories using supervised machine learning.

The dataset is cleaned, missing values are handled, categorical features are encoded, and the data is split into training and testing sets.

Three machine learning models are trained and evaluated: K-Nearest Neighbors (KNN), Decision Tree, and Logistic Regression.

During evaluation, unusually high initial scores raised concerns about possible target leakage. To address this, four suspected leakage features were removed and the models were retrained. Model parameters were selected using cross-validation on the training data, while the test set was reserved for final evaluation.

## Dataset

- **Dataset name:** `bedtime_screentime_sleep_debt.csv`
- **Rows:** 8,500
- **Original columns:** 18
- **Target column:** `sleep_debt_category`
- **Classes:** Mild Deficit, Moderate Debt, Optimal Recovery, Severe Sleep Debt
- **Source:** Dataset file used for the Week 2 assignment.

## Data Preprocessing

- Handled missing numerical values using the median.
- Handled missing categorical values using the most frequent value.
- Removed duplicate records (none were found).
- Removed `user_id`.
- Encoded categorical features.
- Removed four suspected target leakage features:
  - `total_sleep_hours`
  - `sleep_latency_min`
  - `deep_sleep_pct`
  - `next_day_fatigue_score`
- Split the dataset into 80% training and 20% testing sets.

## Model Results

After removing the suspected target leakage features, the models achieved the following test results:

| Model | Accuracy | Precision (Macro) | Recall (Macro) | F1 (Macro) |
|---|---:|---:|---:|---:|
| KNN (K=3) | 63.94% | 62.22% | 52.94% | 55.55% |
| Decision Tree (depth=5) | 74.24% | 72.53% | 70.69% | 71.40% |
| Logistic Regression | **77.41%** | **75.81%** | **73.70%** | **74.69%** |

Logistic Regression achieved the best overall performance, with the highest accuracy and macro F1-score among the three models.

## Best Model

**Logistic Regression** was selected as the best-performing model based on the corrected test results.

Its confusion matrix showed the following correct predictions:

- Mild Deficit: 244
- Moderate Debt: 776
- Optimal Recovery: 199
- Severe Sleep Debt: 97

For the Severe Sleep Debt category, Logistic Regression achieved 75.19% recall, compared with 67.44% for Decision Tree and 32.56% for KNN.

## Model Selection

- **KNN:** K was selected using 5-fold cross-validation with GridSearchCV.
- **Decision Tree:** Maximum tree depth was selected using 5-fold cross-validation with GridSearchCV.
- **Logistic Regression:** Evaluated using the same revised feature set.

The test set was reserved for final model evaluation rather than parameter selection.

## How to Run

1. Install Python and Jupyter Notebook.
2. Download or clone this repository.
3. Install the required packages using `pip install -r requirements.txt`.
4. Keep the CSV dataset in the same folder as the notebook.
5. Open `Week3_SleepDebt_Updated.ipynb` in Jupyter Notebook.
6. Run the cells from top to bottom.

## Tools Used

Python, Pandas, NumPy, Matplotlib, Seaborn, and Scikit-learn.

## Key Learning Outcomes

- Data cleaning and preprocessing.
- Handling missing values and categorical encoding.
- Training and evaluating supervised machine learning models.
- Understanding confusion matrices and classification metrics.
- Identifying and addressing possible target leakage.
- Using cross-validation for hyperparameter selection.
- Comparing models using macro precision, recall, and F1-score.
