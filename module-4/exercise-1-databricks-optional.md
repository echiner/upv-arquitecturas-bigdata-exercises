# Exercise 1 (OPTIONAL): Cloud Data Applications with Databricks

> [!IMPORTANT]
> This is an **OPTIONAL** exercise. 
> Access to the managed **Databricks** environment, workspace, and compute clusters will be provided directly by the teacher.

## 🏆 Project Objective
Gain hands-on experience developing distributed, high-performance data processing pipelines and analytical workflows on **Databricks**. 

You are required to select **one** of the three defined application paths below to implement using a Databricks Notebook, utilizing Spark (PySpark or Scala SQL) and Delta Lake.

---

## 💡 Example Application Definitions (Choose One)

### Option A: Real-Time IoT Telemetry Stream & Delta Lake Ingestion
*   **Definition**: Build a Spark Structured Streaming notebook that reads simulated vehicle telemetry data (GPS coordinates, battery level, speed) from a cloud storage bucket. The pipeline must parse the JSON inputs, clean anomalies (e.g., speed spikes or out-of-bound coordinates), and stream the processed rows into a structured Delta Lake table partitioned by city.

### Option B: Collaborative Filtering Recommender with MLlib & MLflow
*   **Definition**: Build an end-to-end machine learning notebook that loads historical transactional records. Clean the data to construct user-item ratings, train a collaborative filtering recommendation model using Spark's ALS (Alternating Least Squares) algorithm, log model parameters and evaluation metrics using MLflow, and generate a top-10 product recommendation table for all active users.

### Option C: Automated Data Quality Constraints on Medallion Tables
*   **Definition**: Create a pipeline that implements a Medallion architecture (Bronze ➔ Silver ➔ Gold) on Databricks. Incorporate data quality expectations (using Delta Live Tables expectations or custom PySpark assertions) to automatically detect schema drift, isolate invalid transactions (e.g., negative prices or missing customer IDs) to a quarantine table, and output clean analytical views to the Gold layer.

---

## 📤 Project Deliverables

1.  **Deliverable 1: Exported Databricks Notebook**
    *   The completed notebook exported as a `.ipynb` or `.dbc` archive containing your code, inline documentation, and run outputs.
2.  **Deliverable 2: Execution Validation**
    *   A short PDF or Markdown report detailing the execution, demonstrating Spark job outputs (e.g., DAG visualization screenshots, streaming rate statistics, or MLflow runs dashboard).

## 📚 References & Further Reading
*   [Databricks Documentation](https://docs.databricks.com/) - Product documentation for Databricks workspace, clusters, and runtimes.
*   [Apache Spark PySpark Documentation](https://spark.apache.org/docs/latest/api/python/index.html) - Programming guide and reference for PySpark.
*   [Delta Lake Documentation](https://docs.delta.io/latest/index.html) - Documentation for the Delta open storage format.
*   [MLflow Documentation](https://mlflow.org/docs/latest/index.html) - Guide to tracking machine learning experiments and logging models.
*   [Delta Live Tables (DLT) Guide](https://docs.databricks.com/en/delta-live-tables/index.html) - Declaring declarative data processing pipelines on Databricks.

---
[⬅ Back to Module 4 README](./README.md)
