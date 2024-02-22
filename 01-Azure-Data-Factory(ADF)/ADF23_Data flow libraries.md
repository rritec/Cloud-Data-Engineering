Note to faculty: take recording and update

# ADF23_Data flow libraries.md

1. Data flow libraries contain custom functions composed using the expression builder.
2. This can be especially helpful if you often find yourself combining functions regularly in your data flows


## Create required source file.
1. create required source excel file asshown below or download from labdata [working Days2.xlsx
](https://github.com/rritec/Cloud-Data-Engineering/blob/main/Lab%20Data/working%20Days2.xlsx)

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/8d0ea6a8-677d-4178-b536-3d6e73aad50c)



## create Data flow libraries Function
1. Click on **Manage** > Click on  **Data flow libraries** > Click on **New**
2. Name it as **rritec** > Click on **New** > Name it as **workingdays**
3. 
4. 



5. add **Derived Column**  transformation and create three calculations as shown below
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

