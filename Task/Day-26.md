# Day 26 – Deploying Virtual Machines in Azure Public Virtual Network

---

## Task Overview  

The Nautilus DevOps team is working on deploying secure and scalable cloud infrastructure in Microsoft Azure. As part of this task, a Public Virtual Network (VNet) was created along with public subnets, Network Security Groups (NSGs), Static Public IPs, and an Ubuntu Virtual Machine accessible over the internet.

Public Virtual Networks allow cloud resources to communicate externally while maintaining controlled and secure access using NSGs and SSH authentication.

The task includes:

- Creating Azure Public Virtual Networks (VNets)
- Configuring Public Subnets
- Creating and managing Network Security Groups (NSGs)
- Allowing secure SSH access
- Creating Static Public IP resources
- Deploying Ubuntu Virtual Machines using Azure CLI
- Configuring SSH key-based authentication
- Understanding Azure networking and security concepts

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud infrastructure resources.

---

### Step 2: Login Using Azure CLI  

Open Azure Cloud Shell or terminal.

Authenticate using Azure CLI:

```bash
az login
```

#### Explanation  

The `az login` command authenticates your Azure account for CLI-based infrastructure management.

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

This ensures resources are deployed under the correct Azure subscription.

---

### Step 4: Create a Resource Group  

Create a Resource Group:

```bash
az group create \
--name devops-rg \
--location eastus
```

#### Explanation  

A Resource Group logically organizes Azure resources such as Virtual Machines, networking, and storage services.

---

### Step 5: Create a Public Virtual Network and Subnet  

Create a Virtual Network with a Public Subnet:

```bash
az network vnet create \
--resource-group devops-rg \
--name devops-pub-vnet \
--address-prefix 10.0.0.0/16 \
--subnet-name devops-pub-subnet \
--subnet-prefix 10.0.1.0/24
```

#### Explanation  

The Virtual Network provides networking infrastructure for Azure resources, while the subnet hosts internet-accessible resources.

---

### Step 6: Create a Network Security Group (NSG)  

Create an NSG:

```bash
az network nsg create \
--resource-group devops-rg \
--name devops-vm-nsg
```

#### Explanation  

Network Security Groups control inbound and outbound traffic to Azure resources.

---

### Step 7: Allow SSH Access on Port 22  

Create an NSG rule for SSH:

```bash
az network nsg rule create \
--resource-group devops-rg \
--nsg-name devops-vm-nsg \
--name AllowSSH \
--protocol Tcp \
--priority 1000 \
--destination-port-range 22 \
--access Allow
```

#### Explanation  

This rule allows secure SSH access to the Virtual Machine.

---

### Step 8: Create a Static Public IP Address  

Create a Static Public IP:

```bash
az network public-ip create \
--resource-group devops-rg \
--name devops-public-ip \
--sku Standard \
--allocation-method Static
```

#### Explanation  

A Static Public IP ensures the Virtual Machine always retains the same external IP address.

---

### Step 9: Generate SSH Key Pair  

Generate SSH keys:

```bash
ssh-keygen -t rsa -b 4096
```

#### Explanation  

SSH keys provide secure password-less authentication for Linux Virtual Machines.

---

### Step 10: Create Azure Virtual Machine  

Deploy an Ubuntu Virtual Machine:

```bash
az vm create \
--resource-group devops-rg \
--name devops-pub-vm \
--image Ubuntu2204 \
--admin-username azureuser \
--authentication-type ssh \
--ssh-key-values ~/.ssh/id_rsa.pub \
--vnet-name devops-pub-vnet \
--subnet devops-pub-subnet \
--nsg devops-vm-nsg \
--public-ip-address devops-public-ip
```

#### Explanation  

This command deploys the Virtual Machine inside the Public Virtual Network and associates the Static Public IP.

---

### Step 11: Verify Public IP Address  

Retrieve the VM Public IP:

```bash
az vm list-ip-addresses \
--resource-group devops-rg \
--name devops-pub-vm \
--output table
```

#### Explanation  

This confirms the Virtual Machine is accessible over the internet.

---

### Step 12: Connect to the Virtual Machine Using SSH  

Connect securely using SSH:

```bash
ssh azureuser@<PUBLIC_IP>
```

#### Explanation  

SSH provides secure remote administration of Linux Virtual Machines over the internet.

---

### Step 13: Verify Connectivity  

Verify VM access:

```bash
hostname
```

Check network connectivity:

```bash
ip addr
```

#### Explanation  

These commands confirm successful SSH connectivity and VM networking configuration.

---

## Best Practices  

- Use SSH key-based authentication instead of passwords  
- Restrict NSG rules to required ports only  
- Use Static Public IPs for production workloads requiring stable endpoints  
- Avoid exposing unnecessary services publicly  
- Regularly monitor NSG and Public IP configurations  
- Apply least privilege access principles  

---

## Key Learnings  

- Azure VNets provide secure cloud networking infrastructure  
- Public Subnets allow internet-accessible resources  
- NSGs help secure Virtual Machine access  
- Static Public IPs provide stable endpoints for remote access  
- SSH keys improve cloud VM security  
- Azure CLI simplifies networking and VM deployment tasks  

---

Every day brings new cloud and DevOps learning opportunities 🚀
