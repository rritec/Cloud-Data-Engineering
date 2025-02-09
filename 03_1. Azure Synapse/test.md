# Introduction

Azure Synapse Analytics includes **serverless SQL pools**, which are tailored for querying data in a **data lake**. With a serverless SQL pool, you can use **SQL code** to query data in files of various common formats without needing to load the file data into database storage. 

This capability helps **data analysts and data engineers** analyze and process file data in the data lake using a familiar data processing language, without the need to create or maintain a relational database store.

## Learning Objectives
After completing this module, you'll be able to:

- Identify **capabilities and use cases** for serverless SQL pools in Azure Synapse Analytics.
- Query **CSV, JSON, and Parquet files** using a serverless SQL pool.
- Create **external database objects** in a serverless SQL pool.

# Understand Azure Synapse Serverless SQL Pool Capabilities and Use Cases


Azure Synapse Analytics is an **integrated analytics service** that brings together a wide range of commonly used technologies for **processing and analyzing data at scale**. One of the most prevalent technologies used in data solutions is **SQL** - an industry-standard language for querying and manipulating data.

## Serverless SQL Pools in Azure Synapse Analytics
Azure Synapse SQL is a **distributed query system** in Azure Synapse Analytics that offers two kinds of runtime environments:

- **Serverless SQL pool**: On-demand SQL query processing, primarily used to work with data in a data lake.
- **Dedicated SQL pool**: Enterprise-scale relational database instances used to host **data warehouses**, in which data is stored in relational tables.

### **Benefits of Serverless SQL Pool**
In this module, we'll focus on **serverless SQL pool**, which provides a **pay-per-query endpoint** to query the data in your **data lake**. The benefits of using serverless SQL pool include:

✅ **Familiar Transact-SQL Syntax**: Query data in place without the need to copy or load data into a specialized store.  
✅ **Integrated Connectivity**: Supports a wide range of business intelligence and ad-hoc querying tools, including popular drivers.  
✅ **Distributed Query Processing**: Built for large-scale data, leading to fast query performance.  
✅ **Built-in Query Execution Fault-Tolerance**: Ensures high reliability and success rates, even for long-running queries involving large data sets.  
✅ **No Infrastructure Setup**: No clusters to maintain. A built-in endpoint is provided within every Azure Synapse workspace, so you can start querying data immediately.  
✅ **Cost-Effective**: No charge for reserved resources; you're only charged for the data processed by queries you run.  

### **When to Use Serverless SQL Pools?**
Serverless SQL pool is **tailored for querying data** residing in the data lake. Besides eliminating the **management burden**, it removes the need to worry about **ingesting the data into the system**. You simply **point the query to the data in the lake and run it**.

**Synapse SQL serverless resource model** is ideal for **unplanned** or "bursty" workloads. It enables **cost transparency**, allowing you to monitor and attribute costs **based on each executed query**.

🔹 **Note:**  
Serverless SQL pool is an **analytics system** and is **not recommended for OLTP workloads** (such as databases used by applications to store transactional data). Workloads requiring **millisecond response times** or pinpointing a **single row in a dataset** are **not a good fit** for serverless SQL pools.

### **Common Use Cases for Serverless SQL Pools**

#### **1️⃣ Data Exploration**
- Browse the **data lake** to gain **initial insights**.
- Easily achievable with **Azure Synapse Studio**.
- Use **built-in serverless SQL pool** to generate **SQL scripts** to select **TOP 100 rows** from a file or folder.
- Apply **projections, filtering, grouping**, and other SQL operations just as if the data were in a regular SQL Server table.

#### **2️⃣ Data Transformation**
- Azure Synapse Analytics provides **data transformation** capabilities with **Synapse Spark**.
- Some **data engineers** may prefer **SQL-based transformations**.
- Serverless SQL pool enables **SQL-based data transformations**, either **interactively** or as part of an **automated data pipeline**.

#### **3️⃣ Logical Data Warehouse**
- After **exploring data** in the data lake, define **external objects** such as **tables and views** in a serverless SQL database.
- The data **remains in the data lake files**, but is **abstracted** by a relational schema.
- Client applications and **analytical tools** can query the data **as if it were in a relational database hosted in SQL Server**.



