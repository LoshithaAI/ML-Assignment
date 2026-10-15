# Notebooks

This folder contains the Jupyter notebooks for the Machine Learning Programming Assignment: **predicting student dropout and academic success** (3-class classification) with two distinct algorithms.

## Notebooks

| Notebook | Algorithm | Author | Status | Open in Colab |
|---|---|---|---|---|
| [`logistic_regression.ipynb`](logistic_regression.ipynb) | Logistic Regression (multinomial) | Member 1: Thuiyadura L.R (MS26923956) | Complete | [Open](https://colab.research.google.com/github/LoshithaAI/ML-Assignment/blob/main/notebooks/logistic_regression.ipynb) |
| [`random_forest.ipynb`](random_forest.ipynb) | Random Forest | Member 2: Nissanka H.M.D.P (MS26930190) | Complete | [Open](https://colab.research.google.com/github/LoshithaAI/ML-Assignment/blob/main/notebooks/random_forest.ipynb) |

The two notebooks are independent: each can be run on its own. Both use the same dataset, the same preprocessing and the same train/test split, so their results can be compared directly.

## Shared settings (both notebooks)

| Setting | Value |
|---|---|
| Dataset | `data/data.csv` (see [`../data/README.md`](../data/README.md)) |
| Split | 80% training / 20% test (3,539 / 885 students), stratified by class, `random_state=42` |
| Encoding | One-hot encoding of the 9 integer-coded categorical columns (36 features become 238 columns) |
| Model selection | 5-fold stratified cross-validation on the training set only, scored by macro-F1 |
| Final evaluation | The test set is used once, with the final tuned model |
| Metrics | Accuracy, per-class precision/recall/F1, macro-F1, confusion matrix, ROC-AUC |

## What each notebook contains

### `logistic_regression.ipynb`
1. Setup and data loading
2. Dataset selection and description
3. Data preprocessing: cleansing, outliers, exploratory analysis, encoding, split, scaling, PCA analysis
4. Algorithm background and justification
5. Model implementation: baseline and hyperparameter tuning (`GridSearchCV`, 12 combinations of `C` and `class_weight`)
6. Results on the held-out test set, with interpretation of the coefficients
7. Critical analysis: improvement experiments (class weights, L1, PCA, early prediction), learning curve, comparison with Random Forest (Tables A and B), statistical check (McNemar test and paired bootstrap), limitations and future work
8. Contribution, 9. Conclusion, 10. References

### `random_forest.ipynb`
1. Setup and data loading
2. Dataset selection and description
3. Data preprocessing (no scaling is needed for trees)
4. Algorithm background and justification
5. Model implementation: baseline and hyperparameter tuning (`RandomizedSearchCV`, 20 combinations of trees, depth, leaf size, features per split and class weights)
6. Results on the held-out test set, out-of-bag and cross-validation checks, feature importance (impurity-based and permutation), comparison with Logistic Regression
7. Critical analysis: improvement experiments, number of trees, learning curve, discussion, limitations and future work

## Key results (test set)

| Metric | Logistic Regression (tuned) | Random Forest (tuned) |
|---|---|---|
| Accuracy | 0.734 | 0.759 |
| Macro-F1 | 0.696 | 0.703 |
| Macro-AUC (one-vs-rest) | 0.884 | 0.887 |
| F1 / recall, class "Enrolled" | 0.504 / 0.635 | 0.491 / 0.509 |
| Best hyperparameters | `C = 0.1`, `class_weight = "balanced"` | 300 trees, `max_depth = 16`, `min_samples_leaf = 2`, `max_features = "sqrt"`, `class_weight = "balanced"` |

Random Forest is slightly more accurate, but the difference is borderline (McNemar p ≈ 0.055) and the two models are tied on macro-F1. "Enrolled" is the hardest class for both.

## How to run

**In Google Colab (recommended)**
1. Open the notebook from GitHub: *File → Open notebook → GitHub*, then choose this repository and the notebook.
2. Run all cells from the top (*Runtime → Run all*). The cells depend on each other, so a later cell run on its own fails with a `NameError`.
3. The first cell clones the repository to get `data/data.csv`; if that fails, the notebook falls back to downloading the file from GitHub.
4. Each notebook takes a few minutes, mostly the hyperparameter search.

**Locally**
```bash
pip install pandas numpy scipy scikit-learn matplotlib seaborn jupyter
jupyter notebook
```
Run the notebook from the repository root so that `data/data.csv` is found. The `!git clone` cell at the top is only needed in Colab and can be skipped.

## Results files

Each notebook saves its test metrics to a JSON file (`logistic_regression_results.json` and `random_forest_results.json`). Commit both files to the [`../results/`](../results/) folder. The comparison cells (Table B and the statistical check in the Logistic Regression notebook, and Section 6.2 in the Random Forest notebook) read these files, so both must be present in the folder the cell expects. In Colab, files are lost when the session ends, so download them and commit them.

## Environment

Python 3, pandas 2.2.3, numpy 2.1.3, scikit-learn 1.6.1, scipy, matplotlib, seaborn. A fixed random seed (`RANDOM_STATE = 42`) makes the results reproducible.
