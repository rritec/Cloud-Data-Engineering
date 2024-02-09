# Load file if available

## Step 1: Create a parameter file and read using Lookup activity
1. Open notepad copy below content and save file as json file **ParameterFile1.json** or download the file from our github labdata folder [ParameterFile1.json](https://github.com/rritec/Cloud-Data-Engineering/blob/main/01-Azure-Data-Factory(ADF)/labdata/ParameterFile1.json)
``` json
{
  "srcs_tgts": [
    {
      "ContainerName": "erp",
      "FolderName": "ap",
      "FileName": "emp.csv",
      "SchemaName": "ap",
      "TableName": "tgt_emp"
    },
    {
      "ContainerName": "erp",
      "FolderName": "ar",
      "FileName": "dept.csv",
      "SchemaName": "ar",
      "TableName": "tgt_dept"
    }
  ]
}

```
2. upload this file into **erp** container
  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/3174845d-8cf6-40ac-9cbd-e221c4ee5fce)


3. Create a pipeline with the name of **erp_modules_automation**
4. Drag and drop **lookup Activity** name it as **lookup_to_Read_parameter_file**

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/3979139b-85a6-4058-ab57-066769eab746)

4. Click on **settings** > Click on **New** > select **Azure Blob Storage** > Click on **continue** > Select **JSON** > Click on **Continue** > Name it as **parameter_file_json1** > select storage account Linked Service **ls_for_azure_blob_storage** > browse and select json file

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/a755cd4d-f534-42a0-b3d9-e88581c80924)



5. Click on **Preview data** > observe it.
6. Click on debug and obseve **Lookup Activity** output.
## Step 2: Create a dynamic Source to handle different csv files
1. Click on **New Dataset** > Select **Azure Blob Storage** > Click on **Continue** > Click on **DelimitedText** > Click on **Continue** > Name it is **src_dynamic_csv** > Click on **ok**
   
  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/d4a508a5-822e-48ce-9b99-8689a64e0cf3)

2. Click on **parameters** > define as shown below
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/eaacac2e-5524-4a75-b753-e87a9fb03266)

3. Click on **connection** > and set parameters as shown below
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/da4d9bff-79f3-40b8-ba39-bd0e3d408b81)

4. 
## Step 3: Create a dynamic target to handle different azure sql database tables

1. Click on **New Dataset** > Select **Azure Sal Database** > Click on **Continue** > Name it is **tgt_dynamic** > Click on **ok**
   
2. Click on parameters > create below parameters
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c4193227-f38c-4f84-af5d-950261460c85)

3. Click on **Connections** > provide below parameters
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c00620f5-969b-4866-9554-82c1714319c9)

4. 
## Step 4: finish pipeline
1. Drag and drop **ForEach** Activity
4. Clcik on **settings** > Select **Sequential** > Select **items** as shown below **@activity('read parameterfile').output.firstRow.srcs_tgts**

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/041c49e8-c893-4f0d-8824-7fd52ebd387d)


5. Click on **Activities** > Click on **edit**
6. Drag and drop **Get Metadata** Activity
7. Click on **settings** > map dataset and parameters as shown below
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/84840885-e77e-4535-9f64-8eff67b086a1)

8. Drag and drop **If Condition** activity
9. Connect **Get Metadata** and **If Condition**
10. Configure **if Condition** as shiwn below
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/996fc934-2dac-4d9a-a41a-e10029e5fc89)

11. Click on **true** edit > drag and drop **copy Activity**
12. configure **source** as shown below
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/fec90dd5-36e1-425f-83f2-08f2fafe78e1)

13. Configure **sink** as shown below
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/9770339c-7f59-474d-9ef8-2a732f68f357)

14. Click on debug and observe output.

    
## Questions
## Answers
