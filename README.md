# energy-azure-data-factory
check this blog for more description

https://medium.com/@waranlokesh84/energy-prediction-using-azure-data-factory-and-azure-ml-49749f90c1d5

The problem is to create a energy prediction model of prosumers to reduce energy imbalance costs. check the below kaggle link for more description about the data and problem statement.

Data engineering and ML flowchart

Step 1 : Upload the dataset to google drive

The data from the kaggle competiton is uploaded to my google drive and changed the file access to public

Step 2 : Ingest data from google drive to azure data lake using Azure Data Factory

i) create a blob storage account with hierarchical namespace option

ii) create a container called “energydata” in the storage account

iii) create two folders “rawdata” and “transformeddata”. The “rawdata” folder is used to store the ingested data and the “transformeddata” is used to stored the processed data using rawdata.

iv) create a Azure Data Factory workspace.

create a HTTP linked service to ingest data from google drive

create Data Lake linked service to store the ingested data in data lake

create a pipeline to ingest and copy data using created linked service as source and sink

Step 3 : create a azure databricks workspace and create a compute

The data from the datalake were mounted to azure databricks and the data were preprocessed using pyspark. The preprocessed data is stored in “transformeddata” Azure data lake folder

create an app registration and create client & secret id. we have to use this app to connect data lake to data bricks.

Give api permission for “energyapplication” app to access azure storage and azure data lake

Use the appid , clientsecret, tenant id of app and azure data lake container name and storage account name to mount azure data lake to azure data bricks

Go to the storage container and give “energyapplication” app Storage Blob Data Contributor permission. This permission gives “energyapplication” to access energydata Data lake container.

Step 4: create azure machine learning workspace.

In order to access data for azure ML workspace we have to connect azure ml to azure data storage.

Before that we have to give Azure ML data scientist role permission for “energyapplication” to access azure ml workspace. with the help of “energyapplication” app we can use python sdk to create connection to azure ml workspace

I have used phython SDK to create datastore which copies the data from data lake. below is the python code to create connection to azure data store using azure ml client

create a compute in azure machine learning workspace with below configuration

create notebook in azure ml workspace. create a pipeline to process and train ElasticNet regression model and log the model and parameters using ML flow. Below is the python notebook code.

After the pipeline job we can check the evaluation metrics in job overview tab. we can again train the model with different hyper parameters by changing the train-model.yml files. The process_data pipeline will not run if we change hyperparameter because the processed data is stored in ml workspace. Hence process_data pipeline is not computed again.


