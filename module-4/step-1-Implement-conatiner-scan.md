

# Docker Image Vulnerability Scan - GitHub Actions Workflow

## Overview

This repository contains a GitHub Actions workflow that scans Docker images for vulnerabilities using [Grype](https://github.com/anchore/grype). It ensures that images pushed to Docker Hub are scanned for critical vulnerabilities.

This workflow is triggered on every push to the `main` branch and performs the following tasks:
1. **Pull the Docker image** from Docker Hub.
2. **Save the Docker image as a tarball**.
3. **Scan the Docker image** for critical vulnerabilities using Grype.
4. **Allow the workflow to pass even with vulnerabilities** by forcing a successful exit code (`exit 0`).

## Workflow Configuration

The workflow is configured in a GitHub Actions YAML file and is stored in `.github/workflows/docker-image-vulnerability-scan.yml`.

### Key Steps in the Workflow

1. **Checkout Repository**:  
   The first step checks out the repository so that the workflow can access the required files.

2. **Login to Docker Hub**:  
   Logs into Docker Hub using credentials stored as GitHub Secrets.

3. **Pull Docker Image**:  
   Pulls the Docker image from Docker Hub based on the version stored in `version.txt`.

4. **Save Docker Image as Tarball**:  
   Converts the pulled Docker image into a tarball to facilitate scanning.

5. **Verify Tarball Exists**:  
   Verifies that the tarball file is created successfully.

6. **Install and Configure Grype**:  
   Grype is installed to scan Docker images. It is cached to improve scan performance for subsequent runs.

7. **Run Grype Vulnerability Scan**:  
   The Docker image tarball is scanned using Grype. Critical vulnerabilities are reported, but the workflow allows passing even if vulnerabilities are found.

### Complete YAML Workflow

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
          grype docker-archive://$(pwd)/supermariolatestdockerimage.tar --fail-on critical || exit 0
```

### Key Notes:
- **Secrets Configuration**: Make sure to configure your Docker Hub username and token as GitHub Secrets. These will be used in the workflow for authentication.
  - `DOCKERHUB_USERNAME`
  - `DOCKERHUB_TOKEN`

- **Grype Tool**: Grype is used for scanning Docker images for vulnerabilities. In this workflow, we set it up to fail on critical vulnerabilities but allow the workflow to complete with an exit code of `0`, ensuring it does not fail due to vulnerabilities found during the scan.

## How to Use

1. **Set Up DockerHub Secrets**:  
   Ensure you have added your Docker Hub credentials in the repository secrets:
   - `DOCKERHUB_USERNAME`
   - `DOCKERHUB_TOKEN`

2. **Push to Main Branch**:  
   Whenever you push changes to the `main` branch, the GitHub Action workflow will automatically trigger. It will scan the Docker image for vulnerabilities and provide a report.

3. **View Action Results**:  
   You can monitor the results of the workflow in the **Actions** tab of the GitHub repository. If vulnerabilities are found, they will be reported, but the workflow will pass due to the `exit 0` command.

## Conclusion

This workflow helps automate the process of scanning Docker images for vulnerabilities in your continuous integration pipeline. By using Grype in combination with GitHub Actions, it integrates vulnerability scanning into your CI/CD process seamlessly. Even if vulnerabilities are found, the scan will allow the workflow to pass and will not cause disruptions in your deployment pipeline.

---

### How to Add This Workflow

1. **Create a `.github/workflows/` directory** if it doesn't exist.
2. **Create a new YAML file** named `docker-image-vulnerability-scan.yml` inside the `workflows` directory.
3. **Copy and paste the YAML configuration** into the newly
