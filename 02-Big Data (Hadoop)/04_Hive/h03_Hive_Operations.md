# Hive Operations

1. Add comment to Database
``` sql
create database rritec comment "big data training by rritec";
```
2. observe comment
``` sql
describe database rritec;
```
![image](https://user-images.githubusercontent.com/20516321/215237182-d8c405fd-06db-40df-b33e-b80ed0591526.png)

3. Add comment to Table and columns
``` sql 
create table emp(empno int comment "employee number",ename string,sal int) comment "it is a test table" row format delimited fields terminated by '|';
```
4. observe comments
``` sql
desc formatted emp;
```
![image](https://user-images.githubusercontent.com/20516321/215237826-fca28300-2f1f-4e6e-b746-fc6ad1bdbfb7.png)

5. Load data into table in **append** mode
``` sql
load data local inpath '/home/cloudera/Desktop/rritec/emp.txt' into table emp;
```
``` sql
select * from emp;
```
``` sql
load data local inpath '/home/cloudera/Desktop/rritec/emp.txt' into table emp;
```
``` sql
select * from emp;
```
![image](https://user-images.githubusercontent.com/20516321/215381506-a2accaf4-2f1f-4585-b7c9-c64d14bcdd5c.png)

6. Load data into table in **overwrite** mode
``` sql
load data local inpath '/home/cloudera/Desktop/rritec/emp.txt' overwrite into table emp;
```
``` sql
select * from emp;
```
![image](https://user-images.githubusercontent.com/20516321/215381867-0487dc9a-da86-47e6-a581-2784c6eb354a.png)

7. Truncate internal tables
``` sql
truncate table emp;
```
![image](https://user-images.githubusercontent.com/20516321/215382081-1b6fb79c-68f7-41ea-bbcc-dd5cc77e415c.png)

8. Truncate external tables
``` sql 
create external table if not exists emp(empno int comment "employee number",ename string,sal int) comment "it is a test table" row format delimited fields terminated by '|';
```
``` sql
desc formatted emp;
```
``` sql
load data local inpath '/home/cloudera/Desktop/rritec/emp.txt' overwrite into table emp;
```
``` sql
select * from emp;
```
``` sql
truncate table emp;
```


10. drop database without tables
``` sql
drop database rritec;
```
11. drop database with tables
``` sql
drop database rritec cascade;
```
``` sql
show databases;
```
![image](https://user-images.githubusercontent.com/20516321/215387074-443dce60-1ce4-4208-9bbd-d53469f16c30.png)

12. Observe Default hive execution engine
    1. There are three execut engines available
    2. those are
        1. MR > Map Reduce (default Execution Engine)
        2. TeZ
        3. Spark > Most of the times we will use this in projects
``` sql
SET hive.execution.engine
```

13. Change Default hive execution engine

``` sql
SET hive.execution.engine=spark
```
