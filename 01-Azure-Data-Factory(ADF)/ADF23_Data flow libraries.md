# ADF23_Data flow libraries.md

1. Data flow libraries contain custom functions composed using the expression builder.
2. This can be especially helpful if you often find yourself combining functions regularly in your data flows


## Create required source file.
1. create required source excel file asshown below or download from labdata 

Hiredate	PayDay	NETWORKDAYS_minus_1	weekday	dayname_using_text_fun
1/1/2024	2/1/2024	23	2	Monday
1/2/2024	2/1/2024	22	3	Tuesday
1/3/2024	2/1/2024	21	4	Wednesday
1/4/2024	2/1/2024	20	5	Thursday
1/5/2024	2/1/2024	19	6	Friday
1/6/2024	2/1/2024	18	7	Saturday
1/7/2024	2/1/2024	18	1	Sunday
1/8/2024	2/1/2024	18	2	Monday
1/9/2024	2/1/2024	17	3	Tuesday
1/10/2024	2/1/2024	16	4	Wednesday
1/11/2024	2/1/2024	15	5	Thursday
1/12/2024	2/1/2024	14	6	Friday
1/13/2024	2/1/2024	13	7	Saturday
1/14/2024	2/1/2024	13	1	Sunday
1/15/2024	2/1/2024	13	2	Monday
1/16/2024	2/1/2024	12	3	Tuesday
1/17/2024	2/1/2024	11	4	Wednesday
1/18/2024	2/1/2024	10	5	Thursday
1/19/2024	2/1/2024	9	6	Friday
1/20/2024	2/1/2024	8	7	Saturday
1/21/2024	2/1/2024	8	1	Sunday
1/22/2024	2/1/2024	8	2	Monday
1/23/2024	2/1/2024	7	3	Tuesday
1/24/2024	2/1/2024	6	4	Wednesday
1/25/2024	2/1/2024	5	5	Thursday
1/26/2024	2/1/2024	4	6	Friday
1/27/2024	2/1/2024	3	7	Saturday
1/28/2024	2/1/2024	3	1	Sunday
1/29/2024	2/1/2024	3	2	Monday
1/30/2024	2/1/2024	2	3	Tuesday
1/31/2024	2/1/2024	1	4	Wednesday


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
        ``` json
        minus(HIREDATE,toDate(currentTimestamp()))
        ```
    

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/b34b1527-bf62-4e44-aa7e-b8c59a9165e8)



5. add **sink**

## Map dataflow/run pipeline.

6. create new pipeline and Map to pipeline using dataflow activity
7. run pipeline
8. observe output
   
## Questions

1. Do you know `days` function and `networkdays.intl` in excel ?

## Answers

1. Observe it . ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/efe92fe9-20b4-4ebd-a624-a1e0115982a1)

