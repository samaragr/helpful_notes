Type: #docker #DockerCompose #inputFile

- https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.programonaut.com%2Fthe-most-important-docker-compose-properties%2F&psig=AOvVaw085LhsB0uV72TQNWd8Ppdf&ust=1691207724747000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCLD69u-NwoADFQAAAAAdAAAAABAE
- from v2 - network auto created for all containers in yaml so links not needed
- can create custom project name in command line

## Structure

- `services:` - 
	- `<container>:`
- `networks:` - 
	- `network:`
- `volumes:` - 
	- `volume:`

## Property types
- value
	- `key: value`
- array
	- `key:`
		- `- value`
- dictionary
	- `master:`
		- `key: value`

## Properties
- `build: <./dockerfile>` -  replace "`image:`" with build if image not yet built
- `image: <image-name>` - define image name
- `container_name: <container-name>` - define container name
- `volumes:` - define container volumes to persist data
	- `- /path:/path` - 
- `command: <execute>` - override start command for the container 
- `environment:` - define env variables for the container
- `env_file:` - define an env file for the container to set and override env variables
- `restart:` - define restart rule
	- no, always, on-failure, unless-stopped
- `expose:` - define ports to expose only to other containers, 
	- `- "port no."` 
- `networks:` - define all networks for the container
	- `-network-name`  
- `ports:` - define ports to expose to other containers and host
	- `- "port no.:port no."`
- `network_mode:` - define network driver
	- host, bridge, none
- `depends_on:` - define build, start and stop order of container
	- `- <container-name>` - 

## Formatting 
- double space indent
### Version 1
```yaml
<container>:
image: # specify image
build: <./dockerfile> # replace image with build if image not yet built
ports:
  - <host>:<internal>
links:
  - <conatiner:host> # ==deprecated?== links container to container
```

### Version 2

```yaml
version: 2
services:
  <container>:
    image:
    ports:
      - <host>:<internal>
    depends_on:
networks:
volumes:
```

### Version 3

```yaml
version: 3
services:
  <container>:
    image:
    ports:
      - <host>:<internal>
    depends_on:
networks:
volumes:
```


