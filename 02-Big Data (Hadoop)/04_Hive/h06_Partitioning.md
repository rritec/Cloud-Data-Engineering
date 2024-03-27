# Partitioning

1. Partitioning is the `optimization technique` in Hive which improves the `performance` significantly
2. Apache Hive organizes tables into partitions. Partitioning is a way of dividing a table into related parts based on the values of particular columns like `date`, `city,` and `department`

![image](https://user-images.githubusercontent.com/20516321/216234868-7f22531c-1108-4cbd-9203-cc7f7e0ebf68.png)

3. To create data partitioning in Hive the syntax is
``` sql
CREATE TABLE table_name (column1 data_type, column2 data_type) PARTITIONED BY (partition1 data_type, partition2 data_type,….);
```

4. Types of Hive Partitioning

    1. Static Partitioning
    2. Dynamic Partitioning

## Static Partitioning

1. Insert input data files individually into a partition table is Static Partition.
2. Usually when loading files (big files) into Hive tables static partitions are preferred.
3. Static Partition saves your time in loading data compared to dynamic partition.
4. You “statically” add a partition in the table and move the file into the partition of the table.
5. We can alter the partition in the static partition.
6. You can get the partition column value from the filename, day of date etc without reading the whole big file.
7. You can perform Static partition on Hive `Manage` table or `external` table.
10. create table
    ``` sql
    create table emp_partition(empno int,ename string,sal int) partitioned by(deptno int) row format delimited fields terminated by '|' ;
    ```
    ``` sql
    desc formatted emp_partition;
    ```
    ``` sql
    load data local inpath '/home/cloudera/Desktop/rritec/emp10.txt' into table emp_partition partition(deptno=10);
    ```
    ``` sql
    select * from emp_partition;
    ```
    ``` linux
    hdfs dfs -ls /user/hive/warehouse/rritec.db/emp_partition/deptno=10/
    ```
    ``` sql
    load data local inpath '/home/cloudera/Desktop/rritec/emp20.txt' into table emp_partition partition(deptno=20);
    ```
    ``` sql
    desc formatted emp_partition;
    ```
    ``` sql
    select * from emp_partition;
    ```
    ``` linux
    hdfs dfs -ls /user/hive/warehouse/rritec.db/emp_partition/deptno=20/
    ```
    ``` linux
    show partitions emp_partition;
    ```
    
11. 
## Dynamic Partitioning

1. Single insert to partition table is known as a dynamic partition.
2. Usually, dynamic partition loads the data from the non-partitioned table.
3. Dynamic Partition takes more time in loading data compared to static partition.
4. When you have large data stored in a table then the Dynamic partition is suitable.
5. If you want to partition a number of columns but you don’t know how many columns then also dynamic partition is suitable.
6. we can’t perform alter on the Dynamic partition.
7. You can perform dynamic partition on hive external table and managed table.
8. If you want to use the Dynamic partition in the hive then the mode is in `nonstrict` mode.
9. lab
    1. change hive properties
    ``` sql
    set hive.exec.dynamic.partition.mode=nonstrict;
    ```
    2. create staging table and load data
    ``` sql
    create table emp_dp_stage(empno int,ename string,sal int,deptno int) row format delimited fields terminated by '|' ;
    ```
    ``` sql
    load data local inpath '/home/cloudera/Desktop/rritec/emp1020.txt' into table emp_dp_stage;
    ```
    
    
    3. Create final table and load data
    ``` sql
    create table emp_dp(empno int,ename string,sal int) partitioned by(deptno int) row format delimited fields terminated by '|' ;
    ```
    ``` sql
    insert into emp_dp partition(deptno) select empno,ename,sal,deptno from emp_dp_stage;
    ```
    ```linux
    hdfs dfs -ls /user/hive/warehouse/rritec.db/emp_dp/
    ```
    
    
    
    4. 
10.
## Questions
1. how to do pratition based on multiple columns ?
## Answers
1. run below scripts and observe it.
``` sql
create table emp_dp2(ename string,sal int) partitioned by(deptno int,empno int) row format delimited fields terminated by '|' ;
```
``` sql
insert into emp_dp2 partition(deptno,empno) select ename,sal,deptno,empno from emp_dp_stage;
```
``` linux
hdfs dfs -ls -R /user/hive/warehouse/b2403.db/emp_dp2
```
Note: Do make sure that the column on which you want to partition should come last in select statements. If there are series of column then there order in partition(deptno,empno) should match in select statement.
2. 
