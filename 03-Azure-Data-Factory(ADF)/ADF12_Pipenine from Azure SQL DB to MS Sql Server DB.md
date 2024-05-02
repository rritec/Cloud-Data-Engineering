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

# Questions
1. 
# Answers
1. 
