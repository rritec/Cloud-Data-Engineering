# How to Load the data from Recursive Folders :

## INTRODUCTION :

I am attempting to retrieve files from four levels of folders within Azure Blob Storage and copy all the data files into an Azure SQL Database, as per the below screen shots.

### Step : 1

1. I Need to get the files from **Inside** **Input Folder** as per below screen shot.

    ![image](https://github.com/user-attachments/assets/9b2d70a3-e227-426f-9ab6-198ef9eb040a)

### Step : 2

1. Again, I have to get the files from **24** **folder** inside the **inputfolder** as per below screen shot
   
    ![image](https://github.com/user-attachments/assets/bfba57e5-8ea0-45c1-b53e-52c62d097944)

### Step : 3

1.  Again, I have to get the files from **11** **folder** inside the **24 folder** as per below screen shot.

    ![image](https://github.com/user-attachments/assets/034625ff-ee1e-474c-a47d-01f32c41ef70)
    
### Step : 4 

1.  Again, I have to get the files from **19** **folder** inside the **11 folder** as per below screen shot.

   ![image](https://github.com/user-attachments/assets/3c60382b-40ae-46be-a4ac-32ea6c519733)

### Step : 5 

1. Again, I have to get the file from **file2.csv** inside the **11 folder** as per below screen shot.

![image](https://github.com/user-attachments/assets/75f2ce6f-7bd3-4cd1-8245-82eb34f823fd)


## How to create pipeline to get files recursively as per above screen shots.



Create **Parameters** outside the pipeline as per below screen shot.

 ![image](https://github.com/user-attachments/assets/ecb251ec-bf82-4771-8d99-ebbb07cf8ccb)

Drag **GetMetadata** Activity into **Pipeline** and name it as **getBaseInsideFolders**

Create **dataset** and name it as **ds_rec**

Open dataset and create one parameter as Per below image

![image](https://github.com/user-attachments/assets/d5630731-e100-4bc3-a02a-d3b98d9ad7cd)

Now go to dataset **settings** and pass the **parameter** in **dataset properties** **Value**

Click on **Value** then it will take you to **Pipeline expression Builder**

In pipeline expression builder click on Parameters tab below and select **pBasePath** Parameter (which we created outside pipeline) as per below image

![image](https://github.com/user-attachments/assets/36dce897-50a3-430d-9fad-aa5de73b8e97)

Click On **Ok** then screen looks like with **passing parameter** in **value tab**

![image](https://github.com/user-attachments/assets/dcc889db-951f-444a-9508-8924a00a67ba)

In **FiledLists**  **Arguments** select **Child Items** as per below Image

![image](https://github.com/user-attachments/assets/a41e8358-c129-4a3f-8d40-55a05c85dd5f)

Run the **activity** and check the **output** you will get the **sub folders**(Child items) from inside the **Imput** floder

![image](https://github.com/user-attachments/assets/520e7ad8-62a2-4cbc-81cc-041ff861504a)     ![Uploading image.png…]()











   

    

   

   



   





   

   








