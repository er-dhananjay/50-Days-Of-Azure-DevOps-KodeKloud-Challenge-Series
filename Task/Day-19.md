# Day 19 – Convert Public Azure Blob Container to Private

---

## Task Overview  

The Nautilus DevOps team is working on improving cloud storage security and access management in Azure. As part of this task, an existing public Azure Blob Storage container needs to be converted to private access.

Azure Blob Storage containers can be configured as:

- Public
- Private
- Blob-level public access
- Container-level public access

The task includes:

- Managing Azure Storage Accounts
- Modifying Blob container access levels
- Restricting anonymous/public access
- Understanding cloud storage security concepts
- Implementing secure access control practices

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
Storage Accounts manage Azure storage services including Blob Storage.

---

### Step 3: Open Existing Storage Account  

Select the target Storage Account.

Example:

| Storage Account |
|---|
| `devopsstorage01` |

#### Explanation  
This opens the management page of the Azure Storage Account.

---

### Step 4: Open Blob Containers Section  

From the left-side menu, open:

- **Containers**

Select the target Blob container.

Example:

| Blob Container |
|---|
| `public-container` |

#### Explanation  
Blob containers store files and objects inside Azure Blob Storage.

---

### Step 5: Change Container Access Level  

Inside the Blob container, click:

- **Change access level**

or:

- **... (More options) → Change access level**

#### Explanation  
Azure allows modifying Blob container visibility and public access settings.

---

### Step 6: Configure Private Access  

Under:

| Setting |
|---|
| Public access level |

Select:

| Access Type |
|---|
| Private (no anonymous access) |

Click:

- **OK**
or
- **Save**

#### Explanation  
This disables anonymous/public access to the Blob container and secures stored data.

---

### Step 7: Verify Container Access Level  

Go back to:

- **Storage Account → Containers**

Verify:

| Property | Expected Value |
|---|---|
| Container Name | `public-container` |
| Access Level | Private |

#### Explanation  
This confirms the Blob container is now configured as private.

---

## Best Practices  

- Use private containers for sensitive or internal data  
- Avoid unnecessary anonymous public access  
- Apply least privilege access principles  
- Use RBAC and SAS tokens for controlled storage access  
- Regularly audit Blob Storage permissions  
- Enable monitoring and logging for storage activities  

---

## Key Learnings  

- Azure Blob containers support multiple access levels  
- Private containers prevent anonymous/public access  
- Proper access control improves cloud storage security  
- Azure Storage Accounts centrally manage Blob Storage services  
- Public vs private access impacts security and data exposure  
- Secure cloud storage management is critical in DevOps environments  

---

Step by step, strengthening cloud security and DevOps skills 🚀
