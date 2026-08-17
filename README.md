# Churn-Analysis-Customer-Intelligence
End-to-end OTT subscriber churn analysis and customer retention intelligence pipeline using Python (Pandas, Seaborn) and SQL (SQLite).
# 📉 OTT Subscriber Churn Analysis & Customer Retention Intelligence

## 📌 Executive Summary
In subscription video-on-demand (SVOD/OTT) platforms (e.g., Netflix, Disney+ Hotstar, Amazon Prime), customer retention directly dictates business profitability. 

This project delivers an **end-to-end data analytics and retention intelligence pipeline** analyzing customer demographics, subscription plans, billing models, and support interactions from a relational SQLite database.

---

### 🎯 Key Performance Indicators (KPIs)
* **Overall Churn Rate:** `28.57%` (6 out of 21 accounts canceled)
* **Retention Rate:** `71.43%`
* **Average Revenue Per User (ARPU):** `₹18.85 / month`
* **Average Customer Tenure:** `1,510 Days` (~4.1 years)
* **Monthly Revenue at Risk (MRR):** `₹73.94 / month` (18.7% revenue leakage)
* **Total Customer Lifetime Value (CLTV) Lost:** `₹2,047`
* **Escalation-to-Churn Correlation:** `0.77` (Strong positive correlation)

---

## 🗂️ Data Architecture & Relational Schema
The data was extracted from a relational database (`customer_churn.db`) comprising three core entities:
* **`db_customer`**: Demographic and geographical records (`customerid`, `customer_name`, `country`, `state`, `gender`, `dob`).
* **`db_subscription`**: Plan details, billing intervals, cancellation dates, and churn risk scores (`plan_type`, `contract_type`, `monthly_charges`, `cltv`, `churn_score`).
* **`db_support`**: Customer support tickets, issue severity, and satisfaction scores (`complaint_date`, `escalations`, `csat_score`, `complaint_count`).

---

## ⚙️ Analytics Pipeline & Methodology
1. **Database Ingestion:** Established Python SQLite3 connection and queried relational tables into Pandas DataFrames.
2. **Data Cleaning & Standardization:** 
   - Imputed missing `country` values using geographical state mappings.
   - Standardized categorical gender variables (`men`/`women` → `Male`/`Female`).
   - Converted string dates to `datetime64` objects.
   - Dropped redundant/empty attributes (`pincode`, `interests`).
3. **Data Deduplication:** Grouped and aggregated multi-ticket support logs into single customer summaries (`complaint_count`) before joining.
4. **Feature Engineering:**
   - `churn_flag`: Binary indicator ($1$ = Canceled, $0$ = Active).
   - `tenure_days`: Active lifetime calculation based on start and cancellation/current dates.
   - `age`: Calculated from date of birth (`dob`).
   - `churn_risk`: Tiered risk segmentation (`Low` < 50, `Medium` 50–69, `High` ≥ 70).
5. **Exploratory Data Analysis & Statistical Modeling:** Pearson correlation matrices, time-series monthly attrition analysis, and multi-variable pivot tables.

---

## 📊 Key Findings & Analytical Breakdown

### 1. Contract Commitment Disparity
* **Monthly Contracts:** `55.6%` Churn Rate
* **Annual Contracts:** `8.3%` Churn Rate
* **Finding:** Monthly subscribers exhibit **6.7x higher churn** due to low switching barriers and frequent billing checkpoints.

### 2. Plan Tier Vulnerability
* **Basic Plan:** `60.00%` Churn
* **Standard Plan:** `22.22%` Churn
* **Premium Plan:** `14.29%` Churn
* **Finding:** Basic tier accounts represent the highest churn volume due to trial expirations and price sensitivity.

### 3. Customer Service Impact
* Strong **0.77 correlation** between support escalations and subscription cancellation.
* Customers with low CSAT scores ($\le 30$) accounted for the majority of churn events.

---

## 🚀 Business Action Plan
1. **Annual Upgrades:** Offer targeted 15–20% discounts for annual plan upgrades to lower recurring monthly friction.
2. **Priority Escalation SLA:** Deploy automated priority routing for escalated/low CSAT tickets to be resolved within 2 hours.
3. **Regional Market Audit:** Conduct CDN latency, localized pricing, and regional competitor promotional audits for high-churn geographies like Karnataka.

---

## 💻 Tech Stack
- **Languages & Libraries:** Python (Pandas, NumPy, Matplotlib, Seaborn)
- **Database:** SQLite3 / SQL
- **Environment:** Jupyter Notebook

---
**Author:** Ankit  
**Focus:** Data Analytics | Business Intelligence | Customer Intelligence
