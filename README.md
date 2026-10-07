# Diabetes Prediction: Numerical vs Categorical Data Representation with SHAP

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-F7931E?logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Classification-0064A5)
![SHAP](https://img.shields.io/badge/SHAP-Explainable%20AI-8A2BE2)
![Domain](https://img.shields.io/badge/Domain-Health%20Data%20Science-2E8B57)

An academic health data science project comparing **numerical** and **clinically categorized** representations of diabetes predictors using **Random Forest**, **XGBoost**, and **Multilayer Perceptron (MLP)** models. Model behavior is interpreted with **SHAP** at both global and individual levels.

**Academic group project:** Yuana Wira Dwi Satya Ilham Putra, Rafah Hassanah, and Mohammad Maliki Rafli  
**Program:** Master of Public Health - Biostatistics and Health Data Science, Universitas Airlangga  
**Portfolio maintenance:** Mohammad Maliki Rafli

> **Important validity note:** the Frankfurt diabetes file used in the coursework contains extensive duplicate observations. The original notebook identified **1,256 duplicated rows among 2,000 observations**. Consequently, the very high tree-model performance should be treated as potentially optimistic and not as evidence of external clinical performance.

## Project Overview

This project examines what changes when continuous health measurements are preserved as numerical values versus converted into clinically interpretable categories.

The comparison uses the same target and seven predictors after excluding `Glucose`:

- Pregnancies
- BloodPressure
- SkinThickness
- Insulin
- BMI
- DiabetesPedigreeFunction
- Age

The numerical workflow retains continuous measurements, while the categorical workflow applies clinical or data-derived cut points. SHAP is used to compare feature importance, direction of contribution, interaction patterns, and individual explanations.

## Repository Structure

```text
.
├── 01_Laporan/
│   └── Diabetes_Numerical_vs_Categorical_Model_Comparison_Report.pdf
├── 02_Script/
│   ├── Diabetes_Numerical_Modeling_SHAP.ipynb
│   └── Diabetes_Categorical_Modeling_SHAP.ipynb
├── 03_Data/
│   └── README.md
├── 04_Output/
│   └── README.md
├── 05_Presentation/
│   └── Diabetes_Numerical_vs_Categorical_Model_Comparison_Presentation.pdf
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

The public portfolio notebooks have their cell outputs cleared, and the row-level dataset is not included.

## Analytical Workflow

1. Load the Frankfurt diabetes dataset and inspect duplicate observations.
2. Exclude `Glucose` to align the two representation strategies used in the coursework.
3. Build numerical and categorical representations.
4. Split data into 70% training and 30% testing sets using `random_state=6`.
5. Fit Random Forest, XGBoost, and MLP classifiers.
6. Evaluate precision, recall, F1 score, and accuracy.
7. Interpret model behavior with SHAP.
8. Compare predictive performance and interpretability across representations.

## Primary Results Reported in the Coursework

| Model | Representation | Accuracy | Class 1 Recall | Macro F1 | Weighted F1 |
|---|---|---:|---:|---:|---:|
| Random Forest | Numerical | 0.97 | 0.95 | 0.97 | 0.97 |
| XGBoost | Numerical | 0.97 | 0.95 | 0.96 | 0.97 |
| MLP | Numerical, unstandardized | 0.75 | 0.58 | 0.72 | 0.75 |
| Random Forest | Categorical | 0.76 | 0.60 | 0.72 | 0.76 |
| XGBoost | Categorical | 0.76 | 0.58 | 0.72 | 0.75 |
| MLP | Categorical | 0.75 | 0.57 | 0.71 | 0.74 |

A later sensitivity analysis applies `StandardScaler` before numerical MLP training. In that run, accuracy increased to **0.81** and class-1 recall to **0.68**, illustrating the importance of scaling for neural networks.

## Methodological Review and Limitations

- The source file contains extensive duplicate observations, creating a risk of leakage across a random train-test split.
- In the original numerical workflow, median imputation is calculated before splitting; production-quality validation should fit data-dependent preprocessing on training data only.
- The original split does not specify `stratify=y`.
- Random Forest and MLP use integer category codes in the categorical workflow, which can impose an artificial ordered numeric structure.
- XGBoost uses native categorical features while the scikit-learn models receive encoded categories, so representation handling differs by model.
- The primary report compares an unstandardized numerical MLP; the standardized MLP result should be treated as a sensitivity analysis.
- Several early categorical definitions are later overwritten by the final definitions used for modeling.

These limitations are documented because leakage control, preprocessing design, encoding, and validation strategy are central to rigorous health machine learning.

## Reproducing the Analysis

```bash
git clone https://github.com/mohmalikirafli/diabetes-data-representation-ml-shap.git
cd diabetes-data-representation-ml-shap
pip install -r requirements.txt
```

Place the authorized dataset at:

```text
03_Data/frankfurt_diabetes.csv
```

Then run the notebooks in `02_Script/` from top to bottom.

## Academic and Clinical Use

This repository is intended for **education, methodological discussion, and portfolio demonstration**. The results are not externally validated and must not be used as a clinical diagnostic or treatment tool.

Source code is released under the MIT License. Academic report and presentation materials remain the intellectual work of the project authors and should be cited appropriately when reused.

## Contact

**Mohammad Maliki Rafli**  
Master of Public Health - Biostatistics and Health Data Science  
Universitas Airlangga
