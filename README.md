## ETL, Data Analysis, and Predictive Modeling

### Introduction

BridgeBay seeks to implement an end-to-end data pipeline to enhance data-driven decision-making. This project integrates ETL (Extract, Transform, Load), data analysis, and predictive modeling to provide valuable insights into customer behavior, optimize business strategies, and forecast Customer Lifetime Value (CLV). The objective is to ensure scalability, real-time processing, and actionable intelligence for strategic growth.

### ETL (Extract, Transform, Load) Process
1. Data Sources & Collection
The data pipeline ingests data from multiple sources to ensure detailed insights:
- Sales Data: Includes transaction details such as order date, product ID, quantity, payment method, and sales channel.
- Customer Data: Contains demographic information, purchase history, and behavioral attributes.
- Web Event Data: Captures real-time user interactions on the e-commerce platform, such as page views, clicks, cart additions, and checkout events.
- Product and Region Data: Catalog details for all electronics products and geographical segmentation for regional analysis.

2. Data Pipeline Architecture
- Data Ingestion:

  i. Batch ingestion of Product, Customer and Regional data from structured sources (On-prem SQL Server and CSV file) into Azure Data Lake Storage (ADLS).

  ii. Real-time Sales and Event data ingestion via Azure Event Hub for live tracking of customer interactions and sales activities.

- Data Transformation:
Processing of batch-ingested data via Databricks (PySpark) for:

  i. Data cleaning (handling nulls, duplicates, and inconsistent formats).
  
  ii. Implementing Slowly Changing Dimension (SCD) Type 2 to track product and customer changes over time.

- Data Loading:

  i. Processed data stored in Azure SQL Database (with two marts for the Data Analysis and Machine Learning Team) for business intelligence, analytics and predictive modelling.
  
  ii. Aggregated metrics and real-time insights pushed to Power BI dashboards for visualization.

3. Data Quality & Governance
- Data Validation: Ensured referential integrity between sales, customers, and products.
- Missing Data Handling: Used imputation for categorical values.
- Performance Optimization: Applied partitioning and indexing in SQL for efficient querying.

![Architecture_diagram](https://github.com/user-attachments/assets/8307c764-a2de-47b6-9c31-70fb7c5afdea)

### Dimensional Modeling and Warehouse Design
__Schema Design & Data Organization__
BridgeBay’s data warehouse follows a Snowflake Schema, designed for normalized storage, reduced redundancy, and improved query performance.
Fact Tables - 
- Sales Transactions: storing all sales transactions, with foreign keys linking to multiple dimension tables.
- Web Events: Contains granular event types and traffic source details, improving segmentation with a foreign key linking to a dimension table
  
Normalized Dimension Tables (Snowflaked structure for efficiency):
- Customers
- Products
- Region → Further normalized into Country and Location tables for hierarchical analysis.

__Performance & Optimization Considerations__
- Normalization for Storage Efficiency: Reduces data duplication and improves consistency.
- Foreign Key Indexing: Ensures fast joins between fact and dimension tables.
- Incremental Data Loads: Optimized ETL to only update changed records, reducing processing time.

![ERD](https://github.com/user-attachments/assets/6ce8976a-183c-4729-8d23-053ba85426f9)


Overall ETL Architecture
- Raw Data Layer: Stores unprocessed data in Azure Data Lake Storage (ADLS).
- Transformed Data Layer: Cleaned and structured data stored in Azure SQL Database.
- Analytical Layer: Snowflake schema optimized for Power BI reporting and predictive modeling.

### Data Analysis
__Business Insights Derived__

The following analyses were conducted to extract meaningful business insights:
- Customer Segmentation: Grouped customers based on purchase patterns, frequency, and spending behavior.
- Sales Performance: Assessed revenue trends across different cities, timeframes (month and year), and products.
- Conversion Rate Optimization: Identified the purchase rate for the average activity on the website.

__Power BI Dashboards__

A single-page Sales Performance dashboard was developed to provide visual insight into revenue trends, best-selling products, and customer purchase pattern.

![image](https://github.com/user-attachments/assets/f3c58d11-6bd8-4915-88ac-0ef7c4c59dee)

### Predictive Modeling
__Objective & Problem Statement__

The goal was to develop a machine learning model to predict Customer Lifetime Value (CLV) and improve targeted marketing strategies.

__Data Preparation__

Feature Selection:
- Transaction frequency, average order value, and historical spending.
- Web interaction data to capture engagement levels.
- Customer demographics and location-based factors.

__Data Splitting:__

- Train-test split (80%-20%) to ensure model generalization.
- Stratified sampling to maintain class distributions.
  
__Model Development & Evaluation__

Algorithms Evaluated:
Linear Regression: Baseline model for interpretability.

Gradient Boosting (XGBoost): Best-performing model due to its ability to capture nonlinear relationships.

Random Forest: Used for benchmarking.

Performance Metrics:

Root Mean Square Error (RMSE):  Used to measure prediction accuracy.

R-Squared (R²): Evaluated how well the model explains variance in CLV.

### Recommendations & Future Improvements
_Enhancing Real-Time Analytics_
- Implement Azure Stream Analytics to enable instant insights from customer interactions.

_Model Refinements & Feature Engineering_
- Introduce new features such as customer service interactions, loyalty program data, and social media sentiment analysis.
- Regularly retrain models to adapt to changing business conditions.

_Scalability & Performance Optimization_
- Migrate high-volume data processing to Azure Synapse Analytics for faster query execution.
- Optimize data pipeline execution using incremental refresh and parallel processing.

_Business Integration & Automation_
- Automate marketing campaigns based on predictive insights to increase conversion rates.
- Seamlessly integrate CLV predictions into CRM systems for better customer relationship management.

Conclusively, this project successfully established a scalable ETL pipeline, advanced data analytics framework, and predictive modeling system for BridgeBay. The integration of real-time analytics and CLV prediction has provided a competitive advantage by enabling data-driven decision-making. Moving forward, the focus will be on expanding real-time analytics, refining predictive models, and integrating insights seamlessly into business processes to drive continued growth and profitability.

