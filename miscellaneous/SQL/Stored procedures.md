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



