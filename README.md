
description: "This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster."
---
Try quick start - TIME challenge record time 15 minutes for app, then delete resource group:

1st attempt 03apr22 19:17 took 21:25.67 to complete up to delete command

2nd attempt 03apr22 19:53 took 14:31:48 to delete command

3rd attempt 03apr22 20:25 took 13:48:14 to delete command

4th attempt 04apr22 00:30 took 15:09:09 to delete command

5th attempt 06apr22 14:50 took 13:20:59 to delete command

6th attempt 10apr22 09:45 took 10:10:37 to delete command

7th attempt 21apr22 21:00 took 09:48:53 to delete command (chromebook)

8th attempt 01Jul22 16:00 took 20:00:00 to delete command (w)

This is a shorter version of docs.microsoft.com/en-us/azure/aks/quickstart-helm so any modifications to the below, check the page. i.e. if the acr name is different then you must update  the name in azure-vote-front/values.yaml

az login

az group create --name atestcluster --location uksouth

az acr create --resource-group atestcluster --name testacrjm --sku Basic

az aks create --resource-group atestcluster --name myaks --location uksouth --attach-acr testacrjm --generate-ssh-keys

az aks get-credentials --resource-group atestcluster --name myaks

git clone https://github.com/tradexy/azure-vote-front.git

cd azure-vote-front/azure-vote/

az acr build --image azure-vote-front:v1 --registry testacrjm --file Dockerfile .

helm install azure-vote-front azure-vote-front/

kubectl get --namespace default svc -w azure-vote-front

use external IP to see the App

az group delete --name atestcluster --yes --no-wait

az group delete --name MC_testcluster_myaks_uksouth --yes --no-wait

stop the clock

(remember to check 2 resource groups in portal and delete both -  MC_myres.. should be deleted when myres.. is deleted))

helm practice:

(if necessary?) cd .\test\azure-vote-front\azure-vote\

helm status azure-vote-front

[make changes to helm file, i.e. replica]

helm upgrade azure-vote-front azure-vote-front

helm get values azure-vote-front --all

[check get pods....]

helm upgrade azure-vote-front azure-vote-front --set replicaCount=5

helm get values azure-vote-front

helm rollback azure-vote-front 2

helm history azure-vote-front

helm get manifest azure-vote-front![image](https://user-images.githubusercontent.com/31375255/176990636-adf8de82-a6b7-4f2a-9dda-a1ecf48afe24.png)


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

