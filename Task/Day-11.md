# Day 11 – Change Azure Virtual Machine Size Using Console

---

## Task Overview  

The Nautilus DevOps team is working on optimizing cloud infrastructure resources in Azure. As part of this task, an existing Azure Virtual Machine needs to be resized to a larger VM size.

The Virtual Machine currently uses the `Standard_B1s` size and needs to be upgraded to `Standard_B2s`.

- Stop (deallocate) the Virtual Machine before resizing
- Change the VM size
- Restart the Virtual Machine after configuration
- Verify the updated VM size

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based management interface used to manage cloud resources.

---

### Step 2: Open Virtual Machines Service  

Search for:

| Search |
|---|
| Virtual machines |

Open the **Virtual machines** service.

#### Explanation  
This section contains all Virtual Machines available in the Azure subscription.

---

### Step 3: Open the Existing Virtual Machine  

Select the target Virtual Machine.

Example:

| Virtual Machine |
|---|
| `devops-vm` |

#### Explanation  
This opens the management page of the selected Virtual Machine.

---

### Step 4: Stop (Deallocate) the Virtual Machine  

Click:

- **Stop**

Wait until the VM status changes to:

| Property | Expected Value |
|---|---|
| Status | Stopped (deallocated) |

#### Explanation  
Azure requires a VM to be deallocated before changing its size to ensure safe hardware resource reallocation.

---

### Step 5: Open Size Configuration  

From the left-side menu, open:

- **Size**

#### Explanation  
The Size section allows changing CPU, RAM, and performance configurations of the Virtual Machine.

---

### Step 6: Change VM Size  

Search and select:

| Current Size | New Size |
|---|---|
| Standard_B1s | Standard_B2s |

Click:

- **Resize**

#### Explanation  
This upgrades the Virtual Machine resources to the selected VM size.

---

### Step 7: Start the Virtual Machine  

After resizing completes, click:

- **Start**

Wait until the VM status becomes:

| Property | Expected Value |
|---|---|
| Status | Running |

#### Explanation  
The Virtual Machine must be restarted after resizing to apply the updated hardware configuration.

---

### Step 8: Verify Updated VM Size  

Go to:

- **Virtual Machine → Overview**

Verify:

| Property | Expected Value |
|---|---|
| VM Size | Standard_B2s |

#### Explanation  
This confirms the VM size was successfully updated.

---

## Best Practices  

- Always deallocate VMs before resizing  
- Choose VM sizes based on workload requirements  
- Monitor CPU and memory utilization regularly  
- Avoid overprovisioning resources unnecessarily  
- Use cost-effective VM sizes for development environments  
- Scale resources according to application demand  

---

## Key Learnings  

- Azure Virtual Machines can be resized dynamically  
- VM resizing requires deallocation before changes  
- VM sizes determine CPU, RAM, and performance capacity  
- Azure provides flexible infrastructure scaling options  
- Proper VM sizing improves cost optimization and performance  
- Cloud infrastructure can be managed efficiently through the Azure Portal  

---

Step by step, improving cloud management and DevOps skills 🚀
