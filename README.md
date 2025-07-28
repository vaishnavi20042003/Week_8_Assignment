🚕 NYC Cab Trip Analysis using PySpark  
This project showcases how to ingest NYC Taxi trip datasets into Azure Data Lake / Blob Storage / Databricks, transform it with PySpark DataFrames, and execute a variety of analytical tasks to gather insights on fares, high-traffic zones, and payment statistics.

📁 Project Layout  
NYC-Cab-Trip-Analysis/  
│  
├── dataset/              # Raw data samples (CSV or JSON)  
├── notebooks/            # PySpark exploration notebooks  
├── results/              # Output files in Parquet / query results  
├── etl_jobs/             # PySpark ETL transformation scripts  
├── README.md             # Project summary and steps  

📥 Data Reference  
The data used in this demo originates from NYC TLC's official trip records:

Trip Data Sample (Yellow Cabs - February 2020)  
🔗 Download CSV  
📂 Official Source: NYC Taxi and Limousine Commission  

🔧 Workflow Summary  

📌 Load Trip Data  
- Ingest CSV records into DBFS (Databricks File System)  

📌 Data Cleanup & Shaping  
- Process data using PySpark DataFrame operations  
- Flatten any nested JSON if applicable  

📌 Persist Processed Data  
- Store transformed records as external Parquet tables for query usage  

📊 Key Queries Executed  
All queries below utilize either Spark SQL or DataFrame transformations within Databricks notebooks.

✅ Query 1: Compute Earnings Column  
Append a new column `Earnings` by summing:  
- fare_amount  
- extra  
- mta_tax  
- improvement_surcharge  
- tip_amount  
- tolls_amount  
- total_amount  

✅ Query 2: Total Passengers by Zone  
Aggregate total number of passengers grouped by pickup zone  

✅ Query 3: Vendor Revenue Stats (Live)  
Calculate live average fare and cumulative revenue by vendor ID  

✅ Query 4: Analyze Payment Preferences  
Use window function or streaming to count occurrences of each payment method over time  

✅ Query 5: Top Vendors for a Given Day  
Identify the top 2 vendors by total earnings on a specific date, including passenger count and total miles  

✅ Query 6: Highest Traffic Route  
Determine the route (pickup → dropoff pair) with the most passengers  

✅ Query 7: Live Popular Pickup Areas  
Track top pickup locations by passenger volume in the last few seconds using streaming window logic  

💻 Stack & Tools  
- Databricks / Azure Blob Storage / Data Lake  
- Apache Spark (via PySpark)  
- Parquet Storage Format  
- Spark SQL / DataFrame API  
- Streaming / Window-based processing (optional)  

🧠 Core Concepts Learned  
- Performing large-scale data cleanup and summarization with PySpark  
- Applying real-time and batch techniques using Spark APIs  
- Designing efficient Spark queries using DataFrame and SQL mix  
- Managing external storage using columnar formats like Parquet  

📎 Helpful Snippets  

# Read raw trip data from mounted blob storage  
df = spark.read.csv("/mnt/storage/yellow_tripdata_2020-02.csv", header=True, inferSchema=True)  

# Save cleaned data as Parquet for analytics  
df.write.mode("overwrite").parquet("/mnt/results/yellow_tripdata_cleaned.parquet")  

