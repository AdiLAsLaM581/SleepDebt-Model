# Week 3 — Supervised Machine Learning Models

## Project Summary

This project uses a bedtime screen-time and sleep-debt dataset to predict sleep debt categories.  
The data is cleaned, missing values are handled, categorical features are encoded, and the data is split into training and testing sets.  
KNN, Decision Tree, and Logistic Regression are trained and evaluated using accuracy, precision, recall, F1-score, and confusion matrices.

## Dataset

- **Dataset name:** `bedtime_screentime_sleep_debt.csv`
- **Rows:** 8,500
- **Original columns:** 18
- **Target column:** `sleep_debt_category`
- **Classes:** Mild Deficit, Moderate Debt, Optimal Recovery, Severe Sleep Debt
- **Source:** Dataset file used for the Week 2 assignment.

## Results

The Decision Tree with `max_depth=3` achieved the highest test accuracy of **100%** in this experiment. This result should be checked for possible target leakage before being treated as reliable generalization performance.

| Model | Accuracy |
|---|---:|
| KNN (K=11) | 74.24% |
| Decision Tree (depth=3) | 100.00% |
| Logistic Regression | 98.06% |

## How to Run

1. Install Python and Jupyter Notebook.
2. Download or clone this repository.
3. Install the required packages using `pip install -r requirements.txt`.
4. Keep the CSV dataset in the same folder as the notebook.
5. Open `Week3_SleepDebt.ipynb` in Jupyter Notebook and run the cells from top to bottom.

## Tools Used

Python, Pandas, Matplotlib, Seaborn, and Scikit-learn.
