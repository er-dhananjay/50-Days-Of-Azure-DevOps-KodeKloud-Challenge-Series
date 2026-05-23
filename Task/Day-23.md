# Day 23 – Automating User Data Configuration Using the CLI

---

## Task Overview  

The Nautilus DevOps team is working on automating cloud infrastructure deployment and configuration using Azure CLI and User Data scripts. As part of this task, an Azure Virtual Machine is automatically configured during deployment to install and start Nginx without any manual intervention.

User Data (Custom Data) scripts help automate server initialization tasks during VM creation, improving consistency and reducing manual configuration effort.

The task includes:

- Creating Azure Virtual Machines using Azure CLI
- Automating server setup using User Data scripts
- Installing and configuring Nginx automatically
- Managing Network Security Group (NSG) rules
- Allowing HTTP traffic for web access
- Understanding Infrastructure Automation concepts

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

This ensures all Azure resources are deployed under the correct subscription.

---

### Step 4: Create a Resource Group  

Create a Resource Group:

```bash
az group create \
--name devops-rg \
--location eastus
```

#### Explanation  

A Resource Group logically organizes Azure resources such as Virtual Machines, networking, and storage components.

---

### Step 5: Create Virtual Network and Subnet  

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

### Step 6: Create Network Security Group Rule for HTTP  

Allow incoming HTTP traffic on port 80:

```bash
az network nsg rule create \
--resource-group devops-rg \
--nsg-name devopsVMNSG \
--name AllowHTTP \
--protocol Tcp \
--priority 1001 \
--destination-port-range 80 \
--access Allow
```

#### Explanation  

This rule allows external web traffic to reach the Virtual Machine.

---

### Step 7: Create User Data Script  

Create a file:

```bash
vi cloud-init.txt
```

Add the following content:

```yaml
#cloud-config
package_update: true
packages:
  - nginx

runcmd:
  - systemctl enable nginx
  - systemctl start nginx
```

Save and exit.

#### Explanation  

This User Data script automatically installs and starts Nginx during VM initialization.

---

### Step 8: Create Azure Virtual Machine Using Azure CLI  

Create the Ubuntu VM with User Data:

```bash
az vm create \
--resource-group devops-rg \
--name devops-vm \
--image Ubuntu2204 \
--admin-username azureuser \
--generate-ssh-keys \
--custom-data cloud-init.txt
```

#### Explanation  

The `--custom-data` option passes the User Data script to the VM during deployment.

---

### Step 9: Verify Virtual Machine Deployment  

Check Virtual Machine status:

```bash
az vm list \
--output table
```

#### Explanation  

This confirms that the VM was deployed successfully.

---

### Step 10: Retrieve Public IP Address  

Get the Public IP address of the VM:

```bash
az vm list-ip-addresses \
--resource-group devops-rg \
--name devops-vm \
--output table
```

#### Explanation  

The Public IP enables remote access to the Virtual Machine.

---

### Step 11: Test Nginx Service  

Access the web server using curl:

```bash
curl http://<PUBLIC_IP>
```

#### Explanation  

Successful output confirms that the User Data script installed and started Nginx automatically during VM creation.

---

## Best Practices  

- Use User Data for automated server initialization  
- Store automation scripts in Git repositories  
- Restrict unnecessary public access using NSGs  
- Use Infrastructure as Code for scalable deployments  
- Avoid manual repetitive configuration tasks  
- Monitor deployed services regularly  

---

## Key Learnings  

- Azure CLI simplifies infrastructure deployment and automation  
- User Data automates VM initialization tasks  
- Infrastructure automation improves scalability and consistency  
- Nginx installation can be automated during VM creation  
- Network Security Groups help secure cloud infrastructure  
- Automation reduces manual configuration errors  

---

Step by step, improving Azure automation and DevOps skills 🚀
