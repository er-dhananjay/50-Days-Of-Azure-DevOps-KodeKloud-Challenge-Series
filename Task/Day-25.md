# Day 25 – Expanding and Managing Disk Storage

---

## Task Overview  

The Nautilus DevOps team is working on improving storage management and scalability in Microsoft Azure. As part of this task, an Azure Virtual Machine disk was expanded and an additional data disk was created, attached, formatted, and mounted on a Linux Virtual Machine.

Efficient disk management is essential for handling growing workloads, maintaining application performance, and ensuring scalable cloud infrastructure.

The task includes:

- Expanding Azure VM OS disks
- Creating and attaching additional data disks
- Managing Azure storage resources using Azure CLI
- Formatting and mounting disks on Linux
- Verifying storage expansion and disk connectivity
- Understanding cloud storage management concepts

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based platform used to manage cloud infrastructure resources.

---

### Step 2: Login Using Azure CLI  

Open Azure Cloud Shell or terminal.

Authenticate using Azure CLI:

```bash
az login
```

#### Explanation  

The `az login` command authenticates your Azure account and allows CLI-based resource management.

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

This ensures all storage resources are managed under the correct Azure subscription.

---

### Step 4: Identify Resource Group and VM  

List Resource Groups:

```bash
az group list --output table
```

List Virtual Machines:

```bash
az vm list --output table
```

#### Explanation  

This helps identify the target Virtual Machine and associated Resource Group.

---

### Step 5: Expand Existing OS Disk  

Get the OS disk name:

```bash
az vm show \
--resource-group devops-rg \
--name devops-vm \
--query "storageProfile.osDisk.name" \
-o tsv
```

Stop the VM before resizing:

```bash
az vm deallocate \
--resource-group devops-rg \
--name devops-vm
```

Resize the OS disk from 32Gi to 64Gi:

```bash
az disk update \
--resource-group devops-rg \
--name devops-vm_OsDisk \
--size-gb 64
```

Start the VM:

```bash
az vm start \
--resource-group devops-rg \
--name devops-vm
```

#### Explanation  

Azure requires the Virtual Machine to be stopped before modifying certain OS disk properties.

---

### Step 6: Create a New Standard HDD Data Disk  

Create a Standard HDD disk:

```bash
az disk create \
--resource-group devops-rg \
--name devops-data-disk \
--size-gb 64 \
--sku Standard_LRS
```

#### Explanation  

This creates an additional managed data disk using Standard HDD storage.

---

### Step 7: Attach Data Disk to Virtual Machine  

Attach the disk:

```bash
az vm disk attach \
--resource-group devops-rg \
--vm-name devops-vm \
--name devops-data-disk
```

#### Explanation  

The new disk becomes available to the Linux Virtual Machine as an additional block device.

---

### Step 8: Connect to the Virtual Machine  

Retrieve the Public IP:

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

SSH allows secure remote administration of the Linux Virtual Machine.

---

### Step 9: Verify Attached Disks on Linux  

Check available disks:

```bash
lsblk
```

#### Explanation  

This displays attached storage devices and partitions.

---

### Step 10: Create Partition on New Disk  

Create partition using `fdisk`:

```bash
sudo fdisk /dev/sdc
```

Inside `fdisk`:

```text
n
p
1


w
```

#### Explanation  

This creates a new primary partition on the attached disk.

---

### Step 11: Format the Disk  

Format the partition using ext4:

```bash
sudo mkfs.ext4 /dev/sdc1
```

#### Explanation  

Formatting prepares the disk for Linux filesystem usage.

---

### Step 12: Create Mount Point  

Create mount directory:

```bash
sudo mkdir /data
```

#### Explanation  

The mount point acts as the access location for the attached storage.

---

### Step 13: Mount the Disk  

Mount the partition:

```bash
sudo mount /dev/sdc1 /data
```

Verify mounting:

```bash
df -h
```

#### Explanation  

This confirms the disk is mounted successfully.

---

### Step 14: Configure Persistent Mounting  

Get UUID:

```bash
sudo blkid
```

Edit `/etc/fstab`:

```bash
sudo vi /etc/fstab
```

Add entry:

```text
UUID=<UUID> /data ext4 defaults,nofail 0 2
```

#### Explanation  

This ensures the disk mounts automatically after system reboot.

---

## Best Practices  

- Use managed disks for better reliability and scalability  
- Monitor disk usage regularly  
- Use separate data disks for applications and databases  
- Configure persistent mounts using UUIDs  
- Use appropriate disk SKUs based on workload requirements  
- Regularly back up critical data  

---

## Key Learnings  

- Azure supports dynamic storage expansion for Virtual Machines  
- Managed disks simplify cloud storage management  
- Linux disk partitioning and mounting are essential admin skills  
- Persistent mounting ensures disks survive reboots  
- Proper storage planning improves performance and scalability  
- Azure CLI simplifies storage and infrastructure management  

---

Step by step, improving Azure storage management and DevOps skills 🚀
