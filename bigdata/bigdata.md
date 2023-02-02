# Hadoop(BigData)
1. **[Hive Metastore](#Hive-Metastore)**<br>
2. **[Hive Managed Tables](#Hive-Managed-Tables)**<br>
3. **[Hive External Tables](#Hive-External-Tables)**<br>
4. **[Hive Operations](#Hive-Operations)**<br>
5. **[Hadoop File Formats and its Types](#Hadoop-File-Formats-and-its-Types)**<br>
6. **[Different ways to connecting hive](#Different-ways-to-connecting-hive)**<br>
7. 
8. 



# Hive Metastore
1. Connect to hive cli
    1. type ```hive```
    2. type ```show databases;```
    3. type ```create database rritecdb```
    4. desc rritecdb;
        
        ![image](https://user-images.githubusercontent.com/20516321/214228819-f9f120ef-2280-4dd5-9318-8d2f797e7cae.png)

    5. How system knows to create folder in ```/user/hive/warehouse/```
    6. type ```SET;``` observe warehouse location property. using this set property system knows the location of warehouse
2. can we run hive commands from terminal
    1. Yes
    2. In normal terminal type ```hive -e "show databases;"```
    3. also observe ```"hive -e set;" | grep warehouse
        
        ![image](https://user-images.githubusercontent.com/20516321/214229607-49d7673b-0eef-4818-ab04-001ab46455de.png)

3. hive-site.xml configuration file has metastore database information
    1. open terminal ```cd /etc/hive/conf/```
    2. type ```cat hive-site.xml | grep metastore```
    3. observe metastore database as mysql
4. Connect to mysql(Metastore)
    1. open terminal > type ```mysql -uroot -pcloudera```

        ![image](https://user-images.githubusercontent.com/20516321/214223593-bffe40ce-a79c-41e7-8baa-414e8cef7c36.png)

    2. type ```show databases;```

        ![image](https://user-images.githubusercontent.com/20516321/214224728-8d6d2333-0f35-49f1-aebd-b038fc02f822.png)

    3. type ```use metastore;```
    6. type ```select * from DBS;```
  
        ![image](https://user-images.githubusercontent.com/20516321/214237910-5cba6910-c977-4e6b-b275-c48f4e236c04.png)
5. `info:`do you know we can clear the `hive cli` by using `ctrl_i` or `!clear`

# Hive Managed Tables
1. **Create managed table or internal table**
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
5.  
        
