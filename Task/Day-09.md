# Day 09 – Attach Network Interface Card (NIC) to Azure Virtual Machine

---

## Task Overview  

The Nautilus DevOps team is working on improving cloud networking and VM connectivity in Azure. As part of this task, an additional Network Interface Card (NIC) needs to be attached to an existing Azure Virtual Machine.

An existing Virtual Machine and an existing NIC are already available in Azure.

- Stop the Virtual Machine before making networking changes.
- Attach the existing NIC to the target Virtual Machine.
- Start the VM after configuration.
- Verify that the NIC is successfully attached.

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud resources such as Virtual Machines, Networking, Storage, and Security.

---

### Step 2: Open Virtual Machines Service  

In the top search bar search for:

| Search |
|---|
| Virtual machines |

Open the **Virtual machines** service.

#### Explanation  
The Virtual Machines section contains all VMs available in the Azure subscription.

---

### Step 3: Open the Existing Virtual Machine  

Select the target VM from the list.

Example:

| Virtual Machine |
|---|
| `devops-vm` |

#### Explanation  
This opens the configuration and management page of the Virtual Machine.

---

### Step 4: Stop (Deallocate) the Virtual Machine  

Click:

- **Stop**

Wait until the VM status changes to:

| Property | Expected Value |
|---|---|
| Status | Stopped (deallocated) |

#### Explanation  
Azure requires the VM to be deallocated before attaching or detaching additional NICs.

---

### Step 5: Open Networking Section  

From the left-side menu of the VM, open:

- **Networking**
- **Network settings**

#### Explanation  
This section is used to manage Network Interface Cards (NICs), IP addresses, NSGs, and connectivity settings.

---

### Step 6: Attach Existing NIC  

Click:

- **Attach network interface**

Select the existing NIC from the dropdown list.

Example:

| NIC |
|---|
| `devops-nic` |

Click:

- **OK**
- **Save**

#### Explanation  
This attaches the selected Network Interface Card to the Virtual Machine.

---

### Step 7: Start the Virtual Machine  

After NIC attachment is completed, click:

- **Start**

Wait until the VM status becomes:

| Property | Expected Value |
|---|---|
| Status | Running |

#### Explanation  
The VM must be restarted after network configuration changes.

---

### Step 8: Verify NIC Attachment  

Go to:

- **VM → Networking**

Verify the additional NIC appears in the attached network interfaces list.

| Property | Expected Value |
|---|---|
| NIC Status | Attached |

#### Explanation  
This confirms the NIC was successfully attached to the Virtual Machine.

---

## Best Practices  

- Stop (deallocate) Azure VMs before modifying NIC configurations  
- Use separate NICs for traffic isolation and better network management  
- Assign meaningful names to NIC resources  
- Use NSGs to secure network traffic  
- Monitor NIC bandwidth and traffic patterns regularly  
- Avoid unnecessary public IP exposure  

---

## Key Learnings  

- Azure VMs support multiple Network Interface Cards  
- VMs must be deallocated before attaching additional NICs  
- NICs improve traffic management and network isolation  
- Azure networking resources can be managed dynamically  
- Proper NIC configuration improves scalability and security  
- Networking is a critical component of cloud infrastructure management  

---

Step by step, improving cloud networking and DevOps skills 🚀
