docker

# Docker

## Containerization
> Packaging an application with its dependencies so that it can be run anywhere independently.
- runs the application in an isolated environment
- uses the shared operating system


Advantages:
- effeicency 
    - (vs VM) it uses the shared operating system more effeiciently
    - minimal boot time
- portability
- security - isolated
- continuity - a failure in one environmnet does not effect the other
- speed - a container is lightweight

Disadvantages vs VM:
- less secure
- no hardware storage separation
- difficulty of monitoring many concainers


## Docker Images
> Blueprint for a docker container.
- can be built on top of another
- one image per container, but can be multiple containers from the same image
- images can have versions
- 


### Dockerfile how to build

- begin with `FROM`


```bash
# the image you build from
FROM <image-name>
# several run commands
# to build a file for example
RUN
RUN

# copy files to container
COPY

# environment vairables
ENV

# expose ports
EXPOSE 8080


# command to start an app ONLY ONE
CMD java app.jar

```

## Docker commands

```bash
# List your images.
$ docker image ls

# Delete a specific image.
$ docker image rm [image name] 

# Delete all existing images.
$ docker image rm $(docker images -a -q)

# List all existing containers (running and not running).
$ docker ps -a 

# Stop a specific container.
$ docker stop [container name] 

# Stop all running containers.
$ docker stop $(docker ps -a -q) 

# Delete a specific container (only if stopped).
$ docker rm [container name]

# Delete all containers (only if stopped).
$ docker rm $(docker ps -a -q) 

# Display logs of a container.
$ docker logs [container name] 

# Start a container:
$ docker start [CONTAINER] 

# Stop a running container:
$ docker stop [CONTAINER] Stop a running container and start it up again:
$ docker restart [CONTAINER]

```