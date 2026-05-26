# 🏗️ Home Credit Default Risk - SQL Data Warehouse Project

> An end-to-end enterprise data warehouse implementation using Medallion Architecture, SQL Server, and modern analytics practices.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Project Architecture](#project-architecture)
- [Dataset](#dataset)
- [Tech Stack](#tech-stack)
- [Medallion Architecture](#medallion-architecture)
- [Data Metrics](#data-metrics)
- [Data Quality & Validation](#data-quality--validation)
- [Key Analytics](#key-analytics)
- [Project Structure](#project-structure)
- [Learning Outcomes](#learning-outcomes)
- [Future Roadmap](#future-roadmap)
- [Author](#author)

---

## 🎯 Overview

This project demonstrates a **production-grade data warehouse** using the **Home Credit Default Risk** dataset from Kaggle. It simulates a real-world Data Engineering and Analytics workflow, implementing enterprise-level best practices.

### What This Project Covers:
✅ Raw data ingestion from multiple CSV sources  
✅ Scalable ETL pipeline development  
✅ Data cleaning, validation, and standardization  
✅ Dimensional & factual data modeling  
✅ Business-ready analytics layer  
✅ Data quality assurance framework  
✅ Enterprise-level risk analytics  

---

## 🏛️ Project Architecture

```
┌─────────────────────────────────────────────────────────┐
│          Source CSV Files (Kaggle Dataset)              │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│   Bronze Layer - Raw Data (No Transformations)          │
│   [BULK INSERT | Truncate & Load Strategy]             │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│  Silver Layer - Cleaned & Standardized Data             │
│  [Transformations | Quality Checks | Enrichment]       │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│   Gold Layer - Business Ready Analytics Views           │
│   [Dimensions | Facts | Reporting Views]               │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│   Analytics & Reporting (Power BI | Dashboards)         │
└─────────────────────────────────────────────────────────┘
```

---

## 📊 Dataset

### Source Information
- **Dataset Name:** Home Credit Default Risk
- **Source:** [Kaggle Competition](https://www.kaggle.com/competitions/home-credit-default-risk/data)
- **Domain:** Credit Risk Analytics & Financial Services
- **Data Volume:** ~60M+ records across 8 main tables

### Dataset Structure
| Category | Files |
|----------|-------|
| **Application Data** | application_train, application_test |
| **Credit History** | bureau, bureau_balance, previous_application |
| **Payment Records** | installments_payments, POS_CASH_balance, credit_card_balance |
| **Metadata** | sample_submission, HomeCredit_columns_description |

> 📝 **Note:** Large CSV files are stored locally at `C:\home-credit-default-risk\` and not included in the GitHub repository due to size constraints.

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Database Engine** | SQL Server 2019+ |
| **IDE/Tools** | SSMS, Azure Data Studio |
| **Language** | T-SQL |
| **Architecture** | Medallion (Bronze-Silver-Gold) |
| **BI/Analytics** | Power BI |
| **Version Control** | Git & GitHub |

---

## 🏗️ Medallion Architecture Details

### **Bronze Layer** 🥉
The foundation layer that stores raw data in its original state.

**Purpose:**
- Exact replica of source data
- Audit trail and data lineage
- Rollback capability

**Characteristics:**
- ✓ Raw ingestion without transformations
- ✓ Batch loading via `BULK INSERT`
- ✓ Truncate & Insert loading strategy
- ✓ Schema matches source files

**Main Tables:**
```
📦 Bronze Schema
├── application_train (307,511 rows)
├── application_test (48,744 rows)
├── bureau (1,716,428 rows)
├── bureau_balance (27,299,925 rows)
├── previous_application (1,670,214 rows)
├── installments_payments (13,605,401 rows)
├── POS_CASH_balance (10,001,358 rows)
├── credit_card_balance (3,840,312 rows)
├── sample_submission
└── HomeCredit_columns_description
```

---

### **Silver Layer** 🥈
The processing layer that transforms and standardizes data for analytics.

**Purpose:**
- Single source of truth for analytics
- Consistent data quality
- Reduced redundancy

**Transformations Applied:**
- ✓ NULL value handling and imputation
- ✓ Type casting & validation (TRY_CAST)
- ✓ Categorical standardization
- ✓ Derived business columns
- ✓ Financial metrics calculation
- ✓ Payment behavior analysis flags
- ✓ Risk indicators computation

**Enriched Columns Created:**
```
📊 Business-Ready Metrics
├── age_years (Age standardization)
├── employment_years (Tenure calculation)
├── credit_income_ratio (Credit exposure)
├── annuity_income_ratio (Debt burden)
├── overdue_flag (Payment status)
├── underpaid_flag (Underpayment detection)
├── late_payment_flag (Delinquency indicator)
└── [Additional risk indicators]
```

---

### **Gold Layer** 🏆
The presentation layer optimized for reporting and business intelligence.

**Purpose:**
- Serve analytics and BI tools
- Denormalized for query performance
- Business logic encapsulation

**Gold Objects:**

#### Dimensions
- `gold.dim_customer` - Customer master dimension with demographic and financial attributes

#### Fact Tables
- `gold.fact_loan_application` - Core lending application facts and metrics
- `gold.fact_payment_behavior` - Payment transaction details and patterns
- `gold.fact_credit_history` - Historical credit interaction records

#### Reporting Views
- `gold.report_customer_risk_summary` - Executive summary view for risk assessment

---

## 📈 Data Metrics

### Table Statistics

| Table | Row Count | Purpose |
|-------|-----------|---------|
| `bronze.application_train` | **307,511** | Training data for default prediction |
| `bronze.application_test` | **48,744** | Test dataset for model validation |
| `bronze.bureau` | **1,716,428** | Bureau credit history records |
| `bronze.bureau_balance` | **27,299,925** | Monthly bureau balance snapshots |
| `bronze.previous_application` | **1,670,214** | Historical application data |
| `bronze.installments_payments` | **13,605,401** | Individual payment transaction records |
| `bronze.POS_CASH_balance` | **10,001,358** | Point-of-sale balance details |
| `bronze.credit_card_balance` | **3,840,312** | Credit card statement records |

**Total Records:** ~60M+ rows across all tables

---

## ✅ Data Quality & Validation

### Validation Framework
Comprehensive validation scripts ensure data integrity across all layers:

```
🔍 Quality Checks Implemented
│
├── Row Count Validation
│   └── Verify record counts match source extracts
│
├── NULL Key Checks
│   └── Ensure primary keys are non-null
│
├── Duplicate Detection
│   └── Identify and flag duplicate records
│
├── Referential Integrity
│   └── Validate foreign key relationships
│
├── Financial Sanity Checks
│   └── Range validation for financial fields
│
└── Risk Segmentation Validation
    └── Verify risk classifications are correct
```

**Layers Covered:**
- ✓ Bronze Layer validation (raw data integrity)
- ✓ Silver Layer validation (transformation accuracy)
- ✓ Gold Layer validation (reporting accuracy)

---

## 📊 Key Business Analytics

### Core Metrics Implemented

| Metric | Description | Business Impact |
|--------|-------------|-----------------|
| **Default Rate** | Percentage of customers with default events | Risk assessment |
| **Credit-to-Income Ratio** | Total credit vs. annual income | Creditworthiness |
| **Annuity-to-Income Ratio** | Loan amount vs. income | Debt burden analysis |
| **Payment Completion Ratio** | On-time vs. total payments | Payment reliability |
| **Overdue Credit Count** | Number of overdue accounts | Portfolio health |
| **Risk Segmentation** | Customer classification by risk tier | Portfolio stratification |

### Risk Segmentation Model
```
Risk Tiers
├── Low Risk (Score: 0-40)
├── Medium Risk (Score: 41-70)
├── High Risk (Score: 71-85)
└── Critical Risk (Score: 86-100)
```

---

## 📁 Project Structure

```
sql-data-warehouse-project/
│
├── 📂 datasets/
│   └── [Source CSV files - stored locally]
│
├── 📂 docs/
│   ├── data_dictionary.md
│   ├── architecture_design.md
│   └── business_requirements.md
│
├── 📂 scripts/
│   ├── 📂 bronze/
│   │   ├── 01_create_bronze_schema.sql
│   │   ├── 02_create_bronze_tables.sql
│   │   └── 03_load_bronze_data.sql
│   │
│   ├── 📂 silver/
│   │   ├── 01_create_silver_schema.sql
│   │   ├── 02_silver_transformations.sql
│   │   └── 03_data_enrichment.sql
│   │
│   ├── 📂 gold/
│   │   ├── 01_create_gold_schema.sql
│   │   ├── 02_create_dimensions.sql
│   │   ├── 03_create_facts.sql
│   │   └── 04_create_reporting_views.sql
│   │
│   └── 📂 tests/
│       ├── bronze_quality_checks.sql
│       ├── silver_quality_checks.sql
│       └── gold_quality_checks.sql
│
├── 📂 analytics/
│   ├── customer_risk_analysis.sql
│   ├── payment_behavior_analysis.sql
│   └── default_prediction_insights.sql
│
├── 📂 powerbi/
│   ├── dashboard_definitions.pbix
│   └── data_model.xml
│
└── 📄 README.md
```

---

## 🎓 Learning Outcomes

This project enabled me to master:

### Architecture & Design
- ✅ **Medallion Architecture** - Implementing layered data transformation patterns
- ✅ **ETL Pipeline Design** - Building robust, scalable data pipelines
- ✅ **Data Warehouse Layering** - Separating concerns across bronze/silver/gold
- ✅ **Star Schema Concepts** - Dimensional modeling for analytics

### Data Engineering
- ✅ **Data Cleaning Strategies** - Handling missing values, outliers, duplicates
- ✅ **SQL Optimization** - Query performance tuning and indexing
- ✅ **T-SQL Transformations** - Complex business logic implementation
- ✅ **Data Quality Frameworks** - Building validation systems

### Business & Analytics
- ✅ **Real-world Workflows** - End-to-end analytical pipeline
- ✅ **Business-oriented Analytics** - Translating requirements to metrics
- ✅ **Risk Analytics** - Understanding credit risk modeling
- ✅ **Data Storytelling** - Creating actionable insights

---

## 🚀 Future Roadmap

The following enhancements are planned to make this a production-grade system:

### Immediate Improvements
- [ ] **Incremental Loading** - Replace truncate-load with delta processing
- [ ] **SCD Implementation** - Type 2 slowly changing dimensions
- [ ] **SQL Agent Scheduling** - Automated daily/weekly ETL runs
- [ ] **Data Lineage Tracking** - Full audit trail of transformations

### Advanced Features
- [ ] **Advanced Power BI Dashboards** - Interactive executive dashboards
- [ ] **ML-based Risk Prediction** - Predictive default models
- [ ] **Data Orchestration** - Airflow/Fabric/Databricks integration
- [ ] **API Layer** - REST endpoints for analytics queries
- [ ] **Data Governance** - Cataloging and metadata management
- [ ] **Performance Monitoring** - Query execution analytics

---

## 👤 Author

**Anumodit Shukla**

📚 **Education:**  
B.Tech in Biotechnology & Biochemical Engineering  
National Institute of Technology (NIT) Agartala

💼 **Professional Interests:**
- 📊 Data Analytics & Business Intelligence
- 🔧 Data Engineering & ETL Development
- 🤖 Machine Learning & Predictive Modeling
- 🏗️ Data Architecture & Warehouse Design

🔗 **Connect with me:**

<a href="https://github.com/anumodit740" target="_blank">
  <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
</a>
<a href="https://www.linkedin.com/in/anumodit-shukla-59aa18288" target="_blank">
  <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
</a>

---

<div align="center">

### ⭐ If this project helped you, please consider giving it a star!

**Happy Data Engineering! 🎉**

</div>
