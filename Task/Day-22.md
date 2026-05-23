# Day 22 – Configuring Instances with User Data

---

## Task Overview  

The Nautilus DevOps team is working on automating cloud infrastructure configuration in Microsoft Azure. As part of this task, Virtual Machines are configured automatically during deployment using User Data / Custom Script Extensions.

User Data helps automate server initialization tasks such as package installation, service configuration, and application setup during VM creation.

The task includes:

- Creating Azure Virtual Machines
- Automating server setup using User Data
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

The Azure Portal is Microsoft Azure’s web-based management platform used to manage cloud resources.

---

### Step 2: Login Using Azure CLI  

Open terminal or Azure Cloud Shell.

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

A Resource Group logically organizes Azure resources such as Virtual Machines and networking components.

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

### Step 6: Create a Network Security Group Rule for HTTP  

Allow HTTP traffic on port 80:

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

This rule allows incoming web traffic to the Virtual Machine.

---

### Step 7: Create User Data Script  

Create a script file:

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

This User Data script automatically installs and starts the Nginx web server during VM creation.

---

### Step 8: Create Azure Virtual Machine with User Data  

Create the Ubuntu Virtual Machine:

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

### Step 9: Verify Virtual Machine Creation  

Check VM status:

```bash
az vm list \
--output table
```

#### Explanation  

This verifies the VM was created successfully.

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

The Public IP allows external access to the Virtual Machine.

---

### Step 11: Test Nginx Web Server  

Open browser or use curl:

```bash
curl http://<PUBLIC_IP>
```

#### Explanation  

Successful output confirms that the User Data script installed and started Nginx automatically.

---

## Best Practices  

- Use User Data for automated server initialization  
- Avoid manual repetitive configuration tasks  
- Store automation scripts in version control systems  
- Restrict unnecessary public access using NSGs  
- Use Infrastructure as Code for scalable deployments  
- Monitor deployed services regularly  

---

## Key Learnings  

- User Data automates Virtual Machine initialization  
- Azure CLI simplifies infrastructure deployment  
- Infrastructure automation improves consistency and scalability  
- Network Security Groups control access securely  
- Nginx installation can be fully automated during VM creation  
- Automation reduces manual configuration errors  

---

Step by step, improving Azure automation and DevOps skills 🚀
