# Student Dropout and Academic Success Prediction

Fundamentals of Machine Learning – Programming Assignment

Predicts whether a student will **Dropout**, stay **Enrolled** or **Graduate** using supervised learning on the
[UCI dataset](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)
(4,424 students, 36 features, [DOI](https://doi.org/10.24432/C5MC89)).

| Member | Algorithm | Notebook |
|---|---|---|
| Thuiyadura L.R (MS26923956) | Logistic Regression | `notebooks/logistic_regression.ipynb` |
| Nissanka H.M.D.P (MS26930190) | Random Forest | `notebooks/random_forest.ipynb` |

Both use the same stratified 80/20 split (`random_state=42`), 5-fold CV tuning and macro-F1 as the tuning metric.

## Results (test set)

| Metric | Logistic Regression | Random Forest |
|---|---:|---:|
| Accuracy | 73.45% | **75.93%** |
| Macro F1 | 0.6961 | **0.7026** |
| Macro ROC-AUC (OvR) | 0.8844 | **0.8866** |
| CV Macro F1 | 0.7147 | **0.7166** |

**Best hyperparameters:** LR `C=0.1`, `class_weight=balanced` · RF `n_estimators=300`, `max_depth=16`, `max_features=sqrt`, `min_samples_leaf=2`, `class_weight=balanced`

## Key findings
- Random Forest scores slightly higher on all four metrics, but only the accuracy gap is near significance (McNemar p ≈ 0.055); macro-F1 and AUC are effectively tied.
- Logistic Regression finds more Enrolled students (recall 63.5% vs 50.9%) and is easier to interpret.
- Both models struggle most with the Enrolled class.

## How to run
Designed for Google Colab (each notebook clones this repo). To run locally:

```bash
git clone https://github.com/LoshithaAI/ML-Assignment.git
cd ML-Assignment
pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter
jupyter notebook   # open the notebooks in notebooks/
```

The final report (PDF) is in `report/`.

