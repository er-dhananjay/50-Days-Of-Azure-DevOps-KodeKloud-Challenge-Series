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
```

#### Explanation  

The `az login` command authenticates your Azure account and allows CLI-based resource management.

---

### Step 3: Verify Azure Subscription  

Check available subscriptions:

```bash
az account list --output table
```

Set the required subscription:

```bash
az account set --subscription "Azure Free Labs"
```

#### Explanation  

This ensures all deployments are performed under the correct Azure subscription.

---

### Step 4: Create a Resource Group  

Create a new Resource Group:

```bash
az group create \
--name devops-rg \
--location eastus
```

#### Explanation  

A Resource Group acts as a logical container for Azure resources.

---

### Step 5: Create ARM Template File  

Create a file named `azuredeploy.json`:

```bash
vi azuredeploy.json
```

Example ARM Template:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "resources": [
    {
      "type": "Microsoft.Network/virtualNetworks",
      "apiVersion": "2023-05-01",
      "name": "devops-vnet",
      "location": "eastus",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "10.0.0.0/16"
          ]
        },
        "subnets": [
          {
            "name": "default",
            "properties": {
              "addressPrefix": "10.0.1.0/24"
            }
          }
        ]
      }
    }
  ]
}
```

Save and exit.

#### Explanation  

ARM Templates use JSON format to define Azure infrastructure declaratively.

---

### Step 6: Deploy ARM Template  

Deploy the ARM Template:

```bash
az deployment group create \
--resource-group devops-rg \
--template-file azuredeploy.json
```

#### Explanation  

This command deploys Azure resources defined inside the ARM Template.

---

### Step 7: Verify Deployment  

Check deployment status:

```bash
az deployment group list \
--resource-group devops-rg \
--output table
```

Verify Virtual Network:

```bash
az network vnet list \
--output table
```

#### Explanation  

Verification ensures resources were successfully deployed.

---

### Step 8: Update Resource Tags  

Add tags to resources:

```bash
az tag create \
--resource-id $(az network vnet show \
--resource-group devops-rg \
--name devops-vnet \
--query id -o tsv) \
--tags Environment=DevOps Project=ARM
```

#### Explanation  

Tags help organize and manage Azure resources efficiently.

---

### Step 9: Modify ARM Template and Redeploy  

Update resource properties inside `azuredeploy.json`.

Example:

- Add another subnet
- Change address ranges
- Update tags

Redeploy template:

```bash
az deployment group create \
--resource-group devops-rg \
--template-file azuredeploy.json
```

#### Explanation  

ARM Templates support idempotent deployments, meaning existing resources are updated safely.

---

## Best Practices  

- Use Infrastructure as Code for repeatable deployments  
- Store ARM Templates in Git repositories  
- Use parameter files for reusable deployments  
- Apply tagging standards for resource management  
- Validate templates before deployment  
- Use least privilege access principles  

---

## Key Learnings  

- ARM Templates automate Azure infrastructure deployment  
- Azure CLI simplifies deployment and management tasks  
- Infrastructure as Code improves consistency and scalability  
- Resource Groups organize Azure resources efficiently  
- Tags improve resource visibility and governance  
- Declarative templates reduce manual configuration errors  

---

Step by step, improving Azure automation and DevOps skills 🚀
