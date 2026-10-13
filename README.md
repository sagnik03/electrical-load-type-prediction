# Load Type Classification

This project develops a machine learning solution for predicting the electrical load category of a power system based on historical operating data. The target variable is `Load_Type`, which includes three classes:

- `Light_Load`
- `Medium_Load`
- `Maximum_Load`

The solution is designed as an academic machine learning assignment and follows a realistic forecasting setup: the last chronological month in the dataset is held out as the final test set, while all preprocessing and model fitting are performed only on earlier data.

## Objective

The goal is to build a classifier that can predict the load category using operational and time-related attributes such as energy consumption, reactive power, CO2, power factor, and timestamp-derived features.

## Dataset

The project uses the dataset in [data/load_data.csv](data/load_data.csv), which contains historical power-system measurements over the full year 2018. The data includes:

- `Date_Time`
- `Usage_kWh`
- `Lagging_Current_Reactive.Power_kVarh`
- `Leading_Current_Reactive_Power_kVarh`
- `CO2(tCO2)`
- `Lagging_Current_Power_Factor`
- `Leading_Current_Power_Factor`
- `NSM`
- `Load_Type`

The dataset spans the full year and is labeled for supervised classification. The final month is reserved for evaluation, which avoids random train/test leakage and better reflects a real-world deployment scenario.

## Workflow

The notebook performs the following steps:

1. Data loading and basic inspection
2. Date parsing and temporal ordering
3. Train/test split using the last month as the test set
4. Data preprocessing and imputation
5. Feature engineering from timestamp information
6. Exploratory data analysis (EDA)
7. Baseline model training
8. Model comparison using multiple classifiers
9. Evaluation using classification metrics
10. Interpretation of results and findings

## Validation Strategy

To prevent data leakage, the notebook follows this process:

- sort the data by time
- keep the final calendar month as the test set
- fit preprocessing steps and models only on the remaining earlier months
- evaluate only once on the held-out last month

This is important because random splits can create unrealistic performance estimates when the data has temporal structure.

## Models Compared

The notebook compares a simple baseline with several standard classification models, including:

- Dummy classifier (most frequent baseline)
- Logistic Regression
- Random Forest
- Gradient Boosting

These models are trained in a sklearn pipeline so preprocessing is consistently applied to the training data only.

## Metrics Reported

The project reports the following metrics on the final test set:

- Accuracy
- Precision
- Recall
- F1-score
- Classification report
- Confusion matrix

Macro-averaged metrics are used to provide a balanced evaluation across the three load classes.

## Files in the Project

- [data/load_data.csv](data/load_data.csv): source dataset
- [load_type_classification.ipynb](load_type_classification.ipynb): main notebook with the full workflow
- [requirements.txt](requirements.txt): required Python packages
- [README.md](README.md): project overview and usage instructions

## Running the Project

### 1. Create a virtual environment (optional but recommended)

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Install required dependencies

```bash
pip install -r requirements.txt
```

### 3. Open the notebook

Open [load_type_classification.ipynb](load_type_classification.ipynb) in VS Code or Jupyter Notebook and run all cells from top to bottom.

### 4. Reproduce the results

The notebook is designed to run end-to-end without manual editing. It reads the CSV file, performs the split, trains the models, and prints the evaluation metrics automatically.

## Notes

- The notebook is intentionally kept simple and readable for academic use.
- It avoids unnecessary complexity while still covering the main ML pipeline steps required for a classification assignment.
- No random final test split is used; the evaluation is based on a true time-based holdout.

## Expected Outcome

The objective is to achieve a model that performs noticeably better than the baseline on the final month of unseen data. A model that generalizes well to recent load conditions should be able to distinguish among `Light_Load`, `Medium_Load`, and `Maximum_Load` with acceptable classification accuracy and balanced class performance.
