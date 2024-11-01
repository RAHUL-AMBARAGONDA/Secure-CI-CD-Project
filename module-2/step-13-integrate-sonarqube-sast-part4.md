# Step-by-Step Guide to Set Up DevSecOps with SonarQube and GitHub Actions

#### Step 1: Create a Local Directory for Your Project

1. **Open Terminal**: Open your terminal (or command prompt).

2. **Create the Main Directory**:
   ```bash
   mkdir DEV-SEC
   cd DEV-SEC
   ```

3. **Clone Your Existing Project**:
   If you have an existing repository from Visual Studio, clone it using:
   ```bash
   git clone https://github.com/RAHUL-AMBARAGONDA/gitops-practice-devsecops-sonarqube-sast-scan-supermario-repo.git
   cd gitops-practice-devsecops-sonarqube-sast-scan-supermario-repo
   ```

4. **Confirm Directory Structure**:
   ```bash
   ls -la
   ```
   You should see the output similar to:
   ```plaintext
   total 32
   drwxr-xr-x 6 root root 4096 Oct 31 10:28 .
   drwxr-xr-x 4 root root 4096 Oct 31 10:28 ..
   drwxr-xr-x 7 root root 4096 Oct 31 10:28 .git
   drwxr-xr-x 3 root root 4096 Oct 31 10:28 .github
   -rw-r--r-- 1 root root  168 Oct 30 11:21 README.md
   drwxr-xr-x 2 root root 4096 Oct 31 10:28 demo
   -rw-r--r-- 1 root root   42 Oct 30 13:06 sonar-project.properties
   drwxr-xr-x 6 root root 4096 Oct 31 10:28 webapp
   ```

#### Step 2: Configure SonarQube Project

1. **Log into SonarQube**:
   Open your web browser and navigate to your SonarQube instance at `http://<your-azure-vm-ip>:9000`.

2. **Create a New Project**:
   - Click on **Create Project**.
   - Fill in the project key and name.
   - Generate an access token to use in GitHub Actions.

#### Step 3: Set Up GitHub Actions for SAST

1. **Navigate to Your Project Folder**:
   ```bash
   cd .github
   ```

2. **Create Workflow File**:
   Create a file named `sonarqube.yml`:
   ```bash
   nano workflows/sonarqube.yml
   ```

3. **Add the Following Content**:

    name: "Run SAST Scan on SuperMario Game Project"

on:
  push:
    branches:
      - main
  
jobs:

  sonarqube_sast_scan:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3
        with:
          fetch-depth: 0  # Shallow clones should be disabled for better analysis relevance

      - name: SonarQube Scan
        uses: sonarsource/sonarqube-scan-action@master
        env:
          SONAR_HOST_URL: ${{ secrets.SONAR_HOST_URL }}
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
      # If you wish to fail your job when the Quality Gate is red, uncomment the
      # following lines. This would typically be used to fail a deployment.
      - name: SonarQube Quality Gate Check
        uses: sonarsource/sonarqube-quality-gate-action@master
        timeout-minutes: 5
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
  
5. **Save and Exit**:
   If using `nano`, press `CTRL + X`, then `Y`, and `ENTER` to save.

#### Step 4: Add SonarQube Token to GitHub Secrets

1. **Go to Your GitHub Repository**:
   - Click on **Settings**.
   - Click on **Secrets and variables** > **Actions**.

2. **Create New Secret**:
   - Name it `SONAR_TOKEN`.
   - Paste your SonarQube token and click **Add secret**.

#### Step 5: Commit and Push Your Changes

1. **Stage Changes**:
   ```bash
   git add .github/workflows/sonarqube.yml
   ```

2. **Commit Changes**:
   ```bash
   git commit -m "Add SonarQube integration using GitHub Actions"
   ```

3. **Push Changes**:
   ```bash
   git push origin main
   ```

#### Step 6: Verify the GitHub Actions Workflow

1. **Navigate to the Actions Tab**:
   - Go to your GitHub repository on the web.
   - Click on the **Actions** tab.

2. **Check Workflow Status**:
   - You should see the SonarQube Scan job running.
   - Click on it to view the logs and confirm it completed successfully.

#### Step 7: Review SonarQube Results

1. **Return to SonarQube Dashboard**:
   - Go back to your SonarQube instance at `http://<your-azure-vm-ip>:9000`.

2. **View Project Analysis**:
   - Navigate to your project.
   - Review the results of the SAST analysis.
  
   - ![Screenshot (55)](https://github.com/user-attachments/assets/3b78ac3b-63c0-44c1-94ab-1b6197b20e51)


### Summary

You have successfully created a local folder structure, configured SonarQube for SAST integration using GitHub Actions, and pushed your code. You can now monitor your code quality and security directly from the SonarQube dashboard.

Feel free to upload any pictures related to this process or let me know if you need further assistance!
