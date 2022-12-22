### DP-203 Azure Data Engineer
1. **[Introduction](#Introduction)**<br>
2. **[Azure Free Account](#Azure-Free-Account)**<br>
3. **[Storage Account](#Storage-Account)**<br>


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

        ![image](https://user-images.githubusercontent.com/20516321/209080454-923c3672-5e86-4abb-a877-a85f5f43f26d.png)
## Folder
  - Open **rriteccontainer** > Click on **Add Directory** > Name it as **input**
  - Click on **Add Directory** > Name it as **output**

        ![image](https://user-images.githubusercontent.com/20516321/209080956-412e8fa4-eef5-43f7-86b3-58cbc199ae78.png)

