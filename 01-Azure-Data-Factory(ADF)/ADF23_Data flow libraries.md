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
3. Create two arguments **i1 and i2 with datatype as date** as shown below and paste below code

``` sql
/*
i1:date = Initial date
i2:date = End date
*/
size(
 filter(
 mapLoop(
 toInteger(i2 - i1), 
 toString(addDays(i1, toInteger(#index)))
 ),
 not(in([1, 7], dayOfWeek(toDate(#item))))
 )
)
```

 ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/4717bcab-36a6-4b78-8771-4825790e2ca6)

4. Click on **save**

 ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/77a2be8c-8d77-4d3a-aefe-2ed50bb5c181)

5. 

## create Data flow

1. Create new dataflow name it as **dataflow_workingdays**
2. Click on down arrow mark > click on **add source** ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/1086b418-f9ed-4f06-8fc6-f5d596c66999)
3. Click on new > select blob > select excel and create datasource as shown below

   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/8298e33a-956e-4c25-a808-94a0017e6e62)

   
4. Click on source **Projection** tab
5. change datatypes of hiredate and paydate as shown below

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/0fd5776d-d9d4-41fe-b83f-7367c084acdb)

6. 
7. add **Derived Column**  transformation and create calculations as shown below
    1. workingDays
       
       ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/d1a0ff4e-6b3c-4c9b-b643-ba76e3f581c7)

    3. 
        ``` sql
        SAL+iif(isNull(COMM),toDecimal(0),COMM)
        ```
    4. numberOfDays
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

