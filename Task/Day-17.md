# Day 17 – Create a Public Azure Blob Storage Container

---

## Task Overview  

The Nautilus DevOps team is working on cloud storage management and public content hosting in Azure. As part of this task, a public Azure Blob Storage container needs to be created with anonymous read access enabled.

Azure Blob Storage is commonly used for:

- Static website hosting
- Public file sharing
- Images and media hosting
- Backups and logs
- Cloud-based object storage

The task includes:

- Creating an Azure Storage Account
- Creating a Blob Storage container
- Configuring public access permissions
- Enabling anonymous read access
- Understanding Azure object storage access control

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud infrastructure and storage services.

---

### Step 2: Open Storage Accounts Service  

Search for:

| Search |
|---|
| Storage accounts |

Open the **Storage accounts** service.

#### Explanation  
Storage Accounts are used to manage Azure storage resources including Blob Storage, File Shares, Queues, and Tables.

---

### Step 3: Create a Storage Account  

Click:

- **Create**

Configure the following settings:

| Property | Example Value |
|---|---|
| Resource Group | `devops-rg` |
| Storage Account Name | `devopsstorage01` |
| Region | `westus` |
| Performance | Standard |
| Redundancy | LRS |

Click:

- **Review + Create**
- **Create**

#### Explanation  
This creates a new Azure Storage Account to host Blob Storage resources.

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
Blob containers are used to organize and manage objects/files stored in Azure Blob Storage.

---

### Step 6: Create Public Blob Container  

Configure the following settings:

| Property | Example Value |
|---|---|
| Container Name | `public-container` |
| Public Access Level | Container (anonymous read access for containers and blobs) |

Click:

- **Create**

#### Explanation  
This creates a public Blob container with anonymous read access enabled.

---

### Step 7: Verify Container Configuration  

Go to:

- **Storage Account → Containers**

Verify:

| Property | Expected Value |
|---|---|
| Container Name | `public-container` |
| Access Level | Container |

#### Explanation  
This confirms the Blob container is configured for public access.

---

## Best Practices  

- Use public containers only for non-sensitive content  
- Avoid storing confidential data in public containers  
- Use private containers for secure application data  
- Apply proper naming conventions for storage resources  
- Monitor public storage access regularly  
- Use Azure RBAC and SAS tokens for controlled access when needed  

---

## Key Learnings  

- Azure Blob Storage provides scalable cloud object storage  
- Public containers allow anonymous read access to blobs and containers  
- Storage Accounts centrally manage Azure storage services  
- Blob containers organize and manage cloud storage objects  
- Azure supports flexible storage access control models  
- Proper access management improves cloud security and usability  

---

Step by step, improving cloud storage and DevOps skills 🚀
