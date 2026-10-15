# Report

This folder contains the final report for the Machine Learning Programming Assignment: **Predicting Student Dropout and Academic Success**.

| | |
|---|---|
| **File** | [`ML-Assignment-Report.pdf`](ML-Assignment-Report.pdf) |
| **Authors** | Thuiyadura L.R (MS26923956) and Nissanka H.M.D.P (MS26930190) |
| **Task** | Supervised multi-class classification: Dropout, Enrolled or Graduate |
| **Algorithms** | Logistic Regression (Member 1) and Random Forest (Member 2) |
| **Dataset** | [Predict Students' Dropout and Academic Success](https://archive.ics.uci.edu/dataset/697) (UCI Machine Learning Repository) |

> If the PDF has a different file name, update the link in the table above.

## Contents of the report

| Section | Topic |
|---|---|
| Abstract | Summary of the problem, methods and main findings |
| 1 | Introduction and problem statement |
| 2 | Dataset: source, suitability, attributes, class distribution |
| 3 | Data preprocessing: cleansing, outliers, exploratory analysis, encoding, train/test split, scaling, dimensionality reduction |
| 4 | Methodology: background and justification of Logistic Regression and Random Forest |
| 5 | Implementation: tools, tuning method and settings |
| 6 | Results of each algorithm, with interpretation |
| 7 | Comparison of the two algorithms, including a statistical check of the difference |
| 8 | Critical analysis: improvement experiments, learning curves, why accuracy is limited, how to improve it |
| 9 | Limitations and future work |
| 10 | Individual contributions |
| 11 | Conclusion |
| 12 | References |
| Appendix A | Source code of `logistic_regression.ipynb` (as text) |
| Appendix B | Source code of `random_forest.ipynb` (as text) |

## Main results

Both models were evaluated on the same held-out test set (885 students, stratified 80/20 split, `random_state=42`).

| Metric | Logistic Regression | Random Forest |
|---|---|---|
| Accuracy | 0.734 | 0.759 |
| Macro-F1 | 0.696 | 0.703 |
| Macro-AUC (one-vs-rest) | 0.884 | 0.887 |
| F1 for the "Enrolled" class | 0.504 | 0.491 |
| Recall for the "Enrolled" class | 0.635 | 0.509 |

- Random Forest is slightly more accurate, but the difference is borderline (McNemar test, p ≈ 0.055), and the two models are tied on macro-F1.
- "Enrolled" is the hardest class for both models.
- Almost all predictive power comes from academic results after enrolment: without semester data, accuracy drops sharply.
- Logistic Regression is easier to interpret, and Random Forest is slightly better on the Graduate and Dropout classes.

## Related files

| Item | Location |
|---|---|
| Logistic Regression notebook | [`../notebooks/logistic_regression.ipynb`](../notebooks/logistic_regression.ipynb) |
| Random Forest notebook | [`../notebooks/random_forest.ipynb`](../notebooks/random_forest.ipynb) |
| Dataset and its description | [`../data/`](../data/) |
| Saved test metrics (JSON) | [`../results/`](../results/) |

The source code in Appendices A and B is the same code as in the notebooks, included as text as required by the assignment.

## Citation of the dataset

Realinho, V., Vieira Martins, M., Machado, J., & Baptista, L. (2021). *Predict Students' Dropout and Academic Success* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5MC89

