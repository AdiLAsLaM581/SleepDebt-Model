# Sleep Debt & Late-Night Phone Habits Analysis

## Project Overview
This repository contains an end-to-end data preparation and preprocessing pipeline built in Python using Google Colab. The goal of this project is to clean, transform, and preprocess behavioral survey data regarding late-night smartphone usage and sleep patterns, preparing it for supervised machine learning classification models.

## Dataset Information
* **Dataset Name:** Sleep Debt & Late Night Phone Habits Dataset
* **Source:** [Kaggle Public Repository](https://www.kaggle.com/datasets/samartalwar/sleep-debt-and-screen-time-late-night-phone-habits)
* **Dataset Size:** 8,500 rows, 18 columns
* **Target Variable:** `sleep_debt_category` (Multiclass Classification: *Optimal Recovery*, *Mild Deficit*, *Moderate Debt*, *Severe Sleep Debt*)
* **Feature Types:** Numerical (age, screen time, screen brightness, caffeine, sleep latency, fatigue score, etc.) and Categorical (gender, occupation, chronotype, bedtime app).

---

## Key Pipeline Steps Included

1. **Load & Exploratory Data Analysis (EDA):**
   * Statistical summaries (`info()`, `describe()`, `head()`)
   * Class distribution analysis using Seaborn `countplot`
   * Visualizations: Boxplots comparing phone usage across sleep debt classes, Sleep Latency histograms, and numerical feature correlation heatmaps.

2. **Data Cleaning & Missing Value Imputation:**
   * Duplicate record detection and removal.
   * Visualization of missing value counts per column.
   * Dropped arbitrary identifier column (`user_id`).
   * Imputed numerical columns (`sleep_latency_min`, `caffeine_post_5pm_mg`) using the **median** to handle skewness.
   * Imputed categorical columns (`primary_bedtime_app`) using the **mode**.

3. **Feature Engineering:**
   * `screen_impact_score`: Combines bedtime phone usage duration with screen brightness percentage.
   * `sleep_efficiency_ratio`: Ratio of actual sleep time versus overall time spent in bed.

4. **Train/Test Splitting & Stratification:**
   * 80/20 train/test split (`random_state=42`).
   * Applied `stratify=y` to maintain target class proportions (~52.5% Moderate Debt, ~23.6% Mild Deficit, ~16.3% Optimal Recovery, ~7.6% Severe Sleep Debt) across both sets.

5. **Pipeline Preprocessing (Data Leakage Prevention):**
   * Encapsulated `StandardScaler` for numerical features and `OneHotEncoder` for categorical features using Scikit-Learn `ColumnTransformer` and `Pipeline`.
   * Executed `fit_transform()` strictly on `X_train` and `transform()` on `X_test` to prevent test-set data leakage.

---

## How to Run the Notebook

### Option 1: Running in Google Colab (Recommended)
1. Upload `bedtime_screentime_sleep_debt.csv` to your Google Colab environment or Google Drive.
2. Open `SleepDebt.ipynb` in Google Colab.
3. Execute all cells top-to-bottom sequentially (`Runtime` > `Run all`).

### Option 2: Local Jupyter Notebook
1. Clone this repository:
   ```bash
   git clone [https://github.com/AdiLAsLaM581/SleepDebt-Model.git]
   cd SeepDebt-Model
   