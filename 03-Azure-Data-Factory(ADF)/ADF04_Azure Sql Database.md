# Lab 1: Create Free Azure Sql Server and Database
  - Best for modern cloud applications. Hyperscale and serverless
  - Follow this blog for free Azure SQL database [doc](https://learn.microsoft.com/en-us/azure/azure-sql/database/free-offer?view=azuresql)

  ## Lab 2: create one table
  - Open **rritecazuresqldb**
  - Click on **Query Editor(preview)**
  - Under **sql server authentication** > provide **username:** as **saadmin** > **password:** as **RRitec123$**
  - Click on **ok**
  - Create emp,dept and salgrade tables and insert some data by running below code
      ```sql

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

          GO

          CREATE TABLE [dbo].[SALGRADE]
          (GRADE INT NOT NULL,
          LOSAL MONEY,
          HISAL MONEY );

          GO

          INSERT INTO [dbo].[SALGRADE] VALUES (1, 700, 1200);

          INSERT INTO [dbo].[SALGRADE] VALUES (2, 1201, 1400);

          INSERT INTO [dbo].[SALGRADE] VALUES (3, 1401, 2000);

          INSERT INTO [dbo].[SALGRADE] VALUES (4, 2001, 3000);

          INSERT INTO [dbo].[SALGRADE] VALUES (5, 3001, 9999);

          
  - Observe data by runing 
      ``` sql
      select * from emp
      ```
  - ![image](https://user-images.githubusercontent.com/20516321/209278382-d5706988-accb-4f72-add2-5f473a0f774d.png)

## Lab 3: Login and work in SSMS tool
  - Install SSMS tool by following [url]([https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_01_Introduction_Installation.md#instal-sql-server-management-studio-ssms](https://github.com/rritec/POWERBI/blob/master/01.%20Notebooks/PBI_01_01_Introduction_Installation.md))
  - open **rritecAzuresqldb** > copy servername
  - ![image](https://user-images.githubusercontent.com/20516321/209279155-117ad993-851b-4bb2-b732-956579425adc.png)

  - open SSMS tool
  - Provide below information
  - ![image](https://user-images.githubusercontent.com/20516321/209279299-d777b4cd-38e9-4e52-a832-c592d7c1d8a9.png)

  - Click on **Connect**
  - Expand **Databases**
  - Expand **rritecazuresqldb** > Expend **Tables**
  - Right click on **emp** table > click on **select top 1000 rows**
  - ![image](https://user-images.githubusercontent.com/20516321/209279628-efbc9e45-3ceb-431f-8974-8dfb1d27d141.png)

  - observe **query** and **result**
  - ![image](https://user-images.githubusercontent.com/20516321/209279761-0cdbb8b8-8104-4039-9221-72955c9ea239.png)
## Lab 4(optional): Login and work in Azure Data Studio tool
  - Instal Azure Data Studio and explore your own
