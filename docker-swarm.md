# Docker Swarm

Management solution for orchestrating distributed container workloads at scale

# Ports

<code>2377/tcp</code> - secure client-to-swarm communication</br>
<code>4789/udp</code> - control plane messaging</br>
<code>7946/tcp and udp</code> - for VXLAN overlay networks</br>

# Initialization

<code>docker swarm init</code> - activate Docker Swarm on current node</br>
<code>docker swarm init [OPTIONS] --advertise-addr [ip] --listen-addr [ip]</code> - set swarm node to advertise and listen on [ip]</br>
<code>docker swarm init [OPTIONS] --autolock</code> - automatically lock the swarm</br>

# Swarm commands

### View certificate

<code>docker swarm ca</code> - view and rotate CA key</br>

### Joining/leaving a swarm

<code>docker swarm join [host:port]</code> - join node to a swarm hosted on [host:port]</br>
<code>docker swarm join-token [worker | manager]</code> - displays join command to join swarm as either a [worker | manager]</br>
<code>docker swarm leave</code> - remove node from a swarm</br>
<code>docker swarm leave --force</code> - force remove a node from a swarm (e.g. Manager node)</br>

### Locking/unlocking a swarm

<code>docker swarm unlock</code> - unlock a swarm</br>
<code>docker swarm unlock-key</code> - manage the swarm unlock key</br>
<code>docker swarm update --autolock=true</code> - automatically lock the swarm</br>

### Updating a swarm

<code>docker swarm update [OPTIONS]</code> - update swarm configuration</br>

# Nodes

<code>docker node ls</code> - list Swarm nodes</br>
<code>docker node update --availability drain [manager]</code> - set a [manager] node to not accept worker tasks</br>

# Services

### Creating a service

<code>docker service create [image]</code> - create a service from [image]</br>
<code>docker service create [image] [command]</code> - create a service from [image] and run [command]</br>
<code>docker service create [OPTIONS] --name [name]</code> - create a service called [name]</br>
<code>docker service create [OPTIONS] -p [host:container]</code> - create a service publishing ports [host:container] on all containers</br>
<code>docker service create [OPTIONS] --network [name]</code> - create a service on a network called [name]</br>
<code>docker service create [OPTIONS] --replicas [num]</code> - create a service with [num] replicas</br>

### View services

<code>docker service ls</code> - list services</br>
<code>docker service ps [hash]</code> - list containers for the service identified by [hash]</br>

### Updating a service

<code>docker service update [hash] --replicas [num]</code> - updates the swarm service identified by [hash] to have [num] replicas</br>
<code>docker service update [image] --update-parallelism [count] --update-delay [secs]</code> - push new [image] to [count] containers every [secs] seconds</br>

### Scaling a service

<code>docker service scale [name]=[num]</code> - updates the swarm service identified by [name] to have [num] replicas</br>

### Deleting a service

<code>docker service rm [name | service_id]</code> - delete a service</br>

# Networking
 
<code>docker network create --drivers overlay [name]</code> - create a cross-node overlay network called [name]</br>
