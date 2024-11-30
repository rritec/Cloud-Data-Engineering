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

 ![image](https://github.com/user-attachments/assets/e7a482f2-c21a-4711-8ad3-89b72ae29f57)

![image](https://github.com/user-attachments/assets/520e7ad8-62a2-4cbc-81cc-041ff861504a)    

Now we have to Get the required Sub folder **24** using getmetadata Activity output.
 
Drag Foreach activity into the pipeline and name it as Loopforreqyearfolder and give connection with getmeta data activity as per below image

Outside the **foreach** activity in **settings** tab >> select **Squential** and in **items** Click on **add dynamic content** as per below image

![image](https://github.com/user-attachments/assets/b407cf8c-1d45-41b8-89cd-b083b09dd9a2)

After that it will take you to **Pipeline expression Builder** >> Go to **Activity Outputs** and select **getBaseInsideFolders childitems** as per below image

![image](https://github.com/user-attachments/assets/9067848c-99bd-4626-b5f1-8501b7b1827b)

Now inside **foreach** activity, Drag **If Condition** activity to get required **year folder** and Name it as **ifyearFoler**

Go to activities tab and pass the expression dynamically in **expression** value with below logic as per below image

``` ADF
@contains(item().name,pipeline().parameters.pYear)
```
![image](https://github.com/user-attachments/assets/b675139d-1766-490e-a93b-7dcecbdd8ae0)

Inside If condition Activity, if it is **TRUE** drag the **set varaiable** Activity and name it as **VSetYearFolder**

Create one varaiable and name it as **vYearPath** and in below **Value** provide dynamically like **concat** **basefolder** and **year folder** as per below logic and image.

```
@concat(pipeline().parameters.pBasePath,'/',item().name)
```

![image](https://github.com/user-attachments/assets/1751f99d-a1de-4872-b193-d6ecaa878d3a)

Now run the pipeline and **observer** **output**, it will get the **Required Year folder** and it will **concat** with **base folder**

![image](https://github.com/user-attachments/assets/ccdc7d24-90ff-4241-9b0d-9810a6974aab)


![image](https://github.com/user-attachments/assets/b752292c-dc11-4c44-a0bc-f6152a6ea161)

#### How to get Year inside Sub Folders(Month folders)

Drag **GetMetadata** Activity into Pipeline and name it as **getYearInsideFolders**

Create dataset and name it as **ds_rec**

Open **dataset** and create one **parameter** as Per below image.

![image](https://github.com/user-attachments/assets/e9e9ad76-c971-43fe-9c7e-3cabc5c80b88)

Pass **vYearPath** Varaible into **pPath Parameter** as shown in below image.

In **Filedlist** **Arguments** select **ChildItems**

![image](https://github.com/user-attachments/assets/5f04e42b-ef93-447c-ac25-86dc00a3d0ff)

Now you will get all the **Monthfolders** from **24 Year folder** as shown in below image.

![image](https://github.com/user-attachments/assets/8c887815-cdc0-4f29-ae92-2179c5a9ca46)

Now we have to Get the required Sub folder **Max Month Folder** using  getmetadata Activity output(**getYearInsideFolders**).
 
Drag Foreach activity into the pipeline and name it as **loopForReqMonthFolder** and give connection with getmeta data activity as per below image

Outside the **foreach** activity in **settings** tab >> select **Squential** and in **items** Click on **add dynamic content** as per below image

![image](https://github.com/user-attachments/assets/e9653c3c-25db-4b8c-b541-090059fabc5a)

``` ADF
@activity('getMonthInsideFolders').output.childItems
```
Inside If condition Activity, if it is **TRUE** drag the **set varaiable** Activity and name it as **vSetMonthFolder**

Create one varaiable and name it as **vMonthPath** and in below **Value** provide dynamically like **concat** **basefolder** , **year folder** and **Month folder** as per below logic and image

![image](https://github.com/user-attachments/assets/14c10cd4-25e3-4b4c-9e34-40f58b415802)

``` ADF
@concat(variables('vYearPath'),'/',item().name)
```
**Output :**
![image](https://github.com/user-attachments/assets/12bb23c4-3013-40f4-8c29-a2d3cb7daebc)

#### How to get Month inside Sub Folders( folders)

Drag **GetMetadata** Activity into Pipeline and name it as **getYearInsideFolders**

Create dataset and name it as **ds_rec**

Open **dataset** and create one **parameter** as Per below image.















    



















   

    

   

   



   





   

   








