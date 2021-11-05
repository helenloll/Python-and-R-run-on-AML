# Running Python and R in Azure ML Compute - examples


[![license: MIT](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)



## Prerequisites

1. An Azure ML Workspace
2. For CLI based submit : Terminal with Azure ML CLI v2 installed : https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-cli
3. For python based submit: A terminal with Python and Azure ML SDK >=3.6,[\<3.9](https://pypi.org/project/azureml-core)

Terminal is for example any computer on Azure cloud like DSVM, AML Compute Instance, worstation.

## Run Python and R models with CLI v2 
- Step by step explanation how to run Python with CLI v2 on Azure ML Compute https://docs.microsoft.com/en-us/azure/machine-learning/how-to-train-cli
- Complete repository of examples is here https://github.com/Azure/azureml-examples/tree/main/cli#prerequisites 

### Python models with CLI v2
Run in terminal with Azure CLI:
- az ml job create -f workflows/lightgbm/iris/job.yml --web
- az ml job create -f workflows/lightgbm/iris/job-sweep.yml --web

#### Python models with CLI v2 launched via GitHub Actions 
- .github/worklows/run-iris-lightgbm.yml

### R models with CLI v2
Run in terminal with Azure CLI:
- az ml job create -f workflows/r/iris/job.yml --web
- az ml job create -f workflows/r/accidents/job.yml --web

#### R models with CLI v2 launched via GitHub Actions 
- .github/worklows/run-r-accidents.yml
- .github/worklows/run-r-iris.yml


## Python models with Python AzureML SDK
Complete repository of examples is https://github.com/Azure/azureml-examples/tree/main/python-sdk
Azure ML SDK libraries here https://github.com/Azure/azureml-examples/tree/main/python-sdk

Run in Python terminal with libraries in   
- workflows/basic/job.py is the AML control code

These are:
- workflows/basic/requirements.txt specifies required pip packages for the training script
- workflows/basic/src/train.py is the ML training script with mlflow tracking

#### Python models with Python AzureML SDK launched via GitHub Actions 
- .github/worklows/run-python-based.yml

## Git Hub Actions 
### Setup Azure cerdentials for GitHub Actions
In this repository is a resource group named `helenloll`, a workspace named `helenloll`, and a cluster named `cpu-cluster`. 

Create a service principal for the resource group, which is used in GitHub Actions as user/principal to access resources:

```console
az ad sp create-for-rbac --name "helenloll-principal" \
                         --role contributor \
                         --scopes /subscriptions/<your-subscription-id>/resourceGroups/helenloll \
                         --sdk-auth
```

Copy the output json, which looks like this:

```console
{
    "clientId": "<GUID>",
    "clientSecret": "<GUID>",
    "subscriptionId": "<GUID>",
    "tenantId": "<GUID>",
    (...)
}
```

In your repository, navigate to "Settings > Secrets > New Secret". Name the secret `AZ_CREDS` and paste the json output from above. This is used in the Azure login action in the GitHub Actions. If you use a different name for the secret, ensure you change the corresponding names in the `.github/workflows` files.

For complete explanations of various GitHub Actions see here https://github.com/Azure/aml-template 

## Reference

- [Azure Machine Learning Documentation](https://docs.microsoft.com/azure/machine-learning)
