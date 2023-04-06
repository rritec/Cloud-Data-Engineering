# DP-203 Azure Data Engineer(ADF)
1. **[Introduction](#Introduction)**<br>
2. **[Azure Free Account](#Azure-Free-Account)**<br>
3. **[Storage Account](#Storage-Account)**<br>
4. **[Azure Sql Database](#Azure-Sql-Database)**<br>
5. **[Azure Data Factory](#Azure-Data-Factory)**<br>
6. **[Integration runtimes](#Integration-runtimes)**<br>
7. **[Linked Service to blob](#Linked-Service-to-blob)**<br>
8. **[Linked Service to Azure Sql Database](#Linked-Service-to-Azure-Sql-Database)**<br>
9. **[Data Sets](#Data-Sets)**<br>
10. **[Create Pipenine from Blob to Azure Sql Database](#Create-Pipenine-from-Blob-to-Azure-Sql-Database)**<br>
11. **[Additional Columns](#Additional-Columns)**<br>
12. **[Create Pipenine from Blob to Blob](#Create-Pipenine-from-Blob-to-Blob)**<br>
13. **[Install SQL Server](#Install-SQL-Server)**<br>
15. **[Self Hosted IR](#Self-Hosted-IR)**<br>
16. **[Create Pipenine from Blob to MS Sql Server](#Create-Pipenine-from-Blob-to-MS-Sql-Server)**<br>
17. **[Create Pipenine from Azure SQL DB to MS Sql Server DB](#Create-Pipenine-from-Azure-SQL-DB-to-MS-Sql-Server-DB)**<br>
18. **[Load multiple sheets from excel to Azure SQL DB](#Load-multiple-sheets-from-excel-to-Azure-SQL-DB)**<br>
19. **[Get Excel Number of Sheets Dynamically and load it](#Get-Excel-Number-of-Sheets-Dynamically-and-load-it)**<br>
20. **[Incrementally load data](#Incrementally-load-data)**<br>
21. **[Incremental copy multiple tables](#Incremental-copy-multiple-tables)**<br>
22. **[Incremental copy lastmodified copy data tool](#Incremental-copy-lastmodified-copy-data-tool)**<br>
23. **[Incremental copy partitioned file name copy data tool](#Incremental-copy-partitioned-file-name-copy-data-tool)**<br>
24. **[Triggers](#Triggers)**<br>
25. **[Logic Apps](#Logic-Apps)**<br>
26. **[DataFlows](#DataFlows)**<br>
27. **[Split Transformation](#Split-Transformation)**<br>
28. **[Derived Column](#Derived-Column)**<br>
29. **[Azure DevOps](#Azure-DevOps)**<br>
30. **[cost](#cost)**<br>
  


# Introduction
## What is ETL
  - **Extract**: Get Required data(required Tables/Columns/rows) from hetrogenious/homogenious source.
      - Amazon.in > Example of Storage MySQL(OLTP)
      - amazon.co.uk > Example of Storage MS SQL Server(OLTP)
      - amazon.com > Example of Storage PostgresQL(OLTP)
- **Transform**: Convert one form of data into another form (Data Wrangling)
      - Convert one currency(example INR) into another currency(USD)
      - Convert India distance KM terminolgy into USA miles terminology
      - Converting Unix timestamp into windows timestamp
      - Converting all data in a consistency format (1 or M > Male, 0 or F > Female)   
 - **Load**: Final Data which is useful for Analysis/Analytics, will be loadded into warehouse / Datalakes /ADLS /Synposis
## What is ELT ?
- It is same as ETL but the order of work is different
## Different Tools ETL/ELT ?
  - Informatica (ETL/ELT)
  - ODI (ELT)
  - ADF (ETL/ELT)
  - .... etc
## Different BI Tools ?
  - Power BI
  - Tableau
  - ...etc
# Azure Free Account
## Azure Free Account with Credit Card
  - Click on the URL [Azure Free Account]( https://azure.microsoft.com/en-in/free/) > Click on **Start Free** > Provide your emailid > Follow the wizard
## Azure Free Account with Student Mailid
  - Click on the URL [Azure Student Free Account]( https://azure.microsoft.com/en-in/free/students/) > Click on **Start Free** > Provide your emailid > Follow the wizard
## Azure Free sandbox
  - Click on the URL [Azure Free Sandbox](https://docs.microsoft.com/en-us/learn/modules/create-azure-storage-account/5-exercise-create-a-storage-account?ns-enrollment-type=learningpath&ns-enrollment-id=learn.store-data-in-azure) > In the same page click on **Azure Portal**
  - Note: Few Services only available in the sandbox
# Storage Account
  - Azure Storage is a Microsoft-managed service providing cloud storage that is 
      - highly available
      - secure
      - durable
      - scalable
      - redundant. 
  - Azure Storage includes Azure Blobs (objects), Azure Data Lake Storage Gen2, Azure Files, Azure Queues, and Azure Tables
## Lab
  - Open [Azure Portal](https://portal.azure.com/)> > Click on the search bar > Type **Storage accounts** > Click on **Storage Accounts**
  - Click on **Create** > Under **Basics** tab provide below details
      - Subscription: **rritecsubscription**
      - Resource Group: **rritecresoucegroup**
      - Storage Account Name: **rritecsa**
      - Region: **(US) East US**
      - Performance: **Standard**
      - Redundancy: **Locally-Redundant Storage (LRS)**
  - Click on **Advanced** Tab > select **Enable hierarchical namespace**
  - Click on **Review**
  - Click on **Create**
## Container
  - Click on **Data Lake Storage** > Click on **Container** > Name it as **rriteccontainer** > Click on **Create**
  - ![image](https://user-images.githubusercontent.com/20516321/209080454-923c3672-5e86-4abb-a877-a85f5f43f26d.png)
## Folder
  - Open **rriteccontainer** > Click on **Add Directory** > Name it as **input**
  - Click on **Add Directory** > Name it as **output**
  - ![image](https://user-images.githubusercontent.com/20516321/209080956-412e8fa4-eef5-43f7-86b3-58cbc199ae78.png)
## Upload File
  - Open **rriteccontainer** > open **input** folder > Click on **upload** > from **labdata** select **emp.csv** > Click on **upload**
  - Right Click on **emp.csv** > observe all properties
  - ![image](https://user-images.githubusercontent.com/20516321/209083873-83ee8400-13d9-497a-8772-95e3ff065fa3.png)
# Azure Sql Database
  - Best for modern cloud applications. Hyperscale and serverless
  - Follow this blog for free Azure SQL database [doc](https://learn.microsoft.com/en-us/azure/azure-sql/database/free-sql-db-free-account-how-to-deploy?view=azuresql)
## Lab 1(Not required for training room)
  - In search box type **Azure SQL** > Under **services** > Click on **Azure SQL**
  - ![image](https://user-images.githubusercontent.com/20516321/209273844-196f7151-7378-40ea-a945-60bb8d8ef89b.png)

  - Click on **Create** > Select **Resource Type** as **Single Database**> Click on **Create** > provide below details accordingly as for your names
      - **Subsription:** Azure For Students
      - **Resource Groups**: master-rritec
      - **Database Name:** rritecazuresqldb
      - **Server:** click on **create new** > **Server Name:** rritecazuresqlserver > **Location:** (US) East US > Select **Use SQL Authentication** 
      - **Server admin login:**: saadmin
      - **password:** RRitec123$
      - **conformpassword:** RRitec123$
      - Click on **ok**
    - **workload environment:** Development
    - **Compute+Storage:** General purpose server less
    - **Backup Storagy Redundancy:** Local Redunt Backup Storage
    - Click on **Networking** tab > select **public Network Access:** Selected Networks
    - Click on **Add your client IPv4 address**
    - select **Allow Azure Services and resources to access this server**    - 
    - Click on **Review + Create**
    - Click on **Create**
    - ![image](https://user-images.githubusercontent.com/20516321/209275635-0512b890-d319-4a1b-b6f2-1eaa7b576eb8.png)

  ## Lab 2: create one table
  - Open **rritecazuresqldb**
  - Click on **Query Editor(preview)**
  - Under **sql server authentication** > provide **username:** as **saadmin** > **password:** as **RRitec123$**
  - Click on **ok**
  - Create emp,dept and salgrade tables and insert some data by running below code
      ``` sql

          CREATE TABLE [dbo].[DEPT]
          (DEPTNO INT PRIMARY KEY ,
          DNAME VARCHAR(20),
          LOC VARCHAR(20) );

          GO

          INSERT INTO [dbo].[DEPT] VALUES (10, 'ACCOUNTING', 'NEW YORK');

          INSERT INTO [dbo].[DEPT] VALUES (20, 'RESEARCH', 'DALLAS');

          INSERT INTO [dbo].[DEPT] VALUES (30, 'SALES', 'CHICAGO');

          INSERT INTO [dbo].[DEPT] VALUES (40, 'OPERATIONS', 'BOSTON');


          CREATE TABLE [dbo].[EMP]
          (EMPNO INT PRIMARY KEY,
          ENAME VARCHAR(20),
          JOB VARCHAR(20),
          MGR INT,
          HIREDATE DATE,
          SAL MONEY,
          COMM MONEY,
          DEPTNO INT );

          GO

          INSERT INTO [dbo].[EMP] VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-1980', 800, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-1981', 1600, 300, 30);

          INSERT INTO [dbo].[EMP] VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-1981', 1250, 500, 30);

          INSERT INTO [dbo].[EMP] VALUES (7566, 'JONES', 'MANAGER', 7839, '2-APR-1981', 2975, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-1981', 1250, 1400, 30);

          INSERT INTO [dbo].[EMP] VALUES (7698, 'BLAKE', 'MANAGER', 7839, '1-MAY-1981', 2850, NULL, 30);

          INSERT INTO [dbo].[EMP] VALUES (7782, 'CLARK', 'MANAGER', 7839, '9-JUN-1981', 2450, NULL, 10);

          INSERT INTO [dbo].[EMP] VALUES (7788, 'SCOTT', 'ANALYST', 7566, '09-DEC-1982', 3000, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-1981', 5000, NULL, 10);

          INSERT INTO [dbo].[EMP] VALUES (7844, 'TURNER', 'SALESMAN', 7698, '8-SEP-1981', 1500, 0, 30);

          INSERT INTO [dbo].[EMP] VALUES (7876, 'ADAMS', 'CLERK', 7788, '12-JAN-1983', 1100, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7900, 'JAMES', 'CLERK', 7698, '3-DEC-1981', 950, NULL, 30);

          INSERT INTO [dbo].[EMP] VALUES (7902, 'FORD', 'ANALYST', 7566, '3-DEC-1981', 3000, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7934, 'MILLER', 'CLERK', 7782, '23-JAN-1982', 1300, NULL, 10);

          INSERT INTO [dbo].[EMP] VALUES (1234, 'Ram', 'CLERK', 7782, '23-JAN-1982', 1400, NULL, 50);

          GO

          CREATE TABLE [dbo].[SALGRADE]
          (GRADE INT NOT NULL,
          LOSAL MONEY,
          HISAL MONEY );

          GO

          INSERT INTO [dbo].[SALGRADE] VALUES (1, 700, 1200);

          INSERT INTO [dbo].[SALGRADE] VALUES (2, 1201, 1400);

          INSERT INTO [dbo].[SALGRADE] VALUES (3, 1401, 2000);

          INSERT INTO [dbo].[SALGRADE] VALUES (4, 2001, 3000);

          INSERT INTO [dbo].[SALGRADE] VALUES (5, 3001, 9999);
          ```
  - Observe data by runing 
      ``` sql
      select * from emp
      ```
  - ![image](https://user-images.githubusercontent.com/20516321/209278382-d5706988-accb-4f72-add2-5f473a0f774d.png)

## Lab 3: Login and work in SSMS ttol
  - Instal SSMS tool by following [url](https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_01_Introduction_Installation.md#instal-sql-server-management-studio-ssms)
  - open **rritecAzuresqldb** > copy serbername
  - ![image](https://user-images.githubusercontent.com/20516321/209279155-117ad993-851b-4bb2-b732-956579425adc.png)

  - open SSMS tool
  - Provide below information
  - ![image](https://user-images.githubusercontent.com/20516321/209279299-d777b4cd-38e9-4e52-a832-c592d7c1d8a9.png)

  - Click on **Connect**
  - Expand **Databases**
  - Expand **rritecazuresqldb** > Expend **Tables**
  - Right click on **emp** table > click on **select top 1000 rows**
  - ![image](https://user-images.githubusercontent.com/20516321/209279628-efbc9e45-3ceb-431f-8974-8dfb1d27d141.png)

  - observe **query** and **result**
  - ![image](https://user-images.githubusercontent.com/20516321/209279761-0cdbb8b8-8104-4039-9221-72955c9ea239.png)
## Lab 4(optional): Login and work in Azure Data Studio tool
  - Instal Azure Data Studio and explore your own
# Azure Data Factory
  - In search box type **Data Factories** > Under **services** > Click on **Data Factories**
  - ![image](https://user-images.githubusercontent.com/20516321/209284786-7918e604-260e-479b-9b5d-30813b9ea286.png)

  - Click on **Create**
      - **Subsription:** Azure For Students
      - **Resource Groups**: master-rritec
      - **Name:** rritecadf
      - **Region:**East US
      - **Version:** V2
  - Click on **Review & Create**
  - Click on **Create**
  - ![image](https://user-images.githubusercontent.com/20516321/209289546-3f2a5fb3-8e31-492d-87cf-a9640ac9789a.png)
  - Click on **Go to Resource**
  - Click on **Launch Studio**
  - Observe all options

# Integration runtimes

1. The Integration Runtime (IR) is the compute infrastructure used by Azure Data Factory and Azure Synapse pipelines.
2. In Data Factory and Synapse pipelines, an activity defines the action to be performed
3. A linked service defines a target data store or a compute service
4. An integration runtime provides the bridge between activities and linked services
5. Data Factory offers three types of Integration Runtime (IR), and you should choose the type that best serves your data integration capabilities and network environment requirements. The three types of IR are:
  1. Azure
  2. Self-hosted
  3. Azure-SSIS
6. Refer the [doc](https://learn.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime)

# Linked Service

1. Linked services are much like connection strings, which define the connection information needed for the service to connect to external resource
2. `For example`: an Azure Storage linked service links a storage account to the service.
3. Refer the [doc](https://learn.microsoft.com/en-us/azure/data-factory/concepts-linked-services?tabs=data-factory)

# Linked Service to blob
  - Linked service defines the connection information to a data store or compute.
## Lab
  - Click on **Manage**
  - Click on **Linked Services**
  - Click on **New**
  - Under **Data Store** > select **Azure Blob Storage** > Click on **Continue**
  - **Name** it as **ls_to_blob_rritecsa**
  - **Connect Via Integration runtime:** AutoResloveIntegrationRuntime
  - **Authentication Type:** Account Key
  - **Account Selection Method:** From Azure Subscription
  - **Azure Subscription:** Azure For Students
  - **Storage Account Name:** rritecsa
  - Click on **Test Connection**
  - ![image](https://user-images.githubusercontent.com/20516321/209294913-03b3d076-39b6-4a3b-8415-104ee14f4ca6.png)
  - Click on **Create** -  
  - 
# Linked Service to Azure Sql Database  
## Lab
  - Click on **Manage**
  - Click on **Linked Services**
  - Click on **New**
  - Under **Data Store** > select **Azure SQL Database** > Click on **Continue**
  - **Name** it as **ls_to_rritecAzureSqlDB**
  - **Connect Via Integration runtime:** AutoResloveIntegrationRuntime
  - **Account Selection Method:** From Azure Subscription
  - **Azure Subscription:** Azure For Students
  - **Server Name:** rritecAzureSqlServer
  - **Database Name:** rritecAzureSqlDB
  - **Authentication Type:** SQL Authentication
  - **username:** saadmin
  - **password:** RRitec123$
  - Click on **Test Connection**  
  - ![image](https://user-images.githubusercontent.com/20516321/209418103-69375600-171e-47db-9c1f-3bb7fbff9199.png)

  - Click on **Create**

# Data Sets
  - Click on **Author**
  - Right Click on datasets > Create new **Folder** > Name it as **Source**
  - Right Click on **Source** folder > Click on **New Dataset** > Provide below options
  - ![image](https://user-images.githubusercontent.com/20516321/209418572-7638b228-3ec1-4ffd-ae70-af22b80cad39.png)
  - Right Click on datasets > Create new **Folder** > Name it as **target**
  - Right Click on **target** folder > Click on **New Dataset** > Provide below options
  - ![image](https://user-images.githubusercontent.com/20516321/209418743-bcf5f118-00b6-442b-bb0e-5cecbc75b36c.png)

# Create Pipenine from Blob to Azure Sql Database
  - Click on **Author**
  - Right Click on **pipelines** > Click on **New Folder** > Name it as **rritec_pipelines**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p01_from Blob to Azure Sql Database**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **Genera** tab > name it as **Copy_from_blob_to_AzureSqlDB**
  - Click on **Source** tab > Select **Source Dataset** as **src_emp**
  - Click on **Sink** tab > Select **Sink dataset** as **tgt_emp** > Select **Table Option** as **Auto Create Table**
  - Click on **Debug**
  - Under **output** tab > Observe run **Details**
  - ![image](https://user-images.githubusercontent.com/20516321/209774609-19490338-3be6-4f65-8a4e-bc762b3a7dc0.png)

  - Click on **publish** to save the work
  - ![image](https://user-images.githubusercontent.com/20516321/209419233-cd322af4-fb3e-4b62-9713-228462d1bbe8.png)
  - Understand the **output JSON** of **copy Activity**. For More information refer [URL](https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-monitoring?tabs=data-factory#monitor-programmatically) 
  - open SSMS > observe data in table
  - ![image](https://user-images.githubusercontent.com/20516321/209419293-07193ab6-aa37-49d6-bd60-ef786cbcc0ab.png)

# Additional Columns
  - Open Pipeline **p01_from Blob to Azure Sql Database**
  - Select **Copy Data** Activity
  - Click on **Source** tab 
  - In **Additional Columns**  > Click on **New**
  - provide as shown below
  - ![image](https://user-images.githubusercontent.com/20516321/209504074-83671970-e0cd-4a35-a09e-73a7b2e85ec6.png)

  - Click on **Sink** tab
  - In **Pre Copy Script** > type below sql code
``` sql
drop table [dbo].[TGT_EMP]
```
  - ![image](https://user-images.githubusercontent.com/20516321/209504332-94e596eb-5636-4627-b45a-b06c12efb274.png)

  - Click on **debug**
  - observe output jsons
  - open SSMS > observe data in table

# Create Pipenine from Blob to Blob
  - Click on **Author**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p02_from Blob to Blob**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **General** tab > name it as **Copy_from_blob_to_Blob**
  - Click on **Source** tab > Select **Source Dataset** as **src_emp**
  - Click on **Sink** tab > Select **Sink dataset** as **tgt_emp1**
  - ![image](https://user-images.githubusercontent.com/20516321/209508743-32207e73-d66b-4ec4-a705-fe271ef6f839.png)

  - Click on **Debug**
  - Under **Output** > observe **Details**
  - ![image](https://user-images.githubusercontent.com/20516321/209774847-4c1331d1-837d-4ff9-952f-33ec90b94657.png)

**Home Work:**
    1. Create Pipenine from Azure SQL Database to Blob    
    2. Create Pipenine from Azure SQL Database to Azure SQL Database
    
 

# Install SQL Server
  - Follow the [doc](https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_01_Introduction_Installation.md#msft-sql-server-installation) and install SQL Serer database
  - enable `sa` user by following [doc](https://www.top-password.com/knowledge/unlock-sql-server-sa-account.html)
  - provide password and remember it.

# Self Hosted IR
  - Perform data flows, data movement and dispatch activities to **external compute**
  - In **ADF** > Clcik on **Manage** > Under **Connections** > Click on **Integration Runtimes**
  - Click on **New**
  - Click on **Azure, Self-Hosted**
  - Click on **Self-Hosted**
  - Name it as **Self-Hosted-IR**
  - Click on **Create**
  - Click on **Express Setup** and install the software
  - Create a linked service using self-hsted IR
  - create a dataset using above linked service

# Create Pipenine from Blob to MS Sql Server
  - Click on **Author**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p03_from Blob to MS Sql Server**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **General** tab > name it as **Copy_from_blob_to_MS_SQL_Server**
  - Click on **Source** tab > Select **Source Dataset** as **src_emp**
  - Click on **Sink** tab > Select **Sink dataset** as **tgt_sql_server_emp**
  - Click on **Debug**
  - Under **Output** > observe **Details**
  - ![image](https://user-images.githubusercontent.com/20516321/209775129-191c309d-ccce-4c27-9c82-6aad1e5228fa.png)


# Create Pipenine from Azure SQL DB to MS Sql Server DB
  - Click on **Author**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p04_from Azure SQL DB to MS Sql Server DB**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **General** tab > name it as **Copy_from_Azure_sql_DB_to_MS_SQL_Server_DB**
  - Click on **Source** > Click on **New** > Select **Azure SQL Database** > Name it as **src_ds_azure_sql_emp**
  - Select **Linked Service** as **ls_to_rritecAzureSQlDB** > Select **table name** as **dbo.EMP**
  - Clcik on **OK**
  - Under **additional Columns** > click on **New** > **Name** it as **LoadDate** > **Value** as **@pipeline().TriggerTime**
  - ![image](https://user-images.githubusercontent.com/20516321/209767367-0c181c7d-7161-4670-832f-a655120f414a.png)

  - Click on **Sink** > Click on **New**
  - Select **SQL Server** > Click on **Continue**
  - **Name** it as **tgt_ds_sql_server_temp**
  - Select **Linked Service** as **ls_ms_sql_server**
  - provide **Schema** as **dbo** > **table** as **temp** > **Import Schema** as **None** > Click on **OK**
  - Select **Table Option** as **Auto Create Table**
  - ![image](https://user-images.githubusercontent.com/20516321/209773977-b189c318-fa71-4801-9230-b4021515b052.png)

  
  - Click on **Debug**
  - Observe Output.
  - ![image](https://user-images.githubusercontent.com/20516321/209774340-24d92c19-3170-41c9-a362-c46240eadee3.png)

# Load multiple sheets from excel to Azure SQL DB
**Step 1: Create Excel with sample data**
  - Open excel > in Sheet1 type as shown below

    ![image](https://user-images.githubusercontent.com/20516321/191252721-c4e945f6-6823-4747-a86f-e5ab65cf334f.png)

  - In Sheet2 type as shown below

    ![image](https://user-images.githubusercontent.com/20516321/191252829-46b4751e-0949-491b-95bd-bc476b85b506.png)

  - save it > name it as **Load_multiple_sheets_of_excel**
  
**Step 2: Upload Excel into Blob container folder**
  - Open > portal.azure.com > go to **storage account** > open **container** > open **folder** > upload above excel

**Step 3: Create source dataset wth sheetname as parameter**
  - Open **ADF Studio** > Click on **Author** > expand **Datasets** > Navigate to required folder > click on folder **...** > click on **New DataSet**
  - Select **Azure Blob Storage** > Click on **Continue** > Select **Excel** > Click on **Continue** > Name it as **src_multiple_sheets** > Select required **Linked Service** > Browse and point to above **Blob Excel** > select **First row as Header** > select import schema as **None** > Click on **ok**
  - Click on **Parameters** > Click on **New** > provide as shown below

    ![image](https://user-images.githubusercontent.com/20516321/191262796-d7b25243-8387-4eba-94ff-526498ded16e.png)
    


  - Clcik on **Connections** > Click on  **SheetName** > Click on **add dynamic content** > under **parameters** > click on **psheetname** parameter > Click on **ok**
  


    ![image](https://user-images.githubusercontent.com/20516321/191746516-27235344-7af2-41c1-9342-13a97f365f27.png)
    

**Step 4: Create Target dataset**
  - Open **ADF Studio** > Click on **Author** > expand **Datasets** > Navigate to required folder > click on folder **...** > click on **New DataSet**
  - Select **Azure SQL Database** > Click on **Continue** > Name it as **tgt_multiple_sheets** > select required **Linked Service** > Click on **Edit** > provide required schemaname and table name > select **none**
  - Click on **ok**

    ![image](https://user-images.githubusercontent.com/20516321/191257544-6f49fafb-1a42-4a71-92b7-8b1809a462ad.png)


**Step 5: Create Pipeline**

  - Open **ADF Studio** > Click on **Author** > expand **Pipelines** > Navigate to required folder > click on folder **...** > click on **New Pipeline**
  - Name pipeline as **p05_pipeline_load_multiple_sheets_to_azure_sql_database**
  - Click on **Variables** > Click on **New** > Provide as shown below
    
    ![image](https://user-images.githubusercontent.com/20516321/191259230-ae9fe749-6cde-40c2-abdd-11b4f0ca2a89.png)

  - From **Activities** > expand **Itteration & Conditionals** > drag and drop ** **ForEach** into work area
  - Click on **Settings** > select **Sequential** > Click on **Items** > click on **add dynamic content** > Click on **Variables** > click on **list_of_sheets** > clcik on **ok**

    ![image](https://user-images.githubusercontent.com/20516321/191260526-110579a8-5832-4aba-b0db-df82bd48759f.png)

  - Click on **Activities** > Click on **Edit** > drag and drop **CopyData** > Clcik on **Source** > Select **Source Dataset** > select **src_multiple_sheets** > Under **Dataset Properties** > Click on parameter **pSheetName** > Click on **add dynamic content** > Under **ForEachItterator** > click on **ForEach1** > Click on ok
  - Click on **Additional coumns** >> New >> provide as shown below
![image](https://user-images.githubusercontent.com/20516321/192457692-864308ab-32f6-4f57-b19c-79751df6ea6c.png)

  - Click on **Sink** > Select Sink Dataset as **tgt_multiple_Sheets** > Select **table option** as **Auto Create** > Click on **publish all** 

**Step 6: Trigger Pipeline**
  - Click on **Add Trigger** > Click on **Trigger now**
  - observe run status

     ![image](https://user-images.githubusercontent.com/20516321/209803014-312e7b9c-2c8e-4aca-af0b-d54870d76cda.png)


  - go to database and query target table andobserve both records

    ![image](https://user-images.githubusercontent.com/20516321/209803533-21b87745-5ccf-401e-831f-deeb7f17b036.png)

Related Content: 

1. [get dynamically all sheets using index numbers](https://learn.microsoft.com/en-us/answers/questions/986785/how-to-get-excel-sheet-names-dyanamically-in-azure)
2. [ADF xlsx file Dynamic sheet name](https://learn.microsoft.com/en-us/answers/questions/767239/adf-xlsx-file-dynamic-sheet-name)


# Get Excel Number of Sheets Dynamically and load it.

![image](https://user-images.githubusercontent.com/20516321/228440244-8cd81c11-813c-4014-b478-dd2fc385ad51.png)

1. Get Metadata From Excel
    1. Create a pipeline with the name of **Get Excel Number of Sheets Dynamically and load it**
    2. Drag and Drop **Get Metadata** activity into pipeline workarea
    3. Click on **Settings** > Click on **Dataset** `+New` > Select **Azure Blob Storage** > Click on **Continue** > Select **Excel** > Click on **Continue**
    4. Provide Dataset name as **ds_sec_excel** > Select blob linked service
    5. browse the excel file
    6. Select **Index**
    7. Select **First Row as Header**
    8. Import Schema as **None**
    9. Click on **Advanced** > click on **Open Dataset**
    10. Click on **parameters** > Clcik on **+New** > Name it as **pSheetIndex** > Data type as **Int**
    11. Click on **Connections** > 
    12. Provide Sheet index expressionas 
        ``` json
        @dataset().pSheetIndex
        
        ```
    13.Provide parameter value as **999**
    14. Under **Field List** > Click on **New** > select **argument** as **Structure** 

2. Get Error of Metadata Activity

    1. Drag and drop **Set Variable** activity into the work area > Name it as **Get Error of Metadata activity**
    2. connect **Get Metadata** fail with **Set Variable**
    3. Click on **Settings** > Click on **New** > Add new variable name as **Get Error** and Type as **String** > Click on **Conform**
    4. Provide Value as


       ![image](https://user-images.githubusercontent.com/20516321/228446981-5b93b669-1f25-4cfe-953a-0ff5d61b45fd.png)


3. Create Range Object
    1. Drag and drop one more **Set Varaible** > Name it as **range_of_page_numbers**
    2. Connect Previous activity to this activity using **Success**
    3. Click on **Settings** > Click on **New** > Add new variable name as **Range of Page Numbers** and Type as **Array** > Click on **Conform**
    4. Provide Value as
        
        ![image](https://user-images.githubusercontent.com/20516321/228446856-7526191b-6d80-4341-a50e-db328ab64525.png)

       

     
4. Create ForEach and Copy data activities
    1. Develop based on previous exercise knowledge
5. Run and observe each step input and ouput
![image](https://user-images.githubusercontent.com/20516321/228448475-57c9a1fd-520c-4c7d-b532-7b8430774e99.png)



 




# Incrementally load data

1. ![image](https://user-images.githubusercontent.com/20516321/209805592-c0bd3d78-968b-48f8-bdac-f715f11ab663.png)
2. ![image](https://user-images.githubusercontent.com/20516321/229040491-9d803caf-5e67-4997-a25c-72e8527a775c.png)




**Step 1: Create a data source/watermark/stored procedure in your SQL database**

1.  Open SSMS > Run the following SQL command against your SQL database to create a table named as **src_incr_emp** and load **5** records

``` sql

    create table src_incr_emp
    (
        empid int,
        ename varchar(255),
        hiredate datetime
    );
    
    GO

    INSERT INTO src_incr_emp
        (empid, ename, hiredate)
    VALUES
        (1, 'Myla RamReddy','9/1/2020 12:56:00 AM'),
        (2, 'Anam Tarun','9/2/2020 5:23:00 AM'),
        (3, 'John','9/3/2020 2:36:00 AM'),
        (4, 'Mark','9/4/2020 3:21:00 AM'),
        (5, 'Nancy','9/5/2020 8:06:00 AM');

```
2.  Create another table in your SQL database to store the **last load date** value

``` sql

    create table watermarktable
    (

    TableName varchar(255),
    last_load_date datetime,
    );

```
3.  Set the default value of the high watermark with the table name of target data store.

``` sql

    INSERT INTO watermarktable
    VALUES ('tgt_incr_emp','1/1/1900 12:00:00 AM')

```
4.  Observe the data

``` sql

    select * from watermarktable

```
5. Create a stored procedure in your SQL database

``` sql

    CREATE PROCEDURE sp_write_watermark @LastLoadDate datetime, @TableName varchar(50)
    AS

    BEGIN

    UPDATE watermarktable
    SET [last_load_date] = @LastLoadDate
    WHERE [TableName] = @TableName

    END

```
**Step 2: Get last load date**

1. Create a pipeline with the name **po6_IncrementalCopy**
2. Drag and drop the **Lookup** activity to the pipeline designer surface.
3. Change the name of the activity to **Lookup_last_load_date**
4. Click on **Settings** tab > click **+ New** for Source Dataset > Click on **SQL Server**
5. Name it as **ds_WatermarkDataset**
6. Select Linked Service of **SQL Server**
7. Select **Table Name** as **dbo.watermarktable**
8.  Click on **ok**
9.  select **Use query** as **Query**
10.  provide below query

``` sql

select * from [dbo].[watermarktable] 
where [TableName] ='tgt_incr_emp'

```
![image](https://user-images.githubusercontent.com/20516321/229045771-d11f564a-6b0f-4ec5-88d1-106385cc0b55.png)


**Step 3: Get_max_transaction_date_from_source**

1. Drag and drop one more lookup into work area
2. Name it as **Get_max_transaction_date_from_source**
3. Clcik on **Settings** tab > click **+ New** for Source Dataset > Click on **SQL Server**
5. Name it as **ds_src_incr_emp**
6. Select Linked Service of **SQL Server**
7. Select **Table Name** as **dbo.ds_src_incr_emp**
8.  Click on **ok**
9.  select **Use query** as **Query**
10.  provide below query

``` sql

select max(hiredate) as max_hiredate 
from [dbo].[src_incr_emp]

```
![image](https://user-images.githubusercontent.com/20516321/229046242-c9965e63-d216-41db-a5e5-d69730495286.png)

**Step 4: Copy data Incrementally**

1.  Drag and drop the **Copy Data** activity to the pipeline designer surface.
2.  Connect **both lookups** to **Copy Data** activities
3.  Select **Copy Data** activity > Click on **Source**
4.  select **Source Dataset** as **ds_src_incr_emp**
5.  Select **Use Query** as **Query**
6.  Provide **Query** as 

``` sql

select *  
from [dbo].[src_incr_emp]
where 
hiredate >= '@{activity('Get_last_load_date').output.firstRow.last_load_date}'
and hiredate <= '@{activity('Get_max_transaction_date_from_source').output.firstRow.max_hiredate}'

```
![image](https://user-images.githubusercontent.com/20516321/229047115-83b2cbd8-97ad-4cad-9c32-1a2cf7265f04.png)

7. Click on **Sink** > Click on **New** > Select **sql server** > Click on **Continue**
8. Provide **Name** as **ds_tgt_incr_emp**
9. select **Linked Service** as **sql server**
10. Click on **ok**
11. select **table option** as **auto create table**

![image](https://user-images.githubusercontent.com/20516321/229048946-5a3d9693-fa99-4141-ba4c-a63b0d35cdfa.png)


**Step 5: Update Last Load Date using Stored Procedure Activity**

1. Drag and drop **Stored Procedure** activity to the pipeline designer surface.
2. **Name** as **update_last_load_date**
3. Select **linked Service** as **ls_sqlserver**
4. Select **Stored Procedure Name** as **[dbo].[sp_write_watermark]**
5. Under **Stored Procedure Parameters** > Click on **Import**
6. Select **LastLoadDate** value as **@activity('lookup_get_max_date_from_source').output.firstRow.max_date**
7. Select **TableName** value as **@activity('Lookup_last_load_date').output.firstRow.tablename**

![image](https://user-images.githubusercontent.com/20516321/229049854-49c94a7a-f401-464c-9e31-662ffaf4aa54.png)

**Step 6: Run and observe steps**

1. Click on **debug** > observe run steps

![image](https://user-images.githubusercontent.com/20516321/229049992-c4c25531-63ca-46fe-a13e-2a7d34b273b8.png)

**Step 7: Run one more time by adding few rows and observe steps**

1. Insert two records 

``` sql

INSERT INTO src_incr_emp
VALUES (6, 'geo','9/6/2017 2:23:00 AM')

INSERT INTO src_incr_emp
VALUES (7, 'albert','9/7/2017 9:01:00 AM')

```
2. Click on **debug** > observe run steps


# Incremental copy multiple tables
Ref: Follow MSFT [doc](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-multiple-tables-portal)
# Incremental copy lastmodified copy data tool
Ref: Follow MSFT [doc](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-lastmodified-copy-data-tool)
# Incremental copy partitioned file name copy data tool
Ref: Follow MSFT [doc](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-partitioned-file-name-copy-data-tool)

# Triggers

1. A pipeline run in Azure Data Factory and Azure Synapse defines an instance of a pipeline execution.
2. For example, say you have a pipeline that executes at 8:00 AM, 9:00 AM, and 10:00 AM. In this case, there are three separate runs of the pipeline. Each pipeline run has a unique pipeline run ID.
3. A run ID is a GUID that uniquely defines that particular pipeline run
4. types of triggers
    1. Scheduled
    2. Tumbling window
    3. Storage event
    4. Custom event
5. Pipelines and triggers have a many-to-many relationship (except for the tumbling window trigger). 
6. Multiple triggers can kick off a single pipeline, or a single trigger can kick off multiple pipelines
7. Open any Pipeline > Click on **Add Trigger** > Click on **New/Edit**
8. Click on **New** > Name it as **Daily_trigger**

![image](https://user-images.githubusercontent.com/20516321/229695521-76fb098a-04ca-4f0f-89e5-5929997416bc.png)

9. Click on ok

# Logic Apps

**Step 1: Create email workflow endpoint using Gmail**

![image](https://user-images.githubusercontent.com/20516321/208333982-d43d8332-1a6d-44af-809d-d26f25204ce2.png)

1. In search box type **Logic Apps** > Under **services** > Click on **Logic Apps**
2. Click on **Add** > Provide required information as for your subscription
3. ![image](https://user-images.githubusercontent.com/20516321/209438015-aaf01251-0a7c-4f75-93f8-5ac4e009cd2d.png)
3. Click on **review&create**
4. After Deployment completed > click on **Goto resource** > Click on **ADD**
5. Under **Start with a common trigger** > Click on **When a HTTP request is received**

    ![image](https://user-images.githubusercontent.com/20516321/209438373-8aba531f-9851-4634-a768-c27fe2be56dd.png) 
    
6. Under **Request body json Schema** > Copy and paste below **json** code 

``` json 
{
    "properties": {
        "dataFactoryName": {
            "type": "string"
        },
        "pipelineName": {
            "type": "string"
        },
        "status": {
            "type": "string"
        },
        "message": {
            "type": "string"
        }
    },
    "type": "object"
}
 
```
7. At the top of the Logic Apps Designer > Click on **Save** 
8. You can now see the URL of your HTTP request
9. Select the copy icon to copy it 
10. Paste in your **notepad.**
11. We will use this URL later in ADF pipeline web activity
12. ![image](https://user-images.githubusercontent.com/20516321/209442383-618a03ed-462e-46df-a3bb-53a217319f16.png)
13. Click on **New step** > type **Gmail** in the actions search box > Search and select **Send email (V2)** 
14. Type connection name as **sendstatusmail** as per below dialog box
15. Click on **sign in** > Give you **gmail userid and password**.
16. Type TargetGmail in **To** address 
17. click on **Add parameter** and in drop down select **Body** and **subject**.
18. ![image](https://user-images.githubusercontent.com/20516321/211259603-dfa11d6f-b986-41ca-9c1d-4e91b64fcd29.png)

**Step 2: Call Logic app inside the Pipeline to send Succeeded email**
   
1. Go to **Azure Data Factory** > click **Launch Studio** > Click on **Author** 
2. Open the pipeline **p01_Create Pipenine from Blob to Azure Sql Database**
3. In Activities Search for **Web** and drag into workflow.
4. ![image](https://user-images.githubusercontent.com/20516321/209440556-3604c90e-3284-4f8a-a610-2ab37e09378f.png)
5. Click on **web** > In **General** tab give name of Activity **successmail** > open settings tab past **URL** from notepad
6. Select **Method** as **POST**
7. Click on **Body** > Click on **Add dynamic expression**. > Copy and paste below json code > Click on **ok**
``` json
{
    "dataFactoryName":"@{pipeline().DataFactory}",
    "pipelineName":"@{pipeline().Pipeline}",
    "status":"@{activity('Copy data from blob to azuresqldb').output.executionDetails[0].status}",
    "message":"The Number of rows Read from Source is:  @{activity('Copy data from blob to azuresqldb').output.rowsRead} <br/>
    The Number of rows Copied to target is: @{activity('Copy data from blob to azuresqldb').output.rowsCopied}"
}
```
7.  Click on **Headers** **+ New** > Provide **Name** as **Content-Type** > Provide **Value** as **application/json**
14. Click on **Debug**
15. Observe Mail.
16. ![image](https://user-images.githubusercontent.com/20516321/211261313-781433ed-c256-46aa-a912-889f0ed0e4f3.png)


**Step 3: Call Logic app inside the Pipeline to send Failed email**

1. Inside the pipeline click on web activity **clone**
2. In **General** tab give name of Activity **Failedmail** 
7. Click on **Body** > Click on **Add dynamic expression**. > Copy and paste below json code > Click on **ok**
``` json
{
    "dataFactoryName": "@{pipeline().DataFactory}",
    "pipelineName": "@{pipeline().Pipeline}",
    "status": "@{activity('Copy data from blob to azuresqldb').output.executionDetails[0].status}",
    "message": "The Error Message is : @{activity('Copy data from blob to azuresqldb').output.errors[0].Message}"
    
}

```
7.  Select **Copy Data** activity > Click on **Source** > Click on **open**
8.  Change file name as **emp1111111.csv**(Note: this file is not availble inside our blob)
9.  Click on **Debug**
15. Observe Mail.
16. ![image](https://user-images.githubusercontent.com/20516321/211262341-951c70f4-6676-43cb-bcea-2dac4562eb6c.png)

Refer for more information [msft doc](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-control-flow-portal)

# DataFlows

1. Mapping data flows are visually designed data **transformations** in Azure Data Factory.
2. Data flows allow data engineers to develop data transformation logic without writing code.
3. The resulting data flows are executed as activities within Azure Data Factory pipelines that use scaled-out Apache Spark clusters.
4. Data flow activities can be operationalized using existing Azure Data Factory scheduling, control, flow, and monitoring capabilities.
5. Mapping data flows provide an entirely visual experience with no coding required.
6. Your data flows run on ADF-managed execution clusters for scaled-out data processing.
7. Azure Data Factory handles all the code translation, path optimization, and execution of your data flow jobs.
8. Reference1 [MSFT Doc](https://learn.microsoft.com/en-us/azure/data-factory/concepts-data-flow-overview)

## Lab

1. Create required tables for our below lab in sqlserver database.
``` sql

CREATE TABLE [dbo].[DEPT]
(DEPTNO INT PRIMARY KEY ,
DNAME VARCHAR(20),
LOC VARCHAR(20) );

GO

INSERT INTO [dbo].[DEPT] VALUES (10, 'ACCOUNTING', 'NEW YORK');

INSERT INTO [dbo].[DEPT] VALUES (20, 'RESEARCH', 'DALLAS');

INSERT INTO [dbo].[DEPT] VALUES (30, 'SALES', 'CHICAGO');

INSERT INTO [dbo].[DEPT] VALUES (40, 'OPERATIONS', 'BOSTON');


CREATE TABLE [dbo].[EMP]
(EMPNO INT PRIMARY KEY,
ENAME VARCHAR(20),
JOB VARCHAR(20),
MGR INT,
HIREDATE DATE,
SAL MONEY,
COMM MONEY,
DEPTNO INT );

GO

INSERT INTO [dbo].[EMP] VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-1980', 800, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-1981', 1600, 300, 30);

INSERT INTO [dbo].[EMP] VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-1981', 1250, 500, 30);

INSERT INTO [dbo].[EMP] VALUES (7566, 'JONES', 'MANAGER', 7839, '2-APR-1981', 2975, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-1981', 1250, 1400, 30);

INSERT INTO [dbo].[EMP] VALUES (7698, 'BLAKE', 'MANAGER', 7839, '1-MAY-1981', 2850, NULL, 30);

INSERT INTO [dbo].[EMP] VALUES (7782, 'CLARK', 'MANAGER', 7839, '9-JUN-1981', 2450, NULL, 10);

INSERT INTO [dbo].[EMP] VALUES (7788, 'SCOTT', 'ANALYST', 7566, '09-DEC-1982', 3000, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-1981', 5000, NULL, 10);

INSERT INTO [dbo].[EMP] VALUES (7844, 'TURNER', 'SALESMAN', 7698, '8-SEP-1981', 1500, 0, 30);

INSERT INTO [dbo].[EMP] VALUES (7876, 'ADAMS', 'CLERK', 7788, '12-JAN-1983', 1100, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7900, 'JAMES', 'CLERK', 7698, '3-DEC-1981', 950, NULL, 30);

INSERT INTO [dbo].[EMP] VALUES (7902, 'FORD', 'ANALYST', 7566, '3-DEC-1981', 3000, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7934, 'MILLER', 'CLERK', 7782, '23-JAN-1982', 1300, NULL, 10);

INSERT INTO [dbo].[EMP] VALUES (1234, 'Ram', 'CLERK', 7782, '23-JAN-1982', 1400, NULL, 50);

```

2. Develop a dataflow equal to below query

``` sql

select 
  dname, 
  sum(sal) as total_sal 
from 
  emp, 
  dept 
where 
  emp.deptno = dept.deptno 
  and emp.deptno in (10, 20) 
group by 
  dname 
order by 
  2 asc
  
```

![image](https://user-images.githubusercontent.com/20516321/211307068-69491755-f804-41ad-9abd-f3023d54b7e8.png)

3. Create a new pipeline with the name of **p01_dataflow1**
4. From **Activities** > From **Move & transform** > Drag and drop **Data flow** activity
5. In **General** tab > Type **Name** as **d01_dataflow**
6. Click on **Settings** tab > In **Data flow** Section > Click on **+ New**
7. provide **Name** as **d01_dataflow1**
8. Click on **Add Source**
9. Provide **Output Stream Name** as **SrcEmp**
10. Select **Dataset** as **ds_df_src_emp**

![image](https://user-images.githubusercontent.com/20516321/211466552-1753baf0-4a2c-468d-873c-e1822b73f280.png)

12. Click on another empty **Add Source** drop down > Click on **Add Source**
13. Provide **Output Stream Name** as **SrcDept**
14. Select **Dataset** as **ds_df_src_dept**

![image](https://user-images.githubusercontent.com/20516321/211466976-ad58d71e-dece-432d-869a-0b947af0c7a5.png)

16. Click on **SrcEmp** + icon > add **select** Schema Modifier
17. Provide **Output Stream Name** as **select1Emp**
18. Under **input columns** delete all columns except **deptno** and **sal**

![image](https://user-images.githubusercontent.com/20516321/211467974-52456b35-cca6-4362-b947-09be984c577a.png)

22. Click on **SrcDept** + icon > add **select** Schema Modifier
23. Provide **Output Stream Name** as **selectDept**
24. Under **input columns** delete all columns except **deptno** and **dname**

![image](https://user-images.githubusercontent.com/20516321/211468763-b7bf121b-19b7-4059-93a7-916054c437a6.png)

28. Click on **Select1Emp** + icon > add **filter** row Modifier
29. Click on **Filter on** expression builder > provide expression as ``` DEPTNO == 10 || DEPTNO == 20 ```

30. Click on **filter1** + icon > Select **Join** from **Multiple inputs/outputs**
31. Select **join1** > Select **left stream** as **filter1** > select **right stream** as **select2dept** > join type** as **inner** 
32. Select **Join Conditions** > left and right columns as **DEPTNO**

![image](https://user-images.githubusercontent.com/20516321/211472517-a1c652d1-806e-482d-854f-63c39e65dcdf.png)

34. Click on **Join1** + icon > from **Schema Modifier** select **Aggregate**
35. Under **group by** select **Dname** column
36. Under **Aggregates** > name **column** as **totalsal** > **Expression** as ```sum(SAL)```

![image](https://user-images.githubusercontent.com/20516321/211473271-8cd7c99f-15fd-421e-9cb8-1eec83ddd46f.png)

38. Click on **aggregate1** + icon > From **row modifier** select **Sort**
39. select sort column as **totalsal** and order as **ascending**

![image](https://user-images.githubusercontent.com/20516321/211474756-6c8070ff-0617-4324-852a-1f0a3ba4977a.png)

41. Click on **sort1** + icon > From **destination** select **Sink**
42. select dataset as **tgt_azure_sql_agg**
43. under settings select **table actio** as **recreate table**

![image](https://user-images.githubusercontent.com/20516321/211474483-7a2134c5-2ec2-4af8-af40-c13e3d03d568.png)

42. Click on **debug**
43. observe output

![image](https://user-images.githubusercontent.com/20516321/211707073-7e8b9532-e18e-43ea-ae3b-299c732364f1.png)


![image](https://user-images.githubusercontent.com/20516321/211475778-9a14f8f3-ab70-44ec-bece-5a80af570163.png)





Reference : [Joins](https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_06_Power%20Query%20Editor%20Combine%20Data.md)

# Split Transformation

Go to **AzureDataFactory(ADF)** > Click on **Author** > Create New Pipeline > Give name as **Pipeline1_Dataflows_split** > Drag **Dataflow Activity** from Activity pane into work area 

![image](https://user-images.githubusercontent.com/20516321/212013537-97dda0ff-95d0-4019-afdc-9a43482ff8bd.png)

Click on Dataflow Activity > Go to settings > Click on New > Give name as **Dataflow_Split** > Click on **Add Source** > Go to **sourceSetting** > Give name as **Source1emp** > Bottom **sourceSetting** > Select **Dataset** as **Src_azure_sql_emp**

![image](https://user-images.githubusercontent.com/20516321/211998478-8cfbf6b0-01eb-438a-89fa-8299e7aa8afa.png)

Click on add symbol > Search for **Conditional split** > Bottom of Conditional split > In split condition > Follow as per below picture

![image](https://user-images.githubusercontent.com/20516321/212001689-83074d4b-26e2-4ea9-abd5-6fa6dc10e8f2.png)

![image](https://user-images.githubusercontent.com/20516321/212001899-fad78590-b9d7-40df-91f4-dd60c7ca90b1.png)

Click on add symbol > search for **Sink** > Give Name as Sink1 > Below sink Create New dataset > Give name as DS_Sink_Emp10 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink_Emp10

![image](https://user-images.githubusercontent.com/20516321/212005400-e1c0d2d0-9a31-4d5c-840f-95934fac6f45.png)

Click on add symbol > search for **Sink2** > Give Name as Sink2 > Below sink Create New dataset > Give name as DS_Sink_emp20 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink2_Emp20

![image](https://user-images.githubusercontent.com/20516321/212005713-a0d70a1f-b9d5-45dc-9e81-056c04eab7df.png)

Click on add symbol > search for **Sink3** > Give Name as Sink3 > Below sink Create New dataset > Give name as DS_Sink_emp30 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink3_emp30

![image](https://user-images.githubusercontent.com/20516321/212005953-57baff49-37af-43a0-af74-d19bd59b060a.png)

Go to **Pipeline1_Dataflows_Split1** > Click on **validate** > Click on **Publish** > Click on **Debug**

![image](https://user-images.githubusercontent.com/20516321/212010636-3e28670e-de15-4f5a-b526-cde00ab9abea.png)

Now Open **SQL SERVER** > Check data of table **[dbo].[Ds_Sink_emp10]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink_emp10]
```
![image](https://user-images.githubusercontent.com/20516321/212011205-8a77c32e-abd4-46b4-9fa2-4d77560f7d34.png)

Check data of table **[dbo].[Ds_Sink2_emp20]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink2_emp20]
```
![image](https://user-images.githubusercontent.com/20516321/212012385-bb3e4013-fb1f-4eb8-9b00-a4ebcaf993cb.png)

Check data of table **[dbo].[Ds_Sink3_emp30]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink3_emp30]
```

![image](https://user-images.githubusercontent.com/20516321/212012706-9c0caf2a-1c16-4470-9f0f-03cd7408acca.png)

# Azure DevOps
## Source Control

1. Open azure [Free Services](https://portal.azure.com/#view/Microsoft_Azure_Billing/FreeServicesBlade)
2. Click on Azure DevOps **Create**

![image](https://user-images.githubusercontent.com/20516321/230009150-7f2e6965-cce7-4eb5-9fa8-9c913ab396f2.png)

3. Select **Default Directory**
4. Click on **Create New Organization**
5. Click on **Continue**
6. Name organization name as **rritecorg**
7. provide project name as **rritecproj**

# cost

1. refer [link](https://sqlkover.com/how-you-can-save-up-to-80-on-azure-data-factory-pricing/#:~:text=Minimize%20the%20number%20of%20activities,a%20self%2Dhosted%20integration%20runtime.)









