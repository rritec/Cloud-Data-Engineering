# Incrementally load data

1. ![image](https://user-images.githubusercontent.com/20516321/209805592-c0bd3d78-968b-48f8-bdac-f715f11ab663.png)
2. ![image](https://user-images.githubusercontent.com/20516321/229040491-9d803caf-5e67-4997-a25c-72e8527a775c.png)




**Step 1: Create a data source/watermark/stored procedure in your SQL database**

1.  Open SSMS > Run the following SQL command against your SQL database to create a table named as **src_incr_emp** and load **5** records

``` sql

    create table src_incr_emp
    (
        empid int,
        ename varchar(255),
        hiredate datetime
    );
    
    GO

    INSERT INTO src_incr_emp
        (empid, ename, hiredate)
    VALUES
        (1, 'Myla RamReddy','9/1/2020 12:56:00 AM'),
        (2, 'Anam Tarun','9/2/2020 5:23:00 AM'),
        (3, 'John','9/3/2020 2:36:00 AM'),
        (4, 'Mark','9/4/2020 3:21:00 AM'),
        (5, 'Nancy','9/5/2020 8:06:00 AM');

```
2.  Create another table in your SQL database to store the **last load date** value

``` sql

    create table watermarktable
    (

    TableName varchar(255),
    last_load_date datetime,
    );

```
3.  Set the default value of the high watermark with the table name of target data store.

``` sql

    INSERT INTO watermarktable
    VALUES ('tgt_incr_emp','1/1/1900 12:00:00 AM')

```
4.  Observe the data

``` sql

    select * from watermarktable

```
5. Create a stored procedure in your SQL database

``` sql

    CREATE PROCEDURE sp_write_watermark @LastLoadDate datetime, @TableName varchar(50)
    AS

    BEGIN

    UPDATE watermarktable
    SET [last_load_date] = @LastLoadDate
    WHERE [TableName] = @TableName

    END

```
**Step 2: Get last load date**

1. Create a pipeline with the name **po6_IncrementalCopy**
2. Drag and drop the **Lookup** activity to the pipeline designer surface.
3. Change the name of the activity to **Get_last_load_date**
4. Click on **Settings** tab > click **+ New** for Source Dataset > Click on **Azure SQL Database**
5. Name it as **ds_WatermarkDataset**
6. Select Linked Service of **Azure SQL Database**
7. Select **Table Name** as **dbo.watermarktable**
8.  Click on **ok**
9.  select **Use query** as **Query**
10.  provide below query

``` sql

select * from [dbo].[watermarktable] 
where [TableName] ='tgt_incr_emp'

```
![image](https://user-images.githubusercontent.com/20516321/229045771-d11f564a-6b0f-4ec5-88d1-106385cc0b55.png)


**Step 3: Get_max_transaction_date_from_source**

1. Drag and drop one more lookup into work area
2. Name it as **Get_max_transaction_date_from_source**
3. Clcik on **Settings** tab > click **+ New** for Source Dataset > Click on **Azure SQL Database**
5. Name it as **ds_src_incr_emp**
6. Select Linked Service of **Azure SQL Database**
7. Select **Table Name** as **dbo.ds_src_incr_emp**
8.  Click on **ok**
9.  select **Use query** as **Query**
10.  provide below query

``` sql

select max(hiredate) as max_hiredate 
from [dbo].[src_incr_emp]

```
![image](https://user-images.githubusercontent.com/20516321/229046242-c9965e63-d216-41db-a5e5-d69730495286.png)

**Step 4: Copy data Incrementally**

1.  Drag and drop the **Copy Data** activity to the pipeline designer surface.
2.  Connect **both lookups** to **Copy Data** activities
3.  Select **Copy Data** activity > Click on **Source**
4.  select **Source Dataset** as **ds_src_incr_emp**
5.  Select **Use Query** as **Query**
6.  Provide **Query** as 

``` sql

select *  
from [dbo].[src_incr_emp]
where 
hiredate > '@{activity('Get_last_load_date').output.firstRow.last_load_date}'
and hiredate <= '@{activity('Get_max_transaction_date_from_source').output.firstRow.max_hiredate}'

```
![image](https://user-images.githubusercontent.com/20516321/229047115-83b2cbd8-97ad-4cad-9c32-1a2cf7265f04.png)

7. Click on **Sink** > Click on **New** > Select **Azure SQL Database** > Click on **Continue**
8. Provide **Name** as **ds_tgt_incr_emp**
9. select **Linked Service** as **Azure SQL Database**
10. Click on **ok**
11. select **table option** as **auto create table**

![image](https://user-images.githubusercontent.com/20516321/229048946-5a3d9693-fa99-4141-ba4c-a63b0d35cdfa.png)


**Step 5: Update Last Load Date using Stored Procedure Activity**

1. Drag and drop **Stored Procedure** activity to the pipeline designer surface.
2. **Name** as **update_last_load_date**
3. Select **linked Service** as **ls_sqlserver**
4. Select **Stored Procedure Name** as **[dbo].[sp_write_watermark]**
5. Under **Stored Procedure Parameters** > Click on **Import**
6. Select **LastLoadDate** value as **@activity('lookup_get_max_date_from_source').output.firstRow.max_date**
7. Select **TableName** value as **@activity('Lookup_last_load_date').output.firstRow.tablename**

![image](https://user-images.githubusercontent.com/20516321/229049854-49c94a7a-f401-464c-9e31-662ffaf4aa54.png)

**Step 6: Run and observe steps**

1. Click on **debug** > observe run steps

![image](https://user-images.githubusercontent.com/20516321/229049992-c4c25531-63ca-46fe-a13e-2a7d34b273b8.png)

**Step 7: Run one more time by adding few rows and observe steps**

1. Insert two records 

``` sql

INSERT INTO src_incr_emp
VALUES (6, 'geo','9/6/2020 2:23:00 AM')

INSERT INTO src_incr_emp
VALUES (7, 'albert','9/7/2020 9:01:00 AM')

```
2. Click on **debug** > observe run steps


# Incremental copy multiple tables
Ref: Follow MSFT [doc](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-multiple-tables-portal)
# Incremental copy lastmodified copy data tool
Ref: Follow MSFT [doc](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-lastmodified-copy-data-tool)
# Incremental copy partitioned file name copy data tool
Ref: Follow MSFT [doc](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-partitioned-file-name-copy-data-tool)

Correction: 
Select LastLoadDate value as @activity('lookup_get_max_date_from_source').output.firstRow.max_date
It should be max_hiredate
