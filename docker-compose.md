# Docker Compose

Container orchestration tool for building applications with microservices architecture using declarative .yaml configuration files

### Run containers

<code>docker compose up</code> - build and run services defined in the local docker-compose.yml file</br>
<code>docker compose up -d</code> - build and run services in detached mode</br>

### Stop/restart containers

<code>docker compose stop</code> - stops all Compose app containers without deleting them</br>
<code>docker compose restart</code> - restarts all stopped containers</br>

### Tear down

<code>docker compose rm </code> - delete containers and volumes</br>
<code>docker compose down</code> - delete containers and volumes</br>
<code>docker compose down --rmi local -v</code> - same as above and clean up images and volumes</br>

### Container data

<code>docker compose ps -a</code> - list all containers created by <code>docker compose up</code></br>
<code>docker compose top</code> - list all processes running inside each service</br>

### Run commands

<code>docker compose exec [service] [command]</code> - execute the given [command] on the [service] container</br>

#### Examples

<code>docker compose exec web python manage.py create_db</code></br>
<code>docker compose exec db psql --username=db_admin --dbname=flask_test</code></br>
