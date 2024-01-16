# energy-azure-data-factory
check this blog for more information

https://medium.com/@waranlokesh84/energy-prediction-using-azure-data-factory-and-azure-ml-49749f90c1d5

## Project Overview

This project aims to develop an energy prediction model for prosumers, focusing on minimizing energy imbalance costs. The complete workflow involves data engineering, machine learning, and model deployment. Below is a detailed guide on the project structure, data flow, and steps to reproduce the results.

### Kaggle Competition Details

The problem statement and dataset for this project are outlined in the Kaggle competition named "Enefit - Predict Energy Behavior of Prosumers." For more details, please refer to [Kaggle - Predict Prosumer Energy Patterns](www.kaggle.com).


## Data Engineering and ML Workflow

### Step 1: Upload Dataset to Google Drive

- Upload the Kaggle competition dataset to Google Drive.
- Ensure file access is set to public.

### Step 2: Ingest Data to Azure Data Lake using Azure Data Factory

1. Create a Blob Storage account with hierarchical namespace option.
2. Create a container named "energydata" with two folders: "rawdata" and "transformeddata."
3. Set up an Azure Data Factory workspace.
4. Create HTTP and Data Lake linked services.
5. Develop a pipeline to ingest and copy data from Google Drive to Azure Data Lake.
6. Configuration details are available in the [Azure Data Factory folder](https://github.com/lokeshwaran97/energy-azure-data-factory/tree/main/azure_data_factory).

### Step 3: Preprocess Data using Azure Databricks

1. Set up an Azure Databricks workspace and create a compute.
2. Mount data from Azure Data Lake to Azure Databricks.
3. Create an app registration and obtain client & secret ID.
4. Provide API permissions for the app to access Azure Storage and Azure Data Lake.
5. Utilize PySpark for data preprocessing.
6. Code for mounting and preprocessing data can be found in the [Azure Databricks folder](https://github.com/lokeshwaran97/energy-azure-data-factory/tree/main/azure_data_bricks).

### Step 4: Create Azure Machine Learning Workspace

1. Establish an Azure Machine Learning workspace.
2. Connect Azure ML to Azure Data Storage.
3. Grant Azure ML data scientist role permission for the app to access Azure ML workspace.
4. Use Python SDK to create a connection to Azure Data Store.
5. Python code for creating the connection is available in the [Azure ML Data Connection folder](https://github.com/lokeshwaran97/energy-azure-data-factory/blob/main/azure_ml_data_connection/energy_ml_datastore_connection.ipynb).

### Step 5: Train ElasticNet Regression Model using Azure ML

1. Create a compute in the Azure Machine Learning workspace.
2. Develop a notebook in Azure ML workspace for processing and training the ElasticNet regression model.
3. Create a pipeline to automate the process and log model parameters using MLflow.
4. Python notebook code for model training is available in the [Azure ML Training folder](https://github.com/lokeshwaran97/energy-azure-data-factory/blob/main/azure_ml_training/energy_prediction_ml.ipynb).

### Post-Processing and Hyperparameter Tuning

- Evaluate model performance in the job overview tab after pipeline execution.
- Adjust hyperparameters in the train-model.yml file for further model training.
- Note: The process_data pipeline is not recomputed if hyperparameters are changed, as processed data is stored in the ML workspace.




