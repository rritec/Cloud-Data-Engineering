## Create a simple stored procedure
``` sql
drop procedure GetEmployeeList
```
``` sql
-- Create a simple stored procedure
CREATE PROCEDURE GetEmployeeList
AS
BEGIN
    SELECT ename,job,sal
    FROM Emp
    ORDER BY SAL desc;


SELECT ename,job,sal
    FROM Emp
    ORDER BY SAL
END;
```


``` sql
-- Execute the stored procedure

EXEC GetEmployeeList;
```



## Create a simple stored procedure with parameter

``` sql
drop procedure GetEmployeeList_parmeter
```
``` sql
-- Create a simple stored procedure
CREATE PROCEDURE GetEmployeeList_parmeter
@pDeptno int
AS
BEGIN
    SELECT ename,job,sal,emp.deptno,dname,loc
    FROM Emp inner join dept
	on emp.deptno=dept.deptno
	where emp.deptno = @pDeptno 	
END;
```


``` sql
-- Execute the stored procedure
EXEC GetEmployeeList_parmeter @pDeptno = 20
```

## Create a simple stored procedure with multiple parameters

``` sql
drop procedure GetEmployeeList_parmeter
```
``` sql
-- Create a simple stored procedure
CREATE PROCEDURE GetEmployeeList_parmeter
@pDeptno int,@pJob varchar(255)
AS
BEGIN
    SELECT ename,job,sal,emp.deptno,dname,loc
    FROM Emp inner join dept
	on emp.deptno=dept.deptno
	where emp.deptno = @pDeptno
	and job = @pJob
END;
```


``` sql
-- Execute the stored procedure
EXEC GetEmployeeList_parmeter @pDeptno= 20, @pJob ='CLERK'
```

## Create a simple stored procedure with output parameters 
``` sql
-- Create a stored procedure with output parameter
CREATE PROCEDURE GetEmployeeCount
    @Count INT OUTPUT
AS
BEGIN
    SELECT @Count = COUNT(*)
    FROM Emp;
END;
```


``` sql
-- Execute the stored procedure with output parameter
DECLARE @EmployeeCount INT;
EXEC GetEmployeeCount @Count = @EmployeeCount OUTPUT;
print 'Total number '+ cast( @EmployeeCount AS varchar(255))
```

## Error handling in stored procedure

``` SQL
drop table Employees
```
``` SQL
create table Employees(empno int primary key,ename varchar(255))
```
``` SQL
select * from Employees
```

``` SQL
drop PROCEDURE InsertEmployee
```
``` SQL
-- Error handling in stored procedure
CREATE PROCEDURE InsertEmployee
    @empno int,
    @ename NVARCHAR(50)
AS
BEGIN
    BEGIN TRY
        INSERT INTO Employees (empno,ename)
        VALUES (@empno, @ename);
    END TRY
    BEGIN CATCH
        PRINT 'An error occurred: ' + ERROR_MESSAGE();
    END CATCH
END;
```

``` SQL
EXEC InsertEmployee @empno=101,@ename='RamReddy';
select * from Employees;
EXEC InsertEmployee @empno=102,@ename='John';
select * from Employees;
EXEC InsertEmployee @empno=101,@ename='Myla';
select * from Employees;
```




