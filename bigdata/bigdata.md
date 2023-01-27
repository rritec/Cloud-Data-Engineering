# Hadoop(BigData)
1. **[Hive Metastore](#Hive-Metastore)**<br>
2. **[Hive Managed Tables](#Hive-Managed-Tables)**<br>
3. **[Hive External Tables](#Hive-External-Tables)**<br>
4. **[Hive Operations](#Hive-Operations)**<br>
5. 



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

1. Open terminal ```type hive```
2. create table using below script

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

1. In linux desktop > right click open terminal
2. create a file `vi emp_ext.txt`
3. enter data
    ``` 
    101,ram,1000
    102,john,2000
    103,marc,3000
    ```

3. type `:wq!`
4. in hive terminal type 
    ``` sql
    load data local inpath '/home/cloudera/Desktop/emp_ext.txt' into table emp;
    ```
6. the file '/home/cloudera/Desktop/emp.txt' available in this location?
    - Yes

7. observe data

    ``` sql 
    select * from emp_ext limit 2;
    ```

7. to see column titles `set hive.cli.print.header=true;` 
8. observe data
    ``` sql 
    select * from emp_ext limit 2;
    ```
9. To see only column names without table names `set hive.resultset.use.unique.column.names=false;`
10. observe data

    ``` sql 
    select * from emp_ext limit 2;
    ```       
11. Observe table in **metastore** 

``` sql
mysql -uroot -pcloudera
```
``` sql
use metastore;
```
``` sql
select * from TBLS
```
12. Observe `emp.txt` in warehouse path `hdfs dfs -ls /user/hive/warehouse/rritecdb.db/emp/`
13. If we drop **external_table** hive metastore will be cleared and hdfs warehouse will **not** be cleared.

14. drop the table

``` sql
drop table emp_ext;
```
15. Note that metastore table `TBLS` deleted the row of `emp`
16. Note that `emp_ext.txt` not deleted from wareouse path
17. To delete type `hdfs dfs -rm -r -f /user/hive/warehose/emp_ext`

# Hive Operations
1. jjj
        
