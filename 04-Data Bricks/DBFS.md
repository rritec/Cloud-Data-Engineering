# DBFS
## What is Databricks DBFS?

1. Databricks File System (DBFS) is a distributed file system that's built-in with every Databricks workspace.
2. It acts as the storage layer for Databricks, allowing you to store and access data from notebooks and jobs running on Spark clusters.
3. 
## Key capabilities of Databricks DBFS:

1. **Unified Interface:** DBFS provides a single access point for various cloud storage systems like Amazon S3, Azure Data Lake Storage (ADLS), and Google Cloud Storage (GCS).This eliminates the need to use different APIs for each storage solution.
2. **Optimized for Spark:** DBFS is specifically designed for Spark workloads, offering high-performance reads and writes for data processing tasks like ETL, machine learning, and data analytics.
3. **Simplified Management:** DBFS simplifies working with cloud object storage by using familiar file system semantics (directories and files). This makes it easier to manage your data compared to directly interacting with object storage.
4. **Scalability:** DBFS can automatically scale to handle increasing data volumes, avoiding storage bottlenecks as your data grows.
5. **Persistence:** DBFS provides a convenient way to persist files in the cloud storage instead of relying on temporary cluster storage.

## Pre-configured directories in DBFS root
1. Mainly below three folders are pre configured
      1. FileStore
      2. databricks-datasets
      3. databricks-results

2. observe dbutils help

```pyspark
dbutils.help()
```
## fs utilities
3. Observe dbutils filesystem help

```py
dbutils.fs.help()
```
4. Observe ls help
``` py
dbutils.fs.help("ls")
```
5. List root folder of DBFS

```py
dbutils.fs.ls("/")
```
5. Create a folder

``` py
dbutils.fs.mkdirs("/FileStore/rritec/")
``` 
6. Copy file from one DBFS location to another DBFS location

```py
dbutils.fs.cp("/FileStore/b2406/dept.csv","/FileStore/rritec/")
```

7. Copy file from one DBFS location to another DBFS location

```py
dbutils.fs.mv("/FileStore/b2406/emp.csv","/FileStore/rritec/")
```

8. 
## Data utilities
1. Observe help Document
``` py
dbutils.data.help()
```
``` py
dbutils.data.help('summarize')
```
2. Create simple dataframe
``` py
df = (spark
           .read
           .format("csv")
           .option("header", "true")
           .option("inferSchema", "true")           
           .load("/FileStore/rritec/emp.csv"))
```
3. Analyze df
``` py
dbutils.data.summarize(df)
```
4. 

## Questions
## Answers

