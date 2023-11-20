# Generate File Name with Timestamp Dynamically
1. Click on New Pipeline > Name it as pipeline_dynamic_target_fielnames
2. drag and drop copy activity
3. provide Azure SQL DB dataset as source
4. create new blob dataset as shown below
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/f10827f7-d65e-472d-bbab-7c5399330b3a)
``` sql
@concat(
    'emp',
    formatDatetime(
        utcnow(),
        'yyyy-MM-ddTHH:mm:ss.fffffffK'
    ),
    '.csv'
)
```

6. clcik on debug > observe the file
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/b7c14cf7-2122-421b-8da2-918281dff96e)

7. 
