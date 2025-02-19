# Docker & Kubernetes

These are my notes from the course **Docker & Kubernetes: The Practical Guide [2025 Edition]**, by Maximilian Schwarzmüller.

- [Section 1: INTRODUCTION](#section-1---introduction)
- [Section 2: DOCKER IMAGES & CONTAINERS: THE CORE BUILDING BLOCKS](#section-2---docker-images--containers-the-core-building-blocks)

# Section 1 - INTRODUCTION

[Click here](#docker--kubernetes) to go to the beginning 😃

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

# Section 2 - DOCKER IMAGES & CONTAINERS: THE CORE BUILDING BLOCKS

[Click here](#docker--kubernetes) to go to the beginning 😃

- [Images & Containers: What and Why?](#images--containers-what-and-why)
- [Using & Running External (Pre-Built) Images](#using--running-external-pre-built-images)
- [Building your own Image with a Dockerfile](#building-your-own-image-with-a-dockerfile)
- [Running a Container based on your own Image](#running-a-container-based-on-your-image)
- [Images are Read-Only!](#images-are-read-only)
- [Understanding Image Layers](#understanding-image-layers)
- [Managing Images & Containers]()
- [Stopping & Restarting Containers]()
- [Understanding Attached & Detached Containers]()
- [Attaching to an already-running Container]()
- [Entering Interactive Mode]()
- [Deleting Images & Containers]()
- [Removing Stopped Containers Automatically]()
- [A look behind the scenes: Inspecting Images]()
- [Copying Files Into & From a container]()
- [Naming & Tagging Containers and Images]()
- [Sharing Images - Overview]()
- [Pushing Images to DockerHub]()
- [Pulling & Using Shared Images]()
- [Module Summary]()

## Images & Containers: What and Why

### **1. What is a Docker Image?**
- A **Docker image** is a **read-only template** that contains everything needed to run an application:
  - Application code
  - Runtime environment (e.g., Node.js, Python)
  - Libraries and dependencies
  - Configuration files
- Images are built using a **Dockerfile**, which defines the steps to create the image.
- Images are stored in a **registry** (like Docker Hub) and can be shared or reused.

---

### **2. What is a Docker Container?**
- A **container** is a **running instance of a Docker image**.
- It’s an isolated environment where the application runs, separate from the host system and other containers.
- Containers are lightweight because they share the host OS kernel.

---

### **3. Why Use Images and Containers?**
#### **Why Images?**
1. **Consistency**: Images ensure the app runs the same way everywhere (dev, test, production).
2. **Reusability**: You can reuse images for multiple containers.
3. **Versioning**: Images can be tagged (e.g., `v1.0`, `latest`) for easy updates and rollbacks.
4. **Portability**: Images can be shared via registries like Docker Hub.

#### **Why Containers?**
1. **Isolation**: Each container runs in its own environment, avoiding conflicts.
2. **Lightweight**: Containers share the host OS kernel, making them faster and more efficient than VMs.
3. **Scalability**: You can easily start, stop, or replicate containers.
4. **Portability**: Containers can run on any system with Docker installed.

---

### **4. Key Concepts:**
- **Dockerfile**: A text file with instructions to build an image.
  Example:
  ```dockerfile
  FROM python:3.8
  COPY . /app
  RUN pip install -r requirements.txt
  CMD ["python", "app.py"]
  ```
- **Layered Architecture**: Images are made up of layers. Each instruction in a Dockerfile creates a new layer, which makes images efficient and reusable.
- **Container Lifecycle**:
  - Create: `docker create`
  - Start: `docker start`
  - Stop: `docker stop`
  - Remove: `docker rm`

---

### **5. Real-World Example:**
Imagine you’re building a web app:
- **Step 1**: Create a Dockerfile to define the app’s environment (e.g., Node.js, dependencies).
- **Step 2**: Build the image:
  ```bash
  docker build -t my-web-app .
  ```
- **Step 3**: Run the container:
  ```bash
  docker run -d -p 80:3000 my-web-app
  ```
  Now your app is running in an isolated container, accessible on port 80!

---

### **Key Takeaway:**
- **Images** are the blueprints.
- **Containers** are the running instances of those blueprints.
- Together, they make apps **consistent, portable, and scalable**.

---

## Using & Running External (Pre-Built) Images

### **1. What are Pre-Built Images?**
- Pre-built images are **ready-to-use Docker images** available in public or private registries (like Docker Hub).
- Examples: `nginx`, `postgres`, `node`, `python`, etc.
- These images save you time because you don’t have to build everything from scratch.

---

### **2. How to Use Pre-Built Images**
#### **Step 1: Pull the Image**
- Use the `docker pull` command to download the image from a registry (e.g., Docker Hub).
  ```bash
  docker pull nginx
  ```
  This downloads the latest `nginx` image.

#### **Step 2: Run the Image as a Container**
- Use the `docker run` command to start a container from the image.
  ```bash
  docker run -d -p 8080:80 nginx
  ```
  - `-d`: Run in detached mode (in the background).
  - `-p 8080:80`: Map port 80 of the container to port 8080 on your host.
  - `nginx`: The image to use.

#### **Step 3: Verify the Container**
- Check if the container is running:
  ```bash
  docker ps
  ```
- Open your browser and go to `http://localhost:8080`. You should see the Nginx welcome page!

---

### **3. Common Commands for Pre-Built Images**
1. **Search for Images**:
   ```bash
   docker search nginx
   ```
   This lists all `nginx`-related images on Docker Hub.

2. **Pull a Specific Version**:
   ```bash
   docker pull nginx:1.21
   ```
   This pulls version `1.21` of the `nginx` image.

3. **Run with Environment Variables**:
   ```bash
   docker run -d -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql
   ```
   This runs a MySQL container with the root password set.

4. **Mount a Volume**:
   ```bash
   docker run -d -v /host/path:/container/path nginx
   ```
   This mounts a directory from your host into the container.

5. **Remove a Container**:
   ```bash
   docker rm <container_id>
   ```

6. **Remove an Image**:
   ```bash
   docker rmi nginx
   ```

---

### **4. Example: Running a Pre-Built PostgreSQL Image**
1. Pull the image:
   ```bash
   docker pull postgres
   ```
2. Run the container:
   ```bash
   docker run -d -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 postgres
   ```
3. Connect to the database using a PostgreSQL client (e.g., `psql`).

---

### **Key Takeaway:**
- Pre-built images save time and effort.
- Use `docker pull` to download and `docker run` to start containers.
- Customize containers with ports, volumes, and environment variables.

---

## Building Your Own Image with a Dockerfile

### **1. What is a Dockerfile?**
- A **Dockerfile** is a text file that contains instructions for building a Docker image.
- Each instruction creates a new **layer** in the image, making it efficient and reusable.

---

### **2. Basic Dockerfile Instructions**
Here are the most common instructions:

1. **`FROM`**: Specifies the base image to build upon.
   ```dockerfile
   FROM python:3.8
   ```

2. **`WORKDIR`**: Sets the working directory inside the container.
   ```dockerfile
   WORKDIR /app
   ```

3. **`COPY`**: Copies files from your host to the container.
   ```dockerfile
   COPY . /app
   ```

4. **`RUN`**: Executes commands during the build process (e.g., installing dependencies).
   ```dockerfile
   RUN pip install -r requirements.txt
   ```

5. **`CMD`**: Specifies the default command to run when the container starts.
   ```dockerfile
   CMD ["python", "app.py"]
   ```

6. **`EXPOSE`**: Documents the port the container listens on (doesn’t actually publish it).
   ```dockerfile
   EXPOSE 80
   ```

---

### **3. Example Dockerfile**
Let’s build a simple Python app:
```dockerfile
# Use the official Python image as the base
FROM python:3.8

# Set the working directory
WORKDIR /app

# Copy the requirements file and install dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copy the rest of the application code
COPY . .

# Expose port 80
EXPOSE 80

# Run the application
CMD ["python", "app.py"]
```

---

### **4. Building the Image**
1. Save the Dockerfile in your project directory.
2. Run the `docker build` command:
   ```bash
   docker build -t my-python-app .
   ```
   - `-t my-python-app`: Tags the image with a name (`my-python-app`).
   - `.`: Specifies the build context (current directory).

3. Verify the image:
   ```bash
   docker images
   ```

---

### **5. Running the Container**
1. Start a container from your custom image:
   ```bash
   docker run -d -p 4000:80 my-python-app
   ```
   - `-d`: Run in detached mode.
   - `-p 4000:80`: Map port 80 of the container to port 4000 on your host.

2. Access your app at `http://localhost:4000`.

---

### **6. Best Practices for Dockerfiles**
1. **Minimize Layers**: Combine multiple `RUN` commands into one to reduce the number of layers.
   ```dockerfile
   RUN apt-get update && apt-get install -y \
       package1 \
       package2
   ```

2. **Use `.dockerignore`**: Exclude unnecessary files (like `node_modules` or `.git`) from the build context to speed up the build.

3. **Leverage Caching**: Docker caches layers. Place instructions that change less frequently (e.g., installing dependencies) earlier in the Dockerfile.

4. **Use Multi-Stage Builds**: For complex apps, use multiple `FROM` statements to keep the final image small.

---

### **Key Takeaway:**
- A **Dockerfile** is a recipe for building custom Docker images.
- Use `docker build` to create the image and `docker run` to start the container.
- Follow best practices to optimize your Dockerfile.

---

## Running a Container based on your image

### **1. Basic Command: `docker run`**
Use the `docker run` command to start a container from your image:
```bash
docker run [OPTIONS] IMAGE_NAME [COMMAND]
```

---

### **2. Common Options for `docker run`**
- **`-d`**: Run the container in **detached mode** (background).
  ```bash
  docker run -d my-python-app
  ```
- **`-p`**: Map a **host port** to a **container port**.
  ```bash
  docker run -p 4000:80 my-python-app
  ```
- **`--name`**: Assign a custom name to the container.
  ```bash
  docker run --name my-container my-python-app
  ```
- **`-v`**: Mount a **volume** to persist data.
  ```bash
  docker run -v /host/path:/container/path my-python-app
  ```
- **`-e`**: Set **environment variables**.
  ```bash
  docker run -e ENV_VAR=value my-python-app
  ```

---

### **3. Example: Running Your Custom Image**
Suppose you built an image named `my-python-app`:
1. **Run the container in the background** and map port 4000 (host) to 80 (container):
   ```bash
   docker run -d -p 4000:80 my-python-app
   ```
2. **Access your app** at `http://localhost:4000`.

---

### **4. Common Use Cases**
#### **Run Interactively (e.g., for debugging)**
Use `-it` to start an interactive shell inside the container:
```bash
docker run -it my-python-app /bin/bash
```
- Now you can run commands inside the container (e.g., `ls`, `cat app.py`).

#### **Pass Environment Variables**
```bash
docker run -e DATABASE_URL=postgres://user:pass@host/db my-python-app
```

---

### **5. Troubleshooting Commands**
- **List running containers**:
  ```bash
  docker ps
  ```
- **View logs**:
  ```bash
  docker logs <container_id>
  ```
- **Stop a container**:
  ```bash
  docker stop <container_id>
  ```
- **Remove a container**:
  ```bash
  docker rm <container_id>
  ```

---

### **6. Best Practices**
- Use `--restart` policies to handle container crashes:
  ```bash
  docker run --restart=always my-python-app
  ```
- Clean up unused containers to save disk space:
  ```bash
  docker system prune
  ```

---

### **Real-World Example:**
Imagine you built a Node.js app image:
1. Run it with port mapping and a volume for logs:
   ```bash
   docker run -d -p 3000:3000 -v ./logs:/app/logs my-node-app
   ```
2. Your app is now live on port 3000, and logs are stored in `./logs` on your host machine.

---

### **Key Takeaway:**
- `docker run` is your go-to command to start containers from images.
- Use options like `-p`, `-v`, and `-e` to customize runtime behavior.
- Always clean up unused containers to optimize resources.

---

## Images are Read-Only

### **1. What Does "Images are Read-Only" Mean?**
- A **Docker image** is a **read-only template** used to create containers.
- Once an image is built, you **cannot modify it**. Any changes you make (e.g., adding files, installing software) happen in the **container layer**, not the image itself.

---

### **2. Why Are Images Read-Only?**
1. **Consistency**: Ensures the image remains unchanged, so it behaves the same way everywhere.
2. **Efficiency**: Multiple containers can share the same image layers, saving disk space.
3. **Immutability**: Prevents accidental changes to the base image, making deployments more reliable.

---

### **3. How Changes Work in Containers**
When you run a container:
- Docker adds a **writable layer** (called the **container layer**) on top of the read-only image.
- Any changes (e.g., creating files, modifying configurations) are stored in this writable layer.
- When the container is deleted, the writable layer is also deleted. **Changes are not saved to the image**.

---

### **4. Example: Read-Only in Action**
1. **Pull an Image**:
   ```bash
   docker pull nginx
   ```
2. **Run a Container**:
   ```bash
   docker run -d --name my-nginx nginx
   ```
3. **Make Changes in the Container**:
   - Connect to the container:
     ```bash
     docker exec -it my-nginx /bin/bash
     ```
   - Create a file:
     ```bash
     echo "Hello, Docker!" > /usr/share/nginx/html/test.txt
     ```
4. **Stop and Remove the Container**:
   ```bash
   docker stop my-nginx
   docker rm my-nginx
   ```
5. **Run a New Container**:
   ```bash
   docker run -d --name new-nginx nginx
   ```
   - The `test.txt` file is **gone** because the image is read-only, and the writable layer was deleted.

---

### **5. How to Persist Changes**
If you want to save changes:
1. **Commit the Container to a New Image**:
   ```bash
   docker commit my-nginx my-custom-nginx
   ```
   This creates a new image with the changes from the container.

2. **Use Volumes**:
   Mount a host directory to persist data:
   ```bash
   docker run -d -v /host/path:/container/path nginx
   ```

3. **Use Dockerfile**:
   Make changes during the image build process:
   ```dockerfile
   FROM nginx
   RUN echo "Hello, Docker!" > /usr/share/nginx/html/test.txt
   ```

---

### **6. Key Takeaway:**
- **Images are read-only**: They cannot be modified after creation.
- **Containers add a writable layer**: Changes are stored here but are lost when the container is deleted.
- To save changes, **commit the container** or use **volumes** or **Dockerfile**.

---

## Understanding Image Layers

### **1. What Are Image Layers?**
- Docker images are built using **layers**. Each instruction in a `Dockerfile` creates a new layer.
- Layers are **read-only**, and they’re stacked on top of each other to form the final image.
- Layers are cached, making subsequent builds faster and more efficient.

---

### **2. How Layers Work**
- **Example Dockerfile**:
  ```dockerfile
  FROM python:3.8               # Layer 1: Base OS + Python
  WORKDIR /app                  # Layer 2: Create /app directory
  COPY requirements.txt .       # Layer 3: Copy requirements.txt
  RUN pip install -r requirements.txt  # Layer 4: Install dependencies
  COPY . .                      # Layer 5: Copy app code
  CMD ["python", "app.py"]      # Layer 6: Set default command
  ```
- Each line in the Dockerfile creates a new layer. If you rebuild the image, Docker reuses cached layers unless something changes.

---

### **3. Benefits of Layering**
1. **Caching**:
   - If a layer hasn’t changed (e.g., `COPY requirements.txt`), Docker reuses the cached layer, speeding up builds.
2. **Reusability**:
   - Layers can be shared between images (e.g., the `python:3.8` base layer).
3. **Smaller Image Sizes**:
   - Only changed layers are rebuilt, reducing redundancy.

---

### **4. Visualizing Layers**
Use `docker history` to see the layers of an image:
```bash
docker history my-python-app
```
Output:
```
IMAGE          CREATED         CREATED BY                                      SIZE
abc123        2 hours ago     CMD ["python" "app.py"]                         0B
def456        2 hours ago     COPY . .                                        2.5MB
ghi789        2 hours ago     RUN pip install -r requirements.txt             150MB
jkl012        2 hours ago     COPY requirements.txt .                         5kB
mno345        2 weeks ago     WORKDIR /app                                     0B
pqr678        3 weeks ago     /bin/sh -c #(nop)  CMD ["python3"]              0B
...            ...            ...                                             ...
```

---

### **5. Layer Best Practices**
1. **Order Matters**:
   - Place **frequently changing instructions** (e.g., `COPY . .`) **last** to maximize caching.
   ```dockerfile
   # Bad: Code changes will invalidate all layers below!
   COPY . .
   RUN pip install -r requirements.txt

   # Good: Install dependencies first
   COPY requirements.txt .
   RUN pip install -r requirements.txt
   COPY . .
   ```
2. **Minimize Layers**:
   - Combine multiple `RUN` commands into one to reduce layers:
     ```dockerfile
     RUN apt-get update && \
         apt-get install -y git curl
     ```
3. **Use `.dockerignore`**:
   - Exclude unnecessary files (e.g., `node_modules`, `.git`) to avoid bloating layers.

---

### **6. Key Takeaway:**
- **Layers are immutable and cached**: Changes to a layer invalidate all layers below it.
- **Optimize layer order**: Put stable instructions (e.g., installing dependencies) first and volatile instructions (e.g., copying code) last.
- **Use tools like `docker history`** to analyze layers and debug builds.

---

### **Real-World Example:**
Imagine you’re building a Node.js app:
- **Layer 1**: Base image (`FROM node:14`).
- **Layer 2**: Copy `package.json` and `package-lock.json`.
- **Layer 3**: Run `npm install`.
- **Layer 4**: Copy the rest of the app code (`COPY . .`).

If you change your app code (Layer 4), Docker will reuse Layers 1-3 from the cache, saving time!

---

## Managing Images & Containers

### **1. Managing Docker Images**
#### **List Images**
To see all images on your system:
```bash
docker images
```
Output:
```
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
my-python-app latest    abc123        2 hours ago    150MB
nginx         latest    def456        3 days ago     133MB
```

#### **Remove an Image**
To delete an image:
```bash
docker rmi <image_id_or_name>
```
Example:
```bash
docker rmi my-python-app
```

#### **Remove All Unused Images**
To clean up unused images:
```bash
docker image prune -a
```

#### **Pull an Image**
Download an image from a registry (e.g., Docker Hub):
```bash
docker pull nginx
```

#### **Tag an Image**
Tag an image for versioning or pushing to a registry:
```bash
docker tag my-python-app my-python-app:v1
```

#### **Push an Image**
Upload an image to a registry (e.g., Docker Hub):
```bash
docker push my-python-app:v1
```

---

### **2. Managing Docker Containers**
#### **List Containers**
To see running containers:
```bash
docker ps
```
To see all containers (running and stopped):
```bash
docker ps -a
```

#### **Start a Container**
Start a stopped container:
```bash
docker start <container_id_or_name>
```

#### **Stop a Container**
Stop a running container:
```bash
docker stop <container_id_or_name>
```

#### **Remove a Container**
Delete a stopped container:
```bash
docker rm <container_id_or_name>
```
To force-remove a running container:
```bash
docker rm -f <container_id_or_name>
```

#### **Remove All Stopped Containers**
Clean up stopped containers:
```bash
docker container prune
```

#### **View Container Logs**
Check the logs of a container:
```bash
docker logs <container_id_or_name>
```

#### **Run a One-Off Command**
Execute a command in a running container:
```bash
docker exec -it <container_id_or_name> <command>
```
Example:
```bash
docker exec -it my-nginx /bin/bash
```

---

### **3. Advanced Management**
#### **Inspect Containers or Images**
Get detailed information about a container or image:
```bash
docker inspect <container_id_or_name>
docker inspect <image_id_or_name>
```

#### **Resource Usage**
Check CPU, memory, and network usage of containers:
```bash
docker stats
```

#### **Copy Files Between Host and Container**
Copy files to/from a container:
```bash
docker cp <host_path> <container_id_or_name>:<container_path>
docker cp <container_id_or_name>:<container_path> <host_path>
```
Example:
```bash
docker cp my-nginx:/etc/nginx/nginx.conf ./nginx.conf
```

---

### **4. Best Practices**
1. **Clean Up Regularly**:
   - Use `docker system prune` to remove unused images, containers, networks, and volumes.
2. **Use Meaningful Names**:
   - Name your containers for easier management:
     ```bash
     docker run --name my-web-app -d nginx
     ```
3. **Monitor Resource Usage**:
   - Use `docker stats` to keep an eye on container performance.

---

### **Real-World Example:**
Imagine you’re running a web app:
1. **List running containers**:
   ```bash
   docker ps
   ```
2. **Check logs** for errors:
   ```bash
   docker logs my-web-app
   ```
3. **Clean up** unused containers and images:
   ```bash
   docker container prune
   docker image prune -a
   ```

---

### **Key Takeaway:**
- Use `docker images` and `docker ps` to list images and containers.
- Clean up regularly with `docker system prune`.
- Use `docker exec` to interact with running containers.

---

