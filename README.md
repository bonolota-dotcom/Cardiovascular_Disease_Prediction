# Cardiovascular Disease Prediction

## Overview

This project explores a cardiovascular disease classification dataset and demonstrates a structured, end-to-end beginner/intermediate data-science workflow. The primary goal is to analyze clinical and lifestyle risk factors, evaluate baseline machine learning models, and investigate the impact of controlled data cleaning on predictive performance.

## Objectives

- **Data Understanding**: Inspect structure, types, summary statistics, and missing values across features.
- **Exploratory Data Analysis (EDA)**: Visualize distributions and examine relationships between predictors and target status.
- **Data-Quality Investigation**: Identify extreme, suspicious, and physically inconsistent observations.
- **Feature Preparation & Standardization**: Format features and standardize numerical inputs where appropriate.
- **Model Evaluation**: Train baseline Logistic Regression and Decision Tree classifiers, evaluating performance via Accuracy, Precision, Recall, F1 Score, and ROC-AUC.
- **Controlled Cleaning Experiment**: Quantify how removing strictly invalid observations affects evaluation metrics.
- **Feature Importance & Interpretation**: Analyze predictor contributions while maintaining appropriate non-causal distinctions.

## Dataset

- **Observations**: 68,205 rows
- **Features**: 17 original columns (including demographic, vital sign, and laboratory variables)
- **Target Variable**: `cardio` (binary: `0` = absent, `1` = present)
- **Raw Data Availability**: The raw CSV dataset is intentionally **not** tracked in this repository.
- **Source**: [Kaggle - Cardiovascular Disease Dataset](https://www.kaggle.com/datasets/colewelkins/cardiovascular-disease)

## Project Workflow

1. **Data Loading & Understanding**: Loading dataset and validating feature types.
2. **Exploratory Data Analysis**: Analyzing target distribution, age trends, BMI, blood pressure categories, and risk factor relationships.
3. **Data-Quality Investigation**: Quantile inspection of extreme values for height, weight, BMI, and blood pressure (`ap_hi`, `ap_lo`).
4. **Data Preprocessing & Encoding**: Extracting relevant predictors and scaling continuous inputs for linear models.
5. **Train/Test Split**: Applying an 80/20 stratified split to preserve target class proportions.
6. **Model Training**:
   - Logistic Regression (standardized features)
   - Decision Tree Classifier (unpruned, unscaled features)
7. **Model Evaluation**: Computing confusion matrices, ROC curves, and classification metrics.
8. **Controlled Data Cleaning**: Removing 65 clearly inconsistent records (`ap_lo >= ap_hi`) and re-evaluating both models.
9. **Feature Importance Interpretation**: Ranking feature contributions based on Gini impurity reduction.
10. **Limitations & Conclusion**: Documenting dataset boundaries, modeling constraints, and key insights.

## Models Evaluated

- **Logistic Regression**: A linear classification model using standardized feature scaling.
- **Decision Tree Classifier**: An unpruned decision tree using original feature scales.

## Results

Evaluation metrics obtained on the 20% test split:

| Model | Dataset | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Logistic Regression** | Original | 0.729932 | 0.758125 | 0.665132 | 0.708590 | 0.790769 |
| **Logistic Regression** | Cleaned | 0.726299 | 0.750042 | 0.668203 | 0.706761 | 0.790526 |
| **Decision Tree** | Original | 0.640496 | 0.641247 | 0.616870 | 0.628822 | 0.640575 |
| **Decision Tree** | Cleaned | 0.627825 | 0.625856 | 0.611714 | 0.618704 | 0.628109 |

## Key Findings

- **Target Balance**: Target classes were approximately balanced (50.6% negative vs 49.4% positive).
- **EDA Trends**: Higher cardiovascular disease prevalence was observed among older age groups, higher BMI categories, elevated blood pressure tiers, and higher cholesterol levels.
- **Model Comparison**: Logistic Regression demonstrated higher overall predictive discrimination (ROC-AUC 0.7908) compared to the unpruned Decision Tree (ROC-AUC 0.6406) on the evaluated test set.
- **Controlled Cleaning Impact**: Removing 65 clearly inconsistent records (`ap_lo >= ap_hi`) improved dataset consistency but did not increase predictive performance on the test split.
- **Feature Importance**: Gini importance in the Decision Tree was heavily concentrated in `ap_hi`, `bmi`, `age_years`, `weight`, and `height`.
- **Association vs Causation**: Feature importance scores reflect statistical predictive utility within these decision trees, not direct physiological causation.

## Limitations

- **Single Dataset**: Findings are based on a single public dataset and may not generalize across diverse real-world clinical populations.
- **Ambiguous Extreme Records**: Plausible but extreme physiological values were retained to avoid arbitrary data removal, which may leave some measurement noise.
- **Baseline Models**: Analysis is limited to two baseline models without hyperparameter tuning or cross-validation.
- **Split Sensitivity**: Evaluation is derived from a single 80/20 train/test split.
- **Educational Context**: This repository is designed strictly as an educational data science portfolio project, not as a clinical diagnostic tool.

## Reproducibility

To run the analysis locally:

1. Download the dataset from the [Kaggle dataset page](https://www.kaggle.com/datasets/colewelkins/cardiovascular-disease).
2. Place `cardio_data_processed.csv` in the root directory or in `data/`.
3. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```
4. Open and run the Jupyter notebook:
   ```bash
   jupyter notebook notebooks/CardiovascularDiseasePrediction.ipynb
   ```

## Ownership & Usage Notice

This repository is published solely as a personal data science portfolio project. No open-source software license is granted at this time. All rights are reserved by the repository owner.
