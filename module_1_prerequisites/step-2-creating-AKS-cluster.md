# Step-by-Step Guide to Creating the Kubernetes Cluster in Azure

## 1. Access the Kubernetes Cluster Creation Wizard in Azure
- **Log in** to your Azure portal at [portal.azure.com](https://portal.azure.com).
- In the search bar at the top of the portal, type **Kubernetes services** and select it from the list of services.
- Click on **+ Create** to start the Kubernetes cluster creation process.

---

## 2. Configure Basic Cluster Settings
Under the **Basics** tab:

- **Subscription**: Select **Free Trial** to use Azure’s free resources.
- **Resource Group**: Select or create `demo-resource-group`.
- **Cluster Preset Configuration**: Choose **Dev/Test**. This preset is optimized for demonstration purposes and is cost-effective.
- **Kubernetes Cluster Name**: Enter `demoKubernetesCluster`.
- **Region**: Select **East US**.
- **Availability Zones**: Set to **None** for this demo configuration.
- **AKS Pricing Tier**: Select **Free** to keep the cluster within the free tier options.

---

## 3. Configure Kubernetes Version and Upgrade Settings
- **Kubernetes Version**: Select **1.27.7** (the default version available).
- **Automatic Upgrade**: Set to **Disabled** to manually control version upgrades.

---

## 4. Set Authentication and Authorization Options
- **Authentication Method**: Choose **Local Accounts** with Kubernetes RBAC to enable **Role-Based Access Control** for added security.

---

## 5. Configure Node Security and Scheduling
- **Node Security Channel Type**: Set **Node Image** as the security channel type.
- **Scheduler Option**: Choose **No Schedule** to prevent unnecessary load on nodes reserved for security tasks.

---

This configuration establishes the foundational setup for your Kubernetes cluster in Azure, ensuring a cost-effective environment with essential RBAC controls and custom version management, ideal for DevSecOps testing.

---

## Step 3: Configuring Node Pools for Kubernetes Cluster

In this step, we will configure the node pools for our Kubernetes cluster to define the resource allocation and scaling behavior for the nodes that make up the cluster.

### Understanding Node Pool Quotas and Limitations (Free Tier)
- **Free Tier Quotas**: The Free Tier of Azure has a quota limit of 4 node pools with a total capacity of 4 vCPUs. This means:
  - If you use two nodes, each can have 2 vCPUs.
- This limit is ideal for lightweight applications or demos like this DevSecOps project.
- **Note**: If you upgrade to a paid tier, these limitations can be lifted, allowing for additional CPU resources and node pools.

### Node Pool Configuration Steps

#### 1. Delete the Default System Node Pool (Optional for Paid Tier)
- Since the Free Tier has limited capacity, delete the default system node pool created by Azure.
- This ensures that your cluster’s quota is optimized for the nodes you configure manually.

#### 2. Add a New Node Pool (System Node)
Configure the node pool settings for your system node:

- **Node Pool Name**: `demosysnode`
- **Mode**: Select **System** to designate this as the main node pool handling essential cluster operations.
- **OS SKU**: Choose **Azure Linux** (Linux is required for system node pools).
- **Availability Zones**: Select **None**.
- **Enable Azure Spot Instances**: Leave **Disabled**.
- **Node Size**: Set to **Standard B2pls v2** (2 vCPUs, 4 GiB memory).
- **Scale Method**: Choose **Manual** or **Autoscale** (recommended for automatic scaling).
- **Node Count**: Set to **1 node**.
- **Max Pods per Node**: Set to **30** (can be adjusted between 30 - 250).
- **Enable Public IP per Node**: Leave **Disabled**.

#### 3. Add a New Node Pool (User Node)
Now, configure the User Node pool for application workloads:

- **Node Pool Name**: `demousermode`
- **Mode**: Select **User**.
- **OS SKU**: Choose **Azure Linux**.
- **Availability Zones**: Select **Zone 1** for optimized latency.
- **Enable Azure Spot Instances**: Leave **Disabled**.
- **Node Size**: Set to **Standard D2pds v5** (2 vCPUs, 8 GiB memory).
- **Scale Method**: Choose **Autoscale**.
- **Node Count**: Set the initial count to **3 nodes**.

### Optional Settings:
- **Max Pods per Node**: Set to **30**.
- **Enable Public IP per Node**: Leave **Disabled** (recommended unless external access is needed).

---

## Step 4: Configuring the User Node Pool in Kubernetes Cluster
With the system node pool configured, add a user node pool to manage application workloads.

User Node Pool Configuration:

- **Node Pool Name**: Set as `demousermode`.
- **Mode**: Select **User** for handling application workloads.
- **OS SKU**: Choose **Azure Linux**.
- **Availability Zones**: Select **Zone 1**.
- **Node Size**: Set to **Standard D2pds v5** (2 vCPUs, 8 GiB memory).
- **Scale Method**: Choose **Autoscale**.
- **Node Count**: Set the initial count to **3 nodes**.

---

## Step 5: Configuring Networking for the Kubernetes Cluster

### Networking Configuration
- **Public Access**: Set **Authorized IP Ranges** to control which IPs can access the cluster. By default, all IP ranges are blocked for enhanced security.
- **Container Networking**: Use **kubenet**, which is lightweight and effective for small clusters.
- **Bring Your Own Azure Virtual Network (VNet)**: Disabled by default.
- **DNS Name Prefix**: Set as `demoKubernetesCluster-dns`.
- **Network Policy**: None (default).
- **Load Balancer**: Choose **Standard** for higher scalability and security options.

---

## Finalizing Cluster Configuration

### 1. Set Other Options to Default
For this demo setup, leave all remaining configuration settings at their default values to avoid unnecessary complexity.

### 2. Review and Create
- Once all fields are configured, click **Review + Create** at the bottom of the page.
- **Azure Validation**: Azure will validate your configuration. If any errors occur, they will be displayed for correction.
- **Create the Cluster**: If validation passes, click **Create** to deploy the cluster.

### 3. Deployment Confirmation
Once you click **Create**, Azure will start provisioning your Kubernetes cluster. This process may take several minutes. Upon completion, a notification will confirm the successful creation of your Kubernetes cluster (`demoKubernetesCluster`).

Your Azure Kubernetes Service (AKS) cluster is now up and running, configured with secure networking, basic node pools, and an accessible DNS prefix.

---

This setup serves as the foundation for deploying containerized applications securely and efficiently within Azure’s Kubernetes infrastructure. Let me know if you’d like further customization or details on deploying your applications!
