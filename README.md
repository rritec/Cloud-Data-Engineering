
# Cloud Data Engineering Course Content

## For Training Contact 91 - 8374899166

------

This Repository has **Cloud Data Engineering** Training Materials developed by **Myla Ram Reddy**.

Please contact **Renuka** for **Training and Exam DP-203: Data Engineering on Microsoft Azure** @ [8374899166](https://wa.me/918374899166)(whatsapp)

------


# ADF(Azure Data Factory)

1. **Introduction**

- ETL Introduction.
- ELT Introduction
- Different ETL Tools
- Azure Data Factory Introduction
- Azure Data Factory - Important Concepts in ADF
- ADF Architecture
- Create Azure Free Account with credit card
- Create Azure Free Account with out credit card

2. **Storage Account**

- Introduction
- What is subscription
- What is resource group
- create resource group
- Create Storage Account
- Differences among LRS/GRS/ZRS/GZRS
- Difference between Hot and Cool Tiers
- Create Data Lake Gen 2
- Create Containers
- Create Folders
- Upload Files
- Override Files
- Download Files
- Edit Files
- Preview Files in different formats

3. **Azure SQL Database**

- Create SQL Database
- Create Sql Server
- Create Username and password
- Allow Azure resources and selected IPS access
- Create tables and insert data
- Query Tables
- Install SSMS
- Access Azure SQL Database using SSMS   

4. **Linked Service**

- Create Linked Service to BLOB
- Create Linked Service to Azure SQL Database
- Create Linked Service to MSFT SQL Server
- Create Linked Service to Batch Account
- .... etc
- Test Linked Service Connection

5. **Integration Run Times**

- What is Integration Run Time
- Types of IRs
- Azure integration runtime.
- Self-hosted integration runtime.
- Azure-SQL Server Integration Services (SSIS) integration runtime.
- Install Self-Hosted IR
- Configuration of Self-Hosted IR

6. **DataSets**

- Create Source Datasets
- Create Sink Datasets      - 
- Preview data
- Create Lookup datasets
- Understand and preview data


7. **BLOB to BLOB Pipeline**

- Create Pipeline
- Map source Dataset
- Map Sink Dataset
- Debug
- Trigger
- Understand output of run steps
- Understand Json log in each step

8. **Azure Storage Account Integration with ADF**

- Copy multiple files from blob to blob
- Filter activity - Dynamic Copy Activity
- Get File Names from Folder Dynamically
- Copy Activity Behavior in ADF
- Copy Activity Performance Tuning in ADF
- Get Count of files from folder in ADF
- Validate copied data between source and sink in ADF

9. **Azure SQL Database integration with ADF**

- Azure SQL Databases - Introduction - Relational databases in Azure
- Overwrite and Append Modes in Copy Activity in ADF

10. **Incremental Load**

- What is full load
- What is incremental load
- types of incremental loads
- Incrementally load data from Azure SQL Database to Azure Blob storage
- Incrementally load data from multiple tables in SQL Server to a database in Azure SQL Database
- Incrementally copy new and changed files based on LastModifiedDate
- Incrementally copy new files based on time partitioned file name

11. **Logic Apps**

- Send Succeeded mail of ADF pipeline with run stats
- Send Failed mail of ADF pipeline with error message
- Branching and chaining activities

12. **Azure Devops**

- Create organization
- create project
- create Git main branch
- configure Git to ADF
- create a branch in ADF
- publish ADF work in Git branch
- delete git branches
- understand commit in git
- understand and debug merge conflicts 


# Python Basic Level

1. Install Anaconda
1. understand markdown language
1. How to write Python code in normal notepad
2. How to write Python code in spyder
3. How to write Python code in Visual Studio Code
4. How to write Python code in in jupyter/ JupyterLab
5. Different Python Objects
1. int
2. float
3. complex
4. str
5. bool
6. range
6. Data Structures
1. list
2. Dict
3. Tuple
4. Set
5. Mutable Vs Immutable
7. Read items of str /list/Dict/Tuple/Set/range ..etc
1. index
2. slice
3. fancy
8. Operators
1. Comparision(>,<,>=,<=,...)
2. Logical/bool(and/or/not)
3. Numpy logical (logical_and/logical_or/logical_not)
9. Control Flows
1. input
2. if elif elif ... else
3. while loop
4. break
5. continue
6. for loop

# Advanced Python

1. System_Defined_Functions
1. create functions
1. function parameter
1. manadatory parameters
1. optional parameters
1. flexiable parameters
1. key value flexiable parameters
2. LEGB_scope_of_objects_of_functions
3. Methods
4. Modules
5. User_defined_packages
6. system_defined_packages
7. Iterables & Iterators
8. Lambda_Functions
9. Syntax Errors and Exceptions
10. List comprehensions
11. OOPs_Introduction_Classes_Objects_Attributes_Methods
12. OOPs_Inheritance_and_MRO
13. OOPs_Encapsulation
14. OOPs_Polymorphism



# BigData

1. **BigData Introduction**

- What is BigData
- BigData properties
- When to choose bigdata

2. **BigData VM Installation**

- Oracle Virtual box installation
- Cloudera VM installation
- winscp Installation
- Putty Installation

3. **Linux commands**

- Working with folders
- create folder
- remove folder with files
- remove folder without files
- understanding VI editor
- working with Files
- create a file
- copy file
- move file
- remove file
- cat command
- understanding permissions
- grep command
- find command
- ... etc

4. **HDFS**

- mkdir command
- put command
- get command
- CopyFromLocal command
- CopyToLocal command
- rm Command
- merge command
- ... etc

5. **Hive**

- Hive Metastore
- Hive Managed Tables
- Hive External Tables
- Hive Operations
- Hadoop File Formats and its Types
- Different ways to connecting hive
- Partitioning
- Bucketing

4. **Sqoop**

- Sqoop Introduction
- sqoop list-tables
- Sqoop Eval
- Sqoop Import
- Sqoop Export
- Import All Tables
- Import table from mysql to hive

5. **Pyspark**

- Spark Introduction
- Spark Architecture
- Spark Environment Setup (optional)
- Spark RDD with Python
- Spark RDD with Scala
- Spark DF
- Spark SQL
- Spark Structured Streaming

# DataBricks

1. DBFS(DataBricks File System)

- What is DBFS
- Navigate around DBFS
- Understanding path of DBFS

2. Compute (creating clusters)
- what is cluster
- create cluster
- map cluster to notebook

3. Workspace (Creating notebooks and working with notebooks)
- Understand workspace
- create folders
- organize content in the workspace

4. Spark Introduction
5. Spark Architecture
6. Creating RDDs (Reslient Distributed Dataset)
- what is RDD
- create RDD
- Query RDD 
7. Creating DataFrame
- what is DF
- create DF
- add columns to DF
- drop columns from DF
- query required data from DF
- .. etc
8. Reading and writing the Data From semi-structrured formats
9. Reading JSON Files SingleLine/ MultiLine / Complex
10. Reading XML Files
11. Reading CSV / TSV Files
12. Reading and writing the Data From structrured formats
13. Reading data from MySql / SQL SERVER / Oracle etc..
14. Reading and writing the Data From BIG DATA formats
- Parquet
- ORC
- AVRO
- ... etc
15. Reading and writing the Data From AWS S3
9. Reading and writing the Data From Azure Blob
10. PySpark Joins
11. PySpark Union / UnionAll   
4. Scopes
5. Delta Lake
1. ACID Transactions
2. Delta Live Tables
3. COPY INTO
4. Auto Loader
5. Convert Parquet or Iceberg data to Delta Lake

6. Scheduling the jobs





## SandBox

https://docs.microsoft.com/en-us/learn/modules/create-azure-storage-account/5-exercise-create-a-storage-account?ns-enrollment-type=learningpath&ns-enrollment-id=learn.store-data-in-azure
