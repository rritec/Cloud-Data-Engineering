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
## Notebook Utility

1. Observe help documents
``` py
dbutils.notebook.help()
```
``` py
dbutils.notebook.help("exit")
```
``` py
dbutils.notebook.help("run")
```
2. Create a notebook as shown below

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/2b7a8b72-795e-437b-b53c-96bb0f62f62c)

3. Call this notebook from another notebook, it may throw error if you are working in community version.

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/92ffbe69-7288-4858-bdba-e79c24c5ff1c)

4. 
## widget Utility
1. Observe Help document
``` py 
dbutils.widgets.help()
```
2. Create **combobox** input widget
``` py
dbutils.widgets.combobox(name="cb",
                         defaultValue="DATABRICKS",
                         choices=["DATABRICKS","ADF","FABRIC","POWERBI","BIGDATA","PYTHON"],
                         label="combobox")
```
3. Create **dropdown** input widget
``` py
dbutils.widgets.dropdown(name="dd",
                         defaultValue="DATABRICKS",
                         choices=["DATABRICKS","ADF","FABRIC","POWERBI","BIGDATA","PYTHON"],
                         label="dropdown")
```
4. Create **multiselect** input widget
``` py
dbutils.widgets.multiselect(name="ms",
                         defaultValue="DATABRICKS",
                         choices=["DATABRICKS","ADF","FABRIC","POWERBI","BIGDATA","PYTHON"],
                         label="multiselect")
```
5. Create **text** input widget
``` py
dbutils.widgets.text(name="text",
                         defaultValue="DATABRICKS",                         
                         label="textbox")
```
6. Retrieves current value of an input widget
``` py
print(f"combobox input widget value is :{dbutils.widgets.get('cb')}")
print(f"dropdown input widget value is :{dbutils.widgets.get('dd')}")
print(f"multiselect input widget value is :{dbutils.widgets.get('ms')}")
print(f"text input widget value is :{dbutils.widgets.get('text')}")
```
7. if we give wrong input widget name what will be the output
   ``` py
   print(f"combobox input widget value is :{dbutils.widgets.get('wrong_widget')}")
   ```
9. if we give wrong input widget name what will be the output
``` py
   print(f"combobox input widget value is :{dbutils.widgets.getArgument('wrong_widget')}")
   ```
10. if we give wrong input widget name what will be the output
``` py
   print(f"combobox input widget value is :{dbutils.widgets.getArgument('wrong_widget','testvalue')}")
   ```
11. Remove an input widget from the notebook.
    ``` py
    dbutils.widgets.remove("cb")
    ```
13. Remove all widgets in the notebook
``` py
dbutils.widgets.removeAll()
```

## Questions
## Answers

