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
## Step 3: Create a dynamic target to handle different azure sql database tables
## Step 4: Create a pipeline
1. Create a pipeline with the name of **ADF13_3_Load_file_if_available**
2. Create a parameter as shown below and paste above code

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/3750c094-b6ad-4026-b23c-e2044c978235)

3. Drag and drop **ForEach** Activity
4. Clcik on **settings** > Select **Sequential** > Select **items** as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/cca1ce23-fb4c-42ed-80d0-30b52bc679e0)

5. Click on **Activities** > Click on **edit**
6. Drag and drop **Get Metadata** Activity
7. 
## 
