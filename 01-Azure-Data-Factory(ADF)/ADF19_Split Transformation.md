# Split Transformation

Go to **AzureDataFactory(ADF)** > Click on **Author** > Create New Pipeline > Give name as **Pipeline1_Dataflows_split** > Drag **Dataflow Activity** from Activity pane into work area 

![image](https://user-images.githubusercontent.com/20516321/212013537-97dda0ff-95d0-4019-afdc-9a43482ff8bd.png)

Click on Dataflow Activity > Go to settings > Click on New > Give name as **Dataflow_Split** > Click on **Add Source** > Go to **sourceSetting** > Give name as **Source1emp** > Bottom **sourceSetting** > Select **Dataset** as **Src_azure_sql_emp**

![image](https://user-images.githubusercontent.com/20516321/211998478-8cfbf6b0-01eb-438a-89fa-8299e7aa8afa.png)

Click on add symbol > Search for **Conditional split** > Bottom of Conditional split > In split condition > Follow as per below picture

![image](https://user-images.githubusercontent.com/20516321/212001689-83074d4b-26e2-4ea9-abd5-6fa6dc10e8f2.png)

![image](https://user-images.githubusercontent.com/20516321/212001899-fad78590-b9d7-40df-91f4-dd60c7ca90b1.png)

Click on add symbol > search for **Sink** > Give Name as Sink1 > Below sink Create New dataset > Give name as DS_Sink_Emp10 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink_Emp10

![image](https://user-images.githubusercontent.com/20516321/212005400-e1c0d2d0-9a31-4d5c-840f-95934fac6f45.png)

Click on add symbol > search for **Sink2** > Give Name as Sink2 > Below sink Create New dataset > Give name as DS_Sink_emp20 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink2_Emp20

![image](https://user-images.githubusercontent.com/20516321/212005713-a0d70a1f-b9d5-45dc-9e81-056c04eab7df.png)

Click on add symbol > search for **Sink3** > Give Name as Sink3 > Below sink Create New dataset > Give name as DS_Sink_emp30 > Select LinkService as **ls_azuresqldb_dec22** > Click on Create new table > Give name as dbo.DS_Sink3_emp30

![image](https://user-images.githubusercontent.com/20516321/212005953-57baff49-37af-43a0-af74-d19bd59b060a.png)

Go to **Pipeline1_Dataflows_Split1** > Click on **validate** > Click on **Publish** > Click on **Debug**

![image](https://user-images.githubusercontent.com/20516321/212010636-3e28670e-de15-4f5a-b526-cde00ab9abea.png)

Now Open **SQL SERVER** > Check data of table **[dbo].[Ds_Sink_emp10]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink_emp10]
```
![image](https://user-images.githubusercontent.com/20516321/212011205-8a77c32e-abd4-46b4-9fa2-4d77560f7d34.png)

Check data of table **[dbo].[Ds_Sink2_emp20]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink2_emp20]
```
![image](https://user-images.githubusercontent.com/20516321/212012385-bb3e4013-fb1f-4eb8-9b00-a4ebcaf993cb.png)

Check data of table **[dbo].[Ds_Sink3_emp30]**  > Using below Query

``` sql
Select * from [dbo].[Ds_Sink3_emp30]
```

![image](https://user-images.githubusercontent.com/20516321/212012706-9c0caf2a-1c16-4470-9f0f-03cd7408acca.png)

