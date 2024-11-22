# Azure Functions

1. Azure Functions is a cloud service available on-demand that provides all the continually updated infrastructure and resources needed to run your applications. You focus on the code that matters most to you, in the most productive language for you, and Functions handles the rest. Functions provides serverless compute for Azure. You can use Functions to build web APIs, respond to database changes, process IoT streams, manage message queues, and more.

## Install Required Tools

1. Refer [document](https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-python) install python/vs code/python Extension/ Azure Function Extension

## Create Azure Function App

1. open portal.azure.com
2. go to free services
3. click on function **Create**
![image](https://github.com/user-attachments/assets/d537d99f-ca1e-41dd-81ef-e02699b80c49)

4. Click on Select
5. Create new Resource group as **rritecFinApprg**
6. Provide function app name as **rritecFunApp**
7. Select runtime stack as python
8. Click on Review and Create
9. Click on Create
10. Observe all the services under this resource group **rritecFinApprg**

## Create Hello http Trigger

1. Open VS Code
2. Left Side Menu bar > click on **Azure** > Login with azure username and password
![image](https://github.com/user-attachments/assets/d5ee7dba-7811-4bb0-b708-85ccea5a9c73)

3. In Workspace Pane > Click on Azure Functions > Click on create new project
![image](https://github.com/user-attachments/assets/db03b47c-2069-4207-8ebc-199312b4ef87)

4. create a folder anywhere and select it
5. Select language as **Python**
6. python Programming Model as **Model V2**
7. Select python version
8. Select HTTP Trigger
9. provide name as http_trigger > Press Enter
10. Select Authorization level as **Anonymous**
11. Click on **add to workspace** > press Enter
12. Observe all the files created in Explorer window > mainily observe **function_app.py** file
13. Click on Azure Menu > Under workspce pane > inline to Local project > click on **Deploy to Azure**
14. Select function app
15. Click on deploy
16. Go to portal.azure.com > naviagate to function > get function URL
17. paste in browser type **name=ram** > and observe output

## Create http Trigger to do ETL using python
1. In VS Code > In workspace Menu 
