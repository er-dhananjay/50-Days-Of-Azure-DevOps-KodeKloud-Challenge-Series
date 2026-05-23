# Day 16 – Create a Private Azure Blob Storage Container

---

## Task Overview  

The Nautilus DevOps team is working on improving cloud storage security and resource management in Azure. As part of this task, a private Azure Blob Storage container needs to be created for secure object storage.

Azure Blob Storage is used to store unstructured data such as files, backups, logs, images, and application data.

The task includes:

- Creating an Azure Storage Account
- Creating a Blob Storage container
- Configuring the container as private
- Understanding Azure object storage concepts
- Managing storage access and security

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud infrastructure and storage resources.

---

### Step 2: Open Storage Accounts Service  

Search for:

| Search |
|---|
| Storage accounts |

Open the **Storage accounts** service.

#### Explanation  
Storage Accounts are used to manage Azure storage services such as Blob Storage, File Storage, Queues, and Tables.

---

### Step 3: Create a Storage Account  

Click:

- **Create**

Configure the following settings:

| Property | Example Value |
|---|---|
| Resource Group | `devops-rg` |
| Storage Account Name | `devopsstorage01` |
| Region | `southcentralus` |
| Performance | Standard |
| Redundancy | LRS |

Click:

- **Review + Create**
- **Create**

#### Explanation  
This creates a new Azure Storage Account for managing cloud storage resources.

---

### Step 4: Open the Storage Account  

After deployment completes, open:

| Storage Account |
|---|
| `devopsstorage01` |

#### Explanation  
This opens the management page of the Azure Storage Account.

---

### Step 5: Open Blob Containers Section  

From the left-side menu, open:

- **Containers**

Click:

- **+ Container**

#### Explanation  
Blob containers are used to organize and store blobs (objects/files) inside Azure Storage.

---

### Step 6: Create Private Blob Container  

Configure the following settings:

| Property | Example Value |
|---|---|
| Container Name | `private-container` |
| Public Access Level | Private (no anonymous access) |

Click:

- **Create**

#### Explanation  
This creates a private Blob container with restricted access.

---

### Step 7: Verify Container Configuration  

Go to:

- **Storage Account → Containers**

Verify:

| Property | Expected Value |
|---|---|
| Container Name | `private-container` |
| Access Level | Private |

#### Explanation  
This confirms the Blob container is configured with private access.

---

## Best Practices  

- Use private containers for sensitive data  
- Avoid enabling anonymous public access unnecessarily  
- Use RBAC and SAS tokens for secure access management  
- Apply proper naming conventions for storage resources  
- Enable monitoring and logging for storage accounts  
- Regularly review storage security settings  

---

## Key Learnings  

- Azure Blob Storage provides scalable object storage services  
- Private containers restrict anonymous/public access  
- Storage Accounts manage Azure storage resources centrally  
- Blob containers organize cloud storage objects efficiently  
- Azure supports secure cloud storage access management  
- Proper storage security improves cloud infrastructure protection  

---

Step by step, strengthening Azure and DevOps skills 🚀
