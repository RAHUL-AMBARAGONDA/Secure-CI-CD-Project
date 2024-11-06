To maintain consistency, here’s how you can document this step to include using Visual Studio Code to create the YAML file under the `.github/workflows` directory:

```markdown
# Step 6: Pull and Scan Super Mario Docker Image for Vulnerabilities

## Goal of this Step:

To pull the Super Mario Docker image from Docker Hub, run a vulnerability scan on the image, and automatically pass or fail the build based on vulnerability severity.

---

## Steps Involved:

### Step 1: Create the Workflow File

1. Open **Visual Studio Code** and navigate to the root of your repository.
2. In the `.github/workflows` directory, create a new YAML file named `run-container-scan-supermario-image.yaml`.
3. Copy the following code into `run-container-scan-supermario-image.yaml`:

   ```yaml
   name: "Run Container Scan on Super Mario Docker Image with Quality Gate"

   on:
     push:
       branches:
         - main

   env:
     VERSION: $(( $(cat version.txt) + 1 ))

   jobs:

     run_container_image_scan_on_supermario_docker_image:
       runs-on: ubuntu-latest

       steps:
         - name: Checkout Repository
           uses: actions/checkout@v3

         - name: Login to Docker Hub
           run: echo "${{ secrets.DOCKERHUB_TOKEN }}" | docker login -u "${{ secrets.DOCKERHUB_USERNAME }}" --password-stdin

         - name: Get Docker Image from Docker Hub
           run: |
             docker pull docker.io/rahuldocker628/mariogitopsproject:${{ env.VERSION }}
             docker save -o supermariolatestdockerimage.tar docker.io/rahuldocker628/mariogitopsproject:${{ env.VERSION }}

         - name: Run Trivy Vulnerability Scanner in Tarball Mode
           uses: aquasecurity/trivy-action@master
           with:
             input: /github/workspace/supermariolatestdockerimage.tar
             exit-code: '1'
             severity: 'CRITICAL,HIGH'
   ```

   **Explanation of the Code:**
   - **Docker Pull and Save**: This pulls the Docker image from Docker Hub using the version specified in `version.txt` and saves it as `supermariolatestdockerimage.tar`.
   - **Vulnerability Scan**: Trivy scans the tarball for vulnerabilities, specifically looking for any critical or high severity issues. If vulnerabilities at these levels are detected, the build fails, thanks to `exit-code: '1'`.

### Step 2: Save and Push to GitHub

1. After saving the changes in Visual Studio Code, open the terminal in the root of your repository.
2. Run the following commands to commit and push your new workflow:

   ```bash
   git add .github/workflows/run-container-scan-supermario-image.yaml
   git commit -m "Add container scan workflow for Super Mario Docker image"
   git push origin main
   ```

---

Once pushed to GitHub, this workflow will automatically trigger on every push to the `main` branch. It will pull the latest version of the Super Mario Docker image, scan it for vulnerabilities using Trivy, and fail the build if critical or high vulnerabilities are found. This step is crucial for maintaining security in your CI/CD pipeline.
```

This ensures that the instructions are clear, consistent with previous steps, and easy to follow. Let me know if any further adjustments are needed!
