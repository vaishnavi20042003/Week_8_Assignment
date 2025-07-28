# 🚖 NYC Taxi Data Analysis using PySpark

This project demonstrates how to load NYC Taxi trip data into **DataLake / Blob Storage / Databricks**, process it using **PySpark DataFrames**, and run various analytical queries to extract insights such as revenue, popular locations, and payment trends.

---

## 📁 Project Structure


NYC-Taxi-Data-Analysis/
│
├── data/ # Sample data (CSV or JSON)
├── notebooks/ # PySpark notebooks
├── output/ # Output Parquet files / results
├── scripts/ # PySpark ETL scripts
├── README.md # Project documentation




---

## 📥 Dataset Source

Sample data used in this project is from NYC's official trip record data:

- **Trip Record Data (Yellow Cabs - Jan 2020)**  
  🔗 [Download CSV](https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2020-01.csv)  
  📂 Official source: [NYC Taxi & Limousine Commission](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

---

## 🔧 Steps Performed

1. **Load Data**  
   - Load CSV data into **DBFS (Databricks File System)**.

2. **Data Preparation**  
   - Clean and transform the data using **PySpark DataFrame API**.
   - (Optional) Flatten JSON fields if working with nested structures.

3. **Save to External Table**  
   - Write the cleaned DataFrame as an external **Parquet table** for downstream querying.

---

## 📊 Analytical Queries Performed

All queries are executed using **PySpark SQL / DataFrame API** in Databricks notebooks.

### ✅ Query 1: Add a Revenue Column

Add a new column `Revenue` which is the sum of:

- `Fare_amount`
- `Extra`
- `MTA_tax`
- `Improvement_surcharge`
- `Tip_amount`
- `Tolls_amount`
- `Total_amount`

---

### ✅ Query 2: Passenger Count by Area

Group data by pickup area and count total number of passengers.

---

### ✅ Query 3: Realtime Vendor Earnings

Calculate real-time **average fare and total earnings** for each of the **two vendors** in the dataset.

---

### ✅ Query 4: Payment Mode Analysis

Get **moving count** (streaming or window-based) of payments made using each **payment type**.

---

### ✅ Query 5: Top Vendors on Specific Date

Get the **top two vendors** based on total revenue on a particular date.  
Include number of passengers and total trip distance.

---

### ✅ Query 6: Busiest Route

Identify the **most traveled route** (pickup to drop-off) with the **highest passenger count**.

---

### ✅ Query 7: Top Pickup Locations (Real-time)

Get **top pickup locations** with most passengers in the **last 5 or 10 seconds** (real-time streaming or simulated window).

---

## 💻 Technologies Used

- **Databricks / Azure Blob Storage / DataLake**
- **Apache Spark (PySpark)**
- **Parquet Format**
- **SQL / DataFrame API**
- **Streaming / Window Functions (Optional)**

---

## 🧠 Key Learnings

- Using PySpark for large-scale data transformation and aggregation.
- Implementing both batch and simulated real-time processing.
- Writing optimized queries using Spark SQL and DataFrame transformations.
- Working with external data storage and formats like Parquet.

---

## 📎 Related Commands & Tips

```python
# Load CSV into DataFrame
df = spark.read.csv("/mnt/blob/yellow_tripdata_2020-01.csv", header=True, inferSchema=True)

# Write to Parquet as external table
df.write.mode("overwrite").parquet("/mnt/output/yellow_tripdata_cleaned.parquet")
