# Student Academic Success & Dropout Prediction

[![Python 3.11](https://img.shields.io/badge/python-3.11-blue.svg)](https://www.python.org/downloads/release/python-3110/)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![DOI: 10.24432/C5MC89](https://img.shields.io/badge/DOI-10.24432%2FC5MC89-orange.svg)](https://doi.org/10.24432/C5MC89)
[![Code Style: Black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Reproducibility: Verified](https://img.shields.io/badge/Reproducibility-Verified-success.svg)](#)

> **Lead Data Scientist & Project Engineer:** Aryan  
> **Project Type:** AI / Data Analytics / Machine Learning Academic Internship Project  
> **Repository ID:** UCI Machine Learning Repository #697  
> **GitHub repository:** [Student-Academic-Success-Dropout-Prediction.](https://github.com/r3ban-hub/Student-Academic-Success-Dropout-Prediction.)

---

## 1. Project Overview
Student dropout in higher education is a complex challenge with severe personal, institutional, and societal implications. This repository houses an end-to-end, reproducible machine learning project that predicts one of three student outcomes:
1. **Dropout:** Student left the institution without finishing degree requirements.
2. **Enrolled:** Student remains actively enrolled beyond standard course duration.
3. **Graduate:** Student successfully completed their degree program.

To eliminate **temporal data leakage**, this project formulates two operational perspectives:
- **Perspective A (Pre-Enrollment Screening):** 24 audited features known strictly at or before matriculation. Tests whether incoming at-risk students can be identified before classes commence.
- **Perspective B (Academic-Progress Modeling):** Full 36 features including 1st and 2nd semester curricular outcomes (enrolled credits, evaluations, approved units, and GPAs). Quantifies how first-year milestones enhance prediction.

Our empirical benchmark shows that while intake screening (Perspective A) achieves **59.10% accuracy** (Macro-F1: 0.5506), observing first-year academic traction (Perspective B) elevates accuracy to **74.92%** and Macro-F1 to **0.7069** (Random Forest Classifier).

---

## 2. Problem Statement
Universities predominantly intervene *reactively*—after an academic suspension or formal withdrawal occurs. Higher education leadership requires early diagnostic signals to deploy targeted academic counseling, financial aid assistance, and tutoring.

Key technical and operational challenges addressed:
1. **Multiclass Class Imbalance:** The distribution is uneven across classes (`Graduate`: 49.93%, `Dropout`: 32.12%, `Enrolled`: 17.95%). Accuracy alone is misleading; Macro-F1 and per-class recall must guide model selection.
2. **Temporal Data Leakage Safeguards:** Curricular units approved in the second semester cannot be used to evaluate an applicant during admission. Pre-enrollment and longitudinal predictors must be methodologically isolated.
3. **Model Interpretability:** Black-box predictions are insufficient for academic advisors. Feature importance rankings must provide clear diagnostic explanations.

---

## 3. Project Objectives
- [x] Ingest and audit the official UCI 697 dataset (4,424 records, 36 predictors, 0 missing values, 0 duplicates).
- [x] Perform exhaustive Exploratory Data Analysis (EDA) uncovering academic, financial, and demographic attrition drivers.
- [x] Build isolated scikit-learn preprocessing pipelines (`StandardScaler`, `OneHotEncoder`).
- [x] Train and validate five supervised learning model families alongside a stratified DummyClassifier baseline using 5-Fold Stratified Cross-Validation.
- [x] Compare Perspective A (Pre-Enrollment) vs. Perspective B (Academic-Progress).
- [x] Extract global explainability metrics via tree-based Gini importance and permutation analysis.
- [x] Generate a 20-section professional Microsoft Word report (`Aryan_StudentAcademicSuccessReport.docx`).

---

## 4. Dataset Description & Official Citation
- **Source:** [UCI Machine Learning Repository: Predict Students' Dropout and Academic Success](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)
- **Dataset ID:** 697
- **DOI:** [10.24432/C5MC89](https://doi.org/10.24432/C5MC89)
- **License:** Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Creators:** Valentim Realinho, Jorge Machado, Luís Baptista, Mónica V. Martins (Instituto Politécnico de Portalegre)
- **Official Citation:**
  ```bibtex
  @article{realinho2021predict,
    title={Predict Students' Dropout and Academic Success},
    author={Realinho, Valentim and Machado, Jorge and Baptista, Lu{\'\i}s and Martins, M{\'o}nica V},
    journal={Data},
    volume={6},
    number={11},
    pages={124},
    year={2021},
    publisher={MDPI},
    doi={10.3390/data6110124}
  }
  ```

---

## 5. Technologies Used
- **Language:** Python 3.11
- **Data Manipulation:** `pandas`, `numpy`, `scipy`
- **Machine Learning:** `scikit-learn`
- **Visualization:** `matplotlib`, `seaborn`
- **Documentation & Reporting:** `python-docx`, `nbformat`, `nbclient`
- **Official UCI Ingestion:** `ucimlrepo`

---

## 6. Project Directory Structure
```
project-root/
│
├── Aryan_StudentAcademicSuccessPrediction.ipynb  # Master Jupyter Notebook (34 sections, fully executed)
├── Aryan_StudentAcademicSuccessReport.docx       # Professional 20-section Word report with embedded figures
├── DATASET_AUDIT.md                              # Complete data audit & official feature verification table
├── FINAL_PROJECT_AUDIT.md                        # Verification checklist & empirical sign-off audit
├── README.md                                     # Main project documentation & user guide
├── requirements.txt                              # Pinned Python package dependencies
├── .gitignore                                    # Git configuration file
│
├── data/
│   └── data.csv                                  # Official UCI 697 dataset (4,424 rows x 37 columns)
│
└── outputs/
    ├── figures/
    │   ├── class_distribution.png                # Target class counts & pie breakdown
    │   ├── eda_bivariate_academic.png            # 2nd sem approved units & grades by outcome
    │   ├── eda_financial_risk.png                # Tuition fee & debtor status outcome analysis
    │   ├── eda_demographics_admission.png        # Admission grade & age density curves
    │   ├── correlation_matrix.png                # Multi-feature correlation heatmap
    │   ├── perspective_comparison.png            # Perspective A vs. Perspective B benchmark
    │   ├── confusion_matrices.png                # Normalized & count confusion matrices
    │   ├── feature_importance.png                # Top 15 Random Forest Gini feature importances
    │   └── model_metrics_comparison.png          # Comprehensive multi-metric benchmark
    │
    └── model_results/
        ├── model_comparison_metrics.csv          # Complete CV & Test metrics for all 12 pipelines
        └── model_comparison_metrics.json         # Structured JSON export of evaluation results
```

---

## 7. Installation & Reproducibility
### Step 1: Clone Repository
```bash
git clone https://github.com/r3ban-hub/Student-Academic-Success-Dropout-Prediction..git
cd Student-Academic-Success-Dropout-Prediction.
```

### Step 2: Create and Activate Virtual Environment
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate
```

### Step 3: Install Required Dependencies
```bash
pip install -r requirements.txt
```

---

## 8. How to Run the Project
### Option A: Run the Jupyter Notebook
Launch Jupyter Lab or Notebook:
```bash
jupyter notebook Aryan_StudentAcademicSuccessPrediction.ipynb
```
Select **Kernel -> Restart & Run All** to reproduce all visualizations and model benchmarks.

### Option B: Execute Programmatically via Terminal
To execute the notebook end-to-end from the command line:
```bash
python -m nbconvert --execute --inplace Aryan_StudentAcademicSuccessPrediction.ipynb
```

---

## 9. Modeling Methodology
### Preprocessing & Pipeline Isolation
- **Categoricals (Nominal):** `OneHotEncoder(handle_unknown='ignore', sparse_output=False)` applied to `Course`, `Application mode`, `Marital status`, `Nacionality`, and parental background codes.
- **Continuous / Counts:** `StandardScaler()` applied to admission grades, qualification scores, age, macroeconomic rates, and curricular metrics.
- **Data Partitions:** Stratified 80/20 train-test split (`random_state=42`). Preprocessors are fit strictly on the training partition.
- **Cross-Validation:** 5-Fold Stratified Cross-Validation on the training partition.

---

## 10. Model Evaluation & Benchmark Results

### Benchmark Summary (Test Set Performance)

| Perspective | Model | CV Macro-F1 (Mean +/- Std) | Test Accuracy | Test Macro-F1 | Test Weighted-F1 | Dropout Recall | Graduate Recall |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Perspective A** | Baseline (Stratified) | 0.3383 +/- 0.009 | 41.02% | 0.3567 | 0.4097 | 38.38% | 51.13% |
| *(Pre-Enrollment)* | Logistic Regression | 0.5675 +/- 0.017 | 57.40% | 0.5506 | 0.5906 | 57.75% | 59.05% |
| *(24 Features)* | Decision Tree | 0.4988 +/- 0.022 | 49.49% | 0.4989 | 0.5249 | 45.07% | 42.76% |
| | Random Forest | 0.5817 +/- 0.013 | 59.10% | 0.5464 | 0.5986 | 62.32% | 64.48% |
| | HistGradientBoosting | 0.5548 +/- 0.015 | 58.98% | 0.5356 | 0.5919 | 59.51% | 67.87% |
| | Support Vector Machine | 0.5761 +/- 0.024 | 56.72% | 0.5395 | 0.5822 | 56.69% | 59.28% |
| **Perspective B** | Baseline (Stratified) | 0.3383 +/- 0.009 | 41.02% | 0.3567 | 0.4097 | 38.38% | 51.13% |
| *(Longitudinal)* | Logistic Regression | 0.7093 +/- 0.016 | 72.43% | 0.6876 | 0.7372 | 67.96% | 78.51% |
| *(36 Features)* | Decision Tree | 0.6698 +/- 0.016 | 64.86% | 0.6314 | 0.6741 | 61.62% | 64.71% |
| | **Random Forest (Champion)** | **0.7131 +/- 0.025** | **74.92%** | **0.7069** | **0.7577** | **70.42%** | **82.81%** |
| | HistGradientBoosting | 0.7092 +/- 0.014 | 74.46% | 0.6926 | 0.7470 | 70.42% | 84.84% |
| | Support Vector Machine | 0.7124 +/- 0.016 | 72.99% | 0.6904 | 0.7404 | 68.31% | 80.32% |

### Champion Model: Random Forest (Perspective B)
- **Test Accuracy:** 74.92%
- **Test Macro-F1:** 0.7069
- **Dropout Recall:** 70.42% (Achieves 70.42% recall for the Dropout class on the held-out test set.)
- **Graduate Recall:** 82.81% (Achieves 82.81% recall for the Graduate class on the held-out test set.)
- **Enrolled Recall:** 61.01% (Achieves 61.01% recall for the minority Enrolled class on the held-out test set.)

---

## 11. Key Findings & Diagnostic Insights
1. **Academic Checkpoints Outweigh Pre-Entry Factors:** Incorporating first-year academic milestones raises predictive accuracy by **+15.8 percentage points** (from 59.10% to 74.92%) and Macro-F1 from 0.5506 to 0.7069.
2. **Tuition Fee Status Shows a Strong Association with Dropout:** Students who fall behind on tuition fees (`Tuition fees up to date = 0`) exhibit an observed **86.55% dropout rate**. This association could be explored as a potential signal for targeted financial-support interventions.
3. **Second-Semester Course Approvals are Strong Predictive Features:** The number of approved units in semester 2 is the single most predictive feature. Over 75% of dropouts fail to pass more than 2 courses in their second semester.
4. **Higher Observed Dropout Rates Among Older Students:** Enrollees over age 25 experience a 52.8% observed dropout rate (vs. 25.4% among 18-21 year olds), highlighting the value of tailored academic advising and support.

---

## 12. Limitations & Ethical Considerations
- **Single Institutional Context:** Data reflects a single Portuguese polytechnic institution (Instituto Politécnico de Portalegre). External validation on other university types is recommended.
- **Observational Correlation:** Feature importance signifies predictive correlation, not causal mechanisms.
- **Fairness & Non-Punitive Deployment:** Risk predictions must **never** be used punitively (e.g., rescinding financial aid or restricting registration). They must solely guide supportive institutional interventions.

---

## 13. Future Scope
1. **LMS Telemetry Integration:** Incorporate weekly Canvas/Moodle LMS engagement data (login counts, assignment submission lag) for intra-semester early warnings.
2. **Specialized Multi-Stage Modeling:** Develop dedicated sub-classifiers for the ambiguous `Enrolled` cohort.
3. **Advisor Decision Support System:** Deploy real-time risk predictions with SHAP explainability into university advising portals.

---

## 14. Author
**Aryan**  
Lead Data Scientist & Project Engineer  
*Student Academic Success & Retention Analytics Project*  
Dataset: UCI Machine Learning Repository ID #697 | DOI: 10.24432/C5MC89
