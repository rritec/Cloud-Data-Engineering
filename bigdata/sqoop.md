# Hadoop(BigData)(sqoop)
1. **[Sqoop Introduction](#Sqoop-Introduction)**<br>
2. **[Sqoop Eval](#Sqoop-Eval)**<br>
3. **[Sqoop Import](#Sqoop-Import)**<br>
4. **[Sqoop Export](#Sqoop-Export)**<br>
5. **[Import All Tables](#Import-All-Tables)**<br>
6. **[Import table from mysql to hive](#Import-table-from-mysql-to-hive)**<br>
7. 
8. 




# Sqoop Introduction
1. Sqoop = `SQ`L + HAD`OOP`
2. It is command-line tool
3. A tool which we use for transferring data between Hadoop and relational database servers

![image](https://user-images.githubusercontent.com/20516321/216875230-3d41cfcc-dc3a-44d4-8614-83156aa39a69.png)

4. helps to Import individual tables or entire databases to files in HDFS
5. Access help of sqoop

  ``` sql
  sqoop help
  ```
  ![image](https://user-images.githubusercontent.com/20516321/216913759-31f39682-2fab-4a4f-88ef-c6d521109d78.png)

6. know your sqoop version

  ``` sql
  sqoop version
  ```
  ![image](https://user-images.githubusercontent.com/20516321/216913221-8e47346a-8558-4cdf-bc00-0cde896f5cbc.png)

7. know more on perticular command

  ``` sql 
 sqoop help list-databases
 ```

  ![image](https://user-images.githubusercontent.com/20516321/216914197-ccb1209a-88d6-4412-91db-a37c1e7e2581.png)

8. Status of mysql server
``` bash
ps -eaf | grep mysql
```
``` bash
sudo service mysqld status
```

9. verify jar file availability
``` bash
cd /usr/share/java
ls -ltrh
```
``` bash
cd /var/lib/sqoop
ls -ltrh
```

10. list databases

  ``` sql
  sqoop list-databases --connect jdbc:mysql://localhost:3306 --username root --password cloudera
  ```
  ``` sql
  sqoop list-databases \
  --connect jdbc:mysql://localhost:3306 \
  --username root \
  --password cloudera
  ```
   ``` sql
  sqoop list-databases \
  --connect jdbc:mysql://localhost:3306 \
  --username root \
  --P
  ```
  ``` bash
  cd /home/cloudera/Desktop/rritec
  echo -n "cloudera" > sqoop_password.txt
  ```
   ``` sql
  sqoop list-databases \
  --connect jdbc:mysql://localhost:3306 \
  --username root \
  --password-file file:///home/cloudera/Desktop/rritec/sqoop_password.txt
  ```
   ``` sql
  sqoop list-databases \
  --connect jdbc:mysql://localhost:3306 \
  --username root \
  --password-file hdfs:///user/cloudera/rritec/sqoop_password.txt
  ```
# Sqoop Eval
1. Basically, to quickly run simple SQL queries against a database, we use Sqoop `Eval` tool in Sqoop.
2. run simple sql query to see 10 records
  ``` sql
  sqoop eval \
  --connect jdbc:mysql://localhost:3306/retail_db \
  --username root \
  --password-file hdfs:///user/cloudera/rritec/sqoop_password.txt \
  --query "select * from orders limit 10;"
  ```
  
3. Create table and insert rows
  ``` sql
  sqoop eval \
  --connect jdbc:mysql://localhost:3306/retail_db \
  --username root \
  --password-file hdfs:///user/cloudera/rritec/sqoop_password.txt \
  --query "create table test(id int,name varchar(20));"
  ```
  ``` sql
  sqoop eval \
  --connect jdbc:mysql://localhost:3306/retail_db \
  --username root \
  --password-file hdfs:///user/cloudera/rritec/sqoop_password.txt \
  --query "insert into test values(101,'Myla RamReddy');"
  ```
4. Drop the table
  ``` sql
  sqoop eval \
  --connect jdbc:mysql://localhost:3306/retail_db \
  --username root \
  --password-file hdfs:///user/cloudera/rritec/sqoop_password.txt \
  --query "drop table test;"
  ```
5. 

# Sqoop Import

1. Import `orders` table from `retail_db` database

    ``` sql 
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table orders \
    --target-dir /user/cloudera/rritec/orders
    ```
2. Observe files in `hdfs` location

    ``` sql
    hdfs dfs -ls -h /user/cloudera/rritec/orders/
    ```
    ![image](https://user-images.githubusercontent.com/20516321/217207566-4b7e1fc1-edd8-4f15-a1a4-b1eb17279535.png)


3. Observe number of row in each file.
    
    ![image](https://user-images.githubusercontent.com/20516321/217235654-2f2ba0ff-4197-4b57-a9bb-4187d3f2ac08.png)

4. Observe total number of rows is macing with mysql table

  ![image](https://user-images.githubusercontent.com/20516321/217236063-84f44b6a-8ec4-4a8c-b1f8-8e91e52d6dd0.png)
  ![image](https://user-images.githubusercontent.com/20516321/217236250-96b00f2d-4cea-411c-9cb1-80496219658b.png)

  

5. `warehouse-dir` will create directory with the name of mysql table
    ``` sql 
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table order_items \
    --warehouse-dir /user/cloudera/
    ```
6. append data
    ``` sql 
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table orders \
    --target-dir /user/cloudera/rritec/orders \
    --append
    ```
7. Restrict number of mappers
  ``` sql 
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table orders \
    --target-dir /user/cloudera/rritec/orders \
    --append \
    --num-mappers 2
   ```
   ``` sql 
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table orders \
    --target-dir /user/cloudera/rritec/orders \
    --append \
    -m 2
   ```
8. To see detailed log use `verbose`
  ``` sql 
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table orders \
    --target-dir /user/cloudera/rritec/orders \
    --append \
    --num-mappers 2 \
    --verbose
   ```
9. understand the `compress`
  ``` sql 
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table orders \
    --target-dir /user/cloudera/rritec/orders \
    --append \
    --num-mappers 2 \
    --compress
   ```
10. 


# Sqoop Export

1. Export data back from the HDFS to the RDBMS database.
2. The target table must exist in the target database. 
3. The files which are given as input to the Sqoop contain records, which are called rows in table. Those are read and parsed into a set of records
4. The default operation is to insert all the record from the input files to the database table using the INSERT statement.

    ``` sql
    create table emp(empno int, ename varchar(50));
    ```
    
5. Create a file with below records and push into hadoop location

    ![image](https://user-images.githubusercontent.com/20516321/217448279-5c2c50a0-a710-4741-ba65-a4a47f29d1cb.png)


    ``` sh
    sqoop export --connect jdbc:mysql://localhost:3306/retail_db --username root -password cloudera --table emp --export-dir /user/cloudera/emp.txt
    ```


    
6. Verify the data in mysql

    ``` sql 
    select * from emp;
    ```
    ![image](https://user-images.githubusercontent.com/20516321/217448436-a1e793b8-fd9a-4713-9439-c1d81d005839.png)

    
7. 

# Import All Tables

1. import all tables
   ``` sql
    sqoop import-all-tables --connect jdbc:mysql://localhost:3306/retail_db --username root -password cloudera --warehouse-dir /user/cloudera/import_all_tables/
    ```
2. If Pk is not available use `--autoreset-to-one-mapper`
3. If we need to exclude any tables use `--exclude-tables <tables>`
4. observe exported files
    ``` sql
    hdfs dfs -ls -R /user/cloudera/import_all_tables
    ```
    

# Import table from mysql to hive

1. Directly import a table from `mysql` to `hive`

    ``` sql
    sqoop import \
    --connect jdbc:mysql://localhost:3306/retail_db \
    --username root \
    --password cloudera \
    --table orders \
    --hive-import \
    --hive-database rritec_test \
    --hive-table hive_orders
    ```
    
2. 
