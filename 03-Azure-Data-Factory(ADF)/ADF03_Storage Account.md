# Resource Group?
1. A resource group is a container that enables you to manage related resources for an Azure solution
2. Refer more [here](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview#resource-groups)
# Storage Account
  - Azure Storage is a Microsoft-managed service providing cloud storage that is 
      - highly available
      - secure
      - durable
      - scalable
      - redundant. 
  - Azure Storage includes Azure Blobs (objects), Azure Data Lake Storage Gen2, Azure Files, Azure Queues, and Azure Tables
## Azure Storage redundancy
1. LRS

![image](https://github.com/user-attachments/assets/77a9084b-acf8-404e-a81b-98fb08fd25ec)

2. ZRS

![image](https://github.com/user-attachments/assets/d1196b2b-717d-4045-a7ef-cf1f8662857e)

3. GRS or RA-GRS

![image](https://github.com/user-attachments/assets/20d4a895-478e-48ba-8685-342f1c099d98)

4. GZRS or RA-GZRS

![image](https://github.com/user-attachments/assets/50d417c0-bf98-4961-a3c7-04e6b855652b)



## Create BLOB Storage
  - Open [Azure Portal](https://portal.azure.com/)> > Click on the search bar > Type **Storage accounts** > Click on **Storage Accounts**
  - Click on **Create** > Under **Basics** tab provide below details
      - Subscription: **rritecsubscription**
      - Resource Group: **rritecresoucegroup**
      - Storage Account Name: **rritecsa**
      - Region: **(US) East US**
      - Performance: **Standard**
      - Redundancy: **Locally-Redundant Storage (LRS)**  
  - Click on **Review**
  - Click on **Create**
## Create ADLS
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
## Create Container
  - Click on **Data Lake Storage** > Click on **Container** > Name it as **rriteccontainer** > Click on **Create**
  - ![image](https://user-images.githubusercontent.com/20516321/209080454-923c3672-5e86-4abb-a877-a85f5f43f26d.png)
## Create Folder
  - Open **rriteccontainer** > Click on **Add Directory** > Name it as **input**
  - Click on **Add Directory** > Name it as **output**
  - ![image](https://user-images.githubusercontent.com/20516321/209080956-412e8fa4-eef5-43f7-86b3-58cbc199ae78.png)

## Upload File

  - Open **rriteccontainer** > open **input** folder > Click on **upload** > from **labdata** select **emp.csv** > Click on **upload**
  - Right Click on **emp.csv** > observe all properties
  - ![image](https://user-images.githubusercontent.com/20516321/209083873-83ee8400-13d9-497a-8772-95e3ff065fa3.png)

# Learning Path

1. Introduction to Azure Data Lake Storage Gen2](https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-data-lake-storage/)
2. [Exam AZ-900: Microsoft Azure Fundamentals](https://learn.microsoft.com/en-in/credentials/certifications/exams/az-900/)

# Reference Material

1. [storage-account-overview](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview)
2. [storage-account-create](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal)
3. [storage-redundancy](https://learn.microsoft.com/en-us/azure/storage/common/storage-redundancy)
4. [access-tiers-overview](https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview)

# Questions

1. BLOB Stands for ?
    - Binary Large Object
    - It allows users to store large amounts of unstructured data on Microsoft's data storage platform
2. How Many types of redundencys available?
    - LRS
    - ZRS
    - GRS or RA-GRS
    - GZRS or RA-GZRS
3. How many types of Access tiers available?
    - Hot Tier
    - Cool Tier
    - Cold Tier
    - Archive Tier
4. Read blob using python pandas
    - Click on ... blob > Click on Generate SAS > Click on generate SAS token and URL > Copy Blob SAS URL > replace below url and run it in any python notebook
   ```python
    import pandas as pd
    data = pd.read_csv('https://b2311sa.blob.core.windows.net/rritecc/input/emp.csv?sp=r&st=2023-11-07T05:51:14Z&se=2023-11-07T13:51:14Z&sv=2022-11-02&sr=b&sig=dqNiY2dV%2B2FiMTMk5ffDNjjm341clAcM7iMYi8D0UVI%3D')
    print(type(data))
    print(data.head(25))
   ```
6. Azure Data Lake Storage Gen2 stores data in…
    1. A document database hosted in Azure Cosmos DB.
    2. An HDFS-compatible file system hosted in Azure Storage.
    3. A relational data warehouse hosted in Azure Synapse Analytics.
       
7. What option must you enable to use Azure Data Lake Storage Gen2?
    1. Global replication
    2. Data encryption
    3. Hierarchical namespace
8. Blob Storage Vs ADLS Gen1 Vs ADLS Gen2
   
# Answers
6. 2
7. 3
8. Blob Storage Vs ADLS Gen1 Vs ADLS Gen2
    1. **Purpose:**
        1. Blob storage: General-purpose storage for unstructured data like images, videos, text files, and backups.
        2. ADLS Gen1: Primarily for large-scale big data analytics using Hadoop-compatible tools.
        3. ADLS Gen2: Optimized for large-scale data analytics while offering a more modern, flexible file system interface built on top of Blob storage.
    2. **When to use which:**
        1. Blob storage: When you need to store large amounts of unstructured data with simple access requirements, like website content or application backups.
        2. ADLS Gen1: If you have existing Hadoop workflows and need to maintain compatibility with a traditional HDFS-like structure.
        3. ADLS Gen2: For most big data analytics scenarios where you need a hierarchical file system and want to leverage the scalability and cost-effectiveness of Blob storage. 
