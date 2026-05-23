# Day 21 – Assigning Public IP to Azure Virtual Machines

---

## Task Overview  

The Nautilus DevOps team is working on configuring secure and accessible cloud infrastructure in Microsoft Azure. As part of this task, an Azure Virtual Machine needs to be deployed with a Static Public IP to allow stable and secure remote access over the internet.

Azure Public IP addresses help expose cloud resources externally while enabling administrators and applications to connect securely.

The task includes:

- Creating Azure Virtual Machines
- Configuring Static Public IP addresses
- Generating SSH key-based authentication
- Allowing secure remote SSH access
- Managing networking resources in Azure
- Understanding cloud networking concepts

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based management platform used to create and manage cloud resources.

---

### Step 2: Login Using Azure CLI  

Open Azure Cloud Shell or terminal.

Authenticate using Azure CLI:

```bash
az login
```

#### Explanation  

The `az login` command authenticates your Azure account and allows CLI-based management of Azure resources.

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

This ensures all resources are created under the correct Azure subscription.

---

### Step 4: Create a Resource Group  

Create a new Resource Group:

```bash
az group create \
--name devops-rg \
--location eastus
```

#### Explanation  

A Resource Group acts as a logical container for Azure resources such as Virtual Machines, Public IPs, and networking components.

---

### Step 5: Create a Virtual Network and Subnet  

Create a Virtual Network:

```bash
az network vnet create \
--resource-group devops-rg \
--name devops-vnet \
--subnet-name devops-subnet
```

#### Explanation  

The Virtual Network provides private networking for Azure resources, while the subnet logically separates resources inside the network.

---

### Step 6: Generate SSH Key Pair  

Generate SSH keys:

```bash
ssh-keygen -t rsa -b 4096
```

#### Explanation  

SSH keys provide secure passwordless authentication for Linux Virtual Machines.

---

### Step 7: Create a Static Public IP Address  

Create a Static Public IP:

```bash
az network public-ip create \
--resource-group devops-rg \
--name devops-public-ip \
--sku Standard \
--allocation-method Static
```

#### Explanation  

A Static Public IP ensures the VM always keeps the same external IP address.

---

### Step 8: Create Network Security Group Rule for SSH  

Allow SSH access on port 22:

```bash
az network nsg rule create \
--resource-group devops-rg \
--nsg-name devops-vmNSG \
--name Allow-SSH \
--protocol Tcp \
--priority 1000 \
--destination-port-range 22 \
--access Allow
```

#### Explanation  

Network Security Groups (NSGs) control inbound and outbound traffic for Azure resources.

---

### Step 9: Create Azure Virtual Machine  

Create an Ubuntu VM and associate the Static Public IP:

```bash
az vm create \
--resource-group devops-rg \
--name devops-vm \
--image Ubuntu2204 \
--admin-username azureuser \
--authentication-type ssh \
--ssh-key-values ~/.ssh/id_rsa.pub \
--public-ip-address devops-public-ip
```

#### Explanation  

This command creates the Azure VM and attaches the previously created Static Public IP.

---

### Step 10: Verify Public IP Address  

Retrieve the VM Public IP:

```bash
az vm list-ip-addresses \
--resource-group devops-rg \
--name devops-vm \
--output table
```

#### Explanation  

This verifies that the VM has been assigned the Static Public IP successfully.

---

### Step 11: Connect to the Virtual Machine Using SSH  

Connect to the VM:

```bash
ssh azureuser@<PUBLIC_IP>
```

#### Explanation  

SSH allows secure remote administration of Linux Virtual Machines over the internet.

---

## Best Practices  

- Use SSH key-based authentication instead of passwords  
- Use Static Public IPs for production services requiring fixed endpoints  
- Restrict SSH access using NSG rules and trusted IP ranges  
- Avoid exposing unnecessary ports publicly  
- Regularly monitor and audit Public IP usage  
- Apply least privilege security principles  

---

## Key Learnings  

- Azure Public IPs allow secure internet connectivity for cloud resources  
- Static Public IPs provide stable endpoints for applications and administration  
- Azure CLI simplifies Virtual Machine deployment and management  
- SSH keys improve security for remote Linux administration  
- Network Security Groups help control inbound access securely  
- Proper networking configuration is essential in cloud environments  

---

Step by step, improving Azure networking and DevOps skills 🚀
