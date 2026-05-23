# Day 15 – Create and Configure Network Security Group (NSG) in Azure

---

## Task Overview  

The Nautilus DevOps team is working on improving cloud network security and traffic management in Azure. As part of this task, a Network Security Group (NSG) needs to be created and configured to control inbound and outbound traffic for Azure resources.

Network Security Groups act as virtual firewalls that help secure Azure Virtual Networks and Virtual Machines.

The task includes:

- Creating a Network Security Group (NSG)
- Configuring inbound and outbound security rules
- Allowing and restricting specific ports and protocols
- Applying traffic filtering and access control policies
- Understanding Azure network security concepts

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud infrastructure and networking resources.

---

### Step 2: Open Network Security Groups Service  

Search for:

| Search |
|---|
| Network Security Groups |

Open the **Network Security Groups** service.

#### Explanation  
The NSG service is used to create and manage Azure network traffic filtering rules.

---

### Step 3: Create a New NSG  

Click:

- **Create**

Configure the following settings:

| Property | Example Value |
|---|---|
| Resource Group | `devops-rg` |
| Name | `devops-nsg` |
| Region | `southcentralus` |

Click:

- **Review + Create**
- **Create**

#### Explanation  
This creates a new Network Security Group resource in Azure.

---

### Step 4: Open the Created NSG  

After deployment completes, open:

| NSG |
|---|
| `devops-nsg` |

#### Explanation  
This opens the NSG management and rule configuration page.

---

### Step 5: Configure Inbound Security Rules  

From the left-side menu, open:

- **Inbound security rules**

Click:

- **Add**

Example configuration:

| Property | Example Value |
|---|---|
| Source | Any |
| Source Port Ranges | * |
| Destination | Any |
| Destination Port Ranges | 22 |
| Protocol | TCP |
| Action | Allow |
| Priority | 100 |
| Name | Allow-SSH |

Click:

- **Add**

#### Explanation  
Inbound rules control traffic entering Azure resources.

---

### Step 6: Configure Outbound Security Rules  

From the left-side menu, open:

- **Outbound security rules**

Click:

- **Add**

Example configuration:

| Property | Example Value |
|---|---|
| Source | Any |
| Source Port Ranges | * |
| Destination | Internet |
| Destination Port Ranges | * |
| Protocol | Any |
| Action | Allow |
| Priority | 100 |
| Name | Allow-Internet |

Click:

- **Add**

#### Explanation  
Outbound rules control traffic leaving Azure resources.

---

### Step 7: Associate NSG with Subnet or NIC  

Open:

- **Subnets**
or
- **Network interfaces**

Associate the NSG with the target subnet or Virtual Machine NIC.

#### Explanation  
An NSG becomes effective only after association with a subnet or network interface.

---

### Step 8: Verify NSG Rules  

Go to:

- **NSG → Inbound security rules**
- **NSG → Outbound security rules**

Verify rules are configured correctly.

#### Explanation  
This confirms traffic filtering rules are active and applied successfully.

---

## Best Practices  

- Follow least privilege access principles  
- Allow only required ports and protocols  
- Use NSGs together with Azure Firewall for layered security  
- Apply meaningful naming conventions for rules  
- Use priorities carefully to avoid rule conflicts  
- Regularly audit and review NSG configurations  

---

## Key Learnings  

- NSGs act as virtual firewalls in Azure  
- NSGs control inbound and outbound network traffic  
- Security rules are evaluated using priorities  
- NSGs improve cloud network security and isolation  
- Azure networking resources are modular and flexible  
- Proper NSG configuration strengthens infrastructure security  

---

Step by step, building stronger cloud networking and DevOps skills 🚀
