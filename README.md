# Docker & Kubernetes

These are my notes from the course **Docker & Kubernetes: The Practical Guide [2025 Edition]**, by Maximilian Schwarzmüller.

- [Section 1: Getting Started](#section-1)

# Section 1

- [What Is Docker](#what-is-docker)
- [Why Docker & Containers?](#why-docker--containers)
- [Virtual Machines vs Docker Containers](#virtual-machines-vs-docker-containers)
- [Docker Setup - Overview](#docker-setup---overview)
- [An Overview of the Docker Tools](#an-overview-of-the-docker-tools)

## What Is Docker?

**Docker** is a platform that allows you to **create, deploy, and run applications in containers**. Containers are lightweight, portable, and self-sufficient units that package an application along with all its dependencies (like libraries, frameworks, and runtime environments). This ensures that the application runs consistently across different environments (development, testing, production).

### **Key Points:**
1. **Container**: A running instance of a Docker image. It’s isolated from the host system and other containers.
2. **Image**: A read-only template with instructions to create a container. It includes the application code, runtime, libraries, and dependencies.
3. **Dockerfile**: A text file with instructions to build a Docker image (e.g., what base OS to use, what software to install, etc.).
4. **Docker Hub**: A cloud-based registry where you can find and share Docker images.

### **Why Use Docker?**
- **Consistency**: Works the same everywhere.
- **Isolation**: Apps run in separate containers, avoiding conflicts.
- **Portability**: Easily move containers between systems.
- **Efficiency**: Containers share the host OS kernel, making them lightweight compared to virtual machines.

### **Example:**
If you’re running a Python app, Docker ensures it works the same on your laptop, your colleague’s machine, or a cloud server.

---

## Why Docker & Containers?

### **Why Containers?**
Containers are a way to **package and isolate applications** with everything they need to run (code, libraries, dependencies, etc.). Here’s why they’re awesome:

1. **Consistency Across Environments**:
   - Containers ensure your app runs the same way on your laptop, in testing, and in production. No more "it works on my machine" problems!

2. **Isolation**:
   - Each app runs in its own container, so dependencies or libraries won’t conflict with other apps.

3. **Lightweight**:
   - Containers share the host system’s OS kernel, making them much smaller and faster than virtual machines (VMs).

4. **Portability**:
   - You can easily move containers between different systems (Linux, Windows, cloud, etc.).

5. **Scalability**:
   - Containers can be quickly started, stopped, or replicated to handle more load.

---

### **Why Docker?**
Docker is the most popular tool for working with containers. Here’s why it’s widely used:

1. **Simplifies Containerization**:
   - Docker makes it easy to create, manage, and run containers with simple commands and configuration files (like Dockerfiles).

2. **Ecosystem**:
   - Docker provides tools like **Docker Compose** (for multi-container apps) and **Docker Hub** (a registry for sharing images).

3. **Cross-Platform**:
   - Docker works on Linux, Windows, and macOS, making it versatile for developers and teams.

4. **Community Support**:
   - Docker has a huge community and tons of pre-built images available on Docker Hub, so you don’t have to start from scratch.

5. **Integration with DevOps**:
   - Docker fits perfectly into CI/CD pipelines, making it easier to automate testing and deployment.

---

### **Real-World Example:**
Imagine you’re building a web app with a frontend (React), backend (Node.js), and database (PostgreSQL). Without containers:
- You’d need to manually install and configure all these components on every machine.
- If your teammate uses a different OS, things might break.

With Docker:
- Each component (React, Node.js, PostgreSQL) runs in its own container.
- You can share a `docker-compose.yml` file, and anyone can start the entire app with one command: `docker-compose up`.

---

### **Key Takeaway:**
Docker and containers solve the problem of **"it works on my machine"** by making apps portable, consistent, and easy to deploy. They’re essential for modern DevOps and cloud-native development.

---

## Virtual Machines vs Docker Containers

**Virtual Machines (VMs)** and **Docker Containers** are both used to isolate and run applications, but they work very differently. Let’s compare them:

---

### **Virtual Machines (VMs):**
1. **What is a VM?**
   - A VM is a **full copy of an operating system** running on top of a physical machine (host). It includes the OS kernel, libraries, and applications.
   - It uses a **hypervisor** (like VMware or VirtualBox) to manage and allocate resources.

2. **Pros of VMs:**
   - **Strong Isolation**: Each VM is completely independent, with its own OS.
   - **Compatibility**: Can run any OS (Windows, Linux, etc.) on any host.
   - **Legacy Support**: Great for running older applications that need a specific OS.

3. **Cons of VMs:**
   - **Heavyweight**: Each VM includes a full OS, so they consume a lot of disk space, memory, and CPU.
   - **Slow to Start**: Booting a VM can take minutes because it has to load the entire OS.
   - **Resource-Intensive**: Running multiple VMs requires significant hardware resources.

---

### **Docker Containers:**
1. **What is a Container?**
   - A container is a **lightweight, isolated environment** that shares the host OS kernel but packages the application and its dependencies.
   - Docker is the most popular tool for creating and managing containers.

2. **Pros of Containers:**
   - **Lightweight**: Containers share the host OS kernel, so they’re much smaller and faster than VMs.
   - **Fast to Start**: Containers start in seconds because they don’t need to boot an OS.
   - **Efficient**: You can run many containers on the same hardware compared to VMs.
   - **Portable**: Containers can run on any system that supports Docker (Linux, Windows, macOS, cloud).

3. **Cons of Containers:**
   - **Less Isolation**: Containers share the host OS kernel, so they’re not as isolated as VMs.
   - **OS Dependency**: Containers must use the same OS kernel as the host (e.g., Linux containers on a Linux host).

---

### **Key Differences:**

| Feature                | Virtual Machines (VMs)               | Docker Containers                  |
|------------------------|--------------------------------------|------------------------------------|
| **Isolation**          | Full OS-level isolation              | Process-level isolation            |
| **Performance**        | Slower (needs full OS boot)          | Faster (shares host OS kernel)     |
| **Resource Usage**     | Heavy (requires full OS resources)   | Lightweight (shares host resources)|
| **Startup Time**       | Minutes                              | Seconds                            |
| **Portability**        | Less portable (OS-dependent)         | Highly portable (works anywhere)   |
| **Use Case**           | Running multiple OSes on one machine | Running multiple apps on one OS    |

---

### **When to Use VMs vs Containers:**
- **Use VMs** when:
  - You need to run applications that require different OSes (e.g., Windows apps on a Linux host).
  - You need strong isolation for security reasons (e.g., hosting untrusted code).

- **Use Containers** when:
  - You want lightweight, fast, and portable environments for modern applications.
  - You’re building microservices or cloud-native apps.
  - You need to scale quickly and efficiently.

---

### **Real-World Example:**
- **VMs**: A company running legacy Windows apps on a Linux server.
- **Containers**: A startup deploying a microservices-based web app (frontend, backend, database) using Docker and Kubernetes.

---

### **Key Takeaway:**
- **VMs** are like having multiple fully independent computers on one machine.
- **Containers** are like having multiple isolated apps sharing the same computer.

---

## Docker Setup - Overview

Here's the **guidance to install Docker, depending on your OS.**

MacOS and Windows met the requirements: Install Docker Desktop
MacOS and Windows didn't meet the requirements: Install Docker Toolbox

Installation isn't necessary for Linux.

Easy link to the video: [here](https://www.udemy.com/course/docker-kubernetes-the-practical-guide/learn/lecture/22625180#overview)

There's also a Docker Playground: [here](https://labs.play-with-docker.com/)

## An Overview of the Docker Tools

Here’s a quick **overview of Docker tools**—short and sweet! 🚀

---

### **1. Docker Engine**
- The core of Docker. It includes:
  - **Docker Daemon**: Manages containers, images, networks, and storage.
  - **Docker CLI**: Command-line tool to interact with the Docker Daemon.

---

### **2. Docker Compose**
- A tool for defining and running **multi-container applications**.
- Uses a `docker-compose.yml` file to configure services, networks, and volumes.
- Example: Start a web app with a frontend, backend, and database using one command:  
  ```bash
  docker-compose up
  ```

---

### **3. Docker Hub**
- A cloud-based **registry** for Docker images.
- Find pre-built images (e.g., `nginx`, `postgres`) or share your own.

---

### **4. Dockerfile**
- A text file with instructions to build a Docker image.
- Example:
  ```dockerfile
  FROM python:3.8
  COPY . /app
  RUN pip install -r requirements.txt
  CMD ["python", "app.py"]
  ```

---

### **5. Docker Swarm**
- Docker’s built-in **orchestration tool** for managing clusters of containers.
- Less complex than Kubernetes but good for simpler setups.

---

### **6. Docker Desktop**
- A GUI application for Mac and Windows to manage Docker containers, images, and volumes.
- Includes Kubernetes support.

---

### **7. Docker Volumes**
- Persistent storage for containers. Data survives even if the container is deleted.

---

### **8. Docker Networking**
- Tools to connect containers:
  - **Bridge Network**: Default network for containers on the same host.
  - **Overlay Network**: Connects containers across multiple hosts (e.g., in a cluster).

---

### **9. Docker Registry**
- A place to store and distribute Docker images. Can be self-hosted or use Docker Hub.

---

### **10. Docker Plugins**
- Extend Docker’s functionality (e.g., logging, monitoring, storage).

---

### **Quick Summary:**
- **Docker Engine**: Core tool.
- **Docker Compose**: Multi-container apps.
- **Docker Hub**: Image registry.
- **Dockerfile**: Build images.
- **Docker Swarm**: Orchestration.
- **Docker Desktop**: GUI for Mac/Windows.
- **Volumes/Networking**: Storage and connectivity.

---

## FOLDER FIRST-DEMO-STARTING-SETUP

Here's just **a quick example of using Docker for the first time.**

### DOCKERFILE
```Dockerfile
FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 8000

CMD [ "node", "app.mjs" ]
```

### Important commands

**docker build .**

**docker run -p [port]:[port] [imageID]**

**docker ps** - show containers

**docker stop [containerID]**