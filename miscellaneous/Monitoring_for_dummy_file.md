1.Open Azure Data Factory -> Pipelines -> create a pipeline name it as **Monitoring_dummy_file**

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/e552c6a9-f050-4ff4-9061-5f17dfb46613)

2.In Activities -> Search for **Get Meta Data activity** then drag drop in pipeline

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/5145914b-2dd4-4bcd-888f-e3784ca1da96)

Click on activity -> Go to Settings 
   .select Dataset if it is available if not create new dataset
   .Field list -> Click on **New** -> In argument drop down select **Exists**

![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/a3c6b478-e05f-4d28-832c-363f4c35b884)

3.In Activities -> Search for **IF condition activity** then drag drop in pipeline and now connect **Get MetaData activity**
   - Click on if activity
     - for True Give **Set Variable activity**
     - for False Give **Wait activity**
     - For Expression search dynamically
     - ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/455ec53d-c45b-4e93-97c7-aa9a06d35d26)

    
![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/5187e289-f5f4-4188-8983-8b0c800cdfed)

4.In Activities -> Search for **Until activity** now cut and paste **IF condition activity** and **Get MetaData activity** in **Until activity**
   -Go to settings in Expression field provide **@equals(variables('vfile'),'Arrived' )**

   ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/8f70d12a-dd7b-4af6-b206-ff0a3c621fae)

5.After completing above steps validate and debug
   -If file exist it will execute if condition it means **meta data activity** will execute
   -else it will execute **wait activity**

  ![image](https://github.com/rritec/Cloud-Data-Engineering/assets/20516321/26337087-3c42-4b96-a88c-2c1c47e68ead)


  

