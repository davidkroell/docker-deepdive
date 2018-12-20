# Docker deep-dive
Presentation about Docker.
Each snippet can be executed in a free [Play with Docker](https://labs.play-with-docker.com/) instance.

## Images
### Exploring Images with Docker Toolset
```bash
df
# Output:
# Filesystem     1K-blocks     Used Available Use% Mounted on
# overlay        318111924 76532844 225400856  26% /var/lib/docker/overlay2/5570076c75...345/merged

# change into mount path
cd /var/lib/docker/overlay2/5570076c75...345/merged

ls
# notice, that this is an os and boot directory is empty or missing
```

### Exploring Docker Images with Dive
```bash
docker pull wagoodman/dive # download image
docker inspect wagoodman/dive # show info

docker pull bitnami/laravel:5 # get Larvel image

# exmplore image with dive
docker run --rm -it \
    -v /var/run/docker.sock:/var/run/docker.sock \
    wagoodman/dive:latest bitnami/laravel:5
```

## Containers
### Run a container
```bash
# mongodb
docker run mongo

# advanced mysql deployment
docker run --name mysql57 –d \
	--restart=always
	–p 127.0.0.1:3306:3306 \
	-v mysql:/var/run/mysql \
	-e MYSQL_ROOT_PASSWORD=my-secret-pw
	mysql:5.7
```

Use Dockers JSON API
```bash
curl --unix /var/run/docker.sock http:80/containers/json
```
Access Docker daemon from windows. Requires local docker client executable in path with at least Docker 18.09 on client and server.
```bat
docker -H ssh://user@host ps
# or for advanced use
set DOCKER_HOST=ssh://user@host
docker ps
```

### Build Docker Image

Build a Docker Image
```bash
git clone https://github.com/ironarachne/namegen # get code

cd namegen # change in code dir
git checkout 2a28fd8 # check out working code

# build image
docker build -t me/namegen .

# use image
docker run me/namegen

# with parameters
docker run me/namegen -o korean -n 10 -m firstname
```

## Networking and Storage
Docker networks and volumes
```bash
docker network ls

docker volume ls
```

## docker-compose
Docker Compose
```bash
# install compose
curl -sSL https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` \
  -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

# TODO
# deploy wordpress service
docker-compose -f wordpress-compose.yml up
```

## Docker Swarm
Start the Docker Swarm Visualizer 
```bash
docker service create \
  --name=viz \
  --publish=8080:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer
```

Deploy Hello world in Docker Swarm
```bash
docker service create \
  --name=hello \
  -p 8000:80 \
  tutum/hello-world
```

Check availability of Hello world
```bash
while true; do
curl -s <URL> | grep "My hostname"
sleep 0.2;
done
```

Scale Hello world service
```bash
docker service scale hello=3
```

Update the service
```bash
# set update policy
docker service update -d --update-order start-first hello

docker service update \
  --image jwilder/whoami \
  --publish-rm 80 \
  --publish-add 8000:8000 hello
```

Deploy the same Wordpress as earlier using Docker Swarm
```bash
docker stack deploy --compose-file wordpress-compose.yml wordpress
```

## Monitoring
Monitor Docker Containers
```bash
docker container stats
```
