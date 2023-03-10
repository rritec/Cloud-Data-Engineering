# Hadoop(BigData)(PySpark)
1. **[Spark Introduction](#Spark-Introduction)**<br>
2. **[Spark Architecture](#Spark-Architecture)**<br>
4. **[Spark Environment Setup (optional)](#Spark-Environment-Setup-(optional))**<br>
5. **[Spark RDD with Python](#Spark-RDD-with-Python)**<br>
6. **[Spark RDD with Scala](#Spark-RDD-with-Scala)**<br>
8. **[Spark DF](#Spark-DF)**<br>
9. **[Databricks Introduction](#Databricks-Introduction)**<br>
10. **[Databricks Signup](#Databricks-Signup)**<br>
11. **[Databricks Login](#Databricks-Login)**<br>
12. **[Databricks Cluster](#Databricks-Cluster)**<br>
13. **[DBFS](#DBFS)**<br>
14. **[Dataframes](#Dataframes)**<br>
15. **[Dataframe Operations](#Dataframe-Operations)**<br>
        15.1. **[Word Count](#Word-Count)**<br>
        15.1. **[Explode Example 1](#Explode-Example-1)**<br>
        15.1. **[Explode Example 2](#Explode-Example-2)**<br>
        
16. **[Write Mode](#Write-Mode)**<br>
17. **[Read Modes](#Read-Modes)**<br>
18. **[custom schema by using Struct Type](#custom-schema-by-using-Struct-Type)**<br>
19. **[custom schema by using DDL String](#custom-schema-by-using-DDL-String)**<br>
20. **[Joining 2 dataframes](#Joining-2-dataframes)**<br>
21. **[dropping the columns](#dropping-the-columns)**<br>
22. **[Spark DF Functions](#Spark-DF-Functions)**<br>
23. 
24. 




# Spark Introduction

1. Single computer works perfectly well for watching movies or working with spreadsheet software
2. However, as many users likely experience at some point, there are some things that your computer is not powerful enough to perform
3. One particularly challenging area is data processing

![image](https://user-images.githubusercontent.com/20516321/219564287-0ad2c33d-796d-462b-ad1e-232728786c5b.png)

4. As of now only solution is

![image](https://user-images.githubusercontent.com/20516321/219564499-358f4b9d-b0ca-4d2d-ae9b-e8490d596da9.png)

5. PySpark is a Spark library written in Python to run Python applications using Apache Spark capabilities, using PySpark we can run applications parallelly on the distributed cluster (multiple nodes)
![image](https://user-images.githubusercontent.com/20516321/219563237-0fa081d5-9a9e-4549-be7d-ce0f381a11e0.png)

5. In the begining, Spark written in Scala and later on due to its industry adaptation it’s API PySpark released for Python using Py4J.
6. Py4J is a Java library that is integrated within PySpark and allows python to dynamically interface with JVM objects, hence to run PySpark you also need Java to be installed along with Python, and Apache Spark
7. Spark supports multiple widely used programming languages (Python, Java, Scala, and R)
9. Spark runs anywhere from a laptop to a cluster of thousands of servers.
10. Spark supports a rich set of higher-level tools including
    1. `Spark SQL` for SQL and structured data processing
    2. `MLlib` for machine learning
    3. `GraphX` for graph processing
    4. `Spark Streaming` for streaming data.

11. SparkContext

    1. SparkContext is the entry point of Spark functionality.
    2. The most important step of any Spark driver application is to generate SparkContext. 
    3. It allows your Spark Application to access Spark Cluster with the help of Cluster Manager.

12. Cluster Manager

    1. Standalone – a simple cluster manager included with Spark that makes it easy to set up a cluster.
    2. Apache Mesos – a general cluster manager that can also run Hadoop MapReduce and service applications.
    3. Hadoop YARN – the resource manager in Hadoop 2.
    4. Kubernetes – an open-source system for automating deployment, scaling, and management of containerized applications.

13. spark features

    1. In-memory computation
    2. Distributed processing using parallelize
    3. Can be used with many cluster managers (Spark, Yarn, Mesos e.t.c)
    4. Fault-tolerant
    5. Immutable
    6. Lazy evaluation
    7. Cache & persistence
    8. Inbuild-optimization when using DataFrames
    9. Supports ANSI SQL

12. Main Advantages of spark

    1. PySpark is a general-purpose, in-memory, distributed processing engine that allows you to process data efficiently in a distributed fashion.
    2. Applications running on PySpark are 100x faster than traditional systems.
    3. You will get great benefits using PySpark for data ingestion pipelines.
    4. Using PySpark we can process data from Hadoop HDFS, AWS S3, and many file systems.
    5. PySpark also is used to process real-time data using Streaming and Kafka.
    6. Using PySpark streaming you can also stream files from the file system and also stream from the socket.
    7. PySpark natively has machine learning and graph libraries.
13. 
14. 
# Spark Architecture

1. Apache Spark works in a master-slave architecture where the master is called “Driver” and slaves are called “Workers”. 
2. When you run a Spark application, Spark Driver creates a context that is an entry point to your application, and all operations (transformations and actions) are executed on worker nodes, and the resources are managed by Cluster Manager.
![image](https://user-images.githubusercontent.com/20516321/219567291-4bf422e9-c6fd-4453-8b0c-00f67940ad80.png)

3. Spark application execution life cycle
    1. `Driver:` Main program / Master in Spark
    2. In `driver` you initiate `spark context`
    3. `Spark context` acts as bridge between `cluster manager` & `driver` to negotiate the resource from cluster manager & the cluster manager allocates the resources to the spark job & then spark job can be submitted to the cluster & then the `executers` will be started on the respective `worker machines`
    4. `cluster manager` or `Resource manager` Mostly it will be `YARN` other options for cluster manager are `MESOS` & `Standalone`
    5. As part of that it will divide the whole spark job into “stages”.
    6. `stages` will be further divided into `tasks`
    7. Those `tasks` are executed on `workers`
    8. `cluster manager` takes a decision on which **tasks** should on which **workers**
    9. workers are physical machines & there can be multiple executors on same worker
    10. executors will register with the driver via `spark.driver.port`
    11. After the driver-executor registration, the driver will send those “tasks” & “application code(defined by JAR)” to the “executors”
    12. Every “executor” will have multiple cores(`--executor-cores`) which can be decided during the spark job submission time
    13. Each core will be called as `executor core`
    14. Example: if there 4 cores on a “worker” machine it can execute 4 tasks
    15. Once job is completed, results are sent back to the driver application or can be saved to disk.

![image](https://user-images.githubusercontent.com/20516321/219569398-ead39a2e-83df-4e59-bad8-9860fcd882f5.png)

    16. 

4. 
# Spark Environment Setup (optional)
1. Install Java
    1. To run PySpark application, you would need Java 8 or later version hence download the Java version from Oracle and install it on your system.
    2. download [here](https://www.oracle.com/java/technologies/downloads/#license-lightbox)
    3. Post installation, set JAVA_HOME and PATH variable
        ``` java        
            JAVA_HOME = C:\Program Files\Java\jdk1.8.0_201
            PATH = %JAVA_HOME%\bin
        ```
    4. 
2. Install Apache Spark
    1. Download Apache spark by accessing Spark Download page [here](https://spark.apache.org/downloads.html)
    2. After download, unzip it
    3. create spark folder in c deive
    4. copy all spark files into c:\spark
        ``` java         
            SPARK_HOME  = C:\spark
            HADOOP_HOME = C:\spark
            PATH=%SPARK_HOME%\bin
            PATH=%HADOOP_HOME%\bin
        ```
3. Install winutils
    1. Download winutils.exe file from winutils, and copy it to %SPARK_HOME%\bin folder. Winutils are different for each Hadoop version hence download the right version [here](https://github.com/steveloughran/winutils)
4. 
# Spark RDD with Python
1. Resilient Distributed Datasets (RDDs):
    1. Spark revolves around the concept of a resilient distributed dataset (RDD), which is a fault-tolerant collection of elements that can be operated parallel. 
    2. There are two ways to create RDDs: 
        1. parallelizing an existing collection in your driver program
        2. referencing a dataset in an external storage system, such as a shared filesystem, HDFS, HBase, or any data source offering a Hadoop InputFormat.2.dfd
2. Reference Spark [doc](https://spark.apache.org/docs/latest/rdd-programming-guide.html)
3. Method 1: Create RDD by parallelizing an existing collection in your driver program
    1. Open `terminal`
    2. type `pyspark`
    3. run below code
        ``` python
        data = [1, 2, 3, 4, 5]
        initRDD = sc.parallelize(data)
        ```
    4. Get first item from RDD
        ``` python       
        initRDD.first()
        ```
    5. Get required number of items
        ``` python
        initRDD.take(3)
        ```
    6. Get all items
        ``` python
        initRDD.collect()
        ```
    7. 
4. Method 2: Create RDD by referencing a dataset in an external storage system
    1. Run below code
        ``` python
        initRDD1=sc.textFile("/user/cloudera/rritec/emp.txt")
        ```
    2. Get first item from RDD
        ``` python       
        initRDD1.first()
        ```
    3. Get required number of items
        ``` python
        initRDD1.take(3)
        ```
    4. Get all items
        ``` python
        initRDD1.collect()
        ```
    5. Print readable format by using `for` loop
        ``` python
        for i in initRDD1.collect():
            print(i)
        ```
5. Map
    1. Return a new RDD by applying a function to each element of this RDD.
    2. run and understand below code.
        ``` python
        r =sc.parallelize(range(1,11)).map(lambda i:(i,i*2))
        r.collect()
        ```
    3. 
7. reduce
    1. Spark RDD `reduce()` aggregate action function is used to calculate `min`, `max`, and total of elements in a dataset
    2. RDD `reduce()` function takes function type as an argument and returns the RDD with the same type as input.
    3. It reduces the elements of the input RDD using the binary operator specified.
        ``` python
        r =sc.parallelize(range(1,4)).reduce(lambda a,b:a+b)
        r
        ```

    
8. filter
    1. Return a new RDD containing only the elements that satisfy a predicate
        ``` python
        r =sc.parallelize(range(1,11)).filter(lambda a:a % 2 ==0)
        r.collect()
        ```
9. 


# Spark RDD with Scala

1. we can do almost all activities of `spark with python` in `spark with scala`
2. open `terminal`
3. type `spark-shell`
    1. create RDD
    ``` scala
    val data = Array(1, 2, 3, 4, 5)
    val distData = sc.parallelize(data)
    ```
    2. Get first item from RDD
        ``` python       
        distData.first()
        ```
    3. Get required number of items
        ``` python
        distData.take(3)
        ```
    4. Get all items
        ``` python
        distData.collect()
        ```
4. 



# Spark DF
1. A DataFrame is a data structure that organizes data into a 2-dimensional table of rows and columns, much like a spreadsheet.
2. DataFrames are one of the most common data structures used in modern data analytics because they are a flexible and intuitive way of storing and working with data
3. Download or copy sample data from [spark github](https://github.com/apache/spark/tree/master/examples/src/main/resources)
4. Creating dataframe from json file

    ``` sql
    from pyspark.sql import SQLContext
    sqlContext = SQLContext(sc)
    df = sqlContext.read.json("/user/cloudera/rritec/people.json")    
    # Displays the content of the DataFrame to stdout
    df.show()
    ```
4. DataFrame Operations
    1. Show the content of the DataFrame
        ``` sql
        df.show()
        ```
    2. Print the schema in a tree format
        ``` sql
        df.printSchema()
        ```
    3. Select only the "name" column
        ``` sql
        df.select("name").show()
        ```
    4. Select everybody, but increment the age by 1
        ``` sql
        df.select(df['name'], df['age'] + 1).show()
        ```
    5. Select people older than 21
        ``` sql
        df.filter(df['age'] > 21).show()
        ```
    6. Count people by age
        ``` sql
        df.show()
        ```
    7. Show the content of the DataFrame
        ``` sql
        df.groupBy("age").count().show()
        ```
        
    8. 
5. 
# Databricks Introduction

1. The Databricks Lakehouse Platform provides a unified set of tools for building, deploying, sharing, and maintaining enterprise-grade data solutions at scale.
2. Databricks integrates with cloud storage and security in your cloud account, and manages and deploys cloud infrastructure on your behalf.
3. Databricks is used to process, store, clean, share, analyze, model, and monetize their datasets with solutions from BI to machine learning
4. common use cases for Databricks
    1. Build an enterprise data lakehouse. Refer [more](https://docs.databricks.com/lakehouse/index.html)
    2. ETL and data engineering
    3. Machine learning, AI, and data science
    4. Data warehousing, analytics, and BI
    5. Data governance and secure data sharing
    6. DevOps, CI/CD, and task orchestration
    7. Real-time and streaming analytics
5. Refer more introduction [here](https://docs.databricks.com/introduction/index.html)




# Databricks Signup

1. Create `Databricks Community` login
2. open the link and follow the instructions https://www.databricks.com/try-databricks#account
3. Provide required details
4. Click on continue
5. click on try community version
6. verify the mail
7. provide password as you like and please remember it.
8. Thats it... we are done.

# Databricks Login

1. open the link https://community.cloud.databricks.com/login.html
2. provide email and password > Click on `Sign in`
![image](https://user-images.githubusercontent.com/20516321/220527727-13334d29-b882-407a-b851-c1493b6e17c8.png)

# Databricks Cluster

    1. click on `create` > Click on `cluster` > provide name `rritecdb`
        ![image](https://user-images.githubusercontent.com/20516321/220528295-0bf2384f-b575-4561-8e74-3d829eda0ddf.png)

# DBFS

1. Upload files into databricks

    1. Click on `data` > under `upload file` > drag and drop file from rritec materials labdata/reatail_db/orders/part-00000

        ![image](https://user-images.githubusercontent.com/20516321/222360084-1a8ab005-c2d4-4721-8a04-207e6f917468.png)

    2.  Copy the path `/FileStore/tables/part_00000-2`, it is needed in next exercise

2. See the data of files in DBFS

    1. Click on **Create** > Click on **Notebook** > Name it as **Create Dataframes** > Click on **Create**
    2. type as for below
        ``` fs
        %fs head /FileStore/tables/part_00000-2
        ```
        ![image](https://user-images.githubusercontent.com/20516321/222361426-8b3fd531-c2ae-49a7-9b36-c97015c30f71.png)

        
    3. 
# Dataframes

1. Create dataframe from csv file
    1. Create dataframe
        ``` sql
        orders_df = (spark.read.csv("/FileStore/tables/part_00000-2")
             .toDF("order_id", "order_date", "order_customer_id", "order_status")
            )
        ```
    2. observe type
        ``` sql
        type(orders_df)
        ```
    3. See some data
        ``` sql
        orders_df.show()
        ```
    4. 
2. Create dataframe from json file
    1. upload order json file
        ![image](https://user-images.githubusercontent.com/20516321/222363656-9aee863c-a7d3-46d8-8837-eba913b6602e.png)

    2. Observe data
        ``` fs
        %fs head /FileStore/tables/part_r_00000_990f5773_9005_49ba_b670_631286032674-1
        ```
    3. Create dataframe
        ``` sql
        orders_json = spark.read.json("/FileStore/tables/part_r_00000_990f5773_9005_49ba_b670_631286032674-1")
        ```
    2. observe type
        ``` sql
        type(orders_json)
        ```
    3. See some data
        ``` sql
        orders_json.show()
        ```
    4. 

3. Create dataframe from json file using format and load

    1. Create dataframe
        ``` sql
        orders_df_json = (spark.read.format("json")
               .load("/FileStore/tables/part_r_00000_990f5773_9005_49ba_b670_631286032674-1")
              )
        ```
    2. observe type
        ``` sql
        type(orders_df_json)
        ```
    3. See some data
        ``` sql
        orders_df_json.show(3)
        ```
    4. 
4. DF Creation by enabling the header
    1. Refer spark help document [here](https://spark.apache.org/docs/latest/sql-data-sources-csv.html)upload employee csv file       

    2. Observe data
        ``` fs
        %fs head  /FileStore/tables/nov2022/emp_csv/employee.csv
        ```
    3. Create dataframe
        ``` sql
        emp_df = (spark
          .read
          .format("csv")
          .option("header", "true")
          .load("/FileStore/tables/nov2022/emp_csv/employee.csv")
          )
        ```
    2. observe type
        ``` sql
        type(emp_df)
        ```
    3. See some data
        ``` sql
        emp_df.show(3)
        ```
    4
5. DF Creation by using pipe (|) delimited data
    1. upload departments csv file       

    2. Observe data
        ``` fs
        %fs head /FileStore/tables/nov2022/dept_pipe/departments
        ```
    3. Create dataframe
        ``` sql
        dept_df = (spark
           .read
           .format("csv")
           .option("header", "true")
           .option("delimiter", "|")
           .load("/FileStore/tables/nov2022/dept_pipe/departments")
           )
        ```
    2. observe type
        ``` sql
        type(dept_df)
        ```
    3. See some data
        ``` sql
        dept_df.show(3)
        ```
    4. 
6. Create dataframe from multiline/nested json file
    1. upload students_nested_json_data file       

    2. Observe data
        ``` fs
        %fs head /FileStore/tables/nov2022/students_nested_json/students_nested_json_data.json
        ```
    3. Create dataframe
        ``` sql
        stu_df = (spark
          .read
          .format("json")
          .option("multiline", "true")
          .load("/FileStore/tables/nov2022/students_nested_json/students_nested_json_data.json")
           )
        ```
    2. observe type
        ``` sql
        type(stu_df)
        ```
    3. See some data
        ``` sql
        stu_df.show(3)
        ```
    4. 
7. observe all the options and find out how to export as html
# Dataframe Operations

## Word Count
1. upload the file `Cloud-Data-Engineering/labdata/sample.txt`
2. Copy DBFS path
3. observe contents of file
       ``` fs
       %fs head /FileStore/tables/sample.txt
       ```
4. Load file and observe data

``` pyspark
       df = (spark
      .read
      .format("text")
      .load("/FileStore/tables/sample.txt")
      .toDF("lines")
     ) 
```
     
```pysaprk
display(df)
```
5. Split into words

``` python
from pyspark.sql.functions import split
split_df = (
df.select(split("lines"," ").alias("words")))
```
```python
split_df.show()
```
``` python
split_df.printSchema()
```
6. get one word in each line

```python
from pyspark.sql.functions import explode
explode_df = split_df.select(explode("words").alias("word"))
```
``` python
display(explode_df)
```
``` python
explode_df.printSchema()
```
7. Aggregate data

``` python
agg_df = explode_df.groupBy("word").count()
display(agg_df)
```
8. Get top 5 records

``` python
from pyspark.sql.functions import desc
sorted_df = agg_df.orderBy(desc("count")).limit(5)
display(sorted_df)
```
9. 
## Explode Example 1
1. Observe Data

``` python
%fs head  /FileStore/tables/dec2022_data/input.json
```
2. Load into dataframe
``` python
input_df = (spark
            .read
            .format("json")
            .option("multiline", "true")
            .load("/FileStore/tables/dec2022_data/input.json"))
```
```python
display(input_df)
```
```python
input_df.printSchema()
```
```python
final_df = input_df.select("name", explode("values").alias("values"))
```
```python
display(final_df)
```

3. 
## Explode Example 2
1. observe data
``` python
%fs head  /FileStore/tables/dec2022_data/students_nested_json_data.json
```

2. Load Data
```python
stu_df = (spark
          .read
          .format("json")
          .option("multiline", "true")
          .load("/FileStore/tables/dec2022_data/students_nested_json_data.json"))
```
```python
display(stu_df)
```
3. print schema

``` python
stu_df.printSchema()
```
4. explode on array
```python
from pyspark.sql.functions import explode
explode_df = stu_df.select("name", explode("Education").alias("edu_exploded"))
```
```python
display(explode_df)
```
```python
explode_df.printSchema()
```
5. work with `*` 
```python
final_df = (explode_df.select("name", "edu_exploded.*"))
```
```python
display(final_df)
```
6. Observe Schema
```python
final_df.printSchema()
```
7. 

# Write Mode
1. Write modes would be used to write `Spark DataFrame` as `JSON, CSV, Parquet, Avro, ORC, Text files` and also used to write to `Hive table`, `JDBC tables like MySQL, SQL server`, e.t.c


| Scala/Java |	Any Language |	Meaning |
| ------- | ------ | ------- |
| SaveMode.ErrorIfExists (default) | "error" or "errorifexists" (default) | When saving a DataFrame to a data source, if data already exists, an exception is expected to be thrown. |
| SaveMode.Append	| "append"	| When saving a DataFrame to a data source, if data/table already exists, contents of the DataFrame are expected to be appended to existing data. |
| SaveMode.Overwrite	| "overwrite"	| Overwrite mode means that when saving a DataFrame to a data source, if data/table already exists, existing data is expected to be overwritten by the contents of the DataFrame. |
| SaveMode.Ignore	| "ignore"	| Ignore mode means that when saving a DataFrame to a data source, if data already exists, the save operation is expected not to save the contents of the DataFrame and not to change the existing data. This is similar to a CREATE TABLE IF NOT EXISTS in SQL. | 

2. Refer Modes [here](https://spark.apache.org/docs/latest/sql-data-sources-load-save-functions.html#save-modes)

1. create a simple dataframe
``` python

df = [("James", "M", 60000),
           ("Maria", "F", 70000),
           ("Mike", None, 50000),
           ("Jen", "", None)]

columns = ["emp_name", "emp_gender", "emp_sal"]
df = spark.createDataFrame(data = emp_data, schema = columns)
display(df)

```
2. Saving the content of dataframe into external storage.
``` pyspark
df.write.format("json").save("/FileStore/tables/rritec/output/df_data")
```
``` pyspark
%fs ls /FileStore/tables/rritec/output/df_data
```
2. Copy the json file dbfs path and observe contents
``` pyspark
%fs head dbfs:/FileStore/tables/rritec/output/df_data/part-00000-tid-766577745249667303-c54f173e-99aa-4f7b-b754-2a8a092de2a9-4-1-c000.json
```
3. What happenes if we write once again

``` pyspark
df.write.format("json").save("/FileStore/tables/rritec/output/df_data")
```
## Write Modes - error / errorifexists
1. Add `error` mode and observe it
``` pyspark
(df
 .write
 .format("json")
 .mode("error")
 .save("/FileStore/tables/rritec/output/df_data"))
 ```
2. Add `errorifexists` mode and observe it
``` pyspark
(df
 .write
 .format("json")
 .mode("errorifexists")
 .save("/FileStore/tables/rritec/output/df_data"))
 ```
## Write modes - ignore
1. Add `error` mode and observe it
``` pyspark
(df
 .write
 .format("json")
 .mode("ignore")
 .save("/FileStore/tables/rritec/output/df_data"))
 ```
 ## Write modes - append
1. Add `error` mode and observe it
``` pyspark
(df
 .write
 .format("json")
 .mode("append")
 .save("/FileStore/tables/rritec/output/df_data"))
 ```
 ``` pyspark
 %fs ls /FileStore/tables/rritec/output/df_data
 ```
 ``` pyspark
 %fs head dbfs:/FileStore/tables/rritec/output/df_data/part-00000-tid-7383138309953482542-3d9411b4-16ae-45e7-afbb-843a0c80f621-5-1-c000.json
 ```
  ``` pyspark
 %fs head dbfs:/FileStore/tables/rritec/output/df_data/part-00000-tid-766577745249667303-c54f173e-99aa-4f7b-b754-2a8a092de2a9-4-1-c000.json
 ```
 ## Write modes - overwrite
1. Add `error` mode and observe it
``` pyspark
(df
 .write
 .format("json")
 .mode("overwrite")
 .save("/FileStore/tables/rritec/output/df_data"))
 ```
``` pyspark
 %fs ls /FileStore/tables/rritec/output/df_data
 ```
## Adding header when writing the DF
1. Write into csv file
``` pyspark
(final_df
 .write
 .format("csv")
 .mode("overwrite")
 .option("header", "true")
 .save("/FileStore/tables/rritec/output/df_csv_data")
 )
```
``` pyspark
%fs ls /FileStore/tables/rritec/output/final_student_csv_data
```
```pysaprk
%fs head dbfs:/FileStore/tables/rritec/output/final_student_csv_data/part-00000-tid-4721931960538371143-1b0b3268-03e9-4725-9d83-269e16786577-8-1-c000.csv
```
# Read Modes
1. mode 
    1. (default `PERMISSIVE`): allows a mode for dealing with corrupt records during parsing.
    2. `PERMISSIVE` : sets other fields to null when it meets a corrupted record, and puts the malformed string into a new field configured by                columnNameOfCorruptRecord. When a schema is set by user, it sets null for extra fields.
    3. `DROPMALFORMED` : ignores the whole corrupted records.
    4. `FAILFAST` : throws an exception when it meets corrupted records.
2. upload and observe the data
``` pyspark
%fs head /FileStore/tables/rritec/output/ford.json
```
2. create dataframe
``` pyspark
ford_df = (spark
           .read
           .format("json")
           .load("/FileStore/tables/rritec/output/ford.json"))
display(ford_df)
```
3. Observe number of records
``` pyspark
ford_df.count()
```
## Read Modes - PERMISSIVE
1. default mode is `PERMISSIVE`
``` pyspark
ford_df = (spark
           .read
           .format("json")
           .option("mode","PERMISSIVE")
           .load("/FileStore/tables/rritec/output/ford.json"))
display(ford_df)
```
## Read Modes - DROPMALFORMED
``` pyspark
ford_df = (spark
           .read
           .format("json")
           .option("mode","DROPMALFORMED")
           .load("/FileStore/tables/rritec/output/ford.json"))
display(ford_df)
```
``` pyspark
ford_df.count()
```
## Read Modes - FAILFAST
1. run below command and observe the error message
``` pyspark
ford_df = (spark
           .read
           .format("json")
           .option("mode","FAILFAST")
           .load("/FileStore/tables/rritec/output/ford.json"))
```
## badRecordsPath
1. Create bad records in one separate file
``` pyspark
ford_df = (spark
           .read
           .format("json")
           .option("badRecordsPath", "/FileStore/tables/rritec/output/ford_corrupted_records")
           .load("/FileStore/tables/rritec/output/ford.json"))
display(ford_df)
```
2. observe bad records
``` pyspark
%fs ls /FileStore/tables/rritec/output/ford_corrupted_records
```
## inferSchema

1. observe data
``` pyspark 
%fs head /FileStore/tables/rritec/output/department.csv
```
``` pyspark
dept_df = (spark
           .read
           .format("csv")
           .option("header", "true")
           .option("inferSchema", "true")
           .load("/FileStore/tables/rritec/output/department.csv"))
```
``` pyspark
display(dept_df)
```
``` pyspark
dept_df.printSchema()
```
# Custom schema by using Struct Type
1. import required functions and creat schema
``` pyspark
from pyspark.sql.types import StructType, StructField, IntegerType, StringType, DateType
 
# StructType --> Row
# StructField --> Fields
 
dept_custom_schema = StructType([StructField("EmployeeID", IntegerType()),
                                StructField("DepartmentName", StringType()),
                                StructField("Client", StringType()),
                                StructField("OnboardedDate", DateType())])
```
                                
2. observe datatype
``` pysaprk
type(dept_custom_schema)
```
3. create dataframe
``` pyspark
dept_df = (spark
           .read
           .format("csv")
           .option("header", "true")
           .schema(dept_custom_schema)
           .load("/FileStore/tables/rritec/output/department.csv"))
```
4. display the contents
``` pysaprk
display(dept_df)
```
5. Observe the schema
``` pyspark
dept_df.printSchema()
```
# Custom Schema by using DDL String

1. observe the content
``` pysaprk
%fs head /FileStore/tables/rritec/output/orders_csv_latest/part_00000
```
2. Create DDL string
``` pyspark
orders_custom_schema = "order_id int, order_date date, order_customer_id int, order_status string"
```
3. create dataframe
``` pyspark
orders_df = (spark
             .read
             .format("csv")
             .schema(orders_custom_schema)
             .load("/FileStore/tables/rritec/output/orders_csv_latest/part_00000"))
display(orders_df)
```
4. observe schema
```pyspark
orders_df.printSchema()
```
# Joining 2 dataframes
1. already we have `dept_df`
``` pysaprk
display(dept_df)
```
2. create `emp_df`
``` pyspark
%fs head /FileStore/tables/rritec/output/emp_csv_latest/employee.csv
```
``` pyspark
emp_df = (spark
          .read
          .format("csv")
          .option("header", "true")
          .load("/FileStore/tables/rritec/output/emp_csv_latest/employee.csv"))
```
``` pyspark
display(emp_df)
```
``` pyspark
joined_df = dept_df.join(emp_df, emp_df.ID == dept_df.EmployeeID)
```
``` pyspark
display(joined_df)
```
3. 
# dropping the columns
1. drop `ID` column
``` pyspark
display(joined_df.drop("ID"))
```
2. observe data
``` pysaprk
display(joined_df)
```
3. create final_df
``` pysaprk
final_df = joined_df.drop("DepartmentName", "Client", "OnboardedDate")
```
``` pysaprk
display(final_df)
```
``` pysaprk
display(joined_df)
```

# Spark DF Functions

1. Create df
``` python

emp_data = [("James", "M", 60000),
           ("Maria", "F", 70000),
           ("Mike", None, 50000),
           ("Jen", "", None)]

columns = ["emp_name", "emp_gender", "emp_sal"]
emp_df = spark.createDataFrame(data = emp_data, schema = columns)
display(emp_df)

```
2. withColumn
``` python

emp_df1=emp_df.withColumn("tax",emp_df.emp_sal *0.01)
display(emp_df1)

```
3. case when
``` python

from pyspark.sql.functions import expr
new_df = emp_df1.withColumn("new_gender", expr("""CASE WHEN emp_gender = 'M' THEN 'Male'
                                                      WHEN emp_gender = 'F' THEN 'Female'
                                                      WHEN emp_gender IS NULL THEN ''
                                                      ELSE emp_gender
                                                  END"""))
display(new_df)

```
4. lit
``` python

from pyspark.sql.functions import lit
org_df = emp_df.withColumn("Organization", lit("Netflix"))
display(org_df)

```

``` python

from pyspark.sql.functions import lit
mgr_df = emp_df.withColumn("manager_id", lit(123))
display(mgr_df)

```

5. split
``` python

emp_data = [("james,a,smith", 123),
           ("steve,john,david", 456)]
columns = ["emp_full_name", "emp_id"]
emp_df = spark.createDataFrame(data = emp_data, schema = columns)
display(emp_df)

```
``` python
from pyspark.sql.functions import split
split_df = emp_df.withColumn("emp_first_name", split("emp_full_name", ",")[0])
display(split_df)

```
6. concat_ws
```python

stu_data = [("steve", ["java", "scala"]),
           ("david", ["c", "python"])]
columns = ["stu_name", "languages_known"]
stu_df = spark.createDataFrame(data = stu_data, schema = columns)
display(stu_df)

```

``` python

stu_df.printSchema()

```

``` python

from pyspark.sql.functions import concat_ws
new_df = stu_df.withColumn("languages", concat_ws("#", "languages_known"))
display(new_df)

```

``` python

new_df.printSchema()

```
7. explode
``` python

display(stu_df)

```
``` python

stu_df.printSchema()

```
``` python

from pyspark.sql.functions import explode
explode_df = stu_df.withColumn("languages", explode("languages_known"))
display(explode_df)

```

8. withColumnRenamed
``` python

display(stu_df)

```
``` python

new_df = stu_df.withColumnRenamed("languages_known", "common_languages")
display(new_df)

```

``` python

new_df.printSchema()

```

9. Explode on a Nested Json

``` python

stu_df = (spark
          .read
          .format("json")
          .option("multiline", "true")
          .load("/FileStore/tables/June2022/stu_nested_json/students_nested_json_data.json"))
display(stu_df)

```
``` python

stu_df.printSchema()

```
```python

from pyspark.sql.functions import explode
explode_df = stu_df.withColumn("edu_flattened", explode("Education"))
display(explode_df)

```
``` python

dropped_df = explode_df.drop("Education")
display(dropped_df)

```
``` python

dropped_df.printSchema()

```

``` python

final_flattened_df = dropped_df.select("name", "edu_flattened.*")
display(final_flattened_df)

```
``` python

final_flattened_df.printSchema()

```
10.  collect_list
``` python

emp_data = [("James", "Sales", 3000),
("Michael", "Sales", 4600),
("Robert", "Sales", 4100),
("Maria", "Finance", 3000),
("James", "Sales", 3000),
("Scott", "Finance", 3300),
("Jen", "Finance", 3900),
("Jeff", "Marketing", 3000),
("Kumar", "Marketing", 3000),
("James", "Sales", 2000),
("Saif", "Sales", 4100)]

columns = ["emp_name", "emp_dept", "emp_sal"]

emp_df = spark.createDataFrame(data = emp_data, schema = columns)

display(emp_df)

``` python

from pyspark.sql.functions import collect_list
display(emp_df.select(collect_list("emp_sal").alias("emp_sal_list")))

```
11. collect_set
 ``` python
 
 from pyspark.sql.functions import collect_set
display(emp_df.select(collect_set("emp_sal").alias("emp_sal_set")))

```
12. count

``` python

from pyspark.sql.functions import count
display(emp_df.select(count("emp_sal").alias("emp_sal_count")))

```
13. countDistinct
``` python

from pyspark.sql.functions import countDistinct
display(emp_df.select(countDistinct("emp_sal").alias("emp_sal_distinct_count")))

```
14. first & last
``` python

from pyspark.sql.functions import first
display(emp_df.select(first("emp_sal").alias("emp_sal_first")))

```

``` python

from pyspark.sql.functions import  last
display(emp_df.select(last("emp_sal").alias("emp_sal_last")))

```

15. max & min
``` python

from pyspark.sql.functions import  max
display(emp_df.select(max("emp_sal").alias("emp_sal_max")))

```
``` python

from pyspark.sql.functions import  min
display(emp_df.select(min("emp_sal").alias("emp_sal_min")))

```

16. sum
``` python

from pyspark.sql.functions import  sum
display(emp_df.select(sum("emp_sal").alias("emp_sal_sum")))

```
17. sumDistinct
``` python

from pyspark.sql.functions import  sumDistinct
display(emp_df.select(sumDistinct("emp_sal").alias("emp_sal_sumDistinct")))

```
18. row_number
``` python

from pyspark.sql.window import Window
from pyspark.sql.functions import desc
windowSpec = Window.partitionBy("emp_dept").orderBy(desc("emp_sal"))

```
``` python

from pyspark.sql.functions import row_number
new_df = emp_df.withColumn("row_number", row_number().over(windowSpec))
display(new_df)

```
``` python

final_df = new_df.filter("row_number == 1")
display(final_df)

```
``` python

display(new_df.filter("row_number <= 2"))

```
20. rank
``` python

from pyspark.sql.window import Window
from pyspark.sql.functions import desc
windowSpec = Window.partitionBy("emp_dept").orderBy(desc("emp_sal"))

```
``` python

from pyspark.sql.functions import rank
new_df = emp_df.withColumn("rank", rank().over(windowSpec))
display(new_df)

```

``` python

final_df = new_df.filter("rank == 1")
display(final_df)

```
``` python

display(new_df.filter("rank <= 2"))

```
21. dense_rank
``` python

from pyspark.sql.window import Window
from pyspark.sql.functions import desc
windowSpec = Window.partitionBy("emp_dept").orderBy(desc("emp_sal"))

```
``` python

from pyspark.sql.functions import dense_rank
new_df = emp_df.withColumn("dense_rank", dense_rank().over(windowSpec))
display(new_df)

```
``` python

final_df = new_df.filter("dense_rank == 1")
display(final_df)

```
``` python

display(new_df.filter("dense_rank <= 2"))

```
22. lag
``` python

from pyspark.sql.window import Window
from pyspark.sql.functions import desc
windowSpec = Window.partitionBy("emp_dept").orderBy(desc("emp_sal"))

```
``` python

from pyspark.sql.functions import lag
new_df = emp_df.withColumn("lag", lag("emp_sal", 1).over(windowSpec))
display(new_df)
```
23. lead
``` python

from pyspark.sql.window import Window
from pyspark.sql.functions import desc
windowSpec = Window.partitionBy("emp_dept").orderBy(desc("emp_sal"))

```
``` python
from pyspark.sql.functions import lead
new_df = emp_df.withColumn("lead", lead("emp_sal", 1).over(windowSpec))
display(new_df)

```
25. partitionBy
``` python

emp_df.write

```
``` python

(emp_df
 .write
 .option("header", "true")
 .partitionBy("emp_dept")
 .format("csv")
 .save("/Filestore/tables/emp_csv_output_dec_2022"))
 
 ```
 
 ``` python
 
 %fs ls /Filestore/tables/emp_csv_output_dec_2022
 
 ```
 
 ``` python
 
 %fs ls dbfs:/Filestore/tables/emp_csv_output_dec_2022/emp_dept=Finance/
 
 ```
 ``` python
 
 %fs head dbfs:/Filestore/tables/emp_csv_output_dec_2022/emp_dept=Finance/part-00002-tid-7195863566135644683-8dcd1890-647d-4722-a2b8-ef7f6f8c0fcb-184-1.c000.csv
 
 ```
 
 ``` python
 
 %fs ls dbfs:/Filestore/tables/emp_csv_output_dec_2022/emp_dept=Marketing/
 
 ```
 
 ``` python
 
 %fs head dbfs:/Filestore/tables/emp_csv_output_dec_2022/emp_dept=Marketing/part-00005-tid-7195863566135644683-8dcd1890-647d-4722-a2b8-ef7f6f8c0fcb-187-2.c000.csv
 
 ```
26. 
