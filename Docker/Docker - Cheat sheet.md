Type: #docker #cheatsheet #commands

- [[Docker - Docker compose]] - to run multi container applications
- [[Docker - Dockerfile]] - to build image

## Docker commands
#commands #docker
- `docker run` - start a container
	- `-d` - run in background mode
	- `--name <container> <image>` - assign a name to container
	- `image:<tag>` - latest is default
	- `-i` - interactive 
	- `-t` - pseudo terminal
	- `-p 80:5000 <conatiner>` - map host port 80 to container port 5000 (listening port)
	- `-v /parent/datadir:/var/lib/container <container>` - map host directory to container directory to persist data
	- `-e <ENV_VAR=value>` - set environment variable for container
	- `--expose=<portnumber>` - expose a port
	- `--link <conatiner>:<host>`
	- `--mount` - mount volume
	- `--restart` - set restart policy (no, always, on-failure, unless-stopped )
	- `--network=<network-name>` - specify [[Docker - Info#Docker networks|network]]
- `docker ps` - list all current containers
	- `-a` - list all running and not
- `docker rm ` - remove container permanently
- `docker images` - list images and sizes
- `docker image`
	- `ls` - list images
	- `prune -a` - remove all local images without associated containers
- `docker rmi` - delete image, must have no running containers 
- `docker pull` - pull image and not run container
- `docker attach <container id>` - attach back to container
- `docker stop <conatiner>` - stop container
	- `ctrl` + `c` - stop container from within
- `docker rm $(docker ps -aq)` - remove all containers
- `docker inspect <container>` - find details on container
	- `docker image inspect <image>`
	- `docker run <image-name> cat /etc/*release*` - image metadata
- `docker logs <conatainer>` - stdout 
- `docker build .` - build docker image 
	- `-t` - add a tag (<acct name/app name>)
- `docker push` - push to dockerhub
- `docker login` - login to docker user acct
- `docker -H=<remote-docker-engine-ipaddress>:<port>` - used to connect CLI to remote docker engine
- `docker history <image id>` - see how image was built
- `docker system df` - disk consumption by images, containers and local volumes
	- `-v` - shows disk consumption by all images 
- `docker network` 
	- `create \` - create own network
		- `--driver <e.g. bridge>`
		- `--subnet <IP range>`
		- `--gateway <IP>` 
		- `<name>`
	- `ls` - list networks


