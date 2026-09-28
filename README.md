# Hospital Readmission & Healthcare Patient Analytics

This repository contains the end-to-end analytical problem formulation, healthcare planning, and clinical data preparation for predicting 30-day hospital readmissions among diabetic patients.

---

## 👨‍🎓 Student Details
* **Student Name**: Akshad Viresh Makhana
* **PRN**: `2124UDSM1007`
* **Department**: TY AIDS(A)
* **GitHub Repository**: [https://github.com/akshad1007/Hospital-Readmission-Patient-Analytics](https://github.com/akshad1007/Hospital-Readmission-Patient-Analytics)
* **Git Remote URL**: `https://github.com/akshad1007/Hospital-Readmission-Patient-Analytics.git`
* **Dataset**: [Diabetes 130-US Hospitals for years 1999–2008](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008) (UCI Machine Learning Repository ID: 296)

---

## 📁 Repository Structure
```
├── Project_1_Hospital_Readmission_Risk_Analytics_Problem_Definition_and_Planning.ipynb
├── Project_2_Healthcare_Data_Preparation_for_Patient_Analytics.ipynb
├── clean_healthcare_dataset.csv
├── dataset_diabetes/
│   ├── diabetic_data.csv
│   └── IDS_mapping.csv
└── README.md
```

---

## 🏥 Project 1: Hospital Readmission Risk Analytics Problem Definition and Planning
* **File**: `Project_1_Hospital_Readmission_Risk_Analytics_Problem_Definition_and_Planning.ipynb`
* **Objective**: Independently understand the healthcare analytics problem and define the analytics requirements prior to model implementation.

### Key Activities & Coverage:
1. **Business Understanding**:
   * **Hospital Readmission Problem**: Analysis of 30-day readmissions in diabetes due to medication volatility and comorbidities.
   * **Healthcare Cost Impact**: Evaluation of CMS Hospital Readmissions Reduction Program (HRRP) penalty cuts (up to 3% Medicare reduction) and $17B annual avoidable US expenditure.
   * **Patient Care Improvement**: Prevention of hospital-acquired infections (HAIs) and care transition protocols.
   * **Hospital Operational Efficiency**: Bed turnover, ER congestion relief, and targeted care coordination.
2. **Healthcare Stakeholders & Challenges**:
   * Multi-disciplinary stakeholder mapping (CMO, CFO, Care Coordinators, Physicians, Patients).
   * Addressing class imbalance (~11.2% high risk) and asymmetric misclassification penalty ($FN \gg FP$).
3. **Dataset Understanding & Feature Dictionary**:
   * Review of 101,766 inpatient admissions and 50 attributes.
   * Feature dictionary detailing data types, missingness, domain values, and clinical descriptions.
   * Target variable analysis: `readmitted` (`<30` high risk vs `>30` / `NO`).
4. **Problem Formulation**:
   * **Supervised Classification**: Predicting High Readmission Risk ($<30$ days) with class-weighted Logistic Regression, ROC-AUC, and Confusion Matrix.
   * **Unsupervised Clustering**: Segmenting patients into 3 clinical phenotypes using K-Means and 2D PCA projection.
5. **Basic Analytics Planning & Governance**:
   * 5-stage clinical analytics workflow.
   * Mermaid project roadmap Gantt chart.
   * Git repository architecture.
   * **Ethics Report**: HIPAA de-identification compliance, algorithmic fairness across demographic groups, and clinical decision support transparency.

---

## 🧪 Project 2: Healthcare Data Preparation for Patient Analytics
* **File**: `Project_2_Healthcare_Data_Preparation_for_Patient_Analytics.ipynb`
* **Objective**: Execute clinical data cleaning, feature transformations, and engineering to produce a machine-learning-ready patient analytics cohort.

### Key Activities & Coverage:
1. **Data Cleaning**:
   * **Dataset Ingestion**: Loaded 101,766 raw encounters.
   * **Handling Missing Records**: Dropped unusable `weight` (96.86% missing), mode-imputed `race`, preserved `payer_code` and `medical_specialty` with explicit missing flags.
   * **Duplicate Encounter Resolution**: Deduplicated records by `patient_nbr` retaining the first index admission (preventing label leakage).
   * **Invalid Value Detection**: Excluded invalid gender records and terminal discharge disposition codes (deceased and hospice patients, disposition IDs: 11, 13, 14, 19, 20, 21).
   * Resulted in **69,987 unique patient admissions**.
2. **Data Transformation**:
   * **Variable Conversion**: Age brackets converted to continuous numeric midpoints (`age_numeric`); treatment change and prescribed meds mapped to binary indicators.
   * **Categorical Encoding**: 23 diabetic medication dosage adjustments mapped to ordinal intensity scales (`No`: 0, `Steady`: 1, `Up`/`Down`: 2).
   * **Feature Scaling**: Evaluated `StandardScaler` vs `RobustScaler` on skewed utilization attributes; adopted `RobustScaler` to handle extreme healthcare utilization outliers.
3. **Feature Engineering**:
   * **Patient Age Groups**: Granular age stratification (`Pediatric_Young_Adult`, `Working_Adult`, `Mature_Adult`, `Geriatric_High_Risk`).
   * **Admission Frequency**: Constructed `total_prior_encounters` and `emergency_intensity_ratio`.
   * **Risk Indicators**: Built flags for severe polypharmacy ($\ge 15$ medications), uncontrolled glycemia ($\text{A1C} > 8\%$ or glucose $> 200$), and high-risk comorbidity triad (Circulatory, Renal, and Endocrine ICD-9 codes).
   * **Composite Healthcare Utilization Score**: Weighted metric combining hospital length of stay, procedures, and prior emergency/inpatient utilization.
4. **Exported Clean Dataset**:
   * Saved to `clean_healthcare_dataset.csv` (69,987 rows × 31 curated columns, ~8.2 MB).

---

## 🛠️ Environment & Prerequisites
To run the notebooks locally, install the required Python packages:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn ucimlrepo nbformat
```

Launch Jupyter Notebook:
```bash
jupyter notebook
```
