# Day 32 – Synchronizing Containers Using the CLI

---

## Task Overview  

The Nautilus DevOps team worked on synchronizing Azure Blob Storage containers as part of a cloud data migration project. In this task, a new private Blob container was created and data was migrated from an existing source container to the destination container using Azure CLI.

Azure Blob Storage synchronization helps ensure secure and reliable cloud-based data migration and storage management.

The task includes:

- Creating Azure Blob Storage containers
- Managing private container access
- Downloading and uploading blobs using Azure CLI
- Migrating files between Blob containers
- Verifying data consistency and integrity
- Understanding cloud storage management workflows

---

## Step-by-Step Implementation  

### Step 1: Login to Azure  

Authenticate using Azure CLI:

```bash
az login
```

#### Explanation  

The `az login` command authenticates the Azure account for CLI-based resource management.

---

### Step 2: Verify Storage Account  

List available storage accounts:

```bash
az storage account list --output table
```

Verify storage account:

```text
devopsst21278
```

#### Explanation  

Azure Storage Accounts manage Blob Storage containers and related services.

---

### Step 3: Create Destination Blob Container  

Create a new private Blob container:

```bash
az storage container create \
--name devops-dest-31266 \
--account-name devopsst21278 \
--auth-mode login \
--public-access off
```

#### Explanation  

This creates a private Blob container with no anonymous public access.

---

### Step 4: Verify Source Container Contents  

List blobs inside the source container:

```bash
az storage blob list \
--container-name devops-source-21129 \
--account-name devopsst21278 \
--auth-mode login \
--output table
```

Verify blob:

```text
devops.txt
```

#### Explanation  

This confirms the source file exists before migration.

---

### Step 5: Download Blob from Source Container  

Download the blob locally:

```bash
az storage blob download \
--container-name devops-source-21129 \
--name devops.txt \
--file devops.txt \
--account-name devopsst21278 \
--auth-mode login
```

#### Explanation  

This downloads the source blob from Azure Blob Storage to the local system.

---

### Step 6: Upload Blob to Destination Container  

Upload the file into the destination container:

```bash
az storage blob upload \
--container-name devops-dest-31266 \
--name devops.txt \
--file devops.txt \
--account-name devopsst21278 \
--auth-mode login
```

#### Explanation  

This uploads the file into the newly created destination Blob container.

---

### Step 7: Verify Destination Container Contents  

List blobs inside the destination container:

```bash
az storage blob list \
--container-name devops-dest-31266 \
--account-name devopsst21278 \
--auth-mode login \
--output table
```

Verify:

```text
devops.txt
```

#### Explanation  

This confirms successful blob upload to the destination container.

---

### Step 8: Verify File Consistency  

Download source blob again:

```bash
az storage blob download \
--container-name devops-source-21129 \
--name devops.txt \
--file source.txt \
--account-name devopsst21278 \
--auth-mode login
```

Download destination blob:

```bash
az storage blob download \
--container-name devops-dest-31266 \
--name devops.txt \
--file dest.txt \
--account-name devopsst21278 \
--auth-mode login
```

Compare files:

```bash
diff source.txt dest.txt
```

#### Explanation  

No output from the `diff` command confirms both files are identical and data migration completed successfully.

---

## Best Practices  

- Use private Blob containers for secure storage  
- Verify source data before migration  
- Validate migrated files after synchronization  
- Use Azure CLI for automation and repeatable workflows  
- Apply least privilege access principles  
- Monitor cloud storage operations regularly  

---

## Key Learnings  

- Azure Blob Storage supports secure cloud-based object storage  
- Azure CLI simplifies storage management and automation  
- Blob synchronization helps ensure reliable cloud migrations  
- Private containers improve data security  
- File verification is important during migration workflows  
- Cloud storage automation improves operational efficiency  

---

Step by step, improving Cloud and DevOps skills 🚀
