Scenario: How to take backup of one file, after loading into azure SQL Database? 

# Create Pipenine from Blob to Blob

1. Click on **Author**
2. Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p02_from Blob to Blob**
3. Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
4. Under **General** tab > name it as **Copy_from_blob_to_Blob**
5. Click on **Source** tab > Select **Source Dataset** as **src_emp**
6. Click on **Sink** tab > Select **Sink dataset** as **tgt_emp1**

   ![image](https://user-images.githubusercontent.com/20516321/209508743-32207e73-d66b-4ec4-a705-fe271ef6f839.png)

7. Click on **Debug**
8. Under **Output** > observe **Details**

![image](https://user-images.githubusercontent.com/20516321/209774847-4c1331d1-837d-4ff9-952f-33ec90b94657.png)

# Home Work:

1. Create Pipenine from Azure SQL Database to Blob    
2. Create Pipenine from Azure SQL Database to Azure SQL Database
   
# Questions
# Answers
