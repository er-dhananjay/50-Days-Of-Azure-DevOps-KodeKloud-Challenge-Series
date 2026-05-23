# Day 12 – Add and Manage Tags for Azure Virtual Machines

---

## Task Overview  

The Nautilus DevOps team is working on improving cloud resource organization and management in Azure. As part of this task, tags need to be added and managed for an Azure Virtual Machine.

Tags help organize resources using key-value pairs and are commonly used for:

- Resource organization
- Cost management
- Filtering and searching
- Environment identification
- Automation and governance

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based management interface used to manage cloud resources.

---

### Step 2: Open Virtual Machines Service  

Search for:

| Search |
|---|
| Virtual machines |

Open the **Virtual machines** service.

#### Explanation  
This section contains all Virtual Machines available in the Azure subscription.

---

### Step 3: Open the Existing Virtual Machine  

Select the target Virtual Machine.

Example:

| Virtual Machine |
|---|
| `devops-vm` |

#### Explanation  
This opens the management and configuration page of the Virtual Machine.

---

### Step 4: Open Tags Section  

From the left-side menu, open:

- **Tags**

#### Explanation  
The Tags section is used to create and manage metadata for Azure resources.

---

### Step 5: Add Tag to Virtual Machine  

Enter the following tag details:

| Key | Value |
|---|---|
| Environment | dev |

Click:

- **Apply**

or

- **Save**

#### Explanation  
This creates a tag that helps identify the environment type of the Virtual Machine.

---

### Step 6: Verify Tag Configuration  

After saving, verify the tag appears under:

- **Virtual Machine → Tags**

| Property | Expected Value |
|---|---|
| Key | Environment |
| Value | dev |

#### Explanation  
This confirms the tag was successfully added to the Azure Virtual Machine.

---

## Best Practices  

- Use standardized naming conventions for tags  
- Use tags for environment identification such as dev, test, and prod  
- Apply tags consistently across resources  
- Use tags for cost tracking and billing analysis  
- Avoid unnecessary or duplicate tags  
- Use automation policies for large-scale tagging management  

---

## Key Learnings  

- Tags in Azure are key-value pairs used for resource organization  
- Tags improve cloud governance and management  
- Azure resources can be filtered and grouped using tags  
- Tags help track resource ownership and environments  
- Cost management becomes easier using resource tagging  
- Proper tagging improves cloud infrastructure visibility and maintainability  

---

Step by step, improving cloud management and DevOps skills 🚀
