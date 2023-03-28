# Hadoop(BigData)(Hive)
1. **[Hive Metastore](#Hive-Metastore)**<br>
2. **[Hive Managed Tables](#Hive-Managed-Tables)**<br>
3. **[Hive External Tables](#Hive-External-Tables)**<br>
4. **[Hive Operations](#Hive-Operations)**<br>
5. **[Hadoop File Formats and its Types](#Hadoop-File-Formats-and-its-Types)**<br>
6. **[Different ways to connecting hive](#Different-ways-to-connecting-hive)**<br>
7. **[Partitioning](#Partitioning)**<br>
9. **[Bucketing](#Bucketing)**<br>
10. 



# Hive Metastore

1. Connect to hive cli
    1. type ```hive```
    2. type ```show databases;```
    3. type ```create database rritecdb```
    4. desc rritecdb;
        
        ![image](https://user-images.githubusercontent.com/20516321/214228819-f9f120ef-2280-4dd5-9318-8d2f797e7cae.png)

    5. How system knows to create folder in ```/user/hive/warehouse/```
    6. type ```SET;``` observe warehouse location property. using this set property system knows the location of warehouse
    7. The property name is `hive.metastore.warehouse.dir=/user/hive/warehouse`
    8. creating one database is nothing but creating a folder inside HDFS location `/user/hive/warehouse`
2. can we run hive commands from terminal
    1. Yes
    2. In normal terminal type ```hive -e "show databases;"```
    3. also observe ```"hive -e set;" | grep warehouse```
        
        ![image](https://user-images.githubusercontent.com/20516321/214229607-49d7673b-0eef-4818-ab04-001ab46455de.png)

3. Metadata is adata about data. examples of metadata database names,tablenames,column names,...etc
4. All metadata stored in separate database known as metastore. 
5. hive-site.xml configuration file has metastore database information
    1. open terminal ```cd /etc/hive/conf/```
    2. type ```cat hive-site.xml | grep metastore```
    3. observe metastore database as mysql
6. Connect to mysql(Metastore)
    1. open terminal > type ```mysql -uroot -pcloudera```

        ![image](https://user-images.githubusercontent.com/20516321/214223593-bffe40ce-a79c-41e7-8baa-414e8cef7c36.png)

    2. type ```show databases;```

        ![image](https://user-images.githubusercontent.com/20516321/214224728-8d6d2333-0f35-49f1-aebd-b038fc02f822.png)

    3. type ```use metastore;```
    6. type ```select * from DBS;```
  
        ![image](https://user-images.githubusercontent.com/20516321/214237910-5cba6910-c977-4e6b-b275-c48f4e236c04.png)
5. `info:`do you know we can clear the `hive cli` by using `ctrl +   L` or `!clear`

# Hive Managed Tables
1. Hive Tables are two types
    1. Managed Tables or Internal Tables
    2. External Tables or Non Managed Tables
3. **Create managed table or internal table**
    1. Open terminal ```type hive```
    2. create table using below script
    
        ``` sql 
        Create table if not exists emp (empno int,ename string,sal int) rows delimited fields terminated by ',';
        ```
    3. Observe Schema of table

        ``` sql
        describe emp;
        ```
        ``` sql
        desc emp;
        ```
        ``` sql
        desc formatted emp;
        ```
    4. Observe data
        ``` sql
        select * from emp;
        ```
    5. load data from **file** into **table**
        1. In linux desktop > right click open terminal
        2. create a file `vi emp.txt`
        3. enter data
            ``` 
            101,ram,1000
            102,john,2000
            103,marc,3000
            ```
            
        3. type `:wq!`
        4. Copy file from linux to hadoop `hdfs dfs -put -f /home/cloudera/Desktop/emp.txt /user/cloudera/`
        5. in hive terminal type 
            ``` sql
            load data inpath '/user/cloudera/emp.txt' into table emp;
            ```
        6. the file '/user/cloudera/emp.txt' available in this location?
            - No
        7. observe data
            ``` sql 
            select * from emp limit 2;
            ```
            
        7. to see column titles `set hive.cli.print.header=true;` 
        8. observe data
            ``` sql 
            select * from emp limit 2;
            ```
        9. To see only column names without table names `set hive.resultset.use.unique.column.names=false;`
        10. observe data
            ``` sql 
            select * from emp limit 2;
            ```       
    6. Observe table in **metastore** 
        ``` sql
        mysql -uroot -pcloudera
        ```
        ``` sql
        use metastore;
        ```
        ``` sql
        select * from TBLS
        ```
    7. Observe `emp.txt` in warehouse path `hdfs dfs -ls /user/hive/warehouse/rritecdb.db/emp/`
    8. If we drop **managed_table** hive metastore and hdfs warehouse will be cleared.
        1. drop the table
            ``` sql
            drop table emp;
            ```
        2. Note that metastore table `TBLS` deleted the row of `emp`
        3. Note that `emp.txt` deleted from wareouse path

 # Hive External Tables

1. it is also called as `non-mangaed` table
2. Open terminal ```type hive```
3. create table using below script

``` sql 
Create external table if not exists emp_ext (empno int,ename string,sal int) rows delimited fields terminated by ',';
```
3. Observe Schema of table

``` sql
describe emp_ext;
```
``` sql
desc emp_ext;
```
``` sql
desc formatted emp_ext;
```
4. Observe data

``` sql
select * from emp_ext;
```
5. load data from **file** into **table**

6. In linux desktop > right click open terminal
7. create a file `vi emp_ext.txt`
8. enter data
    ``` 
    101,ram,1000
    102,john,2000
    103,marc,3000
    ```

9. type `:wq!`
10. in hive terminal type 
    ``` sql
    load data local inpath '/home/cloudera/Desktop/emp_ext.txt' into table emp;
    ```
11. the file '/home/cloudera/Desktop/emp.txt' available in this location?
    - Yes

12. observe data

    ``` sql 
    select * from emp_ext limit 2;
    ```

13. to see column titles `set hive.cli.print.header=true;` 
14. observe data
    ``` sql 
    select * from emp_ext limit 2;
    ```
15. To see only column names without table names `set hive.resultset.use.unique.column.names=false;`
16. observe data

    ``` sql 
    select * from emp_ext limit 2;
    ```       
17. Observe table in **metastore**

``` sql
mysql -uroot -pcloudera
```
``` sql
use metastore;
```
``` sql
select * from TBLS
```
18. Observe `emp.txt` in warehouse path `hdfs dfs -ls /user/hive/warehouse/rritecdb.db/emp/`
19. If we drop **external_table** hive metastore will be cleared and hdfs warehouse will **not** be cleared.
20. drop the table

``` sql
drop table emp_ext;
```

21. Note that metastore table `TBLS` deleted the row of `emp`
22. Note that `emp_ext.txt` not deleted from wareouse path
23. To delete type `hdfs dfs -rm -r -f /user/hive/warehose/emp_ext`
24. 

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
# Hadoop File Formats and its Types

1. Hadoop file formats are
    1. text file
    2. orc file
    3. parquet file
    4. avro file
2. Load data from text file to orc file storage table
    1. load data from text file to dept_text;
        ``` sql
        create table dept_text(deptno int,dname string,loc string) row format delimited fields terminated by ',';
        ```
        ``` sql
        load data local inpath '/home/cloudera/Desktop/b2023jand/dept.txt into table dept_text;

        ```
    2. load data from table to orc storage tale
        ``` sql
        create table dept_orc(deptno int,dname string,loc string) row format delimited fields terminated by ',' stored as orc;
        ```
        ``` sql 
        insert into dept_orc select * from dept_text;
        ```
    3.  load data from table to parquet storage tale
        ``` sql
        create table dept_parquet(deptno int,dname string,loc string) row format delimited fields terminated by ',' stored as parquet;
        ```
        ``` sql 
        insert into dept_parquet select * from dept_text;
        ```
# Different ways to connecting hive
1.  Mainly three ways
    1. HUE UI
    2. Hive CLI
    3. beeline
2.  HUE UI
    1. open http://quickstart.cloudera:8888
    2. provide username: **cloudera** and password as **cloudera**
    3. open hive and try different commands
        ``` sql
        show databases;
        ```
        ``` sql        
        use database rritec;        
        ```
        ``` sql
        show tables;
        ```
    4. 
3.  Hive CLI
    1. we know it
    2. run script in hive cli
        ``` sql
        source /home/cloudera/my_script.hql
        ```
    3. run script in linux
        ``` sql
        hive -f /home/cloudera/my_script.hql
        ```
    4. 
4.  beeline
    1. Connect to beeline
        ``` sql
        beeline -u jdbc:hive2://
        ```
    2. show databases;
        ``` sql
        show databases;
        ```
    3. run script
        ``` sql
        source /home/cloudera/my_script.hql
        ```
    4. run script in linux
        ``` sql
        beeline -u jdbc:hive2:// -f /home/cloudera/my_script.hql
        ```
5. ..

`Home Work`: 
1. Explore nohup command 
2. Explore nohup & command
3. Explore crontab command
  

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

5. Static Partitioning
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
        desc formatted dept_partition;
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
        desc formatted dept_partition;
        ```
        ``` sql
        select * from emp_partition;
        ```
        ``` linux
        hdfs dfs -ls /user/hive/warehouse/rritec.db/emp_partition/deptno=20/
        ```
        
    11. 
6. Dynamic Partitioning
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
# Bucketing
1. In Apache Hive, for decomposing table data sets into more manageable parts, it uses Hive Bucketing concept
2. Why Bucketing?
    1. Basically, the concept of Hive Partitioning provides a way of segregating hive table data into multiple files/directories. However, it only gives effective results in few scenarios. Such as:
        1. When there is the limited number of partitions.
        2. Or, while partitions are of comparatively equal size.
    2. comparatively equal size, is not possible in all scenarios. For example when are partitioning our tables based `geographic` locations like country. Hence, some bigger countries will have large partitions (ex: 4-5 countries itself contributing `70-80%` of total data).
    3. While small countries data will create small partitions (remaining all countries in the world may contribute to just 20-30 % of total data). Hence, at that time Partitioning will not be ideal.
    4. Then, to solve that problem of over partitioning, Hive offers Bucketing concept. It is another effective technique for decomposing table data sets into more manageable parts.
3. Features of Bucketing in Hive
    1. Basically, this concept is based on hashing function on the bucketed column. Along with mod (by the total number of buckets).
    2. Where the hash_function depends on the type of the bucketing column.
    3. However, the Records with the same bucketed column will always be stored in the same bucket.
    4. Moreover,  to divide the table into buckets we use `CLUSTERED BY` clause.
    5. Generally, in the table directory, each bucket is just a file, and Bucket numbering is 1-based.
    6. Along with Partitioning on Hive tables bucketing can be done and even without partitioning.
    7. Moreover, Bucketed tables will create almost equally distributed data file parts.
4. Advantages of Bucketing in Hive
    1. On comparing with non-bucketed tables, Bucketed tables offer the efficient sampling.
    2. Map-side joins will be faster on bucketed tables than non-bucketed tables, as the data files are equal sized parts.
    3. Here also bucketed tables offer faster query responses than non-bucketed tables as compared to  Similar to partitioning.
    4. This concept offers the flexibility to keep the records in each bucket to be sorted by one or more columns.
    5. Since the join of each bucket becomes an efficient merge-sort, this makes map-side joins even more efficient.
5. Creation of bucketed tables
    1. With the help of `CLUSTERED BY` clause and optional `SORTED BY` clause in CREATE TABLE statement we can create bucketed tables.
    2. Understanding `cluster by` and `hashing`
    3. understand below diagram with number of `buckets = 3`
        ![image](https://user-images.githubusercontent.com/20516321/216627516-90d8d264-3a75-425a-bb86-0cac3662e99d.png)

        ``` sql
        set hive.enforce.bucketing=true;
        ```
        ``` sql
        create table orders_stage(order_id int,order_date timestamp,order_customer_id int,order_status string) row format delimited fields terminated by ',' tblproperties("skip.header.line.count"="1");
        ```
        ``` sql
        load data local inpath '/home/cloudera/Desktop/rritec/orders.csv' into table orders_stage;
        ```
        ``` sql
        create table orders_buck(order_id int,order_date timestamp,order_customer_id int,order_status string) clustered by (order_id) into 8 buckets row format delimited fields terminated by ',' tblproperties("skip.header.line.count"="1");
        ```
        ``` sql
        insert into table orders_buck select * from orders_stage;
        ```
        ``` shell
        hdfs dfs -tail /user/hive/warehouse/rritec.db/orders_buck/000000_0
        ```
        ``` shell
        hdfs dfs -tail /user/hive/warehouse/rritec.db/orders_buck/000006_0
        ```       
        
    3. Understanding `sorted by`
        ``` sql
        set hive.enforce.sorting=true;
        ```
        ``` sql
        create table orders_buck_sort(order_id int,order_date timestamp,order_customer_id int,order_status string) clustered by (order_id) sorted by (order_id) into 8 buckets row format delimited fields terminated by ',' tblproperties("skip.header.line.count"="1");
        ```
        ``` sql
        desc formatted orders_buck_sort;
        ```
        ``` sql
        insert into table orders_buck_sort select * from orders_stage;
        ```
        ``` shell
        hdfs dfs -tail /user/hive/warehouse/rritec.db/orders_buck/000000_0
        ```
        ``` shell
        hdfs dfs -tail /user/hive/warehouse/rritec.db/orders_buck/000006_0
        ```         
        
        
    4.  Creating `partition` and `bucketing`

        ![image](https://user-images.githubusercontent.com/20516321/216627245-bfa4b21d-a680-4954-b017-8a53045f4812.png)

        ``` sql
        create table orders_partition_buck(order_id int,order_date timestamp,order_customer_id int) partitioned by (order_status string) clustered by (order_id) into 8 buckets row format delimited fields terminated by ',' tblproperties("skip.header.line.count"="1");
        ```
        ``` sql
        desc formatted orders_partition_buck;
        ```
        ``` sql
        insert into table orders_partition_buck partition(order_status) select * from orders_stage;
        ``` 
        ``` bash
        hdfs dfs -ls -h /user/hive/warehouse/rritec.db/orders_partition_buck/order_status=CANCELED
        ```
        ![image](https://user-images.githubusercontent.com/20516321/216626674-a0a4c49d-3264-449c-8bbf-2f5ef717edf6.png)

       
    5.  
    
6.  





        
