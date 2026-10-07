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

> Citation: `<copy the official citation from the UCI dataset page>`

## Repository Structure

```
.
├── data/
│   └── data.csv                     # dataset (also linked in submission.txt)
├── notebooks/
│   ├── 01_eda_preprocessing.ipynb   # shared: EDA, cleaning, encoding, split
│   ├── 02_logistic_regression.ipynb # Member 1
│   ├── 03_random_forest.ipynb       # Member 2
│   └── 04_comparison.ipynb          # side-by-side evaluation
├── report/
│   └── report.pdf
├── requirements.txt
└── README.md
```

> Update the file names above to match your actual notebooks.

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

| Model | Accuracy | Macro-F1 |
|---|---|---|
| Logistic Regression | `TBD` | `TBD` |
| Random Forest | `TBD` | `TBD` |

> Fill in from your own notebook runs.

## How to Run

```bash
git clone <repo-url>
cd <repo-name>
pip install -r requirements.txt
jupyter notebook
```

Run the notebooks in numeric order. Python 3.9+ is recommended.

**Main libraries:** `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`

## Individual Contributions

- **`<Name 1>`:** `<e.g. preprocessing, Logistic Regression implementation and tuning, relevant report sections>`
- **`<Name 2>`:** `<e.g. EDA, Random Forest implementation and tuning, relevant report sections>`

## Submission Links

- **Dataset:** https://archive.ics.uci.edu/dataset/697
- **Presentation video (YouTube):** `<link>`
- **Report:** `report/report.pdf`

## Limitations and Future Work

- The 2nd-semester features strongly predict the outcome, so an early-prediction version using only enrollment and 1st-semester data would be more useful in practice.
- The "Enrolled" class is the hardest to predict because it is the smallest. Resampling techniques such as SMOTE could be explored.
- Other classical models (SVM, Gradient Boosting) could be compared.
