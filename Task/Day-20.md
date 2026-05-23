# Day 20 – Deploy Azure Resources Using ARM Templates

---

## Task Overview  

The Nautilus DevOps team is working on automating cloud infrastructure deployment in Azure using Infrastructure as Code (IaC). As part of this task, Azure resources are deployed and managed using ARM Templates and Azure CLI.

Azure Resource Manager (ARM) Templates help standardize and automate resource provisioning in Azure environments.

The task includes:

- Modifying and deploying ARM Templates
- Creating and updating Azure resources
- Managing Virtual Networks
- Updating resource properties and tags
- Using Azure CLI for deployment and verification
- Understanding Infrastructure as Code concepts

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud infrastructure resources.

---

### Step 2: Connect to Azure Using Azure CLI  

Open terminal or Azure Cloud Shell.

Login using Azure CLI:

```bash
az login
