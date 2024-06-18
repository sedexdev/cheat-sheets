# Docker Swarm

Management solution for orchestrating distributed container workloads at scale

# Ports

<code>2377/tcp</code> - secure client-to-swarm communication</br>
<code>4789/udp</code> - control plane messaging</br>
<code>7946/tcp and udp</code> - for VXLAN overlay networks</br>

### Initialize a node

<code>docker swarm init</code> - activate Docker Swarm on current node</br>
<code>docker swarm init --advertise-addr [ip] --listen-addr [ip]</code> - set swarm node to advertise and listen on [ip]</br>

### Swarm options

<code>docker swarm ca</code> - view and rotate CA key</br>
<code>docker swarm join [host:port]</code> - join node to a swarm hosted on [host:port]</br>
<code>docker swarm join-token [worker | manager]</code> - displays join command to join swarm as either a [worker | manager]</br>
<code>docker swarm leave</code> - remove node from a swarm</br>
<code>docker swarm leave --force</code> - force remove a node from a swarm (e.g. Manager node)</br>
<code>docker swarm unlock</code> - unlock a swarm</br>
<code>docker swarm unlock-key</code> - manage the swarm unlock key</br>
<code>docker swarm update [OPTIONS]</code> - update swarm configuration</br>

### Nodes

<code>docker node ls</code> - list Swarm nodes</br>

### Services

<code>docker service create [image]</code> - create a service from [image]</br>
<code>docker service create [image] [command]</code> - create a service from [image] and run [command]</br>
<code>docker service ls</code> - list services</br>
<code>docker service ps [hash]</code> - list service data for the service identified by [hash]</br>
<code>docker service update [hash] --replicas [num]</code> - updates the swarm service identified by [hash] to have [num] replicas</br>
<code>docker service rm [name | service_id]</code> - delete a service</br>
 