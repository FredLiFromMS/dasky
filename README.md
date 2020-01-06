# Azure ML and Dask 

![Summary gif](media/describe.gif)

## Introduction

Dask is awesome. Azure ML is cool too. 

## Data overview

The data is hosted at https://data4dask.dfs.core.windows.net/datasets/noaa/isd. It is a copy of the [NOAA Integrated Surface Data (ISD)](https://azure.microsoft.com/services/open-datasets/catalog/noaa-integrated-surface-data/) moved from [Azure Open Dataset](https://azure.microsoft.com/services/open-datasets/catalog/) to a ADLS Gen 2 filesystem for distributed processing. 

Expanded in memory, the full dataset is ~660 GB. It is stored in compressed parquet files in a blob container partitioned by year and month. The dataset is **not** updated in the ADLS Gen 2 storage account, but is in the Azure Open Dataset. Compressed, the files for the dataset are ~8 GB. Uncompressed, the files for the dataset are ~150-200 GB.  

The parition format is `year=*/month=*/part-*.snappy.parquet` with 1 file per month. Each file can contain ~5 GB of data when in a dataframe in memory. Compressed, each file is ~50 MB. Uncompressed, each file is ~1 GB. 

## Create a virtual network 

Create or use an existing virtual network (vNET). Both the interface for the Dask cluster and the cluster itself will be in the virtual network. You can quickly create one in the [Azure Portal](https://docs.microsoft.com/en-us/azure/virtual-network/quick-create-portal) or [Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-network/quick-create-cli) if you do not have one already.

In the `example.ipynb` notebook, the vNET is assumed to be in the same resource group as the workspace with a name 'dialup-network' and subnet 'default'. 

## Create and setup compute instance 

Create an Azure ML Compute Instance in the vNET you have created.

Enabling SSH access is optional.

![Compute instance creation](media/instance-create.png)

## Launch JupyterLab or Jupyter

Launch JupyterLab (recommended) or Jupyter from the list of URIs. 

![Compute instance URIs](media/instance-launch.png)

## Clone repository

Navigate to a directory of your choice and clone repo from github. 

You can use the terminal or UI to clone the repo, hosted at https://github.com/lostmygithubaccount/dasky.git. Copy this link and clone the repo.

![Compute instance github](media/instance-github.png)

## Repository overview

![Compute instance repo](media/instance-repo.png)


