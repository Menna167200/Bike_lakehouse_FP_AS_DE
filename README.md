# Bike Sales Lakehouse Data Engineering Project

## Overview

This project implements an end-to-end **Lakehouse Data Engineering pipeline** for a fictional bike sales company. The pipeline follows the **Medallion Architecture** (Bronze → Silver → Gold) to ingest raw data from CRM and ERP systems, clean and transform it using PySpark, and model it into an analytics-ready **Star Schema**.

The project was built using **Databricks**, **PySpark**, and **Delta Lake**, simulating a real-world modern data platform used by data engineers.

---

## Acknowledgment

This project was developed while following the Databricks Data Engineering bootcamp by **Baraa Khatib Salkini**.
His detailed explanations and hands-on approach were instrumental in helping me understand how to design and build a complete lakehouse pipeline using Databricks.

Special thanks to **Baraa Khatib Salkini** for creating such a valuable learning resource.

---

## Architecture

The pipeline follows the Medallion architecture commonly used in modern data lakehouses.

Raw data is ingested into the **Bronze Layer**, cleaned and standardized in the **Silver Layer**, and finally transformed into business-ready tables in the **Gold Layer**.

```
        Raw Source Files
              │
              ▼
        Bronze Layer
   (Raw ingestion tables)
              │
              ▼
        Silver Layer
   (Cleaning & transformations)
              │
              ▼
         Gold Layer
     (Star Schema Model)


```

---

## Technologies Used

* Databricks
* PySpark
* Python
* SQL
* Delta Lake
* GitHub

---

## Data Sources

The pipeline integrates data from two simulated enterprise systems:

**CRM System**

* Customer information
* Product information
* Sales transactions

**ERP System**

* Customer demographics
* Customer location data
* Product category data

---

## Data Pipeline

### Bronze Layer

The Bronze layer stores **raw ingested data** from source systems with minimal transformation.

Examples:

* `crm_cust_info`
* `crm_prd_info`
* `crm_sales_details`
* `erp_cust_az12`
* `erp_loc_a101`
* `erp_px_cat_g1v2`

Key characteristics:

* Raw format
* Schema inferred
* Stored as Delta tables

---

### Silver Layer

The Silver layer focuses on **data cleaning, standardization, and quality improvements**.

Typical transformations include:

* Removing duplicates
* Handling null values
* Standardizing categorical fields
* Trimming whitespace
* Casting data types
* Fixing invalid dates
* Creating derived columns
* Standardizing gender values
* Cleaning product identifiers

Example Silver tables:

* `silver_cust_info`
* `silver_prd_info`
* `silver_sales_details`
* `silver_cust_az12`
* `silver_loc_a101`
* `silver_px_cat_g1v2`

---

### Gold Layer

The Gold layer organizes data into a **Star Schema** optimized for analytics and reporting.

The final model contains:

#### `dim_customers`

Customer dimension created by combining CRM and ERP customer data.

Attributes include:

* Customer key
* Customer ID
* First name
* Last name
* Gender
* Marital status
* Country
* Birthdate
* Customer creation date

#### `dim_products`

Product dimension enriched with product category information.

Attributes include:

* Product surrogate key
* Product key
* Product name
* Product cost
* Product line
* Category
* Subcategory
* Maintenance flag
* Product start and end dates

#### `fact_sales`

Fact table containing transactional sales metrics.

Measures include:

* Sales amount
* Quantity
* Price

Foreign keys connect to:

* `dim_products`
* `dim_customers`

---

## Star Schema Model

```
           dim_products
                │
                │
dim_customers ── fact_sales
```

This schema allows efficient analytical queries such as:

* Total sales by product category
* Sales by customer demographics
* Sales trends over time
* Top performing products

---

## Key Data Engineering Concepts Demonstrated

This project demonstrates several important data engineering practices:

* Medallion architecture implementation
* Data cleaning and validation with PySpark
* Building dimensional models
* Creating surrogate keys
* Data enrichment from multiple systems
* Pipeline orchestration with Databricks notebooks
* Structuring a scalable lakehouse pipeline

---

## Author

This project was developed as a **Data Engineering portfolio project** to demonstrate practical skills in building modern lakehouse pipelines using PySpark and Databricks.
