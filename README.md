

# 🚀 Let's Build End-to-End DevSecOps Pipeline for Super Mario Game               
  
![WhatsApp Image 2024-10-26 at 9 43 54 PM](https://github.com/user-attachments/assets/546890df-a20c-4676-82cd-2e0f425914fc)

## 📚 Table of Contents  

1. [Project Introduction](#project-introduction)
2. [Prerequisites](#prerequisites)
3. [Project Overview](#project-overview)
4. [Pipeline Architecture](#pipeline-architecture)
5. [Step-by-Step Implementation](#step-by-step-implementation)
6. [Clone the Repository](#clone-the-repository)
7. [Set Up GitHub Actions](#set-up-github-actions)
8. [Configure SonarQube for SAST](#configure-sonarqube-for-sast)
9. [Dockerize the Mario Game](#dockerize-the-mario-game)
10. [Implement Dynamic Tagging](#implement-dynamic-tagging)
11. [Deploy to AKS with ArgoCD](#deploy-to-aks-with-argocd)
12. [Validate End-to-End Pipeline Execution](#validate-end-to-end-pipeline-execution)
13. [Conclusion](#conclusion)

---
 
## 🎮 Project Introduction         
 
**Secure DevSecOps Pipeline for Infinite Mario Game**  
In this project, we establish a secure, automated DevSecOps pipeline to manage the development, security, and deployment lifecycle of the Infinite Mario JavaScript game. This demonstrates the full DevSecOps workflow, from code quality checks and security scans to seamless container deployment in a Kubernetes environment. We implement a robust CI/CD process, enabling automated detection of vulnerabilities, streamlined deployments, and secure infrastructure in a highly adaptable, cloud-based setup.

### 🛠️ This Project Aims to Deliver:
- **Automated Code Quality and Security:** Integration with SonarQube for Static Application Security Testing (SAST) to detect potential security issues early.
- **Container Security:** Use of Grype and other tools to scan container images for vulnerabilities.
- **Infrastructure-as-Code (IaC):** Efficient deployment within Azure Kubernetes Service (AKS).
- **Continuous Deployment:** Leveraging GitHub Actions for automated CI/CD workflows, ensuring rapid and reliable releases.

---

## 📝 Project Prerequisites

Ensure the following prerequisites are met:

- **Azure Account:** An active Azure account (free or paid). Sign up [here](https://azure.microsoft.com/en-us/free/).
- **Azure Kubernetes Service (AKS):** Knowledge of Kubernetes in Azure.
- **Docker Hub Account:** For managing container images.
- **Docker CLI:** Installed on your local machine. [Get Docker CLI here](https://www.docker.com/products/docker-desktop).
- **GitHub Account:** GitHub repository with Actions enabled.
- **SonarQube Account:** Active SonarQube instance for running SAST scans.
- **Basic Knowledge of:**
  - **DevSecOps and CI/CD Pipelines** (GitHub Actions or similar tools).
  - **AKS** (Basic Kubernetes concepts).
  - **Docker** (Creating Dockerfiles, building images).
  - **JavaScript** (Modifying the Infinite Mario game).

---

## ⚙️ Tools and Technologies Used

- **Azure Kubernetes Service (AKS)**
- **Docker and Docker Hub**
- **SonarQube for SAST Scans**
- **GitHub Actions for CI/CD**
- **Grype for Container Security**
- Components of a DevSecOps Pipeline
  

  ![image](https://github.com/user-attachments/assets/ac583368-28ea-457f-85a4-b809f9a80947)


---

## 🏗️ Pipeline Architecture

![WhatsApp Image 2024-10-26 at 9 44 21 PM](https://github.com/user-attachments/assets/76c2f2b6-4ff2-48cd-9cfc-11d7bb0e1089)

### **Pipeline Workflow**:
- **Code Commit:** Push code changes to GitHub.
- **Build & Test:** Run unit tests and static code analysis using SonarQube.
- **Containerization:** Build and push Docker images to Docker Hub.
- **Security Scanning:** Scan images with Grype.
- **Deployment:** Deploy to AKS using ArgoCD.

---

## 🗂️ Modules

### **Module 1: DevSecOps Case Study and Prerequisites**
- [Step 1: Creating Azure Free Trial](./module_1_prerequisites/1-azure-account.md) 
- [Step 2: Creating AKS Cluster](./module_1_prerequisites/step-2-creating-AKS-cluster.md)
- [Step 3: Install ArgoCD on AKS](./module_1_prerequisites/Step-3-install-argocd-on-aks.md)

### **Module 2: Integrate Static Application Security Testing (SAST) with SonarQube**
- [Step 1: Install SonarQube on Azure VM Instance](module-2/step-8-install-sonarqube-azure-vm.md)
- [Step 2: Clone Mario GitHub Repository](module-2/step-9-clone-mario-repo.md)
- [Step 3: Integrate SonarQube for SAST - Part 1](module-2/step-10-integrate-sonarqube-sast-part1.md)
- [Step 4: Integrate SonarQube for SAST - Part 2](module-2/step-11-integrate-sonarqube-sast-part2.md)
- [Step 5: Integrate SonarQube for SAST - Part 3](module-2/step-12-integrate-sonarqube-sast-part3.md)
- [Step 6: Implement Quality Gates for SAST](module-2/step-14-implement-quality-gates.md)

### **Module 3: Dockerization of Mario Game Project**
- [Step 1: Create DockerHub Account](module-3/step-1-create-dockerhub-account.md)
- [Step 2: Write a Dockerfile for Mario Game](module-3/step-2-write-dockerfile.md)
- [Step 3: Build and Push Mario Docker Image - Part 1](module-3/step-3-build-push-mario-docker-image-part1.md)
- [Step 4: Build and Push Mario Docker Image - Part 2](module-3/step-4-build-push-mario-docker-image-part2.md)
- [Step 5: Implement Dynamic Tagging for Mario Docker Image](module-3/step-5-implement-dynamic-tagging.md)

### **Module 4: Implement Container Scan for Mario Game**
- [Step 1: Implement Container Scan - Part 1](module-4/step-1-Implement-conatiner-scan.md)
- [Step 2: Implement Container Scan - Part 2](module-4/step-2-Implement-container-scan-part-2.md)

### **Module 5: Deploy Mario Docker Game on Azure Kubernetes Cluster**
- [Step 1: Deploy Mario Game with ArgoCD - Part 1](module-5/Deploy-Mario-Game-on-Azure-Kubernetes-Cluster-using-ArgoCD-Part-1.md)
- [Step 2: Deploy Mario Game with ArgoCD - Part 2](module-5/Deploy-Mario-Game-on-Azure-Kubernetes-Cluster-using-ArgoCD-Part-2.md)

### **Module 6: Implement End-to-End DevSecOps Pipeline for Mario Game**
- [Step 1: Understanding the Pipeline](module_6/step-1-understanding-end-to-end-devsecops-pipeline-for-mario-game.md)
- [Step 2: Hands-On: Part 1](module_6/step-2-hands-on-part-1-implement-end-to-end-devsecops-pipeline-for-mario-game.md)
- [Step 3: Hands-On: Part 2](module_6/step-3-hands-on-part-2-implement-end-to-end-devsecops-pipeline-for-mario-game.md)

---

## 🎯 Conclusion

In this project, we successfully built a complete DevSecOps pipeline for deploying the Infinite Mario Game. By integrating security at every stage of the CI/CD pipeline, from SAST to container security scans and seamless deployment with AKS, we demonstrated how DevSecOps practices help build secure, scalable applications. This ensures a secure and automated software development lifecycle that allows for continuous improvements and rapid delivery without compromising security.





