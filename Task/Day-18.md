# Day 18 – Copy Data to an Azure Blob Storage Container

---

## Task Overview  

The Nautilus DevOps team is working on cloud data migration and storage management in Azure. As part of this task, data from a Linux environment needs to be copied to an existing Azure Blob Storage container.

Azure Blob Storage is widely used for:

- Data migration
- Application storage
- Backups and archives
- Cloud-based object storage
- File sharing and distribution

The task includes:

- Working with Azure Storage Accounts
- Uploading local files to Blob Storage
- Managing Blob containers
- Understanding storage authentication and access
- Learning basic cloud migration workflows

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  
The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud resources and storage services.

---

### Step 2: Open Storage Accounts Service  

Search for:

| Search |
|---|
| Storage accounts |

Open the **Storage accounts** service.

#### Explanation  
Storage Accounts are used to manage Azure Blob Storage and other storage services.

---

### Step 3: Open Existing Storage Account  

Select the existing Storage Account.

Example:

| Storage Account |
|---|
| `devopsstorage01` |

#### Explanation  
This opens the management page of the Azure Storage Account.

---

### Step 4: Open Blob Container  

From the left-side menu, open:

- **Containers**

Select the target Blob container.

Example:

| Blob Container |
|---|
| `devops-blob-container` |

#### Explanation  
Blob containers are used to store files and objects inside Azure Blob Storage.

---

### Step 5: Prepare Local File  

On the Linux system, verify the file exists:

```bash
ls /tmp
