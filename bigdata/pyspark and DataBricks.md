# Hadoop(BigData)(PySpark)
1. **[Spark Introduction](#Spark-Introduction)**<br>
2. **[Spark Architecture](#Spark-Architecture)**<br>
4. **[Spark Environment Setup (optional)](#Spark-Environment-Setup-(optional))**<br>
5. **[Spark RDD with Python](#Spark-RDD-with-Python)**<br>
6. **[Spark RDD with Scala](#Spark-RDD-with-Scala)**<br>
8. **[Spark DF](#Spark-DF)**<br>
9. **[Databricks](#Databricks)**<br>
10. 
11. 
12. 




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
# Databricks

1. Signup

    1. Create `Databricks Community` login
    2. open the link and follow the instructions https://www.databricks.com/try-databricks#account
    3. Provide required details
    4. Click on continue
    5. click on try community version
    6. verify the mail
    7. provide password as you like and please remember it.
    8. Thats it... we are done.

2. Login

    1. open the link https://community.cloud.databricks.com/login.html
    2. provide email and password > Click on `Sign in`
    ![image](https://user-images.githubusercontent.com/20516321/220527727-13334d29-b882-407a-b851-c1493b6e17c8.png)

3. Create Cluster
    1. click on `create` > Click on `cluster` > provide name `rritecdb`
        ![image](https://user-images.githubusercontent.com/20516321/220528295-0bf2384f-b575-4561-8e74-3d829eda0ddf.png)
4. upload files into databricks
    1. Click on `data` > under `upload file` > drag and drop file from rritec materials labdata/reatail_db/orders/part-00000

        ![image](https://user-images.githubusercontent.com/20516321/222360084-1a8ab005-c2d4-4721-8a04-207e6f917468.png)

    2.  Copy the path `/FileStore/tables/part_00000-2`, it is needed in next exercise

6. See the data of files in DBFS

    1. Click on **Create** > Click on **Notebook** > Name it as **Create Dataframes** > Click on **Create**
    2. type as for below
        ``` fs
        %fs head /FileStore/tables/part_00000-2
        ```
        ![image](https://user-images.githubusercontent.com/20516321/222361426-8b3fd531-c2ae-49a7-9b36-c97015c30f71.png)

        
    3. 
7. Create dataframe from csv file
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
8. Create dataframe from json file
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

9. Create dataframe from json file using format and load

    3. Create dataframe
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
10. DF Creation by enabling the header
    1. upload employee csv file       

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
    4. 
11. DF Creation by using pipe (|) delimited data
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
12. Create dataframe from multiline json file
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
13. observe all the options and find out how to export as html


