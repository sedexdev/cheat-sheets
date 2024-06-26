# Docker

Container runtime for building, shipping, and deploying containerized applications

# Information

<code>docker version</code> - displays the client and server version information</br>
<code>docker info</code> - detailed info on your current docker configuration</br>

# Help

<code>docker</code> - shows all commands and management commands</br>
<code>docker [command] --help</code> - shows usage and all subcommands for [command]</br>

# Login/Logout

<code>docker login</code> - logs you into Docker Hub via the terminal</br>
<code>docker logout</code> - removes auth token for DockerHub</br>

# List resources

<code>docker container ls</code> - list containers</br>
<code>docker image ls</code> - list images</br>
<code>docker volume ls</code> - list volumes</br>
<code>docker network ls</code> - list networks</br>

# View Docker running and stopped containers

<code>docker ps</code> - list running containers</br>
<code>docker ps -a</code> - list running and stopped containers</br>

# Containers

### Run a container

<code>docker container run [image]</code> - runs a container from [image] (pulls if not found locally)</br>
<code>docker container run [image]:[version]</code> - runs a container from specific version of [image]</br>
<code>docker container run -d -p 8000:80 [image]</code> - runs a detached container from [image] and publish on local port 8000</br>
<code>docker container run -d -p 8000:80 --name [name] [image]</code> - same as above with custom [name]</br>
<code>docker container run -it [image] [shell]</code> - runs a container from [image] with an interactive [shell]</br>
<code>docker container run --rm [OPTIONS] [image]></code> - deletes the container automatically on exit</br>

### Stop a container

<code>docker container stop [name | container_id]</code> - stops the given container</br>

### Start a container

<code>docker container start [name | container_id]</code> - starts the given container</br>
<code>docker container start -ai [name | container_id] [shell]</code> - starts the given container with an interactive [shell]</br>

### Update a container

<code>docker container update [OPTIONS]</code> - updates resource allocations for running containers without killing them</br>

### Delete a container

<code>docker container rm [name | container_id]</code> - deletes the given container</br>
<code>docker container rm -f [name | container_id]</code> - forcefully deletes running containers __!!__</br>
<code>docker container rm <[name | container_id] ...></code> - deletes multiple containers</br>

### View container information

<code>docker container logs [name | container_id]</code> - shows logs for given container</br>
<code>docker container top [name | container_id]</code> - shows running processes for given container</br>
<code>docker container inspect [name | container_id]</code> - view container configuration</br>
<code>docker container stats</code> - displays performance metrics for all running containers</br>
<code>docker container stats [name | container_id]</code> - displays performance metrics for given container</br>
<code>docker container exec -it [name | container_id] [shell]</code> - opens an interactive [shell] on an running container</br>

# Container networking

### Network drivers

<code>bridge</code> - Default. Bridge networks allow containers on the same host to communicate</br>
<code>host</code> - Allow communication between a container and the Docker host, using the host's networking</br>
<code>overlay</code> - L2 cross-node communication for Docker daemons and Swarm services/containers</br>
<code>ipvlan</code> - Provides control over IPv4/6 addressing, L2 VLAN tagging, and IPvlan L3 routing for underlay network integration</br>
<code>macvlan</code> - Allows you to assign a MAC address to a container, making it appear as a physical device on your network</br>
<code>none</code> - Completely isolate a container from the host and other containers. Not available for Swarm services</br>

### View network information

<code>docker container port [name | container_id]</code> - show ports configured on the container</br>
<code>docker container inspect --format "{{ .NetworkSettings.IPAddress }}" [name | container_id]</code> - show container IP address</br>
<code>docker network inspect [name]</code> - show virtual network [name] configuration</br>

### Create a network

<code>docker network create [name]</code> - create new virtual network called [name]</br>

### Run new container on specific network

<code>docker container run [OPTIONS] --network [network] [image]</code> - runs a container attached to [network]</br>

### Connecting existing container to a network

<code>docker network connect [network] [name]</code> - connects container [name] to [network]</br>
<code>docker network disconnect [network] [name]</code> - disconnects container [name] from [network]</br>

### Network aliases

<code>docker container run [OPTIONS] --net [network] --net-alias [alias] [image]</code> - create a DNS [alias] to discover this container</br>

# Images

### Image data

<code>docker image history [image]:[tag]</code> - shows how data in the image has changed over time</br>
<code>docker image inspect [image]</code> - shows image metadata</br>

### Image tagging

<code>docker image tag [image]:[tag] [username]/[image]:[tag]</code> - change the tag of an existing image</br>

### Push/Pull Docker Hub

<code>docker image push [username]/[image]:[tag]</code> - push an image to Docker Hub</br>
<code>docker image pull [username]/[image]:[tag]</code> - pull an image from Docker Hub (omitting [tag] pulls 'latest')</br>

### Deleting images

<code>docker image rm [name | container_id ]</code> - deletes a specific image</br>
<code>docker rmi [name | container_id ]</code> - deletes a specific image</br>
<code>docker image prune</code> - cleans up dangling images</br>
<code>docker image prune -a</code> - cleans up all images not currently in use __!!__</br>

### Building images

<code>docker image build .</code> - builds a container based on 'Dockerfile' in the current directory</br>
<code>docker image build -f [file]</code> - builds a container based on a docker file called [file]</br>
<code>docker image build -t [name]:[tag] .</code> - builds a container with [name] and [tag] based on 'Dockerfile' in the current directory</br>

### Searching for images

<code>docker search [name]</code> - searches for images on Docker Hub using [name] (pattern matching is done against image name only)</br>

### Signing images

<code>docker trust key generate [name]</code> - generate a key pair called [name]</br>
<code>docker trust key load [pem] --name [name]</code> - load an existing [pem] file and call it [name]</br>
<code>docker trust signer add --key [key] [name] [image]</code> - create a signer for [image] from [key] called [name]</br>
<code>docker trust sign [image]</code> - sign [image] and push to DockerHub</br>

# System

<code>docker system prune</code> - cleans up everything not currently in use __!!__</br>
<code>docker system df</code> - displays disk usage</br>

# Persistance

<code>docker container run [OPTIONS] -v [name]:[location] [image]</code> - runs a container with a named volume at [location]</br>
<code>docker container run [OPTIONS] -v [path]:[location] [image]</code> - mounts a local directory at [path] in [location]</br>
<code>docker container run [OPTIONS] --mount type=volume,src=[volume],target=[path] [image]></code> - mount a [volume] at [path]</br>
<code>docker container run [OPTIONS] --mount type=bind,src=[path1],target=[path2] [image]></code> - bind [path1] to [path2]</br>

# Multi-architecture images

<code>docker manifest inspect [image] | grep 'architecture\|os'></code> - show supported CPU architectures and OSs for an image</br>

# Local container registry

### Run the registry image

<code>docker container run -d -p 5000:5000 --name registry registry</code> - pull and run open-source registry container</br>

### Pull test image

<code>docker pull hello-world</code> - pull the hello-world test image</br>

### Tag as local and push to new registry

<code>docker tag hello-world 127.0.0.1:5000/hello-world</code> - update registry location of image</br>
<code>docker push 127.0.0.1:5000/hello-world</code> - push to local registry</br>

### Delete local image and pull from registry

<code>docker rmi hello-world</code> - remove hello-world image</br>
<code>docker rmi 127.0.0.1:5000/hello-world</code> - remove 127.0.0.1:5000/hello-world image</br>
<code>docker pull 127.0.0.1:5000/hello-world</code> - pull 127.0.0.1:5000/hello-world image</br>

### Bind mount volume for image storage

<code>docker container run [OPTIONS] -v $(pwd)/registry_data:/var/lib/registry registry</code> - bind local folder for storage</br>
