
# Random Forest Notebook

**Notebook:** `random_forest.ipynb`
**Author:** Nissanka H.M.D.P (MS26930190)
**Branch:** `nissanka-hmdp-ms26930190`

## Overview
This notebook predicts whether a student will **Dropout**, remain **Enrolled** or **Graduate**, using a **Random Forest** classifier. It is part of the Machine Learning Programming Assignment, where the same dataset is also modelled with Logistic Regression (`logistic_regression.ipynb`) so the two algorithms can be compared.

## Dataset
*Predict Students' Dropout and Academic Success* (UCI Machine Learning Repository), 4,424 students, 36 features and 3 classes. See `data/README.md` for details.

## Notebook structure
| Section | Content |
|---|---|
| 1. Setup | Clone the repository and import libraries |
| 2. Dataset | Loading, class distribution and feature types |
| 3. Data preprocessing | Cleansing, outlier analysis, exploratory analysis, one-hot encoding, stratified train/test split, scaling and feature selection |
| 4. Algorithm background | How Random Forest works and why it suits this dataset |
| 5. Model implementation | Baseline model and hyperparameter tuning (`RandomizedSearchCV`, 5-fold CV) |
| 6. Results | Test-set metrics, confusion matrix, ROC curves, feature importance, and comparison with Logistic Regression |
| 7. Critical analysis | Improvement experiments, discussion, limitations and future work |
| 8. Contribution | Work done by each member |
| 9. Conclusion | Summary of the findings |
| 10. References | Dataset and sources |

## How to run
**Google Colab (recommended)**
1. Open `random_forest.ipynb` in Colab.
2. Choose **Runtime → Run all**. The first cell clones the repository, and the dataset is loaded from `data/data.csv`.

**Locally**
1. Clone the repository and open the notebook.
2. Install the requirements: `pip install pandas numpy matplotlib seaborn scikit-learn jupyter`
3. Run all cells. If `data.csv` is not found locally, the notebook reads it from the GitHub repository.

Hyperparameter tuning, the tree-count experiment and the learning curve take a few minutes in total.

## Requirements
Python 3, `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`.

## Settings used
- Stratified 80/20 train/test split, `random_state=42` (3,539 training rows, 885 test rows)
- One-hot encoding of the 9 categorical code columns (238 input columns)
- Tuning scored by **macro-F1**, because the "Enrolled" class is small
- The test set is not used for any tuning decision

## Key results (test set, 885 students)
| Model | Accuracy | Macro-F1 | Macro-AUC |
|---|---|---|---|
| Random Forest (baseline) | 0.766 | 0.668 | - |
| Random Forest (tuned) | 0.759 | 0.703 | 0.887 |

Best parameters: 300 trees, `max_depth=16`, `min_samples_leaf=2`, `max_features="sqrt"`, `class_weight="balanced"`.

## Output
The notebook saves its results to `results/random_forest_results.json`. Section 6.2 reads this file together with `results/logistic_regression_results.json` to compare the two models, so both files must be in the `results/` folder.

## Related files
- `logistic_regression.ipynb`: the teammate's Logistic Regression notebook
- `data/data.csv`: the dataset
- `results/`: saved results of both models
