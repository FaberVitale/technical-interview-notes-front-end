# Docker

## What's a container

A sandboxed process that runs on a machine isolated from all other processes of the host machine.
Containers are based on 2 linux features:

- control groups (cgroups) -> limit resource usage (CPU, memory, disk I/O, network, etc...) of a collection of processes. 
- namespaces -> limit process visibility to a collection of processes.

### Main container features

- is portable, can run on any OS.
- can run on physical or virtual machines.
- isolated from other containers and host processes.
- lightweight alternative to virtual machines.

## What's a container image

A blueprint of a container defined in a `Dockerfile`.
It contains all the data required at runtime by the container.
It can contain an executable file that is executed when running the container.

## Common cli commands

### docker run

Creates a docker container from an image and then spins it up.
docker run can thought as the sum of two other commands:

- docker create -> creates a container from an image.
- docker start -> starts stopped process.

### docker build

Creates an image given a context, DockerFile and optional `.dockerignore`.

### docker image

Subsets of all image

- docker image ls
- docker image rm
- docker image tag
- docker image prune

### docker ps

Lists containers

`-a` shows all containers active and non active, default shows only running containers.

### docker exec

runs a command on a running container.

### docker image

Lists images

`-a` shows all images, default hides intermediate images.

### docker tag

Adds tag (name:version) to an existing image. 

### docker kill

removes one or more containers
