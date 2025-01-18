# Docker File

## What is a Dockerfile?
A Dockerfile is a script with a set of commands that are executed in sequence to create a Docker image. Each command in the Dockerfile creates a new layer in the image, making Docker images lightweight and efficient for reuse.

## Why Use Dockerfiles?
- **Automation:** Automate the process of building Docker images.
- **Reproducibility:** Ensure consistency across different environments.
- **Portability:** Share and deploy applications easily.
- **Customizability:** Tailor images to suit specific needs.

## Structure of a Dockerfile
A typical Dockerfile includes the following sections:

1. **Base Image**: Specifies the starting point for the image.
2. **Maintainer Information**: (Deprecated) Specifies the author of the Dockerfile.
3. **Environment Variables**: Defines variables for use in the image.
4. **Commands**: Instructions to modify the image or install software.
5. **Default Executable**: Specifies the command to run when a container starts.

---

## Dockerfile Instructions
Below are the common instructions used in Dockerfiles:

### 1. `FROM`
Specifies the base image to use.
```dockerfile
FROM ubuntu:20.04
```

### 2. `LABEL`
Adds metadata to the image.
```dockerfile
LABEL maintainer="you@example.com"
```

### 3. `RUN`
Executes commands in the shell during the build process.
```dockerfile
RUN apt-get update && apt-get install -y nginx
```

### 4. `CMD`
Specifies the default command to run in the container. Overridable.
```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

### 5. `ENTRYPOINT`
Specifies the default executable. Not easily overridable.
```dockerfile
ENTRYPOINT ["/bin/bash"]
```

### 6. `COPY`
Copies files from the local filesystem to the image.
```dockerfile
COPY index.html /usr/share/nginx/html/index.html
```

### 7. `ADD`
Similar to `COPY` but with extra features like automatic extraction of tar files.
```dockerfile
ADD app.tar.gz /app
```

### 8. `WORKDIR`
Sets the working directory for subsequent instructions.
```dockerfile
WORKDIR /app
```

### 9. `EXPOSE`
Documents the port(s) the container listens on.
```dockerfile
EXPOSE 80
```

### 10. `ENV`
Sets environment variables.
```dockerfile
ENV APP_ENV=production
```

### 11. `ARG`
Defines build-time variables.
```dockerfile
ARG VERSION=1.0
```

### 12. `VOLUME`
Defines mount points to store data outside the container.
```dockerfile
VOLUME ["/data"]
```

### 13. `USER`
Specifies the user for running commands.
```dockerfile
USER nonroot
```

### 14. `ONBUILD`
Defines instructions to execute when the image is used as a base for another build.
```dockerfile
ONBUILD RUN apt-get update
```

---

## Writing a Dockerfile
Here’s a simple example of a Dockerfile:

```dockerfile
# Use an official Python runtime as the base image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Make port 5000 available to the world outside the container
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]
```

---

## Best Practices for Writing Dockerfiles
1. **Use Multi-Stage Builds**: Minimize the final image size by separating build and runtime stages.
   ```dockerfile
   FROM golang:1.18 AS builder
   WORKDIR /app
   COPY . .
   RUN go build -o main .

   FROM alpine:latest
   WORKDIR /app
   COPY --from=builder /app/main .
   CMD ["./main"]
   ```

2. **Minimize Layers**: Combine related commands to reduce the number of layers.
   ```dockerfile
   RUN apt-get update && apt-get install -y \
       curl \
       git
   ```

3. **Use `.dockerignore`**: Exclude unnecessary files from the build context.
   ```
   node_modules
   .git
   *.log
   ```

4. **Pin Dependencies**: Use specific versions for reproducibility.
   ```dockerfile
   RUN pip install numpy==1.21.0
   ```

5. **Leverage Official Images**: Start with trusted base images.

---

## Debugging Dockerfiles
Use the following strategies to debug Dockerfile builds:

- **Intermediate Images**: Use `docker image ls` to view intermediate images and debug each layer.
- **Build with Verbose Output**: Add the `--progress=plain` flag when building.
  ```bash
  docker build --progress=plain -t myapp .
  ```
- **Interactive Shell**: Use `docker run -it` to debug running containers interactively.

