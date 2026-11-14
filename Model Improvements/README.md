# Severe Sleep Debt Detection

A machine learning project that uses sleep habits and screen-time data to identify individuals at risk of severe sleep debt.

## Overview

Sleep habits, late-night phone usage, caffeine consumption, and other lifestyle factors can influence sleep quality. This project explores how machine learning can use these patterns to identify individuals with **Severe Sleep Debt**.

The original four-category classification problem was converted into a binary classification task:

- `1` – Severe Sleep Debt
- `0` – All Other Categories

The main focus was improving the detection of severe cases while maintaining a reasonable balance between precision and recall.

## Dataset

**Source:** [Sleep Debt and Screen Time – Kaggle](https://www.kaggle.com/datasets/samartalwar/sleep-debt-and-screen-time-late-night-phone-habits)

| Property | Details |
|---|---|
| Records | 8,500 |
| Original Features | 18 |
| Target Variable | `sleep_debt_category` |
| Problem Type | Binary Classification |
| Training Split | 80% |
| Testing Split | 20% |

## Machine Learning Workflow

The project follows these main steps:

1. **Data Preparation:** Inspected the dataset, handled missing values, and removed the user identifier and suspected target leakage features.
2. **Target Transformation:** Converted the four original sleep debt categories into a binary target.
3. **Preprocessing:** Applied median imputation to numerical features, most-frequent imputation to categorical features, and One-Hot Encoding.
4. **Baseline Evaluation:** Established initial performance using a Dummy Classifier and Random Forest.
5. **Error Analysis:** Examined false negatives and false positives to understand classification errors.
6. **Model Improvement:** Experimented with class balancing, resampling, feature reduction, and classification threshold tuning.
7. **Final Evaluation:** Evaluated the selected model on the held-out test dataset.

## Model Experiments

Random Forest was selected as the main model for experimentation. Different strategies were evaluated using cross-validation.

| Experiment | Precision | Recall | F1 Score |
|---|---:|---:|---:|
| Baseline Random Forest | 0.8252 | 0.6834 | 0.7476 |
| Balanced Random Forest | 0.8179 | 0.6158 | 0.7026 |
| Random Forest with Resampling | 0.7510 | 0.7394 | 0.7451 |
| Reduced Features | 0.7783 | 0.6911 | 0.7321 |
| Random Forest (Threshold 0.4) | 0.7562 | 0.7664 | 0.7613 |

Threshold tuning provided a useful improvement in recall, making it a promising approach for detecting more severe cases.

## Final Model Performance

The improved Random Forest model used a classification threshold of **0.4** instead of the default 0.5.

| Metric | Baseline Model | Improved Model |
|---|---:|---:|
| Accuracy | 0.9706 | 0.9700 |
| Precision | 0.8835 | 0.8047 |
| Recall | 0.7054 | 0.7984 |
| F1 Score | 0.7845 | 0.8016 |

<details>
<summary>Final confusion matrix results</summary>

| Result | Count |
|---|---:|
| True Positives | 103 |
| True Negatives | 1,546 |
| False Positives | 25 |
| False Negatives | 26 |

</details>

The improved model increased recall from **70.54% to 79.84%** and improved the F1 score from **0.7845 to 0.8016**, while maintaining nearly the same accuracy.

This improvement came with a decrease in precision, meaning the model produced more false alarms in exchange for missing fewer severe cases.

## Feature Importance

The Random Forest model identified the following features as its most influential:

| Feature | Importance |
|---|---:|
| Morning Alarm Snoozes | 0.3611 |
| Bedtime Phone Minutes | 0.2481 |
| Screen Brightness | 0.0567 |
| REM Sleep Percentage | 0.0507 |
| Physical Activity Minutes | 0.0484 |

Morning alarm snoozes and bedtime phone usage had the highest importance scores in the model.

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook

## Key Takeaways

- Accuracy can be misleading when the target classes are imbalanced.
- Recall is particularly important when the objective is to detect severe cases.
- Classification threshold tuning can improve the balance between precision and recall.
- Error analysis helps identify where a model struggles.
- Feature importance provides insight into which variables contribute most to predictions.

## Limitations

- Model predictions depend on the quality and representativeness of the dataset.
- Feature importance does not establish a causal relationship.
- The model has not been validated for real-world clinical use.
- Predictions should not be treated as medical advice or diagnosis.

## Author

**M. Adil Aslam**

[GitHub Profile](https://github.com/AdiLAsLaM581)  
[Project Repository](https://github.com/AdiLAsLaM581/SleepDebt-Model)
