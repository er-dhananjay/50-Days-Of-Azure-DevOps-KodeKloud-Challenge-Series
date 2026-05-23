# Day 27 – Deploying Virtual Machines in a Private Virtual Network

---

## Task Overview  

The Nautilus DevOps team is working on building secure and isolated cloud infrastructure in Microsoft Azure. As part of this task, Virtual Machines were deployed inside a Private Virtual Network (VNet) with controlled internal communication and restricted external exposure.

Private Virtual Networks help improve security by isolating resources from direct internet access while enabling secure communication between internal cloud services.

The task includes:

- Creating Azure Private Virtual Networks (VNets)
- Configuring Private Subnets
- Deploying Virtual Machines inside private networks
- Managing Network Security Groups (NSGs)
- Configuring secure SSH connectivity
- Managing Azure networking using Azure CLI
- Understanding cloud network isolation and security concepts

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based management platform used to manage cloud infrastructure resources.

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

This ensures all Azure resources are created under the correct subscription.

---

### Step 4: Create a Resource Group  

Create a Resource Group:

```bash
az group create \
--name devops-rg \
--location eastus
```

#### Explanation  

A Resource Group acts as a logical container for Azure resources such as Virtual Machines, VNets, and networking components.

---

### Step 5: Create a Private Virtual Network and Subnet  

Create a Private VNet:

```bash
az network vnet create \
--resource-group devops-rg \
--name devops-private-vnet \
--address-prefix 10.0.0.0/16 \
--subnet-name private-subnet \
--subnet-prefix 10.0.1.0/24
```

#### Explanation  

The Virtual Network provides isolated private networking for Azure resources, while the subnet logically separates workloads inside the VNet.

---

### Step 6: Create a Network Security Group (NSG)  

Create an NSG:

```bash
az network nsg create \
--resource-group devops-rg \
--name private-vm-nsg
```

#### Explanation  

Network Security Groups control inbound and outbound traffic to Azure resources.

---

### Step 7: Configure NSG Rule for SSH Access  

Allow SSH access on port 22:

```bash
az network nsg rule create \
--resource-group devops-rg \
--nsg-name private-vm-nsg \
--name AllowSSH \
--protocol Tcp \
--priority 1000 \
--destination-port-range 22 \
--access Allow
```

#### Explanation  

This rule allows secure SSH connectivity to the Virtual Machine.

---

### Step 8: Generate SSH Key Pair  

Generate SSH public and private keys:

```bash
ssh-keygen -t rsa -b 4096
```

#### Explanation  

SSH keys provide secure password-less authentication for Linux Virtual Machines.

---

### Step 9: Create Azure Virtual Machine in Private VNet  

Deploy an Ubuntu Virtual Machine inside the Private VNet:

```bash
az vm create \
--resource-group devops-rg \
--name private-vm \
--image Ubuntu2204 \
--admin-username azureuser \
--authentication-type ssh \
--ssh-key-values ~/.ssh/id_rsa.pub \
--vnet-name devops-private-vnet \
--subnet private-subnet \
--nsg private-vm-nsg \
--public-ip-address ""
```

#### Explanation  

This command creates a Virtual Machine without a Public IP, ensuring it remains accessible only inside the private network.

---

### Step 10: Verify Virtual Machine Deployment  

Check Virtual Machine details:

```bash
az vm list \
--output table
```

#### Explanation  

This verifies successful deployment of the Virtual Machine.

---

### Step 11: Verify Private IP Address  

Retrieve the VM Private IP:

```bash
az vm list-ip-addresses \
--resource-group devops-rg \
--name private-vm \
--output table
```

#### Explanation  

This confirms the VM is using private network addressing only.

---

### Step 12: Verify Internal Connectivity  

Connect to another internal resource or verify networking:

```bash
ping 10.0.1.4
```

Check network interfaces:

```bash
ip addr
```

#### Explanation  

These commands help validate internal network communication inside the Private VNet.

---

### Step 13: Verify SSH Connectivity  

Connect securely using SSH from an authorized internal host:

```bash
ssh azureuser@<PRIVATE_IP>
```

#### Explanation  

SSH allows secure remote administration of Linux Virtual Machines within the private network.

---

## Best Practices  

- Avoid assigning Public IPs to internal-only Virtual Machines  
- Use NSGs to restrict unnecessary inbound traffic  
- Use SSH key-based authentication instead of passwords  
- Separate workloads using multiple subnets  
- Apply least privilege access principles  
- Regularly monitor VNet and NSG configurations  

---

## Key Learnings  

- Private VNets help isolate cloud infrastructure securely  
- NSGs provide controlled access to Azure resources  
- Private IP addressing improves cloud security  
- SSH key authentication enhances secure remote administration  
- Azure CLI simplifies Virtual Machine and networking management  
- Network isolation is critical for secure cloud environments  

---

Step by step improving my cloud and DevOps skills 🚀
