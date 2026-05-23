# Day 24 – Securing Virtual Machine SSH Access

---

## Task Overview  

The Nautilus DevOps team is working on improving cloud infrastructure security in Microsoft Azure. As part of this task, secure SSH key-based authentication is configured for accessing Azure Virtual Machines.

SSH key-based authentication helps eliminate password-based logins and provides a more secure method for remote administration of Linux Virtual Machines.

The task includes:

- Generating and managing SSH key pairs
- Creating Azure Virtual Machines using Azure CLI
- Configuring password-less SSH authentication
- Securing remote access to Linux servers
- Verifying SSH connectivity
- Understanding cloud security best practices

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

This ensures all resources are deployed under the correct Azure subscription.

---

### Step 4: Create a Resource Group  

Create a Resource Group:

```bash
az group create \
--name devops-rg \
--location eastus
```

#### Explanation  

A Resource Group acts as a logical container for Azure resources such as Virtual Machines and networking components.

---

### Step 5: Generate SSH Key Pair  

Generate SSH public and private keys:

```bash
ssh-keygen -t rsa -b 4096
```

Press Enter to accept the default file location.

#### Explanation  

SSH keys provide secure password-less authentication for Linux Virtual Machines.

---

### Step 6: Verify SSH Keys  

Check generated SSH keys:

```bash
ls ~/.ssh/
```

Example output:

```text
id_rsa
id_rsa.pub
```

#### Explanation  

- `id_rsa` → Private Key  
- `id_rsa.pub` → Public Key  

The public key is shared with the server, while the private key remains secure on the client machine.

---

### Step 7: Create Virtual Network and Subnet  

Create a Virtual Network:

```bash
az network vnet create \
--resource-group devops-rg \
--name devops-vnet \
--subnet-name devops-subnet
```

#### Explanation  

The Virtual Network provides private networking for Azure resources.

---

### Step 8: Create Azure Virtual Machine with SSH Authentication  

Create an Ubuntu Virtual Machine:

```bash
az vm create \
--resource-group devops-rg \
--name devops-vm \
--image Ubuntu2204 \
--admin-username azureuser \
--authentication-type ssh \
--ssh-key-values ~/.ssh/id_rsa.pub
```

#### Explanation  

This command creates the Virtual Machine and configures SSH public key authentication.

---

### Step 9: Allow SSH Access Through NSG  

Open SSH port 22:

```bash
az vm open-port \
--resource-group devops-rg \
--name devops-vm \
--port 22
```

#### Explanation  

This configures the Network Security Group (NSG) to allow incoming SSH traffic.

---

### Step 10: Retrieve Public IP Address  

Get the VM Public IP:

```bash
az vm list-ip-addresses \
--resource-group devops-rg \
--name devops-vm \
--output table
```

#### Explanation  

The Public IP allows remote access to the Virtual Machine over the internet.

---

### Step 11: Connect to the Virtual Machine Using SSH  

Connect securely using SSH:

```bash
ssh azureuser@<PUBLIC_IP>
```

#### Explanation  

SSH provides secure remote access to Linux servers using encrypted communication.

---

### Step 12: Verify Password-less Authentication  

Disconnect and reconnect to the VM.

If SSH login works without asking for a password, SSH key-based authentication is configured successfully.

#### Explanation  

Password-less SSH authentication improves security and simplifies remote server management.

---

## Best Practices  

- Use SSH key-based authentication instead of passwords  
- Keep private keys secure and never share them  
- Disable password authentication on production servers  
- Restrict SSH access using NSG rules and trusted IP ranges  
- Rotate SSH keys regularly  
- Apply least privilege security principles  

---

## Key Learnings  

- SSH keys provide secure remote access to cloud Virtual Machines  
- Azure CLI simplifies Virtual Machine deployment and management  
- Password-less authentication improves security and usability  
- Network Security Groups help secure SSH access  
- Proper key management is essential for cloud security  
- Secure remote administration is a critical DevOps skill  

---

Step by step, improving Azure security and DevOps skills 🚀
