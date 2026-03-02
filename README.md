# My Coursework Repository - MedicAid Regression Project
# Medicaid Spending Prediction 

**Predicting total paid Medicaid claims using PySpark MLlib on large-scale CMS data**

**Student:** Vivian Agbasoga  
**Student ID: 16527823**   
**Module:** 7006SCN – Machine Learning and Big Data  
**Submission date:** March 2026  
**Coventry University – MSc Data Science**

## Project Overview

This repository contains the full coursework submission for predicting Medicaid spending using distributed machine learning.

**Main deliverables:**
- Single notebook: full pipeline (ingestion → preprocessing → training → evaluation → export)
- Tableau Public workbook: 4 dashboards (data quality, model performance, insights, scalability)
- Custom Databricks SQL dashboard: model training bottlenecks and performance summary
- Query History (screenshots)

## Repository Structure

project/

├── notebooks/

│   └── Medicaid_Spending_Regression_Full_Pipeline.ipynb     

├── tableau/

│   └── MedicAid Regression.twbx                              

├── Query_history

├── data/

│   └── dashboard4_scalability.csv 

│      └── samples/    
         All other data samples from the project

├── README.md                                              

└── environment.yml                                       

## How to run / reproduce..

### Prerequisites

- Databricks workspace (Serverless or classic cluster)

- Tableau Desktop/Public to open .twbx file

### Steps

1. Open notebooks/Medicaid_Spending_Regression_Full_Pipeline.ipynb in Databricks

2. Attach to a Serverless or cluster

3. Run all cells (the pipeline is self-contained)

4. Download the exported CSVs from /Volumes/workspace/default/avi-coursework/

5. Open tableau/medicaid_analysis.twbx in Tableau → refresh data sources if needed

### Key results (at a glance)

- Best model: Decision Tree – RMSE 0.4736, R² 0.9743 (small sample)
    
- GBT: RMSE 0.6206, R² 0.9559 (slowest at ~34 min)

- Linear Regression: RMSE 2.0123, R² 0.5363 (fast baseline)

- Sampling (5%) necessary due to local-mode memory limits

## Tableau Public Workbook

View the interactive dashboards here:  

**(https://public.tableau.com/views/MedicAidRegression/Dashboard1?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)**

## Databricks SQL Performance Board

Custom dashboard summarizing training times, RMSE/R² and bottlenecks:  

[[(https://dbc-b43580aa-7482.cloud.databricks.com/dashboardsv3/01f114b3f35510deaa51163b1065d7b0/published?o=7474644374456874)]]

## Important Note: Query History

Due to **Databricks Serverless compute restrictions**, classic Spark UI tabs and event log configuration (spark.eventLog.enabled) are not available (results in CONFIG_NOT_AVAILABLE error).  

Instead, the following were used for performance analysis and optimization evidence:
- **Query Profile** (DAG, stages, metrics, shuffle, spill, duration) – available after most notebook cell executions
- **Ganglia Metrics** (CPU/memory graphs during long runs)
- **Query History** list (shows multiple pipeline runs)

**Where to find screenshots:**
- Folder: query_history/ (inside the zipped project)
- Contains selected screenshots covering:
  - Data Ingestion and Validation (Parquet read, schema, approx count)
  - Small sample creation ans splitting (5% fraction, randomSplit 80/20)
  - Converting sample to Pandas (for sklearn baseline comparison)
  - Feature assembly with VectorAssembler and StandardScaler
  - Model training cells (Linear Regression shown; others similar)
  - Final comparison print and export to CSV for Tableau

**Note on missing "See performance" links:**
Not all cells display the "See performance" / Query Profile link after execution. The included screenshots cover the most important long-running and optimization-relevant cells.

The SQL dashbords provide detailed model training visualizations, performance metrics, and bottlenecks — together with the screenshots above, this fully covers the optimization and execution analysis.

- **Sampling**: Full dataset (227M rows) not trainable locally → 5% sample used for feasibility.

- **Feature engineering**: HCPCS one-hot encoding → ~10,882 dimensions (tree models handle this well).







