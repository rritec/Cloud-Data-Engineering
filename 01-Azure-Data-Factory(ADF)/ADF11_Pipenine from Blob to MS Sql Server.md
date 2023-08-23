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
