### Step 1: Create Excel with sample data
  - Open excel > in Sheet1 type as shown below
    ![image](https://user-images.githubusercontent.com/20516321/191252721-c4e945f6-6823-4747-a86f-e5ab65cf334f.png)

  - In Sheet2 type as shown below
    ![image](https://user-images.githubusercontent.com/20516321/191252829-46b4751e-0949-491b-95bd-bc476b85b506.png)

  - save it > name it as **Load_multiple_sheets_of_excel**
  
### Step 2: Upload Excel into Blob container folder
  - Open > portal.azure.com > go to **storage account** > open **container** > open **folder** > upload above excel

### Step 3: Create source dataset wth sheetname as parameter
  - Open **ADF Studio** > Click on **Author** > expand **Datasets** > Navigate to required folder > click on folder **...** > click on **New DataSet**
  - Select **Azure Blob Storage** > Click on **Continue** > Select **Excel** > Click on **Continue** > Name it as **src_multiple_sheets** > Select required **Linked Service**
  - > Browse and point to above **Blob Excel** > Under **SheetName** > select **Edit** > name parameter as **pSheetName** > select **First row as Header** > select import schema as **None** > Click on **ok**
    ![image](https://user-images.githubusercontent.com/20516321/191255618-f07ef258-434d-4af5-ad7f-cd62c1223639.png)
### Step 4: Create Target dataset
  - Open **ADF Studio** > Click on **Author** > expand **Datasets** > Navigate to required folder > click on folder **...** > click on **New DataSet**
  - Select **Azure SQL Database** > Click on **Continue** > Name it as **tgt_multiple_sheets** > select required **Linked Service** > Click on **Edit** > provide required schemaname and table name > select **none**
  - Click on **ok**
    ![image](https://user-images.githubusercontent.com/20516321/191257544-6f49fafb-1a42-4a71-92b7-8b1809a462ad.png)


  -   - 
  - 

