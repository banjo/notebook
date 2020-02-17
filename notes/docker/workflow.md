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