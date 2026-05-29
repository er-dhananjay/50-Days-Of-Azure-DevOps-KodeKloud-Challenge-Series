# Day 33 – Integrating Virtual Machines with Application Load Balancer

---

## Task Overview

The Nautilus DevOps team worked on integrating an Azure Virtual Machine running Nginx with an Azure Load Balancer. The objective was to provide a single public entry point for incoming traffic while ensuring application availability and health monitoring through load balancing components.

This task involved:

- Creating an Azure Load Balancer
- Configuring a Public IP address
- Creating a Backend Pool
- Adding a Virtual Machine to the Backend Pool
- Creating a Health Probe
- Configuring a Load Balancer Rule
- Updating NSG rules to allow HTTP traffic
- Verifying connectivity through the Load Balancer

---

## Step-by-Step Implementation

### Step 1: Verify Existing Virtual Machine

List available VMs:

```bash
az vm list --show-details --output table
```

#### Explanation

This helps identify the VM running Nginx that will be added to the Load Balancer.

---

### Step 2: Find the VM Network Interface

```bash
az vm show \
--name devops-vm \
--resource-group kml_rg_main-5acffc5830754691 \
--query "networkProfile.networkInterfaces[0].id" \
--output tsv
```

#### Explanation

The NIC is required for backend pool configuration.

---

### Step 3: Create Public IP Address

```bash
az network public-ip create \
--resource-group kml_rg_main-5acffc5830754691 \
--name devops-lb-ip \
--sku Standard
```

#### Explanation

A Public IP provides internet-facing access to the Load Balancer.

---

### Step 4: Create Azure Load Balancer

```bash
az network lb create \
--resource-group kml_rg_main-5acffc5830754691 \
--name devops-lb \
--sku Standard \
--public-ip-address devops-lb-ip \
--frontend-ip-name devops-lb-ip \
--backend-pool-name devops-backend-pool
```

#### Explanation

Creates the Load Balancer with frontend and backend configurations.

---

### Step 5: Verify NIC IP Configuration

```bash
az network nic ip-config list \
--nic-name devops-vmVMNic \
--resource-group kml_rg_main-5acffc5830754691 \
--output table
```

#### Explanation

Used to identify the IP configuration attached to the VM NIC.

---

### Step 6: Add VM to Backend Pool

```bash
az network nic ip-config address-pool add \
--address-pool devops-backend-pool \
--ip-config-name ipconfigdevops-vm \
--nic-name devops-vmVMNic \
--resource-group kml_rg_main-5acffc5830754691 \
--lb-name devops-lb
```

#### Explanation

Associates the VM NIC with the Load Balancer backend pool.

---

### Step 7: Create Health Probe

```bash
az network lb probe create \
--resource-group kml_rg_main-5acffc5830754691 \
--lb-name devops-lb \
--name devops-health-probe \
--protocol Tcp \
--port 80
```

#### Explanation

The probe checks whether Nginx is responding on port 80.

---

### Step 8: Create Load Balancer Rule

```bash
az network lb rule create \
--resource-group kml_rg_main-5acffc5830754691 \
--lb-name devops-lb \
--name devops-lb-rule \
--protocol Tcp \
--frontend-port 80 \
--backend-port 80 \
--frontend-ip-name devops-lb-ip \
--backend-pool-name devops-backend-pool \
--probe-name devops-health-probe
```

#### Explanation

Routes incoming HTTP traffic from the Load Balancer to the VM.

---

### Step 9: Allow HTTP Traffic in NSG

```bash
az network nsg rule create \
--resource-group kml_rg_main-5acffc5830754691 \
--nsg-name devops-vmNSG \
--name allow-http \
--priority 1010 \
--direction Inbound \
--access Allow \
--protocol Tcp \
--destination-port-ranges 80
```

#### Explanation

Allows external HTTP traffic to reach the Nginx server.

---

### Step 10: Retrieve Load Balancer Public IP

```bash
az network public-ip show \
--resource-group kml_rg_main-5acffc5830754691 \
--name devops-lb-ip \
--query ipAddress \
--output tsv
```

#### Explanation

Displays the public IP assigned to the Load Balancer.

---

### Step 11: Verify Application Access

```bash
curl http://<LOAD_BALANCER_PUBLIC_IP>
```

Example:

```bash
curl http://20.120.19.92
```

#### Expected Output

```html
Welcome to nginx!
```

#### Explanation

Confirms that traffic is successfully reaching the backend VM through the Azure Load Balancer.

---

## Best Practices

- Use Health Probes for backend monitoring
- Restrict NSG rules to required ports only
- Use Standard SKU Load Balancers for production workloads
- Monitor backend health regularly
- Use multiple backend VMs for high availability
- Implement HTTPS for secure communication

---

## Key Learnings

- Azure Load Balancer distributes traffic across backend resources
- Backend Pools connect application servers to the Load Balancer
- Health Probes ensure only healthy instances receive traffic
- NSG rules control inbound and outbound traffic
- Public IPs provide external access to cloud applications
- Load balancing improves application availability and scalability

---

Step by step, improving Azure, Networking, and DevOps skills 🚀
