---
page_type: sample
languages:
  - python
products:
  - azure
  - azure-redis-cache
description: "This sample creates a multi-container application in an Azure Kubernetes Service (AKS) cluster."
---
# GitHub Demo Day

This demo is part of the GitHub Demo Day sessions hosted weekly! 
- [Demo Days - From A(KS) to Z, automate your workflows with GitHub!](https://www.linkedin.com/events/demodays-keepcalmanddevopson6838532958866022401/)
- Friday - Sep 10, 2021

We will use this repo to see how GitHub can simplify security, automation, container management, K8s deployments and more!

## Prerequisites

1. This demo requires 3 secrets to be generated:

| Secret Name | Value Required |
|-------------      |--------------- |
|AKS_CLUSTER_NAME                     | AKS Cluster name |
|AKS_CLUSTER_RESOURCE_GROUP           | Resource Group that contains the AKS Cluster  |
|AZURE_SERVICE_PROVIDER_CREDENTIALS   | SP with permission to access the Azure Resource Group |
|GH_ENV_PAT                           | PAT with repo admin access | 

### Generate Azure Service Principal
To deploy to Azure you will need to create a service principal. You can do that with the following command:

```sh
az ad sp create-for-rbac --name {yourServicePrincipalName} --role contributor \
                            --scopes /subscriptions/{subscription-id} \
                            --sdk-auth

  # Replace {yourServicePrincipalName}, {subscription-id} with the a service principal name and subscription id.

  # The command should output a JSON object similar to the example below

  {
    "clientId": "<GUID>",
    "clientSecret": "<GUID>",
    "subscriptionId": "<GUID>",
    "tenantId": "<GUID>",
    (...)
  }
```

## How to Demo
1. Open project in Codespaces or VS Code
2. Use `docker-compose build` and `docker-compose up` commands to show off the application locally
  - Navgate to http://localhost:8080
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

# References

## Microsoft Teams
GitHub is the world's leading software development platform. Microsoft Teams is one of the most popular communication platforms where modern development teams come together to build world-class products and services. With two of your most important workspaces connected, you'll stay updated on what's happening on GitHub without leaving Microsoft Teams.
- https://github.com/integrations/microsoft-teams

## GitHub Actions
Environments - You can configure environments with protection rules and secrets. When a workflow job references an environment, the job won't start until all of the environment's protection rules pass.
- https://docs.github.com/en/actions/reference/environments

## GitHub Container Registry
You can store and manage Docker and OCI images in the Container registry, which uses the package namespace https://ghcr.io.
- https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry