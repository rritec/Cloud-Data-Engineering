# DataFlows

1. Mapping data flows are visually designed data **transformations** in Azure Data Factory.
2. Data flows allow data engineers to develop data transformation logic without writing code.
3. The resulting data flows are executed as activities within Azure Data Factory pipelines that use scaled-out Apache Spark clusters.
4. Data flow activities can be operationalized using existing Azure Data Factory scheduling, control, flow, and monitoring capabilities.
5. Mapping data flows provide an entirely visual experience with no coding required.
6. Your data flows run on ADF-managed execution clusters for scaled-out data processing.
7. Azure Data Factory handles all the code translation, path optimization, and execution of your data flow jobs.
8. Reference1 [MSFT Doc](https://learn.microsoft.com/en-us/azure/data-factory/concepts-data-flow-overview)

## Lab

1. Create required tables for our below lab in sqlserver database.
``` sql

CREATE TABLE [dbo].[DEPT]
(DEPTNO INT PRIMARY KEY ,
DNAME VARCHAR(20),
LOC VARCHAR(20) );

GO

INSERT INTO [dbo].[DEPT] VALUES (10, 'ACCOUNTING', 'NEW YORK');

INSERT INTO [dbo].[DEPT] VALUES (20, 'RESEARCH', 'DALLAS');

INSERT INTO [dbo].[DEPT] VALUES (30, 'SALES', 'CHICAGO');

INSERT INTO [dbo].[DEPT] VALUES (40, 'OPERATIONS', 'BOSTON');


CREATE TABLE [dbo].[EMP]
(EMPNO INT PRIMARY KEY,
ENAME VARCHAR(20),
JOB VARCHAR(20),
MGR INT,
HIREDATE DATE,
SAL MONEY,
COMM MONEY,
DEPTNO INT );

GO

INSERT INTO [dbo].[EMP] VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-1980', 800, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-1981', 1600, 300, 30);

INSERT INTO [dbo].[EMP] VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-1981', 1250, 500, 30);

INSERT INTO [dbo].[EMP] VALUES (7566, 'JONES', 'MANAGER', 7839, '2-APR-1981', 2975, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-1981', 1250, 1400, 30);

INSERT INTO [dbo].[EMP] VALUES (7698, 'BLAKE', 'MANAGER', 7839, '1-MAY-1981', 2850, NULL, 30);

INSERT INTO [dbo].[EMP] VALUES (7782, 'CLARK', 'MANAGER', 7839, '9-JUN-1981', 2450, NULL, 10);

INSERT INTO [dbo].[EMP] VALUES (7788, 'SCOTT', 'ANALYST', 7566, '09-DEC-1982', 3000, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-1981', 5000, NULL, 10);

INSERT INTO [dbo].[EMP] VALUES (7844, 'TURNER', 'SALESMAN', 7698, '8-SEP-1981', 1500, 0, 30);

INSERT INTO [dbo].[EMP] VALUES (7876, 'ADAMS', 'CLERK', 7788, '12-JAN-1983', 1100, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7900, 'JAMES', 'CLERK', 7698, '3-DEC-1981', 950, NULL, 30);

INSERT INTO [dbo].[EMP] VALUES (7902, 'FORD', 'ANALYST', 7566, '3-DEC-1981', 3000, NULL, 20);

INSERT INTO [dbo].[EMP] VALUES (7934, 'MILLER', 'CLERK', 7782, '23-JAN-1982', 1300, NULL, 10);

INSERT INTO [dbo].[EMP] VALUES (1234, 'Ram', 'CLERK', 7782, '23-JAN-1982', 1400, NULL, 50);

```

2. Develop a dataflow equal to below query

``` sql

select 
  dname, 
  sum(sal) as total_sal 
from 
  emp, 
  dept 
where 
  emp.deptno = dept.deptno 
  and emp.deptno in (10, 20) 
group by 
  dname 
order by 
  2 asc
  
```

![image](https://user-images.githubusercontent.com/20516321/211307068-69491755-f804-41ad-9abd-f3023d54b7e8.png)

3. Create a new pipeline with the name of **p01_dataflow1**
4. From **Activities** > From **Move & transform** > Drag and drop **Data flow** activity
5. In **General** tab > Type **Name** as **d01_dataflow**
6. Click on **Settings** tab > In **Data flow** Section > Click on **+ New**
7. provide **Name** as **d01_dataflow1**
8. Click on **Add Source**
9. Provide **Output Stream Name** as **SrcEmp**
10. Select **Dataset** as **ds_df_src_emp**

![image](https://user-images.githubusercontent.com/20516321/211466552-1753baf0-4a2c-468d-873c-e1822b73f280.png)

12. Click on another empty **Add Source** drop down > Click on **Add Source**
13. Provide **Output Stream Name** as **SrcDept**
14. Select **Dataset** as **ds_df_src_dept**

![image](https://user-images.githubusercontent.com/20516321/211466976-ad58d71e-dece-432d-869a-0b947af0c7a5.png)

16. Click on **SrcEmp** + icon > add **select** Schema Modifier
17. Provide **Output Stream Name** as **select1Emp**
18. Under **input columns** delete all columns except **deptno** and **sal**

![image](https://user-images.githubusercontent.com/20516321/211467974-52456b35-cca6-4362-b947-09be984c577a.png)

22. Click on **SrcDept** + icon > add **select** Schema Modifier
23. Provide **Output Stream Name** as **selectDept**
24. Under **input columns** delete all columns except **deptno** and **dname**

![image](https://user-images.githubusercontent.com/20516321/211468763-b7bf121b-19b7-4059-93a7-916054c437a6.png)

28. Click on **Select1Emp** + icon > add **filter** row Modifier
29. Click on **Filter on** expression builder > provide expression as ``` DEPTNO == 10 || DEPTNO == 20 ```

30. Click on **filter1** + icon > Select **Join** from **Multiple inputs/outputs**
31. Select **join1** > Select **left stream** as **filter1** > select **right stream** as **select2dept** > join type** as **inner** 
32. Select **Join Conditions** > left and right columns as **DEPTNO**

![image](https://user-images.githubusercontent.com/20516321/211472517-a1c652d1-806e-482d-854f-63c39e65dcdf.png)

34. Click on **Join1** + icon > from **Schema Modifier** select **Aggregate**
35. Under **group by** select **Dname** column
36. Under **Aggregates** > name **column** as **totalsal** > **Expression** as ```sum(SAL)```

![image](https://user-images.githubusercontent.com/20516321/211473271-8cd7c99f-15fd-421e-9cb8-1eec83ddd46f.png)

38. Click on **aggregate1** + icon > From **row modifier** select **Sort**
39. select sort column as **totalsal** and order as **ascending**

![image](https://user-images.githubusercontent.com/20516321/211474756-6c8070ff-0617-4324-852a-1f0a3ba4977a.png)

41. Click on **sort1** + icon > From **destination** select **Sink**
42. select dataset as **tgt_azure_sql_agg**
43. under settings select **table actio** as **recreate table**

![image](https://user-images.githubusercontent.com/20516321/211474483-7a2134c5-2ec2-4af8-af40-c13e3d03d568.png)

42. Click on **debug**
43. observe output

![image](https://user-images.githubusercontent.com/20516321/211707073-7e8b9532-e18e-43ea-ae3b-299c732364f1.png)


![image](https://user-images.githubusercontent.com/20516321/211475778-9a14f8f3-ab70-44ec-bece-5a80af570163.png)





Reference : [Joins](https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_06_Power%20Query%20Editor%20Combine%20Data.md)

# Replicate DataFlows logic in copy activity

1. Create a new pipeline
2. Drag and drop Copy Activity
3. click on the source > create a datasource by pointing sql server
4. provide below query
``` sql

SELECT dept.dname,
       Sum(emp.sal) AS total_sal
FROM   emp,
       dept
WHERE  emp.deptno = dept.deptno
       AND emp.deptno IN ( 10, 20 )
GROUP  BY dname
ORDER  BY 2 DESC 

```
![image](https://user-images.githubusercontent.com/20516321/230277558-39bbd269-d718-455f-bb4a-5df7f1cce3a9.png)

5. click on the sink > create a datasource by pointing sql server
6. run it and observe output
![image](https://user-images.githubusercontent.com/20516321/230277799-9d175d1c-5681-4bad-b47c-61512d134e3c.png)


![image](https://user-images.githubusercontent.com/20516321/230277945-b20663bc-73fa-418d-b659-c9c8bcb75210.png)

7. 
# Split Transformation

Go to **AzureDataFactory(ADF)** > Click on **Author** > Create New Pipeline > Give name as **Pipeline1_Dataflows_split** > Drag **Dataflow Activity** from Activity pane into work area 

![image](https://user-images.githubusercontent.com/20516321/212013537-97dda0ff-95d0-4019-afdc-9a43482ff8bd.png)

Click on Dataflow Activity > Go to settings > Click on New > Give name as **Dataflow_Split** > Click on **Add Source** > Go to **sourceSetting** > Give name as **Source1emp** > Bottom **sourceSetting** > Select **Dataset** as **Src_azure_sql_emp**

![image](https://user-images.githubusercontent.com/20516321/211998478-8cfbf6b0-01eb-438a-89fa-8299e7aa8afa.png)

Click on add symbol > Search for **Conditional split** > Bottom of Conditional split > In split condition > Follow as per below picture

![image](https://user-images.githubusercontent.com/20516321/212001689-83074d4b-26e2-4ea9-abd5-6fa6dc10e8f2.png)

![image](https://user-images.githubusercontent.com/20516321/212001899-fad78590-b9d7-40df-91f4-dd60c7ca90b1.png)

Click on add symbol > search for **Sink** > Give Name as Sink1 > Below sink Create New dataset > Give name as DS_Sink_Emp10 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink_Emp10

![image](https://user-images.githubusercontent.com/20516321/212005400-e1c0d2d0-9a31-4d5c-840f-95934fac6f45.png)

Click on add symbol > search for **Sink2** > Give Name as Sink2 > Below sink Create New dataset > Give name as DS_Sink_emp20 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink2_Emp20

![image](https://user-images.githubusercontent.com/20516321/212005713-a0d70a1f-b9d5-45dc-9e81-056c04eab7df.png)

Click on add symbol > search for **Sink3** > Give Name as Sink3 > Below sink Create New dataset > Give name as DS_Sink_emp30 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink3_emp30

![image](https://user-images.githubusercontent.com/20516321/212005953-57baff49-37af-43a0-af74-d19bd59b060a.png)

Go to **Pipeline1_Dataflows_Split1** > Click on **validate** > Click on **Publish** > Click on **Debug**

![image](https://user-images.githubusercontent.com/20516321/212010636-3e28670e-de15-4f5a-b526-cde00ab9abea.png)

Now Open **SQL SERVER** > Check data of table **[dbo].[Ds_Sink_emp10]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink_emp10]
```
![image](https://user-images.githubusercontent.com/20516321/212011205-8a77c32e-abd4-46b4-9fa2-4d77560f7d34.png)

Check data of table **[dbo].[Ds_Sink2_emp20]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink2_emp20]
```
![image](https://user-images.githubusercontent.com/20516321/212012385-bb3e4013-fb1f-4eb8-9b00-a4ebcaf993cb.png)

Check data of table **[dbo].[Ds_Sink3_emp30]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink3_emp30]
```

![image](https://user-images.githubusercontent.com/20516321/212012706-9c0caf2a-1c16-4470-9f0f-03cd7408acca.png)

# Lookup

[Refer](https://learn.microsoft.com/en-us/azure/data-factory/data-flow-transformation-overview)
