# Branch Files using Switch

1. Create a pipeline and name it as **ADF13_4_Branch Files using Switch**
2. Create a pipeline level parameter/variable as shown below

![image](https://github.com/user-attachments/assets/09b0bc72-4f9c-45db-8c8d-cd6e9442b4bf)

3. Drag and drop **ForEach** activity
4. Click on **Settings** and configure as shown below

![image](https://github.com/user-attachments/assets/21662008-9b60-4bcc-9ee2-3e64c66ee197)

5. Click on **Activities** > Click on **edit** > drag and drop **Switch** Activity and configure as shown below

![image](https://github.com/user-attachments/assets/d04ee0b8-be2d-474e-88de-fa32762ac2a2)


![image](https://github.com/user-attachments/assets/cd9953a2-a8cc-43ea-90ce-565c12540f48)

6. Observe result

![image](https://github.com/user-attachments/assets/c9f02c4b-a0c1-42ce-8fb3-6b9a795656d8)

7. Json Code of pipeline
``` json
{
    "name": "ADF13_4_Branch Files using Switch",
    "properties": {
        "activities": [
            {
                "name": "ForEach1",
                "type": "ForEach",
                "dependsOn": [],
                "userProperties": [],
                "typeProperties": {
                    "items": {
                        "value": "@variables('pInputFiles')",
                        "type": "Expression"
                    },
                    "isSequential": true,
                    "activities": [
                        {
                            "name": "Switch2",
                            "type": "Switch",
                            "dependsOn": [],
                            "userProperties": [],
                            "typeProperties": {
                                "on": {
                                    "value": "@item()",
                                    "type": "Expression"
                                },
                                "cases": [
                                    {
                                        "value": "EMP",
                                        "activities": [
                                            {
                                                "name": "Copy data1",
                                                "type": "Copy",
                                                "dependsOn": [],
                                                "policy": {
                                                    "timeout": "0.12:00:00",
                                                    "retry": 0,
                                                    "retryIntervalInSeconds": 30,
                                                    "secureOutput": false,
                                                    "secureInput": false
                                                },
                                                "userProperties": [],
                                                "typeProperties": {
                                                    "source": {
                                                        "type": "DelimitedTextSource",
                                                        "storeSettings": {
                                                            "type": "AzureBlobStorageReadSettings",
                                                            "recursive": true,
                                                            "enablePartitionDiscovery": false
                                                        },
                                                        "formatSettings": {
                                                            "type": "DelimitedTextReadSettings"
                                                        }
                                                    },
                                                    "sink": {
                                                        "type": "AzureSqlSink",
                                                        "writeBehavior": "insert",
                                                        "sqlWriterUseTableLock": false,
                                                        "tableOption": "autoCreate",
                                                        "disableMetricsCollection": false
                                                    },
                                                    "enableStaging": false,
                                                    "translator": {
                                                        "type": "TabularTranslator",
                                                        "typeConversion": true,
                                                        "typeConversionSettings": {
                                                            "allowDataTruncation": true,
                                                            "treatBooleanAsNumber": false
                                                        }
                                                    }
                                                },
                                                "inputs": [
                                                    {
                                                        "referenceName": "dsemp",
                                                        "type": "DatasetReference"
                                                    }
                                                ],
                                                "outputs": [
                                                    {
                                                        "referenceName": "dstgtemp",
                                                        "type": "DatasetReference"
                                                    }
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "value": "DEPT",
                                        "activities": [
                                            {
                                                "name": "Copy data2",
                                                "type": "Copy",
                                                "dependsOn": [],
                                                "policy": {
                                                    "timeout": "0.12:00:00",
                                                    "retry": 0,
                                                    "retryIntervalInSeconds": 30,
                                                    "secureOutput": false,
                                                    "secureInput": false
                                                },
                                                "userProperties": [],
                                                "typeProperties": {
                                                    "source": {
                                                        "type": "DelimitedTextSource",
                                                        "storeSettings": {
                                                            "type": "AzureBlobStorageReadSettings",
                                                            "recursive": true,
                                                            "enablePartitionDiscovery": false
                                                        },
                                                        "formatSettings": {
                                                            "type": "DelimitedTextReadSettings"
                                                        }
                                                    },
                                                    "sink": {
                                                        "type": "AzureSqlSink",
                                                        "writeBehavior": "insert",
                                                        "sqlWriterUseTableLock": false,
                                                        "tableOption": "autoCreate",
                                                        "disableMetricsCollection": false
                                                    },
                                                    "enableStaging": false,
                                                    "translator": {
                                                        "type": "TabularTranslator",
                                                        "typeConversion": true,
                                                        "typeConversionSettings": {
                                                            "allowDataTruncation": true,
                                                            "treatBooleanAsNumber": false
                                                        }
                                                    }
                                                },
                                                "inputs": [
                                                    {
                                                        "referenceName": "dsdeptsrc",
                                                        "type": "DatasetReference"
                                                    }
                                                ],
                                                "outputs": [
                                                    {
                                                        "referenceName": "dstgtemp10_loglevel",
                                                        "type": "DatasetReference"
                                                    }
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                }
            }
        ],
        "variables": {
            "pInputFiles": {
                "type": "Array",
                "defaultValue": [
                    "EMP",
                    "DEPT"
                ]
            }
        },
        "annotations": []
    }
}
```


