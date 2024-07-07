# How to Resolve Issues with Commas in CSV File Records

## Create CSV file 

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c957f5eb-e1a5-4d0c-95c6-1363ccc9692f)

## Create SQL Table with reqired Columns as in CSV file

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/44858a68-f56a-4084-b3fb-1b14642f30f1)


## Upload the CSV file into Azure Blob

- Go to **Storage Account**>> Click on **Blob Service**

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/d32fae77-b8de-4374-8daf-0efa3ac03d5a)

## Create Container

- Click on **Container** >> Give name as rritec
  
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/e253a5bf-0ced-41b3-94e4-5df327e22146)

- Open rritec container and Upload the CSV file.
  
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/d52a94b2-ffe3-452a-bead-36d1ebd52783)

- Uploaded file in blob Successfully
  
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c749c97c-7c3e-4373-a0fb-7cc59cf83a33)

## How to Create a pipeline

 - Go to **Datafactory**
   
 - Create New **Source dataset** >> Search for **Azure BLOB Storage** >>click on **Continue**
   
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c1ac7b8a-08e3-4100-aaac-fc093d8452be)

- Click on **Delimeted Text** >> click on **continue**
  
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/9611e69a-6a68-4bd2-b187-a0aa8e3361cc)

- In **Set properties** >> Give Source dataset name as **SRC_DQ** >> Select the Required **Linked serveice** >> Click on OK
  
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/bfca6b46-be31-4635-8b1e-6b5eddd2f0af)
- Go to connection
  
- In **Quote Character** >> select Double Qoute (")
  
- In **Escape Character** >> select Double Qoute (") as below Image
  
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/82964d95-af53-48ba-93f9-c50e43ae77fc)

 - Create New **Target dataset** >> Search for **Azure SQL DataBase** >>click on **Continue**

 - ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/18f9a6a7-1fec-42c7-a4a3-3b7cde018b4a)

 - In **Set properties** >> Give Source dataset name as **trg_DQ** >> Select the Required **Linked serveice** >> Click on OK

 - ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/739407e8-eaf7-40a5-a914-b7e92aade749)

 - Click on **Pipelines** >> **New Pipeline** >> Provide name as **Enabling Double Quotes** shown in below Images

 - ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/2a9d6518-2a5c-4c44-9a24-666bb706e5cf)

 - ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/6ca670ac-15a9-45a5-b47a-20b1a7ba8d63)

 - Drag **Copy data Activity** to Workplace

 - ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/216b0036-d1e9-4151-b72e-3386fc350f75)

 - Provide the **Source datset** in **Copy data Activity** which we created earlier as **src_DQ**

 - ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/1a69e7d5-6ac1-4e75-a0a6-336a5de258b7)

 -  Provide the **Target datset** in **Copy data Activity** which we created earlier as **trg_DQ**

 -  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/a2bf51a3-f4c1-47b7-9437-ef7ff7fbd0ec)

 -  Click on **Debug** button

 -  Observe **Output**

 -  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/7d147728-7db4-4aa7-892e-c391310d31f1)

 -  Test Output in **Azure SQL Database**

 -  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/518c6db6-3691-4151-9284-74f1ac21944a)


























