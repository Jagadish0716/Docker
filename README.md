# Docker
this repo will be used to learn and work with docker.

### What is Docker ?

Docker is a containerization platform that provides easy way to containerize your applications, which means, using Docker you can build container images, run the images to create containers and also push these containers to container regestries such as DockerHub, Quay.io and so on.

In simple words, you can understand as `containerization is a concept or technology` and `Docker Implements Containerization`.

### Docker Architecture ?
The above picture, clearly indicates that Docker Deamon is brain of Docker. If Docker Deamon is killed, stops working for some reasons, Docker is brain dead :p (sarcasm intended).

### Docker LifeCycle 
![image](https://github.com/user-attachments/assets/2eb7a27a-ddd3-4cd4-be58-f1e8a416d8ec)

We can use the above Image as reference to understand the lifecycle of Docker.

There are three important things,

1. docker build -> builds docker images from Dockerfile
2. docker run   -> runs container from docker images
3. docker push  -> push the container image to public/private regestries to share the docker images.
   ![image](https://github.com/user-attachments/assets/bf4d1895-50ee-43bc-b0fc-6a9714a5db42)

### Understanding the terminology (Inspired from Docker Docs)
#### Docker daemon
The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

#### Docker client
The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

#### Docker Desktop
Docker Desktop is an easy-to-install application for your Mac, Windows or Linux environment that enables you to build and share containerized applications and microservices. Docker Desktop includes the Docker daemon (dockerd), the Docker client (docker), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper. For more information, see Docker Desktop.

#### Docker registries
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry.

When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry. Docker objects

When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

#### Dockerfile
Dockerfile is a file where you provide the steps to build your Docker Image.

#### Images
An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

## INSTALL DOCKER

A very detailed instructions to install Docker are provide in the below link
https://docs.docker.com/get-docker/

For Demo, 
You can create an Ubuntu EC2 Instance on AWS and run the below commands to install docker.

### Steps for Installing Docker on Ubuntu
#### Step 1: Update Software Repositories using the following command
```
sudo apt update
```
#### Step 2: Install Docker using the following command
```
sudo apt install docker.io -y
```
#### Step 3: Enable and start the docker service by using the following commands.
```
sudo systemctl enable docker --now
```
#### Step 4: Check Docker Version.
```
docker --version
```

## Executing the Docker Command Without Sudo
We will get a permission denied error as a regular user (ubuntu) doesn’t have permission to execute docker commands. Now we need to add the the user to the required group.

#### Step 1: So we need to add an Ubuntu user to the docker group. 
```
sudo usermod -aG docker ubuntu
```
The following command helps in knowing whether current add user assigned to docker group or not:
```
getent group docker
```
Refresh the group permission to use updated one with running following command:
```
newgrp docker
```
![image](https://github.com/user-attachments/assets/738a4a97-6086-41a1-9547-c7ac234a0c02)

#### Step 2: Restart the docker daemon which is already running. After restarting only the changes will comes into effect.
```
sudo service docker restart
```
#### Step 2: Step 3: Leave the current SSH terminal and re-login with SSH. then carry out.


