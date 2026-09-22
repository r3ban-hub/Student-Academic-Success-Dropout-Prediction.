# FINAL PROJECT AUDIT: Student Academic Success & Dropout Prediction

**Project Owner:** Aryan  
**Role:** Lead Data Scientist & Project Engineer  
**Audit Timestamp:** September 2026  
**Auditor Engine:** AntiGravity Automated Verification & Quality Assurance Suite  

---

## 1. Summary of Project Files Created

| File / Folder Path | Type | Size | Status | Verification Detail |
| :--- | :--- | :--- | :--- | :--- |
| `Aryan_StudentAcademicSuccessPrediction.ipynb` | Jupyter Notebook | ~1.10 MB | **Verified & Executed** | 56 cells (34 required sections, 22 executed code cells with outputs and inline figures). |
| `Aryan_StudentAcademicSuccessReport.docx` | Word Report | ~1.44 MB | **Verified** | Complete 20-section report formatted with executive styling, embedded figures, and data tables. |
| `DATASET_AUDIT.md` | Markdown Report | ~15.7 KB | **Verified** | Exhaustive data audit with complete 36-feature verification table vs. official definitions. |
| `README.md` | Documentation | ~12.8 KB | **Verified** | GitHub-ready documentation with badges, installation guide, benchmark tables, and architecture. |
| `requirements.txt` | Package Specs | 166 B | **Verified** | Pinned minimal dependencies (`pandas`, `numpy`, `scipy`, `scikit-learn`, `matplotlib`, `seaborn`, `python-docx`, `ucimlrepo`, `nbformat`, `ipykernel`). |
| `.gitignore` | Git Config | 356 B | **Verified** | Excludes virtualenvs, cache files, temporary logs, and OS artifacts. |
| `data/data.csv` | Raw Dataset | 533.2 KB | **Verified** | Official UCI 697 dataset (4,424 rows x 37 columns, semicolon-delimited). |
| `outputs/figures/` | Visual Assets | 9 PNG files | **Verified** | High-resolution 300 DPI visualizations for all key analytical aspects. |
| `outputs/model_results/` | Metrics Exports | CSV & JSON | **Verified** | Programmatic dumps of CV and test set evaluation metrics across all 12 pipelines. |
| `FINAL_PROJECT_AUDIT.md` | Verification Audit | This file | **Verified** | Final quality assurance and empirical verification sign-off. |

---

## 2. Dataset Verification
- **Official Source:** UCI Machine Learning Repository (ID: 697)
- **Official Title:** *Predict Students' Dropout and Academic Success*
- **DOI:** [10.24432/C5MC89](https://doi.org/10.24432/C5MC89)
- **License:** Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Primary Authors:** Valentim Realinho, Jorge Machado, Luís Baptista, Mónica V. Martins (Instituto Politécnico de Portalegre)
- **Dimensions:** Exactly 4,424 observations and 37 columns (36 feature predictors + 1 multiclass target).
- **Missing Values:** Exactly **0** null/missing cells across all 163,688 data cells.
- **Duplicate Records:** Exactly **0** duplicate rows found.
- **Data Quality Remediation:** Trailing tab character in column name `'Daytime/evening attendance\t'` was sanitized with `.str.strip()`.

---

## 3. Target Class Distribution
- **Target Column:** `Target` (Nominal Multiclass)
- **Classes:**
  1. `Graduate`: 2,209 students (**49.93%**)
  2. `Dropout`: 1,421 students (**32.12%**)
  3. `Enrolled`: 794 students (**17.95%**)
- **Total:** 4,424 students (**100.00%**)
- **Class Balance Strategy:** Stratified splitting (80/20 train/test partition) and cost-sensitive class balancing (`class_weight='balanced'`) inside all classification models.

---

## 4. Modeling Architecture & Temporal Leakage Mitigation
Two distinct operational perspectives were audited, isolated, and evaluated:
- **Perspective A (Pre-Enrollment Screening):** Evaluates early intervention feasibility using 24 features available at the admission threshold (demographics, parental occupation/qualification, admission examination grades, application mode, intake fee status, and cohort macroeconomic indicators).
- **Perspective B (Academic-Progress Longitudinal Modeling):** Evaluates predictive trajectory using all 36 features, incorporating first- and second-semester curricular credit completions, evaluations, and GPA marks.

---

## 5. Machine Learning Models Trained
Five algorithm families were trained under 5-Fold Stratified Cross-Validation on the training partition (3,539 instances) and evaluated on the independent test partition (885 instances):
1. **Baseline Model:** Stratified `DummyClassifier`
2. **Logistic Regression:** Multinomial with L2 regularization
3. **Decision Tree:** Constrained depth (`max_depth=6`)
4. **Random Forest:** Ensemble bagging of 150 estimators (`max_depth=12`, balanced subsampling)
5. **HistGradientBoosting:** Dense one-hot compatible gradient boosting (`max_iter=120`, balanced class weights)
6. **Support Vector Machine (RBF):** Radial basis function kernel with cost-sensitive weighting

---

## 6. Actual Empirical Evaluation Metrics (Zero Fabrication)

### Perspective A: Pre-Enrollment / Early-Stage Screening (24 Features)
| Model | CV Macro-F1 (Mean +/- Std) | Test Accuracy | Test Macro-F1 | Test Weighted-F1 | Dropout Recall | Enrolled Recall | Graduate Recall |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Baseline (Stratified) | 0.3383 +/- 0.009 | 41.02% | 0.3567 | 0.4097 | 38.38% | 17.61% | 51.13% |
| **Logistic Regression** | **0.5675 +/- 0.017** | **57.40%** | **0.5506** | **0.5906** | **57.75%** | **52.20%** | **59.05%** |
| Decision Tree | 0.4988 +/- 0.022 | 49.49% | 0.4989 | 0.5249 | 45.07% | 76.10% | 42.76% |
| Random Forest | 0.5817 +/- 0.013 | 59.10% | 0.5464 | 0.5986 | 62.32% | 38.36% | 64.48% |
| HistGradientBoosting | 0.5548 +/- 0.015 | 58.98% | 0.5356 | 0.5919 | 59.51% | 33.33% | 67.87% |
| Support Vector Machine (RBF) | 0.5761 +/- 0.024 | 56.72% | 0.5395 | 0.5822 | 56.69% | 49.69% | 59.28% |

### Perspective B: Longitudinal Academic-Progress Modeling (36 Features)
| Model | CV Macro-F1 (Mean +/- Std) | Test Accuracy | Test Macro-F1 | Test Weighted-F1 | Dropout Recall | Enrolled Recall | Graduate Recall |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Baseline (Stratified) | 0.3383 +/- 0.009 | 41.02% | 0.3567 | 0.4097 | 38.38% | 17.61% | 51.13% |
| Logistic Regression | 0.7093 +/- 0.016 | 72.43% | 0.6876 | 0.7372 | 67.96% | 63.52% | 78.51% |
| Decision Tree | 0.6698 +/- 0.016 | 64.86% | 0.6314 | 0.6741 | 61.62% | 71.07% | 64.71% |
| **Random Forest (Champion)** | **0.7131 +/- 0.025** | **74.92%** | **0.7069** | **0.7577** | **70.42%** | **61.01%** | **82.81%** |
| HistGradientBoosting | 0.7092 +/- 0.014 | 74.46% | 0.6926 | 0.7470 | 70.42% | 52.83% | 84.84% |
| Support Vector Machine (RBF) | 0.7124 +/- 0.016 | 72.99% | 0.6904 | 0.7404 | 68.31% | 61.01% | 80.32% |

---

## 7. Final Model Selection & Justification
- **Champion Model:** `Random Forest Classifier` under **Perspective B (Academic-Progress)**
- **Test Set Performance:**
  - **Accuracy:** **74.92%**
  - **Macro-F1:** **0.7069**
  - **Weighted-F1:** **0.7577**
  - **Dropout Class Performance:** Precision = **0.830**, Recall = **0.704**, F1 = **0.762**
  - **Graduate Class Performance:** Precision = **0.855**, Recall = **0.828**, F1 = **0.841**
  - **Enrolled Class Performance:** Precision = **0.449**, Recall = **0.610**, F1 = **0.517**
- **Justification:** Random Forest achieved the highest Macro-F1 (0.7069) and test accuracy (74.92%), while successfully capturing over 70% of actual dropouts and 61% of delayed-progress enrolled students. It demonstrated strong cross-validation stability (CV Macro-F1: 0.7131 +/- 0.025).

---

## 8. Quality Assurance & Verification Checklist

| QA Item | Requirement | Verification Result | Status |
| :--- | :--- | :--- | :---: |
| **Notebook Execution** | Full execution from top to bottom with no unhandled errors | Executed cleanly via `nbclient`; all 56 cells and 22 code outputs populated. | **PASSED** |
| **Zero Fabrication** | All numbers derived from actual calculations | Every metric in Markdown, Notebook, Report, and CSV traces to executed models. | **PASSED** |
| **Data Leakage Safeguard** | Isolated train/test preprocessing and temporal perspectives | `ColumnTransformer` fitted strictly on train set; Perspectives A and B isolated. | **PASSED** |
| **HistGradientBoosting** | Compatible with preprocessing pipeline | Dense one-hot encoding array verified; executed without runtime error. | **PASSED** |
| **Early Feature Audit** | Verified against official UCI definitions | Complete 36-feature table documented with citation evidence. | **PASSED** |
| **Report Generation** | Complete 20-section DOCX report with tables & figures | `Aryan_StudentAcademicSuccessReport.docx` generated (1.44 MB). | **PASSED** |
| **README Accuracy** | Exactly matches executed codebase | Complete with badges, benchmark tables, and reproduction commands. | **PASSED** |
| **Requirements Specs** | Minimal pinned dependencies | Clean `requirements.txt` containing only necessary libraries. | **PASSED** |
| **GitHub Readiness** | Clean directory, standard `.gitignore`, no secrets | No cache, no checkpoints, no credentials in repository. | **PASSED** |

---

## 9. Remaining Issues or Technical Debt
- **None.** The project is 100% complete, reproducible, and ready for production submission or GitHub repository publishing.
