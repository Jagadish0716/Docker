# Docker
this repo will be used to learn and work on docker.

### What is Docker ?

Docker is a containerization platform that provides easy way to containerize your applications, which means, using Docker you can build container images, run the images to create containers and also push these containers to container regestries such as DockerHub, Quay.io and so on.

In simple words, you can understand as `containerization is a concept or technology` and `Docker Implements Containerization`.

### Docker Architecture ?
![image](https://github.com/user-attachments/assets/bf4d1895-50ee-43bc-b0fc-6a9714a5db42)

The above picture, clearly indicates that Docker Deamon is brain of Docker. If Docker Deamon is killed, stops working for some reasons, Docker is brain dead :p (sarcasm intended).

### Docker LifeCycle 
![image](https://github.com/user-attachments/assets/2eb7a27a-ddd3-4cd4-be58-f1e8a416d8ec)

We can use the above Image as reference to understand the lifecycle of Docker.

There are three important things,

1. docker build -> builds docker images from Dockerfile
2. docker run   -> runs container from docker images
3. docker push  -> push the container image to public/private regestries to share the docker images.
