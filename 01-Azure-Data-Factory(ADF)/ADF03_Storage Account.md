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

# Learning Path

1. [Exam AZ-900: Microsoft Azure Fundamentals](https://learn.microsoft.com/en-in/credentials/certifications/exams/az-900/)

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
    - GRS
    - RA-GRS
    - GZRS
    - RA-GZRS
3. How many types of Access tiers available?
    - Hot Tier
    - Cool Tier
    - Cold Tier
    - Archive Tier
4. read blob using python pandas
    - Click on ... blob > Click on Generate SAS > Click on generate SAS token and URL > Copy Blob SAS URL > replace below url and run it in any python notebook
   ```python
    import pandas as pd
    data = pd.read_csv('https://b2311sa.blob.core.windows.net/rritecc/input/emp.csv?sp=r&st=2023-11-07T05:51:14Z&se=2023-11-07T13:51:14Z&sv=2022-11-02&sr=b&sig=dqNiY2dV%2B2FiMTMk5ffDNjjm341clAcM7iMYi8D0UVI%3D')
    print(type(data))
    print(data.head(25))
   ```
6. 
