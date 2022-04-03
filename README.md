---
page_type: sample
languages:
  - python
products:
  - azure
  - azure-redis-cache
description: "This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster."
---
Try quick start - challenge record time 15 minutes for app, then delete resource group
az group create --name MyResourceGroup --location eastus

az acr create --resource-group MyResourceGroup --name MyHelmACRjm --sku Basic

az aks create --resource-group MyResourceGroup --name MyAKS --location eastus --attach-acr MyHelmACRjm --generate-ssh-keys

az login

az aks get-credentials --resource-group MyResourceGroup --name MyAKS

git clone https://github.com/tradexy/azure-vote-front.git

cd azure-voting-app-redis/azure-vote/

az acr build --image azure-vote-front:v1 --registry MyHelmACRjm --file Dockerfile .

helm create azure-vote-front

helm install azure-vote-front azure-vote-front/

kubectl get --namespace default svc -w azure-vote-front

use external IP to see the App

# Azure Voting App

This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster. The application interface has been built using Python / Flask. The data component is using Redis.

To walk through a quick deployment of this application, see the AKS [quick start](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough?WT.mc_id=none-github-nepeters).

To walk through a complete experience where this code is packaged into container images, uploaded to Azure Container Registry, and then run in and AKS cluster, see the [AKS tutorials](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app?WT.mc_id=none-github-nepeters).

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
