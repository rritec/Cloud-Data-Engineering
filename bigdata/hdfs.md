# Hadoop(BigData)(HDFS)
1. **[hadoop](#hadoop)**<br>
2. **[usage](#usage)**<br>
3. **[help](#help)**<br>
4. **[ls](#ls)**<br>
4. **[mkdir](#mkdir)**<br>
5. **[touchz](#touchz)**<br>
6. **[help](#help)**<br>
7. **[help](#help)**<br>
8. **[help](#help)**<br>
9. **[help](#help)**<br>
10. **[help](#help)**<br>
11. **[help](#help)**<br>
12. **[help](#help)**<br>
13. **[help](#help)**<br>
14. **[help](#help)**<br>
15. **[help](#help)**<br>
16. **[help](#help)**<br>
17. **[help](#help)**<br>
18. **[help](#help)**<br>
19. **[help](#help)**<br>
20. **[help](#help)**<br>



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


