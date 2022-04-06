
description: "This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster."
---
Try quick start - TIME challenge record time 15 minutes for app, then delete resource group:

1st attempt 03apr22 19:17 took 21:25.67 to complete up to delete command

2nd attempt 03apr22 19:53 took 14:31:48 to delete commands

3rd attempt 03apr22 20:25 took 13:48:14 to delete commands

4th attempt 04apr22 00:30 took 15:09:09 to delete commands

5th attempt 06apr22 14:50 took 13:20:59 to delete commands

This is a shorter version of docs.microsoft.com/en-us/azure/aks/quickstart-helm so any modifications to the below, check the page. i.e. if the acr name is different then you must update  the name in azure-vote-front/values.yaml

az login

az group create --name myresourcegroup --location eastus

az acr create --resource-group myresourcegroup --name myhelmacrjm --sku Basic

az aks create --resource-group myresourcegroup --name myaks --location eastus --attach-acr myhelmacrjm --generate-ssh-keys

az aks get-credentials --resource-group myresourcegroup --name myaks

git clone https://github.com/tradexy/azure-vote-front.git

cd azure-vote-front/azure-vote/

az acr build --image azure-vote-front:v1 --registry myhelmacrjm --file Dockerfile .

helm install azure-vote-front azure-vote-front/

kubectl get --namespace default svc -w azure-vote-front

use external IP to see the App

az group delete --name myresourcegroup --yes --no-wait

az group delete --name MC_myresourcegroup_myaks_eastus --yes --no-wait

stop the clock

(remember to check 2 resource groups in portal and delete both - it maybe that the MC_MyRes.. is deleted when MyRes.. is deleted))

# Azure Voting App

---
page_type: sample
languages:
  - python
products:
  - azure
  - azure-redis-cache

This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster and deployed using Helm. The application interface has been built using Python / Flask. The data component is using Redis.

To walk through a quick deployment of this application, see the AKS [quick start](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough?WT.mc_id=none-github-nepeters).

For more see the [AKS tutorials](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app?WT.mc_id=none-github-nepeters).

