
### Step-by-Step Lab Guide to Create a VM in Azure (with Default Settings)

#### Step 1: Sign in to the Azure Portal
1. Open your web browser and go to the [Azure Portal](https://portal.azure.com).
2. Sign in with your Azure account credentials.

#### Step 2: Create a Virtual Machine
1. In the Azure portal, click on **Virtual machines** from the left-hand menu.
2. Click on the **+ Create** button, then select **Azure virtual machine**.

#### Step 3: Configure Project Details

![Screenshot (21)](https://github.com/user-attachments/assets/2cf13160-636d-4291-91e1-02f2027b42b8)

1. **Subscription**: Select your subscription (e.g., **Free Trial**).
2. **Resource group**: Choose the previously created resource group (`demo-resource-group`).
3. **Virtual machine name**: Enter `sonar-vm`.
4. **Region**: Select **(Europe) UK West**.
5. **Availability options**: Select **No infrastructure redundancy required** (default).
6. **Security type**: Choose **Trusted launch virtual machines** (default).

#### Step 4: Configure Image and Size
1. **Image**: From the dropdown, select **Ubuntu Pro 24.04 LTS - x64 Gen2** (default).
2. **VM architecture**: Select **x64** (default).
3. **Size**: Click on **See all sizes**. Choose **Standard_B2s - 2 vCPUs, 4 GiB memory** (default).
4. **Enable Hibernation**: Ensure this is disabled as it does not support Trusted launch for Linux images (default).

#### Step 5: Configure Administrator Account

![Screenshot (21)](https://github.com/user-attachments/assets/4fa08561-6ba6-4c36-97c7-61b318efa759)

1. **Authentication type**: Select **SSH public key** (default).
2. **Username**: Enter `azureuser` (default).
3. **SSH public key source**: Choose **Generate new key pair** (default).
4. **SSH Key Type**: Select **RSA SSH Format** (default).
5. **Key pair name**: Enter `new-vm` (default).

#### Step 6: Configure Inbound Port Rules
1. **Public inbound ports**: Select **Allow selected ports** (default).
2. **Select inbound ports**: Choose **SSH (22)** (default).

#### Step 7: Review and Create
1. After configuring all settings, click on **Review + create**.
2. Review your settings and ensure everything is correct.
3. Click on **Create** to provision the virtual machine.

#### Step 8: Access Your Virtual Machine
1. Once the VM is created, navigate to the **Virtual machines** section.
2. Click on `sonar-vm` to view its details.
3. To connect via SSH, use a terminal or SSH client. Run the following command (replace `<public-ip>` with the actual public IP of your VM):

   ```bash
   ssh azureuser@<public-ip> -i /path/to/your/private/key
   ```

   Make sure to replace `/path/to/your/private/key` with the path where your private key is stored.

### Conclusion
You have successfully created a virtual machine in Azure named `sonar-vm` within the `demo-resource-group`, using default settings for all other sections. You can now access it using SSH and begin your work with this VM.
