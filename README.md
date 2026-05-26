# sql-data-warehouse-project
# Home Credit Default Risk - SQL Data Warehouse Project

## Overview

This project is an end-to-end SQL Server Data Warehouse project built using the Home Credit Default Risk dataset from Kaggle.

The main goal of this project is to simulate a real-world Data Engineering and Analytics workflow using Medallion Architecture (Bronze → Silver → Gold) inside SQL Server.

The project covers:
- Raw data ingestion
- ETL pipeline development
- Data cleaning & standardization
- Analytical data modeling
- Business-ready reporting layer
- Data quality validation
- Risk analytics

---

# Project Architecture

```text
Source CSV Files
        ↓
Bronze Layer (Raw Data)
        ↓
Silver Layer (Cleaned & Standardized Data)
        ↓
Gold Layer (Business Ready Analytics Views)
        ↓
Power BI / Analytics / Reporting
```

---

# Dataset

Dataset used:

Home Credit Default Risk Dataset from Kaggle

Dataset Link:

https://www.kaggle.com/competitions/home-credit-default-risk/data

Note:
Large CSV files are not uploaded to GitHub.

Datasets were stored locally in:

```text
C:\home-credit-default-risk\
```

---

# Tech Stack

- SQL Server
- SSMS / Azure Data Studio
- T-SQL
- Medallion Architecture
- Power BI
- Git & GitHub

---

# Medallion Architecture

## Bronze Layer

Purpose:
Store raw CSV data exactly as received from source files.

Characteristics:
- Raw ingestion
- No transformations
- Batch loading using BULK INSERT
- Truncate & Insert strategy

Main Tables:
- application_train
- application_test
- bureau
- bureau_balance
- previous_application
- installments_payments
- POS_CASH_balance
- credit_card_balance
- sample_submission
- HomeCredit_columns_description

---

## Silver Layer

Purpose:
Clean and standardize raw data for analytics usage.

Transformations performed:
- NULL handling
- TRY_CAST conversions
- Standardized categorical values
- Derived columns
- Financial ratios
- Payment behavior flags
- Risk indicators

Examples:
- age_years
- employment_years
- credit_income_ratio
- annuity_income_ratio
- overdue_flag
- underpaid_flag
- late_payment_flag

---

## Gold Layer

Purpose:
Create business-ready analytical views for reporting and BI tools.

Gold Objects:

### Dimensions
- gold.dim_customer

### Facts
- gold.fact_loan_application
- gold.fact_payment_behavior
- gold.fact_credit_history

### Reporting Views
- gold.report_customer_risk_summary

---

# Row Counts

| Table | Rows |
|---|---|
| bronze.application_train | 307511 |
| bronze.application_test | 48744 |
| bronze.bureau | 1716428 |
| bronze.bureau_balance | 27299925 |
| bronze.previous_application | 1670214 |
| bronze.installments_payments | 13605401 |
| bronze.POS_CASH_balance | 10001358 |
| bronze.credit_card_balance | 3840312 |

---

# Data Quality Checks

Validation scripts were created for:
- Bronze Layer
- Silver Layer
- Gold Layer

Checks include:
- Row count validation
- NULL key checks
- Duplicate detection
- Referential validation
- Financial sanity checks
- Risk segmentation validation

---

# Key Business Metrics

Examples of analytical metrics created:
- Default Rate
- Credit-to-Income Ratio
- Annuity-to-Income Ratio
- Payment Completion Ratio
- Overdue Credit Count
- Risk Segmentation

---

# Folder Structure

```text
sql-data-warehouse-project/
│
├── datasets/
├── docs/
├── scripts/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│   └── tests/
│
├── analytics/
├── powerbi/
└── README.md
```

---

# Learning Outcomes

This project helped me understand:
- Medallion Architecture
- ETL pipeline design
- Data warehouse layering
- Data cleaning strategies
- Star schema concepts
- Business-oriented analytics
- SQL optimization & transformations
- Real-world analytical workflows

---

# Future Improvements

Planned improvements:
- Incremental loading
- SCD implementation
- SQL Agent scheduling
- Advanced Power BI dashboards
- ML-based risk prediction
- Data orchestration using Airflow/Fabric

---

