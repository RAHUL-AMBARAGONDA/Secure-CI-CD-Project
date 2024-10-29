# Lets Build End-to-End DevSecOps Pipeline for Super Mario Game
![WhatsApp Image 2024-10-26 at 9 43 54 PM](https://github.com/user-attachments/assets/546890df-a20c-4676-82cd-2e0f425914fc)

**Table of Contents**
Introduction
Prerequisites
Project Overview
Pipeline Architecture
Step-by-Step Implementation
1. Clone the Repository
2. Set Up GitHub Actions
3. Configure SonarQube for SAST
4. Dockerize the Mario Game
5. Implement Dynamic Tagging
6. Deploy to AKS with ArgoCD
7. Validate End-to-End Pipeline Execution
Conclusion
License

**Project Introduction:** Secure DevSecOps Pipeline for Infinite Mario Game In this project, we establish a secure, automated DevSecOps pipeline to manage the development, security, and deployment lifecycle of the Infinite Mario JavaScript game. This project demonstrates the full DevSecOps workflow, from code quality checks and security scans to seamless container deployment in a Kubernetes environment. By implementing a robust CI/CD process, we enable automated detection of vulnerabilities, streamlined deployments, and secure infrastructure, all in a highly adaptable, cloud-based setup.

**This project aims to deliver:**

**Automated Code Quality and Security:** Integration with SonarQube for Static Application Security Testing (SAST) to ensure high code quality and detect potential security issues at an early stage. 

**Container Security:** Use of Trivy and other tools to scan for vulnerabilities in container images before deployment.

**Infrastructure-as-Code (IaC):** Efficient deployment and management of the Infinite Mario game within Azure Kubernetes Service (AKS), allowing rapid scaling and seamless updates.

**Continuous Deployment:** Leverage GitHub Actions workflows to automate CI/CD processes, ensuring rapid and reliable releases with every code change.

**Project Prerequisites**

To get started with this project, ensure that the following prerequisites are met:

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


# Modules

**Module 1 :DevSecOps Case Study and Prerequisites**
- [Step 1 Project requirements](./module_1_prerequisites)
- [Step 2 Creating Azure Free Trail](./module_1_prerequisites/1-azure-account.md)
- [Step 3 install Argo-Cd on Aks](./module_1_prerequisites/Step-3-install-argocd-on-aks.md)




