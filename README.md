# IBRD-Loan-Management-Efficiency

# 💸 Enhancing Loan Management Efficiency for IBRD  
### A Modern Data Engineering Case Study with Snowflake, DBT & AWS

---

## 🌍 Project Overview

The International Bank for Reconstruction and Development (IBRD), part of the World Bank Group, provides loans to middle and low-income countries for development projects. Loan cancellations (withdrawn before disbursement) create major time and financial inefficiencies.  

This project focuses on building a cloud-native data platform to analyze historical and streaming loan data, detect patterns in cancelled loans, and enable a downstream predictive model to proactively reduce cancellations.

---

## 🧩 Problem Statement

- Understand why and where loan cancellations occur.  
- Build a robust data pipeline to serve analytics and ML workloads.  
- Enable real-time monitoring of new loans and status changes using streaming data.  

---

## 🛠 Tech Stack

- ❄ Snowflake (Snowpark, Snowpipe, Streams & Tasks)  
- 🧱 dbt Cloud/Core
- 🌟 AWS GLUE with Pyspark
- ☁ AWS S3 (external stages & storage options)  
- ⚡ Streaming / Real-time ingestion (Snowflake Streaming, optionally Spark Streaming)  
- 📊 BI / Dashboards (any tool – e.g., Power BI, Tableau, Streamlit, etc.)

---

## 📂 Datasets

- Batch / Historical Data  
  - IBRD Statement Of Loans – Historical Data  
  - https://finances.worldbank.org/Loans-and-Credits/IBRD-Statement-Of-Loans-Historical-Data/zucq-nrc3  

---

## 🎯 Key Business Objectives

- ⏱ Calculate loan processing time (e.g., days between agreement signing and repayments).  
- 🥇 Identify top three countries with highest loan amounts and detect sudden drops.  
- 🚩 Detect countries with at least one loan cancellation (with sufficient borrowing history).  
- 📆 Compute average repayment period for each country.  

---

## 🧱 Medallion Architecture & Approach

<img width="400" height="500" alt="image" src="https://github.com/user-attachments/assets/f068eec2-6c75-4f6b-a78f-b53a4b2185cd" />

### 🥉 Bronze / Raw Layer

- Ingest files from AWS S3 using:
  - External stages + file formats  
  - Snowpipe for auto-ingest  
- Store raw data as-is in schema like:  
  - team1_bronze, team2_bronze, etc.  
- No transformations; acts as the source of truth.

### 🥈 Silver / Cleaned Layer

- Use Snowflake SQL, **Snowpark and dbt to:
  - Clean and standardize data  
  - Handle nulls, parse dates, fix types  
  - Remove duplicates and bad records  
  - Apply basic business rules  
- Store cleaned tables in schemas like:  
  - team1_silver, team2_silver, etc.  

### 🥇 Gold / Curated Layer

- Build business-ready marts using dbt:
  - Fact and dimension tables (star schema)  
  - Aggregations for analytics & dashboards  
- Optimized for:
  - BI tools  
  - ML feature extraction  
  - Monitoring and reporting  

---

## 🔄 Orchestration & Streaming
<img width="400" height="500" alt="image" src="https://github.com/user-attachments/assets/8805c1c9-2d58-4a55-84cf-602094cd14e9" />

- Snowpipe  
  - Auto-ingestion when new files land in S3.  
- Streams & Tasks  
  - Streams track incremental changes.  
  - Tasks schedule transformations and downstream jobs.  
- dbt Cloud Jobs  
  - Run staging → intermediate → marts models.  
  - Apply tests (unique, not_null, relationships) for data quality.  
- Real-time / Near Real-time  
  - Optional Snowflake Streaming / Spark Streaming to process latest loan feed.  

---

## 👥 Team Execution Plan

- 👨‍💻 3 members per team.  
- 🎯 Clear ownership of:
  - Ingestion  
  - Transformation (dbt / Snowpark)  
  - Streaming & orchestration  
  - Visualization / reporting  
- 🤝 Integrate all components at the end for a final presentation to SMEs and mentors.

---

## 📐 Data Model (Star Schema)
 <img width="400" height="500" alt="image" src="https://github.com/user-attachments/assets/69e034e0-f4e3-459c-8014-82888fef0325" />


## 🚀 How to Get Started

1. Clone this repository.  
2. Configure Snowflake account, warehouses, and role-based access.  
3. Create schemas for bronze/silver/gold per team (e.g., team1_bronze).  
4. Set up AWS S3 buckets, external stages, and file formats.  
5. Configure Snowpipe for auto-ingestion of batch and streaming files.  
6. Run dbt models for staging, intermediate, and marts.  
7. Connect your BI tool or Streamlit app to gold layer tables for dashboards.  

---

## 📊 Streamlit / Dashboard Ideas

- 📈 Loan cancellation trends by country / region / year.  
- 🧮 Average processing time and repayment period per country.  
- 🧱 Drill-down by loan type, **status, and **project.  
- 🚨 Real-time view of new loans and potential cancellation risk signals.
  <img width="1591" height="421" alt="image" src="https://github.com/user-attachments/assets/6d09b4e4-0343-4e3e-98b2-8eba0cf58442" />
  <img width="1610" height="435" alt="image" src="https://github.com/user-attachments/assets/d10c9c5d-7c0e-427e-b262-521351717b12" />
  <img width="1613" height="447" alt="image" src="https://github.com/user-attachments/assets/b4413880-5341-40e5-a357-cf8df07670ca" />
  <img width="1591" height="649" alt="image" src="https://github.com/user-attachments/assets/67302caa-6449-4125-b921-d84427236c4a" />
