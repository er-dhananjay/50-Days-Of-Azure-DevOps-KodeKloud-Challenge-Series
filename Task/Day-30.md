# Day 30 – Create Azure SQL Database

---

## Task Overview  

The Nautilus DevOps team worked on deploying and configuring a publicly accessible Azure SQL Database for cloud-based application workloads. As part of this task, a new Azure SQL Server and SQL Database were created with appropriate compute, storage, backup redundancy, and authentication configurations.

Azure SQL Database is a fully managed relational database service that simplifies database management, scalability, security, and cloud-native application deployment.

The task includes:

- Creating Azure SQL Database instances
- Configuring Azure SQL Server
- Selecting compute and storage configurations
- Configuring backup storage redundancy
- Setting SQL authentication credentials
- Managing public database accessibility
- Verifying database deployment and status

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based management platform used for managing cloud infrastructure and services.

---

### Step 2: Open SQL Databases Service  

Search:

```text
SQL databases
```

Open:

```text
SQL databases
```

#### Explanation  

This service manages Azure SQL Database resources.

---

### Step 3: Create a New SQL Database  

Click:

```text
+ Create
```

Select:

```text
SQL database
```

#### Explanation  

This opens the SQL Database creation wizard.

---

### Step 4: Configure Database Basics  

Fill the required details:

| Field | Value |
|---|---|
| Subscription | Azure Free Labs |
| Resource Group | Existing Resource Group |
| Database Name | `xfusion-sqldb` |
| Region | `Central US` |

#### Explanation  

The database name uniquely identifies the Azure SQL Database resource.

---

### Step 5: Create SQL Server  

Under Server:

Click:

```text
Create new
```

Configure:

| Field | Value |
|---|---|
| Server Name | `xfusion-server-6350` |
| Location | `Central US` |
| Authentication Method | SQL authentication |
| Admin Username | `xfusion-admin` |
| Password | Strong password |

Click:

```text
OK
```

#### Explanation  

Azure SQL Server acts as the logical hosting server for Azure SQL Databases.

---

### Step 6: Configure Compute and Storage  

Under:

```text
Compute + storage
```

Click:

```text
Configure database
```

Select:

| Setting | Value |
|---|---|
| Service Tier | `Basic` |
| Database Size | `2 GiB` |

Click:

```text
Apply
```

#### Explanation  

The Basic tier is suitable for lightweight and less demanding workloads.

---

### Step 7: Configure Backup Storage Redundancy  

Under:

```text
Backup storage redundancy
```

Select:

```text
Locally-redundant backup storage
```

#### Explanation  

Locally-redundant storage keeps database backups replicated within the same Azure region.

---

### Step 8: Configure Networking  

Under Networking:

Enable:

```text
Public endpoint
```

Enable:

```text
Allow Azure services and resources to access this server
```

Keep remaining settings as default.

#### Explanation  

This allows controlled public accessibility to the Azure SQL Database.

---

### Step 9: Review and Create  

Click:

```text
Review + create
```

After validation succeeds:

Click:

```text
Create
```

#### Explanation  

Azure validates and deploys the SQL Database resources.

---

### Step 10: Verify Database Deployment  

Open:

```text
SQL databases
```

Select:

```text
xfusion-sqldb
```

Verify:

| Property | Expected Value |
|---|---|
| Database Name | `xfusion-sqldb` |
| Status | `Ready / Online` |
| Server Name | `xfusion-server-6350` |
| Region | `Central US` |

#### Explanation  

This confirms successful deployment and database availability.

---

### Step 11: Verify Using Azure CLI  

Check database status:

```bash
az sql db show \
--name xfusion-sqldb \
--resource-group kml_rg_main-c41fd61fd17f4571 \
--server xfusion-server-6350 \
--output table
```

List databases:

```bash
az sql db list \
--resource-group kml_rg_main-c41fd61fd17f4571 \
--server xfusion-server-6350 \
--output table
```

#### Explanation  

Azure CLI helps verify deployment and manage SQL Database resources programmatically.

---

## Best Practices  

- Use strong SQL authentication credentials  
- Select appropriate compute tiers based on workload requirements  
- Enable backup redundancy for data protection  
- Restrict public access whenever possible  
- Monitor database performance and usage regularly  
- Apply least privilege access principles  

---

## Key Learnings  

- Azure SQL Database is a fully managed relational database service  
- Azure SQL Server logically manages SQL Databases  
- Basic compute tier is suitable for lightweight workloads  
- Backup redundancy improves database reliability and recovery  
- Azure Portal and Azure CLI simplify cloud database management  
- Cloud databases improve scalability, availability, and operational efficiency  

---

Step by step, improving Cloud Database and DevOps skills 🚀
