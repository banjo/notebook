# :whale: Docker workflow

## Basic actions

```bash
# stop all containers
> docker container stop $(docker container ls -aq)

# remove all containers
> docker container rm $(docker container ls -aq)
```

## Create docker image

This example is based on a Angular + ASP.NET Core application.

1. Create `Dockerfile` in the root directory.
2. Build the image

```bash
docker build . -t name:tag
```

-   `.`: means the current directory, as the `Dockerfile` is there.
-   `-t`: will add a tag to the image

3. Run a container based on the image

```bash
docker run -d -p 8090:80 name:tag
```

-   `-d`: means detached, so no interactiveness or code.
-   `-p`: specifies the port. Local port `8090` and `80` within the container.

## Save modified container as image

Download and use a container, modify it, and then save it like this.

1. Download the image you want to use.
2. Modify it
3. Commit the changes to a new image

```bash
docker commit <name-of-container> banjoanton/<new-name>:<tag>
```

4. Push to DockerHub

```bash
docker push banjoanton/<name-of-image>
```