---
page_type: sample
languages:
  - python
products:
  - azure
  - azure-redis-cache
description: "This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster."
---
# Demo Prep / Setup
**This repo was created from the [demo-bootstrap](https://github.com/octodemo/demo-bootstrap) orchestrator.*

This repo will demonstrate using AKS, GitHub Codespaces, Actions, Environments, and GitHub Container Registry.

Leveraged tutorials/content from Microsoft Docs:
- [Tutorial: Prepare an application for Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app)
- [GitHub Actions for deploying to Kubernetes service](https://docs.microsoft.com/en-us/azure/aks/kubernetes-action)

## Prerequisites

1. This demo requires 3 secrets to be generated:

| Secret Name | Value Required |
|-------------      |--------------- |
|AKS_CLUSTER_NAME             | AKS Cluster name |
|AKS_CLUSTER_RESOURCE_GROUP   | Resource Group that contains the AKS Cluster  |
|AZURE_SERVICE_PROVIDER_CREDENTIALS   | SP with permission to access the Azure Resource Group |


## How to Demo
1. Open project in Codespaces or VS Code
2. Use `docker-compose build` and `docker-compose up` commands to show off the application
3. Create a new branch, 
    - modify `azure-vote/azure-vote/config_file.cfg` to update homepage values
1. Create a PR, utilize review-lab keyword comment - if desired.
1. Show AKS Cluster to demonstrate any namespace updates/changes.
1. Merge PR, observe that **Cleanup PR** and **AKS Staging & Production - Deploy** workflows kick off
1. View Staging and Production environment deployments


# Azure Voting App

This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster. The application interface has been built using Python / Flask. The data component is using Redis.

To walk through a quick deployment of this application, see the AKS [quick start](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough?WT.mc_id=none-github-nepeters).

To walk through a complete experience where this code is packaged into container images, uploaded to Azure Container Registry, and then run in and AKS cluster, see the [AKS tutorials](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app?WT.mc_id=none-github-nepeters).

# Troubleshooting / Limitations

## Manifest File
Currently the `manifests/deployment.yml` file needs to have the `azure-vote-front` **image** value updated to match your repository.

## Available resources for multiple namespaces
For demo purposes, the manifest files only ask for 1 replica for the services. Multiple replicas or namespaces (5+) may hit resource limitations for your AKS cluster.
