# UNION Transformation

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/b591a580-22a1-445c-9b1b-759025b66050)



## Create required source tables.
``` sql
SELECT * INTO [dbo].[emp1020] FROM [dbo].[EMP] WHERE DEPTNO in (10,20);

SELECT * INTO [dbo].[emp2030] FROM [dbo].[EMP] WHERE DEPTNO in (20,30);

```
## create dataflow
1. Click on **New data flow** > name it as **union_dataflow**
2. map **source1** as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c3cd769c-ca61-4102-afcb-415be79f6710)

3. map **source2** as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/2cfca641-1987-4f04-aab4-f2fbbdefbd6e)

4. add **union**  transformation

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/b482f995-f3a1-4550-b0a1-7438a120f557)


5. add **sink**

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/f3dfd8a6-9f5a-4329-be28-6e6b82405d92)



## Map dataflow/run pipeline.

6. create new pipeline and Map to pipeline using dataflow activity

  

7. run pipeline

  

8. observe output

  

9. 
## Questions
1. Do you know UNION in SQL?
2. Do you know UNION ALL in SQL ?
## Answers
1. observe below sql
  ``` sql
select * from [dbo].[emp1020]
UNION
select * from [dbo].[emp2030]
```
  

2. Observe below sql
  ``` sql
select * from [dbo].[emp1020]
UNION ALL
select * from [dbo].[emp2030]
```
 

