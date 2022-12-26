# Create email workflow endpoints

Ref: https://learn.microsoft.com/en-us/azure/data-factory/tutorial-control-flow-portal

![image](https://user-images.githubusercontent.com/20516321/208333982-d43d8332-1a6d-44af-809d-d26f25204ce2.png)

# Create Logic Apps using Gmail


1. In search box type **Logic Apps** > Under **services** > Click on **Logic Apps**
2. 2. Click on **Add** > Provide required information as for your subscription
3. ![image](https://user-images.githubusercontent.com/20516321/209438015-aaf01251-0a7c-4f75-93f8-5ac4e009cd2d.png)
3. Click on review&create > After Deployment > click on **Goto resource** > Click on ADD

3. Under **Start with a common trigger** > Click on **When a HTTP request is received**

    ![image](https://user-images.githubusercontent.com/20516321/209438373-8aba531f-9851-4634-a768-c27fe2be56dd.png) 
    
  * Use this json code for your refernce.  

``` 
{
    "properties": {
        "dataFactoryName": {
            "type": "string"
        },
        "message": {
            "type": "string"
        },
        "pipelineName": {
            "type": "string"
        }
    },
    "type": "object"
}
 
```
4. At the top of the Logic Apps Designer>>select Save>>You can now see the URL of your HTTP request trigger>>Select the copy icon to copy it for later use>>For Your reference copy and paste in your notepad.
 
 ![image](https://user-images.githubusercontent.com/20516321/209442383-618a03ed-462e-46df-a3bb-53a217319f16.png)
    
4. Click New step>>type **Gmail** in the actions search box>>Search and select **Send email (V2)**>>type connection name as sendsuccessmail as per below dialog box
5. Click on sign in>>Give you gmail user and password.
6. Type TargetGmail in **To**>>click on Add parameter and in drop down select Body and subject.

   ![image](https://user-images.githubusercontent.com/20516321/209439215-4055ccb8-8efd-49cc-893e-61f929ece512.png)
   

   ![image](https://user-images.githubusercontent.com/20516321/209438553-a8abceee-ce88-4ee0-a777-652168c368c7.png)
   
7. Type Target Gmail in **To**>>click on Add parameter and in drop down select Body and subject.

   ![image](https://user-images.githubusercontent.com/20516321/209439215-4055ccb8-8efd-49cc-893e-61f929ece512.png)
   
8. Go to **Azure Data Factory**>>click **Launch Audio**>>Click on **Author**>>Create a pipeline.
9. Expand Your practicing pipeline>>In Activities Search for **Web** and drag into workflow.

   ![image](https://user-images.githubusercontent.com/20516321/209440556-3604c90e-3284-4f8a-a610-2ab37e09378f.png)
   
10. click on web>>open General tab give name of Activity **successmail**>>open settings tab past **URL**>>click on **Body** as **Add dynamic expression**.


    ![image](https://user-images.githubusercontent.com/20516321/209442837-aefb6c5c-10b9-43dc-a6df-bd9f03f81817.png)
    
11. connect with your Blob activity pipeline (or) old people.

    ![image](https://user-images.githubusercontent.com/20516321/209442917-f4d3c19b-c275-470d-a4b2-31f6b0d74130.png)
    
12. Now top of Your work flow>>click on **Validate** for Validation.
13. click on **Publish**.
14. click on **Debug**
15. After Debug, click **Trigger**.

# Create Fail Logic App

1. Copy the Succeslogicapp>>Click on Successlogicapp>>On tool bar menu>>click on **Clone** to copy.

  ![image](https://user-images.githubusercontent.com/20516321/209443382-bd837d01-b694-420f-a542-d410d55991b6.png)
  
2. Give name as **Faillogicapp**.
3. Copy **URL** and past into notepad.
4. Goto Data factory>>click on your **Successpipeline**>>click on **successmailweb**>>click on clone to copy web activity.

    ![image](https://user-images.githubusercontent.com/20516321/209443590-60825e3f-7d35-4eb6-a012-2b08ce050c5e.png)
5. After clone Successmail web Activity>>Go to general tab give name as Fail mail.
6. click on setting and paste (or) change the **URL**.
7. Connect to **BlobActivity** as fail
![image](https://user-images.githubusercontent.com/20516321/209444154-3140df5d-8b78-45a4-99c1-6f99957a62e1.png) 
  
8. Now top of Your work flow>>click on **Validate** for Validation.
9. click on **Publish**.
10. click on **Debug**.
11. After Debug, click **Trigger**.




   
    
    
    

   
   
   
   
   



  





