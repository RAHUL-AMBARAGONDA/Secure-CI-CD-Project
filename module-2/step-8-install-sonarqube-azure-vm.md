
### Step-by-Step Lab Guide to Create a VM in Azure (with Default Settings)

#### Step 1: Sign in to the Azure Portal
1. Open your web browser and go to the [Azure Portal](https://portal.azure.com).
2. Sign in with your Azure account credentials.

#### Step 2: Create a Virtual Machine
1. In the Azure portal, click on **Virtual machines** from the left-hand menu.
2. Click on the **+ Create** button, then select **Azure virtual machine**.

#### Step 3: Configure Project Details

![Screenshot (20)](https://github.com/user-attachments/assets/8d17b505-70a8-44ee-a350-10acf543de0f)

1. **Subscription**: Select your subscription (e.g., **Free Trial**).
2. **Resource group**: Choose the previously created resource group (`demo-resource-group`).
3. **Virtual machine name**: Enter `sonar-vm`.
4. **Region**: Select **(Europe) UK West**.
5. **Availability options**: Select **No infrastructure redundancy required** (default).
6. **Security type**: Choose **Trusted launch virtual machines** (default).

#### Step 4: Configure Image and Size

![Screenshot (22)](https://github.com/user-attachments/assets/a5e78221-2fc6-403d-9617-083a2df3d131)

1. **Image**: From the dropdown, select **Ubuntu Pro 24.04 LTS - x64 Gen2** (default).
2. **VM architecture**: Select **x64** (default).
3. **Size**: Click on **See all sizes**. Choose **Standard_B2s - 2 vCPUs, 4 GiB memory** (default).
4. **Enable Hibernation**: Ensure this is disabled as it does not support Trusted launch for Linux images (default).

#### Step 5: Configure Administrator Account



Authentication type: Select Password instead of SSH public key.
Username: Enter azureuser (default).
Password: Enter a strong password (ensure it meets Azure's password complexity requirements).

#### Step 6: Configure Inbound Port Rules
1. **Public inbound ports**: Select **Allow selected ports** (default).
2. **Select inbound ports**: Choose **SSH (22)** (default).

#### Step 7: Review and Create
1. After configuring all settings, click on **Review + create**.
2. Review your settings and ensure everything is correct.
3. Click on **Create** to provision the virtual machine.

#### Step 8: Access Your Virtual Machine
Once the VM is created, navigate to the Virtual machines section.

Click on sonar-vm to view its details.

To connect via SSH, use a terminal or SSH client. Run the following command (replace <public-ip> with the actual public IP of your VM):

bash
Copy code
ssh azureuser@<public-ip>
Note: You will be prompted to enter the password you set during the VM creation.

### Conclusion
You have successfully created a virtual machine in Azure named `sonar-vm` within the `demo-resource-group`, using default settings for all other sections. You can now access it using SSH and begin your work with this VM.

 

### Now we need to Configure Inbound Port Rules for Your Azure VM

#### Step 1: Navigate to Your Virtual Machine

1. In the left-hand menu, click on **Virtual machines**.
2. From the list of virtual machines, click on the name of your VM (e.g., **sonar-vm**).

#### Step 2: Go to Networking Settings
![Screenshot (26)](https://github.com/user-attachments/assets/43520793-0f87-4523-b63e-ab6d3007cf6d)

1. In the left-hand menu of your VM's overview page, scroll down and click on **Networking**.

#### Step 3: Configure Inbound Port Rules
1. In the **Networking** pane, you will see the **Inbound port rules** section.
2. By default, Azure may have created a rule for SSH (port 22). To add an additional rule, click on **Add inbound port rule**.

#### Step 4: Set Up the New Inbound Port Rule
1. In the **Add inbound security rule** pane, configure the following settings:
   - **Destination port ranges**: Enter `9000`.
   - **Protocol**: Select **TCP** from the dropdown menu.
   - **Name**: Optionally, you can enter a name for this rule (e.g., `TCP-9000`).
   - **Priority**: Leave this at the default or adjust as needed (lower numbers indicate higher priority).
   - **Action**: Ensure this is set to **Allow**.

2. After entering the necessary information, click on **Add** to create the inbound port rule.

#### Step 5: Verify the Inbound Port Rule
1. After adding the rule, you will return to the **Networking** pane.
2. Under **Inbound port rules**, verify that the new rule for TCP port `9000` is listed alongside the existing rules.

### Conclusion
You have successfully configured the inbound port rules for your Azure VM, allowing access on TCP port 9000 in addition to SSH (port 22). This configuration enables external traffic to reach your applications that may be running on port 9000, facilitating better functionality and access. If you have any further questions or need additional assistance, feel free to ask!
