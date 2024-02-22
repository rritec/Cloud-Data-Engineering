# Replicate DataFlows logic in copy activity

1. Create a new pipeline
2. Drag and drop Copy Activity
3. click on the source > create a datasource by pointing sql server
4. provide below query
``` sql

SELECT dept.dname,
       Sum(emp.sal) AS total_sal
FROM   emp,
       dept
WHERE  emp.deptno = dept.deptno
       AND emp.deptno IN ( 10, 20 )
GROUP  BY dname
ORDER  BY 2 DESC 

```
![image](https://user-images.githubusercontent.com/20516321/230277558-39bbd269-d718-455f-bb4a-5df7f1cce3a9.png)

5. click on the sink > create a datasource by pointing sql server
6. run it and observe output
![image](https://user-images.githubusercontent.com/20516321/230277799-9d175d1c-5681-4bad-b47c-61512d134e3c.png)


![image](https://user-images.githubusercontent.com/20516321/230277945-b20663bc-73fa-418d-b659-c9c8bcb75210.png)

7. 
