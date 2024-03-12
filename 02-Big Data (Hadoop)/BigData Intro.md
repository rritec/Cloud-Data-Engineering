# BigData Introduction

1. Sources of BigData ?

    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/8d25230e-3cc8-4094-9e4b-e650dfad380b)

2. What is BIGDATA ?
    1. 'Big Data' is also a data but with a huge size.
    2. 'Big Data' is nothing but the huge amount of data which cannot be stored & processed by traditional systems such as RDBMS
    3. It is stated that almost 90% of today's data has been generated in the past few years.
        ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/3b8bf33b-37ff-4164-ac6a-b24bda69f065)

3. Categories of BIGDATA ?   
    1. Structured
    2. Unstructured
    3. Semi-structured
4. 3 V’s / Characteristics of BIGDATA ?
   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/fa2b954f-3d8d-4431-8fb2-1cdae5ecdce1)

5. What is the solution for BIG DATA ?
    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/a3552e6d-e43d-435b-8588-ccee645d5d26)

6. Traditional RDBMS vs. Hadoop
    1. Storage limit
    2. Varieties
    3. Cost of software
    4. Processing type
    5. Cost of hardware
    6. Source code
7. History of Hadoop?
    1. Doug cutting is the founder of Hadoop
    2. Doug cutting named it as Hadoop after his son’s toy elephant name.
    3. He published below 2 white papers:
        1. Google File System(GFS) in 2003
        2. MapReduce: Simplified Data Processing on Large Clusters in 2004
8. What is Hadoop ?
    1. An open source project from the apache software foundation
    2. It provides a software framework for distributing and running applications on cluster of servrs
    3. It is inspired by Google map reducing Model as well as its file system(GFS)
    4. Haddop was orginally written for the nutch search engine project
    5. Hadoop is open source framework written in Java
    6. It efficiently process large volumes of data on a cluster of commodity hardware
    7. Hadoop can be setup on single machine, but real power of hadoop comes with a cluster of machines, it can be scaled from single machine to thousands of machines on the fly.
    
9. Hadoop ecosystem components ?
    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/d18917a0-37cb-46b7-89d5-f713e7a8d3ae)

10. Hadoop Architecture
    1. Master: Name Node(NN)
    2. Secondary Master: Secondary Name Node(SNN)
    3. Slaves: Data Nodes(DN) / Worker Nodes(WN)

    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/5a1cd33b-65c6-4a28-8689-39405e0c3c11)

12. Hadoop Core Components
    
    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/b38cab75-aaa9-49cd-8268-15143f6d2e7e)

13. HDFS
    1. HDFS is a highly fault tolerant , distributed file system for data storage
    2. HDFS stores multiple copies of data on different Data Nodes(DN)/Worker Nodes(WN)
    3. A file is split up into blocks and stored across multiple Data Nodes(DN) by maintaining multiple copies of each block
    4. Block size = 64 MB by default in Hadoop 1.X
    5. Block size = 128 MB by default in Hadoop 2.X
    6. Hadoop cluster typically has a single Name Node(NN) and number of Data Nodes(DN) to form the HDFS Cluster
    7. When a file is added to HDFS, it is split into blocks.
    8. Every block is replicated 3 times by default.
    9. Default block size is 64 MB (configurable)   (Hadoop 1x), 128 MB (Hadoop 2x).
        ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/f4e461f4-3e6d-4691-a1a8-dcbf00aead76)

14. HDFS-Fault Tolerance
    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/a54ce944-9c46-4843-86f3-f89b71e49ebe)

    ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/c5054582-d165-45f3-97db-bf257f533b6c)


16. What is Map-Reduce ?
    1. Map-Reduce is a programming model designed for processing large volumes of data in parallel by dividing the work into a set of independent tasks
    2. Map-Reduce is a paradigm for distributed processing of large data set over a cluster of nodes

## Questions
1. Which of the below can be considered as characteristics of bigdata ?
    A. Volume
    B. Velocity
    C. Variety
    D. All the above
2. Hadoop is the solution for bigdata problem.
    A. True
    B. False

3.Hadoop follows distributed/parallel processing mechanism to process bigdata
    A. True
    B. False
4. Which of the below in traditional RDBMS lead to the evolution of hadoop ?
    A. Storage limit constraint
    B. Parallel Processing
    C. Open-Source 
    D. Cost of the software is free

5.What is the default block size in Hadoop 2.X ?

A. 64MB
B. 128 MB
C. 256 MB
D. 512 MB

6. Which is the Master Node in Hadoop ?

A. Name Node(NN)
B. Data Node(DN)
C. Secondary Name Node(SNN)
D. None of the above


7.Into how many blocks a file of 260 MB will be divided into in Hadoop 2.X ?

A. 1
B. 2
C. 3
D. 4


8.Which of below can be considered as Worker Nodes(WN) in Hadoop ?

A. Name Node(NN)
B. Data Node(DN)
C. Secondary Name Node(SNN)
D. None of the above


9.Is Hadoop Fault-Tolerant ?

A.True
B.false

10.Select popular Hadoop distributions from below:

A. Cloudera
B. Horton Works
C. MapR
D. All the above

## Answers




