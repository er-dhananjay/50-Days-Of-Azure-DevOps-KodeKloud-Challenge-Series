# Day 10 – Attach Public IP to Azure Virtual Machine

---

## Task Overview  

The Nautilus DevOps team is working on improving external connectivity and networking for Azure Virtual Machines. As part of this task, a Public IP address needs to be attached to an Azure Virtual Machine.

An existing Virtual Machine and a Public IP resource are already available in Azure.

- Attach the existing Public IP to the target Virtual Machine.
- Configure the NIC IP settings properly.
- Verify that the Public IP is associated successfully.

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based management platform used to manage cloud resources.

---

### Step 2: Open Virtual Machines Service  

Search for:

| Search |
|---|
| Virtual machines |

Open the **Virtual machines** service.

#### Explanation  
This section contains all Azure Virtual Machines available in the subscription.

---

### Step 3: Open the Existing Virtual Machine  

Select the target Virtual Machine.

Example:

| Virtual Machine |
|---|
| `devops-vm` |

#### Explanation  
This opens the VM management and configuration page.

---

### Step 4: Open Networking Configuration  

From the left-side menu, open:

- **Networking**

Click the attached Network Interface Card (NIC).

#### Explanation  
Public IP addresses in Azure are attached through the NIC configuration, not directly from the VM.

---

### Step 5: Open IP Configurations  

Inside the NIC page, open:

- **IP configurations**

Select the existing IP configuration.

Example:

| IP Configuration |
|---|
| `ipconfig1` |

#### Explanation  
The IP configuration controls how the NIC handles private and public IP assignments.

---

### Step 6: Attach Public IP  

Under:

| Setting |
|---|
| Public IP address |

Select the existing Public IP resource.

Example:

| Public IP |
|---|
| `devops-public-ip` |

Click:

- **Save**

#### Explanation  
This associates the Public IP address with the Virtual Machine through the NIC configuration.

---

### Step 7: Verify Public IP Association  

Go back to:

- **Virtual Machine → Networking**

Verify:

| Property | Expected Value |
|---|---|
| Public IP | Attached |

#### Explanation  
This confirms the Virtual Machine is now associated with the Public IP address.

---

## Best Practices  

- Use Public IPs only when external access is required  
- Protect VMs using NSGs and firewall rules  
- Avoid exposing unnecessary ports to the internet  
- Use static Public IPs for production workloads when required  
- Monitor inbound and outbound traffic regularly  
- Use Bastion or VPN access for secure administration whenever possible  

---

## Key Learnings  

- Public IPs in Azure are attached via NIC IP configurations  
- NICs provide flexible networking management for VMs  
- Public IPs enable internet connectivity for Azure resources  
- Proper network security is essential when exposing VMs publicly  
- Azure networking resources are modular and independently manageable  
- Understanding NIC and IP configuration is important for cloud networking  

---

Step by step, improving cloud networking and DevOps skills 🚀
