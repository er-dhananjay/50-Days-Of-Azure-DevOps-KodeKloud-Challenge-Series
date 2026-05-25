# Day 29 – Working with Azure Container Registry (ACR)

---

## Task Overview  

The Nautilus DevOps team worked on managing containerized application images using Microsoft Azure Container Registry (ACR). As part of this task, a private Azure Container Registry was created, a Docker image was built from a Dockerfile, and the image was pushed successfully to ACR.

Azure Container Registry helps securely store and manage Docker container images for cloud-native applications and DevOps deployment workflows.

The task includes:

- Creating an Azure Container Registry (ACR)
- Using Azure CLI for container registry management
- Building Docker images from Dockerfiles
- Tagging Docker images for ACR
- Pushing container images to Azure Container Registry
- Verifying repositories and image tags
- Understanding containerization workflows in Azure

---

## Step-by-Step Implementation  

### Step 1: Login to Azure Portal  

Open the Azure Portal:

https://portal.azure.com

Login using your Azure credentials.

#### Explanation  

The Azure Portal is Microsoft Azure’s web-based management platform used to manage cloud resources and services.

---

### Step 2: Login Using Azure CLI  

Open Azure Cloud Shell or terminal.

Authenticate using Azure CLI:

```bash
az login
```

#### Explanation  

The `az login` command authenticates your Azure account for CLI-based cloud resource management.

---

### Step 3: Verify Azure Subscription  

Check available subscriptions:

```bash
az account show --output table
```

#### Explanation  

This verifies the currently active Azure subscription.

---

### Step 4: Verify Available Resource Groups  

List Resource Groups:

```bash
az group list --output table
```

#### Explanation  

Resource Groups organize Azure resources logically within a subscription.

---

### Step 5: Create Azure Container Registry (ACR)  

Create a Basic tier ACR in East US:

```bash
az acr create \
--resource-group kml_rg_main-531817c5b854475a \
--name devopsacr29734 \
--sku Basic \
--location eastus
```

#### Explanation  

Azure Container Registry provides a private container image repository for storing Docker images securely.

---

### Step 6: Verify ACR Creation  

Check ACR details:

```bash
az acr list --output table
```

#### Explanation  

This confirms that the Azure Container Registry was created successfully.

---

### Step 7: Login to Azure Container Registry  

Authenticate Docker with ACR:

```bash
az acr login --name devopsacr29734
```

#### Explanation  

This command allows Docker to interact with Azure Container Registry securely.

---

### Step 8: Navigate to Application Directory  

Move to the Dockerfile location:

```bash
cd /root/pyapp
```

Verify files:

```bash
ls
```

Expected output:

```text
Dockerfile
```

#### Explanation  

The Dockerfile contains instructions for building the container image.

---

### Step 9: Build Docker Image  

Build the Docker image:

```bash
docker build -t devopsacr29734:latest .
```

#### Explanation  

Docker builds the application image using instructions defined inside the Dockerfile.

---

### Step 10: Tag Docker Image for ACR  

Tag the image:

```bash
docker tag devopsacr29734:latest devopsacr29734.azurecr.io/devopsacr29734:latest
```

#### Explanation  

Tagging associates the local image with the Azure Container Registry repository.

---

### Step 11: Push Docker Image to ACR  

Push the image:

```bash
docker push devopsacr29734.azurecr.io/devopsacr29734:latest
```

#### Explanation  

This uploads the Docker image to Azure Container Registry.

---

### Step 12: Verify Repository and Tags  

Check repositories:

```bash
az acr repository list \
--name devopsacr29734 \
--output table
```

Check image tags:

```bash
az acr repository show-tags \
--name devopsacr29734 \
--repository devopsacr29734 \
--output table
```

Expected output:

```text
latest
```

#### Explanation  

This confirms that the Docker image was successfully pushed to Azure Container Registry.

---

## Best Practices  

- Use private container registries for secure image management  
- Use proper image tagging strategies such as versioning  
- Scan container images regularly for vulnerabilities  
- Avoid storing secrets inside Docker images  
- Use lightweight base images for better performance  
- Automate image builds and deployments using CI/CD pipelines  

---

## Key Learnings  

- Azure Container Registry securely stores Docker container images  
- Azure CLI simplifies ACR management and authentication  
- Docker images can be built and pushed directly to ACR  
- Container registries are essential for cloud-native deployments  
- Image tagging helps manage container versions efficiently  
- Containerization improves portability and scalability of applications  

---

Step by step, improving Containerization and Cloud DevOps skills 🚀
