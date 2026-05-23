# Day 13 – SSH into an Azure Virtual Machine

---

## Task Overview  

The Nautilus DevOps team is working on secure remote administration and cloud access management in Azure. As part of this task, secure SSH access needs to be configured for an Azure Linux Virtual Machine.

The task includes:

- Connecting to the Azure VM using SSH
- Configuring SSH key-based authentication
- Managing root user SSH access
- Adding SSH public keys to authorized_keys
- Setting proper file permissions
- Troubleshooting SSH and cloud-init restrictions

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud resources.

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

### Step 3: Locate the Linux Virtual Machine  

Select the target Virtual Machine.

Example:

| Virtual Machine |
|---|
| `devops-vm` |

#### Explanation  
This opens the management page of the Linux VM.

---

### Step 4: Connect to VM Using SSH  

From the VM overview page, obtain the Public IP address.

Use SSH from the terminal:

```bash
ssh azureuser@<public-ip>
