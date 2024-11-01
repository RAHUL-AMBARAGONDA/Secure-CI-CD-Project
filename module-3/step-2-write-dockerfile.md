# Docker Lab: Dockerizing the Mario Application

## Introduction

This lab will guide you through the process of  setting up a Dockerfile to build and run your application in a containerized environment.

## Prerequisites

Before you begin, ensure you have the following:
- A computer with Docker installed
- A GitHub account
- A basic understanding of Docker concepts

## Steps to Complete the Lab

### Step 1: Set Up Your Project

1. **Open Visual Studio**: Start Visual Studio and create a new project or open an existing one.
2. **Create a Dockerfile**:
   - Right-click on your project folder in the Solution Explorer and select **Add** > **New Item**.
   - Choose **Text File** and name it `Dockerfile` (without an extension).
3. **Add Dockerfile Content**: Copy and paste the following code into your `Dockerfile`:

   ```dockerfile
   # Use an official Tomcat image as a base image
   FROM tomcat:9.0.14-jre8-alpine

   LABEL maintainer="github.com/asecurityguru"

   # Copy your web application to the Tomcat webapps directory
   COPY webapp/ /usr/local/tomcat/webapps/ROOT/

   # Change the default shell to bash
   SHELL ["/bin/bash", "-c"]

   # Expose the default Tomcat port
   EXPOSE 8080

   # Start Tomcat when the container starts
   CMD ["catalina.sh", "run"]
   ```

### Step 2: Open Terminal in the Root Folder

1. Open the integrated terminal in Visual Studio by going to **View** > **Terminal**.
2. Ensure you are in the root folder of your project.

### Step 6: Stage and Commit Your Changes

1. **Stage Your Changes**: In the terminal, run the following command:

   ```bash
   git add *
   ```

2. **Commit Your Changes**: Commit the changes with a descriptive message:

   ```bash
   git commit -m "Added Dockerfile to the repo"
   ```

### Step 3: Push Your Changes to GitHub

Push your changes to your GitHub repository:

```bash
git push origin main
```

### Step 4: Verify Your Changes on GitHub

1. Go to your GitHub repository and navigate to the **Code** tab.
2. You should see your `Dockerfile` and other files in the repository.

## Conclusion

Congratulations! You have successfully created a Docker Hub account, set up a repository, created a Dockerfile, and pushed your changes to GitHub. You can now build and run your Docker container for the Mario application. Feel free to share your Docker image with others or deploy it in your projects.

## Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Docker Hub Documentation](https://docs.docker.com/docker-hub/)

If you have any questions or need further assistance, feel free to reach out!

