# 📅 Day 4 – 01/04/2025

## 🚀 Topics Covered
- Launching EC2 Instances
- Using PuTTY for SSH access
- Docker installation and status check
- Environments in DevOps (Dev, Testing, UAT, Production)
- Dockerfile instructions explained
- Docker commands: image, container, run, exec, etc.
- Detached containers and exposing ports
- Docker Hub: Login and pushing images

---

## ☁️ Launch EC2 Instance & Connect via PuTTY

1. Use AWS EC2 Console to launch an Amazon Linux instance.
2. Download `.pem` file and convert it to `.ppk` using PuTTYgen.
3. Open PuTTY → Provide public IP → Navigate to SSH → Auth → Load `.ppk` file.
4. Connect as root:

### 🐳 Docker Installation on Amazon Linux
    
    sudo su  
    yum install docker -y   
    service docker status  
    service docker start  
    docker --version

## 🌐 Environments in DevOps

| Environment | Description |
|-------------|-------------|
| **Development** | Where software is developed and minimal functionality is tested. |
| **Testing** | QA environment where all functional/non-functional, performance, and load testing is done. |
| **UAT** | User Acceptance Testing – Show a prototype to the customer before release. |
| **Production** | Live environment where the application is accessible to end users. |


## 📦 What is a Container?

A lightweight virtual environment where applications run in isolation.  

#### 🛠️ Dockerfile – Key Instructions
| Instruction   | Purpose                                                                 |
|---------------|-------------------------------------------------------------------------|
| `FROM`        | Specifies the base image. Required as the first line.                   |
| `COPY`        | Copies files/folders from host to container.                            |
| `ADD`         | Same as COPY + download from URL or extract tar files.                  |
| `RUN`         | Executes commands to install dependencies inside the image.             |
| `CMD`         | Defines default command to run in the container.                        |
| `ENTRYPOINT`  | Same as CMD but doesn't allow runtime arguments.                        |
| `EXPOSE`      | Opens a port on the container.                                          |
| `ENV`         | Sets environment variables.                                             |
| `USER`        | Creates a user inside the container.                                    |


    📝 Docker images = templates with app + config + dependencies
    📤 Docker Hub = Registry to push/pull Docker images

### 🧪 Docker Commands – Basics
```bash
# View all containers (including stopped ones)
docker ps -a

# Create a container (but not start)
docker create -it --name webserver amazonlinux /bin/bash

# Start the container
docker start webserver

# Access container
docker exec -it webserver /bin/bash

# Run container in one go (create + start + attach)
docker run -it --name sample ubuntu /bin/bash

# Exit from container
exit

# Detached Mode (Daemon - runs in background)
docker run -td --name web-app -p 3002:3000 node-app

# List all Docker images
docker images

# Inspect image details/ Detailed image/container info
docker inspect <image_name_or_id>

# Docker stats/ Monitor usage stats
docker stats
```
   > Use CTRL + P + Q to detach from running container without stopping it.

### 📥 Docker Hub

Docker Hub is a cloud-based registry to store Docker images.

Create account: https://hub.docker.com

Login via CLI:
```bash
# Login to Docker Hub
docker login

# Push image to Docker Hub
docker push <image_name> <yourusername>/<repo-name>

# View all images
docker images
```
💡 Public IP + Port (exposed) = Access your deployed app in browser
### 🛠 Troubleshooting

   > If PuTTY session is inactive:
    → Right-click → "Restart Session" and reconnect with .ppk credentials.