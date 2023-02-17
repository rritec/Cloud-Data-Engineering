# Hadoop(BigData)(PySpark)
1. **[Spark Introduction](#Spark-Introduction)**<br>
2. **[Spark Architecture](#Spark-Architecture)**<br>
4. **[Spark Environment Setup](#Spark-Environment-Setup)**<br>
5. **[Spark RDD](#Spark-RDD)**<br>
6. **[Spark DF](#Spark-DF)**<br>
7. **[Spark SQL](#Spark-SQL)**<br>
8. **[Spark Structured Streaming ](#Spark-Structured-Streaming)**<br>
9. 
10. 




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
# Spark Environment Setup
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
# Spark RDD
# Spark DF
# Spark SQL
# Spark Structured Streaming 
# Sqoop Introduction
