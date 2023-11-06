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
# Questions
1. BLOB Stands for ?
    - Binary Large Object
    - It allows users to store large amounts of unstructured data on Microsoft's data storage platform
2. 
