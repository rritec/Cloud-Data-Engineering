# Transformations in Stored Procedure

1. If you are good with coding do transformations inside stored procedure, that means we do not required dataflows.

## Create Stored Procedure

1. create Stored procedure inside database


```sql
-- Create a table to store the results
CREATE TABLE ResultTable (
    empno INT,
    ename NVARCHAR(255),
    job NVARCHAR(255),
    sal DECIMAL(10,2),
    comm DECIMAL(10,2),
    totalSal DECIMAL(10,2)
);

-- if already procedure available drop it.
DROP PROCEDURE emp_total_sal

-- create procedure
CREATE PROCEDURE emp_total_sal
AS
BEGIN
drop table [dbo].[tgt_emp1]
select empno,ename,sal,comm,sal+isnull(comm,0) as total_sal 
into ResultTable
from emp
END
```
## Call this Stored procedure and verify results
``` sql
-- Call the stored procedure
EXEC emp_total_sal;

-- Check the contents of the ResultTable
SELECT * FROM ResultTable;

```
## Map this stored procedure in ADF

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/34935fa4-9b74-4d0e-ac16-be5def3e95a9)

4. Run and observe it.
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/5833de7f-ac19-4845-803b-82161e952769)

5. 
## Questions
## Answers
