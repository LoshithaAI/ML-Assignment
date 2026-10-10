# Dataset

## Name
Predict Students' Dropout and Academic Success

## Source
UCI Machine Learning Repository: https://archive.ics.uci.edu/dataset/697

## File
`data.csv` (semicolon-separated CSV)

## Description
The dataset contains demographic, socioeconomic, academic-path and academic-performance information about students at a Portuguese higher-education institution, plus macroeconomic indicators. It is used for a **supervised multi-class classification** task: predicting one of three outcomes at the end of the normal course duration.

| Class | Meaning | Students | Share |
|---|---|---|---|
| Graduate | The student graduated | 2,209 | 49.9% |
| Dropout | The student dropped out | 1,421 | 32.1% |
| Enrolled | The student is still enrolled | 794 | 17.9% |

## Key facts
- **Rows:** 4,424 students
- **Columns:** 36 input features + 1 target (`Target`)
- **Missing values:** none; **duplicate rows:** none
- **Feature types:** 9 integer-coded categorical columns (e.g. `Course`, `Application mode`), 8 binary flags, 18 continuous columns, and `Application order`
- **Class balance:** imbalanced ("Enrolled" is the smallest class)

## Purpose
Used for the Machine Learning Programming Assignment to develop and evaluate classification models: Logistic Regression and Random Forest.

## Licence
CC BY 4.0 (attribution required).

## Citation
Realinho, V., Vieira Martins, M., Machado, J., & Baptista, L. (2021). *Predict Students' Dropout and Academic Success* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5MC89
