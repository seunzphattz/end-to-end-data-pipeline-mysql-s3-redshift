# AWS MySQL to Redshift ETL Pipeline

Production-style end-to-end data pipeline demonstrating extraction from MySQL, storage in Amazon S3, transformation into analytics-ready datasets, and loading into Amazon Redshift.

## Tech Highlights

AWS Glue • Amazon S3 • Amazon Redshift • MySQL • Python • SQL • ETL • Data Lake • Data Warehouse

---

## Overview

This project implements a cloud-native ETL pipeline that moves data from a transactional MySQL source system into a structured analytics environment on Amazon Redshift.

The pipeline is designed using a layered architecture that separates ingestion, storage, transformation, and serving concerns.

It simulates a real-world batch data engineering workflow where operational data is extracted from a relational database, landed in a data lake, transformed into clean and curated datasets, and loaded into a warehouse for reporting and analytics.

---

## Architecture (High-Level)

```text
MySQL (Source System)
    ↓
Extraction Script / Glue Job
    ↓
Amazon S3 (Raw Layer)
    ↓
Transformation Job
    ↓
Amazon S3 (Clean / Curated Layer)
    ↓
Amazon Redshift (Staging Layer)
    ↓
Amazon Redshift (Serving Layer)
```

**Flow:** MySQL → S3 Raw → S3 Curated → Redshift Staging → Redshift Serving

---

## Problem Statement

Operational databases such as MySQL are designed for transaction processing, not for large-scale analytics.

To support reporting, dashboarding, and business intelligence, data must be:

- extracted safely from the source system
- stored durably in a scalable data lake
- cleaned and standardised
- modelled for analytics
- loaded into a warehouse optimised for query performance

This project demonstrates how to build that pipeline using AWS-native services and production-style design principles.

---

## What This Pipeline Does

- Extracts data from MySQL source tables
- Lands raw source data in Amazon S3
- Preserves source history in a raw layer
- Cleans and standardises data into curated datasets
- Loads transformed data into Amazon Redshift staging tables
- Builds analytics-ready serving tables in Redshift
- Separates operational data from analytical workloads

---

## Data Flow

1. Data is extracted from MySQL source tables
2. Extracted records are written to Amazon S3 raw storage
3. Transformation logic validates, cleans, and standardises the data
4. Curated datasets are written back to Amazon S3
5. Redshift loads curated data into staging tables
6. SQL transformations populate serving tables for analytics and reporting

---

## Project Structure

```text
config/
  config.yaml

scripts/
  extract_mysql_to_s3.py
  transform_s3_data.py
  load_s3_to_redshift.py

sql/
  create_staging_tables.sql
  create_serving_tables.sql
  transform_staging_to_serving.sql

data_samples/
  sample_output.csv

architecture/
  pipeline_diagram.png

docs/
  design_notes.md
```

---

## Architectural Layers

### 1. Source Layer
MySQL acts as the operational system where transactional data is generated and stored.

### 2. Raw Layer
Amazon S3 stores extracted data in its original form with minimal changes. This preserves source fidelity and supports replay or reprocessing.

### 3. Clean / Curated Layer
Transformation jobs standardise formats, handle null values, apply quality rules, and prepare data for downstream analytics.

### 4. Staging Layer
Redshift staging tables provide a controlled landing zone before final modelling and business transformation.

### 5. Serving Layer
Redshift serving tables expose analytics-ready data models for dashboards, reporting, and business intelligence.

---

## Key Engineering Concepts Demonstrated

- End-to-end ETL pipeline design
- Data lake to warehouse movement
- Layered architecture (raw, curated, staging, serving)
- Separation of operational and analytical systems
- Data modelling for analytics
- Batch processing design
- Cloud-native storage and warehouse loading
- Scalable pipeline structure for future orchestration

---

## Example Use Case

A business stores customer orders in MySQL as part of its operational application.

This pipeline extracts those orders, stores them in S3, prepares them for analysis, and loads them into Redshift where analysts can answer questions such as:

- What is total revenue by month?
- Which customers buy most frequently?
- Which products perform best by region?
- What are the trends in order volume over time?

---

## System Design Thinking

This pipeline was designed with the following considerations:

- Scalability: S3 and Redshift support large-scale analytical workloads
- Reliability: Raw data is preserved before transformation
- Maintainability: Each stage is separated by clear responsibility
- Query performance: Redshift serving tables support analytical workloads
- Reusability: Curated data can be reused by multiple downstream consumers
- Recoverability: Raw layer allows reprocessing when business rules change

---

## Production Considerations

- Incremental extraction using watermark columns or timestamps
- CDC support for changed records
- Partitioned S3 paths for efficient storage and retrieval
- Data quality validation before warehouse loading
- Error handling and retry logic
- Monitoring and alerting via CloudWatch
- Secrets management for database credentials
- IAM least-privilege permissions
- CI/CD for deployment and promotion
- Orchestration using Airflow or Step Functions

---

## Future Improvements

- Add orchestration with Apache Airflow
- Implement Glue-based ETL jobs
- Add automated data quality checks
- Add schema drift detection
- Add dimensional modelling examples
- Add dashboard integration
- Add infrastructure-as-code deployment

---

## Why This Project Matters

This project demonstrates practical understanding of how modern data engineering systems move data from operational databases into analytical platforms.

It shows:

- source-system awareness
- storage layer design
- transformation thinking
- warehouse loading patterns
- analytics modelling awareness
- production-style system architecture

---

## Cost

Development-scale cost depends on service usage, but the architecture is designed to be modular and cost-conscious for small test workloads.
