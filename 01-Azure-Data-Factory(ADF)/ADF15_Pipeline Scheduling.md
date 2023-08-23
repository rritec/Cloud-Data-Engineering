# Triggers

1. A pipeline run in Azure Data Factory and Azure Synapse defines an instance of a pipeline execution.
2. For example, say you have a pipeline that executes at 8:00 AM, 9:00 AM, and 10:00 AM. In this case, there are three separate runs of the pipeline. Each pipeline run has a unique pipeline run ID.
3. A run ID is a GUID that uniquely defines that particular pipeline run
4. types of triggers
    1. Scheduled
    2. Tumbling window
    3. Storage event
    4. Custom event
5. Pipelines and triggers have a many-to-many relationship (except for the tumbling window trigger). 
6. Multiple triggers can kick off a single pipeline, or a single trigger can kick off multiple pipelines
7. Open any Pipeline > Click on **Add Trigger** > Click on **New/Edit**
8. Click on **New** > Name it as **Daily_trigger**

![image](https://user-images.githubusercontent.com/20516321/229695521-76fb098a-04ca-4f0f-89e5-5929997416bc.png)

9. Click on ok
