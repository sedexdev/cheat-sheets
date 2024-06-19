# Docker Stacks

Compose files for Docker Swarm service and container orchestration

### Deployment

<code>docker stack deploy -c [file] [name]</code> - deploy a Stack configuration stored in [file] called [name]</br>

### Stack data

<code>docker stack ls</code> - view existing stacks</br>
<code>docker stack ps [name]</code> - view services running on stack called [name]</br>
<code>docker stack services [name]</code> - similar output to <code>docker services ls</code></br>

# Secrets

Secure secret storage built into Docker Swarm (usernames/passwords/TLS certs/SSH keys/API keys etc.)

### Create a secret

<code>docker secret create [file | arg]</code> - create a secret stored in the RAFT database using a [file] or command line [arg]</br>

#### Examples

<code>docker secret create username username.txt</code> - create a secret stored in the RAFT database using a file</br>
<code>echo "userpass123" | docker secret create password -</code> - create a secret stored in the RAFT database using a command line [arg]</br>

### View secret data

<code>docker secret inspect [name]</code> - view secret metadata (does not show the value)</br>

### Use a secret

<code>docker service create [OPTIONS] --secret [name] -e [var]=[path]</code> - pass containers secret [name] and set [var] to value from [path]</br>

#### Example

Secrets are stored on the container in <code>/run/secrets</code></br>

<code>docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass postgres</code></br>
