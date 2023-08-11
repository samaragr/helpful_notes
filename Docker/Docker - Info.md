Type: #docker #general

- containers - only lives as long as the process is alive, will not just run an OS
- user access map ports from docker host to docker container for web access
- persist data - map a directory on host to container directory
- establish duplicate connection to docker host to detach
- Dockerfile - instruction/argument
- registry (dockerhub [docker.io] )- upload/pull images
- files stored under `/var/lib/docker`

## Docker engine

- Docker engine
	- Docker CLI - uses REST API to interact with docker daemon, does not need to be on same host as REST API and Daemon (-H)
	- REST API - used to interact with docker daemon
	- Docker Daemon - background process that manages docker objects images/containers/volumes/networks

## Docker networks

- default networks
	- Bridge - default network
	- none
	- host - conatiner here doesn't need port mapping as its on host network
- 