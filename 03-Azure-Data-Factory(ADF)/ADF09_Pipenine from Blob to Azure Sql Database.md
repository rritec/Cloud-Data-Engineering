# Lab 1: Create Pipenine from Blob to Azure Sql Database

  1. Click on **Author**
  1. Right Click on **pipelines** > Click on **New Folder** > Name it as **rritec_pipelines**
  1. Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p01_from Blob to Azure Sql Database**
  1. Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  1. Under **Genera** tab > name it as **Copy_from_blob_to_AzureSqlDB**
  1. Click on **Source** tab > Select **Source Dataset** as **src_emp**
  1. Click on **Sink** tab > Select **Sink dataset** as **tgt_emp** > Select **Table Option** as **Auto Create Table**
  1. Click on **Debug**
  1. Under **output** tab > Observe run **Details**

     ![image](https://user-images.githubusercontent.com/20516321/209774609-19490338-3be6-4f65-8a4e-bc762b3a7dc0.png)

  1. Click on **publish** to save the work

     ![image](https://user-images.githubusercontent.com/20516321/209419233-cd322af4-fb3e-4b62-9713-228462d1bbe8.png)

  1. Understand the **output JSON** of **copy Activity**. For More information refer [URL](https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-monitoring?tabs=data-factory#monitor-programmatically) 
  1. open SSMS > observe data in table

     ![image](https://user-images.githubusercontent.com/20516321/209419293-07193ab6-aa37-49d6-bd60-ef786cbcc0ab.png)

# Lab 2: Additional Columns

1. Open Pipeline **p01_from Blob to Azure Sql Database**
2. Select **Copy Data** Activity
3. Click on **Source** tab 
4. In **Additional Columns**  > Click on **New**
5. provide as shown below
6. ![image](https://user-images.githubusercontent.com/20516321/209504074-83671970-e0cd-4a35-a09e-73a7b2e85ec6.png)
7. Click on **Sink** tab
8. In **Pre Copy Script** > type below sql code

``` sql
drop table [dbo].[TGT_EMP]
```
9. ![image](https://user-images.githubusercontent.com/20516321/209504332-94e596eb-5636-4627-b45a-b06c12efb274.png)
10. Click on **debug**
11. observe output jsons
12. open SSMS > observe data in table

# Questions
1. What is Pipeline ?  
2. Types of Activities ?
3. What is the output if $$FILEPATH and $$FILENAME,inbelow configuration?
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/aa516e7d-9768-4d6f-a347-6063698518b1)

4. 


# Answers
1. A data-driven workflow that can ingest data from multiple sources
2. Three types, those are given below, for more info refer [doc](https://learn.microsoft.com/en-in/azure/data-factory/concepts-pipelines-activities?tabs=data-factory)
    1. **Data movement activities:** These activities write data from any source store to a data sink.
    2. **Data transformation activities:** These activities transform, filter, and enhance data.
    3. **Control activities:** These activities can include deleting a file, copying data between sources, or looping through items.
3. ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/789c670f-6cc9-4752-8953-7443e30addee)

