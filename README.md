---

# End-to-End Real-Time Data Engineering Project

This project is a comprehensive **real-time streaming data engineering solution** modeled after a **ride-booking system like Uber or Ola**. It demonstrates a modern Azure-based architecture to handle both **real-time events** and **historical bulk data** using the **Medallion Architecture**.

<p align="center">
  <img src="https://github.com/Dharmil290998/End-to-End-Realtime-Data/blob/main/Data Architecture.png" width="800"/>
</p>

## 📌 Project Overview

The objective of this project is to build an **end-to-end data pipeline** that processes real-time ride confirmation events and integrates them with historical records and mapping data to create a production-ready **Star Schema** for analytics.


## 🏗️ Architecture & Tech Stack

* **Real-time Ingestion:**
  A **FastAPI** web application simulates user ride bookings (Producer). Events are sent to **Azure Event Hubs** (Managed Kafka).

* **Batch Ingestion:**
  **Azure Data Factory (ADF)** ingests historical and mapping data from GitHub using **metadata-driven pipelines**.

* **Storage:**
  **Azure Data Lake Storage (ADLS Gen2)** for Bronze, Silver, and Gold layers.

* **Processing:**
  **Azure Databricks** using **PySpark** and **Spark Structured Streaming**.

* **Orchestration:**
  **Spark Declarative Pipelines (SDP)** (formerly Delta Live Tables) for automation, lineage, and schema management.


## 🔄 Data Pipeline (Medallion Architecture)

### 🥉 Bronze Layer (Raw)

* Stores raw data exactly as received
* Includes:

  * Real-time events from Event Hubs
  * JSON mapping & historical data


### 🥈 Silver Layer (One Big Table - OBT)

* Combines streaming + batch + mapping data
* Creates a **One Big Table (OBT)**
* Uses **Jinja2 templates** for:

  * Metadata-driven design
  * Reusable and scalable transformations


### 🥇 Gold Layer (Analytics)

* Transforms OBT into a **Star Schema**
* Includes:

  * 1 Fact Table
  * Multiple Dimension Tables (e.g., `dim_passenger`, `dim_driver`, `dim_location`)


## 🚀 Key Features & Learnings

* **Pub-Sub Architecture:**
  Implemented **Producer-Consumer model** using Event Hubs

* **Metadata-Driven Pipelines:**
  Used **Jinja SQL templating** to automate transformations and reduce hardcoding

* **Slowly Changing Dimensions (SCD Type 2):**
  Tracks historical changes using start/end timestamps

* **Advanced Spark Capabilities:**
  Leveraged **SDP (DLT)** for:

  * Incremental processing
  * Auto CDC
  * DAG-based orchestration

* **Watermarking:**
  Handles **late-arriving data** in streaming pipelines


## ⚙️ How It Works

1. A user books a ride via the **FastAPI** application
2. The event is published to **Azure Event Hubs**
3. **Databricks (SDP)** consumes the stream and combines it with historical data
4. Data is transformed into a **Star Schema**
5. Final data is stored in **ADLS Gen2** for analytics and reporting


## 📊 Outcome

* Built a **production-style real-time data pipeline**
* Enabled scalable and modular architecture
* Delivered analytics-ready datasets for BI tools

