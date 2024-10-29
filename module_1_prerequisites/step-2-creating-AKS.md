# **Step-by-Step Guide to Creating the Kubernetes Cluster in Azure**

#  **1. Access the Kubernetes Cluster Creation Wizard in Azure**

1. Log in to your Azure portal at [portal.azure.com](https://portal.azure.com).
2. In the search bar at the top of the portal, type **Kubernetes services** and select it from the list of services.
3. Click on **+ Create** to start the Kubernetes cluster creation process.

---

#### **2. Configure Basic Cluster Settings**

Under the **Basics** tab:

1. **Subscription**: Select **Free Trial** to use Azure’s free resources.
2. **Resource Group**: Select or create **demo-resource-group**. 
3. **Cluster Preset Configuration**: Choose **Dev/Test**. This preset is optimized for demonstration purposes and is cost-effective.
4. **Kubernetes Cluster Name**: Enter `demoKubernetesCluster`.
5. **Region**: Select **East US**.
6. **Availability Zones**: Set to **None** for this demo configuration.
7. **AKS Pricing Tier**: Select **Free** to keep the cluster within the free tier options.

---

#### **3. Configure Kubernetes Version and Upgrade Settings**

1. **Kubernetes Version**: Select **1.27.7** (the default version available).
2. **Automatic Upgrade**: Set to **Disabled** to manually control version upgrades.

---

#### **4. Set Authentication and Authorization Options**

1. **Authentication Method**: Choose **Local Accounts with Kubernetes RBAC** to enable Role-Based Access Control for added security.
   
---

#### **5. Configure Node Security and Scheduling**

1. **Node Security Channel Type**: Set **Node Image** as the security channel type.
2. **Scheduler Option**: Choose **No Schedule** to prevent unnecessary load on nodes reserved for security tasks.

---

This configuration establishes the foundational setup for your Kubernetes cluster in Azure, ensuring a cost-effective environment with essential RBAC controls and custom version management, ideal for DevSecOps testing. 

Let me know if you’re ready to proceed to the next steps, where we’ll create and co
### **Step 3: Configuring Node Pools for Kubernetes Cluster**

In this step, we will configure the node pools for our Kubernetes cluster to define the resource allocation and scaling behavior for the nodes that make up the cluster. 

---

#### **Understanding Node Pool Quotas and Limitations (Free Tier)**

In the **Free Tier** of Azure, there is a **quota limit of 4 node pools** with a total capacity of **4 vCPUs**. This means that:

- If you use two nodes, each can have **2 vCPUs**.
- This limit is ideal for lightweight applications or demos, like this DevSecOps project.

> **Note:** If you upgrade to a paid tier, these limitations can be lifted, allowing for additional CPU resources and node pools.

---

#### **Node Pool Configuration Steps**

1. **Delete the Default System Node Pool (Optional for Paid Tier)**
   - Since the Free Tier has limited capacity, delete the default **system node pool** created by Azure.
   - This ensures that your cluster’s quota is optimized for the nodes you configure manually.

2. **Add a New Node Pool (System Node)**

   Configure the node pool settings for your system node as follows:

   - **Node Pool Name**: `demosysnode`
   - **Mode**: Select **System** to designate this as the main node pool handling essential cluster operations.
   - **OS SKU**: Choose **Azure Linux** (Linux is required for system node pools).
   - **Availability Zones**: Select **None**.
   - **Enable Azure Spot Instances**: Leave **Disabled** (Spot instances are not compatible with system node pools).
   - **Node Size**: Set to **Standard B2pls v2** (2 vCPUs, 4 GiB memory).
   - **Scale Method**: Choose **Manual** or **Autoscale** (recommended for automatic scaling).
   - **Node Count**: Set to **1** node.
   - **Max Pods per Node**: Set to **30** (can be adjusted between 30 - 250).
   - **Enable Public IP per Node**: Leave **Disabled** (optional for this demo).

3. **Add a New Node Pool (User Node)**

   We will now add a **User Node** pool with similar settings to support the application workloads in the cluster.

   - Configure the **User Node** settings similarly, making sure it is designated for workload handling.

---

This setup provides a flexible, efficient foundation within Azure’s Free Tier, allocating resources specifically for system functions and user workloads. When ready, we’ll proceed to containerize and deploy the application on this Kubernetes infrastructure. Let me know if you’d like further customization details!

### **Step 4: Configuring the User Node Pool in Kubernetes Cluster**

With the system node pool configured, we’ll now add a **user node pool** that will manage our application workloads within the Kubernetes cluster. This setup allows us to distribute the cluster's responsibilities, separating system processes from user-defined workloads.

---

#### **User Node Pool Configuration**

Configure the settings for the **User Node Pool** as follows:

1. **Node Pool Name**: Set as `demousermode`.

2. **Mode**: Select **User**.  
   - This designation focuses on handling application workloads, leaving essential cluster processes to the system node pool.

3. **OS SKU**: Choose **Azure Linux** for consistency, though **Ubuntu Linux** and Windows versions (2022 or 2019) are also available.

4. **Availability Zones**: Select **Zone 1** to ensure the user node pool resides in the same geographic zone for optimized latency and failover.

5. **Enable Azure Spot Instances**: Leave **Disabled**.
   - Spot instances are cost-effective but can lead to interruptions, making them better suited for non-critical tasks.

6. **Node Size**: Set to **Standard D2pds v5** (2 vCPUs, 8 GiB memory).
   - This configuration provides more memory, useful for handling multiple application containers.

7. **Scale Method**: Choose **Autoscale** (recommended).
   - Autoscaling dynamically adjusts the node count based on workload requirements, ensuring optimal resource usage without manual intervention.

8. **Node Count**: Set the **initial count to 3 nodes**.
   - This configuration allows for better load distribution and redundancy within the user node pool.

9. **Optional Settings**
   - **Max Pods per Node**: Set to **30** (adjustable between 10 - 250).
   - **Enable Public IP per Node**: Leave **Disabled** (recommended unless each node requires individual external access).

---

With the **system** and **user node pools** set up, your Kubernetes cluster is now ready for deploying applications securely and efficiently. This two-tiered node configuration ensures separation of concerns, with system nodes dedicated to core functions and user nodes handling scalable workloads.

Let me know when you're ready to move forward or if you need additional customization!

### **Step 5: Configuring Networking for the Kubernetes Cluster**

Configuring networking is a critical step to control how your Kubernetes cluster communicates within the Azure environment and with external resources. We’ll use the **kubenet** network plugin, a simple and effective choice for smaller clusters.

---

#### **Networking Configuration**

1. **Public Access**  
   - **Set Authorized IP Ranges**: Define which IP ranges can access the cluster if public access is enabled. By default, all IP ranges are blocked unless specified, enhancing security by controlling access to the Kubernetes API server.

2. **Container Networking**
   - **Network Configuration**: Choose **kubenet**.
     - **Kubenet** is a lightweight network model that works well with smaller clusters and is simple to set up. Each node gets a unique IP, and traffic between nodes is routed through Azure's internal network.

3. **Bring Your Own Azure Virtual Network (VNet)**
   - **Disabled** by default for a basic setup.
   - **Note**: You can enable this if you want to connect the cluster to an existing Azure VNet for more control over network traffic and security.

4. **DNS Name Prefix**
   - Set as `demoKubernetesCluster-dns`.
     - This prefix will be used to create a fully qualified domain name (FQDN) for the cluster, facilitating identification and access.

5. **Network Policy**
   - **None** (default).
     - Azure Network Policies, which control the communication between pods, can be enabled later if you need more advanced network security configurations.

6. **Load Balancer**
   - Choose **Standard**.
     - The **Standard Load Balancer** offers higher scalability and additional security options compared to the Basic Load Balancer, ideal for production-ready clusters. 

---

With the networking configured, your cluster is now accessible via controlled public IP ranges, and its container networking is optimized for smaller deployments. The **Standard Load Balancer** adds a robust layer for managing inbound and outbound traffic efficiently.

Let me know if you'd like to continue with further configuration or any additional clarifications on networking!

### **Finalizing Cluster Configuration**

1. **Set Other Options to Default**  
   For this demo setup, all remaining configuration settings that we haven’t explicitly defined can remain at their default values. This keeps the setup straightforward and avoids additional complexity.

2. **Review and Create**  
   - Once all fields are configured as described:
     - Click **Review + Create** at the bottom of the page.
   - **Azure Validation**: Azure will validate the configuration settings you’ve entered. If there are any errors, they’ll appear here for correction.
   - **Create the Cluster**: If everything passes validation, click **Create** to begin the cluster deployment process.

---

### **Deployment Confirmation**
Once you press **Create**, Azure will start provisioning your Kubernetes cluster. This process may take a few minutes. Upon completion, you’ll see a notification in the Azure portal confirming the successful creation of `demoKubernetesCluster`.

---

Your Azure Kubernetes Service (AKS) cluster is now up and running, configured with secure networking, basic node pools, and an accessible DNS prefix. This setup serves as the foundation for deploying containerized applications securely and efficiently in Azure.


