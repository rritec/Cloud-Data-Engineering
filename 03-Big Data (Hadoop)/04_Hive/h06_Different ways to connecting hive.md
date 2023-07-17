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
