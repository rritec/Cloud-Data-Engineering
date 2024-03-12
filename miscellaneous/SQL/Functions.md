# Create Functions
``` sql
CREATE OR ALTER FUNCTION CalculateTotalSalary (
@Salary DECIMAL(10, 2), 
@Commission DECIMAL(10, 2)
)
RETURNS DECIMAL(10, 2)
AS
BEGIN
  DECLARE @TotalSalary DECIMAL(10, 2);
  SET @TotalSalary = @Salary + isnull(@Commission,0);
  RETURN @TotalSalary;
END;
```
# test the function
```sql
SELECT dbo.CalculateTotalSalary(5000, 1000) AS TotalSalary;
```
# Use function
``` sql
select empno,ename,sal,comm,
[dbo].[CalculateTotalSalary](sal,COMM) as totalSal from emp;
```
# Question
# Answers
