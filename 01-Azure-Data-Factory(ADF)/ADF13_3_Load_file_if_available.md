# Load file if available

## Step 1: Create a parameter file
``` json
[
{
"ContainerName":"cdrive",
"FolderName":"input",
"FileName":"dept1.csv",
"SchemaName":"dbo",
"TableName":"tgt_dy_dept"
},
{
"ContainerName":"cdrive",
"FolderName":"input",
"FileName":"emp1.csv",
"SchemaName":"dbo",
"TableName":"tgt_dy_emp1"
}
]

```

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
## Step 4: Create a pipeline
1. Create a pipeline with the name of **ADF13_3_Load_file_if_available**
2. Create a parameter as shown below and paste above code

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/3750c094-b6ad-4026-b23c-e2044c978235)

3. Drag and drop **ForEach** Activity
4. Clcik on **settings** > Select **Sequential** > Select **items** as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/cca1ce23-fb4c-42ed-80d0-30b52bc679e0)

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
