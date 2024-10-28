**Module 2: Installing ArgoCD on AKS**

In this module, you’ll connect to your AKS cluster, create a namespace for ArgoCD, install ArgoCD, and set up a LoadBalancer to access the ArgoCD UI. Follow each step carefully to complete the setup.

---
**Prerequisites**
- Azure CLI installed and configured
- AKS cluster created (as completed in Module 1)

---

**Step-by-Step Guide**

**1. Connect to AKS Cluster**

   1. Go to your AKS cluster overview in the Azure Portal.
   2. Click on **Connect**.
   3. Copy the provided command to connect to your cluster and paste it in Azure CLI.
   
   Example:
   ```bash
   az aks get-credentials --resource-group <resource-group> --name <aks-cluster-name>
   ```

**2. Create a Namespace for ArgoCD**

   Run the following command to create a namespace:
   ```bash
   kubectl create namespace argocd
   ```

**3. Install ArgoCD in the `argocd` Namespace**

   Use the following command to install ArgoCD:
   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

**4. Verify ArgoCD Resources**

   After installation, verify that the resources have been created with:
   ```bash
   kubectl get all -n argocd
   ```

**5. Set Up LoadBalancer for External Access**

   To access ArgoCD from a browser, patch the ArgoCD service to use a LoadBalancer:
   ```bash
   kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
   ```

**6. Retrieve LoadBalancer IP and Port**

   Get the LoadBalancer's public IP and port with:
   ```bash
   kubectl get svc -n argocd
   ```

**7. Log into ArgoCD**

   - **Username**: `admin`
   - **Initial Password**: Retrieve it using this command:
     ```bash
     kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
     ```
   - Use the LoadBalancer IP and port to access ArgoCD in your browser and log in.

---

### Additional Notes
- Be sure to replace `<resource-group>` and `<aks-cluster-name>` with your actual resource group and cluster names.
- The default ArgoCD admin password is encoded in a Kubernetes secret; remember to change the password after logging in.

