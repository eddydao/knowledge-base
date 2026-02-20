#devops #docker
# Definition
- Docker is open platform
- provide the ability to package and run an application in a loosely **isolated** environment called **container**
- Containers are lightweight and contain everything that needed to run the application

## Use case
- For fast, consistent delivery of applications
- Responsive deployment and scaling
- running more workloads on the same hardware

## Docker architecture
- Use client-server architecture
- Docker clients communicate with Docker daemon ( building, running, distributing Docker containers)
- Docker client and daemon can be run on the same system or connect client to remote daemon
- The connection is RestAPI over UNIX sockets or network interface
- Docker compose (also a Docker client) lets you work with applications consisting of a set of containers

### Docker daemon
- daemon ( dockerd) listens for Docker API requests
- manages Docker object like images, containers, networks, volumes
- can communicate with other daemons to manage Docker services

### Docker client
- Client (docker) is the primary way of interact with Docker
- use Docker APi
- Can communicate with more than one daemon

### Docker desktop
- easy to install application for mac, windows, linux env
- includes daemon, client, compose, content trust, kubernetes, credential help

### Docker registries
- stores Docker images
- centralize location
- repository is a collection of related container images within a registry

### Docker object
#### Docker images
- **ready-only** template with instruction for creating a Docker container
- each instruction in a Dockerfile creates a layer in the image
- when rebuild the image, only those layers which have changed are rebuilt
- => advantages: lightweight, small, fast

#### Containers
- Self contained: every container has it needs to function with no reliance on any pre-installed dependencies on the host machine
- isolated
- independent
- portable

#### Docker compose
- allow to define and config all containers in a single YAML file
=> up and running all with single command





# Docker command
- Open Docker desktop from command `open -a Docker`
- Run an exist container: `docker start <container>`