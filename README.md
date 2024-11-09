# Lets Build End-to-End DevSecOps Pipeline for Super Mario Game
![WhatsApp Image 2024-10-26 at 9 43 54 PM](https://github.com/user-attachments/assets/546890df-a20c-4676-82cd-2e0f425914fc)

# Table of Contents

1. Introduction
2. Prerequisites
3. Project Overview
4. Pipeline Architecture
5. Step-by-Step Implementation
6. Clone the Repository
7. Set Up GitHub Actions
8. Configure SonarQube for SAST
9. Dockerize the Mario Game
10. Implement Dynamic Tagging
11. Deploy to AKS with ArgoCD
12. Validate End-to-End Pipeline Execution
13. Conclusion


**Project Introduction:** Secure DevSecOps Pipeline for Infinite Mario Game In this project, we establish a secure, automated DevSecOps pipeline to manage the development, security, and deployment lifecycle of the Infinite Mario JavaScript game. This project demonstrates the full DevSecOps workflow, from code quality checks and security scans to seamless container deployment in a Kubernetes environment. By implementing a robust CI/CD process, we enable automated detection of vulnerabilities, streamlined deployments, and secure infrastructure, all in a highly adaptable, cloud-based setup.

**This project aims to deliver:**

**Automated Code Quality and Security:** Integration with SonarQube for Static Application Security Testing (SAST) to ensure high code quality and detect potential security issues at an early stage. 

**Container Security:** Use of Trivy and other tools to scan for vulnerabilities in container images before deployment.

**Infrastructure-as-Code (IaC):** Efficient deployment and management of the Infinite Mario game within Azure Kubernetes Service (AKS), allowing rapid scaling and seamless updates.

**Continuous Deployment:** Leverage GitHub Actions workflows to automate CI/CD processes, ensuring rapid and reliable releases with every code change.

**Project Prerequisites**

To get started with this project, ensure that the following prerequisites are met:

Clone the Repository
To get started with this project, clone the repository containing the Mario Game project from the forked repository:

bash
Copy code
git clone https://github.com/[your-github-username]/[forked-repo-name].git

Then, follow the step-by-step guide below to set up and deploy the project
**Azure Account:** An active Azure account with a free or paid subscription. Sign up here for a free trial if needed.

**Azure Kubernetes Service (AKS):** Knowledge of creating and managing Kubernetes clusters in Azure. Docker Hub Account: A Docker Hub account to store and manage container images.

**Docker CLI:** Installed on your local machine to build and push images. Get Docker CLI here. GitHub Account: GitHub repository with Actions enabled for automating CI/CD workflows.

**SonarQube:** An active SonarQube instance or account for running SAST scans.

**SonarQube Tokens:** For authentication and integration with GitHub Actions.

**Basic Knowledge of the Following:**

**DevSecOps and CI/CD Pipelines:** Familiarity with GitHub Actions or other CI/CD tools.

**AKS :** Understanding of basic Kubernetes concepts, including nodes, pods, services, and deployments.

**Docker:** Knowledge of Docker basics, including Dockerfile creation, image building, and pushing images to a container registry.

**JavaScript:** Basic understanding to implement modifications to the Infinite Mario game.

**Tools and Technologies Used**

Azure Kubernetes Service (AKS) Docker and Docker Hub SonarQube for SAST Scans GitHub Actions for CI/CD Trivy for Container Security
Pipeline Architecture

**The pipeline workflow integrates the following stages:**


![WhatsApp Image 2024-10-26 at 9 44 21 PM](https://github.com/user-attachments/assets/76c2f2b6-4ff2-48cd-9cfc-11d7bb0e1089)


**Code Commit:** Push code changes to GitHub.

**Build & Test:** Run unit tests and static code analysis using SonarQube.

**Containerization:** Build and push Docker images to Docker Hub.

**Security Scanning:** Scan images with Trivy for vulnerabilities.

**Deployment:** Deploy to AKS using ArgoCD.


## Modules

## Module 1 :DevSecOps Case Study and Prerequisites

[**Step 1:** Creating Azure Free Trail](./module_1_prerequisites/1-azure-account.md)

[**Step 2:** Creating Aks Cluster](./module_1_prerequisites/step-2-creating-AKS-cluster.md)

[**Step 3:** install Argo-Cd on Aks](./module_1_prerequisites/Step-3-install-argocd-on-aks.md)

## Module 2: Integrate Static Application Security Testing (SAST) with SonarQube

[**Step 1.** Install SonarQube on Azure VM Instance](module-2/step-8-install-sonarqube-azure-vm.md)

[**Step 2.** Clone Mario GitHub Repository](module-2/step-9-clone-mario-repo.md)

[**Step 3.** Integrate SonarQube for SAST in DevSecOps Pipeline - Part 1](module-2/step-10-integrate-sonarqube-sast-part1.md)

[**Step 4.** Integrate SonarQube for SAST in DevSecOps Pipeline - Part 2](module-2/step-11-integrate-sonarqube-sast-part2.md)

[**Step 5.** Integrate SonarQube for SAST in DevSecOps Pipeline - Part 3](module-2/step-12-integrate-sonarqube-sast-part3.md)

[**Step 6.** Integrate SonarQube for SAST in DevSecOps Pipeline - Part 4](module-2/step-13-integrate-sonarqube-sast-part4.md)

[**Step 7.** Implement Quality Gates for SAST](module-2/step-14-implement-quality-gates.md)




## Module 3: Dockerization of Mario Game Project## Module 3: Dockerization of Mario Game Project

[**Step 1.** Create a DockerHub Account and DockerHub Repository](module-3/step-1-create-dockerhub-account.md)

[**Step 2.** Write a Dockerfile for Mario Game Project](module-3/step-2-write-dockerfile.md)

[**Step 3.** Build and Push Mario Docker Image to DockerHub Repo - Part 1](module-3/step-3-build-push-mario-docker-image-part1.md)

[**Step 4.** Build and Push Mario Docker Image to DockerHub Repo - Part 2](module-3/step-4-build-push-mario-docker-image-part2.md)

[**Step 5.** Implement Dynamic Tagging for Mario Docker Image](module-3/step-5-implement-dynamic-tagging.md)

### Module 4: Implement Container Scan for Mario Game

 [**Step 1.** Implement Container Scan for Mario Game - Part 1](module-4/step-1-Implement-conatiner-scan.md)

 [**Step 2.** Implement Container Scan for Mario Game - Part 2](module-4/step-2-Implement-container-scan-part-2.md)

### Module 5: Deploy Mario Docker Game on Azure Kubernetes Cluster

 [**Step 1:.** Deploy Mario Game on Azure Kubernetes Cluster using ArgoCD - Part 1](module-5/Deploy-Mario-Game-on-Azure-Kubernetes-Cluster-using-ArgoCD-Part-1.md)
 
 [**Step 2.** Deploy Mario Game on Azure Kubernetes Cluster using ArgoCD - Part 2](module-5/Deploy-Mario-Game-on-Azure-Kubernetes-Cluster-using-ArgoCD-Part-2.md)

### Module 5: Implement End-to-End DevSecOps Pipeline for Mario Game

 [**Step 1**: Understanding End-to-End DevSecOps Pipeline for Mario Game]
 
 [ **Step 2**: Hands-On: Part 1 - Implement End-to-End DevSecOps Pipeline for Mario Game]
 
 [**Step 3**: Hands-On: Part 2 - Implement End-to-End DevSecOps Pipeline for Mario Game]






