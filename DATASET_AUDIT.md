# DATASET AUDIT: Predict Students' Dropout and Academic Success

**Project Owner:** Aryan  
**Project Title:** Student Academic Success & Dropout Prediction  
**Dataset Reference:** UCI Machine Learning Repository ID 697  
**DOI:** [10.24432/C5MC89](https://doi.org/10.24432/C5MC89)  
**License:** Creative Commons Attribution 4.0 International (CC BY 4.0)  
**Audit Date:** September 2026 (AntiGravity Data Science Engine)

---

## 1. Dataset Source & Provenance
- **Repository:** UCI Machine Learning Repository
- **URL:** [https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)
- **Creators:** Valentim Realinho, Jorge Machado, Luís Baptista, Mónica V. Martins (Instituto Politécnico de Portalegre)
- **Primary Citation:** Realinho, V., Machado, J., Baptista, L., & Martins, M. V. (2021). *Predict Students' Dropout and Academic Success*. Data, 6(11), 124. DOI: 10.3390/data6110124.

---

## 2. Dataset Size & Dimensions
- **Total Records (Instances):** 4,424
- **Total Columns:** 37 (36 feature predictors + 1 multiclass target)
- **Total Cells:** 163,688
- **File Format:** Semicolon-delimited CSV (`data.csv` inside official zip distribution)
- **Character Encoding:** UTF-8 / UTF-8 with BOM

---

## 3. Target Variable
- **Variable Name:** `Target`
- **Type:** Nominal / Multiclass Categorical (3 classes)
- **Class Distribution:**
  - **Graduate:** 2,209 instances (49.93%)
  - **Dropout:** 1,421 instances (32.12%)
  - **Enrolled:** 794 instances (17.95%)
- **Imbalance Assessment:** Moderate class imbalance. The minority class (`Enrolled`) represents ~18% of observations, while `Graduate` comprises ~50%. Stratified train-test splitting and reporting of both Macro-F1 and Weighted-F1 are mandatory.

---

## 4. Feature Groups & Taxonomic Breakdown
The 36 predictor features span 7 distinct operational and contextual categories:

1. **Demographic Factors (6 features):**
   - `Marital status` (categorical/integer codes 1–6)
   - `Nacionality` (categorical/integer codes 1–109)
   - `Displaced` (binary: 0 = No, 1 = Yes)
   - `Gender` (binary: 1 = Male, 0 = Female)
   - `Age at enrollment` (discrete integer, range: 17–70 years)
   - `International` (binary: 0 = No, 1 = Yes)

2. **Socioeconomic & Parental Background (4 features):**
   - `Mother's qualification` (categorical/integer codes 1–44)
   - `Father's qualification` (categorical/integer codes 1–44)
   - `Mother's occupation` (categorical/integer codes 0–194)
   - `Father's occupation` (categorical/integer codes 0–195)

3. **Academic Admission & Prior Education (7 features):**
   - `Application mode` (categorical/integer codes 1–57)
   - `Application order` (ordinal integer 0–9; preference order)
   - `Course` (categorical degree program codes 33–9991; 17 distinct programs)
   - `Daytime/evening attendance` (binary: 1 = Daytime, 0 = Evening)
   - `Previous qualification` (categorical/integer codes 1–43)
   - `Previous qualification (grade)` (continuous scale 95.0–190.0)
   - `Admission grade` (continuous scale 95.0–190.0)
   - `Educational special needs` (binary: 0 = No, 1 = Yes)

4. **Financial & Institutional Standing (3 features):**
   - `Debtor` (binary: 0 = No, 1 = Yes; student has overdue debts)
   - `Tuition fees up to date` (binary: 1 = Yes, 0 = No)
   - `Scholarship holder` (binary: 0 = No, 1 = Yes)

5. **1st Semester Academic Progress (6 features):**
   - `Curricular units 1st sem (credited)` (integer 0–20)
   - `Curricular units 1st sem (enrolled)` (integer 0–26)
   - `Curricular units 1st sem (evaluations)` (integer 0–45)
   - `Curricular units 1st sem (approved)` (integer 0–26)
   - `Curricular units 1st sem (grade)` (continuous 0.0–18.875; Portuguese 0–20 grading scale)
   - `Curricular units 1st sem (without evaluations)` (integer 0–12)

6. **2nd Semester Academic Progress (6 features):**
   - `Curricular units 2nd sem (credited)` (integer 0–19)
   - `Curricular units 2nd sem (enrolled)` (integer 0–23)
   - `Curricular units 2nd sem (evaluations)` (integer 0–33)
   - `Curricular units 2nd sem (approved)` (integer 0–20)
   - `Curricular units 2nd sem (grade)` (continuous 0.0–18.571; Portuguese 0–20 grading scale)
   - `Curricular units 2nd sem (without evaluations)` (integer 0–12)

7. **Macroeconomic Indicators (3 features):**
   - `Unemployment rate` (continuous percentage: 7.6%–16.2%)
   - `Inflation rate` (continuous percentage: -0.8%–3.7%)
   - `GDP` (continuous economic growth rate: -4.06%–3.51%)

---

## 5. Missing-Value & Duplicate Analysis
- **Missing Values:** Exactly **0** missing values across all 4,424 rows and 37 columns.
- **Null / NaN Checks:** No null strings (`"NA"`, `"null"`, `"?"`, `""`).
- **Duplicate Records:** Exactly **0** duplicate rows found across the 4,424 observations.
- **Consistency:** All numerical codes map strictly within their expected domain ranges according to the official UCI documentation.

---

## 6. Data-Type & Encoding Audit
- **Categorical Columns Encoded as Integers:** Variables such as `Course`, `Application mode`, `Marital status`, `Nacionality`, `Mother's qualification`, and `Father's occupation` are stored numerically as integer codes. Treating them as raw continuous variables would create arbitrary ordinal bias.
- **Binary Indicator Columns:** Coded as `0` and `1` (`Displaced`, `Educational special needs`, `Debtor`, `Tuition fees up to date`, `Gender`, `Scholarship holder`, `International`, `Daytime/evening attendance`).
- **Continuous Ratio/Interval Scales:** `Admission grade`, `Previous qualification (grade)`, curricular grades (0–20 scale), and macroeconomic rates.

---

## 7. Potential Data Quality & Syntactic Issues
1. **Trailing Whitespace in Column Names:** The official CSV column header for daytime/evening attendance contains an escaped tab character: `'Daytime/evening attendance\t'`.
   - *Remediation:* Clean all column names using `.str.strip()` upon ingestion.
2. **Spelling Conventions:** Portuguese spelling variants are present in the official dataset (e.g., `'Nacionality'`).
   - *Remediation:* Standardize column naming or map systematically while retaining traceability to UCI metadata.
3. **Zero Values in Academic Performance:** Curricular unit grades of `0.0` occur predominantly when students complete zero evaluations or approve zero units. These represent valid factual states (did not pass or attend exams) rather than corrupted missing values.

---

## 8. Data Leakage & Temporal Risk Analysis: Official Feature Verification
A critical methodological hazard in student dropout modeling is **temporal data leakage**:
- **Risk:** The 12 curricular progress features (`Curricular units 1st sem ...` and `Curricular units 2nd sem ...`) reflect outcomes measured *after* one to two full semesters of college. A student with 0 approved units in the 2nd semester is virtually guaranteed to be a dropout, allowing an ML model to achieve deceptively high accuracy by "peeking into the future".
- **Real-World Utility:** An institution cannot use a 2nd-semester completion model to identify at-risk students upon matriculation.
- **Systematic Feature Verification Against Official UCI Definitions & Realinho et al. (2021):**

| Feature | Available at enrollment/early stage? | Reason | Included in Perspective A? | Evidence/source |
| :--- | :--- | :--- | :--- | :--- |
| `Marital status` | **Yes** | Personal demographic status recorded on the institutional admissions application form. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Demographic data. |
| `Application mode` | **Yes** | Specifies the application pathway/contingent (e.g., 1st phase, transfer, ordinance) determined during admission. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Academic data - enrollment. |
| `Application order` | **Yes** | The institutional preference ranking (0-9) submitted by the applicant at the time of university selection. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Academic data - enrollment. |
| `Course` | **Yes** | The specific higher education degree program into which the student is matriculated. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Academic data - enrollment. |
| `Daytime/evening attendance` | **Yes** | The attendance modality/shift chosen upon formal enrollment registration. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Academic data - enrollment. |
| `Previous qualification` | **Yes** | Prior credential/diploma achieved before university entry (secondary education or prior degree). | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Academic data - enrollment. |
| `Previous qualification (grade)` | **Yes** | Grade achieved on the prior qualifying examination/high school certificate (0-200 scale). | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Academic data - enrollment. |
| `Nacionality` | **Yes** | Student citizenship declared on legal matriculation documentation. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Demographic data. |
| `Mother's qualification` | **Yes** | Parental educational background reported on institutional student profile during intake. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Social-economic data. |
| `Father's qualification` | **Yes** | Parental educational background reported on institutional student profile during intake. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Social-economic data. |
| `Mother's occupation` | **Yes** | Parental professional occupation code recorded at intake. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Social-economic data. |
| `Father's occupation` | **Yes** | Parental professional occupation code recorded at intake. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Social-economic data. |
| `Admission grade` | **Yes** | Standardized competitive entrance score computed for higher education admission (0-200 scale). | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Academic data - enrollment. |
| `Displaced` | **Yes** | Identifies if the student had to relocate from their permanent residence to attend college. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Demographic data. |
| `Educational special needs` | **Yes** | Registered accommodation/disability status established during enrollment. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Educational special needs. |
| `Debtor` | **Yes** | Flag indicating previous outstanding debt or fee arrears to the polytechnic institution at registration. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Debtor (administrative record). |
| `Tuition fees up to date` | **Yes (with caveat)** | Indicates whether first tuition payment/registration fee was fulfilled at enrollment. (Investigated for post-enrollment leakage risk). | **Yes (baseline)** | UCI doc & Realinho et al. (2021) Table 1: Tuition fees up to date. |
| `Gender` | **Yes** | Demographic binary indicator (1 = Male, 0 = Female) from admissions record. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Demographic data. |
| `Scholarship holder` | **Yes** | Social grant/merit scholarship award status granted upon entry. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Scholarship holder. |
| `Age at enrollment` | **Yes** | Chronological age computed directly at the date of matriculation. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Demographic data. |
| `International` | **Yes** | Foreign student visa/contingent classification known at registration. | **Yes** | UCI doc & Realinho et al. (2021) Table 1: Demographic data. |
| `Curricular units 1st sem (credited)` | **No** | Requires completed evaluation and validation of credit transfers after 1st semester. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 1st semester. |
| `Curricular units 1st sem (enrolled)` | **No (Academic Progress)** | Reflects academic load finalized across the 1st semester course period. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 1st semester. |
| `Curricular units 1st sem (evaluations)` | **No** | Total number of exam/assignment attempts during winter examination sessions. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 1st semester. |
| `Curricular units 1st sem (approved)` | **No** | Final number of courses passed after mid-year exam grading (Feb/March). | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 1st semester. |
| `Curricular units 1st sem (grade)` | **No** | Grade point average earned across 1st semester curricular units. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 1st semester. |
| `Curricular units 1st sem (without evaluations)` | **No** | Number of enrolled units where student skipped all evaluations. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 1st semester. |
| `Curricular units 2nd sem (credited)` | **No** | Longitudinal academic milestone recorded at conclusion of second term. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 2nd semester. |
| `Curricular units 2nd sem (enrolled)` | **No** | Spring semester enrollment registration count finalized months after matriculation. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 2nd semester. |
| `Curricular units 2nd sem (evaluations)` | **No** | Spring exam evaluation attempts recorded at end of academic year (June/July). | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 2nd semester. |
| `Curricular units 2nd sem (approved)` | **No** | End-of-year courses passed; strong direct determinant of progression. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 2nd semester. |
| `Curricular units 2nd sem (grade)` | **No** | Spring semester GPA earned across 2nd semester courses. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 2nd semester. |
| `Curricular units 2nd sem (without evaluations)` | **No** | Non-attendance/abandonment metric recorded at end of academic year. | **No** | UCI doc & Realinho et al. (2021) Table 1: Academic data - 2nd semester. |
| `Unemployment rate` | **Yes** | Annual national unemployment figure published for the student's admission year cohort. | **Yes** | UCI doc & Realinho et al. (2021) Section 2: Macroeconomic data at intake. |
| `Inflation rate` | **Yes** | Annual inflation rate published for the student's admission year cohort. | **Yes** | UCI doc & Realinho et al. (2021) Section 2: Macroeconomic data at intake. |
| `GDP` | **Yes** | Annual economic GDP growth percentage corresponding to the student's enrollment year. | **Yes** | UCI doc & Realinho et al. (2021) Section 2: Macroeconomic data at intake. |

### Methodological Summary of Modeling Perspectives:
1. **Perspective A (Pre-Enrollment / Early-Stage Screening):** 24 audited features known strictly at or prior to enrollment start. Evaluates institutional capacity to proactively detect at-risk students before first-semester classes begin.
2. **Perspective B (Academic-Progress / Longitudinal Model):** Full 36 features incorporating 1st and 2nd semester curricular performance (credits, evaluations, approved units, GPA). Evaluates performance gains when in-college academic history is observable.

---

## 9. Conclusion of Audit & Sign-Off
The dataset is clean, structurally sound, free of missing values and duplicates, and fully suited for multiclass predictive modeling. By enforcing strict separation of pre-enrollment vs. longitudinal feature sets, we prevent accidental data leakage while delivering deep institutional insights.
