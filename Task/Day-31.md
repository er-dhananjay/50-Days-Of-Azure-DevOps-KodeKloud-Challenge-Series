# Day 31 – Deploying and Managing a Web Application

---

## Task Overview  

The Nautilus DevOps team worked on deploying and managing a Python-based web application using Azure App Services. As part of this task, a Linux-based Azure Web App and App Service Plan were configured to host and manage cloud-native Python applications.

Azure App Services simplify web application deployment, scaling, monitoring, and infrastructure management in cloud environments.

The task includes:

- Creating Azure Web Apps
- Configuring Linux-based hosting environments
- Creating App Service Plans
- Selecting pricing and compute tiers
- Managing runtime stack configurations
- Disabling Application Insights
- Adding resource tags for organization
- Verifying web application deployment and status

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based management platform for cloud infrastructure and services.

---

### Step 2: Open App Services  

Search:

```text
App Services
```

Open:

```text
App Services
```

#### Explanation  

Azure App Services provide a managed platform for hosting web applications and APIs.

---

### Step 3: Create a New Web App  

Click:

```text
+ Create
```

Select:

```text
Web App
```

#### Explanation  

This opens the Azure Web App deployment wizard.

---

### Step 4: Configure Basic Settings  

Fill the required details:

| Field | Value |
|---|---|
| Subscription | Azure Free Labs |
| Resource Group | Existing Default Resource Group |
| Web App Name | `nautilus-webapp` |
| Publish | `Code` |
| Runtime Stack | `Python` |
| Operating System | `Linux` |
| Region | `West US` |

#### Explanation  

These settings define the application runtime environment and hosting region.

---

### Step 5: Create App Service Plan  

Under:

```text
App Service Plan
```

Click:

```text
Create new
```

Set:

| Field | Value |
|---|---|
| App Service Plan Name | `nautilus-learn-python` |

#### Explanation  

App Service Plans define the compute resources allocated to the web application.

---

### Step 6: Configure Pricing Tier  

Click:

```text
Explore pricing plans
```

Select:

| Tier | SKU |
|---|---|
| Basic | `B1` |

Click:

```text
Select
```

#### Explanation  

The Basic B1 plan provides affordable compute resources suitable for lightweight workloads.

---

### Step 7: Disable Application Insights  

Locate:

```text
Application Insights
```

Select:

```text
Disable
```

or

```text
No
```

#### Explanation  

Application Insights monitoring was intentionally disabled as per task requirements.

---

### Step 8: Configure Tags  

Open:

```text
Tags
```

Add:

| Name | Value |
|---|---|
| Name | `WebAppLearning` |
| Environment | `Dev` |

#### Explanation  

Tags help organize and manage Azure resources efficiently.

---

### Step 9: Review and Create  

Click:

```text
Review + create
```

Verify configuration:

| Setting | Expected Value |
|---|---|
| Web App Name | `nautilus-webapp` |
| App Service Plan | `nautilus-learn-python` |
| Runtime | Python |
| OS | Linux |
| Region | West US |
| SKU | Basic B1 |
| Application Insights | Disabled |

Click:

```text
Create
```

#### Explanation  

Azure validates and deploys the web application infrastructure.

---

### Step 10: Verify Web App Deployment  

Open:

```text
App Services
```

Select:

```text
nautilus-webapp
```

Verify:

| Property | Expected |
|---|---|
| State | `Running` |
| Runtime | Python |
| OS | Linux |
| Region | West US |

#### Explanation  

This confirms the successful deployment and operational status of the web application.

---

### Step 11: Verify Using Azure CLI  

Check Web App status:

```bash
az webapp show \
--name nautilus-webapp \
--resource-group kml_rg_main-048006e533884d12 \
--query "{Name:name,State:state,Location:location}" \
--output table
```

Expected output:

```text
Name               Location    State
-----------------  ----------  -------
nautilus-webapp    westus      Running
```

#### Explanation  

Azure CLI enables programmatic management and verification of Azure resources.

---

## Best Practices  

- Use Linux-based hosting for lightweight Python applications  
- Select appropriate App Service Plan tiers based on workload requirements  
- Use tags for resource organization and cost management  
- Disable unnecessary services when not required  
- Monitor application health and scalability regularly  
- Follow least privilege access principles  

---

## Key Learnings  

- Azure App Services simplify cloud web application hosting  
- App Service Plans define compute and scaling resources  
- Python applications can be deployed easily on Linux-based Azure environments  
- Azure Portal and Azure CLI support efficient cloud management  
- Resource tagging improves infrastructure organization and governance  
- Managed web hosting reduces operational overhead in DevOps workflows  

---

Step by step, improving Cloud and DevOps skills 🚀
