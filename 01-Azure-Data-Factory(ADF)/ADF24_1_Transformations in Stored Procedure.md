# Transformations in Stored Procedure

1. If you are good with coding do transformations inside stored procedure, that means we do not required dataflows.

## Create Stored Procedure

1. create Stored procedure inside database

``` sql
drop table ResultTable;
GO
DROP PROCEDURE CalculateTotalSalAndInsertForAll;
GO

-- Create a table to store the results
CREATE TABLE ResultTable (
    empno INT,
    ename NVARCHAR(255),
    job NVARCHAR(255),
    sal DECIMAL(10,2),
    comm DECIMAL(10,2),
    totalSal DECIMAL(10,2)
);
GO

-- Create the stored procedure
CREATE  PROCEDURE CalculateTotalSalAndInsertForAll
AS
BEGIN        
    DECLARE @p_empno INT;
    DECLARE @p_ename NVARCHAR(255);
    DECLARE @p_job NVARCHAR(255);
    DECLARE @p_sal DECIMAL(10,2);
    DECLARE @p_comm DECIMAL(10,2);
    DECLARE @p_totalSal DECIMAL(10,2);

    -- Declare a cursor to loop through all rows in the emp table
    DECLARE emp_cursor CURSOR FOR
        SELECT empno, ename, job, sal, comm
        FROM emp;

    OPEN emp_cursor;

    -- Fetch the first row
    FETCH NEXT FROM emp_cursor INTO @p_empno, @p_ename, @p_job, @p_sal, @p_comm;

    -- Loop through all rows
    WHILE @@FETCH_STATUS = 0
    BEGIN
        -- Calculate total salary
        SET @p_totalSal = @p_sal + ISNULL(@p_comm, 0);

        -- Insert into the ResultTable
        INSERT INTO ResultTable (empno, ename, job, sal, comm, totalSal)
        VALUES (@p_empno, @p_ename, @p_job, @p_sal, @p_comm, @p_totalSal);

        -- Fetch the next row
        FETCH NEXT FROM emp_cursor INTO @p_empno, @p_ename, @p_job, @p_sal, @p_comm;
    END

    -- Close and deallocate the cursor
    CLOSE emp_cursor;
    DEALLOCATE emp_cursor;
END;


```
2. Call this Stored procedure and verify results
``` sql
-- Call the stored procedure
EXEC CalculateTotalSalAndInsertForAll;

-- Check the contents of the ResultTable
SELECT * FROM ResultTable;

```
3. Map this stored procedure in ADF
  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/34935fa4-9b74-4d0e-ac16-be5def3e95a9)

4. 
