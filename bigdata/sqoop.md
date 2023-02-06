# Hadoop(BigData)(sqoop)
1. **[Sqoop Introduction](#Sqoop-Introduction)**<br>
2. 




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
11. run query
  ``` sql
  sqoop \
  eval \
  --connect jdbc:mysql://localhost:3306/retail_db \
  --username root \
  --password-file hdfs:///user/cloudera/rritec/sqoop_password.txt \
  --query "select * from orders limit 10;"
  ```
12. 

