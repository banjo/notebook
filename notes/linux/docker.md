# Docker

## Install Docker

### Install Script
Script that is only recommended for testing.

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker banjo
```

### Repository
Read the updated way on the [official webiste](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository). 

## Cheat Sheet
An official cheat sheet from 2016: [here](https://www.docker.com/sites/default/files/Docker_CheatSheet_08.09.2016_0.pdf)

## Basic Docker Use

### Build and run
Build a image in the current directory and run it.
```bash
docker build -t friendlyhello .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyhello  # Run "friendlyhello" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
```

### Containers
How to handle containers.

```bash
docker container ls                                # List all running containers
docker container ls -a             # List all containers, even those not running
docker container stop <hash>           # Gracefully stop the specified container
docker container kill <hash>         # Force shutdown of the specified container
docker container rm <hash>        # Remove specified container from this machine
docker container rm $(docker container ls -a -q)         # Remove all containers
```

### Image
How to handle images.

```bash
docker image ls -a                             # List all images on this machine
docker image rm <image id>            # Remove specified image from this machine
docker image rm $(docker image ls -a -q)   # Remove all images from this machine
```
### Docker Hub
How to use Dockerhub. Tag and image, push it to the hub and run it from the cloud.

```bash
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
```

### Stacks and services
How to handle stacks and services.

`docker swarm init` must be run before deploying a stack.

```bash
docker stack ls                                            # List stacks or apps
docker stack deploy -c <composefile> <appname>  # Run the specified Compose file
docker service ls                 # List running services associated with an app
docker service ps <service>                  # List tasks associated with an app
docker inspect <task or container>                   # Inspect task or container
docker container ls -q                                      # List container IDs
docker stack rm <appname>                             # Tear down an application
docker swarm leave --force      # Take down a single node swarm from the manager
```
