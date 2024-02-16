# UNION Transformation

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/bcf8350f-37ac-4442-8a1b-0839fa982761)


## Create required source tables.
``` sql
SELECT * INTO [dbo].[emp1020] FROM [dbo].[EMP] WHERE DEPTNO in (10,20);

SELECT * INTO [dbo].[emp2030] FROM [dbo].[EMP] WHERE DEPTNO in (20,30);

```
## create dataflow
1. Click on **New data flow** > name it as **exists_dataflow**
2. map **source1** as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c3cd769c-ca61-4102-afcb-415be79f6710)

3. map **source2** as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/2cfca641-1987-4f04-aab4-f2fbbdefbd6e)

4. add **Exists**  transformation

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/6591b3da-2f55-4bab-bcba-8d607781d713)

5. add **sink**

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/f3dfd8a6-9f5a-4329-be28-6e6b82405d92)



## Map dataflow/run pipeline.

6. create new pipeline and Map to pipeline using dataflow activity

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/a4dbfda8-bf39-4780-b762-3afa38c89749)

7. run pipeline

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/8d4fce2e-18b6-4284-8924-19cc8905a3fd)

8. observe output

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/97c8cd47-9c78-40db-92ac-954e8d084fba)

9. 
## Questions
1. Do you know Intersect in SQL?
2. Do you know Except in SQL ?
## Answers
1. observe below sql
  ``` sql
select * from [dbo].[emp1020]
INTERSECT
select * from [dbo].[emp2030]
```
  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/d64385bf-6e46-49be-9fbf-72796d5d4842)

2. Observe below sql
  ``` sql
select * from [dbo].[emp1020]
EXCEPT
select * from [dbo].[emp2030]
```
  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/b00d130b-1481-471b-ba48-e8c447d66bb1)

``` sql
select * from [dbo].[emp2030]
EXCEPT
select * from [dbo].[emp1020]
```
  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/b2ddd342-5c40-4d02-9a03-49104f62da0d)

