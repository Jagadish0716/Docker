## Comprehensive Guide to the docker run Command

The docker run command is one of the most frequently used commands in Docker. It is used to create and start a container from a specified Docker image. This document covers the basic usage, options, and advanced features of the docker run command.

#### Basic Syntax
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

IMAGE: The name of the Docker image to create the container from.

COMMAND: (Optional) Overrides the default command specified in the Docker image.

ARG: (Optional) Arguments passed to the COMMAND.

#### Example
```
docker run ubuntu echo "Hello, Docker!"
```
This command pulls the ubuntu image (if not already available locally), creates a container, and runs the echo "Hello, Docker!" command inside it.

### Key Options

#### 1. Detaching Containers
Run a container in the background and print its container ID.
```
docker run -d IMAGE
```

#### 2. Interactive Mode
Keep the container's standard input open and allocate a pseudo-TTY.
```
docker run -it IMAGE
```

#### 3. Port Mapping
Publish a container's port to the host.
```
docker run -p HOST_PORT:CONTAINER_PORT IMAGE
```

#### 4. Environment Variables
Set environment variables in the container.
```
docker run -e VAR_NAME=value IMAGE
```

#### 5. Mount Volumes
Mount host directories or volumes into the container.
```
docker run -v HOST_PATH:CONTAINER_PATH IMAGE
```

#### 6. Restart Policy
Set the restart policy for the container.
```
docker run --restart [no|always|unless-stopped|on-failure[:max-retries]] IMAGE
```

#### 7. Name the Container
Assign a name to the container.
```
docker run --name CONTAINER_NAME IMAGE
```

### Advanced Options

#### 1. Resource Constraints
Limit CPU Usage
Limits the container to use at most 2 CPUs.
```
docker run --cpus="2" IMAGE
```

Limit Memory Usage
Limits the container to use a maximum of 512 MB of memory.
```
docker run --memory="512m" IMAGE
```

#### 2. Networking Options
Use a Specific Network
```
docker run --network NETWORK_NAME IMAGE
```

Disable Networking
```
docker run --network none IMAGE
```

### 3. Health Checks
Specify a health check command and interval.
```
docker run --health-cmd="CMD" --health-interval=30s IMAGE
```

4. Security Options

Run as a Specific User

docker run --user UID:GID IMAGE

Limit Capabilities

docker run --cap-drop=ALL --cap-add=NET_ADMIN IMAGE

5. Custom DNS Servers

Set custom DNS servers for the container.

docker run --dns=8.8.8.8 IMAGE

6. Read-Only Filesystem

Make the container's filesystem read-only.

docker run --read-only IMAGE

7. Logging Options

Configure logging drivers and options.

docker run --log-driver=json-file --log-opt max-size=10m IMAGE

Example: Complex docker run Command

docker run \
  -d \
  -p 8080:80 \
  -e "ENV_VAR=production" \
  -v /host/data:/container/data \
  --cpus="2" \
  --memory="1g" \
  --restart=always \
  --name=my_container \
  my_image

This command:

Runs the container in detached mode.

Maps port 8080 on the host to port 80 in the container.

Sets an environment variable ENV_VAR to production.

Mounts /host/data to /container/data.

Limits the container to 2 CPUs and 1 GB of memory.

Restarts the container automatically on failure or reboot.

Names the container my_container.

Common Troubleshooting Tips

Image Not Found: Ensure the image name is correct or pull it manually using docker pull IMAGE.

Port Conflict: Verify that the host port is not already in use.

Permission Denied: Use sudo or ensure your user is part of the docker group.