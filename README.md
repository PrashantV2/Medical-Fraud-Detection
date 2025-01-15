# Medical Fraud Detection

## 1. Project Overview

Medicare fraud is a critical issue that increases healthcare costs and undermines the integrity of healthcare systems. This project aims to detect potential fraudulent claims submitted by healthcare providers using machine learning models and data analysis techniques.

---

## 2. Project Description

### Objective
To develop a machine learning model to identify fraudulent Medicare claims based on inpatient, outpatient, and beneficiary data.

### Datasets
- **Inpatient Data**: Contains claims for admitted patients with details like admission/discharge dates and diagnoses.
- **Outpatient Data**: Contains claims for non-admitted patients.
- **Beneficiary Data**: Includes demographic information and chronic conditions of beneficiaries.

### Key Features
- **Claims Amount Reimbursed** (`InscClaimAmtReimbursed`).
- **Length of Stay** (`LengthOfStay`).
- Diagnosis and procedure codes.
- Chronic conditions of beneficiaries.

---

## 3. Workflow and Methodology

### Data Loading
- Load inpatient, outpatient, and beneficiary datasets into PySpark DataFrames.

### Data Cleaning
- Handle missing values:
  - **Categorical Columns**: Replace with `Unknown`.
  - **Numerical Columns**: Replace with `0`.
- Align schemas between inpatient and outpatient datasets by adding missing columns with null values.

### Feature Engineering
- Calculate **Length of Stay** for inpatient claims as the difference between `DischargeDt` and `AdmissionDt`.
- Derive **Age** from the `DOB` column.

### Fraud Detection Rules
- High reimbursement amounts (e.g., **$20,000+**).
- Short stays (≤ 2 days) with high costs (e.g., **$5,000+**).
- Duplicate claims for the same beneficiary with overlapping dates.
- Excessive claims by providers (e.g., more than 100 claims).


---

## 4. Challenges Encountered

### Schema Mismatch
- Inpatient and outpatient datasets had different schemas, causing errors during union operations.

### Missing Columns
- Columns like `AdmissionDt` and `DischargeDt` were missing in outpatient data.

### Imbalanced Data
- Fraudulent claims were significantly fewer than non-fraudulent ones, leading to class imbalance issues during model training.

---

## 5. Troubleshooting Steps

### Resolving Schema Mismatch Errors
- Identified missing columns using:
  ```python
  set(inpatient_df.columns) - set(outpatient_df.columns)
