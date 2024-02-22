# Integration runtimes

1. The Integration Runtime (IR) is the compute infrastructure used by Azure Data Factory and Azure Synapse pipelines.
2. In Data Factory and Synapse pipelines, an activity defines the action to be performed
3. A linked service defines a target data store or a compute service
4. An integration runtime provides the bridge between activities and linked services
5. Data Factory offers three types of Integration Runtime (IR), and you should choose the type that best serves your data integration capabilities and network environment requirements. The three types of IR are:
	  1. Azure
	  2. Self-hosted
	  3. Azure-SSIS
6. Refer the [doc](https://learn.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime)
# Questions
1. What is IR ?
- Integration runtime (IR) is the compute infrastructure used by Azure Data Factory and Azure Synapse pipelines to execute and dispatch activities

2. Types of IRs
    - Azure
    - Self-Hosted
    - Azure-SSIS
	
3. If source and targets are in Azure then which IR is needed?
    - Azure
4. If source or targets or both in private network then which IR is needed?
    - Self-Hosted
5. To run SSIS package which IR is needed?
    - Azure-SSIS
6. 
