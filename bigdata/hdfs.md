# Hadoop(BigData)(HDFS)
1. **[hadoop](#hadoop)**<br>
2. **[usage](#usage)**<br>
3. **[help](#help)**<br>
4. **[ls](#ls)**<br>
4. **[mkdir](#mkdir)**<br>
5. **[touchz](#touchz)**<br>
6. **[Put](#Put)**<br>
7. **[copyFromLocal](#copyFromLocal)**<br>
8. **[get](#get)**<br>
9. **[copyToLocal](#copyToLocal)**<br>
10. **[cp](#cp)**<br>
11. **[getmerge](#getmerge)**<br>
12. **[rmdir](#rmdir)**<br>
13. **[rm](#rm)**<br>
14. **[moveFromLocal](#moveFromLocal)**<br>
15. **[mv](#mv)**<br>
16. **[tail](#tail)**<br>
17. **[Interview Questions](#Interview-Questions)**<br>
18. **[Answers](#Answers)**<br>




##### hadoop
``` sh

hadoop

```
``` sh

hadoop fs

```
``` sh

hdfs dfs

```
##### usage
1. `Usage` command is useful to know the available options on a particular command

``` sh

hdfs dfs -usage ls

```
##### help

1. If you want to know complete details of all available options go with `help` command

``` sh

hdfs dfs -usage ls

```
##### ls
1. `ls` without any options in hdfs is equal to `ls –lrt` in `linux`
```sh

hdfs dfs -ls /user/cloudera/b20230201/

```
2. to list only directories
```sh

hdfs dfs -ls /user/cloudera/b20230201/ | grep ^d

```
3. to list only files
```sh

hdfs dfs -ls /user/cloudera/b20230201/ | grep ^-

```
4. human readable format of file size using –h option
```sh

hdfs dfs -ls -h /user/cloudera/b20230201/

```
5. recursively listing all the files and directories
```sh

hdfs dfs -ls -R /user/cloudera/b20230201/

```
6. to display the paths of files and directories only (not detailed info such as permissions etc)
```sh

hdfs dfs -ls -C /user/cloudera/b20230201/

```

##### mkdir
1. creating `one` directory

``` sh

hdfs dfs -mkdir /user/cloudera/b20230201

```
2. creating `multiple` directories

``` sh

hdfs dfs -mkdir /user/cloudera/b20230201/d1 /user/cloudera/b20230201/d2

```
3. creting `multilevel` directory

``` sh

hdfs dfs -mkdir -p /user/cloudera/b20230201/country/state/district/

```
4. test it

``` sh

hdfs dfs -ls -R /user/cloudera/b20230201/

```
##### touchz

1. create `one` zero kb file
``` sh

hdfs dfs -touchz /user/cloudera/b20230201/emp.txt

```
2. create `multiple` zero kb files
``` sh

hdfs dfs -touchz /user/cloudera/b20230201/emp1.txt /user/cloudera/b20230201/emp2.txt

```
##### put

1. Navigate to linux desktop and create a folder and file
``` sh

cd Desktop

```
``` sh

mkdir b20230201

```
``` sh

cd b20230201

```
``` sh

vi emp.txt
# type i from the keyboard to switch from command mode to edit mode
# type some data like > iam learning hdfs commands
```
2. Copy this file from linux machine path to hadoop path
``` sh

hdfs dfs -put emp.txt /user/cloudera/b20230201/

```
``` sh

hdfs dfs -ls /user/cloudera/b20230201/

```
##### copyFromLocal

1. same as put
2. Copy this file from linux machine path to hadoop path
``` sh

hdfs dfs -copyFromLocal emp.txt /user/cloudera/b20230201/emp1.txt

```
``` sh

hdfs dfs -ls /user/cloudera/b20230201/

```

##### get

1. Copy file from hadoop path to linuxpath
``` sh

hdfs dfs -get /user/cloudera/b20230201/emp.txt  emp10.txt 

```
``` sh

ls -l

```
##### copyToLocal

1. same as get
2. Copy file from hadoop path to linuxpath
``` sh

hdfs dfs -copyToLocal /user/cloudera/b20230201/emp.txt  emp11.txt 

```
``` sh

ls -l

```
##### cp

1. copy files within the HDFS locations
2. take backup of file in same location
``` sh

hdfs dfs -cp /user/cloudera/b20230201/emp.txt /user/cloudera/b20230201/emp_bkp.txt

```
``` sh

hdfs dfs -ls /user/cloudera/b20230201/

```

3. take backup of file in different location
``` sh

hdfs dfs -cp /user/cloudera/b20230201/emp.txt /user/cloudera/b20230201/d1/emp_bkp.txt

```
``` sh

hdfs dfs -ls /user/cloudera/b20230201/d1/

```
##### getmerge

1. merging multiple HDFS files into a single file on local FS
    1. create three files using `vi` editor and write content as `it is file1`  in first file `it is file2` in second file and `it is file3` in third file
        ``` sh
        
        vi merge_emp1.txt
        vi merge_emp2.txt
        vi merge_emp3.txt
        
        ```
        ``` sh
        
        ls -l | grep merge
        
        ```
        ``` sh
        
        cat merge*
        
        ```
    2. copy these three files into hdfs location
        ``` sh
        
        hdfs dfs -put merge* /user/cloudera/b20230201/
        # verify it
        hdfs dfs -ls /user/cloudera/b20230201 | grep merge
        
        ```
    3. merge all three files
        ``` sh

        hdfs dfs -getmerge /user/cloudera/b20230201/merge* merge_emp_1_to_3.txt
        # verify
        cat merge_emp_1_to_3.txt
        

        ```
2. adding a new line character at the end of each file using –nl option
``` sh
hdfs dfs -getmerge -nl /user/cloudera/b20230201/merge* merge_emp_1_to_3_nl.txt
```
``` sh
cat merge_emp_1_to_3_nl.txt
```




