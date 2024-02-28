## Create a simple stored procedure
``` sql
drop procedure GetEmployeeList
```
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


-- Execute the stored procedure

EXEC GetEmployeeList;



## Create a simple stored procedure with parameter

drop procedure GetEmployeeList_parmeter
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


-- Execute the stored procedure
EXEC GetEmployeeList_parmeter @pDeptno = 20------can i pass more than 1 value with in one parameter

## Create a simple stored procedure with multiple parameters

drop procedure GetEmployeeList_parmeter
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


-- Execute the stored procedure
EXEC GetEmployeeList_parmeter @pDeptno= 20, @pJob ='CLERK'

## Create a simple stored procedure with output parameters 
-- Create a stored procedure with output parameter
CREATE PROCEDURE GetEmployeeCount
    @Count INT OUTPUT
AS
BEGIN
    SELECT @Count = COUNT(*)
    FROM Emp;
END;


-- Execute the stored procedure with output parameter
DECLARE @EmployeeCount INT;
EXEC GetEmployeeCount @Count = @EmployeeCount OUTPUT;
print 'Total number '+ cast( @EmployeeCount AS varchar(255))



