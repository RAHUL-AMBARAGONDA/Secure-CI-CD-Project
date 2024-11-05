# Step-by-Step Guide: Implementing GitOps for Super Mario Docker Image

This guide provides instructions for setting up a GitOps workflow to build and push the Super Mario Docker image to Docker Hub with a static tag using GitHub Actions.

---

## Steps Involved

### Step 1: Create a YAML File for GitOps Workflow

1. In your `.github/workflows` directory, create a new YAML file named `gitops-build-push-supermario-image.yaml`.

### Step 2: Add the GitHub Actions Workflow Code

1. Copy and paste the following code into `gitops-build-push-supermario-image.yaml`:

    ```yaml
    name: "Build and push Super Mario Docker image with static tag to Docker Hub"
     
    on:
      push:
        branches:
          - main
     
    jobs:
     
      build_push_supermario_docker_image:
        runs-on: ubuntu-latest
     
        steps:
          - name: Checkout Repository
            uses: actions/checkout@v3
     
          - name: Login to Docker Hub
            run: echo "${{ secrets.DOCKERHUB_TOKEN }}" | docker login -u "${{ secrets.DOCKERHUB_USERNAME }}" --password-stdin
     
          - name: Build and Push Docker Image
            run: |
              docker build -t docker.io/raghuthesecurityexpert/supermariogitopsproject:1 .
              docker push docker.io/raghuthesecurityexpert/supermariogitopsproject:1
    ```

--- 

Continue with the next steps after adding this YAML code.

