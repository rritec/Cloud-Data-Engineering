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

# Questions

1. I have two Azure SQL Databases (for example **asdb1**, **asdb2** ) then how many Linked services required?
2. Linked service is a connection string ? is it true?

# Answers
1. 2
2. True
