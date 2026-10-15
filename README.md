# ML-Assignment
Fundamentals of Machine Learning Programming Assignment
# Predicting Student Dropout and Academic Success

**Fundamentals of Machine Learning – Programming Assignment**

A supervised machine learning project that classifies higher-education students as **Dropout**, **Enrolled** or **Graduate**, and compares two distinct algorithms: **Logistic Regression** and **Random Forest**.

## Team

| Member | Student ID | Email | Algorithm |
|---|---|---|---|
| `Thuiyadura L.R` | `MS26923956` | `ms26923956@my.sliit.lk` | Logistic Regression |
| `Nissanka H.M.D.P` | `MS26930190` | `ms26930190@my.sliit.lk` | Random Forest |

## Problem

Student dropout is a major problem in higher education. This project builds classification models that predict a student's outcome at the end of the normal duration of the course, so that students at risk can be identified early and supported.

- **Learning type:** Supervised learning (multi-class classification)
- **Target:** `Target` (Dropout / Enrolled / Graduate)
- **Constraint:** Only classical machine learning is used (no deep learning)

## Dataset

- **Name:** Predict Students' Dropout and Academic Success
- **Source:** UCI Machine Learning Repository – https://archive.ics.uci.edu/dataset/697
- **License:** CC BY 4.0
- **Size:** 4,424 students, 36 features + 1 target column
- **Content:** Demographic, socioeconomic and academic-path information known at enrollment, plus academic performance at the end of the 1st and 2nd semesters, and macroeconomic indicators (unemployment rate, inflation rate, GDP)
- **Class distribution:** Graduate ~50%, Dropout ~32%, Enrolled ~18% (imbalanced)
- **Missing values / duplicates:** none
- **Format note:** the CSV is semicolon-separated, so it is loaded with `pd.read_csv('data.csv', sep=';')`


## Repository Structure

```
.
├── data/
│   └── data.csv                     # dataset (also linked in submission.txt)
├── notebooks/
│   ├── logistic_regression.ipynb   # Thuiyadura L.R
│   ├── random_forest.ipynb # Nissanka H.M.D.P
├── report/
│   └── MS26923956_MS26930190 .pdf
├── results/
│   └── logistic_regression_results.json
│   └── random_forest_results.json
├── requirements.txt
└── README.md
```

## Methodology

1. **Data loading and cleaning:** correct delimiter, strip whitespace from column names, check for missing values, duplicates and outliers.
2. **Preprocessing:**
   - One-hot encoding of integer-coded categorical features (e.g. `Course`, `Application mode`, `Marital status`)
   - Scaling of numeric features
   - Stratified train/test split with a fixed `random_state`
3. **Models:**
   - **Logistic Regression** (multinomial): an interpretable linear baseline
   - **Random Forest:** a non-linear ensemble of decision trees
4. **Hyperparameter tuning:** cross-validated search on the training set only.
5. **Evaluation:** both models are tested on the same untouched test set using accuracy, per-class precision, recall and F1, macro-F1, and confusion matrices. Class imbalance is handled with class weights.

## Results

| Metric | Logistic Regression | Random Forest |
|---|---|---|
| Accuracy | 0.734 | 0.759 |
| Macro-F1 | 0.696 | 0.703 |
| Macro-AUC (one-vs-rest) | 0.884 | 0.887 |
| Recall of "Enrolled" | 0.635 | 0.509 |


## How to run
1. `pip install -r requirements.txt`
2. Run `random_forest.ipynb` and `logistic_regression.ipynb` top to bottom. Each saves its JSON file in `results/`.
3. The comparison cells in Section 7.4 of `logistic_regression.ipynb` read both JSON files, so run that notebook last.

Both notebooks use `random_state=42` and the same split, so the comparison is fair. 

**Main libraries:** `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`

| | **Member 1** | **Member 2** |
|---|---|---|
| **Name** | `Thuiyadura L.R` | `Nissanka H.M.D.P` |
| **Student ID** | `MS26923956` | `MS26930190` |
| **Algorithm** | `Logistic Regression` | `Random Forest` |
| **Notebook** | `logistic_regression.ipynb` | `random_forest.ipynb` |
| **GitHub branch** | `thuiyadura-lr-ms26923956` | `nissanka-hmdp-ms26930190` |

### Shared work (both members)
| Task | Done by |
|---|---|
| Dataset selection and checking it against the assignment requirements | Both |
| Agreeing the shared settings: `random_state=42`, stratified 80/20 train/test split, same one-hot encoding, macro-F1 for tuning | Both |
| Repository structure and branches (`main`, `final-development`, one branch per member) | Both |
| Comparison of the two algorithms (Table A, Table B and the discussion in Section 7.4) | Both |
| Final report (PDF), `members.txt` and `submission.txt` | Both |

### Individual work
| Task | Member 1: Logistic Regression | Member 2: Random Forest |
|---|---|---|
| Data cleansing, validity checks and outlier analysis | Missing values, duplicates, range and consistency checks, IQR outlier analysis, decision to keep outliers (limited by L2 regularisation) | Missing values, duplicates, IQR outlier analysis, decision to keep outliers (trees split on thresholds, so they are robust to outliers) |
| Exploratory analysis | Class distribution, boxplots by outcome, correlation matrix, VIF (multicollinearity) | Class distribution, boxplots by outcome, correlation matrix |
| Model-specific preprocessing | Standardisation of continuous features inside a `Pipeline` (no data leakage), PCA analysis | No scaling needed for trees; feature selection by importance instead of PCA |
| Algorithm background and justification | Logistic Regression (softmax, regularised loss, `C`) | Random Forest (decision tree and Gini impurity, bagging, random feature subsets, out-of-bag estimate) |
| Hyperparameter tuning | `GridSearchCV` over `C` and `class_weight`, scored by macro-F1 | `RandomizedSearchCV` (20 settings, 5-fold CV) over `n_estimators`, `max_depth`, `min_samples_leaf`, `max_features` and `class_weight`, scored by macro-F1 |
| Evaluation | Accuracy, per-class precision, recall and F1, macro-F1, confusion matrix, ROC-AUC, precision-recall curves, cross-validation | Accuracy, per-class precision, recall and F1, macro-F1, confusion matrix, ROC-AUC, cross-validation, out-of-bag accuracy |
| Model interpretation | Coefficients and odds ratios (risk and protective factors) | Impurity-based and permutation feature importance |
| Improvement experiments | Class weights, L1, PCA, early prediction, approval-rate features (all by CV), learning curve, Enrolled decision-rule tuning | Class weights, default hyperparameters, raw codes vs one-hot, top-30 features, early prediction, 1st-semester only, number of trees, learning curve |
| Critical analysis, limitations, future work | Written for Logistic Regression | Written for Random Forest |
| Statistical comparison of the two models | McNemar test, paired bootstrap and repeated cross-validation (Section 7.4), using the Random Forest settings from the results file | Tuned Random Forest and its results file (`results/random_forest_results.json`), plus the comparison table in its own notebook (Section 6.2) |
| Results file for the comparison | `results/logistic_regression_results.json` | `results/random_forest_results.json` |

## Submission Links

- **Dataset:** [https://archive.ics.uci.edu/dataset/697](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)
- **Presentation video (YouTube):** `[<link>](https://youtu.be/X3Lj_QzbAp0?si=wFHo8UzK0HWaM499)`
- **Report:** `report/MS26923956_MS26930190.pdf`

## Limitations and Future Work

- The "Enrolled" class is the hardest to predict because it is the smallest. Resampling techniques such as SMOTE could be explored.
- Other classical models (SVM, Gradient Boosting) could be compared.
