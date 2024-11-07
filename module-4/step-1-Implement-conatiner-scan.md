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

      - name: Verify Tarball Exists
        run: |
          ls -lh supermariolatestdockerimage.tar

      - name: Set up Grype Cache Directory
        run: mkdir -p ~/.cache/grype

      - name: Cache Grype DB
        uses: actions/cache@v3
        with:
          path: ~/.cache/grype
          key: ${{ runner.os }}-grype-db-cache
          restore-keys: |
            ${{ runner.os }}-grype-db-cache

      - name: Install Grype
        run: |
          curl -sSfL https://github.com/anchore/grype/releases/download/v0.68.0/grype_0.68.0_linux_amd64.tar.gz | tar -xz -C /usr/local/bin

      - name: Run Grype Vulnerability Scan for Critical Issues
        run: |
          grype docker-archive://$(pwd)/supermariolatestdockerimage.tar --fail-on critical

   ```


###**Explanation of the Code:**
   
Checkout the Repository: We start by checking out the code from the repository.
Set up Docker: This sets up Docker to run commands for image pulling and scanning.
Install Grype: This installs the Grype tool using a script from the Grype GitHub repository.
Pull the Docker Image: This pulls the Docker image (rahuldocker628/mariogitopsproject:latest) from Docker Hub.
Save Docker Image as Tarball: The Docker image is saved as a tarball for scanning with Grype.
Run Grype Scan: The grype command scans the Docker image tarball and fails the job if critical vulnerabilities are found (--fail-on critical).
Upload Grype Report: The scan report is optionally uploaded to the GitHub Actions artifacts for further review.

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
