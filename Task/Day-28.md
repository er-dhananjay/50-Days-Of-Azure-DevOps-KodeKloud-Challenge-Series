# Day 28 – Troubleshooting Public Virtual Network Configurations

---

## Task Overview  

The Nautilus DevOps team worked on troubleshooting and configuring networking components in a Microsoft Azure Public Virtual Network environment. The task focused on resolving connectivity issues, configuring secure public access, and deploying a web server on an Azure Virtual Machine.

This hands-on troubleshooting activity helped improve understanding of Azure networking, NSGs, Route Tables, Public IPs, and internet accessibility in cloud environments.

The task includes:

- Attaching Public IPs to Azure Virtual Machines
- Configuring Network Security Group (NSG) rules
- Troubleshooting Route Table issues
- Resolving blocked internet connectivity
- Installing and configuring Nginx on Linux
- Verifying public access using browser and curl
- Understanding real-world Azure networking troubleshooting

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based management platform used to manage networking and cloud resources.

---

### Step 2: Login Using Azure CLI  

Open Azure Cloud Shell or terminal.

Authenticate using Azure CLI:

```bash
az login
```

#### Explanation  

The `az login` command authenticates your Azure account for CLI-based resource management.

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

This ensures all resources are managed under the correct Azure subscription.

---

### Step 4: Verify Virtual Machine Configuration  

List Virtual Machines:

```bash
az vm list --output table
```

Retrieve VM details:

```bash
az vm show \
--resource-group devops-rg \
--name devops-vm \
--output table
```

#### Explanation  

This verifies the Virtual Machine configuration and deployment status.

---

### Step 5: Create and Attach Public IP Address  

Create a Static Public IP:

```bash
az network public-ip create \
--resource-group devops-rg \
--name devops-public-ip \
--sku Standard \
--allocation-method Static
```

Associate the Public IP with the VM NIC:

```bash
az network nic ip-config update \
--resource-group devops-rg \
--nic-name devops-vmVMNic \
--name ipconfig1 \
--public-ip-address devops-public-ip
```

#### Explanation  

A Public IP allows external internet access to the Azure Virtual Machine.

---

### Step 6: Configure NSG Rules for SSH and HTTP  

Allow SSH access on port 22:

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

Allow HTTP access on port 80:

```bash
az network nsg rule create \
--resource-group devops-rg \
--nsg-name devops-vm-nsg \
--name AllowHTTP \
--protocol Tcp \
--priority 1001 \
--destination-port-range 80 \
--access Allow
```

#### Explanation  

Network Security Groups control inbound and outbound traffic for Azure resources.

---

### Step 7: Troubleshoot Route Table Configuration  

Verify Route Tables:

```bash
az network route-table list --output table
```

Check subnet association:

```bash
az network vnet subnet show \
--resource-group devops-rg \
--vnet-name devops-vnet \
--name public-subnet
```

#### Explanation  

Incorrect Route Table configuration can block internet connectivity for Azure resources.

---

### Step 8: Connect to the Virtual Machine  

Retrieve Public IP:

```bash
az vm list-ip-addresses \
--resource-group devops-rg \
--name devops-vm \
--output table
```

Connect using SSH:

```bash
ssh azureuser@<PUBLIC_IP>
```

#### Explanation  

SSH provides secure remote administration of Linux Virtual Machines.

---

### Step 9: Install and Configure Nginx  

Update packages:

```bash
sudo apt update
```

Install Nginx:

```bash
sudo apt install nginx -y
```

Start and enable Nginx:

```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

#### Explanation  

Nginx acts as the web server hosted on the Azure Virtual Machine.

---

### Step 10: Verify Nginx Service  

Check service status:

```bash
sudo systemctl status nginx
```

Verify listening ports:

```bash
ss -tlnp | grep 80
```

#### Explanation  

This confirms that Nginx is running and accepting HTTP connections.

---

### Step 11: Verify Public Connectivity  

Test from browser or terminal:

```bash
curl http://<PUBLIC_IP>
```

Expected output:

```text
Welcome to nginx!
```

#### Explanation  

This confirms successful public internet access to the web server hosted on the Azure VM.

---

## Best Practices  

- Use NSGs to restrict unnecessary public access  
- Verify Route Table associations carefully  
- Use Static Public IPs for stable endpoints  
- Regularly monitor network connectivity and security rules  
- Avoid exposing unnecessary ports publicly  
- Use SSH key-based authentication for secure VM access  

---

## Key Learnings  

- Azure Public VNets enable internet-accessible cloud infrastructure  
- NSGs provide secure traffic filtering and access control  
- Route Tables impact internet routing and connectivity  
- Public IPs allow external access to Azure resources  
- Nginx deployment helps validate network accessibility  
- Troubleshooting networking issues is a critical DevOps skill  

---

Step by step, improving Azure networking and troubleshooting skills 🚀
