
# End-to-End Data Engineering Pipeline – Ecommerce Sales on Google Cloud Platform

## Overview

This project implements a **production-grade, cloud-native data engineering pipeline** simulating the retail operations of Apple accessories across Pakistan. It captures the full lifecycle of data within a retail context—starting from **synthetic data generation** to **cloud storage, transformation, warehousing**, and **business intelligence dashboards**.

The solution is built entirely on **Google Cloud Platform (GCP)** and demonstrates real-world retail data flows involving sales, customer behavior, payments, logistics, inventory, and store performance analytics.

---

## Objective

To design and deploy a **modular, scalable, and automated** data pipeline for simulated ecommerce operations, enabling:

* Realistic generation of transactional retail data
* Structured ingestion into a cloud data lake
* Scalable transformations and schema enforcement in a data warehouse
* Interactive business intelligence dashboards for strategic decision-making

---

## Architecture Summary

The pipeline adheres to the **modern Lakehouse architecture** and aligns with the **Medallion architecture pattern**:

* **Bronze Layer (Raw)**: GCS staging zone with raw CSV/JSON files
* **Silver Layer (Cleansed)**: Structured and cleaned data in BigQuery
* **Gold Layer (Business)**: Aggregated data models for analysis and visualization

Technologies used across the pipeline are cloud-native, serverless, and optimized for high availability and performance.

---

## Technology Stack

| Component             | Tools & Services                            |
| --------------------- | ------------------------------------------- |
| Data Generation       | Python, Faker, UUID, Pandas                 |
| Data Storage          | Google Cloud Storage (GCS)                  |
| Data Warehousing      | Google BigQuery (partitioned, clustered)    |
| Visualization         | Looker Studio (formerly Google Data Studio) |
| Orchestration & Tools | Google Cloud SDK, Shell, CSV/JSON, SQL      |

---

## Core Components

### 1. Synthetic Data Engine

* Simulates real-time ecommerce transactions across 7 normalized entities: `Customers`, `Products`, `Inventory`, `Sales`, `Payments`, `Shipping`, and `Stores`.
* Automated batch ingestion triggered every 100 transactions.
* Built using Python, Pandas, and the Faker library to ensure realistic data simulation.

### 2. Data Lake – Google Cloud Storage

* Raw data serialized in CSV/JSON formats.
* Stored in a GCS bucket, partitioned by entity and timestamp.
* Designed for schema-on-read access and scalable parallel processing.

### 3. Data Warehouse – Google BigQuery

* Ingests and transforms raw data using ELT principles.
* Schema validation, referential integrity, deduplication, and casting performed during ingestion.
* Utilizes star schema design with partitioned and clustered tables for analytical performance.

### 4. Business Intelligence – Looker Studio

* Real-time dashboards connected to BigQuery views.
* Includes KPIs, promotional trends, regional sales analytics, inventory health, and customer demographics.
* Supports stakeholder-specific analytics: C-suite executives, operations, and customer insights.

---

## Database Design

### Dimension Tables

* `Products`, `Customers`, `Stores`, `Inventory`

### Fact Tables

* `Sales`, `Payments`, `Shipping`

### Key Relationships

* Foreign keys connect fact tables with dimensions via star schema.
* Referential integrity is enforced at the BigQuery level.

---

## SQL Sample (Join Across All Entities)

```sql
SELECT
    s.sale_id, s.sale_date, s.quantity, s.total_price,
    c.full_name AS customer_name, c.city, c.loyalty_tier,
    p.model_name AS product, p.base_price,
    st.store_name, st.region,
    pay.payment_method, sh.delivery_status
FROM Sales s
LEFT JOIN Customers c ON s.customer_id = c.customer_id
LEFT JOIN Products p ON s.product_id = p.product_id
LEFT JOIN Stores st ON s.store_id = st.store_id
LEFT JOIN Payments pay ON s.sale_id = pay.sale_id
LEFT JOIN Shipping sh ON s.sale_id = sh.sale_id;
```

---

## Dashboard Highlights (Looker Studio)

### Executive Summary

* Total Revenue, Sales Volume, Customer Growth
* Time Series Analysis
* Payment Method Distribution
* Regional Store Performance

### Sales Analytics

* Top-selling products
* Salesperson performance
* Store-wise revenue trends
* Discount analysis

### Customer Insights

* Age, gender, and loyalty tier distributions
* Purchase frequency
* Regional purchasing trends

### Inventory and Shipping

* Stock level tracking
* Shipment delays and carrier efficiency
* Damaged units and restock cycles

---

## Key Features

* End-to-end automation from data generation to reporting
* Real-time ingestion and transformation using serverless infrastructure
* Modular Python-based codebase for future extensibility
* Adheres to enterprise BI and data governance standards
* Cost-optimized design using GCP-native tools

---

## Project Outcomes

* Successfully delivered a fully automated data engineering pipeline on GCP
* Generated and linked 7 synthetic datasets with realistic business logic
* Achieved high-performance analytical querying with BigQuery
* Built and deployed professional-grade dashboards in Looker Studio
* Aligned project architecture with scalable enterprise data patterns

---

## Future Enhancements

* Integrate real-time streaming using Cloud Pub/Sub
* Deploy Airflow or Cloud Composer for orchestration
* Enable anomaly detection using BigQuery ML
* Export data to external systems (e.g., Salesforce, Power BI)

---

## Repository Structure (Suggested)

```
ecommerce-data-pipeline-gcp/
│
├── data_generator/
│   └── simulate_data.py
├── gcs_upload/
│   └── gcs_utils.py
├── sql/
│   ├── schema.sql
│   └── joins.sql
├── dashboards/
│   └── looker_studio_links.txt
├── docs/
│   ├── architecture_diagram.png
│   └── ERD.png
└── README.md
```

---

## Author

**Muhammad Faizan Mahmood**
Data Engineering Fellow – Atomcamp x Datapilot
[LinkedIn](https://linkedin.com/in/m-faizan-mahmood) | [Email](mailto:faizanworkmail1@gmail.com)

