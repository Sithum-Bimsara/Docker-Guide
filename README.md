# **Docker-Guide**

---
## Why we want Docker?

Docker is important because it solves common issues related to software development and deployment by providing a consistent and isolated environment for applications. 

- one or more files missing.
- software version mismatch.
- different configuration settings.


## Why Docker Is Important:
#### **1. Consistency**
The same Docker container works identically on any system with Docker installed, ensuring that software runs reliably regardless of the environment.

#### **2. Isolation**
Each container runs in its isolated environment, preventing conflicts between applications or services running on the same host.

#### **3. Portability**
Applications in Docker containers can easily be moved between development, testing, and production, reducing deployment headaches.

#### **4. Efficient Resource Use**
Docker containers are lightweight and share the host OS kernel, making them more efficient than traditional virtual machines.

#### **5. Ease of Collaboration**
Teams can share the same containerized environment, ensuring that everyone works with the same setup. This eliminates environment-related discrepancies.

#### **6. Simplified Project Deletion**

**Importance**: When a project needs to be deleted, Docker makes it straightforward by encapsulating the entire application, dependencies, and configurations in containers and images.

**How**: By removing the container and its associated image (docker rm and docker rmi), all files, dependencies, and settings tied to the project are erased from the system without leaving behind residual files or affecting other projects.

**Benefit**: This prevents clutter and ensures that the system remains clean without manual hunting for files, dependencies, or configurations to delete.

---

# Containers vs Virtual Machines

## **What is a Container?**
- An isolated environment for running an application.

## **What is a Virtual Machine?**
- An abstraction of a machine (physical hardware).

### **What are Virtual Machines Used For?**

Virtual Machines (VMs) provide an isolated environment that emulates physical hardware, enabling multiple operating systems to run on a single host machine. They are commonly used for:  
1. **Application Testing**: Testing applications on different operating systems or configurations.  
2. **Legacy Software**: Running software that requires outdated or specific environments.  
3. **Server Consolidation**: Running multiple servers on one physical machine to save resources.  
4. **Development and Training**: Providing isolated, disposable environments for developers or training purposes.

### Example:
![Virtual Machine Architecture](assets/1.png)

- **Virtual Machine 1**: App 1, Node 14, Mongo 4
-  
  Virtual Machine 1 can be used to host an application that requires Node.js version 14 and MongoDB version 4. This setup ensures that the application has a dedicated environment without conflicts from other applications or dependencies.

- **Virtual Machine 2**: App 2, Node 9, Mongo 3  
  
  Virtual Machine 2 provides an isolated space for running another application with Node.js version 9 and MongoDB version 3. It is particularly useful for legacy applications or projects that require older versions of software to function correctly.

## **Hypervisors**
- Hypervisors act as the foundation for running virtual machines.

![Virtual Machine Architecture](assets/2.png)

### Common Hypervisors:
- VirtualBox
- VMware
- Hyper-V (Windows only)


## **Problems with Virtual Machines**
1. Each VM needs a full-blown OS.
2. Slow to start.
3. Resource-intensive.

## **Benefits of Containers**
1. Allow running multiple apps in isolation.
2. Lightweight.
3. Use the OS of the host.
4. Start quickly.
5. Need less hardware resources.
---
# Docker Architecture and Usage

## Overview

Docker is a platform that enables developers to build, deploy, and manage applications in lightweight containers. It leverages containerization technology to create isolated environments for running applications, ensuring consistency and efficiency across various platforms.

---

# Docker Client-Server Architecture

### Client and Server

Docker follows a **Client-Server Architecture**:

- **Client**: Sends requests to the server to perform tasks such as building, running, and managing containers. These requests are sent via REST APIs.
- **Server (Docker Engine)**: Processes client requests and handles container operations.

### REST API

**REST API (Representational State Transfer API)** is a communication method used for client-server interaction. It uses HTTP methods like `GET`, `POST`, and `DELETE` for resource management.

In Docker:

![Virtual Machine Architecture](assets/3.png)

1. **Client** sends a REST API request to the server (Docker Engine).
2. **Docker Engine** interprets the request and executes the corresponding action (e.g., creating or starting a container).

Example:

- The client sends a `docker run` command → Translates into a REST API request → Docker Engine executes the request.
 
### Kernel

The **kernel** is the core component of an operating system, managing system resources and communication between hardware and software. In the context of Docker:

- **Linux Kernel**: Docker relies on features like namespaces and cgroups in the Linux kernel to provide isolation and resource management for containers.
- **Windows Kernel**: For Windows containers, Docker utilizes Windows Server Containers or Hyper-V isolation to run containers natively on the Windows kernel.

### **It's important to note that Docker containers share the host system's kernel; they do not have their own separate kernel. This shared kernel approach allows containers to be lightweight and efficient, as they avoid the overhead associated with running separate operating system instances, unlike traditional virtual machines**

![Virtual Machine Architecture](assets/4.png)

### Containers and Processes

- Containers are lightweight, isolated environments that run applications.
- They share the **host OS kernel**, making them faster and more resource-efficient than virtual machines (VMs).
- A container can be thought of as a **process** running on the host operating system.


## Docker on Various Platforms

![Virtual Machine Architecture](assets/5.png)

### Windows

On Windows, Docker can run both Windows and Linux containers, but not simultaneously. Users can switch between the two modes:

1. **Windows Containers**: Run natively on the Windows kernel.
2. **Linux Containers**: Run within a lightweight virtual machine provided by the Windows Subsystem for Linux 2 (WSL 2).

**Windows Subsystem for Linux (WSL)** is a compatibility layer for running Linux binary executables natively on Windows. **WSL 2** introduces a full Linux kernel, improving performance and system call compatibility. Docker Desktop leverages WSL 2 to run Linux containers on Windows efficiently. :contentReference[oaicite:0]{index=0}

### Linux

On Linux systems, Docker runs natively:

- **Native Execution**: Docker utilizes the host's Linux kernel features, such as namespaces and cgroups, to create isolated containers without the need for a separate virtual machine. This results in efficient and performant container operations. :contentReference[oaicite:4]{index=4}


### macOS

On macOS, Docker utilizes a Linux virtual machine to run containers:

- **Hypervisor Framework**: Docker Desktop for Mac uses Apple's Hypervisor framework to create a lightweight virtual machine that runs a Linux kernel. This VM hosts the Docker Engine and manages containers. :contentReference[oaicite:2]{index=2}

- **File System and Network Integration**: Docker Desktop integrates with macOS to provide seamless file system sharing and network connectivity between the host and the containers. :contentReference[oaicite:3]{index=3}


---

# Step-by-Step Guide to Install Docker Desktop on Your System


## 1. Download Docker Desktop
#### Step 1: Visit the Official Website
Navigate to the Docker Desktop page at: [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/).

#### Step 2: Choose Your Platform
On the webpage:

![Docker install](assets/6.png)

1. Click the **Download Docker Desktop** button.
2. A dropdown menu will appear (as seen in the screenshot).
3. Select the appropriate version based on your system:
   - **Windows**: 
     - If you have a 64-bit processor, choose `Download for Windows - AMD64`.
     - For ARM-based processors, choose `Download for Windows - ARM64`.
   - **Mac**: Choose the version matching your chip type (`Intel Chip` or `Apple Silicon`).
   - **Linux**: Click `Download for Linux`.
4. The download will start, and you’ll receive a `.exe` file for Windows.


## 2. Install Docker Desktop

#### Step 1: Run the Installer
1. Locate the downloaded `.exe` file (e.g., `Docker Desktop Installer.exe`) in your **Downloads** folder.
2. Double-click the installer to run it.

#### Step 2: Follow the Setup Wizard
1. **Welcome Screen**: A setup wizard will open. Click **Next** to proceed.
2. **Configuration Options**:
   - Ensure that **Enable WSL 2 Features** is checked (recommended for better performance).
   - If you don't have WSL 2 installed, the installer will prompt you to install it.
3. Click **Install** to begin the installation process.
4. Wait for the installation to complete. Once done, click **Finish**.

#### Step 3: Start Docker Desktop
1. After installation, Docker Desktop should open automatically. If not, search for "Docker Desktop" in the Windows **Start Menu** and open it.
2. Log in or create a Docker account (if required).


## 3. Verify Docker Installation
After installation, it’s crucial to verify that Docker Desktop is installed and running correctly.

1. Open a **Command Prompt** or **PowerShell** window.
2. Type the following command and press Enter:

   ```bash
   docker --version
   ```
4. You should see the installed Docker version (e.g., `Docker version 27.4.0, build bde2b89`).

---

# Docker Workflow: Understanding Images, Containers, and Docker Hub

![Docker Workflow](assets/7.png)

## Dockerfile

**Definition**: A Dockerfile is a plain-text file containing instructions for building a Docker image. It defines the steps required to assemble an image, including the operating system, application code, dependencies, environment variables, and configuration.

**Key Features**:

- **Layered Builds**: Each instruction in a Dockerfile creates a new image layer, enabling efficient reuse and storage of common layers.
- **Customizability**: Developers can tailor images to specific application requirements using a Dockerfile.

**Basic Structure**:
Here’s an example Dockerfile for a Node.js application:

```dockerfile
# Use a base image
FROM node:16

# Set the working directory
WORKDIR /app

# Copy application files
COPY package*.json ./
COPY . .

# Install dependencies
RUN npm install

# Expose the application port
EXPOSE 3000

# Define the command to run the application
CMD ["npm", "start"]

```

### Workflow:

Write a Dockerfile: Developers define the application's environment and dependencies in the Dockerfile.

Build the Image: Run the docker build command to create an image from the Dockerfile.

```
docker build -t my-app .
```
Run a Container: Use the built image to create and start a container.

```
docker run -d -p 3000:3000 my-app
```

### Relationship to Image:

![Docker Workflow](assets/8.png)

A Dockerfile is the blueprint for creating a Docker image.
The docker build command processes the Dockerfile to generate a reusable and portable image.

## Docker Images

**Definition**: A Docker image is a read-only template that contains instructions for creating a Docker container. It includes the application code, libraries, dependencies, and the necessary configuration to run the application.

**Key Characteristics**:

- **Layered Structure**: Images are built in layers, with each layer representing a set of file changes or instructions. This layering allows for efficient storage and reuse of common layers across multiple images.

- **Immutability**: Once created, images do not change. Any modifications result in the creation of a new image layer, ensuring consistency and reliability.
- 
It includes everything required to run an application, such as:

- **A stripped-down operating system** (e.g., Linux-based OS).
- **Runtime environment** (e.g., Node.js for JavaScript applications).
- **Application files**.
- **Third-party libraries** and dependencies.
- **Environment variables**.


## Docker Containers

**Definition**: A Docker container is a runtime instance of a Docker image. It encapsulates the application and its environment, running in an isolated process on the host system.

**Key Characteristics**:

- **Isolation**: Containers run in isolated environments, ensuring that applications do not interfere with each other or the host system.

- **Ephemeral Nature**: Containers can be started, stopped, and deleted without affecting the underlying image. Any changes made to a running container can be committed to create a new image layer.

**Analogy**: Think of a Docker image as a blueprint (class) and a container as a building (object) constructed from that blueprint. Multiple buildings can be constructed from the same blueprint, just as multiple containers can be instantiated from the same image.



## Relationship Between Images and Containers

- **Creation**: Containers are created from images. When you run an image, Docker creates a container based on that image.

- **Independence**: An image can exist without any containers, but a container cannot exist without an image. Containers depend on images as their source.

- **Lifecycle**: While images are static and immutable, containers are dynamic and can be modified during their lifecycle. Changes made to a container can be saved by committing those changes to a new image.



## Docker Hub

![Docker Hub](assets/9.png)

**Definition**: Docker Hub is a cloud-based repository service for storing, managing, and sharing Docker images. It serves as a central platform for developers to distribute and access containerized applications.

**Key Features**:

- **Image Repository**: Hosts both public and private repositories, allowing users to store and share Docker images.

- **Automated Builds**: Supports automated builds, allowing users to automatically build Docker images from source code.

- **Webhooks**: Notifies external services of events, such as when a new image is pushed to a repository.

- **Official Images**: Provides a library of curated images for popular applications and operating systems, maintained by Docker and the community.

## Docker Workflow: Development to Production

### Development (Dev):
Developers build and test Docker images on their local machines or development servers.
Using a Dockerfile, the application, dependencies, and environment are packaged into an image.
After testing the container locally, the image is deemed ready for sharing or deployment.

### Registry:

Once an image is finalized, it is pushed to a registry, such as Docker Hub, Amazon ECR, or a private repository. The registry acts as a centralized storage for Docker images.
The registry enables collaboration and easy sharing of images between development and production environments.

### Test/Production (Prod):

From the registry, the image is pulled into different environments:
- Test Environment: The image is deployed to a test server, where QA teams validate the application.
- Production Environment: Once the image passes testing, it is deployed to production servers where it runs live.

---



