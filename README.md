# Medical-Fraud-Detection
1. Project Overview
Medicare fraud is a significant issue that increases healthcare costs and undermines the integrity of healthcare systems. This project aims to detect potential fraudulent claims submitted by healthcare providers using machine learning models and data analysis techniques.
2. Project Description

    Objective: To develop a machine learning model to identify fraudulent Medicare claims based on inpatient, outpatient, and beneficiary data.
    Datasets:
        Inpatient Data: Contains claims for admitted patients with details like admission/discharge dates and diagnoses.
        Outpatient Data: Contains claims for non-admitted patients.
        Beneficiary Data: Includes demographic information and chronic conditions of beneficiaries.
    Key Features:
        Claims amount reimbursed (InscClaimAmtReimbursed).
        Length of stay (LengthOfStay).
        Diagnosis and procedure codes.
        Chronic conditions of beneficiaries.

3. Workflow and Methodology

    Data Loading:
        Load inpatient, outpatient, and beneficiary datasets into PySpark DataFrames.
    Data Cleaning:
        Handle missing values using fillna() for categorical columns (Unknown) and numerical columns (0).
        Align schemas between inpatient and outpatient datasets by adding missing columns with null values.
    Feature Engineering:
        Calculate LengthOfStay for inpatient claims as the difference between DischargeDt and AdmissionDt.
        Derive Age from the DOB column.
    Fraud Detection Rules:
        High reimbursement amounts ($20,000+).
        Short stays (≤≤ 2 days) with high costs ($5,000+).
        Duplicate claims for the same beneficiary with overlapping dates.
        Excessive claims by providers (e.g., more than 100 claims).
    Machine Learning Models:
        Models like Random Forest, Logistic Regression, and Gradient Boosting were trained to classify providers as fraudulent or non-fraudulent.

4. Challenges Encountered

    Schema Mismatch:
        Inpatient and outpatient datasets had different schemas, causing errors during the union operation.
    Missing Columns:
        Columns like AdmissionDt and DischargeDt were missing in outpatient data.
    Imbalanced Data:
        Fraudulent claims were significantly fewer than non-fraudulent ones, leading to class imbalance issues during model training.

5. Troubleshooting Steps

    To resolve schema mismatch errors:
        Identified missing columns using set(inpatient_df.columns) - set(outpatient_df.columns).
        Added missing columns to outpatient data using withColumn() with default values (None or 0).
    To address class imbalance:
        Used oversampling techniques like SMOTE (Synthetic Minority Oversampling Technique) to balance the dataset.
    To handle unresolved column errors:
        Verified column names in all datasets before performing operations like joins or unions.

6. Lessons Learned and Future Improvements

    Importance of schema alignment when working with multiple datasets.
    Handling imbalanced datasets effectively improves model performance.
    Future improvements:
        Incorporate additional features like relationships between providers and beneficiaries.
        Use advanced anomaly detection techniques like autoencoders for unsupervised fraud detection.
