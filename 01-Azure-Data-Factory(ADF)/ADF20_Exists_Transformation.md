# Exists Transformation

## Create required source tables.
``` sql
SELECT * INTO [dbo].[emp1020] FROM [dbo].[EMP] WHERE DEPTNO in (10,20);

SELECT * INTO [dbo].[emp2030] FROM [dbo].[EMP] WHERE DEPTNO in (20,30);

```
## create dataflow
## Map dataflow/run pipeline.
