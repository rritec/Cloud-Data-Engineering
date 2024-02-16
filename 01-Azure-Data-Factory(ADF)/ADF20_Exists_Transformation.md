# Exists Transformation

## Create required source tables.
``` sql
SELECT * INTO [dbo].[emp1020] FROM [dbo].[EMP] WHERE DEPTNO in (10,20);

SELECT * INTO [dbo].[emp2030] FROM [dbo].[EMP] WHERE DEPTNO in (20,30);

```
## create dataflow
1. Click on **New data flow** > name it as **exists_dataflow**
2. map **source1** as shown below
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c3cd769c-ca61-4102-afcb-415be79f6710)

3. 
## Map dataflow/run pipeline.
## Questions
## Answers
