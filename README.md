# Docker & Kubernetes

These are my notes from the course **Docker & Kubernetes: The Practical Guide [2025 Edition]**, by Maximilian Schwarzmüller.

- [Section 1: INTRODUCTION](#section-1---introduction)
- [Section 2: DOCKER IMAGES & CONTAINERS: THE CORE BUILDING BLOCKS](#section-2---docker-images--containers-the-core-building-blocks)
- [Section 3: MANAGING DATA & WORKING WITH VOLUMES](#section-3---managing-data--working-with-volumes)
- [Section 4: NETWORKING: (CROSS-)CONTAINER COMMUNICATION](#section-4---networking-cross-container-communication)
- [Section 5: BUILDING MULTI-CONTAINER APPLICATIONS WITH DOCKER](#section-5---building-multi-container-applications-with-docker)

# [Section 1 - INTRODUCTION](#docker--kubernetes)

- [What Is Docker](#what-is-docker)
- [Why Docker & Containers?](#why-docker--containers)
- [Virtual Machines vs Docker Containers](#virtual-machines-vs-docker-containers)
- [Docker Setup - Overview](#docker-setup---overview)
- [An Overview of the Docker Tools](#an-overview-of-the-docker-tools)

## [What Is Docker?](#section-1---introduction)

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

## [Why Docker & Containers?](#section-1---introduction)

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

## [Virtual Machines vs Docker Containers](#section-1---introduction)

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

## [Docker Setup - Overview](#section-1---introduction)

Here's the **guidance to install Docker, depending on your OS.**

MacOS and Windows met the requirements: Install Docker Desktop
MacOS and Windows didn't meet the requirements: Install Docker Toolbox

Installation isn't necessary for Linux.

Easy link to the video: [here](https://www.udemy.com/course/docker-kubernetes-the-practical-guide/learn/lecture/22625180#overview)

There's also a Docker Playground: [here](https://labs.play-with-docker.com/)

## [An Overview of the Docker Tools](#section-1---introduction)

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

# [Section 2 - DOCKER IMAGES & CONTAINERS: THE CORE BUILDING BLOCKS](#docker--kubernetes)

- [Images & Containers: What and Why?](#images--containers-what-and-why)
- [Using & Running External (Pre-Built) Images](#using--running-external-pre-built-images)
- [Building your own Image with a Dockerfile](#building-your-own-image-with-a-dockerfile)
- [Running a Container based on your own Image](#running-a-container-based-on-your-image)
- [Images are Read-Only!](#images-are-read-only)
- [Understanding Image Layers](#understanding-image-layers)
- [Managing Images & Containers](#managing-images--containers)
- [Stopping & Restarting Containers](#stopping--restarting-containers)
- [Understanding Attached & Detached Containers](#understanding-attached--detached-containers)
- [Attaching to an already-running Container](#option-2-attach-to-a-running-container)
- [Entering Interactive Mode](#entering-interactive-mode)
- [Deleting Images & Containers](#deleting-images--containers)
- [Removing Stopped Containers Automatically](#removing-stopped-containers-automatically)
- [A look behind the scenes: Inspecting Images](#a-look-behind-the-scenes-inspecting-images)
- [Copying Files Into & From a container](#copying-files-into--from-a-container)
- [Naming & Tagging Containers and Images](#naming--tagging-containers-and-images)
- [Sharing Images - Overview](#sharing-images---overview)
- [Pushing Images to DockerHub](#pushing-images-to-dockerhub)
- [Pulling & Using Shared Images](#pulling--using-shared-images)

## [Images & Containers: What and Why](#section-2---docker-images--containers-the-core-building-blocks)

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

## [Using & Running External (Pre-Built) Images](#section-2---docker-images--containers-the-core-building-blocks)

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

## [Building Your Own Image with a Dockerfile](#section-2---docker-images--containers-the-core-building-blocks)

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

## [Running a Container based on your image](#section-2---docker-images--containers-the-core-building-blocks)

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

## [Images are Read-Only](#section-2---docker-images--containers-the-core-building-blocks)

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

## [Understanding Image Layers](#section-2---docker-images--containers-the-core-building-blocks)

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

## [Managing Images & Containers](#section-2---docker-images--containers-the-core-building-blocks)

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

## [Stopping & Restarting Containers](#section-2---docker-images--containers-the-core-building-blocks)

### **1. Stopping Containers**
When you stop a container, it gracefully shuts down the processes inside it. Here’s how to do it:

#### **Command: `docker stop`**
```bash
docker stop <container_id_or_name>
```
- **Example**:
  ```bash
  docker stop my-nginx
  ```
- **What Happens**:
  - Docker sends a `SIGTERM` signal to the main process inside the container, allowing it to shut down gracefully.
  - If the process doesn’t stop within 10 seconds, Docker sends a `SIGKILL` to force it to stop.

#### **Force-Stop a Container**
If a container is unresponsive, you can force-stop it:
```bash
docker kill <container_id_or_name>
```
- This sends a `SIGKILL` immediately, bypassing the graceful shutdown.

---

### **2. Restarting Containers**
Restarting a container stops and starts it again. This is useful for applying changes or recovering from issues.

#### **Command: `docker restart`**
```bash
docker restart <container_id_or_name>
```
- **Example**:
  ```bash
  docker restart my-nginx
  ```
- **What Happens**:
  - The container is stopped (gracefully) and then started again.
  - Any changes made to the container’s writable layer (e.g., files created, configurations modified) are preserved.

---

### **3. Starting Stopped Containers**
If a container is stopped, you can start it again without recreating it.

#### **Command: `docker start`**
```bash
docker start <container_id_or_name>
```
- **Example**:
  ```bash
  docker start my-nginx
  ```
- **Options**:
  - `-a` (attach): Attach to the container’s output (like `docker run`).
  - `-i` (interactive): Attach to the container interactively.

---

### **4. Common Use Cases**
#### **Graceful Shutdown**
- Use `docker stop` to ensure your app shuts down properly (e.g., saving data, closing connections).

#### **Force-Stop Unresponsive Containers**
- Use `docker kill` if a container is frozen or unresponsive.

#### **Apply Configuration Changes**
- Restart a container to apply changes (e.g., updated environment variables or mounted files).

#### **Recover from Crashes**
- Use `docker start` to bring back a stopped container without losing its state.

---

### **5. Example Workflow**
1. **Stop a Running Container**:
   ```bash
   docker stop my-web-app
   ```
2. **Start the Container Again**:
   ```bash
   docker start my-web-app
   ```
3. **Restart the Container** (stop + start in one command):
   ```bash
   docker restart my-web-app
   ```

---

### **6. Best Practices**
1. **Use `docker stop` for Graceful Shutdowns**:
   - Always prefer `docker stop` over `docker kill` unless the container is unresponsive.
2. **Monitor Container Logs**:
   - Check logs after restarting to ensure everything is working:
     ```bash
     docker logs my-web-app
     ```
3. **Automate Restarts**:
   - Use `--restart` policies to automatically restart containers on failure:
     ```bash
     docker run -d --restart=always my-web-app
     ```

---

### **Key Takeaway:**
- **`docker stop`**: Gracefully stops a container.
- **`docker kill`**: Force-stops a container.
- **`docker restart`**: Stops and starts a container in one command.
- **`docker start`**: Starts a stopped container.

---

## [Understanding Attached & Detached Containers](#section-2---docker-images--containers-the-core-building-blocks)

### **1. Attached Containers (Foreground Mode)**
- **What**: When you run a container in **attached mode**, it stays connected to your terminal, and you see its logs/output in real time.
- **Command**:
  ```bash
  docker run [image_name]
  ```
  - Example:
    ```bash
    docker run nginx
    ```
- **Behavior**:
  - The container runs in the foreground.
  - You see all logs/output directly in your terminal.
  - Pressing `Ctrl+C` stops the container.
- **Use Case**:
  - Debugging or testing short-lived processes (e.g., running a script and seeing immediate output).

---

### **2. Detached Containers (Background Mode)**
- **What**: When you run a container in **detached mode**, it runs in the background, freeing up your terminal.
- **Command**:
  ```bash
  docker run -d [image_name]
  ```
  - Example:
    ```bash
    docker run -d nginx
    ```
- **Behavior**:
  - The container starts and runs in the background.
  - You get the container ID but don’t see logs/output unless you explicitly check them.
- **Use Case**:
  - Running long-lived services (e.g., web servers, databases).

---

### **3. Switching Between Attached and Detached**
#### **Detach from an Attached Container**
If you started a container in attached mode and want to detach:
- Press `Ctrl+P` followed by `Ctrl+Q`.
- The container keeps running in the background.

#### **Reattach to a Detached Container**
To reconnect to a running container’s output:
```bash
docker attach <container_id_or_name>
```
- Example:
  ```bash
  docker attach my-nginx
  ```
- **Warning**: Pressing `Ctrl+C` here will **stop the container** (not just detach). To detach again, use `Ctrl+P` + `Ctrl+Q`.

---

### **4. Running Interactive Containers**
For containers that need input (e.g., a shell):
- Use `-it` (interactive + TTY) to attach and interact:
  ```bash
  docker run -it ubuntu /bin/bash
  ```
- This lets you type commands into the container’s shell.

---

### **5. Key Differences**

| Feature               | Attached (Foreground)          | Detached (Background)          |
|-----------------------|--------------------------------|--------------------------------|
| **Terminal Output**   | Logs visible in real time      | No output unless checked       |
| **Terminal Control**  | `Ctrl+C` stops the container   | Terminal freed for other tasks |
| **Use Case**          | Debugging, short-lived tasks   | Long-running services          |

---

### **6. Real-World Example**
1. **Run a Detached Web Server**:
   ```bash
   docker run -d -p 8080:80 --name my-web nginx
   ```
2. **Check Logs**:
   ```bash
   docker logs my-web
   ```
3. **Reattach to the Container** (if needed):
   ```bash
   docker attach my-web
   ```
4. **Detach Again**:
   Press `Ctrl+P` + `Ctrl+Q`.

---

### **7. Best Practices**
- Use **detached mode** for production services (e.g., databases, APIs).
- Use **attached mode** for debugging or interactive tasks (e.g., shell access).
- Always name your containers (`--name`) for easier management.

---

### **Key Takeaway**:
- **Attached** = Foreground (logs visible, terminal blocked).
- **Detached** = Background (terminal free, use `docker logs` to check output).
- Use `-it` for interactive shells and `Ctrl+P` + `Ctrl+Q` to detach safely.

---

## [Entering Interactive Mode](#section-2---docker-images--containers-the-core-building-blocks)

### **1. What is Interactive Mode?**
- Interactive mode allows you to **connect to a running container** and interact with it as if you were inside the container itself.
- It’s commonly used for:
  - Running commands in a shell (e.g., `bash`, `sh`).
  - Debugging or inspecting the container’s filesystem.

---

### **2. How to Enter Interactive Mode**
Use the `-it` flags with `docker run` or `docker exec`:
- `-i`: Keeps the input stream open (interactive).
- `-t`: Allocates a pseudo-TTY (terminal).

#### **Option 1: Start a New Container in Interactive Mode**
```bash
docker run -it [image_name] [command]
```
- Example:
  ```bash
  docker run -it ubuntu /bin/bash
  ```
  - This starts a new Ubuntu container and drops you into a `bash` shell.

#### **Option 2: Attach to a Running Container**
```bash
docker exec -it <container_id_or_name> [command]
```
- Example:
  ```bash
  docker exec -it my-nginx /bin/bash
  ```
  - This connects to the `my-nginx` container and starts a `bash` shell.

---

### **3. Common Use Cases**
#### **Run a Shell in a Container**
- Start a new container with a shell:
  ```bash
  docker run -it python:3.8 /bin/bash
  ```
- Attach to a running container with a shell:
  ```bash
  docker exec -it my-python-app /bin/sh
  ```

#### **Debugging**
- Inspect files or logs inside a container:
  ```bash
  docker exec -it my-nginx ls /etc/nginx
  ```

#### **Install Software**
- Install tools or dependencies inside a running container:
  ```bash
  docker exec -it my-ubuntu apt-get update
  ```

---

### **4. Exiting Interactive Mode**
- To **exit the shell** but **keep the container running**, type:
  ```bash
  exit
  ```
  or press `Ctrl+D`.

- To **detach from the container** without stopping it, press:
  ```bash
  Ctrl+P` followed by `Ctrl+Q
  ```

---

### **5. Example Workflow**
1. **Start a New Container in Interactive Mode**:
   ```bash
   docker run -it --name my-ubuntu ubuntu /bin/bash
   ```
   - You’re now inside the container’s shell.

2. **Run Commands**:
   ```bash
   apt-get update
   apt-get install -y curl
   curl --version
   ```

3. **Exit the Shell**:
   ```bash
   exit
   ```

4. **Reattach to the Container**:
   ```bash
   docker exec -it my-ubuntu /bin/bash
   ```

---

### **6. Best Practices**
- Use **`docker exec`** to interact with running containers instead of starting new ones.
- Always **name your containers** (`--name`) for easier access.
- Use **`.dockerignore`** to avoid copying unnecessary files into the container.

---

### **Key Takeaway:**
- Use `-it` to enter interactive mode with a container.
- Use `docker run -it` for new containers and `docker exec -it` for running containers.
- Exit with `exit` or detach with `Ctrl+P` + `Ctrl+Q`.

---

## [Deleting Images & Containers](#section-2---docker-images--containers-the-core-building-blocks)

### **1. Deleting Containers**
#### **Remove a Single Container**
```bash
docker rm <container_id_or_name>
```
- Example:
  ```bash
  docker rm my-nginx
  ```

#### **Force-Remove a Running Container**
If the container is running, use the `-f` flag:
```bash
docker rm -f <container_id_or_name>
```

#### **Remove All Stopped Containers**
Clean up all stopped containers:
```bash
docker container prune
```
- Confirm with `y` when prompted.

---

### **2. Deleting Images**
#### **Remove a Single Image**
```bash
docker rmi <image_id_or_name>
```
- Example:
  ```bash
  docker rmi my-python-app
  ```

#### **Remove All Unused Images**
Clean up images not associated with a container:
```bash
docker image prune -a
```
- Confirm with `y` when prompted.

---

### **3. Advanced Cleanup**
#### **Remove Everything**
To remove all containers, images, networks, and volumes:
```bash
docker system prune -a
```
- **Warning**: This is a **nuclear option**—it removes everything not actively in use.

#### **Remove Volumes**
To remove unused volumes:
```bash
docker volume prune
```

---

### **4. Example Workflow**
1. **List Containers**:
   ```bash
   docker ps -a
   ```
2. **Remove a Stopped Container**:
   ```bash
   docker rm my-nginx
   ```
3. **List Images**:
   ```bash
   docker images
   ```
4. **Remove an Unused Image**:
   ```bash
   docker rmi my-python-app
   ```
5. **Clean Up Everything**:
   ```bash
   docker system prune -a
   ```

---

### **5. Best Practices**
- **Regular Cleanup**: Use `docker system prune` periodically to free up disk space.
- **Avoid `-f` Unless Necessary**: Force-removing containers can lead to data loss.
- **Use `.dockerignore`**: Prevent unnecessary files from bloating your images.

---

### **Key Takeaway:**
- Use `docker rm` to delete containers and `docker rmi` to delete images.
- Use `docker system prune` for a full cleanup.
- Always double-check before running `docker system prune -a`!

---

## [Removing Stopped Containers Automatically](#section-2---docker-images--containers-the-core-building-blocks)

### **1. Why Automate Removal?**
- Avoids clutter from stopped containers.
- Saves disk space.
- Reduces manual cleanup.

---

### **2. Methods to Auto-Remove Stopped Containers**

#### **Method 1: Use `--rm` Flag When Running Containers**
- Add the `--rm` flag to automatically remove the container **when it exits**.
  ```bash
  docker run --rm -d -p 8080:80 nginx
  ```
  - The container will be deleted once it stops.

#### **Method 2: Auto-Remove All Stopped Containers**
Use `docker container prune` to remove **all stopped containers**:
```bash
docker container prune
```
- Confirm with `y` when prompted.

#### **Method 3: Use a `docker run` Policy**
For **long-running containers**, use `--restart` with `--rm`:
```bash
docker run --rm --restart=unless-stopped -d my-app
```
- The container restarts if it crashes but is removed if explicitly stopped.

---

### **3. Automate with Cron Jobs (Linux/macOS)**
Schedule `docker container prune` to run periodically (e.g., daily).

1. Open your crontab:
   ```bash
   crontab -e
   ```
2. Add a line to run the cleanup daily at midnight:
   ```bash
   0 0 * * * docker container prune -f
   ```
   - `-f` skips the confirmation prompt.

---

### **4. Use Docker Compose Auto-Remove**
In a `docker-compose.yml`, set `auto_remove` for specific services:
```yaml
services:
  web:
    image: nginx
    restart: unless-stopped
    auto_remove: true
```

---

### **5. Example Workflow**
1. **Run a Temporary Container**:
   ```bash
   docker run --rm -it ubuntu /bin/bash
   ```
   - When you `exit`, the container is automatically deleted.

2. **Clean Up All Stopped Containers**:
   ```bash
   docker container prune -f
   ```

---

### **6. Best Practices**
- Use `--rm` for **short-lived containers** (e.g., running tests or scripts).
- Avoid `--rm` for **persistent services** (e.g., databases) where you need logs or data.
- Combine with **volumes** to persist data even if containers are removed.

---

### **Key Takeaway:**
- `--rm` removes the container automatically when it stops.
- `docker container prune` cleans up all stopped containers.
- Automate cleanup with cron jobs or Docker Compose policies.

---

## [A look behind the scenes: Inspecting Images](#section-2---docker-images--containers-the-core-building-blocks)

### **1. Why Inspect Images?**
- Understand the **layers** and **history** of an image.
- Debug issues (e.g., missing files, incorrect configurations).
- Verify the **size** and **contents** of an image.

---

### **2. Inspecting Images with `docker inspect`**
The `docker inspect` command provides detailed metadata about an image.

#### **Command**:
```bash
docker inspect <image_id_or_name>
```
- Example:
  ```bash
  docker inspect nginx
  ```

#### **Output**:
- A JSON object with details like:
  - **Layers**: Filesystem layers.
  - **Config**: Environment variables, working directory, entrypoint, etc.
  - **Size**: Total size of the image.
  - **Created**: Timestamp of when the image was built.

#### **Filter Specific Fields**:
Use `--format` to extract specific information:
```bash
docker inspect --format='{{.Config.WorkingDir}}' nginx
```
- This returns the working directory of the `nginx` image.

---

### **3. Inspecting Layers with `docker history`**
The `docker history` command shows the **layers** of an image and how they were built.

#### **Command**:
```bash
docker history <image_id_or_name>
```
- Example:
  ```bash
  docker history nginx
  ```

#### **Output**:
- A table showing:
  - **Layer ID**: Unique identifier for each layer.
  - **Created**: When the layer was created.
  - **Created By**: The Dockerfile instruction that created the layer.
  - **Size**: Size of the layer.

#### **Example Output**:
```
IMAGE          CREATED         CREATED BY                                      SIZE
abc123        2 hours ago     CMD ["nginx", "-g", "daemon off;"]              0B
def456        2 hours ago     COPY file:1234abcd /etc/nginx/conf.d/default.conf 1.5kB
ghi789        2 weeks ago     /bin/sh -c #(nop)  EXPOSE 80                    0B
...            ...            ...                                             ...
```

---

### **4. Inspecting Layers with `docker image inspect`**
This is similar to `docker inspect` but focuses on image-specific details.

#### **Command**:
```bash
docker image inspect <image_id_or_name>
```

---

### **5. Inspecting Image Filesystem**
To explore the filesystem of an image, you can:
1. **Run the Image Interactively**:
   ```bash
   docker run -it <image_id_or_name> /bin/sh
   ```
   - Navigate the filesystem manually.

2. **Export the Image Filesystem**:
   ```bash
   docker save <image_id_or_name> -o image.tar
   ```
   - Extract the `.tar` file to inspect its contents:
     ```bash
     tar -xvf image.tar
     ```

---

### **6. Real-World Example**
1. **Inspect the `nginx` Image**:
   ```bash
   docker inspect nginx
   ```
   - Check the `Config` section for environment variables and commands.

2. **View Layer History**:
   ```bash
   docker history nginx
   ```
   - Identify which layers contribute the most to the image size.

3. **Explore the Filesystem**:
   ```bash
   docker run -it nginx /bin/sh
   ```
   - Navigate to `/etc/nginx` to see the configuration files.

---

### **7. Best Practices**
- **Minimize Layers**: Combine multiple `RUN` commands in your Dockerfile to reduce the number of layers.
- **Use `.dockerignore`**: Exclude unnecessary files to keep the image small.
- **Regularly Inspect Images**: Understand what’s inside your images to optimize and debug them.

---

### **Key Takeaway:**
- Use `docker inspect` for detailed metadata.
- Use `docker history` to see how an image was built layer by layer.
- Explore the filesystem interactively or by exporting the image.

---

## [Copying Files into & from a container](#section-2---docker-images--containers-the-core-building-blocks)

### 1. **Copying Files into & from a Container**

When working with Docker containers, you often need to copy files between your host machine and the container. Docker provides two main commands for this: `docker cp` and using Docker volumes.

#### **Copying Files into a Container**

To copy a file or directory from your host machine into a running container, you use the `docker cp` command. The syntax is:

```bash
docker cp <source_path> <container_id>:<destination_path>
```

- `<source_path>`: The path to the file or directory on your host machine.
- `<container_id>`: The ID or name of the container.
- `<destination_path>`: The path inside the container where you want to copy the file or directory.

**Example:**

```bash
docker cp /home/user/myfile.txt mycontainer:/app/myfile.txt
```

This command copies `myfile.txt` from your host machine to the `/app` directory inside the container named `mycontainer`.

#### **Copying Files from a Container**

Similarly, you can copy files from a container to your host machine using the same `docker cp` command, but with the source and destination paths reversed:

```bash
docker cp <container_id>:<source_path> <destination_path>
```

**Example:**

```bash
docker cp mycontainer:/app/myfile.txt /home/user/myfile.txt
```

This command copies `myfile.txt` from the `/app` directory inside the container to your host machine.

#### **Using Docker Volumes**

While `docker cp` is useful for one-off file transfers, Docker volumes are a more robust solution for persistent data storage and sharing files between the host and container. Volumes are managed by Docker and can be mounted to specific paths in the container.

**Example:**

```bash
docker run -v /home/user/data:/app/data myimage
```

This command mounts the `/home/user/data` directory on your host machine to `/app/data` inside the container.

## [Naming & Tagging Containers and Images](#section-2---docker-images--containers-the-core-building-blocks)

### 2. **Naming & Tagging Containers and Images**

#### **Naming Containers**

When you run a container, Docker assigns it a random name by default. However, you can give your container a custom name using the `--name` option.

**Example:**

```bash
docker run --name mycontainer myimage
```

This command runs a container from the `myimage` image and names it `mycontainer`.

#### **Tagging Images**

Docker images can have tags, which are essentially versions or labels for the image. Tags help you manage different versions of an image. When you build or pull an image, you can specify a tag.

**Example:**

```bash
docker build -t myimage:1.0 .
```

This command builds an image from the Dockerfile in the current directory and tags it as `myimage:1.0`.

If you don't specify a tag, Docker uses `latest` by default.

**Pulling a Tagged Image:**

```bash
docker pull myimage:1.0
```

This command pulls the `myimage` image with the `1.0` tag.

#### **Tagging an Existing Image**

You can also tag an existing image with a new tag using the `docker tag` command.

**Example:**

```bash
docker tag myimage:1.0 myimage:latest
```

This command tags the `myimage:1.0` image as `myimage:latest`.

#### **Renaming a Container**

If you want to rename an existing container, you can use the `docker rename` command.

**Example:**

```bash
docker rename old_container_name new_container_name
```

This command renames the container from `old_container_name` to `new_container_name`.

## [Sharing Images - Overview](#section-2---docker-images--containers-the-core-building-blocks)

1. **What is an Image?**
   - A Docker image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, and dependencies.
   - Images are built from a `Dockerfile`, which defines the steps to create the image.

2. **Why Share Images?**
   - **Collaboration**: Share images with team members or the community.
   - **Consistency**: Ensure everyone uses the same environment.
   - **Deployment**: Simplify deployment by using pre-built images.
   - **Reusability**: Avoid rebuilding images from scratch.

3. **Image Repositories**
   - Docker images are stored in **registries** (e.g., Docker Hub, AWS ECR, Google Container Registry).
   - **Docker Hub** is the default public registry for sharing Docker images.

4. **Image Tags**
   - Tags are used to version images (e.g., `myimage:1.0`, `myimage:latest`).
   - The `latest` tag is applied by default if no tag is specified.

---

## [Pushing Images to DockerHub](#section-2---docker-images--containers-the-core-building-blocks)

1. **Prerequisites**
   - A Docker Hub account ([hub.docker.com](https://hub.docker.com)).
   - Docker installed on your machine.
   - An image built locally (e.g., `myimage:1.0`).

2. **Steps to Push an Image**
   - **Step 1: Log in to Docker Hub**
     ```bash
     docker login
     ```
     Enter your Docker Hub username and password when prompted.

   - **Step 2: Tag the Image**
     - Docker Hub requires images to be tagged with your Docker Hub username.
     - Format: `docker tag <local-image> <dockerhub-username>/<repository-name>:<tag>`
     - Example:
       ```bash
       docker tag myimage:1.0 mydockerhubusername/myimage:1.0
       ```

   - **Step 3: Push the Image**
     - Use the `docker push` command to upload the image to Docker Hub.
     - Example:
       ```bash
       docker push mydockerhubusername/myimage:1.0
       ```

3. **Verifying the Push**
   - Visit your Docker Hub account and check the repository to ensure the image has been uploaded.

---

## [Pulling & Using Shared Images](#section-2---docker-images--containers-the-core-building-blocks)

1. **Pulling an Image**
   - Use the `docker pull` command to download an image from a registry.
   - Example:
     ```bash
     docker pull mydockerhubusername/myimage:1.0
     ```
   - If no tag is specified, Docker will pull the `latest` tag by default.

2. **Running a Container from a Pulled Image**
   - Use the `docker run` command to create and start a container from the pulled image.
   - Example:
     ```bash
     docker run -d --name mycontainer mydockerhubusername/myimage:1.0
     ```
   - Flags:
     - `-d`: Run the container in detached mode (in the background).
     - `--name`: Assign a name to the container.

3. **Using Public Images**
   - Public images on Docker Hub can be pulled without authentication.
   - Example:
     ```bash
     docker pull nginx:latest
     docker run -d --name webserver nginx:latest
     ```

4. **Updating Images**
   - To update an image, pull the latest version and restart the container.
   - Example:
     ```bash
     docker pull mydockerhubusername/myimage:2.0
     docker stop mycontainer
     docker rm mycontainer
     docker run -d --name mycontainer mydockerhubusername/myimage:2.0
     ```

---

### **Best Practices**

1. **Use Semantic Versioning**:
   - Tag images with meaningful versions (e.g., `1.0`, `1.1`, `2.0`).

2. **Avoid Using `latest` in Production**:
   - The `latest` tag can lead to inconsistencies. Always specify a version.

3. **Optimize Image Size**:
   - Use multi-stage builds and minimize layers to reduce image size.

4. **Secure Your Images**:
   - Use private repositories for sensitive images.
   - Scan images for vulnerabilities using tools like `docker scan`.

5. **Document Your Images**:
   - Add a `README.md` to your Docker Hub repository to explain how to use the image.

---

# [Section 3 - MANAGING DATA & WORKING WITH VOLUMES](#docker--kubernetes)

- [Understanding Data Categories / Different Kinds of Data](#understanding-data-categories--different-kinds-of-data)
- [Introducing Volumes](#introducing-volumes)
- [Volumes: Named and Anonymous / Bind Mounts](#volumes-named-and-anonymous--bind-mounts)
- [Bind Mounts: Shortcuts](#bind-mounts-shortcuts)
- [Combining & Merging Different Volumes](#combining--merging-different-volumes)
- [A Look at Read-Only Volumes](#a-look-at-read-only-volumes)
- [Managing Docker Volumes](#managing-docker-volumes)
- [Using "COPY" vs Bind Mounts](#using-copy-vs-bind-mounts)
- [Don't COPY everything: Using "dockerignore" Files](#dont-copy-everything-using-dockerignore-files)
- [Adding more to the .dockerignore File](#adding-more-to-the-dockerignore-file)
- [Working with Environment Variables & ".env" Files](#working-with-environment-variables--env-files)
- [Environment Variables & Security](#environment-variables--security)
- [Using Build Arguments (ARG)](#using-build-arguments-arg)

## [Understanding Data Categories / Different Kinds of Data](#section-3---managing-data--working-with-volumes)

### **Understanding Data Categories / Different Kinds of Data**

When working with Docker, it’s important to understand the different types of data your applications might use. Data can be broadly categorized into two main types:

1. **Persistent Data**  
2. **Ephemeral Data**

Let’s break these down:

---

#### **1. Persistent Data**
Persistent data is data that needs to survive beyond the lifecycle of a container. This type of data is critical for applications that require long-term storage, such as databases, user uploads, or configuration files.

- **Characteristics**:
  - Survives container restarts, removal, or crashes.
  - Must be stored outside the container’s writable layer.
  - Typically stored in **volumes** or **bind mounts**.

- **Examples**:
  - Database files (e.g., MySQL, PostgreSQL).
  - Application logs that need to be retained.
  - Configuration files that should persist across deployments.
  - User-uploaded files (e.g., images, documents).

- **How Docker Handles Persistent Data**:
  - **Volumes**: Managed by Docker and stored in a dedicated directory on the host machine (`/var/lib/docker/volumes/`). Volumes are the preferred way to handle persistent data in Docker.
  - **Bind Mounts**: Directly map a file or directory on the host machine into the container. Useful for development or when you need to share specific files.

---

#### **2. Ephemeral Data**
Ephemeral data is temporary data that only exists for the duration of the container’s lifecycle. This type of data is not critical to retain after the container stops or is removed.

- **Characteristics**:
  - Tied to the container’s lifecycle.
  - Stored in the container’s writable layer (container layer).
  - Deleted when the container is removed.

- **Examples**:
  - Temporary cache files.
  - Session data (e.g., user sessions in a web application).
  - Intermediate computation results.

- **How Docker Handles Ephemeral Data**:
  - By default, all data written to the container’s filesystem is ephemeral.
  - For better performance, you can use **tmpfs mounts** to store ephemeral data in memory (RAM) instead of on disk.

---

#### **Key Differences Between Persistent and Ephemeral Data**

| **Aspect**            | **Persistent Data**                          | **Ephemeral Data**                        |
|------------------------|----------------------------------------------|-------------------------------------------|
| **Lifetime**           | Survives container restarts/removal.         | Tied to the container’s lifecycle.        |
| **Storage Location**   | Volumes or bind mounts.                      | Container’s writable layer or tmpfs.      |
| **Use Case**           | Databases, logs, user uploads, configs.      | Cache, session data, temporary files.     |
| **Performance**        | Slower (disk-based).                         | Faster (in-memory for tmpfs).             |
| **Management**         | Managed by Docker (volumes) or manually (bind mounts). | Automatically managed by Docker.          |

---

#### **Best Practices for Managing Data in Docker**
1. **Use Volumes for Persistent Data**: Volumes are the recommended way to manage persistent data because they are fully managed by Docker and provide better performance and portability.
2. **Avoid Writing Data to the Container Layer**: Writing data to the container’s writable layer can lead to bloated images and slower performance. Use volumes or bind mounts instead.
3. **Use tmpfs for Ephemeral Data**: For temporary data that doesn’t need to persist, consider using tmpfs mounts to store data in memory for faster access.
4. **Backup Your Volumes**: Regularly back up data stored in volumes to prevent data loss.
5. **Use Named Volumes for Production**: Named volumes are easier to manage and reference than anonymous volumes.

---

#### **Summary**
Understanding the difference between persistent and ephemeral data is crucial for effectively managing data in Docker. Persistent data should be stored in volumes or bind mounts to ensure it survives container restarts or removal, while ephemeral data can be stored in the container’s writable layer or in memory using tmpfs. By following best practices, you can ensure your applications are both efficient and reliable.

---

## [Introducing Volumes](#section-3---managing-data--working-with-volumes)

### **Introducing Volumes**

Volumes are a mechanism for **persisting data** generated and used by Docker containers. They are the preferred way to manage persistent data in Docker because they are fully managed by Docker and provide several advantages over other storage options (like bind mounts or the container’s writable layer).

---

#### **What Are Volumes?**
- Volumes are **directories** (or files) stored outside the container’s filesystem, typically on the host machine.
- They are managed by Docker and stored in a dedicated directory on the host (`/var/lib/docker/volumes/` on Linux).
- Volumes are independent of the container lifecycle, meaning they persist even if the container is stopped, removed, or replaced.

---

#### **Why Use Volumes?**
1. **Data Persistence**: Volumes ensure that data is not lost when a container is removed or crashes.
2. **Performance**: Volumes are optimized for performance, especially when compared to writing data to the container’s writable layer.
3. **Portability**: Volumes can be easily shared among multiple containers.
4. **Backup and Migration**: Volumes make it easier to back up and migrate data.
5. **Decoupling Data from Containers**: Volumes allow you to separate data storage from the application logic, making your containers more modular and easier to manage.

---

#### **Types of Volumes**
1. **Named Volumes**: 
   - Created and managed by Docker.
   - Easier to reference and manage than anonymous volumes.
   - Example: `myapp_data`.

2. **Anonymous Volumes**:
   - Created by Docker automatically when no volume name is specified.
   - Harder to manage because they have random, auto-generated names.
   - Example: `f7a8b9c0d1e2`.

3. **Host Volumes (Bind Mounts)**:
   - Not technically a "volume," but a way to map a specific directory on the host to a directory in the container.
   - Useful for development or when you need fine-grained control over the host’s filesystem.
   - Example: `/home/user/app:/app`.

---

#### **Real-World Examples of Using Volumes**

##### **Example 1: Database Storage**
Imagine you’re running a MySQL database in a Docker container. You want to ensure that your database files (like tables and records) are not lost if the container is removed.

```bash
# Create a named volume for MySQL data
docker volume create mysql_data

# Run a MySQL container and attach the volume
docker run -d \
  --name mysql_db \
  -e MYSQL_ROOT_PASSWORD=mysecretpassword \
  -v mysql_data:/var/lib/mysql \
  mysql:latest
```

- Here, the `mysql_data` volume stores the database files at `/var/lib/docker/volumes/mysql_data/_data` on the host.
- Even if the container is removed, the data remains safe in the volume.

---

##### **Example 2: Sharing Data Between Containers**
Suppose you have a web application that consists of two containers: one for the app and one for a logging service. You want both containers to access the same log files.

```bash
# Create a named volume for logs
docker volume create app_logs

# Run the app container and attach the volume
docker run -d \
  --name my_app \
  -v app_logs:/app/logs \
  my_app_image

# Run the logging service and attach the same volume
docker run -d \
  --name logging_service \
  -v app_logs:/logs \
  logging_service_image
```

- Both containers can read/write to the `app_logs` volume, enabling seamless sharing of log files.

---

##### **Example 3: Development with Bind Mounts**
During development, you might want to mount your local source code into the container for real-time updates.

```bash
# Run a Node.js app with a bind mount for the source code
docker run -d \
  --name my_node_app \
  -v /home/user/myapp:/app \
  -p 3000:3000 \
  node:14
```

- The `/home/user/myapp` directory on the host is mounted to `/app` in the container.
- Any changes you make to the source code on your host are immediately reflected in the container.

---

##### **Example 4: Using tmpfs for Ephemeral Data**
For temporary data that doesn’t need to persist, you can use `tmpfs` to store it in memory.

```bash
# Run a container with tmpfs for temporary data
docker run -d \
  --name my_temp_app \
  --tmpfs /tmp \
  my_temp_app_image
```

- The `/tmp` directory in the container is stored in memory (RAM) and is deleted when the container stops.

---

#### **Key Commands for Managing Volumes**
Here are some essential Docker commands for working with volumes:

1. **Create a Volume**:
   ```bash
   docker volume create my_volume
   ```

2. **List Volumes**:
   ```bash
   docker volume ls
   ```

3. **Inspect a Volume**:
   ```bash
   docker volume inspect my_volume
   ```

4. **Remove a Volume**:
   ```bash
   docker volume rm my_volume
   ```

5. **Remove All Unused Volumes**:
   ```bash
   docker volume prune
   ```

---

#### **Best Practices for Using Volumes**
1. **Use Named Volumes for Production**: Named volumes are easier to manage and reference than anonymous volumes.
2. **Avoid Using the Container’s Writable Layer**: Writing data to the container’s filesystem can lead to bloated images and slower performance.
3. **Backup Your Volumes**: Regularly back up data stored in volumes to prevent data loss.
4. **Use Bind Mounts for Development**: Bind mounts are great for development because they allow you to sync files between the host and the container in real time.
5. **Use tmpfs for Temporary Data**: For ephemeral data, use `tmpfs` to store it in memory for better performance.

---

#### **Summary**
Volumes are a powerful feature in Docker that allow you to manage persistent data effectively. They decouple data storage from containers, ensuring data persistence, improving performance, and making it easier to share data between containers. Whether you’re running a database, sharing logs, or developing an application, volumes are an essential tool in your Docker toolkit.

---

## [Volumes: Named and Anonymous / Bind Mounts](#section-3---managing-data--working-with-volumes)

Docker provides several ways to manage and persist data in containers. The three main mechanisms are:
1. **Volumes** (Named and Anonymous)
2. **Bind Mounts**

Let’s break them down:

---

### **1. Volumes**
Volumes are the preferred way to persist data in Docker. They are managed by Docker and stored in a dedicated directory on the host machine (usually `/var/lib/docker/volumes` on Linux). Volumes are independent of the container lifecycle, meaning they persist even if the container is deleted.

#### **Types of Volumes:**
- **Named Volumes**: Volumes with a specific name that you define.
- **Anonymous Volumes**: Volumes that are automatically created by Docker and assigned a random name.

#### **Key Features:**
- Managed by Docker.
- Can be shared across multiple containers.
- Persist even after the container is removed.
- Ideal for databases, application data, and other persistent storage needs.

#### **Example: Named Volume**
```bash
# Create a named volume
docker volume create my_named_volume

# Run a container and attach the named volume
docker run -d --name my_container -v my_named_volume:/app/data my_image
```
- Here, `my_named_volume` is a named volume mounted to `/app/data` inside the container.
- The data stored in `/app/data` will persist even if the container is deleted.

#### **Example: Anonymous Volume**
```bash
# Run a container with an anonymous volume
docker run -d --name my_container -v /app/data my_image
```
- Docker automatically creates an anonymous volume and mounts it to `/app/data`.
- The volume will have a random name like `f7a2b3c4d5e6...`.

#### **Inspecting Volumes**
```bash
# List all volumes
docker volume ls

# Inspect a specific volume
docker volume inspect my_named_volume
```

---

### **2. Bind Mounts**
Bind mounts allow you to mount a specific file or directory from the host machine into the container. Unlike volumes, bind mounts are not managed by Docker and rely on the host's filesystem.

#### **Key Features:**
- Directly map a host directory to a container directory.
- Useful for development (e.g., mounting source code).
- Changes on the host are immediately reflected in the container, and vice versa.
- Not ideal for production (due to tight coupling with the host filesystem).

#### **Example: Bind Mount**
```bash
# Run a container with a bind mount
docker run -d --name my_container -v /home/user/app:/app my_image
```
- Here, the host directory `/home/user/app` is mounted to `/app` in the container.
- Any changes made in `/home/user/app` on the host will be reflected in `/app` in the container, and vice versa.

#### **Use Case: Development Workflow**
Bind mounts are commonly used during development to sync code between the host and the container:
```bash
# Mount a local project directory into the container
docker run -d --name dev_container -v $(pwd):/app my_image
```
- This allows you to edit code on your local machine and see the changes immediately in the container.

---

### **Comparison: Volumes vs. Bind Mounts**

| Feature                  | Volumes                        | Bind Mounts                  |
|--------------------------|--------------------------------|------------------------------|
| **Managed by Docker**    | Yes                            | No                           |
| **Persistence**          | Persist beyond container life  | Tied to host directory       |
| **Performance**           | Optimized for Docker           | Depends on host filesystem   |
| **Use Case**             | Production, databases          | Development, local testing   |
| **Portability**          | Easily portable                | Tied to host filesystem      |

---

### **Real-World Examples**

#### **1. Using Named Volumes for a Database**
```bash
# Create a named volume for PostgreSQL data
docker volume create pg_data

# Run a PostgreSQL container with the named volume
docker run -d --name postgres_db -v pg_data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=mysecretpassword postgres
```
- The database data is stored in the `pg_data` volume and will persist even if the container is deleted.

#### **2. Using Bind Mounts for Development**
```bash
# Mount a local React app directory into a Node.js container
docker run -d --name react_dev -v $(pwd)/src:/app/src -p 3000:3000 node:14
```
- You can edit the React app code on your local machine, and the changes will be reflected in the container in real-time.

#### **3. Combining Volumes and Bind Mounts**
```bash
# Run a container with both a named volume and a bind mount
docker run -d --name my_app -v my_named_volume:/app/data -v $(pwd)/config:/app/config my_image
```
- Persistent data is stored in the named volume (`my_named_volume`), while configuration files are mounted from the host (`$(pwd)/config`).

---

### **Best Practices**
- Use **named volumes** for production workloads where data persistence and portability are critical.
- Use **bind mounts** for development or when you need direct access to host files.
- Avoid using **anonymous volumes** unless you have a specific use case, as they can be harder to manage.

---

## [Bind Mounts: Shortcuts](#section-3---managing-data--working-with-volumes)

macOS / Linux:
```bash
-v $(pwd):/app
```

Windows:
```bash
-v "%cd%":/app
```

## [Combining & Merging Different Volumes](#section-3---managing-data--working-with-volumes)

When running a container, you can mount multiple volumes or bind mounts to different directories inside the container. However, sometimes you may want to **combine or merge** data from multiple volumes or directories into a single directory inside the container. This can be achieved using Docker's volume mounting mechanisms.

---

### **Key Concepts**

1. **Overlapping Mounts**:
   - When you mount multiple volumes or bind mounts to the same directory inside the container, the last mount will **override** the previous ones.
   - This means only the data from the last-mounted volume or directory will be visible in the container.

2. **Merging Data**:
   - Docker does not natively support merging data from multiple volumes or bind mounts into a single directory.
   - However, you can achieve this by using **union filesystems** (e.g., `overlayfs`) or by manually copying data during container startup.

---

### **Example 1: Overlapping Mounts**
When multiple volumes or bind mounts are mounted to the same directory, the last mount takes precedence.

```bash
# Create two named volumes
docker volume create volume1
docker volume create volume2

# Run a container with both volumes mounted to the same directory
docker run -d --name my_container -v volume1:/app/data -v volume2:/app/data my_image
```
- In this case, only the data from `volume2` will be visible in `/app/data` inside the container because it was mounted last.

---

### **Example 2: Combining Volumes into Separate Directories**
If you want to combine data from multiple volumes without overlapping, mount them to separate directories inside the container.

```bash
# Create two named volumes
docker volume create volume1
docker volume create volume2

# Run a container with both volumes mounted to separate directories
docker run -d --name my_container -v volume1:/app/data1 -v volume2:/app/data2 my_image
```
- Here, the data from `volume1` will be available in `/app/data1`, and the data from `volume2` will be available in `/app/data2`.

---

### **Example 3: Merging Data Using a Union Filesystem**
To merge data from multiple volumes or bind mounts into a single directory, you can use a **union filesystem** like `overlayfs`. This requires some manual setup.

#### **Steps:**
1. Create a directory structure on the host for the union filesystem.
2. Use the `overlay` storage driver to merge the directories.

```bash
# Create directories for the union filesystem
mkdir -p /tmp/overlay/{lower1,lower2,upper,work,merged}

# Create files in the lower directories
echo "Data from volume1" > /tmp/overlay/lower1/file1.txt
echo "Data from volume2" > /tmp/overlay/lower2/file2.txt

# Mount the overlay filesystem
mount -t overlay overlay -o lowerdir=/tmp/overlay/lower1:/tmp/overlay/lower2,upperdir=/tmp/overlay/upper,workdir=/tmp/overlay/work /tmp/overlay/merged

# Run a container with the merged directory mounted
docker run -d --name my_container -v /tmp/overlay/merged:/app/data my_image
```
- The contents of `lower1` and `lower2` will be merged into `/tmp/overlay/merged` and mounted to `/app/data` in the container.

---

### **Example 4: Merging Data During Container Startup**
If you cannot use a union filesystem, you can manually copy data from multiple volumes into a single directory during container startup.

#### **Dockerfile Example:**
```Dockerfile
FROM alpine:latest
RUN mkdir -p /app/data
COPY merge-script.sh /merge-script.sh
RUN chmod +x /merge-script.sh
CMD ["/merge-script.sh"]
```

#### **merge-script.sh:**
```bash
#!/bin/sh
# Copy data from multiple volumes into a single directory
cp -r /app/data1/* /app/data/
cp -r /app/data2/* /app/data/

# Start the main application
exec my_application
```

#### **Running the Container:**
```bash
# Create two named volumes
docker volume create volume1
docker volume create volume2

# Run the container with both volumes mounted
docker run -d --name my_container -v volume1:/app/data1 -v volume2:/app/data2 my_image
```
- The `merge-script.sh` script will copy data from `/app/data1` and `/app/data2` into `/app/data` during container startup.

---

### **Best Practices**
- Use **separate directories** for each volume or bind mount if you don’t need to merge data.
- Use a **union filesystem** (e.g., `overlayfs`) if you need to merge data from multiple sources.
- Avoid overlapping mounts unless you intentionally want to override data.
- For complex setups, consider using **Docker Compose** to manage multiple volumes and bind mounts.

---

### **Real-World Use Case: Combining Configuration and Data**
Imagine you have a web application that requires:
- Default configuration files (stored in a named volume).
- Custom configuration files (stored in a bind mount on the host).
- Application data (stored in another named volume).

You can combine these into a single directory structure inside the container using the techniques described above.

---

## [A Look at Read-Only Volumes](#section-3---managing-data--working-with-volumes)

- **Purpose**: Read-only volumes are used to ensure that the container can only read data from the volume and cannot modify it. This is particularly useful for scenarios where data integrity is critical, such as configuration files, shared libraries, or static assets.
- **Usage**: You can create a read-only volume by appending the `:ro` flag to the volume mount command.
- **Example**:
  ```bash
  docker run -v /host/config:/container/config:ro my-image
  ```
  In this example:
  - `/host/config` is the directory on the host machine.
  - `/container/config` is the directory inside the container.
  - The `:ro` flag makes the volume read-only, so the container cannot write to `/container/config`.

---

## [Managing Docker Volumes](#section-3---managing-data--working-with-volumes)

- **Purpose**: Docker volumes are used to persist data outside of containers, ensuring that data is not lost when containers are stopped or removed. Volumes are managed by Docker and can be shared among multiple containers.
- **Commands**:
  - **Create a volume**: `docker volume create my-volume`
    - Creates a new volume named `my-volume`.
  - **List volumes**: `docker volume ls`
    - Lists all volumes on the Docker host.
  - **Inspect a volume**: `docker volume inspect my-volume`
    - Provides detailed information about the volume, including its mount point on the host.
  - **Remove a volume**: `docker volume rm my-volume`
    - Deletes the specified volume.
  - **Prune unused volumes**: `docker volume prune`
    - Removes all unused volumes to free up space.
- **Example**:
  ```bash
  docker run -d --name my-container -v my-volume:/app/data my-image
  ```
  - This command mounts the `my-volume` volume to `/app/data` in the container.
  - Data written to `/app/data` will persist even if the container is removed.

---

## [Using "COPY" vs Bind Mounts](#section-3---managing-data--working-with-volumes)

- **COPY**:
  - **Purpose**: The `COPY` instruction in a Dockerfile is used to copy files or directories from the host machine into the Docker image during the build process. This is ideal for static files that are part of the application, such as code, configuration files, or assets.
  - **Example**:
    ```Dockerfile
    COPY ./src /app/src
    ```
    - This copies the `./src` directory on the host to `/app/src` in the image.
    - The files become part of the image and are immutable once the image is built.

- **Bind Mounts**:
  - **Purpose**: Bind mounts are used to link a directory or file from the host machine to the container at runtime. This is useful for development, where you want to sync changes between the host and container without rebuilding the image.
  - **Example**:
    ```bash
    docker run -v /host/app:/container/app my-image
    ```
    - This mounts `/host/app` on the host to `/container/app` in the container.
    - Changes made on the host are immediately reflected in the container, and vice versa.

---

## [Don't COPY everything: Using "dockerignore" Files](#section-3---managing-data--working-with-volumes)

- **Purpose**: The `.dockerignore` file prevents unnecessary files from being copied into the Docker image during the build process. This reduces the image size and speeds up the build process.
- **Example**:
  ```.dockerignore
  node_modules
  .git
  *.log
  ```
  - This ignores the `node_modules` directory, `.git` folder, and all `.log` files.
  - These files are not copied into the image, even if they exist in the build context.

---

## [Adding more to the .dockerignore File](#section-3---managing-data--working-with-volumes)

- **Purpose**: You can add more patterns to the `.dockerignore` file to exclude additional files or directories. This is useful for excluding temporary files, logs, or other non-essential files.
- **Example**:
  ```.dockerignore
  # Ignore all temporary files
  tmp/*
  
  # Ignore specific file types
  *.md
  *.txt
  
  # Ignore a specific directory
  tests/
  ```
  - This ensures that temporary files, markdown files, text files, and the `tests/` directory are not copied into the image.

---

## [Working with Environment Variables & ".env" Files](#section-3---managing-data--working-with-volumes)

- **Purpose**: Environment variables are used to configure container behavior without modifying the Docker image. The `.env` file is a convenient way to define these variables in a single location.
- **Example**:
  ```.env
  DB_HOST=localhost
  DB_USER=admin
  DB_PASS=password
  ```
  - You can use these variables in your Dockerfile or during container runtime:
    ```bash
    docker run --env-file .env my-image
    ```
  - The container will have access to `DB_HOST`, `DB_USER`, and `DB_PASS` as environment variables.

---

## [Environment Variables & Security](#section-3---managing-data--working-with-volumes)

- **Purpose**: Environment variables can contain sensitive information (e.g., passwords, API keys). It's important to handle them securely to avoid exposing sensitive data.
- **Best Practices**:
  - **Avoid hardcoding sensitive data in Dockerfiles**: Use `.env` files or Docker secrets instead.
  - **Use `.env` files securely**: Ensure `.env` files are not committed to version control by adding them to `.gitignore`.
  - **Use Docker secrets for production**: Docker secrets provide a secure way to manage sensitive data.
- **Example**:
  ```bash
  docker run -e DB_PASSWORD=secret my-image
  ```
  - This sets the `DB_PASSWORD` environment variable securely.
  - Avoid using this method in production; instead, use Docker secrets or a secrets management tool.

---

## [Using Build Arguments (ARG)](#section-3---managing-data--working-with-volumes)

- **Purpose**: Build arguments (`ARG`) allow you to pass variables during the image build process. These variables are not available in the final image or at runtime, making them ideal for build-time configuration.
- **Example**:
  ```Dockerfile
  ARG APP_VERSION=1.0
  ENV APP_VERSION=${APP_VERSION}
  ```
  - This sets a default value for `APP_VERSION` as `1.0`.
  - You can override the default value during the build:
    ```bash
    docker build --build-arg APP_VERSION=2.0 -t my-image .
    ```
  - The `APP_VERSION` environment variable in the container will be set to `2.0`.

---

# [Section 4 - NETWORKING: (CROSS-)CONTAINER COMMUNICATION](#docker--kubernetes)

- [Container to WWW Communication](#container-to-www-communication)
- [Container to Local Host Machine Communication](#container-to-local-host-machine-communication)
- [Container to Container Communication](#container-to-container-communication)
- [Introducing Docker Networks: Elegant Container to Container Communication](#introducing-docker-networks-elegant-container-to-container-communication)
- [How Docker Resolves IP Addresses](#how-docker-resolves-ip-addresses)
- [Docker Network Drivers](#docker-network-drivers)

## Module Introduction

### Introduction to Networking in Docker
Networking is a fundamental aspect of Docker that enables containers to communicate with each other, with the host system, and with external networks. In this section, you'll learn how Docker handles networking and how to configure it for various use cases, such as:

1. **Container-to-Container Communication**: How containers within the same Docker network can talk to each other.
2. **Container-to-Host Communication**: How containers can communicate with services running on the host machine.
3. **Container-to-External Communication**: How containers can access external networks (e.g., the internet) and how external systems can access services running inside containers.
4. **Cross-Container Communication**: How containers running on different hosts or in different environments can communicate securely.

---

### Why Networking Matters in Docker
- **Isolation**: By default, containers are isolated from each other. Networking allows you to control how and when containers interact.
- **Scalability**: Networking enables you to scale applications by running multiple containers and distributing traffic among them.
- **Microservices Architecture**: In modern applications, services are often broken into smaller, independent components (microservices). Networking allows these components to communicate seamlessly.
- **Security**: Properly configured networks ensure that only authorized containers can communicate with each other, reducing the risk of unauthorized access.

---

### Key Concepts in Docker Networking
1. **Docker Network Drivers**:
   Docker provides several network drivers to support different use cases:
   - **Bridge**: The default network driver. It creates an internal network for containers on the same host.
   - **Host**: Removes network isolation between the container and the host, allowing the container to use the host's network directly.
   - **Overlay**: Enables communication between containers running on different Docker hosts (e.g., in a Docker Swarm or Kubernetes cluster).
   - **Macvlan**: Assigns a MAC address to each container, making it appear as a physical device on the network.
   - **None**: Disables networking for the container.

2. **Container Networking Model (CNM)**:
   Docker uses the CNM to manage networking. It consists of three main components:
   - **Sandbox**: An isolated network stack for a container (includes interfaces, routing tables, and DNS settings).
   - **Endpoint**: A connection point that links a sandbox to a network.
   - **Network**: A group of endpoints that can communicate with each other.

3. **DNS Resolution**:
   Docker provides built-in DNS resolution for containers on the same network. Containers can communicate using their container names instead of IP addresses.

4. **Port Mapping**:
   Containers can expose ports to the host or external networks, allowing external systems to access services running inside the container.

---

### What You'll Learn in This Section
- **Creating and Managing Docker Networks**: How to create custom networks and connect containers to them.
- **Container-to-Container Communication**: How to enable communication between containers on the same network.
- **Cross-Container Communication**: How to connect containers running on different hosts or in different environments.
- **Exposing Container Ports**: How to map container ports to the host or external networks.
- **Using Docker Compose for Networking**: How to define and manage networks in multi-container applications using Docker Compose.
- **Advanced Networking Scenarios**: How to configure overlay networks, use Macvlan, and secure container communication.

---

### Real-World Use Cases
1. **Microservices Communication**:
   - Multiple containers (e.g., a frontend, backend, and database) need to communicate with each other.
   - Docker networks allow them to interact securely and efficiently.

2. **Load Balancing**:
   - Multiple instances of a service can run behind a load balancer, distributing traffic across containers.

3. **Multi-Host Applications**:
   - In a Docker Swarm or Kubernetes cluster, containers running on different hosts need to communicate using overlay networks.

4. **Development and Testing**:
   - Networking allows you to simulate production environments locally, enabling easier debugging and testing.

---

### Example: Basic Container Communication
Let's say you have two containers: a web server (`web`) and a database (`db`). You want the web server to communicate with the database.

1. **Create a custom network**:
   ```bash
   docker network create my-network
   ```

2. **Run the database container**:
   ```bash
   docker run -d --name db --network my-network my-database-image
   ```

3. **Run the web server container**:
   ```bash
   docker run -d --name web --network my-network -p 80:80 my-web-image
   ```

4. **Communication**:
   - The `web` container can connect to the `db` container using the hostname `db`.
   - For example, the web server can connect to the database using the connection string `db:3306`.

---

## [Container to WWW Communication](#section-4---networking-cross-container-communication)

### Explanation:
Containers can communicate with the outside world (e.g., the internet) by default. Docker uses the host machine's network interface to allow containers to access external resources. This is facilitated by Docker's default bridge network.

### Example:
If you run a container and it tries to access a website (e.g., `curl https://www.google.com`), Docker will route the request through the host machine's network interface.

```bash
docker run alpine ping google.com
```

This command will start an Alpine Linux container and ping `google.com`. The container uses the host's network to reach the internet.

---

## [Container to Local Host Machine Communication](#section-4---networking-cross-container-communication)

### Explanation:
Containers can communicate with the local host machine using the special DNS name `host.docker.internal`. This is particularly useful for accessing services running on the host machine, such as databases or APIs.

### Example:
If you have a web server running on your host machine at `localhost:8080`, a container can access it using `host.docker.internal:8080`.

```bash
docker run alpine curl http://host.docker.internal:8080
```

This command will start an Alpine Linux container and make an HTTP request to the web server running on the host machine.

---

## [Container to Container Communication](#section-4---networking-cross-container-communication)

### Explanation:
Containers can communicate with each other directly. By default, Docker assigns each container an IP address on the `bridge` network. Containers can use these IP addresses to communicate with each other.

### Example:
Start two containers and have one ping the other using its IP address.

```bash
# Start the first container
docker run -d --name container1 alpine sleep 1000

# Get the IP address of container1
CONTAINER1_IP=$(docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container1)

# Start the second container and ping container1
docker run alpine ping $CONTAINER1_IP
```

This will start two containers, and the second container will ping the first one using its IP address.

---

## [Introducing Docker Networks: Elegant Container to Container Communication](#section-4---networking-cross-container-communication)

### Explanation:
Docker provides a more elegant way to handle container-to-container communication through **user-defined networks**. When containers are connected to the same user-defined network, they can communicate with each other using their container names as hostnames.

### Example:
Create a custom network and connect two containers to it.

```bash
# Create a custom network
docker network create my_network

# Start two containers connected to the custom network
docker run -d --name container1 --network my_network alpine sleep 1000
docker run -d --name container2 --network my_network alpine sleep 1000

# Ping container1 from container2 using its name
docker exec container2 ping container1
```

In this example, `container2` can ping `container1` using the hostname `container1` because they are on the same custom network.

---

## [How Docker Resolves IP Addresses](#section-4---networking-cross-container-communication)

### Explanation:
Docker uses an embedded DNS server to resolve container names to IP addresses within user-defined networks. When containers are connected to the same network, they can communicate using their container names instead of IP addresses.

### Example:
When you create a custom network and connect containers to it, Docker automatically handles DNS resolution.

```bash
# Create a custom network
docker network create my_network

# Start two containers connected to the custom network
docker run -d --name container1 --network my_network alpine sleep 1000
docker run -d --name container2 --network my_network alpine sleep 1000

# Ping container1 from container2 using its name
docker exec container2 ping container1
```

Here, Docker resolves `container1` to its IP address automatically.

---

## [Docker Network Drivers](#section-4---networking-cross-container-communication)

### Explanation:
Docker provides several network drivers to manage how containers communicate with each other and the outside world. The most common drivers are:

1. **Bridge**: The default network driver. Containers on the same bridge network can communicate with each other using IP addresses or container names.
2. **Host**: Removes network isolation between the container and the host. The container uses the host's network directly.
3. **Overlay**: Used for multi-host communication in Docker Swarm. Allows containers on different hosts to communicate.
4. **Macvlan**: Assigns a MAC address to each container, making it appear as a physical device on the network.
5. **None**: Disables all networking for the container.

### Example:
Using the `host` network driver.

```bash
docker run --network host alpine ifconfig
```

This command will start an Alpine container using the host's network stack, and the `ifconfig` command will show the host's network interfaces.

### Instructor Notes:

Docker Networks actually support different kinds of **"Drivers"** which influence the behavior of the Network.

The default driver is the **"bridge"** driver - it provides the behavior shown in this module (i.e. Containers can find each other by name if they are in the same Network).

The driver can be set when a Network is created, simply by adding the `--driver` option.
```bash
docker network create --driver bridge my-net
```

_Of course, if you want to use the "bridge" driver, you can simply omit the entire option since "bridge" is the default anyways._

Docker also supports these alternative drivers - though you will use the "bridge" driver in most cases:

1. **host**: For standalone containers, isolation between container and host system is removed (i.e. they share localhost as a network)

2. **overlay**: Multiple Docker daemons (i.e. Docker running on different machines) are able to connect with each other. Only works in "Swarm" mode which is a dated / almost deprecated way of connecting multiple containers

3. **macvlan**: You can set a custom MAC address to a container - this address can then be used for communication with that container

4. **none**: All networking is disabled.

5. **Third-party plugins**: You can install third-party plugins which then may add all kinds of behaviors and functionalities

As mentioned, the **"bridge"** driver makes most sense in the vast majority of scenarios.

---

# [Section 5 - BUILDING MULTI-CONTAINER APPLICATIONS WITH DOCKER](#docker--kubernetes)

- [Our Target App & Setup](#our-target-app--setup)
- [Dockerizing the MongoDB Service](#dockerizing-the-mongodb-service)
- [Dockerizing the Node App](#dockerizing-the-node-app)
- [Moving the React SPA into a Container](#moving-the-react-spa-into-a-container)
- [Adding Docker Networks for Efficient Cross-Container Communication](#adding-docker-networks-for-efficient-cross-container-communication)
- [Fixing MongoDB Authentication Errors (relevant for next lecture)](#fixing-mongodb-authentication-errors)
- [Adding Data Persistence to MongoDB with Volumes](#adding-data-persistence-to-mongodb-with-volumes)
- [Volumes, Bind Mounts & Polishing for the NodeJS Container](#volumes-bind-mounts--polishing-for-the-nodejs-container)
- [Live Source Code Updates for the React Container (with Bind Mounts)](#live-source-code-updates-for-the-react-container-with-bind-mounts)

## Module Introduction

In modern application development, it's common to build applications that consist of multiple services or components. For example, a web application might have a frontend, a backend, a database, and a caching layer. Each of these components can be run in separate containers, allowing for better scalability, isolation, and maintainability.

Docker is a powerful tool for containerizing applications, but when working with multi-container applications, managing these containers individually can become complex. This module focuses on **orchestrating multi-container applications** using Docker tools and best practices. You'll learn how to define, manage, and scale multi-container applications effectively.

---

### Why Multi-Container Applications?

#### Benefits of Multi-Container Applications

1. **Modularity**: Each service can be developed, deployed, and scaled independently.
2. **Isolation**: Containers isolate services, reducing the risk of conflicts between dependencies.
3. **Scalability**: Individual services can be scaled horizontally to handle increased traffic.
4. **Portability**: Docker containers can run on any system that supports Docker, ensuring consistency across environments.

#### Challenges of Multi-Container Applications

While multi-container applications offer many benefits, they also introduce complexity:

1. **Coordination**: Ensuring all containers start and stop in the correct order.
2. **Networking**: Configuring communication between containers.
3. **Data Persistence**: Managing data for stateful services like databases.
4. **Scalability**: Scaling individual services without disrupting the application.

---

### Example: A Typical Multi-Container Application

Consider a web application with the following components:

1. **Frontend**: A React application served by an Nginx web server.
2. **Backend**: A Node.js API that handles business logic.
3. **Database**: A PostgreSQL database for storing application data.
4. **Cache**: A Redis instance for caching frequently accessed data.

Each of these components can be run in a separate container. Docker allows you to define how these containers interact with each other, ensuring the application works as a cohesive unit.

---

### The Need for Orchestration Tools

Managing multi-container applications manually can be tedious and error-prone. For example:

- Starting each container individually with the correct configuration.
- Ensuring containers are connected to the same network.
- Managing dependencies between services (e.g., the backend depends on the database).

This is where **orchestration tools** like Docker Compose come in. Docker Compose simplifies the process of defining, running, and managing multi-container applications by using a single configuration file.

---

### What You'll Learn in This Section

In this section, you'll learn:

1. **The Basics of Multi-Container Applications**: How to break down an application into multiple services and run them in separate containers.
2. **Manual Multi-Container Setup**: How to manually create and connect containers using Docker commands.
3. **Challenges of Manual Setup**: The limitations of managing multi-container applications without orchestration tools.
4. **Introduction to Docker Compose**: A brief overview of Docker Compose and how it solves the challenges of manual container management.

---

### Hands-On Example: Manual Multi-Container Setup

To understand the challenges of managing multi-container applications, let's manually set up a simple application with two services:

1. **Web Server**: An Nginx container serving a static website.
2. **Database**: A PostgreSQL container for storing data.

#### Steps:

1. **Create a Network**:
   ```bash
   docker network create myapp-network
   ```

2. **Run the Database Container**:
   ```bash
   docker run -d \
     --name myapp-db \
     --network myapp-network \
     -e POSTGRES_USER=user \
     -e POSTGRES_PASSWORD=password \
     postgres:13
   ```

3. **Run the Web Server Container**:
   ```bash
   docker run -d \
     --name myapp-web \
     --network myapp-network \
     -p 80:80 \
     nginx:latest
   ```

#### Challenges:

- **Dependency Management**: If the web server depends on the database, you need to ensure the database starts first.
- **Networking**: You must manually create and connect containers to the same network.
- **Scalability**: Scaling services manually is time-consuming and error-prone.

---

### Conclusion

This section introduced the concept of multi-container applications and highlighted the challenges of managing them manually. In the next section, you'll learn how **Docker Compose** simplifies this process by allowing you to define and run multi-container applications with a single configuration file.

---

Absolutely! Below are detailed notes for each of the topics in the section. I'll use a simple Node.js app as the example, which includes a React frontend, a Node.js backend, and a MongoDB database. These notes are structured for clarity and can be saved in a `.md` file for your Git repository.

---

## [Our Target App & Setup](#section-5---building-multi-container-applications-with-docker)

### Overview
The target application is a simple **To-Do List** app with the following components:
1. **Frontend**: A React Single Page Application (SPA) for the user interface.
2. **Backend**: A Node.js API for handling CRUD operations.
3. **Database**: A MongoDB instance for storing to-do items.

### Directory Structure
```
todo-app/
├── frontend/          # React SPA
├── backend/           # Node.js API
├── docker-compose.yml # Docker Compose configuration
└── README.md
```

---

## [Dockerizing the MongoDB Service](#section-5---building-multi-container-applications-with-docker)

### Steps to Dockerize MongoDB
1. Create a `Dockerfile` for MongoDB (optional, as we'll use the official image).
2. Use the official MongoDB image in the `docker-compose.yml` file.

### Example `docker-compose.yml` for MongoDB:
```yaml
version: '3.8'
services:
  mongodb:
    image: mongo:6.0
    container_name: todo-mongodb
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```

### Key Points:
- **Ports**: Expose MongoDB on port `27017`.
- **Environment Variables**: Set up authentication for MongoDB.
- **Volumes**: Use a named volume (`mongodb_data`) for data persistence.

---

## [Dockerizing the Node App](#section-5---building-multi-container-applications-with-docker)

### Steps to Dockerize the Node.js Backend
1. Create a `Dockerfile` in the `backend/` directory.
2. Use a multi-stage build to optimize the image size.

### Example `Dockerfile` for Node.js:
```dockerfile
# Stage 1: Build
FROM node:16 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Run
FROM node:16-alpine
WORKDIR /app
COPY --from=build /app .
EXPOSE 3000
CMD ["node", "server.js"]
```

### Example `docker-compose.yml` Addition:
```yaml
backend:
  build: ./backend
  container_name: todo-backend
  ports:
    - "3000:3000"
  environment:
    - MONGO_URI=mongodb://admin:password@mongodb:27017/todo?authSource=admin
  depends_on:
    - mongodb
```

### Key Points:
- **Dependencies**: The backend depends on MongoDB.
- **Environment Variables**: Pass the MongoDB connection string.

---

## [Moving the React SPA into a Container](#section-5---building-multi-container-applications-with-docker)

### Steps to Dockerize the React Frontend
1. Create a `Dockerfile` in the `frontend/` directory.
2. Use a multi-stage build for optimization.

### Example `Dockerfile` for React:
```dockerfile
# Stage 1: Build
FROM node:16 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Example `docker-compose.yml` Addition:
```yaml
frontend:
  build: ./frontend
  container_name: todo-frontend
  ports:
    - "80:80"
  depends_on:
    - backend
```

### Key Points:
- **Static Files**: Serve the built React app using Nginx.
- **Dependencies**: The frontend depends on the backend.

---

## [Adding Docker Networks for Efficient Cross-Container Communication](#section-5---building-multi-container-applications-with-docker)

### Why Use Docker Networks?
- Containers can communicate with each other using service names as hostnames.
- Isolates the application from other Docker networks.

### Example `docker-compose.yml` Network Configuration:
```yaml
networks:
  todo-network:
    driver: bridge

services:
  mongodb:
    networks:
      - todo-network
  backend:
    networks:
      - todo-network
  frontend:
    networks:
      - todo-network
```

### Key Points:
- **Service Discovery**: Use `mongodb`, `backend`, and `frontend` as hostnames.
- **Isolation**: The `todo-network` isolates the app from other Docker networks.

---

## [Fixing MongoDB Authentication Errors](#section-5---building-multi-container-applications-with-docker)

### Common Issues
- Incorrect connection strings.
- Missing or incorrect environment variables.

### Solution
Ensure the connection string in the backend matches the MongoDB credentials:
```yaml
environment:
  - MONGO_URI=mongodb://admin:password@mongodb:27017/todo?authSource=admin
```

---

## [Adding Data Persistence to MongoDB with Volumes](#section-5---building-multi-container-applications-with-docker)

### Why Use Volumes?
- Prevents data loss when containers are restarted or removed.

### Example Volume Configuration:
```yaml
volumes:
  mongodb_data:
```

### Key Points:
- **Named Volume**: Use `mongodb_data` to persist MongoDB data.
- **Data Location**: Data is stored in `/data/db` inside the container.

---

## [Volumes, Bind Mounts & Polishing for the NodeJS Container](#section-5---building-multi-container-applications-with-docker)

### Bind Mounts for Development
- Use bind mounts to sync local files with the container for live updates.

### Example `docker-compose.yml` Addition:
```yaml
backend:
  volumes:
    - ./backend:/app
    - /app/node_modules
```

### Key Points:
- **Development Workflow**: Changes to local files are reflected in the container.
- **Node Modules**: Exclude `node_modules` from the bind mount to avoid conflicts.

---

## [Live Source Code Updates for the React Container (with Bind Mounts)](#section-5---building-multi-container-applications-with-docker)

### Bind Mounts for React Development
- Use bind mounts to enable live updates during development.

### Example `docker-compose.yml` Addition:
```yaml
frontend:
  volumes:
    - ./frontend:/app
    - /app/node_modules
```

### Key Points:
- **Hot Reloading**: Changes to React code are reflected immediately.
- **Node Modules**: Exclude `node_modules` to avoid conflicts.

---

## [Module Summary](#section-5---building-multi-container-applications-with-docker)

This section walked you through the process of building a multi-container application using Docker. You learned how to:
1. Dockerize each component (MongoDB, Node.js, React).
2. Use Docker networks for cross-container communication.
3. Add data persistence with volumes.
4. Enable live updates with bind mounts.

---

