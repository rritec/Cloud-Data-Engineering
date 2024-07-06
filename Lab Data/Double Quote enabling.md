# How to Resolve Issues with Commas in CSV File Recordsrecords

## Create CSV file 
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c957f5eb-e1a5-4d0c-95c6-1363ccc9692f)

## Create SQL Table with reqired Columns as in CSV file


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

















