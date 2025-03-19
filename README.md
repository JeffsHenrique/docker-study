# Docker & Kubernetes

These are my notes from the course **Docker & Kubernetes: The Practical Guide [2025 Edition]**, by Maximilian Schwarzmüller.

- [Section 1: INTRODUCTION](#section-1---introduction)
- [Section 2: DOCKER IMAGES & CONTAINERS: THE CORE BUILDING BLOCKS](#section-2---docker-images--containers-the-core-building-blocks)
- [Section 3: MANAGING DATA & WORKING WITH VOLUMES](#section-3---managing-data--working-with-volumes)
- [Section 4: NETWORKING: (CROSS-)CONTAINER COMMUNICATION](#section-4---networking-cross-container-communication)
- [Section 5: BUILDING MULTI-CONTAINER APPLICATIONS WITH DOCKER](#section-5---building-multi-container-applications-with-docker)
- [Section 6: DOCKER COMPOSE: ELEGANT MULTI-CONTAINER ORCHESTRATION](#section-6---docker-compose-elegant-multi-container-orchestration)
- [Section 7: WORKING WITH "UTILITY CONTAINERS" & EXECUTING COMMANDS IN CONTAINERS](#section-7---working-with-utility-containers--executing-commands-in-containers)
- [Section 8: A MORE COMPLEX SETUP: A LARAVEL & PHP DOCKERIZED PROJECT](#section-8---a-more-complex-setup-a-laravel--php-dockerized-project)
- [Section 9: DEPLOYING DOCKER CONTAINERS](#section-9---deploying-docker-containers)

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

# [Section 6 - DOCKER COMPOSE: ELEGANT MULTI-CONTAINER ORCHESTRATION](#docker--kubernetes)

- [Docker-Compose: What & Why?](#docker-compose-what--why)
- [Creating a Compose File](#creating-a-compose-file)
- [Diving into the Compose File Configuration](#diving-into-the-compose-file-configuration)
- [Installing Docker Compose on Linux](#installing-docker-compose-on-linux)
- [Docker Compose Up & Down](#docker-compose-up--down)
- [Working with Multiple Containers](#working-with-multiple-containers)
- [Adding Another Container](#adding-another-container)
- [Building Images & Understanding Container Names](#building-images--understanding-container-names)
- [Module Summary](#module-summary-1)

## Module Introduction

Docker Compose is a powerful tool that simplifies the process of managing multi-container Docker applications. While Docker itself is excellent for running individual containers, real-world applications often require multiple services (e.g., a web server, a database, and a cache) to work together. Docker Compose allows you to define and manage these services in a single, easy-to-read configuration file. This module will guide you through the fundamentals of Docker Compose, from understanding its purpose to creating and managing multi-container applications.

By the end of this module, you will:
- Understand the purpose and benefits of Docker Compose.
- Learn how to create and configure a `docker-compose.yml` file.
- Install Docker Compose on Linux.
- Use Docker Compose commands to manage your application lifecycle.
- Work with multiple containers and understand how they interact.
- Build custom images and manage container naming.

Let’s dive into the topics!

---

## [Docker-Compose: What & Why?](#section-6---docker-compose-elegant-multi-container-orchestration)

### What is Docker Compose?
Docker Compose is a tool for defining and running multi-container Docker applications. It uses a YAML file (`docker-compose.yml`) to configure the application's services, networks, and volumes. With a single command, you can spin up all the services defined in the file.

### Why Use Docker Compose?
- **Simplifies Multi-Container Management**: Instead of running multiple `docker run` commands, you can start all services with `docker-compose up`.
- **Reproducibility**: The `docker-compose.yml` file ensures that the same setup can be replicated across different environments.
- **Isolation**: Each service runs in its own container, ensuring isolation and reducing conflicts.
- **Networking**: Docker Compose automatically sets up a network for your services, allowing them to communicate seamlessly.

### Example Use Case
Imagine you have a web application that requires:
- A web server (e.g., Nginx)
- A backend API (e.g., Node.js)
- A database (e.g., PostgreSQL)

Instead of manually starting each container and linking them, Docker Compose allows you to define all these services in a single file and start them together.

---

## [Creating a Compose File](#section-6---docker-compose-elegant-multi-container-orchestration)

### What is a Compose File?
A `docker-compose.yml` file is a YAML file that defines the services, networks, and volumes for your application. It is the heart of Docker Compose.

### Basic Structure
```yaml
version: '3.8'  # Specifies the Docker Compose file version
services:       # Defines the services (containers) in your application
  web:
    image: nginx:latest
    ports:
      - "80:80"
  db:
    image: postgres:13
    environment:
      POSTGRES_PASSWORD: example
```

### Key Points:
- `version`: Specifies the Docker Compose file format version.
- `services`: Lists the services (containers) in your application.
- Each service can specify an `image`, `ports`, `environment` variables, and more.

---

## [Diving into the Compose File Configuration](#section-6---docker-compose-elegant-multi-container-orchestration)

### Common Configuration Options
- **image**: Specifies the Docker image to use.
- **ports**: Maps container ports to host ports (e.g., `"80:80"`).
- **environment**: Sets environment variables for the container.
- **volumes**: Mounts directories or files from the host to the container.
- **networks**: Connects the service to a custom network.
- **depends_on**: Specifies dependencies between services.

### Example
```yaml
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    depends_on:
      - db
  db:
    image: postgres:13
    environment:
      POSTGRES_PASSWORD: example
```

---

## [Installing Docker Compose on Linux](#section-6---docker-compose-elegant-multi-container-orchestration)

### Steps to Install Docker Compose on Linux
1. Download the Docker Compose binary:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```
2. Apply executable permissions:
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```
3. Verify the installation:
   ```bash
   docker-compose --version
   ```

---

## [Docker Compose Up & Down](#section-6---docker-compose-elegant-multi-container-orchestration)

### Starting Services
Use the `docker-compose up` command to start all services defined in the `docker-compose.yml` file:
```bash
docker-compose up
```
- Add the `-d` flag to run in detached mode:
  ```bash
  docker-compose up -d
  ```

### Stopping Services
Use the `docker-compose down` command to stop and remove all containers, networks, and volumes:
```bash
docker-compose down
```

---

## [Working with Multiple Containers](#section-6---docker-compose-elegant-multi-container-orchestration)

### Multi-Container Example
```yaml
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  api:
    image: my-node-app:latest
    ports:
      - "3000:3000"
  db:
    image: postgres:13
    environment:
      POSTGRES_PASSWORD: example
```

### Key Points:
- Each service runs in its own container.
- Services can communicate with each other using the service name as the hostname (e.g., `db`).

---

## [Adding Another Container](#section-6---docker-compose-elegant-multi-container-orchestration)

### Adding a Redis Container
```yaml
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  api:
    image: my-node-app:latest
    ports:
      - "3000:3000"
  db:
    image: postgres:13
    environment:
      POSTGRES_PASSWORD: example
  cache:
    image: redis:latest
```

---

## [Building Images & Understanding Container Names](#section-6---docker-compose-elegant-multi-container-orchestration)

### Building Custom Images
You can build custom images using a `Dockerfile` and reference them in your `docker-compose.yml` file:
```yaml
version: '3.8'
services:
  web:
    build: ./web-app  # Path to the Dockerfile
    ports:
      - "80:80"
```

### Container Names
By default, Docker Compose names containers using the format:
```
<project_name>_<service_name>_<index>
```
- `project_name`: The name of the directory containing the `docker-compose.yml` file.
- `service_name`: The name of the service in the `docker-compose.yml` file.
- `index`: A number (starting from 1) for multiple instances of the same service.

---

## [Module Summary](#section-6---docker-compose-elegant-multi-container-orchestration)

### Key Takeaways
- Docker Compose simplifies multi-container application management.
- The `docker-compose.yml` file is used to define services, networks, and volumes.
- Use `docker-compose up` to start services and `docker-compose down` to stop them.
- Services can communicate with each other using service names.
- You can build custom images and manage container names.

### Next Steps
- Practice creating `docker-compose.yml` files for different applications.
- Experiment with advanced features like volumes, networks, and environment variables.

---

# [Section 7 - WORKING WITH "UTILITY CONTAINERS" & EXECUTING COMMANDS IN CONTAINERS](#docker--kubernetes)

- [Utility Containers: Why would you use them?](#utility-containers-why-would-you-use-them)
- [Different Ways of Running Commands in Containers](#different-ways-of-running-commands-in-containers)
- [Building a First Utility Container](#building-a-first-utility-container)
- [Utilizing ENTRYPOINT](#utilizing-entrypoint)
- [Using Docker Compose](#using-docker-compose)
- [Utility Containers, Permissions & Linux](#utility-containers-permissions--linux)
- [Module Summary](#module-summary-2)

## Module Introduction & What are "Utility Containers"?

### Module Introduction

In this module, we explore the concept of **Utility Containers**—specialized Docker containers designed to perform specific tasks or provide tools without running a long-lived service. These containers are often used for development, debugging, or running one-off commands in an isolated environment. 

Utility containers are lightweight, portable, and ensure consistency across different environments. They are particularly useful for tasks like running scripts, debugging applications, or providing tools (e.g., linters, compilers, or database clients) without requiring installation on the host machine.

---

### What are Utility Containers?

Utility Containers are Docker containers that are designed to execute specific commands or provide tools rather than running a persistent service (like a web server or database). They are often used for:

- Running one-off commands (e.g., database migrations, linting, or testing).
- Providing a consistent environment for development tasks.
- Debugging applications in an isolated environment.
- Avoiding the need to install tools or dependencies on the host machine.

Unlike service containers, utility containers are typically short-lived and terminate after completing their task.

---

## [Utility Containers: Why would you use them?](#section-7---working-with-utility-containers--executing-commands-in-containers)

**Key Points:**
- **Consistency:** Utility containers ensure that the same tools and environment are used across different machines or environments.
- **Isolation:** They provide an isolated environment for running commands, avoiding conflicts with the host system.
- **Portability:** Utility containers can be shared and reused across teams or projects.
- **No Host Dependency:** You don’t need to install tools or dependencies on your local machine.

**Example Use Cases:**
- Running a database migration script.
- Linting or formatting code.
- Running tests in a specific environment.
- Debugging an application with specific tools.

---

## [Different Ways of Running Commands in Containers](#section-7---working-with-utility-containers--executing-commands-in-containers)

**Key Points:**
- **Interactive Mode (`-it`):** Run a command interactively in a container.
  ```bash
  docker run -it <image_name> <command>
  ```
  Example:
  ```bash
  docker run -it ubuntu bash
  ```

- **Detached Mode (`-d`):** Run a container in the background.
  ```bash
  docker run -d <image_name> <command>
  ```

- **One-Off Commands:** Run a command and exit immediately.
  ```bash
  docker run <image_name> <command>
  ```
  Example:
  ```bash
  docker run alpine echo "Hello, World!"
  ```

- **Exec into a Running Container:** Execute a command in a running container.
  ```bash
  docker exec -it <container_id> <command>
  ```
  Example:
  ```bash
  docker exec -it my_container bash
  ```

---

## [Building a First Utility Container](#section-7---working-with-utility-containers--executing-commands-in-containers)

**Key Points:**
- Create a `Dockerfile` to define the utility container.
- Use a lightweight base image (e.g., `alpine` or `ubuntu`).
- Install necessary tools or dependencies.
- Define the default command using `CMD` or `ENTRYPOINT`.

**Example:**
```Dockerfile
# Dockerfile
FROM alpine:latest
RUN apk add --no-cache curl
CMD ["curl", "--version"]
```

**Build and Run:**
```bash
docker build -t my-utility-container .
docker run my-utility-container
```

---

## [Utilizing ENTRYPOINT](#section-7---working-with-utility-containers--executing-commands-in-containers)

**Key Points:**
- `ENTRYPOINT` defines the main command to run when the container starts.
- Arguments passed to `docker run` are appended to the `ENTRYPOINT` command.
- Useful for creating reusable utility containers.

**Example:**
```Dockerfile
# Dockerfile
FROM alpine:latest
RUN apk add --no-cache curl
ENTRYPOINT ["curl"]
```

**Run with Arguments:**
```bash
docker run my-utility-container https://example.com
```

---

## [Using Docker Compose](#section-7---working-with-utility-containers--executing-commands-in-containers)

**Key Points:**
- Docker Compose simplifies running multi-container applications.
- Define utility containers in a `docker-compose.yml` file.
- Use `docker-compose run` to execute commands in a utility container.

**Example:**
```yaml
# docker-compose.yml
version: '3'
services:
  curl-utility:
    image: alpine
    command: curl https://example.com
```

**Run with Docker Compose:**
```bash
docker-compose run curl-utility
```

---

## [Utility Containers, Permissions & Linux](#section-7---working-with-utility-containers--executing-commands-in-containers)

**Key Points:**
- Utility containers often need to interact with the host system (e.g., files or directories).
- Use Docker volumes to share files between the host and container.
- Be mindful of file permissions, especially when running as a non-root user.

**Example:**
```bash
docker run -v $(pwd):/app -w /app my-utility-container <command>
```

**Permissions:**
- Run the container as a specific user to avoid permission issues.
  ```Dockerfile
  # Dockerfile
  FROM alpine:latest
  RUN adduser -D myuser
  USER myuser
  ```


**Q&A Section**
This is truly an awesome course Max! Well done!

I wanted to point out that on a Linux system, the Utility Container idea doesn't quite work as you describe it.  In Linux, by default Docker runs as the "Root" user, so when we do a lot of the things that you are advocating for with Utility Containers the files that get written to the Bind Mount have ownership and permissions of the Linux Root user.  (On MacOS and Windows10, since Docker is being used from within a VM, the user mappings all happen automatically due to NFS mounts.)

So, for example on Linux, if I do the following (as you described in the course):

Dockerfile

```Dockerfile
FROM node:14-slim
WORKDIR /app
```

```bash
docker build -t node-util:perm .
```

```bash
docker run -it --rm -v $(pwd):/app node-util:perm npm init
```

```bash
ls -la
```

total 16

drwxr-xr-x  3 scott scott 4096 Oct 31 16:16 ./

drwxr-xr-x 12 scott scott 4096 Oct 31 16:14 ../

drwxr-xr-x  7 scott scott 4096 Oct 31 16:14 .git/

-rw-r--r--  1 root  root   202 Oct 31 16:16 package.json

You'll see that the ownership and permissions for the package.json file are "root".  But, regardless of the file that is being written to the Bind Mounted volume from commands emanating from within the docker container, e.g. "npm install", all come out with "Root" ownership.

-------

**Solution 1:  Use  predefined "node" user (if you're lucky)**

There is a lot of discussion out there in the docker community (devops) about security around running Docker as a non-privileged user (which might be a good topic for you to cover as a video lecture - or maybe you have; I haven't completed the course yet).  The Official Node.js Docker Container provides such a user that they call "node". 

https://github.com/nodejs/docker-node/blob/master/Dockerfile-slim.template

```Dockerfile
FROM debian:name-slim
RUN groupadd --gid 1000 node \
         && useradd --uid 1000 --gid node --shell /bin/bash --create-home node
```

Luckily enough for me on my local Linux system, my "scott" uid:gid is also 1000:1000 so, this happens to map nicely to the "node" user defined within the Official Node Docker Image.

So, in my case of using the Official Node Docker Container, all I need to do is make sure I specify that I want the container to run as a non-Root user that they make available.  To do that, I just add:

```Dockerfile
FROM node:14-slim
USER node
WORKDIR /app
```

If I rebuild my Utility Container in the normal way and re-run "npm init", the ownership of the package.json file is written as if "scott" wrote the file.

```bash
ls -la
```

total 12

drwxr-xr-x  2 scott scott 4096 Oct 31 16:23 ./

drwxr-xr-x 13 scott scott 4096 Oct 31 16:23 ../

-rw-r--r--  1 scott scott 204 Oct 31 16:23 package.json

------------

Solution 2:  Remove the predefined "node" user and add yourself as the user

However, if the Linux user that you are running as is not lucky to be mapped to 1000:1000, then you can modify the Utility Container Dockerfile to remove the predefined "node" user and add yourself as the user that the container will run as:

-------

```Dockerfile
FROM node:14-slim

RUN userdel -r node

ARG USER_ID

ARG GROUP_ID

RUN addgroup --gid $GROUP_ID user

RUN adduser --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID user

USER user

WORKDIR /app
```
-------

And then build the Docker image using the following (which also gives you a nice use of ARG):

```bash
docker build -t node-util:cliuser --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g) .
```

And finally running it with:

```bash
docker run -it --rm -v $(pwd):/app node-util:cliuser npm init
```

```bash
ls -la
```

total 12

drwxr-xr-x  2 scott scott 4096 Oct 31 16:54 ./

drwxr-xr-x 13 scott scott 4096 Oct 31 16:23 ../

-rw-r--r--  1 scott scott  202 Oct 31 16:54 package.json



Reference to Solution 2 above: https://vsupalov.com/docker-shared-permissions/



Keep in mind that this image will not be portable, but for the purpose of the Utility Containers like this, I don't think this is an issue at all for these "Utility Containers"

---

## [Module Summary](#section-7---working-with-utility-containers--executing-commands-in-containers)

**Key Takeaways:**
- Utility containers are designed for running specific tasks or providing tools.
- They ensure consistency, isolation, and portability.
- Use `docker run`, `docker exec`, or Docker Compose to interact with utility containers.
- Leverage `ENTRYPOINT` for reusable utility containers.
- Be mindful of permissions when sharing files between the host and container.

**Next Steps:**
- Practice building and running utility containers for common tasks (e.g., linting, testing, or debugging).
- Explore advanced use cases, such as integrating utility containers into CI/CD pipelines.

---

# [Section 8 - A MORE COMPLEX SETUP: A LARAVEL & PHP DOCKERIZED PROJECT](#docker--kubernetes)

This module is to practice by dockerizing a laravel & php project. [Here is the folder containing the project.](https://github.com/JeffsHenrique/Docker-Laravel-Setup/tree/master/Docker%20Laravel)

# [Section 9 - DEPLOYING DOCKER CONTAINERS](#docker--kubernetes)

- [From development to production](#from-development-to-production)
- [Deployment process & providers](#deployment-process--providers)
- [Getting Started With an Example](#getting-started-with-an-example)
- [Bind Mounts in Production](#bind-mounts-in-production)
- [Introducing AWS & EC2](#introducing-aws--ec2)
- [Connecting to an EC2 instance](#connecting-to-an-ec2-instance)
- [Important: Installing Docker on a Virtual Machine](#important-installing-docker-on-a-virtual-machine)
- [Installing docker on a Virtual Machine](#installing-docker-on-a-virtual-machine)
- [Installing Docker on Linux in General](#installing-docker-on-linux-in-general)
- [Pushing our local image to the cloud](#pushing-our-local-image-to-the-cloud)
- [Running & Publishing the App (on EC2)](#running--publishing-the-app-on-ec2)
- [Managing & updating the container / image](#managing--updating-the-container--image)
- [Disadvantages of our current approach](#disadvantages-of-our-current-approach)
- [From manual deployment to managed services](#from-manual-deployment-to-managed-services)
- [Deploying with AWS ECS: A managed Docker container service](#deploying-with-aws-ecs-a-managed-docker-container-service)
- [More on AWS](#more-on-aws)
- [Updating managed containers](#updating-managed-containers)
- [Preparing a multi-container App](#preparing-a-multi-container-app)
- [Configuring the nodeJS backend container](#configuring-the-nodejs-backend-container)
- [Deploying a second container & a load balancer](#deploying-a-second-container--a-load-balancer)
- [Using a load balancer for a stable domain](#using-a-load-balancer-for-a-stable-domain)
- [Using EFS Volumes with ECS](#using-efs-volumes-with-ecs)
- [Our current architecture](#our-current-architecture)
- [Databases & Containers: An important consideration](#Databases--containers-an-important-consideration)
- [Moving to MongoDB Atlas](#moving-to-mongodb-atlas)
- [Using MongoDB Atlas in production](#using-mongodb-atlas-in-production)
- [Our updated & target architecture](#our-updated--target-architecture)
- [Understanding a common problem](#understanding-a-common-problem)
- [Creating a "build-only" container](#creating-a-build-only-container)
- [Introducing Multi-stage builds](#introducing-multi-stage-builds)
- [Building a multi-stage image](#building-a-multi-stage-image)
- [Deploying a Standalone frontend app](#deploying-a-standalone-frontend-app)
- [Development vs production: Differences](#development-vs-production-differences)
- [Understanding multi-stage build targets](#understanding-multi-stage-build-targets)
- [Beyond AWS](#beyond-aws)
- [Module Summary](#module-summary-3)

## Module Introduction

In this module, we transition from developing Docker containers locally to deploying them in production environments. The goal is to understand the entire lifecycle of a Dockerized application, from development to deployment, and how to manage it effectively in real-world scenarios.

You'll learn how to:
- Move a Dockerized application from development to production.
- Work with cloud providers like AWS to deploy containers.
- Use managed services like AWS ECS (Elastic Container Service) to simplify deployment.
- Handle multi-container applications, load balancers, and persistent storage.
- Optimize Docker images for production using multi-stage builds.
- Address common challenges like database management and container updates.

By the end of this module, you'll have a solid understanding of how to deploy, manage, and scale Docker containers in production environments, using both manual and managed approaches.

---

## [From development to production](#section-9---deploying-docker-containers)

- **Explanation**: Transitioning from a local development environment to a production environment involves several considerations, such as security, performance, and scalability.
- **Key Points**:
  - Development environments are often less strict about resource usage and security.
  - Production environments require optimized images, secure configurations, and proper resource management.
  - Example: A Node.js app running locally with a bind mount for live code updates won't work the same way in production.

---

## [Deployment process & providers](#section-9---deploying-docker-containers)

- **Explanation**: The deployment process involves packaging your application, pushing it to a registry, and running it on a server or cloud provider.
- **Key Points**:
  - Common providers: AWS, Google Cloud Platform (GCP), Azure, DigitalOcean, etc.
  - Steps:
    1. Build the Docker image.
    2. Push the image to a container registry (e.g., Docker Hub, AWS ECR).
    3. Pull and run the image on a production server.
  - Example: Deploying a Python Flask app to AWS EC2.

---

## [Getting Started With an Example](#section-9---deploying-docker-containers)

- **Explanation**: We'll use a simple application (e.g., a Node.js app) to demonstrate the deployment process.
- **Key Points**:
  - Create a Dockerfile for the app.
  - Build and run the app locally.
  - Prepare the app for production (e.g., remove bind mounts, optimize the Dockerfile).
  - Example: A "Hello World" Node.js app.

---

## [Bind Mounts in Production](#section-9---deploying-docker-containers)

- **Explanation**: Bind mounts are useful in development for live code updates but are not recommended in production.
- **Key Points**:
  - Bind mounts tie the container's filesystem to the host, which can be risky in production.
  - Use volumes or copy files into the image for production.
  - Example: Replace `-v $(pwd):/app` with `COPY . /app` in the Dockerfile.

---

## [Introducing AWS & EC2](#section-9---deploying-docker-containers)

- **Explanation**: AWS EC2 (Elastic Compute Cloud) is a popular service for running virtual machines in the cloud.
- **Key Points**:
  - EC2 instances are virtual servers that can run Docker containers.
  - Use EC2 for full control over the deployment environment.
  - Example: Launching an EC2 instance with Ubuntu.

---

## [Connecting to an EC2 instance](#section-9---deploying-docker-containers)

- **Explanation**: Use SSH to connect to your EC2 instance and manage it.
- **Key Points**:
  - Generate a key pair for secure access.
  - Use `ssh -i key.pem ubuntu@<public-ip>` to connect.
  - Example: Connecting to an EC2 instance and installing Docker.

---

## [Important: Installing Docker on a Virtual Machine](#section-9---deploying-docker-containers)

In the next lecture, we'll install Docker on a virtual EC2 instance.

Please note that the following command (which is used in the next lecture) will unfortunately not work anymore:

amazon-linux-extras install docker
Instead, use this approach / these commands:

sudo yum update -y
sudo yum -y install docker
 
sudo service docker start
 
sudo usermod -a -G docker ec2-user
Make sure to log out + back in after running these commands.

Once you logged back in, run this command:

sudo systemctl enable docker
Thereafter, you can check whether Docker is available by running:

docker version
Also see: https://stackoverflow.com/questions/53918841/how-to-install-docker-on-amazon-linux2/61708497#61708497

## [Installing docker on a Virtual Machine](#section-9---deploying-docker-containers)

- **Explanation**: Docker can be installed on any Linux-based virtual machine.
- **Key Points**:
  - Use the official Docker installation script:
    ```bash
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    ```
  - Example: Installing Docker on an Ubuntu EC2 instance.

---

## [Installing Docker on Linux in General](#section-9---deploying-docker-containers)

- **Explanation**: The process of installing Docker on Linux is similar across distributions.
- **Key Points**:
  - Follow the official Docker documentation for your Linux distribution.
  - Example: Installing Docker on CentOS or Debian.

---

## [Pushing our local image to the cloud](#section-9---deploying-docker-containers)

- **Explanation**: Push your Docker image to a container registry for deployment.
- **Key Points**:
  - Tag the image: `docker tag my-app:latest my-dockerhub-username/my-app:latest`.
  - Push the image: `docker push my-dockerhub-username/my-app:latest`.
  - Example: Pushing a Node.js app to Docker Hub.

---

## [Running & Publishing the App (on EC2)](#section-9---deploying-docker-containers)

- **Explanation**: Pull and run the Docker image on an EC2 instance.
- **Key Points**:
  - Pull the image: `docker pull my-dockerhub-username/my-app:latest`.
  - Run the container: `docker run -d -p 80:3000 my-dockerhub-username/my-app`.
  - Example: Running a Node.js app on EC2.

---

## [Managing & updating the container / image](#section-9---deploying-docker-containers)

- **Explanation**: Update your app by rebuilding the image and redeploying the container.
- **Key Points**:
  - Rebuild the image: `docker build -t my-app:latest .`.
  - Push the updated image: `docker push my-dockerhub-username/my-app:latest`.
  - Pull and restart the container on EC2.
  - Example: Updating a Node.js app with a new feature.

---

## [Disadvantages of our current approach](#section-9---deploying-docker-containers)

- **Explanation**: Manual deployment has limitations, such as lack of scalability and high maintenance.
- **Key Points**:
  - No automatic scaling.
  - Manual updates are time-consuming.
  - Example: Managing multiple EC2 instances for a high-traffic app.

---

## [From manual deployment to managed services](#section-9---deploying-docker-containers)

- **Explanation**: Managed services like AWS ECS simplify deployment and scaling.
- **Key Points**:
  - ECS handles container orchestration, scaling, and load balancing.
  - Example: Migrating from EC2 to ECS.

---

## [Deploying with AWS ECS: A managed Docker container service](#section-9---deploying-docker-containers)

### **Deploying Docker Containers with AWS ECS**

#### **1. What is AWS ECS?**
- **AWS ECS (Elastic Container Service)** is a fully managed container orchestration service provided by Amazon Web Services (AWS).
- It allows you to run, stop, and manage Docker containers on a cluster of EC2 instances or using AWS Fargate (serverless compute for containers).
- ECS integrates with other AWS services like Elastic Load Balancing (ELB), Identity and Access Management (IAM), and CloudWatch for monitoring.

#### **2. Key Concepts in AWS ECS**
- **Cluster**: A logical grouping of EC2 instances or Fargate tasks where containers are deployed.
- **Task Definition**: A blueprint for your application, which defines parameters like Docker image, CPU/memory requirements, networking, and environment variables.
- **Service**: Ensures that a specified number of tasks (containers) are running and can handle updates, scaling, and load balancing.
- **Container Instance**: An EC2 instance that is part of an ECS cluster and runs Docker containers.
- **Task**: An instantiation of a Task Definition, representing a running Docker container.
- **Fargate**: A serverless compute engine for containers that eliminates the need to manage EC2 instances.

#### **3. Steps to Deploy Docker Containers with AWS ECS**

##### **Step 1: Prepare Your Docker Image**
- Build your Docker image locally and test it.
- Push the Docker image to a container registry like **Amazon ECR (Elastic Container Registry)** or Docker Hub.
  ```bash
  docker build -t my-app .
  docker tag my-app:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:latest
  docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:latest
  ```

##### **Step 2: Create an ECS Cluster**
- Go to the AWS Management Console > ECS > Clusters > Create Cluster.
- Choose between:
  - **EC2 Launch Type**: Manages EC2 instances for running containers.
  - **Fargate Launch Type**: Serverless, no need to manage EC2 instances.
- Configure networking (VPC, subnets, security groups).

##### **Step 3: Define a Task Definition**
- A Task Definition is a JSON file that describes how your container should run.
- Key parameters:
  - **Container Image**: Specify the Docker image URI (e.g., from ECR).
  - **CPU and Memory**: Allocate resources for the container.
  - **Port Mappings**: Map container ports to host ports.
  - **Environment Variables**: Pass configuration to the container.
  - **Logging**: Configure logging to CloudWatch or other destinations.
- Example Task Definition:
  ```json
  {
    "family": "my-app-task",
    "containerDefinitions": [
      {
        "name": "my-app-container",
        "image": "<aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:latest",
        "memory": 512,
        "cpu": 256,
        "essential": true,
        "portMappings": [
          {
            "containerPort": 80,
            "hostPort": 80
          }
        ]
      }
    ]
  }
  ```

##### **Step 4: Create an ECS Service**
- A Service ensures that a specified number of tasks are running and can handle updates and scaling.
- Configure:
  - **Task Definition**: Link the Task Definition created earlier.
  - **Load Balancer**: Attach an Application Load Balancer (ALB) or Network Load Balancer (NLB) if needed.
  - **Desired Count**: Number of tasks to run.
  - **Auto Scaling**: Configure scaling policies based on CPU/memory usage or custom CloudWatch metrics.

##### **Step 5: Deploy and Monitor**
- Deploy the service and monitor its status in the ECS console.
- Use **CloudWatch** to monitor logs and metrics.
- Use **ECS Exec** to debug containers by running commands inside them.

#### **4. AWS Fargate vs EC2 Launch Types**
- **Fargate**:
  - Serverless, no need to manage EC2 instances.
  - Pay for the resources (CPU/memory) used by your containers.
  - Ideal for small to medium workloads or when you don’t want to manage infrastructure.
- **EC2 Launch Type**:
  - You manage the EC2 instances in the cluster.
  - More control over the underlying infrastructure.
  - Ideal for large workloads or when you need custom configurations.

#### **5. Best Practices for ECS Deployment**
- **Use IAM Roles**: Assign IAM roles to ECS tasks for secure access to AWS resources.
- **Enable Logging**: Use CloudWatch Logs to capture container logs for debugging and monitoring.
- **Use Secrets Manager**: Store sensitive information like API keys or database credentials in AWS Secrets Manager and inject them into containers.
- **Auto Scaling**: Configure auto-scaling for your services to handle traffic spikes.
- **Health Checks**: Implement health checks for your containers to ensure they are running correctly.

#### **6. Common AWS ECS Commands**
- List clusters:
  ```bash
  aws ecs list-clusters
  ```
- Describe a cluster:
  ```bash
  aws ecs describe-clusters --cluster <cluster-name>
  ```
- List tasks in a cluster:
  ```bash
  aws ecs list-tasks --cluster <cluster-name>
  ```
- Stop a task:
  ```bash
  aws ecs stop-task --cluster <cluster-name> --task <task-id>
  ```

#### **7. Troubleshooting ECS Deployments**
- **Check Task Status**: Use the ECS console or CLI to check the status of tasks.
- **View Logs**: Use CloudWatch Logs to view container logs.
- **Inspect Containers**: Use `ECS Exec` to run commands inside a running container.
- **Check IAM Permissions**: Ensure the task role has the necessary permissions to access AWS resources.

#### **8. Integration with Other AWS Services**
- **Elastic Load Balancing (ELB)**: Distribute traffic across containers.
- **Route 53**: Route traffic to your ECS services.
- **CloudWatch**: Monitor and log container metrics.
- **Secrets Manager**: Securely manage secrets for your containers.

---

### **Summary**
AWS ECS is a powerful service for deploying and managing Docker containers at scale. By understanding its core components (clusters, tasks, services) and integrating it with other AWS services, you can build robust and scalable containerized applications. Whether you choose EC2 or Fargate depends on your workload and infrastructure preferences.

---

## [More on AWS](#section-9---deploying-docker-containers)

- **Explanation**: Explore additional AWS services like ECR (Elastic Container Registry) and CloudWatch.
- **Key Points**:
  - ECR: A private Docker registry for storing images.
  - CloudWatch: Monitor container logs and metrics.
  - Example: Using ECR to store images and CloudWatch to monitor app performance.

---

## [Updating managed containers](#section-9---deploying-docker-containers)

- **Explanation**: Update containers in a managed service like ECS.
- **Key Points**:
  - Update the task definition with a new image.
  - Redeploy the service.
  - Example: Updating a Node.js app on ECS.

---

## [Preparing a multi-container App](#section-9---deploying-docker-containers)

- **Explanation**: Many apps consist of multiple containers (e.g., frontend, backend, database).
- **Key Points**:
  - Use Docker Compose for local development.
  - Deploy each container as a separate service in production.
  - Example: A Node.js backend with a React frontend.

---

## [Configuring the nodeJS backend container](#section-9---deploying-docker-containers)

- **Explanation**: Configure the backend container for production.
- **Key Points**:
  - Set environment variables (e.g., database credentials).
  - Optimize the Dockerfile (e.g., multi-stage builds).
  - Example: Configuring a Node.js app to connect to MongoDB.

---

## [Deploying a second container & a load balancer](#section-9---deploying-docker-containers)

- **Explanation**: Deploy multiple containers and use a load balancer for traffic distribution.
- **Key Points**:
  - Use AWS Application Load Balancer (ALB) to route traffic.
  - Example: Deploying a React frontend and Node.js backend with an ALB.

---

## [Using a load balancer for a stable domain](#section-9---deploying-docker-containers)

- **Explanation**: A load balancer provides a stable domain name and handles traffic distribution.
- **Key Points**:
  - Configure DNS for the load balancer.
  - Example: Mapping `my-app.com` to an ALB.

---

## [Using EFS Volumes with ECS](#section-9---deploying-docker-containers)

- **Explanation**: EFS (Elastic File System) provides persistent storage for containers.
- **Key Points**:
  - Mount EFS volumes to containers for shared storage.
  - Example: Storing user uploads in an EFS volume.

---

## [Our current architecture](#section-9---deploying-docker-containers)

- **Explanation**: Review the architecture of the deployed app.
- **Key Points**:
  - Frontend: React app.
  - Backend: Node.js app.
  - Database: MongoDB.
  - Example: Diagram of the architecture.

---

## [Databases & Containers: An important consideration](#section-9---deploying-docker-containers)

- **Explanation**: Databases should not be run in containers in production.
- **Key Points**:
  - Use managed database services (e.g., AWS RDS, MongoDB Atlas).
  - Example: Migrating from a containerized MongoDB to MongoDB Atlas.

---

## [Moving to MongoDB Atlas](#section-9---deploying-docker-containers)

- **Explanation**: MongoDB Atlas is a managed MongoDB service.
- **Key Points**:
  - Create a cluster on MongoDB Atlas.
  - Update the app to use the Atlas connection string.
  - Example: Connecting a Node.js app to MongoDB Atlas.

---

## [Using MongoDB Atlas in production](#section-9---deploying-docker-containers)

- **Explanation**: Best practices for using MongoDB Atlas in production.
- **Key Points**:
  - Enable backups and monitoring.
  - Use VPC peering for secure connections.
  - Example: Configuring a production-ready MongoDB Atlas cluster.

---

## [Our updated & target architecture](#section-9---deploying-docker-containers)

- **Explanation**: Final architecture with all components in place.
- **Key Points**:
  - Frontend: React app on ECS.
  - Backend: Node.js app on ECS.
  - Database: MongoDB Atlas.
  - Example: Updated architecture diagram.

---

## [Understanding a common problem](#section-9---deploying-docker-containers)

- **Explanation**: Large Docker images can slow down deployment.
- **Key Points**:
  - Use multi-stage builds to reduce image size.
  - Example: Optimizing a Node.js app's Dockerfile.

---

## [Creating a "build-only" container](#section-9---deploying-docker-containers)

- **Explanation**: Use a separate container for building the app.
- **Key Points**:
  - Build the app in one container and copy the output to a smaller runtime container.
  - Example: Building a React app in a Node.js container and serving it with Nginx.

---

## [Introducing Multi-stage builds](#section-9---deploying-docker-containers)

- **Explanation**: Multi-stage builds allow you to use multiple `FROM` statements in a Dockerfile.
- **Key Points**:
  - Use one stage for building and another for running.
  - Example: A multi-stage Dockerfile for a Node.js app.

---

## [Building a multi-stage image](#section-9---deploying-docker-containers)

- **Explanation**: Build and optimize a Docker image using multi-stage builds.
- **Key Points**:
  - Reduce image size by excluding build dependencies.
  - Example: Building a Node.js app with a multi-stage Dockerfile.

---

## [Deploying a Standalone frontend app](#section-9---deploying-docker-containers)

- **Explanation**: Deploy a frontend app separately from the backend.
- **Key Points**:
  - Use a static hosting service (e.g., AWS S3, Netlify).
  - Example: Deploying a React app to AWS S3.

---

## [Development vs production: Differences](#section-9---deploying-docker-containers)

- **Explanation**: Key differences between development and production environments.
- **Key Points**:
  - Development: Bind mounts, debug tools, etc.
  - Production: Optimized images, secure configurations, etc.
  - Example: Comparing a development and production Dockerfile.

---

## [Understanding multi-stage build targets](#section-9---deploying-docker-containers)

- **Explanation**: Use different build targets for development and production.
- **Key Points**:
  - Define multiple stages in the Dockerfile.
  - Example: A Dockerfile with `dev` and `prod` targets.

---

## [Beyond AWS](#section-9---deploying-docker-containers)

- **Explanation**: Explore other deployment options (e.g., Kubernetes, GCP, Azure).
- **Key Points**:
  - Kubernetes: A powerful container orchestration platform.
  - GCP: Google Cloud Run, GKE.
  - Example: Deploying a Docker app on Kubernetes.

---

## [Module Summary](#section-9---deploying-docker-containers)

- **Explanation**: Recap of the module's key takeaways.
- **Key Points**:
  - Learned how to deploy Docker containers in production.
  - Explored AWS services like EC2, ECS, and ECR.
  - Understood the importance of multi-stage builds and managed services.
  - Example: Summarizing the deployment process for a Node.js app.

---

