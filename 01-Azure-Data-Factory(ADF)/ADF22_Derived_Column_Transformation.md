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


