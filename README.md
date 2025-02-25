# Docker & Kubernetes

These are my notes from the course **Docker & Kubernetes: The Practical Guide [2025 Edition]**, by Maximilian Schwarzmüller.

- [Section 1: INTRODUCTION](#section-1---introduction)
- [Section 2: DOCKER IMAGES & CONTAINERS: THE CORE BUILDING BLOCKS](#section-2---docker-images--containers-the-core-building-blocks)

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
- [Sharing Images - Overview]()
- [Pushing Images to DockerHub]()
- [Pulling & Using Shared Images]()
- [Module Summary]()

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

