# DS-2002 Final Project – Chinook Data Lakehouse

## About Chinook

The Chinook data model represents a digital media store. It includes tables for artists, albums, media tracks, invoices, and customers.

https://github.com/lerocha/chinook-database

---

## Project Overview

This project builds a **local data lakehouse** using the Chinook dataset with both batch and simulated streaming data.

The pipeline follows the **bronze → silver → gold** architecture demonstrated in class labs and uses **Apache Spark Structured Streaming** to process invoice data as a real-time source.

The goal is to analyze music sales trends over time, specifically focusing on **monthly track sales by genre**.

---

## Data Sources

### Local CSV Files
- CSV files for `track`, `album`, `artist`, `genre`, and related reference data

### MongoDB JSON file
- JSON file for `customer` data

### Relational Database (MySQL)
- Chinook operational database created using `chinook__mysql.sql`
- Fetched data from the `employee` table in MySQL
- A `dim_date` table populated using a provided SQL script (`populate_dim_date.sql`)

### Streaming Data (Local File Stream)
- Three JSON files simulating real-time invoice line events
- Processed using Spark Structured Streaming with file-based triggers

---

## Lakehouse Architecture

### Bronze Layer
- Raw ingestion of batch and streaming data
- Streaming invoice data stored as Parquet
- Minimal transformations applied

### Silver Layer
- Cleaned and conformed fact table (`fact_invoice_sales`)
- Invoice lines joined with customer, track, and date dimensions
- Surrogate keys applied for analytics-ready data

### Gold Layer
- Aggregated business reports
- Monthly track sales grouped by genre
- Streaming aggregation written in **complete** output mode

---

## Instructions

### 1. Clone this repo
```bash
git clone https://github.com/echiino/ds-2002-capstone.git
cd ds-2002-capstone
```

### 2. Execute **`chinook_mysql.sql`** and **`populate_dim_date.sql`** (found in the scripts folder) in MySQL to create the chinook database and dim_date table.

### 3. Before running the notebook, update the following connection parameters:

```python
# MySQL connection settings
host_name = "localhost"
port = "3306"
uid = "your_mysql_username"
pwd = "your_mysql_password"

# MongoDB connection settings
mongodb_args = {
    "user_name" : "your_mongodb_username",
    "password" : "your_mongodb_password",
    "cluster_name" : "your_cluster_name",
    "cluster_subnet" : "your_cluster_subnet",
    "cluster_location" : "atlas",  # or "local" if running MongoDB locally
    "db_name" : "chinook"
}
```

### 4. Run the **`chinook_data_lakehouse.ipynb`** notebook.
