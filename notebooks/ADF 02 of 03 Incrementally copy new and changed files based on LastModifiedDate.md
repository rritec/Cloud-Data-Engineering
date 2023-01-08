Ref: https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-lastmodified-copy-data-tool

# Use the Copy Data tool to create a pipeline.

1. Open Azure Data Factory > home page > Click on **Ingest tile** to open the Copy Data tool.

![image](https://user-images.githubusercontent.com/20516321/211182064-86b55df4-95b9-44ca-9ff8-e7162326c7f3.png)

2. Click on **Properties** > Select Task type as **Built-in Copy task** > Below Task select **Schedule** > In start date (UTC) select date and time.

  * In **start date (UTC)** select date and time > In **Recurrence** set refreshing Time > Click **Spicfy** an end date radio button > **End On (UTC)** > Select end date 
    of Refreshing (Or) Scheduling.

![image](https://user-images.githubusercontent.com/20516321/211182803-c63e1318-5a10-4f3b-bb7f-7b833a5507d9.png)

3. Select **Source Type** as ALL > **connection** as **IS_blob_dec22** > **File Folder** > Click on **Browse** > Root Folder > click on **Sourcedec22** > click on ok.
   * Below **File or Folder** > Options > Click On **File loading behaviour** Drop Down > Selcect **Incremental load: LastModifiedDate** > Observe **ParameterValues**. 
   * Select **Binary Copy**.
   * Select **Recursively**
   * Click on next.

![image](https://user-images.githubusercontent.com/20516321/211183601-a5c0e277-1e6b-4216-90c0-dc25fb8d5326.png)


4. Select **Destination Type** as ALL > **connection** as **IS_blob_dec22** > **File Folder** > Click on **Browse** > Root Folder > click on **destinationdec22**.
   * File (or) Folder path > Paste in path **destinationdec22/{year}/{month}/{day}/{hour}/{minute}** then below folder path you can see Yea, month and day Format.
   * Click on **Year** format Drop down > Select **YY** (or) You Can take any format as per your requirement.
   * Click on **Month** format Drop down > Select **MM** (or) You Can take any format as per your requirement.
   * Click on **Day** format Drop down > Select **DD** (or) You Can take any format as per your requirement.
   * Click on Next.

![image](https://user-images.githubusercontent.com/20516321/211186208-35580b73-b829-4701-a0f5-3ccec5efb99d.png)


5. In setting > Give **Task name** as **CopyPipeline_u7w_dec22** > Click on Next.

![image](https://user-images.githubusercontent.com/20516321/211186311-af922da6-d3e4-45b8-ace0-b379267107c3.png)


6. After Settings > **Review and finish** > Summary > Click on next > observer below Picture.

![image](https://user-images.githubusercontent.com/20516321/211186454-5b4b2996-8b24-4c49-ae6f-6f5aecb45392.png)

7. Deployement > Click on Moniter.

![image](https://user-images.githubusercontent.com/20516321/211186807-2c852e48-0c37-45b4-8a03-791c0a8cf58a.png)

8. clicK on **Author** > Expand **Pipelines** > Drag Created Pipeline **CopyPipeline_u7w_dec22**.

![image](https://user-images.githubusercontent.com/20516321/211186922-fc7e8b9c-a902-42fd-9731-a8a40c566030.png)


















