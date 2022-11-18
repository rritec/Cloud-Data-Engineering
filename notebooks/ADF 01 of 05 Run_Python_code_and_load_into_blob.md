# Run Python code and load into blob
-----------
1. **Create python code to write output into blob**
      1. Create **pycode** container
      2. save below code as **main.py**

            ```python            
            import pandas as pd
            from azure.storage.blob import BlobClient

            # Define parameters
            connectionString = "DefaultEndpointsProtocol=https;AccountName=xxxxxxxx;AccountKey=xxxxxxxx;EndpointSuffix=core.windows.net"
            containerName = "output"
            outputBlobName	= "sample_output.csv"
            # Establish connection with the blob storage account
            blob = BlobClient.from_connection_string(conn_str=connectionString, 
                                                     container_name=containerName,
                                                     blob_name=outputBlobName)  
            # assign data of lists.  
            data = {'Name': ['Tom', 'Joseph', 'Krish', 'John'], 'Age': [20, 21, 19, 18]}  

            # Create DataFrame  
            df = pd.DataFrame(data) 
            df.to_csv(outputBlobName, index = False)
            with open(outputBlobName, "rb") as data:
                blob.upload_blob(data,overwrite=True)            
            ```
      3. Upload **main.py** into blob **pycode** container
2. **Create custom activity pipeline**
4. **Create custom activity pipeline**
5. **Create custom activity pipeline**

## Reference:

Review MSFT help document for more information [here](https://learn.microsoft.com/en-us/azure/batch/tutorial-run-python-batch-azure-data-factory)
