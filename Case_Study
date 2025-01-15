# Case Study: Medicare Fraud Detection

## 1. Executive Summary

Medicare fraud is a significant issue, leading to billions of dollars in losses annually. This project focuses on detecting fraudulent claims submitted by healthcare providers using data analysis and machine learning techniques. By analyzing inpatient, outpatient, and beneficiary data, the project identifies suspicious patterns and flags potential fraud cases for further investigation.

---

## 2. Problem Statement

Medicare fraud occurs when healthcare providers submit false or misleading claims to obtain reimbursement for services that were not provided or were unnecessary. This not only increases healthcare costs but also impacts the quality of care for legitimate beneficiaries.

### Goals:
- Detect fraudulent claims based on suspicious patterns in provider behavior.
- Identify high-risk providers for further auditing.

---

## 3. Objectives

1. Analyze Medicare claims data (inpatient, outpatient, and beneficiary datasets) to identify fraudulent claims.
2. Develop a machine learning-based fraud detection system that flags potential fraud cases.
3. Provide actionable insights into provider behavior for fraud prevention.

---

## 4. Data Description

### Datasets Used:
1. **Inpatient Data**
   - Details of admitted patients, including admission/discharge dates, diagnoses, and reimbursement amounts.
   - **Key Columns**: `BeneID`, `ClaimID`, `AdmissionDt`, `DischargeDt`, `InscClaimAmtReimbursed`.

2. **Outpatient Data**
   - Details of non-admitted patients.
   - **Key Columns**: `BeneID`, `ClaimID`, `ClaimStartDt`, `ClaimEndDt`, `InscClaimAmtReimbursed`.

3. **Beneficiary Data**
   - Demographic details (e.g., age, gender) and chronic conditions of beneficiaries.
   - **Key Columns**: `BeneID`, `DOB`, `DOD`, `ChronicCond_Diabetes`, etc.

---

## 5. Methodology

### Step 1: Data Preprocessing
- Loaded datasets into PySpark DataFrames.
- Handled missing values:
  - Replaced missing categorical values with `'Unknown'`.
  - Filled missing numerical values with `0`.
- Aligned schemas between inpatient and outpatient datasets by adding missing columns with default values (`None`).

### Step 2: Feature Engineering
- **Calculated New Features**:
  - `LengthOfStay`: Difference between `DischargeDt` and `AdmissionDt` for inpatient claims.
  - `Age`: Derived from the beneficiary's `DOB`.
- Standardized column names across datasets for consistency.

### Step 3: Fraud Detection Rules
Applied the following rules to identify potential fraud cases:
1. **High Reimbursement Amounts**:
   - Flagged claims with reimbursement amounts greater than `$20,000`.
2. **Short Stays with High Costs**:
   - Flagged inpatient claims with a `LengthOfStay ≤ 2 days` but reimbursement amounts greater than `$5,000`.
3. **Duplicate Claims**:
   - Identified multiple claims for the same beneficiary (`BeneID`) with overlapping dates.
4. **Excessive Claims by Providers**:
   - Flagged providers submitting an unusually high number of claims (e.g., more than 100).



---

## 6. Challenges Encountered

### 1. Schema Mismatch
- **Issue**: Inpatient and outpatient datasets had different schemas, causing errors during data integration.
- **Solution**: Added missing columns to outpatient data using PySpark's `withColumn()` function.

### 2. Imbalanced Dataset
- **Issue**: Fraudulent claims were significantly fewer than non-fraudulent ones, leading to class imbalance during model training.
- **Solution**: Used oversampling techniques like **SMOTE** to balance the dataset.

### 3. Unresolved Column Errors
- **Issue**: Some columns were not recognized due to inconsistent naming conventions across datasets.
- **Solution**: Standardized column names before performing operations like joins or unions.

