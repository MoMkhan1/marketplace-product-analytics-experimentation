# 📊 Marketplace Product Analytics & Experimentation Framework

## Overview

This repository implements an end-to-end Product Data Science framework for a simulated two-sided marketplace platform.  
It replicates how modern marketplaces (e.g., Whatnot, Airbnb, Stripe) evaluate:

- Product feature launches  
- User conversion and retention  
- Revenue lift  
- Long-term customer value (LTV)  

The system integrates:

- SQL-based warehouse analytics  
- Controlled A/B experimentation with causal inference  
- Cohort retention modeling  
- Marketplace LTV estimation with stochastic projection  
- Automated executive dashboard generation  

All outputs, plots, tables, and reports are automatically generated and saved in `/outputs/` for reproducibility.

---

## 🎯 Business Scenario

We simulate a marketplace feature release designed to:

- Increase buyer conversion rate (CR)  
- Improve retention (R_t)  
- Increase average order value (AOV)  
- Drive long-term revenue growth  

We generate user-level (`u_i`) and transaction-level (`t_j`) data and evaluate treatment effects using:

Delta_CR = CR_treatment - CR_control
p-value = t-test(CR_treatment, CR_control)


---

## 🧠 Key Product KPIs

Conversion Rate (CR):

CR = Number of Buyers / Number of Visitors


Average Order Value (AOV):

AOV = Revenue / Number of Orders


Total Revenue (TR):

TR = Sum of all transaction amounts
TR = sum(t_j.amount for j in all orders)


Retention Rate (R_t):
R_t = Users active at month t / Users in cohort


Estimated Customer Lifetime Value (LTV):

LTV = AOV * f * H
Where:
f = purchase frequency per period
H = time horizon (months/years)


---

## 🏗 Project Structure

marketplace-product-analytics-experimentation/
│
├── data/ # Input CSVs
│ ├── users.csv
│ └── transactions.csv
│
├── sql/ # SQLite warehouse simulation
│ └── warehouse.db
│
├── outputs/ # Generated artifacts
│ ├── plots/ # Cohort heatmaps, KPI plots
│ ├── dashboards/ # Executive dashboards
│ ├── tables/ # KPI summaries & LTV estimates
│ └── reports/ # Experiment results
│
├── marketplace_full_pipeline.ipynb # Full Jupyter pipeline
├── requirements.txt
└── README.md


---

## 🔥 Core Components

### 1️⃣ SQL Warehouse Simulation

- SQLite-based analytical warehouse  
- Tables: `users`, `transactions`  
- KPI aggregation via SQL:

ELECT cohort, COUNT(user_id) AS buyers, SUM(amount) AS revenue
FROM transactions
GROUP BY cohort;


- Demonstrates advanced joins, aggregation, and filtering, similar to Snowflake/BigQuery pipelines.

---

### 2️⃣ A/B Experimentation Framework

- Treatment vs Control simulation at user-level (`u_i`)  
- Two-sample t-tests for KPI differences:

t = (mean1 - mean2) / sqrt((s1^2 / n1) + (s2^2 / n2))t = (mean1 - mean2) / sqrt((s1^2 / n1) + (s2^2 / n2))


- Conversion lift estimation:
Lift (%) = (CR_treatment - CR_control) / CR_control * 100


- Outputs: `ab_test_results.txt` and KPI comparison tables  
- Automates statistical validation for feature launch decisions.

---

### 3️⃣ Retention Cohort Analysis

- Assign users to monthly cohorts (`C_m`) based on first activity  
- Compute cohort retention matrix (`R_i,j`):
R_i,j = Number of users from cohort i active in month j / Number of users in cohort i


- Visualize as heatmaps for longitudinal engagement tracking  
- Outputs: `retention_cohort.csv`, `retention_cohort_heatmap.png`

---

### 4️⃣ Marketplace LTV Modeling

- Estimate group-level LTV:
LTV_g = sum(AOV_i * f_i * H for i in group g) / size of g


- Stochastic simulations for variability in purchase frequency and AOV:
f_i ~ Poisson(lambda_i)
AOV_i ~ Normal(mu_i, sigma_i)


- Output: `ltv_estimates.csv`  
- Provides actionable long-term revenue projections.

---

### 5️⃣ Executive Dashboard Generation

- Automatically generates a Power BI-style dashboard:  
  - Conversion comparison  
  - AOV comparison  
  - Revenue visualization  
  - LTV trends  

- Saved as: `outputs/dashboards/product_dashboard.png`  
- Demonstrates data storytelling and decision-ready reporting.

---

## ⚙️ Reproducibility

To run the full pipeline:

```bash
pip install -r requirements.txt

Then:

Open marketplace_full_pipeline.ipynb

Run all cells

All outputs, plots, tables, and reports are automatically saved in /outputs/.
No manual steps required.

💼 Skills Demonstrated

Product & Growth Analytics

Statistical Experimentation & Causal Inference

SQL Data Modeling & Warehouse Simulation

Retention & Cohort Modeling

LTV & Revenue Forecasting (Stochastic Modeling)

Python (Pandas, NumPy, SciPy, Matplotlib, Seaborn)

Reproducible Analytics Engineering

Executive Reporting & Data Storytelling

🚀 Future Enhancements

CUPED variance reduction

Bayesian A/B testing

Survival analysis for retention

Causal uplift modeling

Automated PDF executive reporting

dbt-style transformation layer

👤 Author

Mohammed Moniruzzaman Khan
PhD Candidate in Mathematics
Specialization: Stochastic Systems, Quantitative Modeling & Product Analytics




