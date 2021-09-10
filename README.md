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

1. You should have 2 secrets generated for this repo:

| Secret Name | Value Required |
|-------------      |--------------- |
|AKS_CLUSTER_NAME             | AKS Cluster name |
|AKS_CLUSTER_RESOURCE_GROUP   | Resource Group that contains the AKS Cluster  |


## How to Demo
1. Open project in Codespaces or VS Code
2. Use `docker-compose build` and `docker-compose up` commands to show off the application
3. Create a new branch, 
    - modify `azure-vote/azure-vote/config_file.cfg` to update homepage values
1. Create a PR, utilize review-lab keyword comment - if desired.
1. Show AKS Cluster to demonstrate any namespace updates/changes.
1. Merge PR, observe that **Cleanup PR** and **AKS Staging & Production - Deploy** workflows kick off
1. View Staging and Production environment deployments

# Additional Features/Scenarios

## Environments

## ACR
The Azure Container Registry be added as part of the deployment process to showcase a multi-registry approach.

Create an Azure container registry and generate a username and password as seen in the following [guide](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-github-action).
  - Set the corresponding output as repo secret: `REGISTRY_USERNAME`
  - Set the corresponding output as repo secret: `REGISTRY_PASSWORD`

See `.github/example-workflows/` for an example. 

## AKS Staging and Production DNS URLs
AKS namespaces generated will produce an external IP Address, if you would like to use a prettier url for persistent namespaces such as 'staging' and 'production'.

Utilize the 'Public IP Address' resource configurations for adding an **Alias record set**:
- https://docs.microsoft.com/en-us/azure/dns/dns-alias

See `.github/example-workflows/` for an example. 

## Microsoft Teams Integration
The GitHub and Microsoft Teams integration can be used to show case chatops functionality.

In a Microsoft Teams channel, setup a connector for 'Incoming Webhook' and copy the generated 'webhook url'.
- https://docs.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/connectors-using#setting-up-a-custom-incoming-webhook

See `.github/example-workflows/` for an example. 

## Advanced Security - Code Scanning

# Azure Voting App

This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster. The application interface has been built using Python / Flask. The data component is using Redis.

To walk through a quick deployment of this application, see the AKS [quick start](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough?WT.mc_id=none-github-nepeters).

To walk through a complete experience where this code is packaged into container images, uploaded to Azure Container Registry, and then run in and AKS cluster, see the [AKS tutorials](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app?WT.mc_id=none-github-nepeters).

# Troubleshooting / Limitations

## Manifest File
Currently the `manifests/deployment.yml` file needs to have the `azure-vote-front` **image** value updated to match your repository.

## Available resources for multiple namespaces
For demo purposes, the manifest files only ask for 1 replica for the services. Multiple replicas or namespaces (5+) may hit resource limitations for your AKS cluster.
