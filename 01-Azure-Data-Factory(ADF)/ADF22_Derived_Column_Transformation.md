# Derived Column Transformation

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/22ecb850-5acc-4e74-91cc-b0252b0a7f18)



## Observe required source table.
``` sql
SELECT * from emp;

```
## create dataflow
1. Click on **New data flow** > name it as **Derived_Column_dataflow**
2. map **source1** as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/10e9a30f-cd5a-4c85-bc61-bd14d2bbc460)



4. add **Derived Column**  transformation and create three calculations as shown below
    1. totalSal
        ``` sql
        SAL+iif(isNull(COMM),toDecimal(0),COMM)
        ```
    2. numberOfDays
        ``` sql
        minus(HIREDATE,toDate(currentTimestamp()))
        ```
    3. numberOfWorkingDays
        ``` sql
        iif(
        or(
	   in( [1, 7],dayOfWeek(HIREDATE)),  /* Sunday or Saturday*/
	   in( [1, 7],dayOfWeek(toDate(currentTimestamp())))      /* Sunday or Saturday*/
        ),
        0,
        minus(toDate(currentTimestamp()), HIREDATE) -
        divide(minus(toDate(currentTimestamp()), HIREDATE) + dayOfWeek(HIREDATE) - dayOfWeek(toDate(currentTimestamp())), 7) * 2 -
        iif(dayOfWeek(toDate(currentTimestamp())) < dayOfWeek(HIREDATE), 2, 0)
        ) +1
   
        ```

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/3a86b308-4ccd-4ec0-b5a9-dd3d1ddd7c9b)


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

