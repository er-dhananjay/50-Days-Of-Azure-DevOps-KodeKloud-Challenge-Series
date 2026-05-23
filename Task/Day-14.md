# Day 14 – Create and Attach Managed Disks in Azure

---

## Task Overview  

The Nautilus DevOps team is working on improving cloud storage management and infrastructure scalability in Azure. As part of this task, a managed disk needs to be created and attached to an Azure Virtual Machine.

Managed disks provide scalable, durable, and highly available storage for Azure Virtual Machines.

The task includes:

- Creating a managed disk
- Configuring disk type and size
- Understanding managed disk storage options
- Attaching disks to Virtual Machines
- Verifying disk attachment

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud infrastructure resources.

---

### Step 2: Open Disks Service  

Search for:

| Search |
|---|
| Disks |

Open the **Disks** service.

#### Explanation  
The Disks service is used to create and manage managed disks for Azure Virtual Machines.

---

### Step 3: Create a Managed Disk  

Click:

- **Create**

Configure the following settings:

| Property | Value |
|---|---|
| Disk Name | `devops-disk` |
| Region | `southcentralus` |
| Disk Type | `Standard_LRS` |
| Disk Size | `2 GiB` |

Click:

- **Review + Create**
- **Create**

#### Explanation  
This creates a new managed disk resource in Azure with the specified storage configuration.

---

### Step 4: Wait for Deployment Completion  

Monitor deployment status until:

| Property | Expected Value |
|---|---|
| Deployment Status | Succeeded |

#### Explanation  
Azure provisions and initializes the managed disk resource.

---

### Step 5: Open Virtual Machines Service  

Search for:

| Search |
|---|
| Virtual machines |

Open the **Virtual machines** service.

#### Explanation  
This section contains all Azure Virtual Machines available in the subscription.

---

### Step 6: Open the Existing Virtual Machine  

Select the target Virtual Machine.

Example:

| Virtual Machine |
|---|
| `devops-vm` |

#### Explanation  
This opens the management page of the Virtual Machine.

---

### Step 7: Open Disks Section  

From the left-side menu, open:

- **Disks**

#### Explanation  
The Disks section is used to manage OS disks and attached data disks.

---

### Step 8: Attach Existing Managed Disk  

Under:

- **Data disks**

Click:

- **Attach existing disks**

Select the created managed disk.

Example:

| Disk Name |
|---|
| `devops-disk` |

Click:

- **Save**

#### Explanation  
This attaches the managed disk to the Azure Virtual Machine as a data disk.

---

### Step 9: Verify Disk Attachment  

Go to:

- **VM → Disks**

Verify:

| Property | Expected Value |
|---|---|
| Disk Name | `devops-disk` |
| Status | Attached |

#### Explanation  
This confirms the managed disk is successfully attached to the Virtual Machine.

---

## Best Practices  

- Use managed disks for better scalability and reliability  
- Separate OS and application data disks  
- Use appropriate disk types based on workload requirements  
- Monitor disk performance and utilization regularly  
- Use meaningful naming conventions for Azure resources  
- Plan backup and disaster recovery strategies for critical storage  

---

## Key Learnings  

- Managed disks simplify storage management in Azure  
- Azure handles disk availability and durability automatically  
- Data disks can be attached dynamically to Virtual Machines  
- Managed disks improve scalability and operational efficiency  
- Azure storage resources are independently manageable  
- Proper storage planning improves cloud infrastructure performance and reliability  

---

Step by step, improving cloud infrastructure and DevOps skills 🚀
