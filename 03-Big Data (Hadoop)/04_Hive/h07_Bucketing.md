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
