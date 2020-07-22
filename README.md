## Notes taken while running [Automated Partition Management with Azure Analysis Services](https://azure.microsoft.com/en-us/blog/azure-as-automated-partition-management/) both locally and against Azure data services.
Follow white paper to run the sample code locally

### Run sample code locally with in-line initialization (i.e. hard-coded)
1. Deploy the AdventureWorks tabular model
- You will most likely get a connection failure error unless you change the data source on the model from "localhost\sp1" to just "localhost" as noted in [github issue #14](https://github.com/microsoft/Analysis-Services/issues/14)

2. Deploy the configuration database locally by right-clicking AsPartitionProcessing.ConfigurationLogging database project and clicking "publish". Unless you change it, the name of the database will be the same as the project name.

3. Run the AsPartitionProcessing.SampleClient project. Upon completion, verify that "Internet Sales" and "Reseller Sales" tables in the local analysis database now contain partitions.

### Run sample code locally using database initialization
1. Within SampleClient/Program.cs, modify the following line:
```c#
// from
// private static ExecutionMode _executionMode = ExecutionMode.InitializeInline;

// to
private static ExecutionMode _executionMode = ExecutionMode.InitializeFromDatabase;
```
2. Run the sample and verify that it successfully runs to completion.

### Run sample code locally using remote configuration database, remote AdventureWorksDW database, and remove Analysis service
1. Deploy the AdventureWorksDW database (that was restored from the repo's backup file) to an Azure SQL database.
2. Update AdventureWorks tabular model to point to the remote AdventureWorksDW database and Azure Analysis service
- Edit the model's data source from local to the remote AdventureWorksDW; be sure to use "Database" connection type.
- Right-click the project and change the server to the Azure Analysis service
- Publish the model to azure
3. Deploy the configuration database to Azure
- Right-click the ConfigrationLogging project, select "properties", and change the "Target platform" to "Azure SQL Database"
2. Right-click the CofigurationLogging project, select "publish". Edit the "Target database connection" using your Azure SQL Database connection info.
4. In the newly deployed configuration database, update the ModelConfiguration record to use 
5. Run the sample and verify that it successfully runs to completion.

### Run sample code locally using remote configuration database and Azure Analysis service
1. 
