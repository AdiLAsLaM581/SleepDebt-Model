
# Sleep Debt Classification – Machine Learning Model Comparison

A machine learning project focused on classifying sleep debt levels using lifestyle and sleep-related data. The project compares multiple classification algorithms, performs hyperparameter tuning, evaluates model stability, and selects the best-performing model using Macro F1-score.

## Project Overview

The objective is to predict a person's sleep debt category based on relevant lifestyle and sleep-related features.

The target variable, `sleep_debt_category`, contains four classes:

- Mild Deficit
- Moderate Debt
- Optimal Recovery
- Severe Sleep Debt

The project emphasizes model comparison, cross-validation, hyperparameter optimization, and evaluation on an independent test dataset.

## Dataset

- **Dataset:** `bedtime_screentime_sleep_debt.csv`
- **Source:** Kaggle
- **Records:** 8,500
- **Features:** 18 columns
- **Target:** `sleep_debt_category`

### Data Preprocessing

The preprocessing workflow included:

- Removing duplicate records.
- Handling missing values.
- Excluding the `user_id` identifier.
- Removing leakage-related features, including `total_sleep_hours`, `sleep_latency_min`, `deep_sleep_pct`, and `next_day_fatigue_score`.
- Encoding categorical features and preparing numerical features.
- Splitting the dataset into 80% training and 20% testing data.

Five-fold cross-validation was performed using the training data. The independent test set was reserved for final evaluation.

## Models Compared

Four classification algorithms were evaluated using five-fold cross-validation.

| Model | CV Macro F1 |
|---|---:|
| Gradient Boosting | **0.7284** |
| Random Forest | 0.7141 |
| Decision Tree | 0.6345 |
| K-Nearest Neighbors (KNN) | 0.5593 |

Gradient Boosting achieved the highest initial cross-validation Macro F1-score.

## Hyperparameter Tuning

Hyperparameter tuning was performed to improve model performance.

| Model | Best Parameters | Tuned CV Macro F1 |
|---|---|---:|
| KNN | K = 3 | 0.5683 |
| Decision Tree | max_depth = 5 | 0.6955 |
| Random Forest | n_estimators = 100, max_depth = None | 0.7141 |
| Gradient Boosting | learning_rate = 0.2, n_estimators = 50 | **0.7286** |

GridSearchCV was used for Random Forest, while the other models were evaluated with their respective parameter configurations.

## Overfitting and Model Stability

The tuned models were further evaluated using training and validation scores from five-fold cross-validation.

| Model | CV Train Score | CV Validation Score | Gap |
|---|---:|---:|---:|
| Random Forest | 1.0000 | 0.7141 | 0.2859 |
| KNN | 0.7601 | 0.5683 | 0.1918 |
| Gradient Boosting | 0.7980 | **0.7286** | 0.0694 |
| Decision Tree | 0.7096 | 0.6955 | 0.0142 |

Random Forest showed the largest training-validation gap, indicating substantial overfitting. Gradient Boosting provided the strongest balance between validation performance and generalization.

## Final Model Evaluation

**Selected Model: Gradient Boosting**

The final model was evaluated on the independent 20% holdout test dataset.

| Metric | Score |
|---|---:|
| CV Macro F1 | 0.7286 |
| Test Macro F1 | **0.7323** |
| Test Accuracy | **76.29%** |

### Classification Report

| Class | Precision | Recall | F1-Score |
|---|---:|---:|---:|
| Mild Deficit | 0.57 | 0.61 | 0.59 |
| Moderate Debt | 0.85 | 0.86 | 0.85 |
| Optimal Recovery | 0.76 | 0.69 | 0.72 |
| Severe Sleep Debt | 0.81 | 0.71 | 0.76 |
| **Macro Average** | **0.75** | **0.72** | **0.73** |
| **Weighted Average** | **0.77** | **0.76** | **0.76** |

### Confusion Matrix

Rows represent actual classes, while columns represent predicted classes.

| Actual / Predicted | Mild | Moderate | Optimal | Severe |
|---|---:|---:|---:|---:|
| Mild Deficit | 245 | 96 | 60 | 0 |
| Moderate Debt | 103 | 768 | 1 | 21 |
| Optimal Recovery | 82 | 3 | 192 | 0 |
| Severe Sleep Debt | 0 | 37 | 0 | 92 |

The model performed best on the Moderate Debt class. Severe Sleep Debt achieved 0.71 recall, meaning the model identified approximately 71% of actual severe cases. Improving recall for this class is a potential area for future work.

## Key Findings

- Gradient Boosting achieved the highest tuned cross-validation Macro F1-score.
- Random Forest showed signs of overfitting, with a training-validation gap of 0.2859.
- Gradient Boosting maintained a relatively small gap of 0.0694.
- The final test Macro F1-score was 0.7323, slightly higher than its cross-validation score.
- Class-level evaluation revealed that Mild Deficit and Severe Sleep Debt need further improvement.

## Conclusion

Gradient Boosting was selected as the final model because it achieved the highest cross-validation Macro F1-score and demonstrated a reasonable balance between model performance and generalization.

The independent test evaluation produced a Macro F1-score of 0.7323 and an accuracy of 76.29%. Further improvements could focus on increasing recall for the Severe Sleep Debt and Mild Deficit categories.

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib / Seaborn
- Jupyter Notebook
