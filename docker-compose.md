# Docker Compose

### Run containers

<code>docker compose up</code> - build and run services defined in the local docker-compose.yml file</br>

### Tear down

<code>docker compose down</code> - tear down services created by <code>docker compose up</code></br>
<code>docker compose down --rmi local -v</code> - same as above and clean up images and volumes</br>

### Container data

<code>docker compose ps -a</code> - list all containers created by <code>docker compose up</code></br>
