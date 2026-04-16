# 🌦️ Weather Data Pipeline (Databricks)

End-to-end data pipeline for ingesting, transforming, and analyzing weather data using a **Medallion Architecture (Bronze → Silver → Gold)** on Databricks.

🇧🇷 [Leia em Português](README.pt-BR.md)

---

## 📌 Overview

This project consumes data from the OpenWeather API, processes it through multiple transformation layers, and exposes analytical insights via a Databricks Dashboard.

**Key goals:**

* Build a scalable and robust data pipeline
* Ensure data quality and consistency
* Enable analytical consumption through curated datasets

---

## 🏗️ Architecture

![Pipeline Architecture](./images/architecture.png)

### 🥉 Bronze Layer

* Raw data ingestion from API
* Incremental storage (`append`)
* Basic error handling (city fallback for failed requests)

---

### 🥈 Silver Layer

* Data cleaning and normalization
* Timestamp standardization (UTC and local time)
* Unit normalization (e.g., temperature, pressure, wind)
* Deduplication of records
* Upsert logic using **MERGE** for idempotency

---

### 🥇 Gold Layer

Curated analytical datasets:

#### 📊 Daily Aggregations

* Average, minimum, and maximum temperature
* Total precipitation
* Atmospheric metrics (pressure, humidity)

#### ⏱️ Hourly Aggregations

* Hourly trends per city
* Wind, cloud, and temperature metrics

#### 🌥️ Weather Summary

* Frequency of weather conditions
* Percentage distribution per city

---

## 🔄 Orchestration

The pipeline is orchestrated using **Databricks Jobs**:

* Scheduled execution every **1 hour**
* Task dependency flow:

  ```text
  Bronze → Silver → Gold
  ```
* Retry policy configured
* Timeout control applied

---

## 📊 Dashboard

The project includes a dashboard built in Databricks for data visualization.

### Example visualizations:

#### 📈 Average Temperature by City

![Average Temperature](./images/daily_temp.png)

#### 🌧️ Daily Rain Volume

![Rain Volume](./images/rain.png)

#### ⏱️ Hourly Trends

![Hourly Trends](./images/hourly.png)

#### ☁️ Weather Distribution

![Weather Summary](./images/summary.png)

---

## 🎥 Dashboard Demo

![Demo](./images/demo.gif)

---

## 📁 Project Structure

```
.
├── Notebooks/
│   ├── 01_bronze.ipynb
│   ├── 02_silver.ipynb
│   └── 03_gold.ipynb
├── Data/
│   └── cidades.csv
├── images/
│   ├── architecture.png
│   ├── daily_temp.png
│   ├── demo.gif
│   ├── hourly.png
│   ├── rain.png
│   └── summary.gif
└── README.md
```

---

## ⚙️ Tech Stack

* Databricks
* PySpark
* Pandas
* SQL
* Delta Lake
* OpenWeather API
* Git / GitHub

---

## 🧠 Key Design Decisions

* Use of **MERGE in Silver layer** to prevent duplicates and ensure idempotency
* Clear separation of concerns using Medallion Architecture
* Deduplication at ingestion level (`dropDuplicates`)
* Incremental ingestion in Bronze layer
* Strategic use of overwrite/append in Gold depending on use case

---

## 🚀 Future Improvements

* Table partitioning for performance optimization
* Z-Ordering for improved query performance
* Integration with external BI tools (e.g., Power BI, Looker)
* Monitoring and alerting setup in Databricks

---

## 📬 Contact

Feel free to reach out to discuss this project or exchange ideas:

* LinkedIn: www.linkedin.com/in/samkuzmo/
* Email: samkuzmo@outlook.com

---
