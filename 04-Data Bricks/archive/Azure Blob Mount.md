# Azure blob Mount
1. Mount an Azure Blob storage container
``` python
dbutils.fs.mount(
  source = "wasbs://cdrive@b2404sa.blob.core.windows.net",
  mount_point = "/mnt/emp",
  extra_configs = {"fs.azure.account.key.b2404sa.blob.core.windows.net":"<xxxx  account key  xxxx>"})
```
2. Create dataframe
``` python
df = (
    spark
    .read
    .format("csv")
    .option("header","true")
    .load("dbfs:/mnt/emp/inputfolder/emp.csv")
)
```
``` python
df.show()
```
3. Write df in the mount
``` python
df.write.option("header","true").csv("/mnt/emp/emp1.csv")
```
4. List Filesystem
``` py 
dbutils.fs.ls("/mnt/emp/")
```
5. Unmount the Filesystems
``` py
dbutils.fs.unmount("/mnt/emp")
```
6. 
