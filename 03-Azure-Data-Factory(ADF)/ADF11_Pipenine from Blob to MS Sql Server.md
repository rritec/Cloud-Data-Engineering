# Install SQL Server
  - Follow the [doc](https://github.com/rritec/POWERBI/blob/master/01.%20Notebooks/PBI_01_01_Introduction_Installation.md#msft-sql-server-installation) and install SQL Serer database
  - Install SSMS [doc](https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_01_Introduction_Installation.md#instal-sql-server-management-studio-ssms)
  - enable `sa` user by following [doc](https://www.top-password.com/knowledge/unlock-sql-server-sa-account.html)
  - provide password and remember it.
  - Create Database in Local sql server.
    ```Sql
    Create Database RRitecDB
    ```
    


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

    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/6f237696-b51d-4463-be3e-457903482663)

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
# Home Work
1. Create pipeline to copy data from AzureBlob to AzureBlob
2. Create pipeline to copy data from AzureBlob to AzureSqlDatabase
3. Create pipeline to copy data from AzureBlob to SqlServer
4. Create pipeline to copy data from AzureSqlDatabase to AzureBlob
5. Create pipeline to copy data from AzureSqlDatabase to AzureSqlDatabase
6. Create pipeline to copy data from AzureSqlDatabase to SqlServer
7. Create pipeline to copy data from SqlServer to AzureBlob
8. Create pipeline to copy data from SqlServer to AzureSqldatabase
9. Create pipeline to copy data from SqlServer to SqlServer

# Questions
1. DIUhours 
# Answers
1. Data Integration Unit Hours
