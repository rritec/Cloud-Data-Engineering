# Hadoop(BigData)
1. **[Hive Metastore](#Hive-Metastore)**<br>
2. **[Hive Managed External Tables](#Hive-Managed-External-Tables)**<br>



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

# Hive Managed External Tables
1. Create managed table or internal table
    1. Open terminal ```type hive```
    2. create table using below script
    
        ``` sql
        Create table emp if not exists (empno int,ename string,sal int) rows delimited fields terminated by ',';```
    3. 
    
  2. 
  3. Create external Table 
